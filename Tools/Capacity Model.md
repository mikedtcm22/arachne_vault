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

> ⚠️ **PARTLY MEASURED.** Seeded 2026-09-21 from the priors in the v4 spec §6. **Measurements from seven days — 2026-09-22 to 09-25, 09-28, 09-29 and 09-30, 30 scoreable blocks** — are marked below; everything unmarked is still a guess recorded so it can be falsified.
>
> ⚠️ **FOUR CONSECUTIVE DAYS HAVE NOW FALSIFIED A CLAIM FITTED AT n≤5 ON ITS FIRST OUT-OF-SAMPLE TEST** — 9/28 the production rule, 9/29 the narrowed production form and the title axis, 9/30 the commitment-deferral rule. **This is the most robust finding in the note and it is about the loop, not about Michael.** A claim fitted at n≤5 is written **with its own falsification test attached** and is never read into a scheduler rule or a displacement proposal before that test has run. The one thing that worked on 9/30 was a rule used as a test rather than as a fact.

**What this note is.** Only the congealed structure — current parameter values and the rules they imply. It is integrated, maintained and small. It is **not a log**: nightly observations are atomic and stay in [[Open Brain]] as `[ACA-PLAN]` thoughts.

**Update protocol.** `upsert_note` overwrites in full, so the evening run must `read_note` first, merge, and write back. Test **S8** asserts the read preceded the write. Revision line at the foot, capped at the last ten entries. **As a measured value replaces a prior, delete the prior** — this note should shrink as it learns.

---

## 0. The two axes — read them together or not at all

**Minutes-survival alone has now ranked the measured days wrongly in five different directions.**

| Day | Minutes survival | Logged min | Flags cleared | Outbound artifacts | Verdict |
|---|---|---|---|---|---|
| 2026-09-22 | 68.8% | 165 | 0 of 8 | — | high survival, lowest output |
| 2026-09-23 | 30.4% | 105 | **2 of 8**, both top-ranked | 2 emails | better than 9/22 |
| 2026-09-24 | 16.7% | 15 | 2 of 16, one red | 2 emails + 5 Slack + 1 Doc | worst survival, strong output |
| 2026-09-25 | 26.7% | 60 | **3 of 12** | 1 email + 1 Slack DM | mid on both |
| 2026-09-28 | 58.3% | 210 | 2 of 14 | 1 email, 330 min on one client thread | high survival, thin output |
| 2026-09-29 | **71.4%** *(frozen)* | 225 | **3 of 18** + 4 clocks reset | 6 emails + 1 Slack | best day on BOTH axes at once |
| **2026-09-30** | **27.3%** | **360** | **3 of 22**, at 1, 3 and 4 bd | **4 emails + 3 Slack** | ⚠️ **low survival, HIGHEST output and highest logged minutes** |

⚠️ **9/30 is the cleanest demonstration that survival measures adherence to a morning board, not productivity.** 165 minutes were planned; 360 exclusive minutes were worked, with **zero block-on-block overlap**; the morning board was replaced wholesale between 10:54 and 13:27 CT and the replacement was then worked completely. **On a day of wholesale intraday re-planning, survival measures almost nothing.**

**Survival and output are uncorrelated, not anti-correlated** (n=7). Neither predicts the other; both must be reported, always alongside **logged minutes**, **flags cleared** and **artifacts**.

⚠️ **And neither predicts the deadline.** On 9/30 both 9/30-dated red items — the Mixmax audit backup and the DeepScribe/Tabs cleanup — took zero minutes for a tenth consecutive day and their date passed. **A good day and a day that clears its deadlines are different things, and only the flag list tracks the second.**

## 1. What each number actually means

| Tag | Assumed planning minutes | Measured median | n | Drift |
|---|---|---|---|---|
| `1` | 30 | — | 0 | — |
| `2` | 90 | — | 0 | — |
| `3` | 165 | — | 0 | — |
| `4` | not schedulable | n/a | n/a | decompose marker, not a size |

