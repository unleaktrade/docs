---
description: >-
  The RFQ lifecycle describes how an RFQ progresses over time, from creation to
  a final outcome.
---

# Lifecycle

Rather than executing immediately, an RFQ follows a **sequence of phases**, each with:

* a clear purpose,
* a limited time window,
* and explicit actions that move the RFQ forward.

This section explains the lifecycle at a **conceptual level**, before diving into specific outcomes.

***

## A Phase-Based Process

An RFQ does not evolve continuously.\
Instead, it moves through **distinct phases**, each represented by a state (see [RFQ States](../../rfq_states.md)).

Each phase:

* enables a specific set of actions,
* restricts what participants can do,
* and prepares the RFQ for the next phase.

{% hint style="info" %}
Importantly, **nothing happens automatically**:

* phases do not advance on their own,
* deadlines only determine _what is allowed_,
* an RFQ moves forward only when someone acts.
{% endhint %}

***

## High-Level Lifecycle

At a high level, every RFQ follows the same structure:

1. **Preparation**\
   The maker creates and configures the RFQ.
2. **Price Discovery**\
   Takers express interest, then reveal concrete quotes.
3. **Selection**\
   The maker chooses one revealed quote. Selecting locks the maker’s base asset in the same step.
4. **Settlement Window**\
   The selected taker completes the trade within a defined time window.
5. **Final Outcome**\
   The RFQ ends either in settlement or in a defined exit state.

This structure is the same regardless of whether the RFQ succeeds or fails.

***

## Time Windows (TTLs)

Each phase after the RFQ is opened is associated with a **time window**: commit, reveal, selection and funding. Preparation has none: a draft can stay a draft.

The commit, reveal and selection windows are counted from the moment the RFQ is opened. The funding window starts when the maker selects a quote.

Time windows:

* limit how long a phase can last,
* protect participants from indefinite waiting,
* enable clean exits when progress stops.

A deadline does not force the RFQ to move forward.\
It only determines **which actions are still valid** once time has passed.

***

## Bonds and Enforcement

Bonds are used throughout the lifecycle to enforce correct behavior.

At a high level:

* the maker posts a bond when opening the RFQ,
* takers post bonds when committing quotes,
* bonds are refunded when obligations are respected,
* bonds are slashed when obligations are violated.

In practice:

* a taker who commits but never reveals loses their bond,
* a selected taker who does not complete settlement loses their bond,
* a maker who receives revealed quotes but never selects one loses their bond,
* takers who revealed but were not selected reclaim their bond once the funding window has passed,
* the maker’s bond is returned when the RFQ settles, expires without any revealed quote, or is left incomplete by the selected taker.

{% hint style="info" %}
All slashed bonds go **entirely to the protocol**.\
They are never redistributed to other participants.
{% endhint %}

***

## Two Ways an RFQ Can End

Once opened, an RFQ ends in exactly one of two kinds of outcome (before opening, the maker can also simply cancel a draft):

* **Successful settlement**\
  A quote is selected and the trade completes.
* **Exit without settlement**\
  The RFQ closes because commitments, reveals, selection, or settlement did not occur in time.

Both outcomes are intentional parts of the design. As with every other step, the final state is only recorded when a participant submits the closing action.

***

## How This Section Is Organized

This lifecycle section is split into two parts:

### Happy Path

Describes the normal, successful flow:\
from RFQ creation to completed settlement.

### Failure & Exit Paths

Describes how RFQs close safely when things do not go as planned:\
no quotes, no selection, or incomplete settlement.

{% hint style="success" %}
Together, these pages describe the full lifecycle.
{% endhint %}

***

## What’s Next?

To understand how an RFQ is supposed to work end-to-end, start with:

👉 [**Happy Path**](happy-path.md)

If you want to understand how the system handles edge cases and failures, continue with:

👉 [**Failure & Exit Paths**](failure-and-exit-paths.md)
