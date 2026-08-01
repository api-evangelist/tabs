# Tabs

Tabs ([tabs.com](https://www.tabs.com/)) is an AI-native revenue automation platform for B2B companies, covering the full contract-to-cash lifecycle: contract ingestion, billing, invoicing, collections, cash application, ASC 606 revenue recognition, and reporting.

This repository profiles the Tabs API surface for the API Evangelist network:

- **Tabs External API (v3)** — 93 operations over customers, contracts, obligations, billing terms, performance obligations, invoices, payments, credit memos, products, commitments, renewals, revenue, and reports at `integrators.prod.api.tabsplatform.com` ([docs](https://docs.tabsplatform.com/)). OpenAPI in [openapi/](openapi/).
- **Tabs Usage API (Beta)** — high-throughput usage-event ingestion with required UUIDv4 idempotency keys (45-day dedup), 10,000 requests/minute per merchant, at `usage-events.prod.api.tabsplatform.com`.
- **Tabs MCP Server** — official read-only remote MCP server at `https://integrators.prod.api.tabsplatform.com/mcp` (OAuth 2.0 via login.tabs.com, 25+ tools over the "Commercial Graph"). See [mcp/tabs-mcp.yml](mcp/tabs-mcp.yml).

The machine-readable index is [apis.yml](apis.yml) (APIs.json). Supporting artifacts: authentication, conventions (pagination/filtering/idempotency), error catalog, rate limits, lifecycle/SLA, data model, conformance, trust center, domain security, well-known discovery documents, llms.txt, agent skills, and OpenAPI overlays.

Backed by: General Catalyst, Lightspeed Venture Partners.
