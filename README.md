# Experian

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

Experian plc is a global information services company and one of the three major consumer credit bureaus, operating across credit risk, identity verification, fraud prevention, marketing data and data quality. Its public API surface spans two distinct platforms: the Experian Global Developer Portal (developer.experian.com), a region-partitioned OAuth2/OpenID Connect gateway fronting credit, business information, KYC/KYB and decisioning products across the US, UK, EMEA, Brazil, India, Singapore and Australia; and Experian Data Quality / Aperture (api.experianaperture.io), which publishes machine-readable OpenAPI 3.0.4 contracts for address, email and phone validation, demographic enrichment, identity append and bulk batch processing. A legacy SOAP contract (Experian QAS Pro OnDemand) remains published and callable alongside the REST surface.

**Areas:** Company · Credit Bureau · Credit Reporting · Identity Verification · Fraud Prevention · Data Quality · Address Validation · Email Verification · Phone Validation · Data Enrichment · Financial Services · Risk Management

## Experian on APIs.io

Everything profiled for Experian is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/experian/](https://apis.io/providers/experian/)** — or go straight to one of the APIs or properties below.

### APIs (11)

- [Experian Address Validate (Pro OnDemand SOAP)](https://apis.io/apis/experian/address-validate-soap/) — The legacy Experian QAS Pro OnDemand SOAP service, still published and documented by Experian Data Quality. Eleven RPCs (DoSearch, DoRefine, DoGetAddress,…
- [Experian Global Developer Platform](https://apis.io/apis/experian/global-developer-platform/) — The region-partitioned Experian API gateway behind developer.experian.com, fronting credit, business information, KYC/KYB, decisioning and verification…
- [Experian Address Validation API](https://apis.io/apis/experian/experian-address-validation-api/) — The Address Validation API from Experian — 13 operation(s) for address validation.
- [Experian Bulk Address API](https://apis.io/apis/experian/experian-bulk-address-api/) — The Bulk Address API from Experian — 5 operation(s) for bulk address.
- [Experian Bulk Email API](https://apis.io/apis/experian/experian-bulk-email-api/) — The Bulk Email API from Experian — 5 operation(s) for bulk email.
- [Experian Bulk Phone API](https://apis.io/apis/experian/experian-bulk-phone-api/) — The Bulk Phone API from Experian — 5 operation(s) for bulk phone.
- [Experian Email Validation API](https://apis.io/apis/experian/experian-email-validation-api/) — The Email Validation API from Experian — 2 operation(s) for email validation.
- [Experian Enrichment API](https://apis.io/apis/experian/experian-enrichment-api/) — The Enrichment API from Experian — 1 operation(s) for enrichment.
- [Experian Identity Append (USA only) API](https://apis.io/apis/experian/experian-identity-append-usa-only-api/) — The Identity Append (USA only) API from Experian — 1 operation(s) for identity append (usa only).
- [Experian Phone Validation API](https://apis.io/apis/experian/experian-phone-validation-api/) — The Phone Validation API from Experian — 1 operation(s) for phone validation.
- [Experian Reverse Phone Append (USA only) API](https://apis.io/apis/experian/experian-reverse-phone-append-usa-only-api/) — The Reverse Phone Append (USA only) API from Experian — 1 operation(s) for reverse phone append (usa only).

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [experian-aperture](https://apis.io/servers/experian/experian-aperture/)

#### Overlays (1)

OpenAPI overlays, including conversational phrasing for each operation.

- [Experian Aperture Overlay](https://apis.io/overlays/experian/experian-aperture-overlay/)

#### Security (4)

Authentication, trust centre, and vulnerability disclosure.

- [Experian Authentication](https://apis.io/security/experian/experian-authentication/)
- [Experian Domain Security](https://apis.io/security/experian/experian-domain-security/)
- [Experian Trust Center](https://apis.io/security/experian/experian-trust-center/)
- [Experian Vulnerability Disclosure](https://apis.io/security/experian/experian-vulnerability-disclosure/)

#### OAuth scopes (1)

The permissions the API asks for.

- [Experian Scopes](https://apis.io/scopes/experian/experian-scopes/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Experian Plans Pricing](https://apis.io/plans/experian/experian-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Experian Rate Limits](https://apis.io/rate-limits/experian/experian-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.experian.com/)
- [Documentation](https://docs.experianaperture.io/)
- [Getting started](https://developer.experian.com/get-started)
- [API reference](https://docs.experianaperture.io/address-validation/experian-address-validation/realtime-api-reference/api-specification/)
- [Sign up](https://developer.experian.com/sso/register)
- [Support](https://community.experianaperture.io/)
- [Blog](https://developer.experian.com/blogs)
- [Security](https://hackerone.com/experian)
- [Terms of service](https://developer.experian.com/terms-and-conditions)
- [Privacy policy](https://developer.experian.com/privacy-policy)
- [GitHub](https://github.com/experianplc)
- [Status](https://status.edq.com/)

## API Evangelist rating

**Kin Score 57.0** — strong · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 71.4 |
| Contract quality | 49.0 |
| Contract governance | 4.5 |
| Operational transparency | 78.9 |
| Developer ergonomics | 73.2 |
| Access clarity | 42.1 |

**Agent readiness 40.2** — agent-ready (gated down from agent-native)

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | — |
| Reversibility Documented | documented (partial credit) |
| MCP Server | — |
| Auth Clarity | served (partial credit) |
| Idempotency | — |
| Error Semantics | documented (partial credit) |
| OpenAPI Examples | verified |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | — |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | served (partial credit) |
| Protected Resource Metadata | — |
| Dynamic Client Registration | yes |
| Agentic Commerce | — |
| Pagination Ratio | na |
| Operation Distinctiveness | — |

**Regulatory alignment 45.1** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/experian/](https://apis.io/providers/experian/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Experian: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/experian/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
