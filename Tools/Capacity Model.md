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

> ⚠️ **PARTLY MEASURED.** Seeded 2026-09-21 from the priors in the v4 spec §6. **Measurements from nine days — 2026-09-22 to 09-25, 09-28, 09-29, 09-30, 10-01 and 10-02, 39 scoreable blocks** — are marked below; everything unmarked is still a guess recorded so it can be falsified.
>
> ⚠️ **THE n≤5 FALSIFICATION STREAK BROKE AT 5.** Five consecutive days falsified a claim fitted at n≤5 on its first out-of-sample test — 9/28 the production rule, 9/29 the narrowed production form and the title axis, 9/30 the commitment-deferral rule, 10/1 the repurposed-hour rule. **On 10/2 one survived**: 10/1's observation that the shortest blocks survive and the longest roll held exactly, on a 60/60/135 board. **The discipline does not relax.** A claim fitted at n≤5 is still written **with its own falsification test attached** and is still not read into a scheduler rule or a displacement proposal before that test has run — what 10/2 shows is that the test is worth attaching, because it can come back positive.
>
> ⚠️ **AND THE COROLLARY FROM 10/2:** when a day carries **three or fewer scoreable blocks**, no categorical split computed from it goes into a pooled rate without the alternative reading stored beside it. `verb_class` swung from 0 to 100 points of separation in one day on three blocks.

**What this note is.** Only the congealed structure — current parameter values and the rules they imply. It is integrated, maintained and small. It is **not a log**: nightly observations are atomic and stay in [[Open Brain]] as `[ACA-PLAN]` thoughts.

**Update protocol.** `upsert_note` overwrites in full, so the evening run must `read_note` first, merge, and write back. Test **S8** asserts the read preceded the write. Revision line at the foot, capped at the last ten entries. **As a measured value replaces a prior, delete the prior** — this note should shrink as it learns.

---

## 0. The two axes — read them together or not at all

**Minutes-survival alone has now ranked the measured days wrongly in seven different directions.**

| Day | Minutes survival | Logged min (all board, exclusive) | Flags cleared | Outbound artifacts | Verdict |
|---|---|---|---|---|---|
| 2026-09-22 | 68.8% | 165 | 0 of 8 | — | high survival, lowest output |
| 2026-09-23 | 30.4% | 105 | **2 of 8**, both top-ranked | 2 emails | better than 9/22 |
| 2026-09-24 | 16.7% | 15 | 2 of 16, one red | 2 emails + 5 Slack + 1 Doc | worst survival, strong output |
| 2026-09-25 | 26.7% | 60 | **3 of 12** | 1 email + 1 Slack DM | mid on both |
| 2026-09-28 | 58.3% | 210 | 2 of 14 | 1 email, 330 min on one client thread | high survival, thin output |
| 2026-09-29 | **71.4%** *(frozen)* | 225 | **3 of 18** + 4 clocks reset | 6 emails + 1 Slack | best day on BOTH axes at once |
| 2026-09-30 | 27.3% | 360 | 3 of 22, at 1, 3 and 4 bd | 4 emails + 3 Slack | low survival, highest output |
| 2026-10-01 | 20.0% | 375 (150 self-scheduled) | 3 of 24 | 2 emails + 0 Slack | lowest survival AND lowest outbound |
| **2026-10-02** | **47.1%** | **480** (300 self-scheduled) | **3 of 24** | **3 emails + 0 Slack** | ⚠️ **mid survival, highest logged minutes in the corpus — and two of the three flags were cleared by somebody else** |

⚠️ **10/2 adds a seventh wrong ranking, and it is the sharpest.** 480 exclusive minutes, zero overlap, 300 of them self-scheduled work — the most this corpus has recorded — on a day whose survival is only mid-band, because **most of the minutes went to work that did not exist at 07:30.** Two pure logs, one in-flight log and two intraday plans account for 180 of the 300.

⚠️ **AND "FLAGS CLEARED" NEEDS A SECOND COLUMN: WHO CLEARED IT.** On 10/2 three flags moved. The DeepScribe `attivo@deepscribe.tech` lockout was cleared by **Jonathian Quizon escalating and Pavan Manoj answering in 5 min 12 s**; the Frank Rimerman audit acquired a venue and a standing series because **Aashir Ali booked them**; only the Asana hour moved because Michael moved it. **A flag count that does not say who moved it overstates what the system and its owner did.**

**Survival and output are uncorrelated, not anti-correlated** (n=9). Neither predicts the other; both must be reported, always alongside **logged minutes**, **flags cleared**, **who cleared them** and **artifacts**.

