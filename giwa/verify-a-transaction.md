---
description: "Verify the example ByUs Passport and Stamp transactions with the GIWA Sepolia Explorer or JSON-RPC."
icon: circle-check
---

# Verify a transaction

Use the official Explorer for a visual check or the GIWA Sepolia RPC for a machine-readable receipt.

## Passport mint

Transaction:

```text
0x7574bdeb18ca5ecfcffcbc581cad353e9bfdff69d7f3c792d3add471f54c504e
```

[Open in GIWA Sepolia Explorer](https://sepolia-explorer.giwa.io/tx/0x7574bdeb18ca5ecfcffcbc581cad353e9bfdff69d7f3c792d3add471f54c504e)

```bash
curl https://sepolia-rpc.giwa.io \
  -H 'content-type: application/json' \
  --data '{
    "jsonrpc": "2.0",
    "method": "eth_getTransactionReceipt",
    "params": [
      "0x7574bdeb18ca5ecfcffcbc581cad353e9bfdff69d7f3c792d3add471f54c504e"
    ],
    "id": 1
  }'
```

Confirm:

- `status` is `0x1`;
- `to` is `0x17f9fb7658a326dd88db523739c227faf50fca20`;
- an ERC-721 transfer from the zero address minted token ID `6`;
- the receipt includes the `PassportMinted` event.

## Stamp mint

Transaction:

```text
0x4c3bcf6e47388b30c289bf83c468f67fb2047799b47e31b5181e83c44c5ef627
```

[Open in GIWA Sepolia Explorer](https://sepolia-explorer.giwa.io/tx/0x4c3bcf6e47388b30c289bf83c468f67fb2047799b47e31b5181e83c44c5ef627)

```bash
curl https://sepolia-rpc.giwa.io \
  -H 'content-type: application/json' \
  --data '{
    "jsonrpc": "2.0",
    "method": "eth_getTransactionReceipt",
    "params": [
      "0x4c3bcf6e47388b30c289bf83c468f67fb2047799b47e31b5181e83c44c5ef627"
    ],
    "id": 1
  }'
```

Confirm:

- `status` is `0x1`;
- `to` is `0x1adcde3473c4e884e60205b397ece744d8892285`;
- an ERC-1155 mint issued token ID `7` with amount `1`;
- the receipt includes the `StampMinted` event.

## Verify deployed bytecode

Replace `<ADDRESS>` with either deployed contract address:

```bash
curl https://sepolia-rpc.giwa.io \
  -H 'content-type: application/json' \
  --data '{
    "jsonrpc": "2.0",
    "method": "eth_getCode",
    "params": ["<ADDRESS>", "latest"],
    "id": 1
  }'
```

A deployed contract returns a non-empty hexadecimal bytecode value. An externally owned account or unused address returns `0x`.

{% hint style="warning" %}
These are public testnet records. Never paste a private key, seed phrase, service credential, or raw signed production transaction into an Explorer or documentation example.
{% endhint %}
