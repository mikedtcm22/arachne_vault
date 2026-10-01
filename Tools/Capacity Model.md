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

> ⚠️ **PARTLY MEASURED.** Seeded 2026-09-21 from the priors in the v4 spec §6. **Measurements from eight days — 2026-09-22 to 09-25, 09-28, 09-29, 09-30 and 10-01, 36 scoreable blocks** — are marked below; everything unmarked is still a guess recorded so it can be falsified.
>
> ⚠️ **FIVE CONSECUTIVE DAYS HAVE NOW FALSIFIED A CLAIM FITTED AT n≤5 ON ITS FIRST OUT-OF-SAMPLE TEST** — 9/28 the production rule, 9/29 the narrowed production form and the title axis, 9/30 the commitment-deferral rule, **10/1 the repurposed-hour rule** (written last night at n=1; the hour rolled the next day). **This is the most robust finding in the note and it is about the loop, not about Michael.** A claim fitted at n≤5 is written **with its own falsification test attached** and is never read into a scheduler rule or a displacement proposal before that test has run.

**What this note is.** Only the congealed structure — current parameter values and the rules they imply. It is integrated, maintained and small. It is **not a log**: nightly observations are atomic and stay in [[Open Brain]] as `[ACA-PLAN]` thoughts.

**Update protocol.** `upsert_note` overwrites in full, so the evening run must `read_note` first, merge, and write back. Test **S8** asserts the read preceded the write. Revision line at the foot, capped at the last ten entries. **As a measured value replaces a prior, delete the prior** — this note should shrink as it learns.

---

## 0. The two axes — read them together or not at all

**Minutes-survival alone has now ranked the measured days wrongly in six different directions.**

| Day | Minutes survival | Logged min | Flags cleared | Outbound artifacts | Verdict |
|---|---|---|---|---|---|
| 2026-09-22 | 68.8% | 165 | 0 of 8 | — | high survival, lowest output |
| 2026-09-23 | 30.4% | 105 | **2 of 8**, both top-ranked | 2 emails | better than 9/22 |
| 2026-09-24 | 16.7% | 15 | 2 of 16, one red | 2 emails + 5 Slack + 1 Doc | worst survival, strong output |
| 2026-09-25 | 26.7% | 60 | **3 of 12** | 1 email + 1 Slack DM | mid on both |
| 2026-09-28 | 58.3% | 210 | 2 of 14 | 1 email, 330 min on one client thread | high survival, thin output |
| 2026-09-29 | **71.4%** *(frozen)* | 225 | **3 of 18** + 4 clocks reset | 6 emails + 1 Slack | best day on BOTH axes at once |
| 2026-09-30 | 27.3% | 360 | 3 of 22, at 1, 3 and 4 bd | 4 emails + 3 Slack | low survival, highest output |
| **2026-10-01** | **20.0%** | **375** (150 self-scheduled) | **3 of 24** | **2 emails + 0 Slack** | ⚠️ **lowest survival AND lowest outbound — the first day low on both** |

⚠️ **10/1 is the case that stops survival being read as laziness and stops output being read as a substitute.** 375 exclusive minutes sat on the board with **zero overlap**, but only **150** of them were self-scheduled work: the rest were 135 minutes of meetings and 90 of anchors. A day can be full, contiguous, and still move almost nothing.

**Survival and output are uncorrelated, not anti-correlated** (n=8). Neither predicts the other; both must be reported, always alongside **logged minutes**, **flags cleared** and **artifacts**.

⚠️ **And neither predicts the deadline.** On 9/30 both 9/30-dated red items took zero minutes and expired. **On 10/1 the payroll deadline passed unapproved and the consequence compounded — one pushed-back run became three, all check dates moved to Oct 8** — while the two emails that did get sent both answered items that had arrived that same morning. **A good day, a busy day, and a day that clears its deadlines are three different things, and only the flag list tracks the third.**

## 1. What each number actually means

