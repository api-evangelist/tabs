---
name: Ingest usage events into Tabs idempotently
description: >-
  Stream usage events into the Tabs Usage API (Beta) with correct idempotency,
  validation, and retry behavior so usage-based invoices stay accurate.
api: openapi/tabs-usage-api-beta-openapi.yml
operations:
  - ingestEvent
  - getEvents
  - deleteEvent
generated: '2026-07-21'
method: generated
---

# Ingest usage events idempotently

Base URL: `https://usage-events.prod.api.tabsplatform.com`; header
`Authorization: <API_KEY>`. Beta access is enabled per merchant by a Tabs
account manager. Event types and usage-based obligations must exist first
(via the Tabs UI or the External API events endpoints).

1. **Submit an event** — `ingestEvent` (`POST /v1/events`) with `customerId`
   (UUIDv4), `eventTypeId`, `datetime` (ISO-8601 UTC), `value`, and a fresh
   UUIDv4 `idempotencyKey`. Optional: `differentiator` (splits line items),
   `invoiceSplitKey` (splits invoices), `metadata`.
2. **Verify ingestion** — `getEvents` (`GET /v1/events`) with date filters,
   e.g. `filter=datetime:gte:"2026-07-01",datetime:lt:"2026-08-01"`.
3. **Correct a mistake** — `deleteEvent`
   (`DELETE /v1/events/{idempotencyKey}`) creates a deletion event linked to
   the original through `parentEventId`; never mutate events in place.

## Rules

- **Idempotency is mandatory**: one UUIDv4 per event; the
  `(manufacturerId, idempotencyKey)` pair deduplicates for 45 days. A reused
  key returns 400; concurrent duplicates return 409.
- **Retry only on 503/429/network errors.** 200 is returned only after a
  durable write, so a timeout without response is safe to retry with the SAME
  idempotency key.
- **Respect the rate limit**: 10,000 requests/minute per merchant (fixed
  60-second window); on 429 wait the `retryAfter` seconds.
- Invoices refresh hourly with a 1-hour look-back; events older than 1 hour or
  future-dated will not be picked up by that job.
- Send events chronologically when order matters.
