---
description: "Navigate the ByUs monorepo and understand which packages own the production app, workers, contracts, data model, and tooling."
icon: folder-tree
---

# Repository map

The production system lives in a single npm workspace repository.

```text
ByUs/
├── apps/
│   ├── web/
│   └── worker/
├── contracts/
├── supabase/
│   ├── migrations/
│   └── functions/
├── infrastructure/
│   └── aws/
├── scripts/
└── design/
```

## `apps/web`

The production Next.js application.

It contains:

- the public fan product;
- Google login and Privy integration;
- server-side BFF routes;
- owner-scoped Passport, Stamp, and benefit reads;
- internal operations surfaces;
- Playwright and Vitest coverage.

## `apps/worker`

One-shot background workers for:

- Passport and Stamp minting;
- IPFS metadata;
- GIWA transaction preparation and verification;
- Web Push notification delivery.

The mint and notification runtimes are isolated from each other.

## `contracts`

Foundry project containing:

- `ByUsPassport.sol`;
- `ByUsStamp.sol`;
- deployment scripts;
- role, uniqueness, transfer, and pause tests.

## `supabase`

The operational domain and queue layer:

- identity and wallet ownership;
- creator, LIVE, verification, and activity records;
- Passport, Stamp, score, level, and benefit state;
- owner-scoped read projections;
- idempotent blockchain jobs;
- protected Edge Functions.

## `infrastructure/aws`

Scoped deployment infrastructure for one-shot workers and their environment-specific permissions.

## `scripts`

Environment, deployment, security, media, and verification tooling used by maintainers and CI.

## `apps/fan-web`

`apps/fan-web` is a local UI and design workbench. It is not the production application and should not be used as implementation evidence.

## Source repository

[github.com/ByUs-FanPassport/ByUs](https://github.com/ByUs-FanPassport/ByUs)
