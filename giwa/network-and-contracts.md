---
description: "Reference the current ByUs GIWA Sepolia network configuration, deployed Passport and Stamp addresses, and contract behavior."
icon: file-contract
---

# Network and contracts

The addresses on this page were rechecked against the GIWA Sepolia RPC on July 31, 2026.

The independently buildable and tested contract package is available at [ByUs-FanPassport/ByUs-Contracts](https://github.com/ByUs-FanPassport/ByUs-Contracts).

## Network

| Property | Value |
| --- | --- |
| Chain | GIWA Sepolia |
| Chain ID | `91342` |
| Currency | ETH |
| Explorer | [sepolia-explorer.giwa.io](https://sepolia-explorer.giwa.io) |
| Public RPC | `https://sepolia-rpc.giwa.io` |

The public RPC is rate-limited. Use it for development and verification; use an approved provider for production traffic.

## Deployed contracts

| Credential | Address | Standard | Transferability |
| --- | --- | --- | --- |
| Fan Passport | [`0x17f9FB7658A326DD88dB523739c227faf50Fca20`](https://sepolia-explorer.giwa.io/address/0x17f9FB7658A326DD88dB523739c227faf50Fca20) | ERC-721 | Soulbound |
| Live Stamp | [`0x1AdCdE3473c4e884E60205b397ecE744D8892285`](https://sepolia-explorer.giwa.io/address/0x1AdCdE3473c4e884E60205b397ecE744D8892285) | ERC-1155 | Soulbound |

{% hint style="success" %}
Both addresses returned deployed bytecode from the GIWA Sepolia RPC on July 31, 2026.
{% endhint %}

## Fan Passport contract

The Fan Passport contract:

- issues one token for each unique `passportId`;
- blocks approvals and transfers;
- grants mint permission through `MINTER_ROLE`;
- grants emergency pause control through `PAUSER_ROLE`;
- uses delayed default-admin rules;
- emits `PassportMinted`.

```solidity
event PassportMinted(
    bytes32 indexed passportId,
    uint256 indexed tokenId,
    address indexed to,
    string metadataUri
);
```

Source: [`contracts/src/ByUsPassport.sol`](https://github.com/ByUs-FanPassport/ByUs/blob/main/contracts/src/ByUsPassport.sol)

## Live Stamp contract

The Live Stamp contract:

- issues one token for each unique `issuanceId`;
- fixes the supply of each issued Stamp at one;
- blocks operator approvals and transfers;
- grants mint and pause permissions by role;
- emits `StampMinted`.

```solidity
event StampMinted(
    bytes32 indexed issuanceId,
    uint256 indexed tokenId,
    address indexed to,
    string metadataUri
);
```

Source: [`contracts/src/ByUsStamp.sol`](https://github.com/ByUs-FanPassport/ByUs/blob/main/contracts/src/ByUsStamp.sol)

## Role separation

Deployment accepts separate admin and relayer addresses:

- the admin receives administration and pause control;
- the relayer receives mint permission;
- the relayer does not receive default-admin control.

The repository includes Foundry tests for uniqueness, role boundaries, transfer blocking, and pause behavior.

## Metadata

Both contracts reference immutable IPFS metadata. The worker rejects mutable artwork configuration and filters identity fields before pinning.

Read [Data and privacy](../architecture/data-and-privacy.md) for the published metadata boundary.
