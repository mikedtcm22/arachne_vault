---
title: Capacity Model
type: system
pillar: Arachne Intelligence
status: active
created: '2026-09-21'
tags:
  - system
  - ai
  - aca
  - planning
  - capacity
---
# Capacity Model

Up: [[Attivo Comms Agent]]

The compounding artifact behind the ACA v4 scheduler. It answers one question: **how much work will actually survive a day, and where in the day does each kind of work survive?**

> ⚠️ **PARTLY MEASURED.** Seeded 2026-09-21 from the priors in the v4 spec §6. **Measurements from three days — 2026-09-22, 2026-09-23 and 2026-09-24, 13 scoreable blocks** — are marked below; everything unmarked is still a guess recorded so it can be falsified. Three days is enough to say which splits **replicate**. It is not enough to fix a parameter.

**What this note is.** Only the congealed structure — current parameter values and the rules they imply. It is integrated, maintained and small. It is **not a log**: nightly observations are atomic and stay in [[Open Brain]] as `[ACA-PLAN]` thoughts.

**Update protocol.** `upsert_note` overwrites in full, so the evening run must `read_note` first, merge, and write back. Test **S8** asserts the read preceded the write. Revision line at the foot, capped at the last ten entries. **As a measured value replaces a prior, delete the prior** — this note should shrink as it learns.

---

## 0. The two axes — read them together or not at all

**Minutes-survival alone has now ranked the three measured days wrongly in two different directions** (2026-09-23(J), 2026-09-24(J)).

| Day | Minutes survival | Flags cleared | Outbound artifacts | The better day |
|---|---|---|---|---|
| 2026-09-22 | 68.8% | 0 of 8 | — | — |
| 2026-09-23 | 30.4% | **2 of 8**, both top-ranked | 2 emails | **9/23 over 9/22** |
| 2026-09-24 | **16.7%** | 2 of 16, one of them red | **2 emails + 5 Slack posts + 1 Doc** | **9/24 was the highest-output day measured** |

**A plan displaced by more urgent work of the same client is a successful displacement and must not train the scheduler toward smaller plans.** A day can be almost entirely unplanned and still be the most productive one measured. **Always report clearance and artifacts alongside survival.**

---

## 1. What each number actually means

| Tag | Assumed planning minutes | Measured median | n | Drift |
|---|---|---|---|---|
| `1` | 30 | — | 0 | — |
| `2` | 90 | — | 0 | — |
| `3` | 165 | — | 0 | — |
| `4` | not schedulable | n/a | n/a | decompose marker, not a size |

Tags are readable only through Asana, unavailable on all six runs to date. **Nothing in §1 can move until the connector is authorised.**

**Adjacent measurement that does not need tags** (2026-09-22, n = 2): **externally-organised meetings ran 117% of their booked minutes** — Kestrel 40 against 30, DeepScribe×Tabs 61 against 60. Treat a counterparty's booking as a floor, not a box. *Has not advanced since — Fireflies has been absent on 9/23 and 9/24.*

## 2. What each letter actually means

Completion rate for `H` / `M` / `L` by time-of-day window. Still entirely unmeasured — letters live in Asana tags.

| Window | `H` | `M` | `L` |
|---|---|---|---|
| 8:30–11:00 | — | — | — |
| 11:00–1:00 | — | — | — |
| 1:00–4:00 | — | — | — |
| 4:00–6:00 | — | — | — |

**Seed placement priors:**

- `H` → the first contiguous window of ≥90 min after 9:00. ⚠️ The spec attributes this to Lesson 2026-08-18(A), which **did not surface in the Open Brain corpus**. Treat as uncited.
- `M` → mid-morning through mid-afternoon. `L` → fragments, post-meeting recovery, late afternoon.
- Daily `H` budget: **3 hours**, no two cross-client `H` tasks adjacent. Pure guess.

## 3. Survival rate

**⚠️ THE BINARY RATE IS THE WRONG INSTRUMENT ON ITS OWN.** Record planned and logged minutes per block, never merely ran / shifted / rolled / dropped.

**⚠️ EXCLUDE CONTAINERS FROM THE DENOMINATOR** (2026-09-23(C)). `(AI/Team Mgmt & Admin Tasks)` and bare `[hold]`/`[HOLD]` are **allocations of unassigned time, not plans** — Michael's `[MC]` note of 2026-09-02: *"the 'hold' for each day, which I'll replace with task-blocks generally the evening before."* Score a container on what replaced it.

