# pVerify

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
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

pVerify is a US healthcare insurance eligibility and revenue-cycle API company, part of DoseSpot (now Interra Health). Its REST API at https://api.pverify.com exchanges X12 270/271 eligibility transactions and returns parsed, practice-type-specific benefit summaries; runs 276/277 claim status inquiries; discovers unknown active coverage for self-pay patients; looks up Medicare Beneficiary Identifiers; validates patient demographics; publishes a supported-payer catalog with live per-payer up/down status; and estimates patient financial responsibility at the point of service. Authentication is an OAuth2 client-credentials bearer token plus a case-sensitive Client-API-Id header. pVerify publishes no OpenAPI — its machine-readable contract is a public Postman Collection v2.0.0 at https://postman.pverify.com/, from which the OpenAPI documents in this repository were derived operation-for-operation.

**Areas:** Healthcare · Insurance · Eligibility · Claims · EDI · 270/271 · 276/277 · Revenue Cycle · Medicare · Payers · Insurance Discovery · Patient Estimation

## pVerify on APIs.io

Everything profiled for pVerify is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/pverify/](https://apis.io/providers/pverify/)** — or go straight to one of the APIs or properties below.

### APIs (13)

- [pVerify Authentication API](https://apis.io/apis/pverify/pverify-authentication-api/) — OAuth2 client-credentials token endpoint. POST /Token exchanges Client_Id + Client_Secret for a bearer access_token used on every other pVerify call,…
- [pVerify Eligibility API](https://apis.io/apis/pverify/pverify-eligibility-api/) — Real-time X12 270/271 insurance eligibility verification. Submit an EligibilitySummary inquiry, poll the pending queue, retrieve the parsed benefit summary…
- [pVerify Dental Eligibility API](https://apis.io/apis/pverify/pverify-dental-eligibility-api/) — Dental insurance eligibility and benefit verification, including the only version-prefixed path in the pVerify surface (/api/v2/DentalEligibilitySummary)…
- [pVerify Insurance Discovery API](https://apis.io/apis/pverify/pverify-insurance-discovery-api/) — Find unknown or unreported active insurance coverage for a patient presenting as self-pay, returning candidate payers and member IDs plus a hosted details…
- [pVerify MBI Lookup API](https://apis.io/apis/pverify/pverify-mbi-lookup-api/) — Look up a Medicare Beneficiary Identifier for a patient from demographic data, for providers who need the MBI before they can run Medicare eligibility.
- [pVerify Patient Demographic Validator API](https://apis.io/apis/pverify/pverify-patient-demographic-validator-api/) — Validate and complete patient demographic data (pDV) — name, date of birth, gender and address — so that downstream eligibility and discovery inquiries…
- [pVerify Claim Status API](https://apis.io/apis/pverify/pverify-claim-status-api/) — X12 276/277 claim status inquiry. Ask a payer what happened to a submitted claim and retrieve the 277 response by RequestID. Not every payer supports…
- [pVerify Patient Cost Estimator API](https://apis.io/apis/pverify/pverify-estimation-api/) — Estimate patient financial responsibility for a planned service from the payer benefit data, for point-of-service collection.
- [pVerify Payers API](https://apis.io/apis/pverify/pverify-payers-api/) — The payer network surface: the full supported-payer catalog, live per-payer up/down status (the only pVerify operation requiring no authentication), and…
- [pVerify CGX Widget API](https://apis.io/apis/pverify/pverify-cgx-widget-api/) — Provision and drive the embeddable eligibility-and-estimates widget. Setup runs against the premium portal host; CGXInquiry returns a combined estimate plus…
- [pVerify Same or Similar API (discontinued)](https://apis.io/apis/pverify/pverify-same-or-similar-api/) — Medicare same-or-similar DME history check. pVerify labels this product "(Discontinued)" in its own documentation while continuing to document it in full;…
- [pVerify CMN API (discontinued)](https://apis.io/apis/pverify/pverify-cmn-api/) — Certificate of Medical Necessity lookup. Labelled "(Discontinued)" by pVerify; every operation is marked deprecated in the spec.
- [pVerify SNF API (discontinued)](https://apis.io/apis/pverify/pverify-snf-api/) — Skilled Nursing Facility stay verification. Labelled "(Discontinued)" by pVerify; every operation is marked deprecated in the spec.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Pverify Callbacks](https://apis.io/asyncapis/pverify/pverify-callbacks/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [pverify-mcp.yml](https://apis.io/servers/pverify/pverify-mcp-yml/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Pverify Agentic Access](https://apis.io/agentic-access/pverify/pverify-agentic-access/)

#### Vocabulary (1)

The provider's domain terms, defined.

- [Pverify Vocabulary](https://apis.io/vocabularies/pverify/pverify-vocabulary/)

#### Collections (7)

Postman and Open Collection request collections.

- [pVerify API](https://apis.io/collections/pverify/open-pverify/)
- [pVerify Authentication API](https://apis.io/collections/pverify/open-pverify-authentication-api/)
- [pVerify Authentication Batch API](https://apis.io/collections/pverify/open-pverify-batch-api/)
- [pVerify Authentication Claim Status API](https://apis.io/collections/pverify/open-pverify-claim-status-api/)
- [pVerify Authentication Eligibility API](https://apis.io/collections/pverify/open-pverify-eligibility-api/)
- [pVerify Authentication Estimation API](https://apis.io/collections/pverify/open-pverify-estimation-api/)
- [pVerify Authentication Payers API](https://apis.io/collections/pverify/open-pverify-payers-api/)

#### Overlays (13)

OpenAPI overlays, including conversational phrasing for each operation.

- [Pverify Authentication Api Overlay](https://apis.io/overlays/pverify/pverify-authentication-api-overlay/)
- [Pverify Cgx Widget Api Overlay](https://apis.io/overlays/pverify/pverify-cgx-widget-api-overlay/)
- [Pverify Claim Status Api Overlay](https://apis.io/overlays/pverify/pverify-claim-status-api-overlay/)
- [Pverify Cmn Api Overlay](https://apis.io/overlays/pverify/pverify-cmn-api-overlay/)
- [Pverify Dental Eligibility Api Overlay](https://apis.io/overlays/pverify/pverify-dental-eligibility-api-overlay/)
- [Pverify Eligibility Api Overlay](https://apis.io/overlays/pverify/pverify-eligibility-api-overlay/)
- [Pverify Estimation Api Overlay](https://apis.io/overlays/pverify/pverify-estimation-api-overlay/)
- [Pverify Insurance Discovery Api Overlay](https://apis.io/overlays/pverify/pverify-insurance-discovery-api-overlay/)
- [Pverify Mbi Lookup Api Overlay](https://apis.io/overlays/pverify/pverify-mbi-lookup-api-overlay/)
- [Pverify Patient Demographic Validator Api Overlay](https://apis.io/overlays/pverify/pverify-patient-demographic-validator-api-overlay/)
- [Pverify Payers Api Overlay](https://apis.io/overlays/pverify/pverify-payers-api-overlay/)
- [Pverify Same Or Similar Api Overlay](https://apis.io/overlays/pverify/pverify-same-or-similar-api-overlay/)
- [Pverify Snf Api Overlay](https://apis.io/overlays/pverify/pverify-snf-api-overlay/)

#### Security (3)

Authentication, trust centre, and vulnerability disclosure.

- [Pverify Authentication](https://apis.io/security/pverify/pverify-authentication/)
- [Pverify Domain Security](https://apis.io/security/pverify/pverify-domain-security/)
- [Pverify Trust Center](https://apis.io/security/pverify/pverify-trust-center/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Pverify Plans Pricing](https://apis.io/plans/pverify/pverify-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Pverify Rate Limits](https://apis.io/rate-limits/pverify/pverify-rate-limits/)

#### FinOps (1)

What the API costs to run, by operation.

- [Pverify Finops](https://apis.io/finops/pverify/pverify-finops/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.pverify.com)
- [Documentation](https://docs.pverify.io/)
- [Getting started](https://pverify.com/templates/)
- [API reference](https://postman.pverify.com/)
- [Pricing](https://pverify.com/pricing/)
- [Support](https://pverify.com/contact-support/)
- [Blog](https://pverify.com/blog/)
- [Compliance](https://trust.dosespot.com/)
- [Terms of service](https://pverify.com/pverify-legal-documentation/)
- [Privacy policy](https://pverify.com/privacy-policy/)
- [GitHub](https://github.com/pVerify)
- [Status](https://status.dosespot.com/posts/dashboard)

## API Evangelist rating

**Kin Score 51.2** — developing · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 73.2 |
| Contract quality | 56.4 |
| Contract governance | 33.3 |
| Operational transparency | 42.1 |
| Developer ergonomics | 49.4 |
| Access clarity | 53.9 |

**Agent readiness 36.0** — agent-ready

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | documented (partial credit) |
| MCP Server | — |
| Auth Clarity | bearer (partial credit) |
| Idempotency | — |
| Error Semantics | documented (partial credit) |
| OpenAPI Examples | verified |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | yes |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | na |
| Operation Distinctiveness | distinct |

**Regulatory alignment 19.3** — Insurance

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/pverify/](https://apis.io/providers/pverify/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for pVerify: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/pverify/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
