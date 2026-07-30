---
description: "Build with ByUs: the fan participation layer that turns verified activity into Passport, Stamp, and benefit records on GIWA."
cover: .gitbook/assets/byus-docs-cover.png
coverY: 0
layout:
  width: wide
  cover:
    visible: true
    size: full
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# ByUs Developer Documentation

ByUs turns fan participation into a persistent, verifiable record. Fans discover a favorite, verify their fandom, receive a creator-specific Fan Passport, collect Stamps through LIVE activities, and unlock benefits based on what they actually did.

<img src=".gitbook/assets/byus-wordmark.svg" alt="ByUs" width="180">

{% hint style="success" %}
A working ByUs MVP is live at [byus.kr](https://byus.kr/?locale=en). Fan Passport and Stamp mint transactions are verifiable on GIWA Sepolia.
{% endhint %}

<table data-view="cards">
  <thead>
    <tr>
      <th></th>
      <th></th>
      <th data-hidden data-card-target data-type="content-ref"></th>
      <th data-hidden data-card-cover data-type="files"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>Experience the product</strong></td>
      <td>Follow the fan journey from discovery and verification to LIVE participation and benefits.</td>
      <td><a href="getting-started/product-journey.md">getting-started/product-journey.md</a></td>
      <td><a href=".gitbook/assets/product-journey.png">.gitbook/assets/product-journey.png</a></td>
    </tr>
    <tr>
      <td><strong>Understand the architecture</strong></td>
      <td>See how Privy, the ByUs BFF, Supabase, the mint worker, IPFS, and GIWA work together.</td>
      <td><a href="architecture/overview.md">architecture/overview.md</a></td>
      <td><a href=".gitbook/assets/architecture-boundary.png">.gitbook/assets/architecture-boundary.png</a></td>
    </tr>
    <tr>
      <td><strong>Verify the GIWA proof</strong></td>
      <td>Inspect the deployed contracts and successful Passport and Stamp transactions.</td>
      <td><a href="giwa/network-and-contracts.md">giwa/network-and-contracts.md</a></td>
      <td><a href=".gitbook/assets/product-onchain-proof.png">.gitbook/assets/product-onchain-proof.png</a></td>
    </tr>
  </tbody>
</table>

## What ByUs provides

| Layer | What it does |
| --- | --- |
| Fan experience | Discovery, Google sign-in, fan verification, LIVE reservation, attendance, surveys, Passport, Stamps, and benefits |
| Identity | A Privy embedded EVM wallet linked to the canonical ByUs fan account |
| Operational data | Owner-scoped activity, score, level, eligibility, claims, and mint state in Supabase |
| Verifiable credentials | Soulbound Fan Passport and Live Stamp credentials issued on GIWA Sepolia |
| Operations | Server-side BFF, idempotent minting, notifications, and an internal operations console |

## Current network

| Property | Value |
| --- | --- |
| Network | GIWA Sepolia |
| Chain ID | `91342` |
| Passport standard | Soulbound ERC-721 |
| Stamp standard | Soulbound ERC-1155 |
| Product | [byus.kr](https://byus.kr/?locale=en) |
| Application source | [ByUs-FanPassport/ByUs](https://github.com/ByUs-FanPassport/ByUs) |
| Contract source | [ByUs-FanPassport/ByUs-Contracts](https://github.com/ByUs-FanPassport/ByUs-Contracts) |

## Start here

1. Run the application with the [Quickstart](getting-started/quickstart.md).
2. Learn the complete [Product journey](getting-started/product-journey.md).
3. Read the [System overview](architecture/overview.md) before changing identity, activity, or minting behavior.
4. Use [MVP and on-chain proof](getting-started/mvp-evidence.md) to verify the current implementation.

---

<img src=".gitbook/assets/sallylab-logo.svg" alt="SallyLab" width="150">

ByUs is built by SallyLab.
