---
description: "Configure the ByUs web and worker runtimes without crossing the browser, server, worker, or secret-management boundaries."
icon: sliders
---

# Configuration

The repository commits variable names and safe defaults, never populated credentials.

## Web: public browser values

Only variables explicitly prefixed with `NEXT_PUBLIC_` may enter the browser bundle.

| Variable | Purpose |
| --- | --- |
| `NEXT_PUBLIC_APP_URL` | Public application origin |
| `NEXT_PUBLIC_PRIVY_APP_ID` | Privy application identifier |
| `NEXT_PUBLIC_BYUS_DATA_ENVIRONMENT` | Data-environment selector |
| `NEXT_PUBLIC_PRIVY_APP_ENVIRONMENT` | Privy-environment selector |
| `NEXT_PUBLIC_PRIVY_TEST_ACCOUNT_LOGIN_ENABLED` | Explicit development test-login switch |

## Web: server-only values

| Variable group | Purpose |
| --- | --- |
| Privy server values | Token and application verification |
| Supabase URL and service role | Server-side domain and owner projections |
| GIWA RPC and Explorer | Chain reads and proof links |
| Passport and Stamp addresses | Credential read configuration |
| Relayer address | Expected issuer identity; not the private key |

## Worker-only values

The mint worker requires server-side values for:

- Supabase service access;
- GIWA RPC and chain ID;
- Passport and Stamp contract addresses;
- deployment block;
- relayer private key;
- Pinata/IPFS configuration;
- immutable metadata artwork base.

{% hint style="danger" %}
The relayer private key, Pinata credential, and Supabase service-role value must never appear in `apps/web`, a `NEXT_PUBLIC_` variable, a client-side error, or a documentation example.
{% endhint %}

## Network guard

The current worker validates that:

```text
GIWA_CHAIN_ID = 91342
```

This prevents the current runtime from silently targeting a different chain.

## Environment files

Start from the committed examples:

```bash
cp apps/web/.env.example apps/web/.env.local
cp apps/worker/.env.example apps/worker/.env.local
```

Use only authorized development values. Do not copy production values into a personal environment file.

## Metadata guard

The mint worker requires immutable `ipfs://` artwork configuration. Mutable HTTPS artwork is rejected.

## Maintainer-only environment sync

The repository contains a production-local environment sync command for authorized maintainers. It is not the public onboarding path and should not be run without approved access.