| Tag | Assumed planning minutes | Measured median | n | Drift |
|---|---|---|---|---|
| `1` | 30 | — | 0 | — |
| `2` | 90 | — | 0 | — |
| `3` | 165 | — | 0 | — |
| `4` | not schedulable | n/a | n/a | decompose marker, not a size |

Tags are readable only through Asana, unavailable on all **eighteen** runs to date. **Nothing in §1 can move until the connector is authorised.**

**Adjacent measurement that does not need tags** (n=7): **externally-organised meetings run 111.1% of their booked minutes** — 311 of 280. Individual observations range **37.5% to 152%**. 10/1's `Align on Gen 2 pricing and packaging` was booked 60 and ran **90 (150%)**, extended by the organiser at 10:26:54, four minutes before its new end. At n=7 a counterparty's booking is an estimate with a wide **two-sided** error. **Plan no cascade around an assumed overrun — and note that the overrun ate the start of the block that followed it.**

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

**⚠️ EXCLUDE CONTAINERS FROM THE DENOMINATOR** (2026-09-23(C)). `(AI/Team Mgmt & Admin Tasks)` and bare `[hold]`/`[HOLD]` are **allocations of unassigned time, not plans** — Michael's `[MC]` note of 2026-09-02: *"the 'hold' for each day, which I'll replace with task-blocks generally the evening before."* Score a container on what replaced it. **A DECLINED block is not occupied time either** and is excluded from both numerator and denominator; report the face overlap it would have contributed (10/1: 60 minutes).

| Day | Planned blocks | Survived | Planned min | Logged min | **Survival (minutes)** |
|---|---|---|---|---|---|
| 2026-09-22 | 4 (snapshot-restricted) | 3 | 240 | 165 | **68.8%** |
| 2026-09-23 | 6 | 1 | 345 | 105 | **30.4%** |
| 2026-09-24 | 2 (snapshot-restricted) | 1 | 90 | 15 | **16.7%** |
| 2026-09-25 | 4 | 2 | 225 | 60 | **26.7%** |
| 2026-09-28 | 5 | 3 | 360 | 210 | **58.3%** |
| 2026-09-29 | 6 | 3 + 1 partial | 315 | 225 | **71.4%** — **FROZEN**, see instrument error 5 |
| 2026-09-30 | 4 | 0 + 1 partial | 165 | 45 | **27.3%** |
| **2026-10-01** | **5** | **2** | **300** | **60** | **20.0%** — lowest full-snapshot day |
| **Pooled** | **36** | **16** | **2040** | **885** | **43.4%** |

**43.4% is the working figure, and it has now moved 46.2 → 42.2 → 38.3 → 43.4 → 49.5 → 47.4 → 43.4 across seven revisions — in both directions four times.** Band **16.7–71.4%**. **The honest statement is "roughly half, banded 17–71%." Do not hard-code 43 any more than 38 or 70.**

⚠️ **Part of the non-convergence was self-inflicted and is now fixed.** Until 2026-09-30 a prior day could be re-scored every time Michael re-timed it, so the denominator's history was mutable. Instrument error 5 now freezes each day at the run that measured it.

⚠️ **One block of the 36 is unclassified by `verb_class`** (a pre-existing gap carried since 9/23, not introduced by a later run). Recorded rather than silently reconciled.

### ⚠️ Bimodality — weakened on 9/30, REINFORCED on 10/1

**Rule as it stands:** a block runs whole or vanishes whole **unless it is decomposed**; 9/30 added one straight 25% haircut (`Scanner | Deal-Tracking`, 60 planned, 45 run, same event id, no split) that the evidence could not separate from an in-arrears decomposition.

**10/1 produced no intermediate outcome at all**: two blocks ran at exactly 30 of 30, three logged exactly zero. **Twenty-four blocks over five days, two intermediate outcomes, one of them ambiguous.**