⚠️ **And neither predicts the deadline.** 9/30: both 9/30-dated red items took zero minutes and expired. 10/1: the payroll deadline passed unapproved and one pushed-back run became three. **10/2: the payroll deadline passed again with no block, and this time the outcome is UNOBSERVABLE — no post-deadline Rippling notice had arrived by 17:38 CT, and per instrument error 6 that is recorded as unobservable, never inferred in either direction.** **A good day, a busy day, and a day that clears its deadlines are three different things, and only the flag list tracks the third.**

## 1. What each number actually means

| Tag | Assumed planning minutes | Measured median | n | Drift |
|---|---|---|---|---|
| `1` | 30 | — | 0 | — |
| `2` | 90 | — | 0 | — |
| `3` | 165 | — | 0 | — |
| `4` | not schedulable | n/a | n/a | decompose marker, not a size |

Tags are readable only through Asana, unavailable on all **twenty** runs to date. **Nothing in §1 can move until the connector is authorised.**

**Adjacent measurement that does not need tags** (n=8): **externally-organised meetings run 110.0% of their booked minutes** — 341 of 310. Individual observations range **37.5% to 152%**. 10/2's `DeepScribe <> Attivo Check-in` ran 30 of 30 (Fireflies notetaker joined 11:56:06, recap issued 12:26:19 — 30 min 13 s of presence). At n=8 a counterparty's booking is an estimate with a wide **two-sided** error. **Plan no cascade around an assumed overrun.**

⚠️ **Not every external meeting yields a duration.** 10/2's `FR+Co/Mixmax, Inc. Check in` ran with no Fireflies recap and is excluded rather than assumed at face value.

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

**⚠️ EXCLUDE CONTAINERS FROM THE DENOMINATOR** (2026-09-23(C)). `(AI/Team Mgmt & Admin Tasks)` and bare `[hold]`/`[HOLD]` are **allocations of unassigned time, not plans** — Michael's `[MC]` note of 2026-09-02: *"the 'hold' for each day, which I'll replace with task-blocks generally the evening before."* Score a container on what replaced it. **A DECLINED block is not occupied time either** and is excluded from both numerator and denominator.

| Day | Planned blocks | Survived | Planned min | Logged min | **Survival (minutes)** |
|---|---|---|---|---|---|
| 2026-09-22 | 4 (snapshot-restricted) | 3 | 240 | 165 | **68.8%** |
| 2026-09-23 | 6 | 1 | 345 | 105 | **30.4%** |
| 2026-09-24 | 2 (snapshot-restricted) | 1 | 90 | 15 | **16.7%** |
| 2026-09-25 | 4 | 2 | 225 | 60 | **26.7%** |
| 2026-09-28 | 5 | 3 | 360 | 210 | **58.3%** |
| 2026-09-29 | 6 | 3 + 1 partial | 315 | 225 | **71.4%** — **FROZEN**, instrument error 5 |
| 2026-09-30 | 4 | 0 + 1 partial | 165 | 45 | **27.3%** |
| 2026-10-01 | 5 | 2 | 300 | 60 | **20.0%** |
| **2026-10-02** | **3** | **2** | **255** | **120** | **47.1%** — alternative reading 30.8%, below |
| **Pooled** | **39** | **18** | **2295** | **1005** | **43.8%** |

**43.8% is the working figure, and it has moved 46.2 → 42.2 → 38.3 → 43.4 → 49.5 → 47.4 → 43.4 → 43.8 across eight revisions — in both directions four times.** Band **16.7–71.4%**. **The honest statement is "roughly half, banded 17–71%." Do not hard-code 44 any more than 38 or 70.**

