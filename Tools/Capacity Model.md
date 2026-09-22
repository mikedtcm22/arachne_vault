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

> ⚠️ **MOSTLY STILL ASSUMPTION.** Seeded 2026-09-21 from the priors in the v4 spec §6. **First measurements landed 2026-09-22 (n = 1 day, 6 planned blocks)** and are marked `measured` below; everything unmarked is still a guess recorded so it can be falsified. One day does not make a parameter.

**What this note is.** Only the congealed structure — current parameter values and the rules they imply. It is integrated, maintained and small. It is **not a log**: nightly observations are atomic and stay in [[Open Brain]] as `[ACA-PLAN]` thoughts, per the vault's own promotion rule.

**Update protocol.** `upsert_note` overwrites in full, so the evening run must `read_note` first, merge, and write back. Test **S8** asserts the read preceded the write. Revision line at the foot, capped at the last ten entries. **As a measured value replaces a prior, delete the prior** — this note should shrink as it learns.

---

## 1. What each number actually means

| Tag | Assumed planning minutes | Measured median | n | Drift |
|---|---|---|---|---|
| `1` | 30 | — | 0 | — |
| `2` | 90 | — | 0 | — |
| `3` | 165 | — | 0 | — |
| `4` | not schedulable | n/a | n/a | decompose marker, not a size |

Still unmeasured: tags are readable only through Asana, which has been unavailable on every run to date. **Nothing in §1 can move until the connector is authorised.**

**Adjacent measurement that does not need tags** (2026-09-22, n = 2): **externally-organised meetings ran 117% of their booked minutes** — Kestrel 40 against a 30-minute booking, DeepScribe×Tabs 61 against 60. Both overran; neither under-ran. Treat a counterparty's booking as a floor, not a box.

## 2. What each letter actually means

Completion rate for `H` / `M` / `L` by time-of-day window. Still entirely unmeasured — letters live in Asana tags.

| Window | `H` | `M` | `L` |
|---|---|---|---|
| 8:30–11:00 | — | — | — |
| 11:00–1:00 | — | — | — |
| 1:00–4:00 | — | — | — |
| 4:00–6:00 | — | — | — |

**Seed placement priors:**

- `H` → the first contiguous window of ≥90 min after 9:00. ⚠️ The spec attributes this to Lesson 2026-08-18(A), which **did not surface in the Open Brain corpus on 2026-09-21**. Treat as uncited until found or replaced by measurement.
- `M` → mid-morning through mid-afternoon.
- `L` → fragments, post-meeting recovery, late afternoon.
- Daily `H` budget: **3 hours**, no two cross-client `H` tasks adjacent. Pure guess.

## 3. Survival rate — the most urgent number

What share of planned blocks actually run. This replaces the **70% capacity cap**, which is a placeholder.

**⚠️ THE BINARY RATE IS THE WRONG INSTRUMENT ON ITS OWN** (measured, 2026-09-22). A block can appear on the executed calendar under its own name while keeping an eighth of its minutes: `Mixmax | Audit Updates` was planned 9:00–11:00 (120 min) and executed 10:15–10:30 (15 min), and scores "ran shifted" — i.e. *survived*. **Record planned minutes and logged minutes per block, not merely ran / shifted / rolled / dropped.**

| Client | Planned blocks | Ran as planned | Shifted | Rolled | Dropped | Survival (binary) | Planned min | Logged min | **Survival (minutes)** |
|---|---|---|---|---|---|---|---|---|---|
| Scanner | 3 | 2 | 1 | 0 | 0 | 100% | 150 | 210 | **140%** |
| Mixmax | 1 | 0 | 1 | 0 | 0 | 100% | 120 | 15 | **12.5%** |
| Attivo (internal) | 1 | 0 | 1 | 0 | 0 | 100% | 60 | 60 | 100% |
| *(unassigned `[HOLD]`)* | 1 | 0 | 0 | 0 | 1 | 0% | 30 | 0 | 0% |
| **Total (n = 1 day)** | **6** | **2** | **3** | **0** | **1** | **83%** | **360** | **285** | **79%** |

