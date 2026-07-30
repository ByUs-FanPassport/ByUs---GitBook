---
description: "Understand the four ByUs Live Stamp types, their fan actions, score values, and soulbound ERC-1155 credential model."
icon: stamp
layout:
  width: wide
---

# Live Stamps

Live Stamps turn completed fan actions into durable participation records.

## Current Stamp types

<table data-view="cards">
  <thead>
    <tr>
      <th></th>
      <th></th>
      <th data-hidden data-card-cover data-type="files"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>Knowledge</strong></td>
      <td>Pass the creator-specific fan verification quiz. <strong>+1</strong> Fan Score.</td>
      <td><a href="../.gitbook/assets/stamp-knowledge.png">../.gitbook/assets/stamp-knowledge.png</a></td>
    </tr>
    <tr>
      <td><strong>Reservation</strong></td>
      <td>Reserve a published upcoming LIVE. <strong>+1</strong> Fan Score.</td>
      <td><a href="../.gitbook/assets/stamp-reservation.png">../.gitbook/assets/stamp-reservation.png</a></td>
    </tr>
    <tr>
      <td><strong>Attendance</strong></td>
      <td>Enter the Fan Code shared during the LIVE. <strong>+3</strong> Fan Score.</td>
      <td><a href="../.gitbook/assets/stamp-attendance.png">../.gitbook/assets/stamp-attendance.png</a></td>
    </tr>
    <tr>
      <td><strong>Survey</strong></td>
      <td>Complete the post-LIVE survey. <strong>+2</strong> Fan Score.</td>
      <td><a href="../.gitbook/assets/stamp-survey.png">../.gitbook/assets/stamp-survey.png</a></td>
    </tr>
  </tbody>
</table>

The Stamp artwork is a digital credential representation. It does not represent a physical product.

## LIVE participation sequence

```text
Reserve → Watch on YouTube → Enter Fan Code → Complete Survey
```

The product can record each completed activity before the on-chain transaction finishes. The matching Stamp appears with its current mint state and becomes publicly verifiable after the worker confirms the GIWA receipt.

## Credential model

Live Stamps use a soulbound ERC-1155 contract:

- one token for each unique `issuanceId`;
- supply of one for each issued Stamp;
- operator approvals disabled;
- transfers disabled;
- minting restricted by role;
- minting can be paused.

This design preserves the meaning of the record: a participation credential belongs to the fan who completed the activity.

## Idempotency

The database and contract both prevent duplicate issuance:

1. the product creates an idempotent blockchain job;
2. the worker checks the contract's `issuanceId` mapping before preparing a transaction;
3. the contract rejects an issuance ID that already has a token;
4. a retry broadcasts the same signed transaction bytes.

See [Minting pipeline](../architecture/minting-pipeline.md) for the full recovery path.