⚠️ **10/2's alternative reading, recorded not buried.** `Asana-Agent | Add'l Setup, Tagging & Task Review` is scored as **ran shifted** because it sits on the EOD board at 16:00–17:00, 60 of 60, on the same day it was planned. Its final `updated` stamp (17:33:23 CT) post-dates its 17:00 end and sits inside a five-event log-burst, so "it ran" is inferred from a retroactive re-time. **If it is read as a pure log instead, the day is 60 of 195 = 30.8% and the pooled figure is 38 blocks, 2235 planned, 945 logged = 42.3%.**

⚠️ **Part of the non-convergence was self-inflicted and is now fixed.** Until 2026-09-30 a prior day could be re-scored every time Michael re-timed it. Instrument error 5 now freezes each day at the run that measured it.

⚠️ **One block of the 39 is unclassified by `verb_class`** (a pre-existing gap carried since 9/23).

### ⚠️ Bimodality — REINFORCED again on 10/2

**Rule as it stands:** a block runs whole or vanishes whole **unless it is decomposed**. **10/2 produced no intermediate outcome**: two blocks ran at exactly 60 of 60, one logged exactly zero, and the two intraday plans ran at exactly 30 of 30 and 15 of 15. **Twenty-seven blocks over six days, two intermediate outcomes, one of them ambiguous.**

**Size at nominal, expect run-or-vanish.** The prediction target remains **which** blocks vanish, not by how much each shrinks.

### ✅ BLOCK LENGTH — the first n≤5 claim to survive its first out-of-sample test

| Day | Board | Ran | Rolled |
|---|---|---|---|
| 2026-10-01 | 30, 30, 60, 60, 120 | the two **30s** | the **60, 60, 120** |
| 2026-10-02 | 60, 60, 135 | the two **60s** | the **135** |

**Plus 10/2's two intraday plans, 30 min and 15 min, both ran.** At n=2 days the shortest blocks on a board survive at a rate the longest do not. **This is now the most promising live hypothesis in the note. Its next falsification test is a day whose longest block is also its only one that runs.**

⚠️ **The direction-of-shift half of 10/1's claim is FALSIFIED.** 10/1's two survivors both moved *earlier*; 10/2's moved **105 minutes earlier and seven hours later** respectively. **Direction of shift carries no signal. Length may.**

### ⚠️ The title axis is CONTAMINATED — and inverts on one judgement call two days running

| Title type (scored at the morning snapshot) | Day-rates |
|---|---|
| Names a deliverable | 167%, 30%, 100%, 100%, 118%, 66.7%, 42.9%, 33.3%, **100%** |
| Generic / topic only | 50%, 80%, 0%, 15.4%, 0%, 75.0%, 0%, 0%, **30.8%** |

Four rename directions are on record and the axis has a bin for none of them: generic → named *after* running (2026-09-29(B)); generic → named *while being rolled* (2026-09-30(F)); named → named refinement (2026-09-30(F), and again 10/2 — `Scanner | Contract > Revenue Process Documentation` → `… Process + Documentation`); named → **generic** on a block that ran (2026-10-01).

**MANDATORY: score a block's title AS IT STOOD IN THE MORNING SNAPSHOT.** The axis stays **CONTAMINATED**, scheduler rule 3 stays **SUSPENDED**, and **the axis cannot be re-derived from historical EOD boards at all.**

⚠️ **A single judgement call on one title inverts a day's reading, now on two consecutive days.** On 10/2, classing `Mixmax | Audit Open Items` as generic gives named 100% / generic 30.8%; classing it as named gives named 30.8% / generic 100%. Same title, same ambiguity, same inversion as 10/1.

### `verb_class`

| `verb_class` | Blocks | Planned min | Logged min | **Rate** | Replicates? |
|---|---|---|---|---|---|
| **coordination** | 25 | 1575 | 660 | **41.9%** | n=9 days — 50%, 30%, 44%, 27%, 58%, 89%, 0%, 20.0%, **0%** |
| **production** | 13 | 780 | 480 | **61.5%** | n=6 days — 79.2% → 64.7% → 54.5% → **61.5%**, first rise in four revisions |

⚠️ **On 10/1 the two classes returned IDENTICAL rates — 20.0% against 20.0%. On 10/2 they returned 100% against 0%.** Zero separation to total separation in one day, on three blocks. **This axis is measuring sample size, not Michael.**

**Scheduler rules from this section:**
1. Size a block at **nominal**, and expect it to run or vanish — not to shrink.
2. **Anchor it to the venue that forces it.** ✅ Supported at n=1 (2026-09-29(D)). **Corollary:** when a counterparty moves a meeting, look for a prep block anchored to it before treating the freed window as capacity — and when the venue *runs*, expect the prep block to be **deleted rather than rolled** (`Paulex | NIH Grant Research`, 9/30). ⚠️ **Second corollary, 10/2: the venue itself can be withdrawn.** See §7.
3. ~~Prefer a title that names its artifact.~~ **SUSPENDED** — see the contamination warning above.
4. **Do not encode `verb_class` as a scheduler rule.** ✅ **Strengthened at n=9**, now from both directions: the axis has produced one day of zero separation and one of total separation, consecutively.
5. ⚠️ **PROVISIONAL, n=2 days — prefer the shorter block.** When the same work can be placed as one long block or two short ones, two short ones is the better bet. **Not yet a rule; it is the live hypothesis with a test attached.**

## 4. Switching cost

| Contexts in day | Days | Completion (minutes basis) |
|---|---|---|
| **5** | 1 | **71.4%** |
| 4 (+1 internal) | 4 | 79%, 27.3%, 20.0%, **47.1%** |
| 3 (+1 internal) | 1 | 27% |
| 2 (+1 internal) | 3 | 30%, 17%, 58.3% |

⚠️ **The seed cap of five is REFUTED, not merely un-approached** — it was reached on the highest-survival day. **Nine days, no relationship in either direction.** Keep G5 as a reporting line, not as a constraint on the scheduler. ⚠️ **Contiguity is routinely violated without consequence**: 10/2 ran Mixmax at 10:15, 11:00 and 15:00, and DeepScribe at 12:00 and 13:15.

⚠️ **A NEW CLIENT CONTEXT CAN APPEAR WITH NO WARNING AND TAKE THE DAY'S FIRST WORKING BLOCK.** `Kestrel | RevRec Inquiry` logged 09:45–10:15 on 10/2 against a thread that arrived 10/1 16:00 CT. **Kestrel had never appeared in this corpus.** Any capacity figure computed only over the known client list is an underestimate.

## 5. Roll history

A task at three rolls stops being silently re-planned (engine rule 9). **Disposal set: cut the scope · hand it off · accept the slip · deferred to the end of the same day · ~~REPURPOSE the hour~~.**

⚠️ `rolls:` has never been readable or writable. **0 increments across twenty runs, against 17 directly observed rolls.**

| Block / workstream | Observed rolls | Status |
|---|---|---|
| **`Asana-Agent \| Add'l Setup, Tagging & Task Review`** (`07b3d937if5c2v2dljba475qvf`) | **4 — held, did not become 5** | ✅ **DID NOT ROLL ON 10/2.** Moved 09:00 → **16:00–17:00 the same day** and ran 60 of 60; at 17:36:11 Michael created a **successor**, `INBOX  Agent Maintenance & Asana Setup` (`4r3qk50ptj54dl952rh3r6h7k2`), for 10/5 10:00–11:00 — a new event id, not a fifth re-placement |
| `Mixmax \| Audit Open Items` (`2qqif5bppkik8mmf1j44993u1q`) | ⚠️ **2** | → 10/5 13:15–**16:15**, **grown again, 135 → 180**. Rolled at **11:35:50 CT**, 1 h 40 m *before* it was due to start |
| `Scanner \| Contract > Revenue Process + Documentation` (`4uo929rb9dtpevaqtvrusj6qpl`) | **1, frozen** | ✅ **Ran 10/2**, shifted 15:30 → 13:45–14:45, 60 of 60. **No outbound followed** — see instrument error 2 |
| `DeepScribe \| New Update/Agenda Doc` (`2actpm6je9f415eegpm6f5tt1d_…`) | 1, frozen | ✅ Ran 10/1, 30 of 30 |
| `Client/Double Review (...)` (`7u71d6h0k1grovgju1jgeao76c`) | 3, final | **DELETED 2026-09-25** at its fourth placement — rule 9's "cut it", reached independently |
| `Scanner \| Close: Aug Revenue` | 5 (as of 2026-09-15) | past threshold; unverifiable until the connector returns |
| Mixmax audit backup `C-20260917-05` · DeepScribe/Tabs `C-20260910-05` | **n/a — never placed** | **Worse than rolled.** ⚠️ **Tabs leaves this row as of 10/2**: `DeepScribe \| Tabs Setup Review` (`7kjro82tch87hlc6ge74c0f9g6`) was created 11:03:57 as an intraday plan and ran 13:15–13:45 |

