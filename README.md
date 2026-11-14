# Webhook Effect Guard

[Run the free local browser audit](https://webhook-effect-guard.mayasmile.workers.dev)

HTTP200 is a delivery acknowledgement. It does not prove that a shipment or other business action was committed. This checker joins two normalized metadata exports by scope, eventId and action.

## Try the reproducible example

Click **Run the synthetic example**. Five attempts across four event/actions produce one normal retry and three findings: multiple committed effects, acknowledged without effect, and committed without successful acknowledgement. No real customer data is used.

- [Input and expected output JSON](https://webhook-effect-guard.mayasmile.workers.dev/example.json)
- [Offline JavaScript package with17tests](https://webhook-effect-guard.mayasmile.workers.dev/package.zip)
- [Input contract and setup guide](https://webhook-effect-guard.mayasmile.workers.dev/guide)

## Integration contract

Deliveries: scope, eventId, attemptId, status, action. Committed effects: scope, eventId, action, effectId, committed:true. Export durable business rows, not queued jobs. Exactly one effect is expected for each event/action; legitimate fan-out needs distinct actions. Scope separates tenants, environments and destinations. Duplicate export rows are ignored; conflicting identities reject the batch. Max10000rows/table,4MiB combined input. Confirm matching exports and allow asynchronous effects to settle.

The browser runs locally without uploading report data. The [authenticated API](https://rapidapi.com/didyouseethis212sys/api/webhook-effect-guard) is live: BASIC $0/25 requests monthly and PRO $9/500 requests monthly, with hard request limits and separate platform bandwidth fees. The synthetic request returned HTTP200. This project does not send/replay webhooks, prevent duplicates, verify signatures, infer monetary losses or maintain persistent deduplication. Missing rows may be late/incomplete exports. Provider dashboards and SQL scripts may suffice; [Svix](https://www.svix.com/pricing/) also offers a free plan. See [Stripe's webhook documentation](https://docs.stripe.com/webhooks).

Maintainer/AI disclosure: created and documented using an AI agent. Technical tests passed; customer demand and revenue are unverified. Share synthetic examples only, never private payloads, keys or customer information.
