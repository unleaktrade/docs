---
description: A complete RFQ flow, explained as simply as possible.
---

# RFQ in 1 Minute

This page walks through a full RFQ lifecycle in one minute of reading.

It shows what happens, in order, without edge cases or implementation details.

---

## The Situation

A maker wants to trade a meaningful amount of an asset without impacting the open market.

Instead of trading directly, the maker opens an RFQ to discover prices privately and competitively.

---

## Step 1 - Maker Opens an RFQ

The maker:

- defines the trade parameters,
- opens the RFQ,
- posts a bond.

The RFQ is now public and visible to takers.

---

## Step 2 - Takers Commit Quotes

Interested takers:

- commit quotes by posting bonds,
- do not reveal prices yet.

Multiple takers can commit.  
This creates competition without information leakage.

---

## Step 3 - Takers Reveal Quotes

Committed takers:

- reveal their quotes,
- make prices visible to the maker.

Only revealed quotes are valid.

---

## Step 4 - Maker Selects a Quote

The maker:

- reviews the revealed quotes,
- selects exactly one.

By selecting:

- the maker commits to the trade,
- the maker escrows the base asset.

---

## Step 5 - Taker Completes Settlement

The selected taker:

- completes settlement within the allowed time,
- transfers the quote asset to the maker.

The protocol finalizes the trade.

---

## Step 6 - Trade Completes

On successful settlement:

- assets are exchanged,
- bonds are refunded,
- protocol fees are paid.

The RFQ is closed.

---

## If Something Goes Wrong

If a step is missed:

- deadlines apply,
- bonds enforce correct behavior,
- the RFQ exits through a defined failure path.

Every RFQ always reaches a final state.

---

## One-Sentence Summary

> **An RFQ is a time-bounded negotiation where commitment increases step by step until a trade settles or exits cleanly.**

---

## Where to Go Next

If you want the full details behind each step, continue to:

👉 **RFQ States → Overview**