**Size at nominal, expect run-or-vanish.** The prediction target remains **which** blocks vanish, not by how much each shrinks. ⚠️ **And 10/1 sharpens "which": the two that ran were the two SHORTEST on the board (30 min each), and both ran SHIFTED EARLIER. The three that rolled were the three longest (60, 60, 120).** One day is not a rule — **the falsification test is whether the shortest blocks keep surviving at a rate the longest do not.**

### ⚠️ The title axis is CONTAMINATED — titles now move in every observed direction

| Title type (scored at the morning snapshot) | Day-rates |
|---|---|
| Names a deliverable | 167%, 30%, 100%, 100%, 118%, 66.7%, 42.9%, **33.3%** |
| Generic / topic only | 50%, 80%, 0%, 15.4%, 0%, 75.0%, 0%, **0%** |

Four rename directions are now on record and the axis has a bin for none of them:

- **generic → named, seven minutes AFTER running** (2026-09-29(B)) — retrospective description
- **generic → named, WHILE BEING ROLLED** (2026-09-30(F)) — prospective specification
- **named → named refinement** (2026-09-30(F))
- ⚠️ **named → GENERIC, on a block that RAN** (2026-10-01) — `Scanner | Brex gift-card updates` became `Scanner | Accounting Admin`

**MANDATORY: score a block's title AS IT STOOD IN THE MORNING SNAPSHOT.** The axis stays **CONTAMINATED**, scheduler rule 3 stays **SUSPENDED**, and **the axis cannot be re-derived from historical EOD boards at all.**

⚠️ **A single judgement call on one title can invert a day's reading.** On 10/1, classing `Mixmax | Audit Open Items` as generic gives named 33.3% / generic 0%; classing it as named gives named 20.0% and no generic observation. **Record the alternative reading whenever n is small enough for one title to decide the direction.**

### `verb_class`

| `verb_class` | Blocks | Planned min | Logged min | **Rate** | Replicates? |
|---|---|---|---|---|---|
| **coordination** | 24 | 1440 | 660 | **45.8%** | n=8 days — 50%, 30%, 44%, 27%, 58%, 89%, 0%, **20.0%** |
| **production** | 11 | 660 | 360 | **54.5%** | n=5 days — was 79.2%, then 64.7%, now **54.5%** |

⚠️ **On 2026-10-01 the two classes returned IDENTICAL rates for the first time — 20.0% against 20.0%, on exactly equal planned minutes.** Production has fallen on three consecutive revisions and the gap between the classes has closed from 30 points to **9**. **The split may be descriptive only.**

**Scheduler rules from this section:**
1. Size a block at **nominal**, and expect it to run or vanish — not to shrink.
2. **Anchor it to the venue that forces it.** ✅ Supported at n=1 (2026-09-29(D)). **Corollary:** when a counterparty moves a meeting, look for a prep block anchored to it before treating the freed window as capacity — and when the venue *runs*, expect the prep block to be **deleted rather than rolled** (`Paulex | NIH Grant Research`, 9/30).
3. ~~Prefer a title that names its artifact.~~ **SUSPENDED** — see the contamination warning above.
4. **Do not encode `verb_class` as a scheduler rule.** ✅ **Strengthened at n=8** by the zero-separation day. Propose the window and name the artifact; leave the verb to Michael.

## 4. Switching cost

| Contexts in day | Days | Completion (minutes basis) |
|---|---|---|
| **5** | 1 | **71.4%** |
| 4 (+1 internal) | 3 | 79%, 27.3%, **20.0%** |
| 3 (+1 internal) | 1 | 27% |
| 2 (+1 internal) | 3 | 30%, 17%, 58.3% |

⚠️ **The seed cap of five is REFUTED, not merely un-approached** — it was reached on the highest-survival day. **Eight days, no relationship in either direction.** Keep G5 as a reporting line, not as a constraint on the scheduler. ⚠️ **Contiguity is also routinely violated without consequence**: 10/1 ran Scanner at 11:45 and again at 14:15, and DeepScribe at 11:15 and again at 17:30.

