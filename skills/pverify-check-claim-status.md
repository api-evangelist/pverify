---
name: Check claim status with pVerify
description: Submit a 276 claim status inquiry to a payer through pVerify and retrieve the 277 response, including the payer-support check that avoids a guaranteed rejection.
api: openapi/pverify-claim-status-api-openapi.yml
operations: [createToken, claimStatusInquiry, getClaimStatusResponse, getAllPayers, getPayerStatus]
generated: '2026-08-15'
method: generated
source: openapi/pverify-claim-status-api-openapi.yml + errors/pverify-error-codes.yml + conventions/pverify-conventions.yml
---

# Check claim status (276/277)

Use this to ask a payer what happened to a submitted claim, without calling the payer.

## 1. Authenticate — `createToken`

`POST /Token`, client credentials. Send `Authorization: Bearer <token>` and `Client-API-Id`
(case sensitive) on every call.

## 2. Confirm the payer supports Claim Status — `getAllPayers`

`GET /API/GetAllPayers` returns every payer pVerify supports. Claim Status is **not** available
for every payer: if the payer does not support 276/277 electronically, the inquiry comes back
`APIResponseCode 5` (`InvalidPayer`) — the one product where code `5` means "wrong payer" rather
than "wrong format".

Optionally `GET /api/GetPayerStatus` (no authentication required) to check the payer is up before
spending a transaction.

## 3. Submit the inquiry — `claimStatusInquiry`

`POST /API/ClaimStatusInquiry` with the provider (`npi`), the subscriber (`memberID`, name, `dob`),
the claim identifiers and the service date range. Dates are `MM/dd/yyyy`.

## 4. Branch on `APIResponseCode`, not HTTP status

This product publishes its own 0–6 code space:

| Code | Meaning | Action |
|---|---|---|
| `0` | Processed | Read the 277 payload. |
| `1` | Rejected | Read `EDIErrorMessage` / `FollowUpAction` / `PossibleResolution`, correct, resubmit. |
| `2` | NoFunds | pVerify account balance exhausted — escalate, do not retry. |
| `3` | Pending | Store `RequestID`, poll step 5. |
| `4` | InvalidRequest | Required data missing. |
| `5` | InvalidPayer | Payer does not support Claim Status electronically, or is inactive. |
| `6` | LocationError | Location is not configured on the pVerify account. |

**Do not reuse the eligibility code table here** — the enums diverge by product. See
`errors/pverify-error-codes.yml`.

## 5. Retrieve — `getClaimStatusResponse`

`GET /API/GetClaimStatusResponse/{requestId}` with the `RequestID` from step 3. Poll with backoff
until the code is terminal.

Never re-POST `claimStatusInquiry` to poll. There is no idempotency key; a second POST is a second
billable transaction with a different `RequestID`.
