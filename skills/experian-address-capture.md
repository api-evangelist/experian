---
name: experian-address-capture
description: Capture and verify a postal address with Experian Address Validation — run an
  autocomplete search, refine or step into an ambiguous result, then format the chosen address
  under a layout. Use when a form, a record or an agent needs a real, deliverable address rather
  than free text.
api: Experian Address Validation API
generated: '2026-09-13'
method: generated
source: openapi/experian-aperture-openapi.json, https://docs.experianaperture.io/address-validation/experian-address-validation/
operations:
  - GET /address/datasets/v1
  - POST /address/search/v1
  - POST /address/suggestions/refine/v1/{key}
  - GET /address/suggestions/stepin/v1/{global_address_key}
  - POST /address/suggestions/format/v1
  - GET /address/format/v1/{global_address_key}
  - POST /address/validate/v1
---

# Capture a verified address with Experian

Operations are addressed by **method and path**, not by `operationId`. That is not a shortcut: the
published Experian OpenAPI declares zero `operationId` values across all 41 operations, so there is
no identifier to cite. Verify any path below against `openapi/experian-aperture-openapi.json` before
relying on it.

## Before you start

- **Auth.** Send your token in the `Auth-Token` header on every request (`x-app-key` is the
  documented alternative header for the same value). Tokens come from the Self Service Portal, not
  from a signup flow. A valid token that returns 403 usually means the wrong product, no credits, a
  disabled token, or a calling domain/IP that is not on the integration allowlist.
- **There is no sandbox.** Experian Data Quality has no test host. You are calling production.
- **Billing.** A request costs one credit only when it returns HTTP 200 with a metadata status of
  S200 or S206. Anything else is free — so a failed search costs nothing, and a retry after a 5xx
  costs nothing extra.
- **Trace every call.** Set a `Reference-ID` header with your own correlation value. It is what
  support asks for. It is *not* an idempotency key and does not deduplicate anything.

## Steps

1. **Find out what you are allowed to search.** `GET /address/datasets/v1` returns the country
   datasets the token is entitled to and the search types each one supports. Do this once at startup
   and cache it — do not guess a `country_iso`. Country codes are ISO 3166-1 alpha-3 (`GBR`, `USA`,
   `AUS`), not two-letter.

2. **Search.** `POST /address/search/v1` with the partial address, the `country_iso` and the search
   type (`autocomplete` for keystroke-by-keystroke capture, `singleline` for a whole string you
   already hold, `typedown` for a guided drill-down). You get back suggestions, each carrying a
   `global_address_key`. That key is the handle for everything downstream.

3. **Resolve ambiguity, if any.** A suggestion can be a container rather than a deliverable address —
   a building with flats, an office with suites. Two different moves:
   - `POST /address/suggestions/refine/v1/{key}` when you have a refinement term to narrow by.
   - `GET /address/suggestions/stepin/v1/{global_address_key}` to list what is inside a container.
   Loop until a suggestion is a single deliverable address.

4. **Format the result.** `GET /address/format/v1/{global_address_key}` returns the full address —
   formatted lines, components, match info. Pass a layout name to control the shape; layouts are
   managed separately (see `experian-address-layouts`). If you are formatting straight from a
   suggestion list, `POST /address/suggestions/format/v1` does the same in one call.

5. **Or validate in one shot.** If you already hold a complete address and only need to know whether
   it is real, `POST /address/validate/v1` skips the search/refine loop and returns the match level
   plus granular per-component verification flags showing which parts Experian changed.

## Rules an agent must not get wrong

- **Rate limit: 150 requests per minute, per ACCOUNT.** Not per key, not per endpoint — the limit is
  shared across every license, integration and token on the account, and it cannot be raised. An
  autocomplete loop firing per keystroke will starve every other integration your organisation runs.
  Debounce, and treat the budget as shared.
- **Read the headers, not the clock.** Every response carries `X-Rate-Limit-Limit`,
  `X-Rate-Limit-Remaining` and `X-Rate-Limit-Reset` (a UTC epoch timestamp). On 429 there is **no**
  `Retry-After` — compute your own backoff from `X-Rate-Limit-Reset`.
- **Retry only what is retryable.** 408, 429, 500 and 503 are safe to retry (these are read
  operations, so replay is harmless). 400, 401, 403, 404, 406 and 415 are not — fix the request.
  On 503, check `https://status.edq.com/` before looping.
- **Timeouts are yours to set.** You may specify a request timeout; valid range is 3–15 seconds.
  Outside that range you get a 400, not a clamp.
- **Errors.** The body is an `error` object with `type`, `title`, `detail` and `instance` — RFC
  9457 members, but served as `application/json`, not `application/problem+json`, and with no
  `status` member. Full catalog in `errors/experian-problem-types.yml`.