## 5. Roll history

A task at three rolls stops being silently re-planned (engine rule 9). **Disposal set: cut the scope · hand it off · accept the slip · ~~REPURPOSE the hour~~.**

⚠️ `rolls:` has never been readable or writable. **0 increments across eighteen runs, against 16 directly observed rolls.**

| Block / workstream | Observed rolls | Status |
|---|---|---|
| **`Asana-Agent \| Add'l Setup, Tagging & Task Review`** (`07b3d937if5c2v2dljba475qvf`) | ⚠️ **4 — PAST THRESHOLD** | **The repurposing did NOT hold.** Carried 3 rolls as `Monthly Close Prep`, was renamed and re-placed 10/1 16:00–17:00 on 9/30, **and rolled again to 10/2 09:00–10:00 at 17:12:22 on 10/1 — uncontested, nothing scheduled over it.** See the demotion below |
| `Mixmax \| Audit Open Items` (`2qqif5bppkik8mmf1j44993u1q`) | **1** | → 10/2 13:15–15:30, **grown 120 → 135**. Its 10/1 start was eaten by an external meeting's 30-minute overrun |
| `Scanner \| Contract > Revenue Process Documentation` (`4uo929rb9dtpevaqtvrusj6qpl`) | **1** | → 10/2 15:30–16:30. ⚠️ **45 minutes of the same contract→revenue work was logged on 10/1 under a different event id** — the plan rolled, part of the work did not |
| `DeepScribe \| New Update/Agenda Doc` (`2actpm6je9f415eegpm6f5tt1d_…`) | 1, frozen | ✅ **Ran 10/1**, shifted 10:00 → 11:15, 30 of 30 |
| `Client/Double Review (...)` (`7u71d6h0k1grovgju1jgeao76c`) | 3, final | **DELETED 2026-09-25** at its fourth placement — rule 9's "cut it", reached independently |
| `Scanner \| Close: Aug Revenue` | 5 (as of 2026-09-15) | past threshold; unverifiable until the connector returns |
| Mixmax audit backup `C-20260917-05` · DeepScribe/Tabs `C-20260910-05` | **n/a — never placed** | **Worse than rolled.** Both dates passed; the Tabs go-live date passed 10/1 with the cleanup at zero for a twelfth day |

⚠️ **REPURPOSED IS DEMOTED FROM A DISPOSAL TO AN ATTEMPT.** Lesson 2026-09-30(G) read the repurposing as proof that *"an hour that has survived three rolls is an hour Michael intends to keep."* **That claim was fitted at n=1 and failed its first out-of-sample test the next day.** Only two disposals have actually held in the corpus: **deleted outright** (`Client/Double Review`) and **discharged by a counterparty's meeting**. **Repurposing an hour does not make it survive — and the work put into it on 9/30 was the single highest-value unblocking task in the system, which did not help either.**

**Rolls are written when the displacing work takes the window** — ⚠️ **except when nothing displaces it.** The Asana hour was not evacuated; it was abandoned, with an empty board behind it. **Some rolls are already visible at 4:15 PM on most days** — read the calendar; do not assume they cannot be there.

## 6. Tag-prediction accuracy

| | Proposed | Unchanged by MC | Corrected | Accuracy |
|---|---|---|---|---|
| Number | 9 | 0 | 0 | **unmeasurable** |
| Letter | 9 | 0 | 0 | **unmeasurable** |

⚠️ This stream cannot open until the EOD Planner runs once and Michael sets a real tag against an agent proposal. **The EOD Planner has still never fired.**

**Target selection — one content hit in eleven proposals:**

