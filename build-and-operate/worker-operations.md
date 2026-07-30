---
description: "Operate the one-shot ByUs mint and notification workers with explicit enablement, lease ownership, environment isolation, and safe recovery."
icon: gears
---

# Worker operations

ByUs background workers are one-shot, environment-scoped, and disabled by default.

## Mint worker

The mint worker:

1. claims a leased blockchain job;
2. reconciles existing chain state;
3. builds PII-free IPFS metadata;
4. prepares and persists a signed transaction;
5. broadcasts the exact stored bytes;
6. confirms the receipt and mint event;
7. completes or retries the job.

It does not schedule itself. Supabase remains the queue and scheduling source of truth.

## Notification worker

The notification worker is packaged and deployed separately. It:

1. enqueues due fan notifications;
2. claims a notification lease;
3. sends Web Push;
4. records completion or retry state.

A notification enqueue failure is fail-closed: the worker does not continue to claim deliveries.

## Operational invariants

- Workers must be explicitly enabled.
- Environment configuration is validated before work begins.
- Dev and production names and secrets remain isolated.
- A mint retry uses the same signed transaction bytes.
- A worker may complete only jobs whose lease it owns.
- Queue and credential state are reconciled after the GIWA receipt.
- One active mint-worker replica is used per relayer account until database nonce reservation is coordinated.

## Safe verification

Before enabling a worker:

1. validate the intended environment;
2. confirm the exact contract addresses and deployment block;
3. confirm the relayer address without exposing its private key;
4. verify the immutable metadata asset URI;
5. run worker tests, type checks, and build;
6. inspect the deployment plan or dry run;
7. enable scheduling only after the runtime is healthy.

{% hint style="danger" %}
Never publish production secret IDs, AWS account details, profiles, private keys, service-role values, raw signed transactions, or internal job identifiers.
{% endhint %}

## Recovery

If a worker stops after signing:

- do not create a new logical job;
- reload the existing job;
- use the stored expected hash and signed bytes;
- reconcile the contract mapping and event;
- re-broadcast only the identical transaction when required.

Read [Minting pipeline](../architecture/minting-pipeline.md) for the full sequence.