Tags are readable only through Asana, unavailable on all **sixteen** runs to date. **Nothing in §1 can move until the connector is authorised.**

**Adjacent measurement that does not need tags** (n=6): **externally-organised meetings run 100.5% of their booked minutes** — 221 of 220. Individual observations range **37.5% to 152%**. At n=6 a counterparty's booking is an estimate with a wide **two-sided** error. **Plan no cascade around an assumed overrun.**

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
| 2026-09-25 | 4 | 2 | 225 | 60 | **26.7%** |
| 2026-09-28 | 5 | 3 | 360 | 210 | **58.3%** |
| 2026-09-29 | 6 | 3 + 1 partial | 315 | 225 | **71.4%** — **FROZEN**, see instrument error 5 |
| **2026-09-30** | **4** | **0 + 1 partial** | **165** | **45** | **27.3%** |
| **Pooled** | **31** | **14** | **1740** | **825** | **47.4%** |

**47.4% is the working figure, and it has now moved 46.2 → 42.2 → 38.3 → 43.4 → 49.5 → 47.4 across six revisions — in both directions three times.** Band **16.7–71.4%**. **The honest statement is "roughly half, banded 17–71%." Do not hard-code 47 any more than 38 or 70.**

⚠️ **Part of the non-convergence was self-inflicted and is now fixed.** Until 2026-09-30 a prior day could be re-scored every time Michael re-timed it, so the denominator's history was mutable. Instrument error 5 now freezes each day at the run that measured it.

### ⚠️ Bimodality is WEAKENED — the decomposition exception is no longer the only one

**Rule as it stood:** a block runs whole or vanishes whole **unless it is decomposed**, and a decomposed block's partial equals the sum of its named pieces (2026-09-25(F), 2026-09-28(F), 2026-09-29(F)).

**Nineteen blocks over four days now give two intermediate outcomes, and only one is a decomposition.** 9/29's `Monthly Close Prep` split cleanly, 45 = 15 + 30. On 9/30 `Scanner | Deal-Tracking: New Invoice Process` (`453ht69jhk89s9i8lpcri7qoa5`) was planned 60 and ran 45 — **same event id, no split, a straight 25% haircut.** A competing reading is recorded and **not** promoted: an adjacent 30-minute Scanner work-log block on the same contract→revenue process may make it a decomposition that over-delivered (75 against 60).

**Still size at nominal**, still expect run-or-vanish, but **stop stating decomposition as the only exception**. The prediction target remains **which** blocks vanish, not by how much each shrinks.

### ⚠️ The title axis is CONTAMINATED — contamination is broader than first described

| Title type (scored at the morning snapshot) | Day-rates |
|---|---|
| Names a deliverable | 167%, 30%, 100%, 100%, 118%, 66.7%, **42.9%** |
| Generic / topic only | 50%, 80%, 0%, 15.4%, 0%, 75.0%, **0%** |

**2026-09-29(B)** found Michael renaming a generic block to a named one **seven minutes after it ran** and concluded he retitles once he knows what he did. **2026-09-30 found two renames that do not fit that shape:**

- `Monthly Close Prep (...)` — generic, at two rolls, **never ran** — renamed `Asana-Agent | Add'l Setup, Tagging & Task Review` at 17:27:06 while being rolled. **Generic became named on a block that did not run**, at the moment he decided what he *would* do in it.
- `Scanner | Deal-Tracking: New Invoice Process` → `Scanner | Documentation: New Contract > Revenue Process` at 12:53:10 — a **named-to-named refinement**, a category the axis has no bin for.

**Titles move in both directions and for two different reasons: retrospective description of work done, and prospective specification of work intended.** Scoring at the 07:30 snapshot handles both going forward, but **the axis cannot be re-derived from historical EOD boards at all** — the corpus cannot tell which kind of rename produced each title.

**MANDATORY: score a block's title AS IT STOOD IN THE MORNING SNAPSHOT.** The axis stays **CONTAMINATED** and scheduler rule 3 stays **SUSPENDED**.

