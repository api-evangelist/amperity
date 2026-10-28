# Amperity

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Amperity is a Seattle-based customer data platform (CDP) that helps consumer brands build accurate, unified customer profiles by stitching together fragmented first-party data from across their systems. Using AI-powered identity resolution (its patented Stitch technology), Amperity assembles a durable Customer 360 that powers segmentation, marketing campaigns, personalization, analytics, and activation to downstream destinations. For developers, Amperity exposes three public REST APIs: the Amperity API for programmatic access to tenant resources (campaigns, segments, ingest jobs, audit events, and workflow runs), the Profile API for real-time access to unified customer profiles by index, and the Streaming API for low-latency, high-throughput ingestion of events from external systems. Amperity publishes a downloadable OpenAPI 3.0.3 document for the Amperity API plus a separate unstable preview spec, and it hosts an official remote Model Context Protocol server at mcp.amperity.com exposing more than 200 tools across databases, queries, Stitch identity resolution, couriers, destinations, campaigns, journeys and predictive models, gated by OAuth2 authorization-code with PKCE and per-session safety modes. The REST APIs use OAuth2 client-credentials tokens (JWT bearer), cursor pagination, date-based versioning via an api-version header, and an RFC 8594 deprecation/sunset policy. Amperity serves retail, travel, hospitality, financial services, and other consumer-facing verticals.

**Areas:** Company · Enterprise · Customer Data Platform · CDP · Identity Resolution · Customer 360 · Marketing · Data · Profiles · Analytics · MCP · Agents

## Amperity on APIs.io

Everything profiled for Amperity is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/amperity/](https://apis.io/providers/amperity/)** — or go straight to one of the APIs or properties below.

### APIs (8)

- [Amperity MCP Server](https://apis.io/apis/amperity/amperity-mcp-server/) — Amperity's official hosted remote Model Context Protocol server. A single public endpoint at https://mcp.amperity.com routes each request to the Amperity…
- [Amperity Profile API](https://apis.io/apis/amperity/amperity-profile-api/) — RESTful API for real-time access to unified customer profiles. List indexes, fetch an index, and read paginated customer profiles (or a single profile) for…
- [Amperity Streaming API](https://apis.io/apis/amperity/amperity-streaming-api/) — Low-latency, high-throughput REST API for real-time ingestion of event data from external systems into Amperity. POST JSON or XML payloads (up to 1 MB) to a…
- [Amperity Audit Events API](https://apis.io/apis/amperity/amperity-audit-events-api/) — Return records for user activity that occurred in your tenant.
- [Amperity Campaigns API](https://apis.io/apis/amperity/amperity-campaigns-api/) — Return information about campaigns and campaign drafts.
- [Amperity Ingest API](https://apis.io/apis/amperity/amperity-ingest-api/) — Return details about ingest jobs.
- [Amperity Segments API](https://apis.io/apis/amperity/amperity-segments-api/) — Return a list of segments available in your tenant.
- [Amperity Workflow API](https://apis.io/apis/amperity/amperity-workflow-api/) — List, run, and stop workflows.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Amperity Webhooks](https://apis.io/asyncapis/amperity/amperity-webhooks/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [amperity](https://apis.io/servers/amperity/amperity/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Amperity Agentic Access](https://apis.io/agentic-access/amperity/amperity-agentic-access/)

#### Collections (2)

Postman and Open Collection request collections.

- [Amperity API](https://apis.io/collections/amperity/open-amperity-control-plane-2024-04-01/)
- [Amperity API (Unstable)](https://apis.io/collections/amperity/open-amperity-control-plane-unstable/)

#### Overlays (1)

OpenAPI overlays, including conversational phrasing for each operation.

- [Amperity Control Plane Overlay](https://apis.io/overlays/amperity/amperity-control-plane-overlay/)

#### Security (3)

Authentication, trust centre, and vulnerability disclosure.

- [Amperity Authentication](https://apis.io/security/amperity/amperity-authentication/)
- [Amperity Domain Security](https://apis.io/security/amperity/amperity-domain-security/)
- [Amperity Trust Center](https://apis.io/security/amperity/amperity-trust-center/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Amperity Plans Pricing](https://apis.io/plans/amperity/amperity-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Amperity Rate Limits](https://apis.io/rate-limits/amperity/amperity-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.amperity.com)
- [Documentation](https://docs.amperity.com)
- [Getting started](https://docs.amperity.com/api/overview.html)
- [API reference](https://docs.amperity.com/reference/api.html)
- [Blog](https://amperity.com/blog)
- [Compliance](https://trust.amperity.com/)
- [GitHub](https://github.com/amperity)
- [Status](https://status.amperity.com)

## API Evangelist rating

**Kin Score 50.0** — developing · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 73.2 |
| Contract quality | 58.7 |
| Contract governance | 18.2 |
| Operational transparency | 81.6 |
| Developer ergonomics | 58.9 |
| Access clarity | 15.8 |

**Agent readiness 47.1** — agent-ready (gated down from agent-native)

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | — |
| MCP Server | — |
| Auth Clarity | served (partial credit) |
| Idempotency | — |
| Error Semantics | documented (partial credit) |
| OpenAPI Examples | — |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | yes |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | served (partial credit) |
| Protected Resource Metadata | verified |
| Dynamic Client Registration | yes |
| Agentic Commerce | — |
| Pagination Ratio | paginated |
| Operation Distinctiveness | distinct |

**Regulatory alignment 21.6** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/amperity/](https://apis.io/providers/amperity/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Amperity: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/amperity/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