| Day | Proposed | Result |
|---|---|---|
| 9/23–9/28 | four proposals | window and/or verb class wrong every time |
| 9/29 | reply to Jennifer on the $14.8–15.0k range | client HIT, counterparty HIT, **thread MISS** |
| 9/30 | confirm the sales-assist attribution treatment to Jason Tatum and Viola Melis in `#attivo-mixmax` | ✅ **client, counterparty, thread and CONTENT all HIT. Window MISS** |
| **10/1** | **three proposals: bank statements to Aashir Ali; approve the payroll; pull the Moss Adams items** | 🔴 **all three missed — and none on content selection.** See the rule below |

**At n=11 the agent can name WHAT Michael will do and cannot name WHEN.** **Stop scoring window placement as part of proposal accuracy.**

### ⚠️ A PROPOSAL INHERITS THE MOBILITY OF ANY CONTAINER IT NAMES

**10/1's three proposals each failed differently, and none failed on choosing the wrong work:**

1. *"Send Aashir the statements **inside the existing 10:30–12:30 audit block**"* — **the block rolled.** The within-block mechanism is **UNTESTED, not refuted** (2026-09-07(B)); what failed is the narrower claim that he would do it that day.
2. *"Approve the payroll, **riding the 08:30 `INBOX Check-in` anchor**"* — **the anchor moved to 10:30.**
3. *"Pull the Moss Adams items **into Friday 09:00–11:00, the generic hold**"* — **that window filled by 17:12.**

**THE OPERATIONAL FORM: name the artifact and the counterparty who must RECEIVE it, and name NO container — not a block, not an anchor, not an empty window.** A proposal that cannot be stated without saying where it goes is a scheduling claim wearing a content claim's clothes, and it will be scored as a content miss when the container moves. **This is what "name WHAT, not WHEN" actually requires; stating the rule does not execute it.**

### ANSWERABILITY SELECTS THE THREAD — and price is a LATENCY, not a refusal

**He answers what he can answer from knowledge in one or two lines, roughly in arrival order.** A **price commitment is slept on, not refused** — roughly two days where a knowledge answer takes hours — and it is answered **first thing in the morning**. ⚠️ **10/1 replicates the arrival-order half cleanly**: both emails sent that day answered same-morning arrivals, at 1 h 42 m and 2 h 10 m.

⚠️ **CHANNEL SILENCE IS A MEDIUM PREFERENCE, NOT UNRESPONSIVENESS.** Flag the *ask*, not the channel. Medium preference is not stable per counterparty; do not infer the medium of the answer from the medium of the ask. ⚠️ **But an UNREAD email is different from an unanswered one** — it is positive evidence the thread was never engaged, and it is observable where Suralink, Rippling, Ramp and the portals are not.

**A displacement proposal is stale if a counterparty posted after it was written.**

**Name the counterparty who must *receive* the artifact, not the one who produced it.**

⚠️ **A parameter written here but not read into the proposal is not part of the engine** (2026-09-24(K)). **Every displacement proposal must name which rule of this note it applied.**

⚠️ **Do not withhold the highest-value item from the proposal because the model predicts deferral.** Optimising a proposal for predicted uptake rather than for value is how the loop learns to be agreeable instead of useful.

## 7. Counterparty volatility and refill