⚠️ **A FOURTH DISPOSAL NOW EXISTS AND IT HELD: DEFERRED TO THE END OF THE SAME DAY.** The Asana hour reached #4 and was moved to the last working slot of 10/2 rather than onto 10/3. **Three disposals have held in the corpus — deleted outright, discharged by a counterparty's meeting, and deferred to the end of the same day. REPURPOSED is still a failed attempt** (Lesson 2026-09-30(G), falsified at n=1 on 10/1).

⚠️ **A ROLLED BLOCK GROWS.** `Mixmax | Audit Open Items` has gone 120 → 135 → 180 across two rolls. **A roll is not a neutral deferral; the estimate inflates with each one**, which makes the next roll likelier. **Report growth alongside the roll count.**

**Rolls are written when the displacing work takes the window** — ⚠️ **except when nothing displaces it**, and ⚠️ **they are not an end-of-day phenomenon.** 10/2's only roll was written at **11:35 AM**. **Read the calendar at every run; do not assume a roll cannot be there yet.**

## 6. Tag-prediction accuracy

| | Proposed | Unchanged by MC | Corrected | Accuracy |
|---|---|---|---|---|
| Number | 13 | 0 | 0 | **unmeasurable** |
| Letter | 13 | 0 | 0 | **unmeasurable** |

⚠️ This stream cannot open until the EOD Planner runs once and Michael sets a real tag against an agent proposal. **The EOD Planner has still never fired.**

**Target selection — n=15 proposals, one unambiguous content hit:**