Restricted to the four blocks that existed at the 7:30 AM snapshot (the cleanest adherence measure): **165 logged of 240 planned = 68.8%.** First real datum against the 70% seed cap, and it lands almost exactly on it — coincidence at n=1, but worth watching before the cap is moved.

The corpus reason to expect worse, retained: self-scheduled focus blocks are the schedule's shock absorber, sacrificed first and moved *later* rather than earlier (2026-08-13(A), 2026-08-17(E) — one block placed seven times in five business days; 2026-08-28(A); 2026-06-09(B), 2026-06-11(A)). ⚠️ **2026-09-22 produced one counter-case**: `Attivo | Admin-Agents Setup` moved *earlier*, 18:30 → 16:00, into freed time. Blocks move toward opened space in both directions, not only later.

### The split worth instrumenting first — named deliverable vs. generic title

**2026-09-02(A)** put named-deliverable blocks at 7-for-7 and explicitly bounds **2026-08-28(A)** to generic days. First measurement, 2026-09-22, six planned self-scheduled blocks:

| Title type | Planned | Survived (binary) | Binary rate | Planned min | Logged min | **Minutes rate** |
|---|---|---|---|---|---|---|
| Names a deliverable | 2 | 2 | 100% | 90 | 150 | **167%** |
| Generic / topic only | 4 | 3 | 75% | 270 | 135 | **50%** |
| `verb_class: production` | 2 | 2 | 100% | 90 | 150 | **167%** |
| `verb_class: coordination` | 4 | 3 | 75% | 270 | 135 | **50%** |

**Worst cell: generic + coordination — 210 planned minutes, 75 logged, 36%.**

⚠️ **The two splits are confounded at n = 6**: three of the four generic blocks are also coordination. The two cells that separate the axes both held 100% of their minutes — `Attivo | Admin-Agents Setup` (generic + production) and `Scanner | Review FS Package` (named + coordination). That weakly suggests the **combination** is the predictor rather than either axis alone. **Do not act on this until a day separates them.**

## 4. Switching cost

Client-context count per day against completion rate. Seed rule: **maximum five distinct client contexts per day**, batched contiguously.

| Contexts in day | Days observed | Mean completion (minutes basis) |
|---|---|---|
| 4 (+1 internal) | 1 | 79% |

2026-09-22: Scanner, Mixmax, Kestrel, DeepScribe, plus internal Attivo admin. Inside the seed limit. **Contiguity was violated and it did not cost anything measurable** — Scanner ran in three separate windows (9:15, 11:45, 16:15), but each break contained a forcing external meeting, and Scanner was the day's highest-completion client.

## 5. Roll history

Which Workstreams chronically fail to survive — diagnostic of **scoping**, not of discipline. A task at three rolls stops being silently re-planned and becomes a flag.

| Workstream | Rolls | Status |
|---|---|---|
| Scanner \| Close: Aug Revenue | 5 (as of 2026-09-15) | past the flag threshold; unverifiable until the connector returns |

⚠️ `rolls:` has never been readable or writable — it is an Asana fenced-block field. **0 increments have ever been applied.** On 2026-09-22 nothing was increment-able: the single dropped block (`[HOLD]`) carries no task.

## 6. Tag-prediction accuracy

How often the agent's proposed tag pair survives Michael's review.

| | Proposed | Unchanged by MC | Corrected | Accuracy |
|---|---|---|---|---|
| Number | 0 | 0 | 0 | — |
| Letter | 0 | 0 | 0 | — |

⚠️ **This stream cannot open until the EOD Planner runs once.** Zero proposals exist because no agenda has ever been produced. The connector cannot write tags, so every proposal lives in the fenced `--- agent ---` block as `tags:` + `tag_source: agent`, and Michael's correction is observed by comparing the native tag against that field.