| Day | Planned blocks | Survived | Planned min | Logged min | **Survival (minutes)** |
|---|---|---|---|---|---|
| 2026-09-22 | 4 (snapshot-restricted) | 3 | 240 | 165 | **68.8%** |
| 2026-09-23 | 6 | 1 | 345 | 105 | **30.4%** |
| 2026-09-24 | 2 (snapshot-restricted) | 1 | 90 | 15 | **16.7%** |
| **Pooled** | **12** | **5** | **675** | **285** | **42.2%** |

**42% is the working figure** (was 46.2% at n=2). The 70% seed cap is superseded. Do not hard-code 42 either — re-measure.

*Counting plans created mid-day as well as those in the 7:30 AM snapshot, 9/24 reads 2 of 3 blocks and 60 of 135 minutes = 44.4%, and the three-day pooled figure is 45.8%. Report the snapshot-restricted number as the comparable one and this as the honest one.*

### The split that replicates: `verb_class`

| `verb_class` | Blocks | Planned min | Logged min | **Rate** | Replicates? |
|---|---|---|---|---|---|
| **coordination** | 10 | 555 | 240 | **43.2%** | **yes, n=3 days** — 50%, 30%, 44% |
| **production** | 3 | 150 | 210 | **140%** | **n=2 days only** — see the warning below |

| Title type | Blocks | Rate | Replicates? |
|---|---|---|---|
| Names a deliverable | 7 | 84% | **no** — 167%, 30%, 100% |
| Generic / topic only | 8 | 39% | **no** — 50%, 80%, 0% |

**Coordination at ~43% is the model's most stable parameter.** The title axis has produced three different orderings in three days and stays demoted; Lesson 2026-09-02(A)'s 7-for-7 named-deliverable result is narrowed, not refuted (per 2026-09-07(B)).

⚠️ **The 140% production row is measured almost entirely off retroactive logs** (2026-09-24(I)). All four of 9/24's production blocks were created during or after their own window, contributing 300 logged minutes and **zero planned minutes**. Across three measured days, **client-analysis production has been pre-planned on zero of them** — the only pre-planned production block was internal. The row is untested on 9/24, not refuted. Report it with its planned-block count beside it and treat a rate built on fewer than three pre-planned production blocks as decorative.

**Scheduler rules from this:**
1. Size a coordination block at **~45% of nominal**, or
2. **Anchor it to the venue that forces it** — the stronger of the two. Demonstrated within a single afternoon on 9/24: `Mixmax | Meeting Prep/Agenda`, anchored to the next morning's client sync, kept 45 of 45 minutes and shipped its Doc; `Client/Double Review`, anchored to nothing, kept 0 of 75 and rolled.

## 4. Switching cost

Seed rule: **maximum five distinct client contexts per day**, batched contiguously.

| Contexts in day | Days | Mean completion (minutes basis) |
|---|---|---|
| 4 (+1 internal) | 1 | 79% |
| 2 (+1 internal) | 2 | 30%, 17% |

**Three days, no relationship.** 9/22 ran four clients at 79%; 9/23 and 9/24 both ran two at 30% and 17%. Contiguity was violated on all three days with no measurable cost. **Context count is not predictive of anything yet, and the seed limit of five has never been approached.**

## 5. Roll history

A task at three rolls stops being silently re-planned and becomes a flag (engine rule 9).

⚠️ `rolls:` has never been readable or writable — it is an Asana fenced-block field. **0 increments have ever been applied across six runs.**

| Block / workstream | Observed rolls | Status |
|---|---|---|
| `Client/Double Review (...)` (`7u71d6h0k1grovgju1jgeao76c`, created 2026-09-18) | **≥3** — 9/23→9/24 at 17:18:59, 9/24→9/25 at 17:24:47 | **at threshold.** Flag it; do not re-plan it a fourth time without cutting scope or naming what it holds |
| `Scanner \| Close: Aug Revenue` | 5 (as of 2026-09-15) | past threshold; unverifiable until the connector returns |