| Day | Proposed | Result |
|---|---|---|
| 9/23–9/28 | four proposals | window and/or verb class wrong every time |
| 9/29 | reply to Jennifer on the $14.8–15.0k range | client HIT, counterparty HIT, **thread MISS** |
| 9/30 | sales-assist attribution to Jason Tatum and Viola Melis in `#attivo-mixmax` | ✅ **client, counterparty, thread and CONTENT all HIT.** Window MISS |
| 10/1 | three proposals | 🔴 all three missed, each by naming a container that moved |
| **10/2** | **four, all in the operational form** | **1 counterparty hit (Aashir Ali) · 2 clean misses (Tristen Lawrence, Moss Adams) · 1 unobservable (payroll)** |

**At n=15 the agent can sometimes name WHAT Michael will do and cannot name WHEN. Window placement is not scored.**

### ⚠️ A PROPOSAL INHERITS THE MOBILITY OF ANY CONTAINER IT NAMES

**THE OPERATIONAL FORM: name the artifact and the counterparty who must RECEIVE it, and name NO container — not a block, not an anchor, not an empty window.** A proposal that cannot be stated without saying where it goes is a scheduling claim wearing a content claim's clothes, and it will be scored as a content miss when the container moves.

⚠️ **THE FORM IS STILL UNTESTED AFTER ITS FIRST APPARENT WIN.** All four of 10/2's proposals complied. The one that hit — Aashir Ali, bank statements — hit because **Aashir emailed first at 12:01:24 asking to meet**, and Michael answered an inbound. The right counterparty was named for a reason unconnected to naming it. **Per Lesson 2026-09-07(B) this is untested, not vindicated**, and crediting it is how a loop learns to take credit for a counterparty's initiative.

### ANSWERABILITY SELECTS THE THREAD — and price is a LATENCY, not a refusal

**He answers what he can answer from knowledge in one or two lines, roughly in arrival order.** A **price commitment is slept on, not refused** — roughly two days where a knowledge answer takes hours — and it is answered **first thing in the morning**. ⚠️ **10/2 replicates both halves**: Eric at Kestrel asked a rev-rec question at 16:00 on 10/1 and got a full numeric answer at **11:48:15 the next morning**; Aashir asked at 12:01:24 and got an answer at **13:47:02 (1 h 45 m)**.

⚠️ **ARRIVAL LATENCY IS NOW THE BINDING CONSTRAINT ON ANY AGENDA.** 10/2's shortest path from arrival to a calendar block was **eight minutes** — a KnowBe4 training notice at 11:47:54, a block created at 11:55:18, run at 14:45. **An agenda written at 16:15 the evening before is competing against items that do not yet exist.**

⚠️ **CHANNEL SILENCE IS A MEDIUM PREFERENCE, NOT UNRESPONSIVENESS.** Flag the *ask*, not the channel. ⚠️ **But an UNREAD email is different from an unanswered one.**

⚠️ **ESCALATION BY THE PERSON ACTUALLY BLOCKED BEATS A FLAG ON THE PERSON NOMINALLY ACCOUNTABLE** (2026-10-02(E)). The `attivo@deepscribe.tech` lockout sat 18 h with no reply; Jonathian Quizon re-posted at 11:58:14 **naming the downstream consequence** ("I need this to log in to Brex to sync the transactions in QB") and Pavan answered in **5 min 12 s**. **Separate "nobody has replied" from "nobody who can act has noticed" in the flag list — they need different flags, and only the second is Michael's.**

**A displacement proposal is stale if a counterparty posted after it was written.**

**Name the counterparty who must *receive* the artifact, not the one who produced it.**

⚠️ **A parameter written here but not read into the proposal is not part of the engine** (2026-09-24(K)). **Every displacement proposal must name which rule of this note it applied.**

⚠️ **Do not withhold the highest-value item from the proposal because the model predicts deferral.**

## 7. Counterparty volatility and refill

