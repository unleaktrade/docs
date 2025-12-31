---
description: How the protocol enforces behavior and collects fees.
---

# Bonds & Fees

{% hint style="info" %}
Bonds and fees are the economic backbone of the RFQ system.
{% endhint %}

They ensure that participants act on time, follow through on commitments, and that RFQs always reach a clear outcome, whether successful or not.

This page describes **what bonds exist**, **when they are locked**, **when they are refunded**, and **when they are slashed**.

***

## Why Bonds Exist

RFQs introduce time and optionality.

Without enforcement, participants could:

* commit and never reveal,
* receive quotes and never select,
* lock counterparties without settling.

{% hint style="success" %}
Bonds solve this by attaching a **cost to inaction**.
{% endhint %}

A bond is not a fee: it is a refundable guarantee that is only lost when obligations are violated.

***

## Maker Bond

{% hint style="info" %}
The **maker bond** is posted when the RFQ is opened.
{% endhint %}

### Purpose

* Ensures the maker follows through after receiving valid quotes.
* Prevents RFQs from being opened and abandoned.

### When it is locked

* When the maker opens the RFQ.

### When it is refunded

* When the RFQ settles successfully.
* When the RFQ expires without valid reveals.
* When settlement fails due to taker inaction.

### When it is slashed

* When valid quotes are revealed but the maker fails to select one before the deadline.

### Where slashed funds go

* **100% to the protocol treasury.**

***

## Taker Bond

{% hint style="info" %}
The **taker bond** is posted when a taker commits a quote.
{% endhint %}

### Purpose

* Ensures that committed quotes are revealed.
* Ensures that selected takers complete settlement.

### When it is locked

* When the taker commits a quote.

### When it is refunded

* When the RFQ settles successfully.
* When the taker reveals correctly but is not selected.
* When the RFQ expires without a valid market.

### When it is slashed

* When a taker commits but fails to reveal.
* When a selected taker fails to complete settlement in time.

### Where slashed funds go

* **100% to the protocol treasury.**

***

## Protocol Fees

{% hint style="info" %}
In addition to bonds, the protocol collects fees on successful settlement.
{% endhint %}

### Purpose

* Compensates the protocol for providing the RFQ infrastructure.
* Keeps economic incentives aligned over time.

### When fees are paid

* Only on successful settlement.

### Who pays the fee

* The selected taker.

### What happens on failure

* No protocol fee is charged.
* Only bond penalties apply.

***

## Refunds vs Slashing

The protocol follows a simple rule:

* **Refunds** apply when obligations are respected.
* **Slashing** applies when obligations are violated.

There are no partial penalties and no discretionary decisions.

{% hint style="success" %}
All outcomes are deterministic and enforced by the protocol.
{% endhint %}

***

## No Counterparty Redistribution

A key design choice in this system is that:

> **Slashed bonds are never redistributed to counterparties.**

Instead:

* all slashed bonds go entirely to the protocol treasury,
* counterparties only ever receive refunds of their own bonds.

{% hint style="success" %}
This avoids complex incentive interactions and keeps outcomes predictable.
{% endhint %}

***

## Economic Summary

* Maker bond enforces selection.
* Taker bond enforces reveal and settlement.
* Fees are only paid on success.
* Slashed bonds always go to the protocol.
* Every RFQ has a clear economic outcome.

***

## Closing Note

{% hint style="info" %}
Bonds and fees are not an afterthought, they are what makes RFQs reliable.
{% endhint %}

They ensure that:

* time windows are respected,
* optionality is not abused,
* and both success and failure are handled cleanly.

With this foundation in place, the RFQ system becomes safe, predictable, and composable.
