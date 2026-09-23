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

> ⚠️ **PARTLY MEASURED.** Seeded 2026-09-21 from the priors in the v4 spec §6. **Measurements from two days — 2026-09-22 and 2026-09-23, 12 planned blocks** — are marked below; everything unmarked is still a guess recorded so it can be falsified. Two days is enough to see which splits **replicate** and which flip sign. It is not enough to fix a parameter.

**What this note is.** Only the congealed structure — current parameter values and the rules they imply. It is integrated, maintained and small. It is **not a log**: nightly observations are atomic and stay in [[Open Brain]] as `[ACA-PLAN]` thoughts.

**Update protocol.** `upsert_note` overwrites in full, so the evening run must `read_note` first, merge, and write back. Test **S8** asserts the read preceded the write. Revision line at the foot, capped at the last ten entries. **As a measured value replaces a prior, delete the prior** — this note should shrink as it learns.

---

## 0. The two axes — read them together or not at all

**Minutes-survival alone ranked the two measured days backwards** (2026-09-23(J)).

| Day | Minutes survival | Flags cleared | The better day was |
|---|---|---|---|
| 2026-09-22 | **68.8%** | 0 of 8 | — |
| 2026-09-23 | **30.4%** | **2 of 8**, both top-ranked | **9/23** |

On 9/23 one of six plans survived, and the day sent the Mixmax estimate (accepted by the client 27 minutes later), cleared a three-run-old payment instruction, and gave the 9/30-deadline client 240 minutes against 15 the day before. **A plan displaced by more urgent work of the same client is a successful displacement and must not train the scheduler toward smaller plans.** Always report clearance alongside survival.

---

## 1. What each number actually means

| Tag | Assumed planning minutes | Measured median | n | Drift |
|---|---|---|---|---|
| `1` | 30 | — | 0 | — |
| `2` | 90 | — | 0 | — |
| `3` | 165 | — | 0 | — |
| `4` | not schedulable | n/a | n/a | decompose marker, not a size |

Tags are readable only through Asana, unavailable on all four runs to date. **Nothing in §1 can move until the connector is authorised.**

**Adjacent measurement that does not need tags** (2026-09-22, n = 2): **externally-organised meetings ran 117% of their booked minutes** — Kestrel 40 against 30, DeepScribe×Tabs 61 against 60. Both overran; neither under-ran. Treat a counterparty's booking as a floor, not a box. *Did not advance 2026-09-23 — Fireflies was absent that run.*

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

**⚠️ THE BINARY RATE IS THE WRONG INSTRUMENT ON ITS OWN.** A block can appear on the executed calendar under its own name while keeping an eighth of its minutes (`Mixmax | Audit Updates`, 120 → 15 min, scored "ran shifted"). **Record planned and logged minutes per block, never merely ran / shifted / rolled / dropped.**

**⚠️ EXCLUDE CONTAINERS FROM THE DENOMINATOR** (2026-09-23(C)). `(AI/Team Mgmt & Admin Tasks)` and bare `[hold]`/`[HOLD]` are **allocations of unassigned time, not plans** — Michael's `[MC]` note of 2026-09-02: *"the 'hold' for each day, which I'll replace with task-blocks generally the evening before."* On 9/23 the 9:00–11:00 hold was deleted and 09:15–12:00 filled with 165 minutes of named Mixmax work; scored as a plan that is a 120-minute drop, which is the hold **succeeding**. Score a container on what replaced it.

| Day | Planned blocks | Survived | Planned min | Logged min | **Survival (minutes)** |
|---|---|---|---|---|---|
| 2026-09-22 | 4 (snapshot-restricted) | 3 | 240 | 165 | **68.8%** |
| 2026-09-23 | 6 | 1 | 345 | 105 | **30.4%** |
| **Pooled** | **10** | **4** | **585** | **270** | **46.2%** |

**The 70% seed cap is optimistic.** Use 46% as the working figure and re-measure; do not yet hard-code it.

### The split that replicates: `verb_class`

**2026-09-22 left the named/generic and production/coordination axes confounded at n=6 and asked for a day that separated them. 2026-09-23 separated them, and the title axis lost** (2026-09-23(A)).

| `verb_class` | Blocks | Survived | Planned min | Logged min | **Rate** | Replicates? |
|---|---|---|---|---|---|---|
| **production** | 3 | **3 of 3** | 150 | 210 | **140%** | **yes** — 167%, then 100% |
| **coordination** | 7 | 3 of 7 | 420 | 180 | **43%** | **yes** — 50%, then 30% |

| Title type | Blocks | Planned min | Logged min | Rate | Replicates? |
|---|---|---|---|---|---|
| Names a deliverable | 5 | 240 | 195 | 81% | **no — 167% then 30%** |
| Generic / topic only | 7 | 465 | 195 | 42% | **no — 50% then 80%** |

