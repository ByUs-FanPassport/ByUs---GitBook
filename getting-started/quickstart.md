---
description: "Install the ByUs monorepo, configure the web application, start local development, and run the core quality checks."
icon: rocket
---

# Quickstart

Run the ByUs web application locally and confirm the repository is ready for development.

## Requirements

- Node.js `24.13.1`
- npm `11.18.0`
- Git
- Maintainer-approved development values for Privy, Supabase, and GIWA
- Foundry, only when working on smart contracts

## 1. Clone and install

```bash
git clone https://github.com/ByUs-FanPassport/ByUs.git
cd ByUs
npm ci
```

## 2. Configure the web application

Copy the committed environment template:

```bash
cp apps/web/.env.example apps/web/.env.local
```

Fill `apps/web/.env.local` with authorized development values. See [Configuration](../build-and-operate/configuration.md) for the variable groups and security boundary.

{% hint style="danger" %}
Never commit a Privy secret, Supabase service-role key, relayer private key, Pinata credential, or any populated environment file.
{% endhint %}

## 3. Start the web application

```bash
npm run dev --workspace @byus/web
```

Open [http://localhost:3000](http://localhost:3000).

{% hint style="success" %}
The English home should load with the four product destinations: **HOME · LIVE · FAVORITES · MY**.
{% endhint %}

## 4. Run the core checks

```bash
npm run test:web
npm run typecheck
npm run lint:web
npm run build
```

For the worker:

```bash
npm test --workspace @byus/worker
npm run typecheck --workspace @byus/worker
npm run build --workspace @byus/worker
```

For the contracts:

```bash
cd contracts
forge test
```

## Important local-development notes

- Use `npm run dev --workspace @byus/web` for the public onboarding path.
- The root `npm run dev` first enforces a production-local environment contract and is intended for maintainers with approved configuration.
- Do not promise or rely on a one-command `supabase db reset` bootstrap. The repository does not currently include the seed file referenced by the local Supabase configuration.
- `apps/fan-web` is a design workbench, not the production application.

## Next steps

- [Product journey](product-journey.md)
- [Repository map](../build-and-operate/repository-map.md)
- [Testing](../build-and-operate/testing.md)
