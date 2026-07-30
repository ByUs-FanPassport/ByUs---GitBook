---
description: "Learn what ByUs stores off-chain, what it publishes on-chain, and how owner-scoped access and metadata filtering protect fan data."
icon: shield-halved
---

# Data and privacy

ByUs separates product data from public credential data.

## Off-chain operational data

Supabase is the operational source of truth for:

- fan identity and profile;
- wallet ownership mapping;
- fan verification attempts and responses;
- LIVE reservations and attendance;
- surveys and fan activities;
- Fan Score and level;
- Passport and Stamp product state;
- benefit eligibility and claims;
- notification and blockchain job queues.

Private identity tables use row-level security and are not exposed to browser roles.

## On-chain credential data

Published Passport and Stamp metadata is intentionally narrow:

- credential type;
- creator slug;
- transferability status;
- metadata version;
- immutable image reference.

The metadata builder rejects identity and internal fields including:

- email;
- nickname;
- real name;
- phone number;
- wallet field;
- recipient field;
- internal entity ID.

{% hint style="success" %}
The on-chain record proves credential issuance without publishing the fan's private profile or activity detail.
{% endhint %}

## Owner-scoped reads

Passport and Stamp screens are built from server-side owner projections:

1. the server verifies the Privy session;
2. the request is bound to the canonical ByUs user ID;
3. owner-scoped database functions return only that fan's credential view;
4. responses are marked `no-store`.

## Benefits

Public benefit information and private fulfillment values are stored separately.

Shared or unique codes, external links, and claim delivery details are returned only after server-side ownership and eligibility checks.

## Secret boundary

The web runtime must never receive:

- relayer private keys;
- Pinata credentials;
- Supabase service-role values in browser variables;
- raw signed transactions;
- admin allowlists;
- production secret identifiers.

See [Configuration](../build-and-operate/configuration.md) for the environment split.
