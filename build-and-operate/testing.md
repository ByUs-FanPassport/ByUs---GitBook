---
description: "Run the ByUs unit, type, lint, build, end-to-end, contract, and security checks at the correct scope."
icon: vial
---

# Testing

Run checks at the smallest scope that proves the change, then expand before release.

## Web application

```bash
npm run test:web
npm run typecheck
npm run lint:web
npm run build
```

The web package uses:

- Vitest;
- React Testing Library;
- Playwright;
- axe-core for browser accessibility checks;
- TypeScript.

## End-to-end

```bash
npm run test:e2e
```

For the public responsive smoke set:

```bash
npm run test:e2e:smoke --workspace @byus/web
```

End-to-end coverage includes fan discovery, authentication, Passport and LIVE paths, benefit behavior, and responsive product shells.

## Worker

```bash
npm test --workspace @byus/worker
npm run typecheck --workspace @byus/worker
npm run build --workspace @byus/worker
```

Worker tests cover queue behavior, metadata filtering, transaction recovery, notification delivery, and adapter contracts.

## Smart contracts

```bash
cd contracts
forge test
```

Contract tests cover:

- role separation;
- unique Passport and issuance IDs;
- soulbound transfer restrictions;
- pause behavior;
- mint events.

## Lint and security

```bash
npm run lint
npm run security:audit:baseline
npm run security:verify
```

{% hint style="info" %}
The repository tracks an explicit security baseline. Passing the baseline means the known policy is satisfied; it is not a claim that every dependency has zero findings.
{% endhint %}

## Before a release

1. Run the web and worker type checks.
2. Run the relevant unit tests.
3. Run the contract tests when ABI or mint behavior changes.
4. Run Playwright for affected product flows.
5. Run the security baseline and dependency verification.
6. Verify the deployed product and public GIWA evidence separately.
