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

> ⚠️ **PARTLY MEASURED.** Seeded 2026-09-21 from the priors in the v4 spec §6. **Measurements from four days — 2026-09-22, 23, 24 and 25, 16 scoreable blocks** — are marked below; everything unmarked is still a guess recorded so it can be falsified. Four days is enough to say which splits **replicate**. It is not enough to fix a parameter.

**What this note is.** Only the congealed structure — current parameter values and the rules they imply. It is integrated, maintained and small. It is **not a log**: nightly observations are atomic and stay in [[Open Brain]] as `[ACA-PLAN]` thoughts.

**Update protocol.** `upsert_note` overwrites in full, so the evening run must `read_note` first, merge, and write back. Test **S8** asserts the read preceded the write. Revision line at the foot, capped at the last ten entries. **As a measured value replaces a prior, delete the prior** — this note should shrink as it learns.

---

## 0. The two axes — read them together or not at all

**Minutes-survival alone has now ranked the measured days wrongly in three different directions.**

| Day | Minutes survival | Flags cleared | Outbound artifacts | Verdict |
|---|---|---|---|---|
| 2026-09-22 | 68.8% | 0 of 8 | — | highest survival, lowest output |
| 2026-09-23 | 30.4% | **2 of 8**, both top-ranked | 2 emails | better than 9/22 |
| 2026-09-24 | 16.7% | 2 of 16, one red | **2 emails + 5 Slack + 1 Doc** | **highest output measured** |
| 2026-09-25 | 26.7% | **3 of 12** (Carrie, Pilot books, Kestrel) | 1 email + 1 Slack DM + 255 min of new commitment | mid on both |

**A plan displaced by more urgent work of the same client is a successful displacement and must not train the scheduler toward smaller plans.** A day can be almost entirely unplanned and still be the most productive one measured. **Always report clearance and artifacts alongside survival.**

## 1. What each number actually means

| Tag | Assumed planning minutes | Measured median | n | Drift |
|---|---|---|---|---|
| `1` | 30 | — | 0 | — |
| `2` | 90 | — | 0 | — |
| `3` | 165 | — | 0 | — |
| `4` | not schedulable | n/a | n/a | decompose marker, not a size |

Tags are readable only through Asana, unavailable on all **nine** runs to date. **Nothing in §1 can move until the connector is authorised.**

**Adjacent measurement that does not need tags** (n = 3): **externally-organised meetings run 121.7% of their booked minutes** — Kestrel 40 against 30, DeepScribe×Tabs 61 against 60, Attivo×Mixmax 45 against 30. Pooled 146 of 120. **Treat a counterparty's booking as a floor, not a box — and expect the overrun to cascade.** On 9/25 a 15-minute extension pushed two downstream blocks 1h45m later and is why both surviving blocks scored *ran shifted* rather than *ran as planned*.

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
| **Pooled** | **16** | **7** | **900** | **345** | **38.3%** |

**38% is the working figure** (42.2% at n=3, 46.2% at n=2). The 70% seed cap is superseded three times over. Do not hard-code 38 either — re-measure.

⚠️ **Survival is bimodal per block, not a uniform haircut** (2026-09-25(F)). On 9/25 the two surviving blocks each kept **100%** of 30 minutes; the two that did not kept **0** of 90 and **0** of 75. The aggregate rate hides that. **Size a block at its nominal length and expect it to run or vanish** — do not shrink every block to ~40% of nominal.

### The split that replicates: `verb_class`

| `verb_class` | Blocks | Planned min | Logged min | **Rate** | Replicates? |
|---|---|---|---|---|---|
| **coordination** | 14 | 780 | 300 | **38.5%** | **yes, n=4 days** — 50%, 30%, 44%, 27% |
| **production** | 3 pre-planned | 150 | 300 | decorative | **0 pre-planned on 4 of 4 days** — see below |

| Title type | Blocks | Planned min | Logged min | Rate | Replicates? |
|---|---|---|---|---|---|
| Names a deliverable | 8 | — | — | day-rates 167%, 30%, 100%, 100% | **favours named on 3 of 4 days** |
| Generic / topic only | 11 | — | — | day-rates 50%, 80%, 0%, 15.4% | — |

**Coordination at ~38% pooled, banded 27–50%, is the model's most stable measured parameter.** The honest statement at n=4 is *"well under half,"* not a point value.

**The title axis stopped flipping** and now favours named-deliverable on 3 of 4 days. Upgraded from *"does not replicate"* to *"favours named, ordering not yet a point estimate."* It does **not** displace `verb_class`. Lesson 2026-09-02(A)'s 7-for-7 result stays narrowed, not refuted (2026-09-07(B)). ⚠️ The per-day minute totals for this axis were not carried in earlier revisions and cannot be reconstructed; the columns exist from 2026-09-25 forward so the axis can eventually be pooled.