### `verb_class`

| `verb_class` | Blocks | Planned min | Logged min | **Rate** | Replicates? |
|---|---|---|---|---|---|
| **coordination** | 22 | 1290 | 630 | **48.8%** | **yes, n=7 days** — 50%, 30%, 44%, 27%, 58%, 89%, 0% |
| **production** | 8 | 510 | 330 | **64.7%** | n=4 days — was 79.2%, fell 14.5 points on 9/30 |

**Scheduler rules from this section:**
1. Size a block at **nominal**, and expect it to run or vanish — not to shrink.
2. **Anchor it to the venue that forces it.** ✅ Supported at n=1 (2026-09-29(D)). **Corollary, and 9/30 gives it a second edge:** when a counterparty moves a meeting, look for a prep block anchored to it before treating the freed window as capacity — and when the venue *runs*, expect the prep block to be **deleted rather than rolled**. `Paulex | NIH Grant Research` (`1co6khjiailhcme08eqg5okatk`) was deleted on 9/30 after its Paulexbio sync went ahead at 12:30.
3. ~~Prefer a title that names its artifact.~~ **SUSPENDED** — see the contamination warning above.
4. **Do not encode `verb_class` as a scheduler rule at n=7.** Propose the window and name the artifact; leave the verb to Michael.

## 4. Switching cost

| Contexts in day | Days | Completion (minutes basis) |
|---|---|---|
| **5** | 1 | **71.4%** |
| 4 (+1 internal) | 2 | 79%, **27.3%** |
| 3 (+1 internal) | 1 | 27% |
| 2 (+1 internal) | 3 | 30%, 17%, 58.3% |

⚠️ **The seed cap of five is REFUTED, not merely un-approached** — it was reached on the highest-survival day, and 9/30's four contexts produced the lowest-survival / highest-output day. **Seven days, no relationship in either direction.** Keep G5 as a reporting line, not as a constraint on the scheduler.

## 5. Roll history

A task at three rolls stops being silently re-planned (engine rule 9). **Disposal set: cut the scope · hand it off · accept the slip · REPURPOSE the hour.**

⚠️ `rolls:` has never been readable or writable. **0 increments across sixteen runs, against 13 directly observed rolls.**

| Block / workstream | Observed rolls | Status |
|---|---|---|
| `Monthly Close Prep (...)` (`07b3d937if5c2v2dljba475qvf`) | **3 — THRESHOLD REACHED** | ✅ **DISPOSED BY REPURPOSING**, not re-planned. Renamed `Asana-Agent | Add'l Setup, Tagging & Task Review`, 10/1 16:00–17:00, same event id and same hour. **Michael reached rule 9's threshold independently for the second time, before any flag reached him** |
| `DeepScribe \| New Update/Agenda Doc` (`2actpm6je9f415eegpm6f5tt1d_…`) | **1** (9/30→10/1) | Rolled to 10/1 10:00–10:30 and **grown 15 → 30** |
| `Paulex \| NIH Grant Research` (`1co6khjiailhcme08eqg5okatk`) | 1, **frozen** | **DELETED 9/30** once its venue ran. Not a roll — a new disposal mode, §7 |
| `Scanner \| Invoicing/Revenue Updates` (`5k3hffa1uap4kj2p0h3qfho3u9`) | 2, frozen | ✅ Ran 9/29, 90 of 90 |
| `Client/Double Review (...)` (`7u71d6h0k1grovgju1jgeao76c`) | 3, final | **DELETED 2026-09-25** at its fourth placement — rule 9's "cut it" reached independently, the first time |
| `Scanner \| Close: Aug Revenue` | 5 (as of 2026-09-15) | past threshold; unverifiable until the connector returns |
| Mixmax audit backup `C-20260917-05` · DeepScribe/Tabs `C-20260910-05` | **n/a — never placed** | **Worse than rolled.** Ten days flagged, zero minutes, **both dates now passed.** ⚠️ The audit got its **first-ever block** on 10/1 10:30–12:30, the day *after* it was due |

