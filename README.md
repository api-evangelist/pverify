# pVerify (pverify)

pVerify provides real-time healthcare insurance eligibility verification and revenue-cycle APIs. Its RESTful API at https://api.pverify.com exchanges EDI 270/271 eligibility transactions, returns plan and benefit summaries, checks claim status (276/277), lists supported payers, and estimates patient financial responsibility, secured with OAuth2 bearer tokens.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/pverify/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/pverify/refs/heads/main/apis.yml)

## Tags

- Healthcare
- Insurance
- Eligibility
- Claims
- EDI
- 270/271

## Timestamps

- **Created:** 2026-06-21
- **Modified:** 2026-06-21

## APIs

### pVerify Eligibility Inquiry API

Real-time 270/271 eligibility inquiry that posts a full benefit request to a payer and returns the detailed 271 response, with asynchronous retrieval (GetEligibilityResponse), pending-queue listing (GetPendingInquiries), and transaction cancellation (CancelTransaction).

- **Human URL:** [https://docs.pverify.io/](https://docs.pverify.io/)
- **Base URL:** `https://api.pverify.com`

#### Tags

- Eligibility
- 270/271
- Real Time

#### Properties

- [Documentation](https://docs.pverify.io/)
- [API Reference](https://www.pverify.com/rest-api/)
- [OpenAPI](openapi/pverify-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/pverify.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/pverify.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### pVerify Eligibility Summary API

Posts a single real-time eligibility request and returns a condensed, practice-type-specific summary of plan, coverage, copay, coinsurance, deductible, and out-of-pocket benefits.

- **Human URL:** [https://docs.pverify.io/](https://docs.pverify.io/)
- **Base URL:** `https://api.pverify.com`

#### Tags

- Eligibility
- Benefits
- Summary

#### Properties

- [Documentation](https://docs.pverify.io/)
- [API Reference](https://www.pverify.com/rest-api/)
- [OpenAPI](openapi/pverify-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/pverify.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/pverify.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### pVerify Batch Eligibility API

Submits many eligibility verifications in a single batch for asynchronous processing and later retrieval of completed results.

- **Human URL:** [https://docs.pverify.io/](https://docs.pverify.io/)
- **Base URL:** `https://api.pverify.com`

#### Tags

- Batch
- Eligibility
- Async

#### Properties

- [Documentation](https://docs.pverify.io/)
- [OpenAPI](openapi/pverify-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/pverify.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/pverify.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### pVerify Claim Status API

Real-time 276/277 claim status inquiry returning the current processing state, dates, and amounts for a submitted claim direct from the payer.

- **Human URL:** [https://docs.pverify.io/](https://docs.pverify.io/)
- **Base URL:** `https://api.pverify.com`

#### Tags

- Claims
- 276/277
- Claim Status

#### Properties

- [Documentation](https://docs.pverify.io/)
- [API Reference](https://www.pverify.com/claim-status/)
- [OpenAPI](openapi/pverify-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/pverify.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/pverify.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### pVerify Payers API

Returns the current pVerify payer list with payerCode, payerName, and capability flags (isActive, isSupportingEligibility, isSupportingClaims, isEDIPayer) for mapping requests to supported insurers.

- **Human URL:** [https://docs.pverify.io/](https://docs.pverify.io/)
- **Base URL:** `https://api.pverify.com`

#### Tags

- Payers
- Reference Data
- Catalog

#### Properties

- [Documentation](https://docs.pverify.io/)
- [API Reference](https://pverify.com/payer-list/)
- [OpenAPI](openapi/pverify-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/pverify.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/pverify.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### pVerify Estimation API

Patient cost estimation that combines real-time benefits with contracted/fee data to estimate patient financial responsibility for planned services.

- **Human URL:** [https://docs.pverify.io/](https://docs.pverify.io/)
- **Base URL:** `https://api.pverify.com`

#### Tags

- Estimation
- Price Transparency
- Patient Responsibility

#### Properties

- [Documentation](https://docs.pverify.io/)
- [API Reference](https://www.pverify.com/patient-estimator/)
- [OpenAPI](openapi/pverify-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/pverify.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/pverify.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

## Common Properties

- [GitHub Organization](https://github.com/pVerify)
- [LinkedIn](https://www.linkedin.com/company/pverify)
- [Website](https://www.pverify.com)
- [Documentation](https://docs.pverify.io/)
- [Plans](plans/pverify-plans-pricing.yml)
- [Rate Limits](rate-limits/pverify-rate-limits.yml)
- [Fin Ops](finops/pverify-finops.yml)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