### ⚠️ Production is never pre-planned — the strongest finding in the model

**Across four measured days Michael has pre-planned ZERO client-analysis production blocks** (2026-09-24(I), 2026-09-25(B)). Every production block in the corpus was created *during or after* its own window; the only pre-planned production block was internal. The 300 logged production minutes are retroactive logs against **zero** planned minutes, which is why the old "140% production survival" row was decorative and has been deleted.

**SCHEDULER RULE: never propose a production block.** Propose the coordination that forces the artifact, and name the artifact in the flag list instead. The agent proposed production on 9/23 (`3H` audit backup), 9/24 (`2H` audit backup) and 9/25 (`2M` write the answers to Jennifer) and Michael ran coordination all three times.

**Scheduler rules from this section:**
1. Size a coordination block at **nominal**, and expect it to run or vanish (not to shrink).
2. **Anchor it to the venue that forces it.** ⚠️ **DEMOTED to weakly supported** (2026-09-25(D)): its single supporting observation — `Mixmax | Meeting Prep/Agenda` keeping 45 of 45 on 9/24 — was re-filed onto 9/25 underneath the measurement. Not falsified; it has no live evidence.
3. **Never propose production.** See above.

## 4. Switching cost

Seed rule: **maximum five distinct client contexts per day**, batched contiguously.

| Contexts in day | Days | Completion (minutes basis) |
|---|---|---|
| 4 (+1 internal) | 1 | 79% |
| 3 (+1 internal) | 1 | 27% |
| 2 (+1 internal) | 2 | 30%, 17% |

**Four days, no relationship.** Contiguity has been violated on all four with no measurable cost. **Context count is not predictive of anything yet, and the seed limit of five has never been approached.**

## 5. Roll history

A task at three rolls stops being silently re-planned and becomes a flag (engine rule 9).

⚠️ `rolls:` has never been readable or writable — it is an Asana fenced-block field. **0 increments have ever been applied across nine runs, against 4 directly observed rolls.**

| Block / workstream | Observed rolls | Status |
|---|---|---|
| `Client/Double Review (...)` (`7u71d6h0k1grovgju1jgeao76c`) | **3, final** | **DELETED 2026-09-25** at its fourth placement — `get_event` returns *deleted*. **Rule 9's "cut it" is a real disposal mode**, reached by Michael independently. What it held is unknown; `Monthly Close Prep (...)` (9/28 14:15–15:45, same 90-min shape) appeared in the same burst and may or may not be its successor |
| `Scanner \| Updates` (`5k3hffa1uap4kj2p0h3qfho3u9`) | **1** (9/25 → 9/28) | below threshold; re-planned 9/28 10:00–11:30 |
| `Scanner \| Close: Aug Revenue` | 5 (as of 2026-09-15) | past threshold; unverifiable until the connector returns |
| Mixmax audit backup `C-20260917-05` · DeepScribe/Tabs `C-20260910-05` | **n/a — never placed** | **Worse than rolled.** Five days flagged, zero blocks ever created. A never-placed item cannot roll, so the roll instrument is blind to the model's two most overdue items |

**Rolls are written at EOD, in the same burst that plans tomorrow — not when the conflict arises** (2026-09-23(H), confirmed 9/24 and 9/25). **Consequence: the 4:15 PM EOD Planner cannot see the day's rolls and must mark tomorrow's free windows provisional.** This is what makes the evening run's STEP 11 load-bearing.

## 6. Tag-prediction accuracy

| | Proposed | Unchanged by MC | Corrected | Accuracy |
|---|---|---|---|---|
| Number | 3 | 0 | 0 | **unmeasurable** |
| Letter | 3 | 0 | 0 | **unmeasurable** |

⚠️ This stream cannot open until the EOD Planner runs once and Michael sets a real tag against an agent proposal. **No agent proposal to date has been taken up at all**, and the EOD Planner has still never run — it did not fire on its 2026-09-25 go-live day.

**What is scoreable is the agent's own sizing and target selection, and target selection is the bigger error by far.**

- 9/23: proposed `3H` (165 min) into a 120-minute window — violated G1 before Michael saw it; the deliverable took ~30 minutes.
- 9/24: sizing corrected to `2H` into a 105-minute window (G1-conforming) — still not taken; the deliverable was wrong.
- 9/25: `2M` into 90 of a 120-minute hold (G1-conforming) — **still not taken.** The hold's surviving 60 minutes went to two Mixmax *coordination* blocks. Right client, right window, wrong verb class.