**Rolls are written at EOD, in the same burst that plans tomorrow — not when the conflict arises** (2026-09-23(H), confirmed 2026-09-24). **Consequence: the 4:15 PM EOD Planner cannot see the day's rolls and must mark tomorrow's free windows provisional.** This is what makes the evening run's STEP 11 load-bearing.

## 6. Tag-prediction accuracy

| | Proposed | Unchanged by MC | Corrected | Accuracy |
|---|---|---|---|---|
| Number | 2 | 0 | 0 | **unmeasurable** |
| Letter | 2 | 0 | 0 | **unmeasurable** |

⚠️ This stream cannot open until the EOD Planner runs once and Michael sets a real tag against an agent proposal. Neither agent proposal to date was taken up at all.

**What is scoreable is the agent's own sizing and target selection, and target selection is the bigger error.**

- 9/23: proposed `3H` (165 planning minutes) into a 120-minute window — violated G1 before Michael saw it; the deliverable then took ~30 minutes.
- 9/24: sizing corrected to `2H` into a 105-minute window (G1-conforming) — **and the block was still not taken, because the deliverable was wrong again.**

**THE RULE, NOW AT n=3: size and target from thread velocity, not deadline proximity.** On 9/22, 9/23 and 9/24 the morning window went to whichever Mixmax correspondence thread was live — Pilot revenue reconciliation every time — and never to the 9/30-dated audit backup the agent proposed. An open thread with a counterparty actively sending attachments predicts tomorrow's minutes better than any dated deadline on the board. **The hold does not merely attract the client (2026-09-23(C)); it attracts the client's hottest thread.**

**And name the counterparty who must *receive* the artifact, not the one who produced it.**

⚠️ **A parameter written here but not read into the proposal is not part of the engine** (2026-09-24(K)). The thread-velocity rule was in this note on the morning of 9/24, was read (S8 PASS), and was not applied. Reading and applying are separate steps and only the first is tested. **Every displacement proposal should name which rule of this note it applied.**

## 7. Counterparty volatility and refill

| Disposal mode | 9/22 | 9/23 | 9/24 | Note |
|---|---|---|---|---|
| Cancelled by counterparty | 1 | 1 | 1 | 9/24's: Pavan and Ryan out, relayed by Matt Stiffler |
| Moved by counterparty | 1 | 0 | 0 | |
| Deleted by Michael (containers) | 2 | 2 | 3 | |
| Moved within the day by Michael | — | — | 3 | |
| Evacuated by a competing client | 1 | 1 | 0 | |
| Rolled forward by Michael at EOD | 0 | 2 | 1 | |
| Retro-filed onto a prior day | 0 | 1 | **0** | **does not replicate** — 1 for 2 |
| **Disposed by scheduling a meeting** | 0 | 0 | **1** | **new mode** — see below |

⚠️ **Block disposal is not primarily counterparty-driven.** Pooled: **5 of 19.**

**New mode — discharge-by-meeting** (2026-09-24(F)). Jennifer Ricafort's five pricing questions, twice flagged red, were disposed of not by a reply but by accepting a client sync for the next morning and bracketing it with two prep blocks. **When a flagged item acquires a dated venue with the right counterparty in it, it stops being overdue.** Downgrade the flag to "venue booked, prep block standing" and name the venue.

**Refill: freed time is filled by re-pointing a block that already exists somewhere on the same day.** Latency is tight at n=3: **55 min** (9/22), **≤59 min** (9/23), **52 min 44 s** (9/24).

**Scheduler consequence, and it is cheap:** freed time cannot be steered by priority after the hour opens — but the capture block **does not have to be standing in that hour, or even later in the day. It only has to exist somewhere on the same day, in either direction.** On 9/24 the block that took the vacated 14:30 slot had been logged at 10:00–10:45 that morning and was simply re-pointed forward. Far cheaper than maintaining a deadline-client filler bench.

⚠️ **Size a capture block to the vacancy plus the soft time abutting it** (2026-09-24(E)). A 30-minute vacancy was refilled with 75 minutes, overflowing into a declined wellness hour. Declined, tentative and externally-organised blocks are not occupied time.

⚠️ **Focus blocks move in both directions.** The corpus rule that focus blocks move only later is **narrowed to client analysis work displaced by incoming client work**. Internal and continuation production work is what absorbs freed time, not what yields it.

