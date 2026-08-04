# Tabs

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
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Tabs ([tabs.com](https://www.tabs.com/)) is an AI-native revenue automation platform for B2B companies, covering the full contract-to-cash lifecycle: contract ingestion, billing, invoicing, collections, cash application, ASC 606 revenue recognition, and reporting.

This repository profiles the Tabs API surface for the API Evangelist network:

- **Tabs External API (v3)** — 93 operations over customers, contracts, obligations, billing terms, performance obligations, invoices, payments, credit memos, products, commitments, renewals, revenue, and reports at `integrators.prod.api.tabsplatform.com` ([docs](https://docs.tabsplatform.com/)). OpenAPI in [openapi/](openapi/).
- **Tabs Usage API (Beta)** — high-throughput usage-event ingestion with required UUIDv4 idempotency keys (45-day dedup), 10,000 requests/minute per merchant, at `usage-events.prod.api.tabsplatform.com`.
- **Tabs MCP Server** — official read-only remote MCP server at `https://integrators.prod.api.tabsplatform.com/mcp` (OAuth 2.0 via login.tabs.com, 25+ tools over the "Commercial Graph"). See [mcp/tabs-mcp.yml](mcp/tabs-mcp.yml).

The machine-readable index is [apis.yml](apis.yml) (APIs.json). Supporting artifacts: authentication, conventions (pagination/filtering/idempotency), error catalog, rate limits, lifecycle/SLA, data model, conformance, trust center, domain security, well-known discovery documents, llms.txt, agent skills, and OpenAPI overlays.

Backed by: General Catalyst, Lightspeed Venture Partners.
