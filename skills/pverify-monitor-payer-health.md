---
name: Monitor payer health before spending pVerify transactions
description: Use pVerify's payer list, live payer status and rejection statistics to avoid burning billable transactions against a payer that is down, and to triage a spike in rejections.
api: openapi/pverify-payers-api-openapi.yml
operations: [getAllPayers, getPayerStatus, getPayerStatusStatistics, getPendingInquiries]
generated: '2026-08-15'
method: generated
source: openapi/pverify-payers-api-openapi.yml + lifecycle/pverify-lifecycle.yml
---

# Monitor payer health

pVerify bills per transaction and payers go down independently of pVerify. This skill is the
cheapest failure-avoidance loop available on this API — and one of its operations needs no
credentials at all.

## 1. Load the payer catalog — `getAllPayers`

`GET /API/GetAllPayers` (bearer token + `Client-API-Id`) returns every payer pVerify supports,
with the `payerCode` values you send on every inquiry. Cache this; it changes slowly.

Products are not uniformly supported across payers — Claim Status in particular is unavailable for
many. Check the catalog before assuming a payer supports a product.

## 2. Check live status — `getPayerStatus`

`GET /api/GetPayerStatus`. **pVerify documents this call as requiring no authentication.** It
returns per-payer state: `Payer Up`, `Payer Active`, `Payer Inactive`, `Payer Down`.

Gate every inquiry on this. Submitting against a `Payer Down` payer returns `APIResponseCode 1`
(Rejected) and still consumes a billable transaction.

## 3. Triage a rejection spike — `getPayerStatusStatistics`

`GET /API/GetPayerStatusStatistics?status=Rejected&checkForLastNumberOfHours=1` returns payers
that have been failing recently.

When your rejection rate jumps, check this before opening a ticket — the cause is usually a payer
outage, not your request. pVerify's own uptime dashboard is at
`https://status.dosespot.com/posts/dashboard` (operated by its parent, DoseSpot / Interra Health)
and covers the pVerify platform, not the payers.

## 4. Reconcile stranded work — `getPendingInquiries`

`GET /API/GetPendingInquiries?DOS=MM-DD-YYYY` lists inquiries still pending for a date of service.
Use it after an outage to find transactions you already paid for instead of resubmitting them.
The `DOS` parameter uses **dashes** (`MM-DD-YYYY`), unlike the `MM/dd/yyyy` dates in request bodies.

## Why this matters here specifically

pVerify publishes no rate limits, no rate-limit response headers and no retry-safety contract
(`conventions/pverify-conventions.yml`). Payer status is the only real-time health signal in the
API, and it is free to call.
