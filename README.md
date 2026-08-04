# pVerify (pverify)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

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
