---
name: experian-bulk-validation
description: Run an asynchronous bulk validation batch through Experian — create it, start it, poll
  it, retrieve results, and stop it if it goes wrong. Covers the address, email and phone bulk
  surfaces, which share one identical six-operation shape.
api: Experian Bulk Validation API
generated: '2026-09-13'
method: generated
source: openapi/experian-aperture-openapi.json, https://docs.experianaperture.io/address-validation/experian-address-validation/bulk-api-reference/api-specification/
operations:
  - POST /address/bulk/v1/batches
  - GET /address/bulk/v1/batches
  - POST /address/bulk/v1/batches/{batch_id}/start
  - GET /address/bulk/v1/batches/{batch_id}
  - GET /address/bulk/v1/batches/{batch_id}/results
  - POST /address/bulk/v1/batches/{batch_id}/stop
---

# Run a bulk validation batch

The same six operations exist three times over, identically shaped — swap the first path segment for
`email` or `phone`:

```
POST   /{address|email|phone}/bulk/v1/batches                  create
POST   /{address|email|phone}/bulk/v1/batches/{batch_id}/start start
GET    /{address|email|phone}/bulk/v1/batches/{batch_id}       status
GET    /{address|email|phone}/bulk/v1/batches/{batch_id}/results  results
POST   /{address|email|phone}/bulk/v1/batches/{batch_id}/stop  stop
GET    /{address|email|phone}/bulk/v1/batches                  list
```

**This is the one part of Experian's surface that spends money and creates durable state. Read the
safety section before you call it.**

## Steps

1. **Create.** `POST /{type}/bulk/v1/batches` with your records and a `defaults` block (for address:
   `country_iso`; for phone: `output_format`, e.g. `PLUS_E164`, plus options such as
   `get_ported_date`). Address batches accept up to **10,000 addresses per call**. The response
   returns a server-assigned `batch_id`. Set your own `batch_reference_id` so you can find the batch
   again if you lose the response.

2. **Start.** `POST /{type}/bulk/v1/batches/{batch_id}/start`. Creation does not start processing —
   this is a deliberate two-phase commit and it is your only chance to check the batch before it
   costs anything.

3. **Poll.** `GET /{type}/bulk/v1/batches/{batch_id}` until it reports complete. Poll on a sane
   interval: the 150 req/min account-wide limit applies to polling too, and a tight poll loop on one
   batch will throttle everything else on the account.

4. **Retrieve.** `GET /{type}/bulk/v1/batches/{batch_id}/results`.

5. **Stop, if needed.** `POST /{type}/bulk/v1/batches/{batch_id}/stop` halts a running batch.

## Safety rules

- **No idempotency.** There is no `Idempotency-Key` header and no deduplication anywhere in this API.
  `batch_reference_id` and `Reference-ID` are correlation values, not replay protection. **If you
  retry a create after a timeout, you will very likely create a second batch** — and if you then
  start it, you pay twice. Before retrying a create, call `GET /{type}/bulk/v1/batches` and look for
  your `batch_reference_id`.
- **Cost is per successful record.** One credit per record that returns metadata status S200 or
  S206; failures are free. A 10,000-record batch is a 10,000-credit commitment at start time.
- **Stop has no stated window.** A stop operation exists — that is a real reversal path, and better
  than most batch APIs offer. But Experian does not document how long after start a stop is honoured,
  whether records already processed are still billed, or whether a stopped batch can be restarted.
  **Do not assume you can stop a batch you started an hour ago.** If the batch matters, verify the
  behaviour with Experian support before you depend on it in an unattended agent.
- **Confirm before starting an unattended batch.** Because start is billable, not idempotent, and
  reversible only within an unstated window, an agent should treat `start` as an action requiring
  explicit human confirmation, not one it takes on its own judgement.