**An hour that has survived three rolls is an hour Michael intends to keep.** At three rolls the useful question is **what should occupy it**, not whether to re-place the original task.

**Rolls are written when the displacing work takes the window**, anywhere in the day. **Some rolls are already visible at 4:15 PM on most days** — read the calendar; do not assume they cannot be there.

## 6. Tag-prediction accuracy

| | Proposed | Unchanged by MC | Corrected | Accuracy |
|---|---|---|---|---|
| Number | 6 | 0 | 0 | **unmeasurable** |
| Letter | 6 | 0 | 0 | **unmeasurable** |

⚠️ This stream cannot open until the EOD Planner runs once and Michael sets a real tag against an agent proposal. **The EOD Planner has still never fired.**

**Target selection — eight proposals, seven content misses, and then a hit:**

| Day | Proposed | Result |
|---|---|---|
| 9/23–9/28 | four proposals | window and/or verb class wrong every time |
| 9/29 | `1L`, reply to Jennifer on the $14.8–15.0k range, into the only free window | client HIT, counterparty HIT, **thread MISS** |
| **9/30** | **`1L`, confirm the sales-assist attribution treatment in ARR Plan vs Actual, to Jason Tatum and Viola Melis in `#attivo-mixmax`** | ⚠️ **client, counterparty, thread and CONTENT all HIT. Window MISS** — it landed 16:10–16:29, not in the proposed 13:15–14:30 |

**At n=8 the split is that the agent can name WHAT Michael will do and cannot name WHEN.** That is the right way round — the artifact matters and the hour does not. **Stop scoring window placement as part of proposal accuracy.**

### ANSWERABILITY SELECTS THE THREAD — and the price dimension is a LATENCY, not a refusal

**He answers what he can answer from knowledge in one or two lines, roughly in arrival order.**

⚠️ **"He defers what commits his firm to a price" is DELETED.** It was staked falsifiably on 9/30 and failed. Jennifer Ricafort's *"is $14,800–$15,000 a reasonable monthly range?"* — unread and starred at 27 hours on 9/29 — was answered at **09:28:25 on 9/30 in one line**: *"Yes, that sounds like a reasonable estimate."* She acknowledged in 75 seconds. Total latency 1 d 18 h 54 m, against 53 and 60 minutes for two knowledge questions the same day.

**Replacement, stated as a latency prior:** a **price commitment is slept on, not refused** — roughly two days where a knowledge answer takes hours — and it is answered **first thing in the morning**, not in the thread's own window. *Newest live thread* survives only as a predictor of **client**.

**Generalise:** a rule whose evidence is a *delay* must be written as a latency prior, never as "he will not do X."

⚠️ **CHANNEL SILENCE IS A MEDIUM PREFERENCE, NOT UNRESPONSIVENESS.** Flag the *ask*, not the channel. ⚠️ **But the converse now also holds:** on 9/30 Michael cleared a 4-business-day Slack ask **in the channel** (16:10:40) *and* by email (17:38:53). Medium preference is not stable per counterparty; do not infer the medium of the answer from the medium of the ask.

**A displacement proposal is stale if a counterparty posted after it was written.**

**Name the counterparty who must *receive* the artifact, not the one who produced it.**

⚠️ **A parameter written here but not read into the proposal is not part of the engine** (2026-09-24(K)). **Every displacement proposal must name which rule of this note it applied.** The 9/30 hit named three and all three held.

⚠️ **Do not withhold the highest-value item from the proposal because the model predicts deferral.** The 9/30 morning run deliberately did not propose Jennifer's pricing reply, on the model's own prediction that it would be deferred a third day. He answered it 2 h 12 m after the doc was written. **Optimising a proposal for predicted uptake rather than for value is how the loop learns to be agreeable instead of useful.**

## 7. Counterparty volatility and refill