---

## Known instrument errors

Four measurement hazards that would otherwise corrupt this model silently.

1. **Retroactive blocks are work logs, not plans.** Split blocks created *before* their start (a plan, scoreable) from those created *after* their end (a log). On 2026-09-23 five of eleven executed blocks were logs; on 2026-09-24, four of seven. Scoring them would report Mixmax 4-for-4 and teach the scheduler that a 60-minute Mixmax block is a reliable forecast. **A block created *during* its own window is in-flight — treat it as a log, and say so.**

2. **A retro block dates the work, not the output.** The correspondence lands *later* than the block's own window. A same-window search returns a false negative.

3. **Classify a burst by the dates it writes, not by its clock time** (revised 2026-09-24). Blocks are re-timed in clusters of seconds. There are two kinds:
   - A **log-burst** re-times *today* and follows an outbound message within 0–120 s. Confirmed n=2 days / 5 bursts: 77 s, 28 s, 25 s (9/23); **13 s and 53 s** (9/24). The calendar stamp is a send-receipt — search Gmail and Slack in the two minutes before a burst to find what shipped.
   - A **plan-burst** writes *future* dates, sits inside the `INBOX Review + Next Day Planning` block, and logs nothing. 9/24's fired 17:24:47–17:27:07 and created all of Friday.
   Mixing them corrupts both the send-receipt search and the roll count.
   Also: sort by start and subtract pairwise overlap before summing logged minutes, and report the overlap. 9/22 overlapped by 45 min; **9/23 and 9/24 both tiled perfectly with zero overlap — read that as a more careful reconstruction, not a more accurate one.** Trust a tidy log's sequence, not its durations.

4. **A block missing from today may have migrated in either direction — match on event id, never on title or absence** (2026-09-23(G), 2026-09-24(G)). Backwards: `Scanner | Review FS Package` was re-filed onto the *previous* day. Forwards: the 9/24 midday run raised a red flag for `Client/Double Review` "vanished with no calendar trace" when the event had simply been rolled to 9/25 with its `createdTime` intact. **Search prior days and the forward week, and use `created` as the tell — a surviving event keeps its original createdTime.**

---

*Lineage: seeded 2026-09-21 from the ACA v4 specification §6 and §8, cross-checked against the `[ACA]` corpus in [[Open Brain]]. Measurements 2026-09-22 to 2026-09-24 from calendar `created`/`updated` metadata diffed against each day's 7:30 AM and 12:30 PM snapshots and reconciled against Gmail sent and Slack. Asana has been unavailable on every run to date, so §1, §2, §5 and §6 remain unmeasured.*

**Revisions** (last ten)

- 2026-09-21 — created, seeded with v4 priors. No measurements.
- 2026-09-22 — first measured values. §3 populated (n=1 day) and **minutes-weighted columns added**. §4 first row. **New §7, Counterparty volatility.** Third instrument error added.
- 2026-09-23 — second measured day. **`verb_class` replaces named/generic as §3's headline split.** **New §0: survival and flag-clearance must be read together.** **Containers excluded from the denominator.** 70% cap superseded by a measured 46.2%. §5 gains the EOD roll-burst finding. §6 gains the first scoreable agent sizing error. §7 narrowed, and gains the pull-forward refill rule and the backwards-migration mode. Instrument error 3's Inbox-Triage-ritual reading falsified and replaced by the send-receipt mechanism; fourth instrument error added.
- 2026-09-24 — third measured day. **Coordination replicates at 43.2% and is now the model's most stable parameter**; the title split flips a third time and stays demoted. Pooled survival 46.2% → **42.2%**. **§6's thread-velocity rule promoted to n=3 and restated as target selection, not just sizing** — the morning window goes to the client's hottest thread, never its nearest deadline. **New §6 warning: a parameter read but not applied is not part of the engine.** §3 gains the warning that the 140% production row is measured off retroactive logs. §5 puts `Client/Double Review` at the 3-roll threshold. §7 gains **discharge-by-meeting** as a new disposal mode, tightens refill latency to 52–59 min at n=3, widens the capture-block hedge to either direction within the day, adds the soft-time-overflow rule, and records that backwards migration **did not replicate**. Instrument error 3 split into log-bursts and plan-bursts; instrument error 4 widened to both directions.