On 9/23 all three named blocks were coordination (30%) and the one production block was generic (100%). The pooled title advantage is carried entirely by day one.

**Lesson 2026-09-02(A)'s 7-for-7 named-deliverable result is narrowed, not refuted** (per 2026-09-07(B)) — but it is no longer the model's most valuable parameter. **`verb_class` is.**

**Scheduler rules from this:**
1. Size a coordination block at **~45% of nominal**, or
2. **Anchor it to the venue that forces it.** Michael does this unprompted: on 9/23 he dropped `DeepScribe | New Update/Agenda Doc` and re-placed it at 09:00 the next morning, *ahead of* the 14:30 check-in it feeds, rather than in a floating slot.

## 4. Switching cost

Seed rule: **maximum five distinct client contexts per day**, batched contiguously.

| Contexts in day | Days | Mean completion (minutes basis) |
|---|---|---|
| 4 (+1 internal) | 1 | 79% |
| 2 (+1 internal) | 1 | 30% |

**Two days, opposite directions — context count is not yet predictive of anything.** 2026-09-22 ran four clients at 79%; 2026-09-23 ran two at 30%. Contiguity was violated on both days with no measurable cost.

## 5. Roll history

A task at three rolls stops being silently re-planned and becomes a flag.

⚠️ `rolls:` has never been readable or writable — it is an Asana fenced-block field. **0 increments have ever been applied across four runs.** Rolls observed on the calendar (2 on 9/23: `Client/Double Review`, `DeepScribe | New Update/Agenda Doc`) cannot be recorded against their tasks.

| Workstream | Rolls | Status |
|---|---|---|
| Scanner \| Close: Aug Revenue | 5 (as of 2026-09-15) | past threshold; unverifiable until the connector returns |

**Rolls are written at EOD, in the same burst that logs the day's last deliverable — not when the conflict arises** (2026-09-23(H)). Both of 9/23's rolls landed at 17:05:34 and 17:18:59, during the 16:45–17:15 planning block. **Consequence: the 4:15 PM EOD Planner cannot see the day's rolls and must mark tomorrow's free windows provisional.** A 4:15 run on 9/23 would have double-booked 15:00–16:15. This is what makes the evening run's STEP 11 load-bearing.

## 6. Tag-prediction accuracy

| | Proposed | Unchanged by MC | Corrected | Accuracy |
|---|---|---|---|---|
| Number | 1 | 0 | 0 | **unmeasurable** |
| Letter | 1 | 0 | 0 | **unmeasurable** |

⚠️ This stream cannot open until the EOD Planner runs once and Michael sets a real tag against an agent proposal.

**What is already scoreable is the agent's own sizing, and it is poor** (2026-09-23(I)). The single proposal to date — `3H`, "Mixmax | Finalize estimate + answer Viola on pipeline scope", placed 9:00–11:00:

- **It violated G1 before Michael saw it**: a `3` is 165 planning minutes, given a 120-minute window.
- **The deliverable took ~30 minutes** — over-sized ~4× on the window, ~5.5× on the tag.
- **The day's real consumer was absent from the plan**: 210 minutes of Pilot revenue reconciliation, driven by a Gmail thread that was live at 7:30 AM.

**Rule: size from thread velocity, not deadline proximity.** An open correspondence thread with a counterparty actively sending attachments predicts tomorrow's minutes better than any dated deadline on the board. **And name the counterparty who must *receive* the artifact, not the one who produced it** — the 9/23 flag named Dorothy Pavloff (Attivo Ops, who produced the estimate) when the deadline actually belonged to Jennifer Ricafort (the client, not OOO).

## 7. Counterparty volatility and refill

| Disposal mode | 9/22 | 9/23 | Note |
|---|---|---|---|
| Cancelled by counterparty | 1 | 1 | 9/23's was **prompted by Michael** — he asked "anything to go over?", Steve said cancel |
| Moved by counterparty | 1 | 0 | |
| Deleted by Michael | 2 | 2 | includes both containers on 9/23 |
| Evacuated by a competing client | 1 | 1 | |
| Rolled forward by Michael at EOD | 0 | 2 | new mode, see §5 |
| **Retro-filed onto a prior day** | 0 | 1 | **new mode** — see below |

⚠️ **2026-09-22's "three of four disposals were other people's decisions" does not replicate.** On 9/23 it was **one of seven**, and Michael initiated that one. Pooled: **4 of 11.** Do not model block disposal as primarily counterparty-driven.