| Disposal mode | 9/22 | 9/23 | 9/24 | 9/25 | 9/28 | 9/29 | 9/30 | 10/1 | **10/2** | Note |
|---|---|---|---|---|---|---|---|---|---|---|
| Cancelled by counterparty | 1 | 1 | 1 | 0 | 0 | 0 | 0 | 0 | 0 | |
| **Moved by counterparty** | 1 | 0 | 0 | 0 | 0 | 1 | 1 | 0 | **1** | ⚠️ 10/2's **withdrew a discharging venue** — below |
| Extended by counterparty mid-meeting | — | — | — | — | — | — | — | 1 | 0 | |
| **Created same-day by counterparty, and RAN** | — | — | — | — | — | — | — | — | **1** | ⚠️ **new** — 72 minutes' notice |
| **Recurring series created by counterparty** | — | — | — | — | — | — | — | — | **1** | ⚠️ **new** — a standing venue, not a single one |
| Deleted by Michael (containers) | 2 | 2 | 3 | 1 | 0 | 0 | 2 | 0 | **2+** | 10/2 and 10/5 instances, plus `[hold]`/`[HOLD]` |
| Declined by Michael | — | — | — | — | — | — | — | 1 | 0 | not occupied time (§3) |
| Moved within the day by Michael | — | — | 3 | 4 | 6 | 8 | 11 | 4 | **5** | |
| Evacuated by a competing client | 1 | 1 | 0 | 1 | 0 | 0 | 0 | 0 | 0 | |
| Rolled forward by Michael | 0 | 2 | 1 | 1 | 2 | 2 | 2 | 3 | **1** | ⚠️ and it **grew** 135 → 180 |
| Rolled AS A SET onto the same next day | — | — | — | — | — | — | — | 3 | 0 | the whole-day roll |
| Abandoned — rolled with nothing taking the window | — | — | — | — | — | — | — | 1 | 0 | |
| Deleted once its venue RAN | — | — | — | — | — | — | 1 | 0 | 0 | |
| Cancelled by Michael <30 min before start, re-booked | — | — | — | — | — | — | — | 1 | 0 | |
| Retro-filed onto a LATER day | — | — | — | 1 | 0 | 0 | 1 | 0 | 0 | |
| **Deferred to the end of the same day** | — | — | — | — | — | — | — | — | **1** | ⚠️ **new, and it HELD** — §5 |
| Deferred past 17:00 within the day | — | — | — | — | 2 | 2 | 1 | 0 | 0 | |

⚠️ **Block disposal is not primarily counterparty-driven.** Pooled: **12 of 85.** **It is overwhelmingly Michael re-planning his own day intraday.**

⚠️ **A DISCHARGING VENUE CAN BE WITHDRAWN — mark discharge PENDING until the venue runs.** Viola Melis booked `Align on Sales attribution` (`7ed57tj5416idpgeujuu7s9edt`) for 10/2 10:00–10:30 on 10/1, two minutes after the prior call ended; two run documents recorded it as discharging a 10-business-day flag. **On 10/2 at 15:26:14 she moved it to 10/5 11:30.** The flag is at **10 business days and open**. **Discharge-by-meeting is real, but it is not a commitment the system can bank, and the staleness clock must keep running underneath it until the venue actually runs.**

**Discharge-by-meeting** (2026-09-24(F), narrowed 2026-09-25(L), qualified 2026-10-02(F)): when a flagged item acquires a dated venue **with the counterparty in it**, it stops being overdue **once that venue runs**. **A solo prep block does not discharge anything.**

⚠️ **ARRIVAL RECENCY BEATS DEADLINE PROXIMITY EVEN WHEN THE ARRIVING ITEM HAS NO DATE AND NO OWNER** — **n=6** (2026-09-25, 09-28(J), 09-29, 09-30, 10-01, **10-02**). **This is the model's most reliable predictor of where a day's minutes go, and the scheduler cannot fix it.**

⚠️ **A dated venue with a counterparty in it is the only reliable forcing function, and SIX CONSECUTIVE DAYS the counterparty created it, not this system.** On 10/2 it happened **twice in one afternoon**, both by the Mixmax auditor. **A flag's realistic job is not to produce a block — it is to be correct and available at the moment a counterparty creates the forcing function.**

**Refill: freed time is filled by re-pointing a block that already exists somewhere on the same day.** Latency 52–59 min at n=3. ⚠️ **10/2 adds a second refill mode: the vacated window was filled RETROACTIVELY with a log of what actually happened in it.** Viola's 10:00–10:30 left the board at 15:26:14; at 15:41:55 Michael created `Mixmax | Audit Requests` over 10:15–11:00.

⚠️ **Size a capture block to the vacancy plus the soft time abutting it.** Declined, tentative and externally-organised blocks are not occupied time.

⚠️ **Focus blocks move in both directions and in three senses** — to another date, later past 5:00 PM, and earlier within the day. **Direction of shift carries no signal** (§3).

⚠️ **MICHAEL'S OWN FORWARD PLANNING CAN DOUBLE-BOOK ITSELF, AND NOTHING ELSE CATCHES IT.** The 10/2 evening plan-burst (16:40:03 and 17:35:32–17:38:22) wrote four Monday blocks and produced **60 minutes of pairwise overlap**: `Scanner | FP&A - Revenue Mgmt` 09:00–10:30, `INBOX  Agent Maintenance & Asana Setup` 10:00–11:00, `Benchmark | QBO Spot-checking` 10:30–11:30. **First prospective overlap in the corpus** — distinct from instrument error 7, which is retroactive. **This is the single highest-value thing the EOD Planner could do on its first run: read the board Michael has just written and say that two blocks collide.**

---

## Known instrument errors

Seven measurement hazards that would otherwise corrupt this model silently.