| Disposal mode | 9/22 | 9/23 | 9/24 | 9/25 | 9/28 | 9/29 | **9/30** | Note |
|---|---|---|---|---|---|---|---|---|
| Cancelled by counterparty | 1 | 1 | 1 | 0 | 0 | 0 | 0 | |
| Moved by counterparty | 1 | 0 | 0 | 0 | 0 | 1 | **1** | ale@ moved the Paulexbio sync 12:00 → 12:30 |
| Deleted by Michael (containers) | 2 | 2 | 3 | 1 | 0 | 0 | **2** | |
| Moved within the day by Michael | — | — | 3 | 4 | 6 | 8 | **11** | **new maximum** — the whole anchor spine plus the board |
| Evacuated by a competing client | 1 | 1 | 0 | 1 | 0 | 0 | 0 | |
| Evacuated by the SAME client's other work | — | — | — | — | 2 | 1 | 0 | |
| Rolled forward by Michael | 0 | 2 | 1 | 1 | 2 | 2 | **2** | |
| Rolled WITH its venue | — | — | — | — | — | 1 | 0 | |
| **Deleted once its venue RAN** | — | — | — | — | — | — | **1** | ⚠️ **new** — the prep block's reason to exist was discharged, §3 rule 2 |
| Retro-filed onto a prior day | 0 | 1 | 0 | 0 | 0 | 1 | 0 | ⚠️ the 9/29 instance was **reversed** on 9/30 |
| Retro-filed onto a LATER day | — | — | — | 1 | 0 | 0 | **1** | `Scanner \| Monthly Close Prep` moved 9/29 → 9/30 |
| Disposed by scheduling a meeting | 0 | 0 | 1 | 0 | 1 | 0 | 0 | |
| Deleted outright at the roll threshold | 0 | 0 | 0 | 1 | 0 | 0 | 0 | |
| **Repurposed at the roll threshold** | — | — | — | — | — | — | **1** | **new** — §5 |
| Decomposed in arrears | — | — | — | — | — | 1 | 0 | |
| Deferred past 17:00 within the day | — | — | — | — | 2 | 2 | **1** | |

⚠️ **Block disposal is not primarily counterparty-driven.** Pooled: **7 of 65.** **It is overwhelmingly Michael re-planning his own day intraday** — 11 within-day moves on 9/30 alone.

**Discharge-by-meeting** (2026-09-24(F), narrowed 2026-09-25(L)): when a flagged item acquires a dated venue **with the counterparty in it**, it stops being overdue. **A solo prep block does not discharge anything.**

⚠️ **ARRIVAL RECENCY BEATS DEADLINE PROXIMITY EVEN WHEN THE ARRIVING ITEM HAS NO DATE AND NO OWNER** — n=4 (2026-09-25, 2026-09-28(J), 2026-09-29, **2026-09-30**). On 9/30, five threads that arrived inside 48 hours took 360 minutes between them and the two dated red items took zero and expired. **This is the model's most reliable predictor of where a day's minutes go, and the scheduler cannot fix it — only the flag list can.**

⚠️ **And on 9/30 the flag list did not fix it either.** Ten consecutive days of a red flag produced no block; the audit acquired one the day after a live counterparty resurfaced on its thread. **A dated venue with a counterparty in it appears to be the only reliable forcing function.**

**Refill: freed time is filled by re-pointing a block that already exists somewhere on the same day.** Latency 52–59 min at n=3, not re-measured since 9/24.

⚠️ **Size a capture block to the vacancy plus the soft time abutting it.** Declined, tentative and externally-organised blocks are not occupied time.

⚠️ **Focus blocks move in both directions and in three senses** — to another date, later past 5:00 PM, and earlier within the day.

---

## Known instrument errors

Seven measurement hazards that would otherwise corrupt this model silently.