| Disposal mode | 9/22 | 9/23 | 9/24 | 9/25 | 9/28 | 9/29 | 9/30 | **10/1** | Note |
|---|---|---|---|---|---|---|---|---|---|
| Cancelled by counterparty | 1 | 1 | 1 | 0 | 0 | 0 | 0 | 0 | |
| Moved by counterparty | 1 | 0 | 0 | 0 | 0 | 1 | 1 | 0 | |
| **Extended by counterparty mid-meeting** | — | — | — | — | — | — | — | **1** | ⚠️ **new** — Gen 2 call 60 → 90, and the overrun ate the next block's start |
| Deleted by Michael (containers) | 2 | 2 | 3 | 1 | 0 | 0 | 2 | 0 | |
| Declined by Michael | — | — | — | — | — | — | — | **1** | not occupied time (§3) |
| Moved within the day by Michael | — | — | 3 | 4 | 6 | 8 | **11** | 4 | |
| Evacuated by a competing client | 1 | 1 | 0 | 1 | 0 | 0 | 0 | 0 | |
| Rolled forward by Michael | 0 | 2 | 1 | 1 | 2 | 2 | 2 | **3** | |
| **Rolled AS A SET onto the same next day** | — | — | — | — | — | — | — | **3** | ⚠️ **new — the WHOLE-DAY ROLL**, 14 seconds, see below |
| **Abandoned — rolled with nothing taking the window** | — | — | — | — | — | — | — | **1** | ⚠️ **new** — the Asana hour |
| Deleted once its venue RAN | — | — | — | — | — | — | 1 | 0 | |
| **Cancelled by Michael <30 min before start, re-booked next day** | — | — | — | — | — | — | — | **1** | ⚠️ **new** — and **both counterparties then declined the replacement** |
| Retro-filed onto a LATER day | — | — | — | 1 | 0 | 0 | 1 | 0 | |
| Repurposed at the roll threshold | — | — | — | — | — | — | 1 | ⚠️ **failed** | §5 |
| Deferred past 17:00 within the day | — | — | — | — | 2 | 2 | 1 | 0 | |

⚠️ **Block disposal is not primarily counterparty-driven.** Pooled: **8 of 73.** **It is overwhelmingly Michael re-planning his own day intraday.**

⚠️ **THE WHOLE-DAY ROLL is a distinct shape from wholesale re-planning.** On 9/30 the morning board was *deleted* between 10:54 and 13:27 and replaced with work that was then done completely. On 10/1 three blocks were *deferred intact* onto 10/2 in fourteen seconds (17:12:22 / 17:12:32 / 17:12:36), two keeping their exact durations. **9/30 replaced the plan; 10/1 postponed it.** Survival measures the second honestly and the first not at all.

**Discharge-by-meeting** (2026-09-24(F), narrowed 2026-09-25(L)): when a flagged item acquires a dated venue **with the counterparty in it**, it stops being overdue. **A solo prep block does not discharge anything.**

⚠️ **ARRIVAL RECENCY BEATS DEADLINE PROXIMITY EVEN WHEN THE ARRIVING ITEM HAS NO DATE AND NO OWNER** — **n=5** (2026-09-25, 09-28(J), 09-29, 09-30, **10-01**). ⚠️ **10/1 shows it is a SELECTION effect, not a capacity effect**: 9/30 could be explained by recent arrivals consuming 360 minutes, but 10/1 had only 150 minutes of self-scheduled work in total and the dated items *still* lost. **This is the model's most reliable predictor of where a day's minutes go, and the scheduler cannot fix it.**

⚠️ **A dated venue with a counterparty in it is the only reliable forcing function, and FOUR CONSECUTIVE DAYS the counterparty created it, not this system.** On 10/1 Viola booked `Align on Sales attribution` for 10/2 **two minutes after the Gen 2 call ended**, discharging a 9-business-day flag that eighteen run documents had not moved. **A flag's realistic job is not to produce a block — it is to be correct and available at the moment a counterparty creates the forcing function.**

**Refill: freed time is filled by re-pointing a block that already exists somewhere on the same day.** Latency 52–59 min at n=3, not re-measured since 9/24.

⚠️ **Size a capture block to the vacancy plus the soft time abutting it.** Declined, tentative and externally-organised blocks are not occupied time.

⚠️ **Focus blocks move in both directions and in three senses** — to another date, later past 5:00 PM, and earlier within the day. ⚠️ **10/1's two survivors both moved EARLIER**, by 75 and 135 minutes.

---

## Known instrument errors

Seven measurement hazards that would otherwise corrupt this model silently.