1. **Retroactive blocks are work logs, not plans — the test is `updated` vs `end`, NOT `created` vs `start`.** Counts: 9/23 five of eleven, 9/24 four of seven, 9/25 four of ten, 9/28 one of seven, 9/29 three pure logs plus one in-flight, 9/30 two pure logs plus three in-flight, 10/1 one pure log, **10/2 two pure logs, one in-flight and two intraday plans**.
   - **A block created *during* its own window is in-flight — treat it as a log, and say so.** 10/2: `Mixmax | Revenue/Comp - Review Notes, Draft Agenda/Proposal`, created 11:38:41 onto 11:00–12:00.
   - ⚠️ **Apply the test to the block's position AT THE MOMENT IT IS SCORED. Anchor to the 07:30 snapshot: a block present there with `created` before its start is a plan, whatever happens to its stamps afterwards.** 10/2 needs this twice — both survivors carry `updated` stamps after their own ends.
   - ⚠️ **A block created before its start but AFTER the 07:30 snapshot is an intraday plan, not a log.** **10/2 gives two and BOTH RAN** (`DeepScribe | Tabs Setup Review`, created 11:03:57 for 13:15; `Attivo | Security Training`, created 11:55:18 for 14:45). They are **not scoreable against the morning board** and must not be dropped.
   - ⚠️ **ANCHORS MOVE TOO, AND A PROPOSAL THAT RIDES ONE INHERITS THAT.** 10/2: `INBOX Check-in` moved 08:30 → 09:00 and grew 30 → 45; `INBOX Review` moved 16:30 → 17:00.

2. **A retro block dates the work, not the output.** The correspondence lands *later* than the block's own window — **n=9, range 8 min to 3 h 45 m**. The send **always follows** the block, never precedes it. **Search forward from the block's end to the end of the next admin anchor.** 10/2 adds two positives — `Kestrel | RevRec Inquiry` (ends 10:15, email 11:48:15, **+93 min**) and `FR+Co/Mixmax Check in` (ends 15:30, email 16:38:13, **+68 min**) — and **one real negative**: the Scanner block ran 13:45–14:45 and produced **no outbound** by 17:30, which is exactly flag F4 at 11 business days.

3. **Classify a burst by the dates it writes — per block, because a burst can be MIXED.** A **log-burst** re-times *today* or a prior day; a **plan-burst** writes *future* dates. ⚠️ **The plan-burst's location is UNCONSTRAINED — search the whole day INCLUDING the anchors.** 10/2 replicates this a third time: four log-bursts (11:02–11:04, 11:38–11:55, 15:41:33–15:41:55, 17:33:14–17:33:44) and a **plan-burst at 16:40:03 and 17:35:32–17:38:22, straddling and following the 17:00–17:30 `INBOX Review` anchor.** Also: **sort by start and subtract pairwise overlap before summing logged minutes, and report the overlap.**

4. **A block missing from today may have migrated in EITHER direction — match on event id, never on title or absence.** ⚠️ **Use the FULL event id.** ⚠️ **Confirm a deletion with a title search as well as an id lookup.** ⚠️ **Record the event id of every block the day's board carries.**
   - ⚠️ **`search_events` is SEMANTIC, not literal, and returns an empty object on a title that exists.** On 10/2 it returned `{}` for "AI/Team Mgmt & Admin Tasks" while a forward-week `list_events` returned four live instances of exactly that title. **A semantic-search miss is not evidence of absence — fall back to a date-range enumeration.**
   - ⚠️ **A container's `updated` stamp can encode a series edit AND several instance deletions in one value.** When the container's stamp is the latest on the calendar, **enumerate the series across the forward week** before concluding anything about the day. Confirmed three times (9/30, 10/2 morning, 10/2 evening).

5. **A scored block's calendar position is mutable after the run that scored it — SO FREEZE THE DAY.** **RULING (2026-09-30): the measurement of record for a day is the one taken by that day's own evening run, against the stamps closest to the events.** A later re-time is recorded as **calendar churn**, not a new measurement. A day is re-scored **at most once**, and only to correct a *named* instrument error. **9/29 is frozen at 71.4%. 10/2 is frozen at 47.1%, with 30.8% recorded as its alternative reading.**

6. **Client work product is structurally invisible, so a production block's output can never be observed.** The Google Drive connector authenticates as `michael.p.christopher@gmail.com`, **not** the Attivo Workspace. **Record production output as unobservable, exactly as Suralink, Rippling, Ramp, Anrok and the portal layer are. Never score a production block as having produced nothing.** ⚠️ **The exception that proves it useful: Rippling's PAST-TENSE notices are direct evidence.** ⚠️ **But silence from an unobservable surface is still silence** — on 10/2 the 16:30 payroll deadline passed with **no** post-deadline notice by 17:38, and that is recorded as **unobservable**, not as a pass and not as a miss.

