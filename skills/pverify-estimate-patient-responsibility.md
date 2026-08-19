---
name: Estimate patient financial responsibility with pVerify
description: Turn a verified eligibility result into a patient cost estimate, either through the Estimation API or the embeddable CGX widget.
api: openapi/pverify-estimation-api-openapi.yml
operations: [createToken, eligibilitySummary, estimateCalculation, createWidgetSetup, cgxInquiry]
generated: '2026-08-15'
method: generated
source: openapi/pverify-estimation-api-openapi.yml + openapi/pverify-cgx-widget-api-openapi.yml + components/pverify-components.yml
---

# Estimate what the patient will owe

Use this at point of service to give a patient a number before they are treated.

## Path A — server-side estimate

### 1. Authenticate — `createToken`

`POST /Token`, client credentials. Send `Authorization: Bearer <token>` + `Client-API-Id`.

### 2. Verify eligibility first — `eligibilitySummary`

`POST /api/EligibilitySummary`. The estimate is only as good as the benefit data behind it, so run
eligibility for the same patient, payer and date of service first and confirm `APIResponseCode 0`.
See the eligibility skill for the pending/poll path.

### 3. Calculate — `estimateCalculation`

`POST /api/EstimateCalculation` with the payer, provider, patient, service date and the procedure
/ service codes being estimated.

Read `APIResponseCode` before the payload — HTTP 200 is returned on business failure too.

## Path B — embeddable widget (CGX)

### 1. Provision — `createWidgetSetup`

`POST https://premium.pverify.com/Widget/Setup`. Note this runs against the **premium portal host**,
not `api.pverify.com`.

### 2. Drive it — `cgxInquiry`

`POST https://api.pverify.com/api/CGXInquiry` returns a combined estimate + eligibility result for
the widget to render.

Widget details: `components/pverify-components.yml`. There is no published loader script URL or
versioned front-end package, so a consumer cannot pin a widget version — provisioning goes through
pVerify.

## Rules

- Estimates are billable transactions with no idempotency key. Compute once, cache your own result
  against `referenceId`; do not recompute on page refresh.
- Present the number as an estimate. pVerify publishes no accuracy guarantee or SLA
  (`lifecycle/pverify-lifecycle.yml`).
- Test host is `https://testapi.pverify.com`; only 6 of 162 practice types exist there, so estimate
  behaviour for most specialties cannot be exercised before go-live.