1. **Retroactive blocks are work logs, not plans — the test is `updated` vs `end`, NOT `created` vs `start`.** **An event whose last `updated` stamp post-dates its own `end` is retroactively placed and cannot be scored for plan adherence, however old its `created`.** Counts: 9/23 five of eleven, 9/24 four of seven, 9/25 four of ten, 9/28 one of seven, 9/29 three pure logs plus one in-flight, **9/30 two pure logs plus three in-flight**.
   - **A block created *during* its own window is in-flight — treat it as a log, and say so.** 9/30 gives three at once: `Mixmax | Pricing Model - Add Churn Assumptions` (created 10:57:27 onto 09:45–11:00), `Kestrel | Accounting Admin/Follow-ups` (13:24:16 onto 13:00–13:30), `Mixmax | Pricing Pitch` (15:47:19 onto 15:45–17:15, 2 m 19 s in). The mode is now common, not exceptional.
   - ⚠️ **Apply the test to the block's position AT THE MOMENT IT IS SCORED.** **Anchor to the 07:30 snapshot: a block present there with `created` before its start is a plan, whatever happens to its stamps afterwards.**
   - ⚠️ **A block created before its start but AFTER the 07:30 snapshot is an intraday plan, not a log.** 9/30's `(timesheet)` (created 11:53:52 for 15:00) and `Benchmark | Data Spot-check` (13:27:13 for 14:00) are genuine plans written 3 h 06 m and 33 min ahead. They are **not scoreable against the morning board** and must not be dropped — report them as intraday plans.

2. **A retro block dates the work, not the output.** The correspondence lands *later* than the block's own window — **n=6, range 8 min to 3 h 45 m** (8 min 9/04, 27 min 9/25, 33 min and 1 h 25 m 9/29, 3 h 45 m 9/21, **23 min 53 s 9/30**). The send **always follows** the block, never precedes it. **Search forward from the block's end to the end of the next admin anchor; a same-window search returns a false negative.**

3. **Classify a burst by the dates it writes — per block, because a burst can be MIXED.** A **log-burst** re-times *today* or a prior day. A **plan-burst** writes *future* dates.
   ⚠️ **The plan-burst's location is UNCONSTRAINED — search the whole day INCLUDING the anchors.** "Not inside `INBOX Review + Next Day Planning`" was falsified 2026-09-28(H) and replicated 9/29; on **2026-09-30 the 10/1 plan-burst ran 17:25:57–17:28:01, entirely inside the 17:15–17:45 `INBOX Review` block.** A rule falsified as "always" must not be carried forward as "never."
   Also: **sort by start and subtract pairwise overlap before summing logged minutes, and report the overlap.** Trust a tidy log's sequence, not its durations.

4. **A block missing from today may have migrated in EITHER direction — match on event id, never on title or absence.** 9/30: `Scanner | Monthly Close Prep` migrated 9/29 → 9/30; `Monthly Close Prep (...)` and `DeepScribe | New Update/Agenda Doc` migrated to 10/1 under a new name and a new duration. ⚠️ **Use the FULL event id**: a truncated id returns *"could not be found or has been deleted"* — indistinguishable from a real deletion. ⚠️ **And confirm a deletion with a title search as well as an id lookup** before recording one: on 9/30 `Paulex | NIH Grant Research` was confirmed deleted only because a `search_events` on its title returned a single unrelated 9/28 instance.

5. **A scored block's calendar position is mutable after the run that scored it — SO FREEZE THE DAY.** 2026-09-29 has been scored **three times**: 71.4% by its own evening run, 100% by the 9/30 morning run after a 12-second tidy that night, and 109.5% after a second tidy at 10:54–11:51 on 9/30 that moved five more blocks and reversed 9/28's amendment.
   ⚠️ **RULING (2026-09-30): the measurement of record for a day is the one taken by that day's own evening run, against the stamps closest to the events.** A later re-time is recorded as **calendar churn** against that day, not as a new measurement. A day is re-scored **at most once**, and only to correct a *named* instrument error. **9/29 is frozen at 225/315 = 71.4%.** Without this the pooled series has a mutable history and cannot converge by construction.
   **Per-block minutes remain provisional within the run that takes them; anchor durable measurements to send timestamps, which do not move.**

