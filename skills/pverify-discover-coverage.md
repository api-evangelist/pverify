---
name: Discover unknown insurance coverage with pVerify
description: Find active insurance for a patient whose coverage is unknown or self-pay, using pVerify Insurance Discovery plus MBI lookup and patient demographic validation as fallbacks.
api: openapi/pverify-insurance-discovery-api-openapi.yml
operations: [createToken, insuranceDiscovery, getInsuranceDiscoverySummaryResponse, getInsuranceDiscoveryDetailsUrl, getInsuranceDiscoveryReport, mbiInquiry, getMBIResponse, patientFinderInquiry, getPatientFinderResponse]
generated: '2026-08-15'
method: generated
source: openapi/pverify-insurance-discovery-api-openapi.yml + openapi/pverify-mbi-lookup-api-openapi.yml + openapi/pverify-patient-demographic-validator-api-openapi.yml + conventions/pverify-conventions.yml
---

# Discover unknown insurance coverage

Use this when a patient presents as self-pay, or the member ID on file is wrong, and you need to
find billable coverage before writing the encounter off.

## 1. Authenticate — `createToken`

`POST /Token` (client credentials), then send `Authorization: Bearer <token>` **and**
`Client-API-Id` on every subsequent call. See `authentication/pverify-authentication.yml`.

## 2. Fix the demographics first — `patientFinderInquiry`

Insurance Discovery matches on identity, so bad demographics are the usual reason it returns
nothing. `POST /api/PatientFinderInquiry` with the patient's name, DOB, gender and address to
validate and complete the record. Retrieve with
`GET /API/GetPatientFinderResponse/{requestId}` (`getPatientFinderResponse`) or
`POST /API/PatientFinderInquiryResults` (`patientFinderInquiryResults`).

Use the corrected demographics in step 3.

## 3. Run discovery — `insuranceDiscovery`

`POST /api/InsuranceDiscovery` with the (corrected) patient identity and the date of service.

This is an asynchronous product. Expect `APIResponseCode` `3` (Pending) with a `RequestID` far
more often than an immediate `0`.

## 4. Retrieve the result — `getInsuranceDiscoverySummaryResponse`

`GET /api/GetInusuranceDiscoverySummaryResponse/{requestId}`.

Note the path is spelled `GetInusurance…` in pVerify's published surface. That is not a typo on
your side — send it exactly as spelled or you get an IIS 404.

Poll with backoff until `APIResponseCode` is `0` or `1`. Do not re-POST the inquiry; it is
separately billable and there is no idempotency key.

Supporting retrieval operations:

- `GET /API/GetInsuranceDiscoveryDetailsURL/{requestId}` (`getInsuranceDiscoveryDetailsUrl`) — a
  hosted human-viewable detail page.
- `GET /PDFReport/InsuranceDiscovery/{id}` (`getInsuranceDiscoveryReport`) — the PDF report.

## 5. Medicare fallback — `mbiInquiry`

If the patient is likely Medicare but the MBI is missing, `POST /API/MBIInquiry` with name, DOB
and SSN-derived identifiers, then `GET /API/GetMBIResponse/{requestId}` (`getMBIResponse`).

## 6. Confirm before you bill

Discovery returns *candidate* coverage. Verify it for the actual date of service with
`eligibilitySummary` (see the eligibility skill) before submitting a claim against it.

## Rules

- HTTP 200 does not mean success. Branch on `APIResponseCode` — `errors/pverify-error-codes.yml`.
- Code `2` (NoFunds) means the pVerify account balance is out; escalate rather than retry.
- Every call carries PHI and needs a BAA in place. Do not log payloads.
