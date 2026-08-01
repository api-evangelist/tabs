---
name: Pull revenue recognition and reporting data from Tabs
description: >-
  Read ASC 606 performance obligations, recognized revenue, ARR, and cash
  forecasting data from Tabs for dashboards and month-end close.
api: openapi/tabs-external-api-openapi.yml
operations:
  - IntegratorsApiPerformanceObligationsController_searchPerformanceObligations
  - IntegratorsApiContractsv3Controller_getPerformanceObligationsWithRevenue
  - IntegratorsApiPerformanceObligationsController_upsertRecognizedRevenue
  - IntegratorsAPIRevenueV31Controller_getRevenues
  - IntegratorsApiReportsController_getARR
  - IntegratorsApiReportsController_getReport
  - IntegratorsApiMerchantsControllerV3_getBookCloseDate
generated: '2026-07-21'
method: generated
---

# Pull revenue recognition and reporting data

Base URL: `https://integrators.prod.api.tabsplatform.com`; header
`Authorization: <API_KEY>`.

1. **Check the books** — `IntegratorsApiMerchantsControllerV3_getBookCloseDate`
   to know the closed period before writing any revenue data.
2. **Performance obligations** —
   `IntegratorsApiPerformanceObligationsController_searchPerformanceObligations`
   across the merchant, or
   `IntegratorsApiContractsv3Controller_getPerformanceObligationsWithRevenue`
   for one contract's POBs with revenue schedules.
3. **Recognized revenue** — read with
   `IntegratorsAPIRevenueV31Controller_getRevenues`; post manual adjustments
   with `IntegratorsApiPerformanceObligationsController_upsertRecognizedRevenue`
   (only for open periods).
4. **Reports** — `IntegratorsApiReportsController_getARR` for ARR;
   `IntegratorsApiReportsController_getReport` for the paginated cash
   forecasting report (due and paid amounts per period per customer).

## Rules

- All list endpoints paginate with `page`/`limit` and wrap results in
  `{ success, payload }`.
- Never upsert recognized revenue into a closed period — compare against the
  book close date first.
- Custom revenue schedules on obligations belong to
  `IntegratorsApiContractsv3Controller_upsertCustomRevenue`, not the
  recognized-revenue endpoint.