**THE RULE, NOW AT n=4: target the NEWEST live thread — not the nearest deadline, and not an older live thread.** On 9/22–9/24 the morning went to whichever Mixmax correspondence thread was live, never to the dated audit backup. On 9/25 it went further: the afternoon went to a pricing doc posted at 12:04 rather than to the three action items **Michael had committed to live, in front of the client, at 09:30 that morning**. An open thread with a counterparty actively posting predicts tomorrow's minutes better than any dated deadline *and* better than his own same-day verbal commitment.

**A displacement proposal is already stale if a counterparty posted after it was written.** The midday run of 9/25 wrote its proposal 41 minutes after the thread that beat it went live.

**And name the counterparty who must *receive* the artifact, not the one who produced it.**

⚠️ **A parameter written here but not read into the proposal is not part of the engine** (2026-09-24(K)). **Every displacement proposal must name which rule of this note it applied.**

## 7. Counterparty volatility and refill

| Disposal mode | 9/22 | 9/23 | 9/24 | 9/25 | Note |
|---|---|---|---|---|---|
| Cancelled by counterparty | 1 | 1 | 1 | 0 | |
| Moved by counterparty | 1 | 0 | 0 | 0 | |
| Deleted by Michael (containers) | 2 | 2 | 3 | 1 | |
| Moved within the day by Michael | — | — | 3 | 4 | |
| Evacuated by a competing client | 1 | 1 | 0 | **1** | 9/25: `Scanner \| Updates` evacuated by the Mixmax Gen 2 thread |
| Rolled forward by Michael at EOD | 0 | 2 | 1 | **1** | |
| Retro-filed onto a prior day | 0 | 1 | 0 | 0 | **does not replicate** — 1 for 3 |
| **Retro-filed onto a LATER day** | — | — | — | **1** | **new** — `Meeting Prep/Agenda` moved from 9/24 onto 9/25 after the 9/25 window passed |
| Disposed by scheduling a meeting | 0 | 0 | 1 | 0 | |
| **Deleted outright at the roll threshold** | 0 | 0 | 0 | **1** | **new** — see §5 |

⚠️ **Block disposal is not primarily counterparty-driven.** Pooled: **5 of 23.**

**Discharge-by-meeting** (2026-09-24(F)), **narrowed 2026-09-25(L):** when a flagged item acquires a dated venue **with the counterparty in it**, it stops being overdue. **A solo prep block does not discharge anything.** On 9/25 Jennifer's questions acquired `Mixmax | Accounting Proposal Follow-up` (9/28 11:30–12:15, FOCUS_TIME, no attendees) and stayed amber, correctly — the email Michael committed to in the 09:30 sync did not go out.

**Refill: freed time is filled by re-pointing a block that already exists somewhere on the same day.** Latency 52–59 min at n=3 (55 min 9/22, ≤59 min 9/23, 52 min 44 s 9/24). **Not re-measured 9/25** — the freed afternoon was filled by a block created after the fact, so no latency could be observed.

**Scheduler consequence, and it is cheap:** freed time cannot be steered by priority after the hour opens — but the capture block **only has to exist somewhere on the same day, in either direction.**

⚠️ **Size a capture block to the vacancy plus the soft time abutting it** (2026-09-24(E)). Declined, tentative and externally-organised blocks are not occupied time.

⚠️ **Focus blocks move in both directions.** The corpus rule that focus blocks move only later is **narrowed to client analysis work displaced by incoming client work.** Internal and continuation production work absorbs freed time rather than yielding it.

---

## Known instrument errors

Five measurement hazards that would otherwise corrupt this model silently.

1. **Retroactive blocks are work logs, not plans — and the test is `updated` vs `end`, NOT `created` vs `start`** (revised 2026-09-25(C)). The created-versus-start test is fooled by a block that *moved*: `Mixmax | Meeting Prep/Agenda` has a `created` of 9/24 11:36 and was placed onto 9/25 08:45–09:30 at 12:15 on 9/25, after that window passed. **An event whose last `updated` stamp post-dates its own `end` is retroactively placed and cannot be scored for plan adherence, however old its `created`.** On 9/23 five of eleven executed blocks were logs; on 9/24, four of seven; on 9/25, four of ten under the corrected test. **A block created *during* its own window is in-flight — treat it as a log, and say so.**

2. **A retro block dates the work, not the output.** The correspondence lands *later* than the block's own window — 27 minutes later on 9/25 (`Follow-up - Summary Reporting` 11:15–11:45, email 12:12:23). A same-window search returns a false negative.

