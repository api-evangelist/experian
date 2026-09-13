---
name: experian-contact-data-enrichment
description: Validate an email address or phone number and append identity or demographic attributes
  with Experian — email validation, phone validation, reverse phone append, identity append and
  address enrichment. Handles personal data; read the consent rules before calling.
api: Experian Aperture Data Quality API
generated: '2026-09-13'
method: generated
source: openapi/experian-aperture-openapi.json, https://docs.experianaperture.io/email-validation/experian-email-validation-v2,
  https://docs.experianaperture.io/phone-validation/experian-phone-validation
operations:
  - POST /email/validate/v2
  - POST /email/validation/v1
  - POST /phone/validate/v2
  - POST /enrichment/v2
  - POST /identity/append/v1
  - POST /phone/append/v1
---

# Validate and enrich contact data

Two very different classes of operation live here, and an agent must not treat them the same way.

**Class 1 — validation.** Is this email deliverable? Is this phone number real and what kind of line
is it? You submit a datum you already hold and get back an assessment of it.

**Class 2 — append and enrichment.** Who is behind this phone number? What are the demographics of
this household? You submit a datum and get back **new personal information about an identifiable
person that you did not previously have.**

## Steps — validation

1. **Email.** `POST /email/validate/v2` returns a confidence classification (verified, unknown,
   undeliverable, illegitimate). `POST /email/validation/v1` is the older v1 shape — note the Email
   Validate API carries an **End of Service Life date of 30 April 2026**
   (`lifecycle/experian-lifecycle.yml`); build on v2.
2. **Phone.** `POST /phone/validate/v2` returns validity, line type, portability and connectivity
   attributes. Set `output_format: PLUS_E164` to get numbers back in the ITU-T E.164 international
   format rather than a local one — do this if anything downstream stores or dials the number.

## Steps — append and enrichment

3. **Address enrichment.** `POST /enrichment/v2` takes a resolved `global_address_key` (get one from
   `experian-address-capture` first) and returns geocodes, location insight and Mosaic
   geodemographic segmentation.
4. **Identity append.** `POST /identity/append/v1` returns additional contact and identity attributes
   for a known individual. **USA only.**
5. **Reverse phone append.** `POST /phone/append/v1` returns the identity associated with a phone
   number. **USA only.** This is the operation that walks from a contact datum to a person.

## Rules an agent must not get wrong

- **Steps 3–5 return personal data about identifiable people.** An agent must not call them
  speculatively, must not call them to satisfy curiosity, and must not call them on a subject whose
  data it was given for a different purpose. Have a stated purpose and a lawful basis before the
  call, not after.
- **In the United States this is regulated, not merely sensitive.** Experian is a consumer reporting
  agency; use of consumer data is governed by the FCRA and GLBA, and permissible purpose is a legal
  test, not a policy preference. If you cannot name the permissible purpose, do not make the call.
- **Store the minimum.** Append responses often contain more than you asked for. Persist only the
  fields your stated purpose needs.
- **These are reads and are safe to retry** — 408/429/500/503 can be replayed without side effects.
  They are still billable per success, so a retry loop costs credits.
- **Rate limit is the shared account-wide 150/min.** See `experian-address-capture`.
