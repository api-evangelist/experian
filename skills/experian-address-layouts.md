---
name: experian-address-layouts
description: Manage Experian custom address layouts — the named, server-side definitions that decide
  which address elements a formatted response returns and in what order. Create, list, read, update
  and delete them.
api: Experian Address Validation API
generated: '2026-09-13'
method: generated
source: openapi/experian-aperture-openapi.json, https://docs.experianaperture.io/address-validation/experian-address-validation/layouts/introduction/
operations:
  - POST /address/layouts/v2
  - GET /address/layouts/v2
  - GET /address/layouts/v2/{name}
  - PUT /address/layouts/v2/{name}
  - DELETE /address/layouts/v2/{name}
---

# Manage custom address layouts

Experian has no sparse-fieldset query parameter. Response shaping is a **server-side resource**: you
define a named layout once, then name it when formatting an address. That makes layouts shared,
durable configuration — not a per-request option.

## Steps

1. **See what exists.** `GET /address/layouts/v2` lists the layouts on the account. Also check
   `https://docs.experianaperture.io/address-validation/experian-address-validation/layouts/available-layouts/`
   for Experian's built-in layouts before authoring a new one; most needs are already covered.

2. **Inspect one.** `GET /address/layouts/v2/{name}` returns its lines, elements and the datasets or
   countries it applies to.

3. **Create.** `POST /address/layouts/v2` with the layout name, its lines and element configuration,
   and an `applies_to` declaring which datasets/countries it covers. (`POST /address/layouts/v1` is
   the older shape; prefer v2.)

4. **Update.** `PUT /address/layouts/v2/{name}`. Updating an existing layout through the API was
   added alongside the March 2025 Layout Builder UI work.

5. **Use it.** Name the layout when calling `GET /address/format/v1/{global_address_key}` or
   `POST /address/suggestions/format/v1`.

## Rules an agent must not get wrong

- **Layouts are account-wide shared state.** They are not scoped to your integration. Creating,
  renaming or changing one changes the response shape for every integration on the account that
  names it. Treat a `PUT` to an existing layout as a change to someone else's production output.
- **`DELETE` is irreversible.** No undo, no restore, no soft-delete is documented. Experian added
  historical activity logs with email-based user tracking in January 2025 — those record *who*
  deleted a layout, which is auditability, not recovery. **Read the layout with
  `GET /address/layouts/v2/{name}` and keep the body before deleting anything**, because recreating
  it from scratch is the only recovery path.
- **An agent should not delete a layout autonomously.** Of everything in this API, this is the one
  operation with a permanent consequence and no reversal. Ask a human.
- **No idempotency.** A retried `POST` after a timeout may create a duplicate layout. List first.
