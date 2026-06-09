---
title: EMBER
type: system
pillar: Arachne On-Chain
status: reviving / working-design
tags: [arachne, on-chain, bitcoin, ordinals, ember]
created: 2026-06-08
---

# EMBER

Up: [[Arachne On-Chain]] · Part of [[Arachne Finance]]

**EMBER** — *Event-Monitored Bitcoin-Embedded Recursion.* A project on the Bitcoin Ordinals protocol for creating **payment-aware ordinals** ("Embers"): inscriptions whose displayed state changes based on separate transactions that occur on-chain.

## The idea
An Ember is dynamic. Its state is computed by monitoring on-chain events — whether qualifying payment transactions have occurred on a defined schedule or post-condition. Recursion (an inscription that renders by reference to other on-chain data) is what lets the displayed output depend on those events rather than being fixed at mint.

## Contemplated use-cases
1. **Truly on-chain memberships.** An Ember represents an active membership and automatically flips to "inactive" if a top-up transaction isn't processed on a programmatic schedule (e.g., *x* BTC / month). Status lives on-chain and enforces itself, with no off-chain gatekeeper.
2. **On-chain royalty enforcement.** A successor to past failed attempts to enforce NFT royalties. The Ember officially displays something *other than* the inscription unless a qualifying "registration" transaction is made post-sale — making creator payment a condition of displaying the real artwork, enforced by the protocol rather than by marketplace goodwill.

## Placement
In-wheelhouse build, outside the finance workflow — weekend [[Arachne On-Chain]] work. This is also the only public surface where the Arachne name is expected to appear.

## Source
Implementation detail to be pulled in from the project GitHub repo — *link TBD.* Update this note once the repo is wired in.

## Open threads
- **Lead use-case** to build against first: membership state vs. royalty enforcement.
- **Mechanism specifics:** what counts as a "qualifying" transaction; how state is read at render time; the recursion / indexing approach.
- **Naming:** "Embers" as the token; EMBER as the protocol.