7. **The umbrella block: a late-day extension can swallow other blocks, and its face duration double-counts them.** **When an extended block contains other named blocks, its EXCLUSIVE minutes are the honest figure.** ⚠️ 9/30, 10/1 and 10/2 all had **zero** overlap across their logged blocks, so the hazard is intermittent, not structural, and the overlap figure must be reported either way. ⚠️ **Its prospective twin is new and more dangerous** — see §7's double-booking note: a retroactive overlap inflates a measurement, a prospective one guarantees a roll.

---

*Lineage: seeded 2026-09-21 from the ACA v4 specification §6 and §8, cross-checked against the `[ACA]` corpus in [[Open Brain]]. Measurements 2026-09-22 to 2026-10-02 from calendar `created`/`updated` stamps diffed against each day's 7:30 AM snapshot and reconciled against Gmail sent, Slack read by channel id and by thread, Fireflies recap mail, and Drive. Asana has been unavailable on all twenty runs, so §1, §2 and the tag half of §6 remain unmeasured; the EOD Planner has never run, so no agent-authored agenda has ever been scored.*

**Revisions** (last ten)

- 2026-09-22 — first measured values. §3 populated (n=1) and minutes-weighted columns added. §4 first row. New §7. Third instrument error added.
- 2026-09-23 — second measured day. `verb_class` replaces named/generic as §3's headline split. New §0. Containers excluded from the denominator. 70% cap superseded. §7 narrowed; fourth instrument error added.
- 2026-09-24 — third measured day. Coordination replicates. Pooled 46.2% → 42.2%. §7 gains discharge-by-meeting and the soft-time-overflow rule. Instrument error 3 split into log- and plan-bursts; error 4 widened.
- 2026-09-25 — fourth measured day, first withdrawal of a prior measurement. Pooled 42.2% → 38.3%. §3 gains the bimodal-survival warning. Instrument error 1 rewritten around `updated` vs `end`; new error 5.
- 2026-09-28 — fifth measured day, first falsification of the model's strongest claim. Pooled 38.3% → 43.4%. *Never propose production* **deleted**. Title axis promoted. New error 6.
- 2026-09-29 — sixth measured day; best on both axes (71.4%). Pooled 43.4% → 49.5%. **Title axis DEMOTED to CONTAMINATED**; scheduler rule 3 SUSPENDED. Scheduler rule 2 promoted at n=1. §6's *newest live thread* replaced by answerability. New error 7, the umbrella block.
- 2026-09-30 — seventh measured day; lowest survival (27.3%) on the highest-output day. Pooled 49.5% → 47.4%. **Instrument error 5 gains the FREEZE RULE**; 9/29 frozen. Plan-burst location declared unconstrained. §6's commitment-deferral rule DELETED. §3 bimodality WEAKENED. §5 and §7 gain REPURPOSED and DELETED-ONCE-ITS-VENUE-RAN.
- 2026-10-01 — eighth measured day; lowest survival (20.0%) AND lowest outbound. Pooled 47.4% → 43.4%. **§5's REPURPOSED DEMOTED to a failed attempt**; the n≤5 falsification sequence reaches n=5. §7 gains the WHOLE-DAY ROLL and three other shapes; arrival-recency n=4 → n=5, re-characterised as a selection effect. §6 gains **a proposal inherits the mobility of any container it names**. Title axis gains the named → generic direction.
- **2026-10-02 — ninth measured day; 47.1% on the highest logged-minute day in the corpus (480 exclusive, zero overlap, 300 self-scheduled).** Pooled **43.4% → 43.8%**; coordination 45.8% → **41.9%**; production 54.5% → **61.5%**, its first rise in four revisions, one day after returning zero separation. **The n≤5 falsification streak BREAKS at 5** — 10/1's block-length claim passes out of sample on a 60/60/135 board and becomes §3's provisional **scheduler rule 5, prefer the shorter block**; its direction-of-shift half is falsified. §5 gains a **fourth disposal that held — deferred to the end of the same day** — after the Asana hour ran at roll #4 instead of becoming roll #5, and gains **a rolled block GROWS** (135 → 180). §7 gains **a discharging venue can be withdrawn** (Viola moved the 10-bd flag's venue to 10/5), **the same-day counterparty-created venue** (72 min notice), **the counterparty-created recurring series**, **retroactive refill of a vacated window**, and **prospective self-overlap in Michael's own planning** (60 min on 10/5). §6 gains **arrival latency as the binding constraint on any agenda** (8 minutes, arrival to block) and **escalation by the person actually blocked**; the operational form's first apparent win is recorded as **untested, not vindicated**. §4 gains **a new client context can appear with no warning**. Error 2 n=6 → **n=9** with one real negative; error 4 gains **`search_events` is semantic** and the container-stamp rule, confirmed three times; error 6 gains **silence from an unobservable surface is still silence**.