1. **Retroactive blocks are work logs, not plans — the test is `updated` vs `end`, NOT `created` vs `start`.** **An event whose last `updated` stamp post-dates its own `end` is retroactively placed and cannot be scored for plan adherence, however old its `created`.** Counts: 9/23 five of eleven, 9/24 four of seven, 9/25 four of ten, 9/28 one of seven, 9/29 three pure logs plus one in-flight, 9/30 two pure logs plus three in-flight, **10/1 one pure log and no in-flight**.
   - **A block created *during* its own window is in-flight — treat it as a log, and say so.**
   - ⚠️ **Apply the test to the block's position AT THE MOMENT IT IS SCORED.** **Anchor to the 07:30 snapshot: a block present there with `created` before its start is a plan, whatever happens to its stamps afterwards.**
   - ⚠️ **A block created before its start but AFTER the 07:30 snapshot is an intraday plan, not a log.** 10/1 gives two (`Attivo | Review/Approve Timesheets` created 11:23:31 for 14:00; `Benchmarking | Revenue/Expense Data Spot-checks` created 11:43:45 for 12:15). They are **not scoreable against the morning board** and must not be dropped.
   - ⚠️ **ANCHORS MOVE TOO, AND A PROPOSAL THAT RIDES ONE INHERITS THAT.** On 10/1 `INBOX Check-in` moved 08:30 → 10:30 and grew 30 → 45. §6's container rule is the operational consequence.

2. **A retro block dates the work, not the output.** The correspondence lands *later* than the block's own window — **n=6, range 8 min to 3 h 45 m**. The send **always follows** the block, never precedes it. **Search forward from the block's end to the end of the next admin anchor; a same-window search returns a false negative.** ⚠️ **A forward search that finds nothing is a real negative and worth recording** — 10/1's 45-minute Scanner log produced no outbound, which is exactly flag F4.

3. **Classify a burst by the dates it writes — per block, because a burst can be MIXED.** A **log-burst** re-times *today* or a prior day; a **plan-burst** writes *future* dates. ⚠️ **The plan-burst's location is UNCONSTRAINED — search the whole day INCLUDING the anchors.** 10/1 replicates 9/30: the roll-burst ran 17:12:22–17:12:36, inside the 17:00–17:30 `INBOX Review`. **A rule falsified as "always" must not be carried forward as "never."** Also: **sort by start and subtract pairwise overlap before summing logged minutes, and report the overlap.**

4. **A block missing from today may have migrated in EITHER direction — match on event id, never on title or absence.** ⚠️ **Use the FULL event id**: a truncated id returns *"could not be found or has been deleted"* — indistinguishable from a real deletion. ⚠️ **And confirm a deletion with a title search as well as an id lookup.** ⚠️ **When a prior run did not record a block's id, identity after a rename cannot be confirmed at all** — 10/1's `Scanner | Brex gift-card updates` → `Scanner | Accounting Admin` is an inference from duration, client and creation time, and the day's survival is 20.0% if it holds and 10.0% if it does not. **Record the event id of every block the day's board carries, so tomorrow's run can match it.**

5. **A scored block's calendar position is mutable after the run that scored it — SO FREEZE THE DAY.** **RULING (2026-09-30): the measurement of record for a day is the one taken by that day's own evening run, against the stamps closest to the events.** A later re-time is recorded as **calendar churn** against that day, not as a new measurement. A day is re-scored **at most once**, and only to correct a *named* instrument error. **9/29 is frozen at 225/315 = 71.4%.**

6. **Client work product is structurally invisible, so a production block's output can never be observed.** The Google Drive connector authenticates as `michael.p.christopher@gmail.com`, **not** the Attivo Workspace. **Record production output as unobservable, exactly as Suralink, Rippling, Ramp, Anrok and the portal layer are. Never score a production block as having produced nothing.** ⚠️ **The exception that proves it useful: Rippling's PAST-TENSE notices are direct evidence, and on 10/1 one reported a negative** — three payroll runs not approved. **An unobservable surface can still speak when it reports a consequence that already happened.**

