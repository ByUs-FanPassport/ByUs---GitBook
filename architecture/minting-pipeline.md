---
description: "Follow the idempotent database-first worker pipeline that issues Fan Passport and Live Stamp credentials on GIWA Sepolia."
icon: arrows-rotate
---

# Minting pipeline

ByUs makes the product record usable first, then mints the matching credential asynchronously.

## Processing sequence

1. **Commit the business action**
   A Supabase transaction records the activity, score change, Passport or Stamp state, and an idempotent blockchain job.

2. **Claim a lease**
   The one-shot worker claims only jobs whose lease it owns.

3. **Reconcile before signing**
   The worker checks the Passport `passportId` or Stamp `issuanceId` mapping and relevant mint event on GIWA.

4. **Build metadata**
   The worker creates PII-free metadata and pins it to an immutable IPFS URI.

5. **Prepare locally**
   The relayer signs an EIP-1559 transaction.

6. **Persist before broadcast**
   While the lease is still held, the worker stores the expected transaction hash and exact raw signed bytes.

7. **Broadcast deterministically**
   The worker broadcasts the stored bytes. A retry re-broadcasts the same transaction instead of consuming a second nonce.

8. **Confirm and reconcile**
   The worker validates the receipt and mint event, then updates both the queue and credential to `minted`.

## Recovery invariant

```text
prepare → persist expected hash + signed bytes → broadcast → verify receipt
```

The order is deliberate. A process failure after signing but before or after broadcast can be recovered without creating a second credential.

## Scheduling

The current mint runtime is:

```text
Supabase pg_cron
  → protected Edge Function
  → SigV4-signed AWS Lambda invocation
  → one-shot worker
  → Supabase queue
```

The worker does not schedule itself and is disabled unless explicitly enabled.

## Queue states

The queue tracks work through leased, retryable states. Credential and job state are reconciled transactionally so the product cannot report a successful mint without the corresponding receipt.

{% hint style="warning" %}
Run one active mint-worker replica per relayer account until nonce reservation is coordinated at the database layer.
{% endhint %}

## Notification isolation

Notification delivery is a separate one-shot worker with its own queue, schedule, environment, and Web Push sender. A notification failure does not change mint-worker configuration or credential state.