## 7. Counterparty volatility

**New section, 2026-09-22.** The corpus has treated block disposal as a property of Michael's discipline. On the first measured day, **three of four disposals were other people's decisions.**

| Disposal mode | Count (2026-09-22) | Example |
|---|---|---|
| Cancelled by counterparty | 1 | ResFrac weekly, cancelled 9:04 AM |
| Moved by counterparty | 1 | Steve Nathan check-in → Fri 9/25, moved 11:20 AM, ten minutes before start |
| Deleted by Michael | 2 | `[HOLD]`; `Out of office (dentist)`, freeing 2 hours |
| Evacuated by a competing client | 1 | `Mixmax \| Audit Updates` 120 → 15 min, displaced by Scanner |

**Refill latency: 55 minutes** — ResFrac cancelled 9:04:22 AM, `Scanner | Revenue Review` created 9:59:51 AM for the vacated slot.

**Refill destination: the client already in hand, not the client with the deadline.** All four freed hours went to Scanner, which carries no dated deadline; Mixmax, carrying the 9/30 audit and a one-day estimate window, kept 15 minutes. **Scheduler consequence: freed time cannot be steered by priority after the fact. A deadline client's block has to be standing there before the hour opens.**

---

## Known instrument errors

Three measurement hazards that would otherwise corrupt this model silently.

1. **Retroactive blocks are work logs, not plans.** Michael creates named calendar blocks *after* doing the work — 2026-09-04(C) found one created eight minutes after the artifact it names was emailed; 2026-09-21(E) found a 1:30–2:00 PM block created at 5:20 PM. Split blocks created *before* their start (a plan, scoreable) from those created *after* their end (a log). Scoring the second kind as plan adherence measures nothing.

2. **A retro block dates the work, not the output.** Per 2026-09-21(E) the correspondence out of a retro block lands *later* than the block's own window — 3h45m later in the observed case. A same-window search returns a false negative.

3. **Retro-logged blocks overlap, and they are re-written in bursts** (2026-09-22(D)). On 2026-09-22 Michael re-timed three morning blocks in **six seconds** at 12:47 PM, from inside his 12:45 Inbox Triage block, and two afternoon blocks 33 seconds apart at 5:33 PM. The afternoon pair **overlaps by 45 minutes and cannot both be true.** Two rules: (a) sort by start and subtract pairwise overlap before summing logged minutes, and report the overlap rather than resolving it silently — the overlap measures how approximate the log is; (b) **a cluster of `updated` stamps within seconds of each other is a re-write burst**, and everything in it is a log, even where an individual block's `created` stamp predates its start. The 12:45 Inbox Triage block looks like a standing reconciliation ritual, which makes the **pre-12:45 snapshot the only clean record of the morning's intent.**

---

*Lineage: seeded 2026-09-21 from the priors in the ACA v4 specification §6 and §8, cross-checked against the `[ACA]` lesson corpus in [[Open Brain]]. First measurements 2026-09-22 from calendar `created`/`updated` metadata diffed against that morning's 7:30 AM snapshot, plus two Fireflies durations. Asana has been unavailable on every run to date, so §1, §2, §5 and §6 remain unmeasured.*

**Revisions** (last ten)

- 2026-09-21 — created, seeded with v4 priors. No measurements yet.
- 2026-09-22 — first measured values. §3 survival populated (n=1 day, 6 blocks) and **minutes-weighted columns added** — the binary rate alone scored a 120→15 min collapse as a survival. §3 named/generic and verb_class splits populated with the n=6 confounding stated. §4 first row. **New §7, Counterparty volatility** — three of four disposals were other people's decisions; refill latency 55 min. Third instrument error added (retro-log overlap + re-write bursts). Corpus claim that focus blocks move only later is narrowed by one counter-case.
