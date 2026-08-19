---
name: Operate Amperity safely over MCP
description: Connect to Amperity's hosted MCP server and drive its 227 tools without writing to a production tenant by accident.
api: mcp/amperity-mcp.yml
operations: [session_start, tenant_list, tenant_info, tenant_use, safety_get_mode, safety_set_mode]
---

# Operate Amperity safely over MCP

Amperity hosts a remote MCP server at **`https://mcp.amperity.com`**. One public URL; it routes each
request to the stack holding the calling user's tenant. It is not installed locally.

Connect with `claude mcp add --transport http --scope user amperity https://mcp.amperity.com`, or add
it as a remote connector in Claude.ai / ChatGPT / Copilot Studio. Auth is OAuth2 authorization-code
with PKCE (`S256`); the first tool call opens a browser tab.

**This surface is far wider than the REST API.** The published OpenAPI has 10 operations. The MCP
server has 227 tools, and it reaches things REST cannot touch at all: databases, core tables, Stitch
identity resolution, couriers, feeds, destinations, orchestrations, journeys, predictions and Spark.
Amperity's own docs say MCP "does not replace the Amperity REST API" — use REST for non-agent
integrations. See `mcp/amperity-tool-crosswalk.yml`.

## Steps

1. **Start the session** — call `session_start` first on a hosted multi-user client; it mints the
   session token.
2. **Know where you are** — `tenant_list` then `tenant_info`. Session state (selected tenant + safety
   mode) is per-token and persists for the session. Switch with `tenant_use`.
3. **Check the guardrail before any write** — `safety_get_mode`. New sessions default to **`strict`**:
   writes to a **production** tenant are blocked, reads are allowed, and reads *and writes* against a
   **sandbox** tenant are allowed. Strict mode is a real sandbox-only execution mode — do meaningful
   work in it.
4. **Escalate deliberately, never reflexively** — `safety_set_mode`:
   - `strict` (default) — production is read-only
   - `confirm` — production writes require an explicit `confirm: true` argument per call
   - `unrestricted` — everything runs with no confirmation
   Prefer `confirm` for routine production work; it surfaces each change for human review.
5. **Expect three tools to refuse anyway** — `campaign_schedule`, `courier_group_run` and
   `orchestration_group_run` **always** require mode `unrestricted` **and** `confirm: true`. Missing
   either and the call is not allowed. These push data to systems outside Amperity.
6. **Use exact IDs on mutations** — the admin tools take the `user_id` / `policy_id` returned by a
   list or create call, not a display name or an email. List first.

## Know the blast radius

- `user_delete` is a **hard, global, irreversible** deletion. It must run from the parent tenant with
  `confirm=true`, and it does not detach tenant policies first. For reversible access removal use
  `user_revoke_policy`.
- `user_revoke_policy` removes **one direct attachment only** — it does not remove access inherited
  from a group mapping.
- **Safety mode is a guardrail, not a permission boundary.** The agent itself can call
  `safety_set_mode`. The real boundary is the tool permissions set in the MCP client plus the calling
  user's Amperity policies.
- Tool results may include **PII**. Amperity holds you responsible for whether the connected model is
  approved to handle it.
- Tools that do work consume **amps** (Amperity usage credits), the same as running that operation in
  the UI. LLM tokens are billed by your own AI platform, never by Amperity.

## Discover the real contract

The tool reference at `https://docs.amperity.com/api/mcp_tool_reference.html` is a grouped list of
names. **`tools/list` is the authority** — it returns the exact tool surface your account is
authorized to call, with input schemas. Call it on connect; do not hardcode this repo's list.
