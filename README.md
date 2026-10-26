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

Experian plc is a global information services company and one of the three major consumer credit
bureaus, operating across credit risk, identity verification, fraud prevention, marketing data and
data quality.

Its public API surface spans two distinct platforms with very different postures.

**Experian Data Quality / Aperture** (`api.experianaperture.io`) is the machine-readable half.
Eleven OpenAPI 3.0.4 documents are published openly at `api.experianaperture.io/docs/`, covering 41
operations across 34 paths: address search, validate, format and layouts; email validation; phone
validation; demographic enrichment; identity append; reverse phone append; and an asynchronous bulk
batch surface for all three data types. A legacy SOAP contract — Experian QAS Pro OnDemand V3, 11
RPCs — is still published and callable at `ws.ondemand.qas.com` and is documented by Experian
alongside the REST surface.

**Experian Global Developer Platform** (`developer.experian.com`) fronts the credit, business
information, KYC/KYB and decisioning products. It is region-partitioned — the US, UK, EMEA, Brazil,
India, Singapore and Australia each run their own production and sandbox hosts with their own
OAuth2/OIDC issuer — and it publishes no OpenAPI. Product reference sits behind a Developer Portal
account.

## What this profile found

- **11 OpenAPI 3.0.4 documents and 1 WSDL**, saved verbatim in `openapi/` and `wsdl/`.
- **12 OAuth/OIDC discovery documents** served across ten hosts, saved verbatim in `well-known/`.
  No `security.txt`, no `api-catalog`, no `apis.json` and no A2A agent card on any Experian host.
- **Zero `operationId` values across all 41 operations** in the published spec, and zero operation
  descriptions — the single highest-leverage fix available to Experian in this contract.
- **A 150 request/minute limit enforced per ACCOUNT**, shared across every license, integration and
  token, with the `X-Rate-Limit-*` header triplet returned at runtime.
- **No idempotency mechanism anywhere**, on a surface that includes a billable, non-idempotent bulk
  batch create.
- **A documented SDK you cannot install** — the current Data Validation Solutions SDKs ship as
  GitHub source only; the TypeScript manifest names `@experianplc/edq.dvs.sdk`, which returns 404
  on npm.
- **No MCP server and no agent card.** `mcp/` holds a derived candidate tool list, explicitly marked
  `mode: none`.

See `apis.yml` for the full artifact index.
