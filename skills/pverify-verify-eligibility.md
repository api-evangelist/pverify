---
name: Verify patient insurance eligibility with pVerify
description: Authenticate to pVerify, submit a real-time 270 eligibility inquiry, handle the pending/poll path, and read the parsed benefit summary without double-billing the account.
api: openapi/pverify-eligibility-api-openapi.yml
operations: [createToken, eligibilitySummary, getEligibilitySummary, getEligibility271, getPendingInquiries, cancelTransaction]
generated: '2026-08-15'
method: generated
source: openapi/pverify-eligibility-api-openapi.yml + conventions/pverify-conventions.yml + errors/pverify-error-codes.yml
---

# Verify patient insurance eligibility

Use this to answer "is this patient covered, and what will they owe" against a real payer.

## Before you start

- Every request carries PHI. Do not log request or response bodies.
- **There is no idempotency key.** Every `eligibilitySummary` POST is a new, separately billable
  transaction. If a call times out, **do not retry it** — go to step 4.
- Test and production differ only by host: `https://testapi.pverify.com` vs `https://api.pverify.com`.
  The credential is the same, so the base URL is the only switch. Confirm which one you are on.

## 1. Get a token — `createToken`

`POST /Token` with `Content-Type: application/x-www-form-urlencoded` and body
`Client_Id=<id>&client_secret=<secret>&grant_type=client_credentials`.
Send the `Client-API-Id` header on this call too. **Header keys are case sensitive.**

Read `access_token` and `expires_in` from the response. Cache the token until it expires; do not
mint a new one per request.

## 2. Submit the inquiry — `eligibilitySummary`

`POST /api/EligibilitySummary` with:

- `Authorization: Bearer <access_token>`
- `Client-API-Id: <your client api id>`
- `Content-Type: application/json`

Body carries `payerCode`, the `provider` block (`npi`, `lastName`), the `subscriber` block
(`firstName`, `lastName`, `dob`, `memberID`), `isSubscriberPatient`, `doS_StartDate` /
`doS_EndDate` and `PracticeTypeCode`. Dates are `MM/dd/yyyy`. Field casing in this API is
inconsistent — send the keys exactly as the spec spells them.

Set `referenceId` to your own correlation id so you can match the response back to your record.

## 3. Read `APIResponseCode` before anything else

pVerify returns **HTTP 200 even when the transaction failed**. Branch on the envelope, not the
status line:

| `APIResponseCode` | Meaning | Do this |
|---|---|---|
| `0` | Processed | Read the benefit payload. Done. |
| `1` | Rejected | Read `EDIErrorMessage`, `FollowUpAction`, `PossibleResolution`; fix the request and resubmit. |
| `2` | NoFunds | The pVerify account balance is exhausted. Stop and escalate — retrying will not help. |
| `3` / `4` | Pending / New | Store `RequestID` and go to step 4. |

Full table: `errors/pverify-error-codes.yml`.

## 4. Poll, don't retry — `getPendingInquiries` then `getEligibilitySummary`

If the POST timed out or returned code 3/4:

1. `GET /API/GetPendingInquiries?DOS=MM-DD-YYYY` (note: this parameter uses **dashes**, unlike the
   request body's slashes) to find the `RequestID` pVerify already created for your inquiry.
2. `GET /API/GetEligibilitySummary/{requestId}` until `APIResponseCode` is `0` or `1`.

Back off between polls. Never re-POST the inquiry to "check" — that bills again and creates an
orphan transaction.

To abandon a pending transaction, `POST /API/CancelTransaction` (`cancelTransaction`).

## 5. Optional artifacts

- `GET /API/GetEligibility271/{requestId}` (`getEligibility271`) returns the raw X12 271 when you
  need the untranslated payer response for audit.
- `GET /Report/EligibilityPDFReport/{requestId}` (`getEligibilityPdfReport`) returns a PDF; it
  authenticates with `Client-API-Id` + `Client-Secret` rather than the bearer token.

## Failure modes to expect

- A payer being down is the most common cause of code `1`. Check `getPayerStatus` (see the
  payer-health skill) before blaming the request.
- Only 6 of 162 practice types exist in the test environment, so test coverage of practice-specific
  benefit objects is thin. See `sandbox/pverify-sandbox.yml`.
