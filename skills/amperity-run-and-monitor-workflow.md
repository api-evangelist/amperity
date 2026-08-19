---
name: Run and monitor an Amperity workflow
description: Start a courier group, orchestration group or campaign through the Amperity API and poll it to completion, handling the fact that the start call is not idempotent.
api: openapi/amperity-control-plane-2024-04-01-openapi.json
operations: [run-workflow, get-workflow, list-workflows, stop-workflow]
---

# Run and monitor an Amperity workflow

`POST /workflow/runs` is Amperity's generic runner. The same operation starts a courier group, an
orchestration group, or a campaign — which one is decided by the `config_id` you pass.

## Before you call

Every request needs three headers (`conventions/amperity-conventions.yml`):

- `Authorization: Bearer ${access-token}` — from the OAuth2 client-credentials exchange
- `Amperity-Tenant: {tenant-id}` — production and sandbox share a base URL, so **this header is the
  only thing separating a test run from a production run**
- `api-version: 2024-04-01` — required; an unsupported value returns `400`

Base URL is `https://app.amperity.com/api` on AWS, `https://{tenant-id}.amperity.com/api` on Azure.

## Steps

1. **Start the run** — `run-workflow` (`POST /workflow/runs`). Body is a `WorkflowRunRequest`:
   `config_id` (required — the courier group / orchestration group / campaign to run), plus optional
   `range_from`, `range_to` and `run_mode`. Returns `201` with a `Workflow`.
2. **Capture `id` from the response immediately, before doing anything else.** There is **no
   idempotency key on this endpoint**. If the call times out and you retry, you start the work twice.
   On a timeout do **not** retry — call `list-workflows` (`GET /workflow/runs`) and look for a run
   matching your `config_id` with a recent `created_at`, and only start a new one if there is none.
3. **Poll** — `get-workflow` (`GET /workflow/runs/{workflow-id}`) until `state` is terminal. The
   response carries `task_instances[]`, each a `WorkflowTaskInstance` with its own `state`,
   `created_at`, `ended_at` and `error`.
4. **Respect the rate limit while polling** — the Amperity API allows **10 requests per second**, and
   there are **no rate-limit response headers and no `Retry-After`**. Poll on a fixed backoff of your
   own; on `429`, back off and retry.
5. **Read failures from `error`** — both `Workflow` and `WorkflowTaskInstance` carry a `WorkflowError`
   with `type`, `message`, `attribution` and `data`. `attribution` is what tells you whose problem it
   is.
6. **Abort if needed** — `stop-workflow` (`POST /workflow/runs/{workflow-id}/stop`). Unlike starting,
   stopping is naturally idempotent — stopping an already-stopped workflow is safe to retry.

## Errors

`400` malformed or unsupported `api-version` · `401` no valid bearer token · `403` the API key lacks
the policy (e.g. DataGrid Operator) in that tenant · `404` unknown workflow id or wrong tenant ·
`429` rate limited · `500` retry with backoff.

The body is `{status, message}` — **not** RFC 9457. Amperity's docs also show `request_id` and
`trace_id` in the error body (the spec's `ErrorResponse` forbids them with
`additionalProperties: false`), so parse leniently and keep those two values: they are what Amperity
Support asks for. See `errors/amperity-problem-types.yml`.

## Do not

- Do not retry `POST /workflow/runs` blindly.
- Do not assume the sandbox has a different URL. It does not. Check the `Amperity-Tenant` value.
