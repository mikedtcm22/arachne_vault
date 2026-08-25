---
created: '2026-08-25T00:00:00.000Z'
pillar: Arachne Intelligence
status: active
tags:
  - tool
  - ai
  - vpf
  - attivo
  - career
title: VPF System
type: tool
---
# VPF System

Up: [[Arachne Intelligence]]

A multi-agent operating system for converting the Assistant Controller workload at Attivo into a **VP of Finance** role. Six agents, one operating loop, a 13-week runway. Case locked 2026-11-24; conversation end of year.

An Augmentation tool in the same family as the [[Attivo Comms Agent]] and the [[Advisory Circle]] — built to serve the consulting work without being the consulting work. It writes the case into [[Attivo VP of Finance Pitch]].

## The thesis

> The constraint is not effort or skill. It is **allocation.** Hours go to work a lower-cost resource or a machine should do, which suppresses both output mix and Attivo's margin. The system re-allocates those hours and generates the evidence that justifies re-titling and re-pricing the role.

North-star metric — the **Mix Ratio**: `(AI resource mgmt + systems/practice design + strategic advisory) ÷ total hours`. Target 75%.

## The organizing fact

ResFrac is sunsetting, and a large block of senior hours is about to come free **at exactly the moment the case is due.** One of two things happens to them: they silently refill with close and compliance work on other clients, or they are pre-committed — before they free up — to FP&A depth, practice IP, and insertion at clients that have gone unserved for bandwidth reasons.

The single highest-leverage act in the system is **pre-allocating those hours before they exist.** A **Reallocation Ledger** traces every freed hour to a named destination, because a rising Mix Ratio with no reallocation trail is a measurement artifact — and "you shed ResFrac and backfilled with easier work" is the most likely objection in December.

Three exclusions follow: no offload transition, no tooling build, and no practice pilot at a sunsetting engagement. The one exception is **harvesting the evidence while the context is fresh** — three annual audits and the Banneker transaction diligence→close, already the strongest single asset in [[Career Facts]].

## The six agents

| Agent | Role |
|---|---|
| **The Ledger** | Sensor. Classifies the calendar into hours by category × client × energy. Classifies only, never proposes. |
| **The Offload Analyst** | Human delegation. Produces Transition Packets that pre-answer *"is this worth it?"* |
| **The Automation Architect** | AI delegation. Build Specs, every build transferable. |
| **The Practice Designer** | Reusable client-visibility IP — the VP-level argument. |
| **The Case Builder** | Evidence accumulation. Writes into [[Attivo VP of Finance Pitch]]. |
| **The Chief of Staff** | Orchestrator. Intake mode (Phase 0) → Operate mode (Phases 1–4). |

## What the ACA taught it

The [[Attivo Comms Agent]]'s learned behavior model is the highest-value input in the system — an empirical map of how I actually work, not a theory of it. Two rules do most of the work:

- **Task-type governs slip, not client gravity.** Build-a-deliverable items slip until they have a block *titled for that deliverable*.
- **Proactive-build forcing function.** On days with an FP&A focus block — especially Fridays — an unprompted client-facing BUILD deliverable ships, with no inbound trigger.

Read together: **the named calendar block is the causal mechanism by which the highest-value work happens.** Since I already time-box tomorrow at the end of each day, the Chief of Staff participates in that ritual rather than proposing a new one. This moves the Mix Ratio *before any delegation completes* — the only lever that produces results inside two weeks.

**Roster-ownership deferral** turned out to be a map of where delegation already works: where roster ownership is clean, the handoff has happened socially and the packet is mostly paperwork. Where I still reply despite a named owner, that gap *is* the transition cost.

The ACA also contributed its **failure**. Its learnings file didn't persist across ephemeral session containers, so evening runs wrote lessons morning runs couldn't see and the agent periodically reset to "first run." The VPF System's durable-state rule is written directly against it: no agent state in local files, and no agent may declare "no prior context" while a system of record exists.

## Two guardrails enforced in code

Both are the kind that get waved through when they are only comments.

**The anti-anchoring gate.** The blueprint's work taxonomy was written without seeing a single hour of my calendar. It ships marked `status: hypothesis`, and the engine *refuses* to emit a figure labeled "baseline" until a human validates it against a real elicited week. Session 1 runs elicitation-first — walk a real week block by block, derive categories from what's described, and only then reconcile against the hypothesis, flagging every divergence. A guessed baseline cannot ship by accident.

**The client-data firewall.** The repo holds mechanism; Drive holds client data. The classifier engine is versioned; its rules are not. A test fails if a real client name reaches the code layer. This also satisfies the transferability requirement — a tool only I can run is a liability in a promotion case.

Numbers ship with tests, per [[Test-Driven Building]]. Practice work follows [[Sliver at a Time]] — on a 13-week runway, sequential big-phase delivery won't produce a demonstrable win in time.

## Why the move is correct either way

The VP move is not a hedge against leaving; it's **the enabling move for both outcomes**, which means the next 13 weeks require no decision about which path to take. It fixes the title problem for external search — screeners read titles before bullets, and the gap between "Assistant Controller" and the [[Career Facts]] headline is doing real damage. And it may also be the destination.

The unresolved tension worth naming: the [[Finance-as-a-Service]] / [[CFO Archetypes]] archetype-D thesis is about *function-design* agency, which is the internal thing. But the revealed preference here — cross-client practice IP, reusable systems — is *portfolio* agency, which is the services-firm thing. Those pull in different directions.

Don't resolve it now. **The promotion conversation is itself how the missing data gets collected** — what Attivo actually offers at VP level is unknowable until asked. That reframes December from a verdict into an input.

Design implication: build every artifact **dual-use** — client-anonymized, outcome-anchored, portable. The same asset is the promotion case and the strongest external candidacy material, and [[Finance Leadership Briefcase]] is already the pattern for the external version.

## Repo

`mikedtcm22/vpf-system` — charter, six agent definitions, seven ritual skills, the calculation engine, artifact templates. Client-identifiable material lives in Drive under Attivo scope, never here and never in this vault.

## Open threads

- Obtain the Attivo VP of Finance JD and comp bands — it's the scoring rubric; every metric should map to a line in it.
- Who decides? One partner or a committee — determines whether this is a document or a campaign.
- Resolve the blueprint's internal inconsistency: 25% of target hours are allocated to a bucket no category maps to.
- Confirm the ACA's learning-loop persistence gap is closed before Phase 1 — if it's still resetting, its output is an unreliable Ledger input.