**Refill: freed time is filled by pulling forward whatever is already booked later that day** (2026-09-23(D)). Steve's 14:30 meeting was cancelled at 14:16:51 and cleared from the calendar at 14:19:06; `INBOX: Admin-Agents Setup`, standing at 17:00–18:00 since 9/21, executed 14:15–15:15 and kept all 60 minutes. Refill latency ≤ 59 min (55 min on 9/22).

**Scheduler consequence, and it is cheap:** freed time cannot be steered by priority after the hour opens — but the block that captures it **does not have to be standing in that hour. It only has to be standing later the same day.** To get the audit backup into a vacated 11:00 slot, it is enough that an audit-backup block exists at 4:00 PM. This is far cheaper than maintaining a deadline-client filler bench.

⚠️ **The hold attracts the client, not the client's dated work** (2026-09-23(C)). On 9/23 Mixmax — the 9/30-deadline client — took 240 of 465 logged minutes, and **zero of them** went to the audit backup. Putting the right client on the calendar is not sufficient; **the block has to name the dated deliverable.**

⚠️ **Focus blocks move in both directions, and internal production work moves *earlier*.** `INBOX: Admin-Agents Setup` moved ~2.75 h earlier on two consecutive days (18:30→16:00, then 17:00→14:15), both times into counterparty-vacated space. The corpus rule that focus blocks move only later (2026-08-13(A), 2026-08-14(H), 2026-08-17(E), 2026-08-28(A)) is **narrowed to client analysis work displaced by incoming client work**. Internal production work is what absorbs freed time, not what yields it.

---

## Known instrument errors

Four measurement hazards that would otherwise corrupt this model silently.

1. **Retroactive blocks are work logs, not plans.** Split blocks created *before* their start (a plan, scoreable) from those created *after* their end (a log). On 2026-09-23, **five of eleven executed blocks were logs** — scoring them would have reported Mixmax 5-for-5 and taught the scheduler that a 45-minute Mixmax block is a reliable forecast.

2. **A retro block dates the work, not the output.** The correspondence lands *later* than the block's own window. A same-window search returns a false negative.

3. **The re-write burst is triggered by a send, not by the clock** (revised 2026-09-23). Blocks are re-timed in clusters of seconds, and everything in a cluster is a log even where an individual `created` stamp predates its start. ⚠️ **The 2026-09-22 reading — that the 12:45 Inbox Triage block is a standing reconciliation ritual and the pre-12:45 snapshot is the only clean record — is falsified.** On 9/23 Inbox Triage moved to 12:30 and the four bursts fired at 14:03, 14:17, 16:20 and 17:05/17:18, **each immediately after an outbound artifact: 77 s, 28 s and 25 s behind an email or Slack message.** The calendar stamp is a **send-receipt**. Search Gmail and Slack in the 0–120 seconds *before* a burst to find what shipped.
   Also: sort by start and subtract pairwise overlap before summing logged minutes, and report the overlap. 9/22 overlapped by 45 min; **9/23 tiled perfectly with zero overlap — read that as a more careful reconstruction, not a more accurate one.** Trust a tidy log's sequence, not its durations.

4. **A block can migrate backwards across days** (2026-09-23(G)). `Scanner | Review FS Package` was placed five times in two days and ended up re-filed onto the *previous* day. A block missing from today at EOD may have been retro-filed to a prior day, not deleted. **Search prior days as well as the forward week, and match on event id, not title.**

---

*Lineage: seeded 2026-09-21 from the ACA v4 specification §6 and §8, cross-checked against the `[ACA]` corpus in [[Open Brain]]. Measurements 2026-09-22 and 2026-09-23 from calendar `created`/`updated` metadata diffed against each day's 7:30 AM snapshot, plus two Fireflies durations. Asana has been unavailable on every run to date, so §1, §2, §5 and §6 remain unmeasured.*

**Revisions** (last ten)

- 2026-09-21 — created, seeded with v4 priors. No measurements.
- 2026-09-22 — first measured values. §3 populated (n=1 day) and **minutes-weighted columns added**. §4 first row. **New §7, Counterparty volatility.** Third instrument error added.
- 2026-09-23 — second measured day. **`verb_class` replaces named/generic as §3's headline split** — production replicates at 140%, coordination at 43%; the title split flips sign and is demoted. **New §0: survival and flag-clearance must be read together**, because minutes-survival ranked the two days backwards. **Containers excluded from the denominator.** 70% cap superseded by a measured two-day 46.2%. §5 gains the EOD roll-burst finding. §6 gains the first scoreable agent sizing error (4× over, and the day's real consumer omitted). §7 narrowed — the counterparty-driven disposal claim does not replicate (4 of 11 pooled) — and gains the pull-forward refill rule and the backwards-migration mode. Instrument error 3's Inbox-Triage-ritual reading **falsified and replaced by the send-receipt mechanism**; fourth instrument error added.
