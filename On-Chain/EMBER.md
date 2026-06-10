---
title: EMBER
type: system
pillar: Arachne On-Chain
status: v0 specs drafted; reference impl pending (TDD)
tags:
  - arachne
  - on-chain
  - bitcoin
  - ordinals
  - ember
  - recursion
created: '2026-06-08'
repo: 'https://github.com/mikedtcm22/embers-protocol'
---
# EMBER

Up: [[Arachne On-Chain]] · Part of [[Arachne Finance]]

**EMBER** — *Event-Monitored · Bitcoin · Embedded · Recursion.* A Bitcoin Ordinals primitive: inscriptions ("Embers") that render their state by verifying related on-chain events — payment or registration transactions — **without relying on any authoritative third-party server**.

Repo: https://github.com/mikedtcm22/embers-protocol — protocol-first; specs Draft, reference implementation pending.

## The idea
A parent inscription declares a **policy**, discovers valid **child event inscriptions**, verifies their backing Bitcoin transactions, **reduces** those events into state, and **renders** from that state. Recursion (Ord's recursive endpoints) is what lets an inscription inspect related on-chain data — block height, child inscriptions, and crucially raw transaction hex via `/r/tx/<txid>` — so the rendered output depends on real events rather than being fixed at mint. Missing or malformed data **fails closed** (renders inactive/expired).

## One primitive, two profiles
The earlier "two use-cases" framing has resolved: they aren't separate products, they're two profiles of a single primitive.

`EMBER = parent + policy manifest + event children + verifier + reducer + renderer`

- **`ember.balance-decay.v0`** — memberships / subscriptions / prepaid cards. Balance decays by block height and is topped up by valid payment events:
  `remaining_sats = sum(valid_topups) − decay_per_block × elapsed_blocks` → `active = remaining_sats > 0`. (The reducer still has to choose aggregate vs. per-receipt decay.) This is the on-chain **membership** use-case.
- **`ember.registration-gate.v0`** — renders active only while a valid registration event exists for the current ownership epoch (`H_child == H_parent`). The clean successor to the royalty idea: it doesn't *force* marketplace royalties, it makes registration the condition for canonical display — economically and socially meaningful. This is the **royalty-enforcement** use-case, reframed.

## How verification works
The **parent** holds the policy manifest + verifier + reducer + renderer; **event children** carry an event envelope + profile payload + transaction references / raw hex.

Verification runs in layers, each failing closed: (1) envelope shape → (2) profile matches policy → (3) parent matches policy → (4) payload shape → (5) referenced tx valid & bounded → (6) OP_RETURN commitment binds event↔parent → (7) required payment outputs exist → (8) height / replay rules.

A **qualifying transaction** (the thing that flips state) is one that pays ≥ the required amount to the policy's payout `scriptPubKey` **hex** — matched exactly, not by decoding addresses inside inscription code — with a commitment binding it to the parent and passing height/replay checks.

Commitment format direction: `EMBER0|<profile>|<parent_digest>|<event_type>|<expiry_block>|<event_digest>`, revised from the old `EMBR1|…|receipt_hash` to avoid the circular-hash problem (a receipt hash that includes data the OP_RETURN itself changes).

Draft API: `verifyEvent(policy, event)` → valid / invalid(+reason); `reduceEvents(policy, events, context)` → state.

## Non-negotiables (the design spine)
- No authoritative backend; parent rendering must stand alone.
- Missing required data fails closed.
- Verification is deterministic and bounded.
- Inscription-targeted code stays tiny and dependency-light.
- Server tooling may observe or debug, but is never the source of truth.

See the [threat model](https://github.com/mikedtcm22/embers-protocol/blob/main/docs/threat-model.md) for attack surfaces — e.g. parsing OP_RETURN structurally rather than naive `0x6a` scanning, and pinning any loaded child library against supply-chain risk.

## Status & lineage
- **Stage:** v0 specs drafted (status: Draft); reference implementation is a stub (`EMBER_CORE_VERSION = '0.0.0'`), no tests yet. Built under strict **TDD** — smallest failing test → minimal code → refactor.
- **Lineage:** a clean rewrite (ADR 0001, 2026-06-01) out of the archived `ordPayCard` repo (the SatSpray membership-card app). That repo proved the parent→child Ord flow on Signet — parent inscription, transfer, OP_RETURN payment, child receipt — but left the on-chain Embers Core as a stub returning `0n`: the infrastructure worked, the business logic was never proven on-chain.
- **Read order:** EMBER-CONTEXT → ember-core-v0 spec → balance-decay profile → registration-gate profile → threat model.

## Open threads
Resolved since the last revision of this note:
- **Lead profile:** start with **balance-decay** (the simpler first proof); use **registration-gate** to pressure-test the security model from day one.
- **Naming:** confirmed — "Embers" are the inscriptions, EMBER is the protocol.
- **Mechanism:** "qualifying transaction" and how state is read at render time are specified above.

Still open (from the repo):
- Parent IDs in commitments: human-readable vs. `parent_digest = sha256(lowercase inscription_id)`.
- Should the event reveal tx be required to be the payment tx wherever possible?
- Event-child encoding: JSON, JSONP, or both?
- Library-upgrade pinning for immutable parents (supply-chain).
- Which subset of Ord recursive endpoints is safe across common viewers/wallets (reconfirm exact response shapes against current Ord docs).
- First TDD slice: reject a top-up/event for the wrong parent — protocol shape before Bitcoin-parser complexity.