3. **Classify a burst by the dates it writes — per block, because a burst can be MIXED** (revised 2026-09-25(I)). Blocks are re-timed in clusters of seconds. Two kinds:
   - A **log-burst** re-times *today* and follows an outbound message. Confirmed n=3 days / 6 bursts: 77 s, 28 s, 25 s (9/23); 13 s, 53 s (9/24); **3 m 24 s (9/25)**. The mechanism replicates; the 0–120 s window does not. **Search Gmail and Slack in the five minutes before a burst.**
   - A **plan-burst** writes *future* dates and sits inside the `INBOX Review + Next Day Planning` block. n=2: 9/24 at 17:24:47–17:27:07, 9/25 at 16:50:45–16:55:02. **The day's owed replies land in the same anchor** — Carrie Sechel's was answered at 16:59:04 on 9/25, after both proposed windows.
   - **A single continuous sequence can contain both.** 9/25's 16:37:12–16:55:02 wrote one same-day log and five future plans. Classify each written block by its own dates; report the burst as mixed.
   Also: sort by start and subtract pairwise overlap before summing logged minutes, and report the overlap. **Trust a tidy log's sequence, not its durations.**

4. **A block missing from today may have migrated in either direction — match on event id, never on title or absence** (2026-09-23(G), 2026-09-24(G)). On 9/25 this changed three answers: `Scanner | Updates` had rolled (createdTime intact), `Client/Double Review` was genuinely deleted (`get_event` → *deleted*), and `Mixmax | Accounting Proposal Notes` had merely been **renamed** to `Accounting Admin`. **Search prior days and the forward week, use `created` as the tell, and confirm a deletion with `get_event` on the id rather than inferring it from absence.**

5. **A scored block's calendar position is mutable after the run that scored it** (2026-09-25(D)). `Mixmax | Meeting Prep/Agenda` was scored 45-of-45 on 9/24 and then moved onto 9/25, so the same 45 minutes are claimed on two days. **Per-block minutes are provisional; anchor durable measurements to send timestamps and Doc `createdTime`s, which do not move.** When a prior day's measurement loses its supporting event, demote the rule it supported rather than deleting or defending it.

---

*Lineage: seeded 2026-09-21 from the ACA v4 specification §6 and §8, cross-checked against the `[ACA]` corpus in [[Open Brain]]. Measurements 2026-09-22 to 2026-09-25 from calendar `created`/`updated` stamps diffed against each day's 7:30 AM and 12:30 PM snapshots and reconciled against Gmail sent and Slack. Asana has been unavailable on all nine runs, so §1, §2, §5 and §6 remain unmeasured; the EOD Planner has never run, so no agent-authored agenda has ever been scored.*

**Revisions** (last ten)

- 2026-09-21 — created, seeded with v4 priors. No measurements.
- 2026-09-22 — first measured values. §3 populated (n=1) and minutes-weighted columns added. §4 first row. New §7. Third instrument error added.
- 2026-09-23 — second measured day. `verb_class` replaces named/generic as §3's headline split. New §0. Containers excluded from the denominator. 70% cap superseded by 46.2%. §5 gains the EOD roll-burst finding. §6 gains the first scoreable sizing error. §7 narrowed; fourth instrument error added.
- 2026-09-24 — third measured day. Coordination replicates at 43.2%; the title split flips a third time. Pooled 46.2% → 42.2%. §6's thread-velocity rule promoted to n=3. New §6 warning: a parameter read but not applied is not part of the engine. §5 puts `Client/Double Review` at the threshold. §7 gains discharge-by-meeting, tightens refill to 52–59 min, adds the soft-time-overflow rule. Instrument error 3 split into log- and plan-bursts; error 4 widened.
- 2026-09-25 — fourth measured day, and the first on which a prior measurement was withdrawn. Pooled survival 42.2% → **38.3%**; coordination 43.2% → **38.5%** (band 27–50%). **The 140% production row deleted and replaced by the finding that production is pre-planned on 0 of 4 days — now the model's strongest claim, and a new scheduler rule: never propose production.** §3 gains the bimodal-survival warning; **scheduler rule 2 demoted** after its supporting observation was re-filed onto another day. §1 externally-organised overrun 117% → **121.7%** (n=3). §5: `Client/Double Review` **deleted at its fourth placement** — rule 9's "cut it" is a real mode; never-placed items recorded as blind to the roll instrument. §6 restated as **newest-live-thread**, n=4, and the staleness of a midday proposal named. §7 gains two new disposal modes and narrows discharge-by-meeting to venues with the counterparty in them. **Instrument error 1 rewritten around `updated` vs `end`**; error 3 gains the mixed-burst case and a widened latency; **new error 5: a scored block's position is mutable.**