7. **The umbrella block: a late-day extension can swallow other blocks, and its face duration double-counts them.** **When an extended block contains other named blocks, its EXCLUSIVE minutes are the honest figure.** ⚠️ 9/30 and 10/1 both had **zero** overlap across their logged blocks, so the hazard is intermittent, not structural, and the overlap figure must be reported either way.

---

*Lineage: seeded 2026-09-21 from the ACA v4 specification §6 and §8, cross-checked against the `[ACA]` corpus in [[Open Brain]]. Measurements 2026-09-22 to 2026-10-01 from calendar `created`/`updated` stamps diffed against each day's 7:30 AM snapshot and reconciled against Gmail sent, Slack read by channel id, and Drive. Asana has been unavailable on all eighteen runs, so §1, §2, §5 and §6 remain unmeasured; the EOD Planner has never run, so no agent-authored agenda has ever been scored.*

**Revisions** (last ten)

- 2026-09-22 — first measured values. §3 populated (n=1) and minutes-weighted columns added. §4 first row. New §7. Third instrument error added.
- 2026-09-23 — second measured day. `verb_class` replaces named/generic as §3's headline split. New §0. Containers excluded from the denominator. 70% cap superseded. §7 narrowed; fourth instrument error added.
- 2026-09-24 — third measured day. Coordination replicates. Pooled 46.2% → 42.2%. §7 gains discharge-by-meeting and the soft-time-overflow rule. Instrument error 3 split into log- and plan-bursts; error 4 widened.
- 2026-09-25 — fourth measured day, first withdrawal of a prior measurement. Pooled 42.2% → 38.3%. §3 gains the bimodal-survival warning. Instrument error 1 rewritten around `updated` vs `end`; new error 5.
- 2026-09-28 — fifth measured day, first falsification of the model's strongest claim. Pooled 38.3% → 43.4%. *Never propose production* **deleted**. Title axis promoted. New error 6.
- 2026-09-29 — sixth measured day; best on both axes (71.4%). Pooled 43.4% → 49.5%. **Title axis DEMOTED to CONTAMINATED**; scheduler rule 3 SUSPENDED. Scheduler rule 2 promoted at n=1. §6's *newest live thread* replaced by answerability. New error 7, the umbrella block.
- 2026-09-30 — seventh measured day; lowest survival (27.3%) on the highest-output day. Pooled 49.5% → 47.4%; production 79.2% → 64.7%. §0 gains a fifth wrong ranking. **Instrument error 5 gains the FREEZE RULE** and 9/29 is frozen at 71.4%. Plan-burst location declared unconstrained. §6's commitment-deferral rule DELETED and restated as a latency prior. §3 bimodality WEAKENED. §5 and §7 gain REPURPOSED and DELETED-ONCE-ITS-VENUE-RAN.
- **2026-10-01 — eighth measured day; lowest survival (20.0%) AND lowest outbound (2 emails, 0 Slack) — the first day low on both.** Pooled **47.4% → 43.4%**; coordination 48.8% → **45.8%**; production 64.7% → **54.5%**, with the **first day of zero separation between the classes**. **§5's REPURPOSED DEMOTED from a disposal to a failed attempt** — the repurposed Asana hour rolled at #4, uncontested, one day after the rule was written; **the n≤5 falsification sequence reaches n=5**. §7 gains the **WHOLE-DAY ROLL**, **abandoned-with-nothing-taking-the-window**, **cancelled-<30-min-before-start-and-re-booked**, and **extended-by-counterparty-mid-meeting**; arrival-recency goes **n=4 → n=5** and is re-characterised as a **selection** effect. §6 gains **a proposal inherits the mobility of any container it names** after all three of 10/1's proposals died that way. §3 bimodality **reinforced**; title axis gains the **named → generic** direction. §1's external-meeting figure 100.5% (n=6) → **111.1% (n=7)**. Instrument error 4 gains **record every block's event id**; error 6 gains the past-tense exception.