6. **Client work product is structurally invisible, so a production block's output can never be observed.** The Google Drive connector authenticates as `michael.p.christopher@gmail.com`, **not** the Attivo Workspace. **Record production output as unobservable, exactly as Suralink, Rippling, Ramp and the portal layer are. Never score a production block as having produced nothing.**

7. **The umbrella block: a late-day extension can swallow other blocks, and its face duration double-counts them.** **When an extended block contains other named blocks, its EXCLUSIVE minutes are the honest figure.** ⚠️ 9/30 had **zero** overlap across eight logged blocks — a fully contiguous board — so the hazard is intermittent, not structural, and the overlap figure must be reported either way.

---

*Lineage: seeded 2026-09-21 from the ACA v4 specification §6 and §8, cross-checked against the `[ACA]` corpus in [[Open Brain]]. Measurements 2026-09-22 to 2026-09-30 from calendar `created`/`updated` stamps diffed against each day's 7:30 AM snapshot and reconciled against Gmail sent, Slack read by channel id and by thread, and Drive. Asana has been unavailable on all sixteen runs, so §1, §2, §5 and §6 remain unmeasured; the EOD Planner has never run, so no agent-authored agenda has ever been scored.*

**Revisions** (last ten)

- 2026-09-22 — first measured values. §3 populated (n=1) and minutes-weighted columns added. §4 first row. New §7. Third instrument error added.
- 2026-09-23 — second measured day. `verb_class` replaces named/generic as §3's headline split. New §0. Containers excluded from the denominator. 70% cap superseded. §5 gains the EOD roll-burst finding. §7 narrowed; fourth instrument error added.
- 2026-09-24 — third measured day. Coordination replicates. Pooled 46.2% → 42.2%. §7 gains discharge-by-meeting and the soft-time-overflow rule. Instrument error 3 split into log- and plan-bursts; error 4 widened.
- 2026-09-25 — fourth measured day, first withdrawal of a prior measurement. Pooled 42.2% → 38.3%. §3 gains the bimodal-survival warning. Instrument error 1 rewritten around `updated` vs `end`; new error 5.
- 2026-09-28 — fifth measured day, first falsification of the model's strongest claim. Pooled 38.3% → 43.4%. *Never propose production* **deleted**. Title axis promoted. New error 6.
- 2026-09-29 — sixth measured day; best on both axes (71.4%). Pooled 43.4% → 49.5%. **Title axis DEMOTED to CONTAMINATED**; scheduler rule 3 SUSPENDED. Scheduler rule 2 promoted at n=1. §1's overrun collapsed to 100.6% and *treat a booking as a floor* withdrawn. §6's *newest live thread* replaced by answerability. New error 7, the umbrella block.
- **2026-09-30 — seventh measured day; lowest survival (27.3%) on the highest-output day (360 logged min, 4 emails + 3 Slack, 3 flags cleared).** Pooled **49.5% → 47.4%**; production 79.2% → **64.7%**. **§0 gains a fifth direction in which survival ranks a day wrongly.** **Instrument error 5 gains the FREEZE RULE and 9/29 is frozen at 71.4%** after reading 71.4 / 100 / 109.5 on three successive boards. **Instrument error 3's "plan-burst is not inside `INBOX Review`" replaced by "location unconstrained"** — tonight's burst was inside it. **§6's commitment-deferral rule DELETED and restated as a latency prior** after Jennifer's price question was answered in one line; §6 gains *do not withhold the highest-value item because the model predicts deferral*, and target selection records its **first content hit in eight proposals**. **§3 bimodality WEAKENED** — first partial that is not a decomposition. **§5 and §7 gain REPURPOSED at the roll threshold** (`Monthly Close Prep` at 3 rolls → `Asana-Agent | Add'l Setup, Tagging & Task Review`) **and DELETED-ONCE-ITS-VENUE-RAN**. §4's five-context cap stays refuted. Errors 1, 2 and 4 gain the intraday-plan row, n=6, and the title-search confirmation.
