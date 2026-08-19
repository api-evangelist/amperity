---
name: Paginate any Amperity list endpoint
description: Walk a complete result set from any Amperity API GET endpoint using the cursor contract, without re-reading pages or requesting expensive totals.
api: openapi/amperity-control-plane-2024-04-01-openapi.json
operations: [list-events, list-campaign, list-segment, list-ingest-jobs, list-workflows]
---

# Paginate any Amperity list endpoint

Every `GET` endpoint on the Amperity API uses one cursor contract, and every list response is the same
three-field envelope. Learn it once and it applies to audit events, campaigns, segments, ingest jobs
and workflow runs alike.

## Request parameters

| Parameter | In | Meaning |
|---|---|---|
| `limit` | query | Max records in one page |
| `next_token` | query | Opaque cursor. **Omit** it for the first page. It can never be `null`. |
| `with_total` | query | `true` to include a total count. Default `false`. |

## Response envelope

```json
{ "data": [ ... ], "next_token": "ZVEy1iwsKBs9a6H", "total": 1234 }
```

- `data` — the current page
- `next_token` — the cursor for the next call. **You have the last page when `next_token` is absent
  or empty.**
- `total` — returned only when you asked for it with `with_total=true`

## Steps

1. Call the list operation with `limit` and **no** `next_token`.
2. Process `data`.
3. If `next_token` is present and non-empty, call again with that exact value as `next_token`.
4. Stop when `next_token` is absent or empty. Do not stop on an empty `data` array alone.
5. Never construct or mutate a cursor — it is opaque.

## Cost and limits

- Do not set `with_total=true` on a routine walk. Amperity warns the total count is an **expensive
  operation** over a large result set. Ask for it once if a caller needs it, not on every page.
- The Amperity API allows **10 requests per second**, so a full walk of a large set is rate-bound.
  There are **no rate-limit headers** to read remaining budget from; on `429` back off and retry.
- The Profile API is a different budget: **2000 rps across the whole tenant, sandboxes included** — a
  heavy sandbox job eats production capacity.

## Headers

`Authorization: Bearer ${access-token}`, `Amperity-Tenant: {tenant-id}`, `api-version: 2024-04-01`.
All three are required on every page.
