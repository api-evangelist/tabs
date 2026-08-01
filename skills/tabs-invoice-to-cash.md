---
name: Work an invoice from issue to cash in Tabs
description: >-
  Retrieve invoices, deliver them, record payments, and apply credit memos so
  receivables reconcile in Tabs and the connected ERP.
api: openapi/tabs-external-api-openapi.yml
operations:
  - IntegratorsApiInvoicesController_getInvoices
  - IntegratorsApiCustomersController_getInvoice
  - IntegratorsApiCustomersController_getInvoiceAsPdf
  - IntegratorsApiCustomersController_invoiceActions
  - IntegratorsApiCustomersController_createPayment
  - IntegratorsApiCustomersController_getPayment
  - IntegratorsApiCreditMemosController_createCreditMemo
  - IntegratorsApiCreditMemosController_applyCreditMemo
generated: '2026-07-21'
method: generated
---

# Work an invoice from issue to cash

Base URL: `https://integrators.prod.api.tabsplatform.com`; header
`Authorization: <API_KEY>`.

1. **Find invoices** — `IntegratorsApiInvoicesController_getInvoices`
   (`GET /v3/invoices`) with filters such as
   `filter=status:eq:"PENDING",total:gt:"500"`; paginate with `page`/`limit`.
2. **Inspect one invoice** — `IntegratorsApiCustomersController_getInvoice`;
   render or archive it via `IntegratorsApiCustomersController_getInvoiceAsPdf`.
3. **Act on the invoice** — `IntegratorsApiCustomersController_invoiceActions`
   performs state transitions; update the PO or memo first with
   `IntegratorsApiCustomersController_updateInvoicePO` /
   `IntegratorsApiCustomersController_updateInvoiceMemo` when needed.
4. **Record payment** — `IntegratorsApiCustomersController_createPayment`
   against the invoice; verify with
   `IntegratorsApiCustomersController_getPayment`. Payments settle
   invoices — most arrive from the connected bank, so check for an existing
   payment before creating one manually.
5. **Handle credits** — `IntegratorsApiCreditMemosController_createCreditMemo`
   then `IntegratorsApiCreditMemosController_applyCreditMemo` to apply it to
   the invoice; list per-invoice credits with
   `IntegratorsApiCustomersController_getCreditMemosByInvoice`.

## Rules

- Responses use the `{ success, payload }` envelope; list payloads carry
  `currentPage`/`limit`/`totalItems`.
- 404 means a wrong invoice/customer id; 409 indicates a conflicting action —
  re-read the invoice state before retrying.
- Customers with `autoCharge: true` and a default payment method are charged
  automatically; do not double-record payments for them.
