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

> ⚠️ **PARTLY MEASURED.** Seeded 2026-09-21 from the priors in the v4 spec §6. **Measurements from six days — 2026-09-22, 23, 24, 25, 28 and 29, 26 scoreable blocks** — are marked below; everything unmarked is still a guess recorded so it can be falsified.
>
> ⚠️ **THREE CONSECUTIVE DAYS HAVE NOW FALSIFIED A CLAIM FITTED AT n≤5 ON ITS FIRST OUT-OF-SAMPLE TEST** — 9/28 the production rule, 9/29 both the narrowed production form and the title axis. **That sequence is the most robust finding in this note and it is about the loop, not about Michael. Stop promoting four- and five-day splits to rules.**

**What this note is.** Only the congealed structure — current parameter values and the rules they imply. It is integrated, maintained and small. It is **not a log**: nightly observations are atomic and stay in [[Open Brain]] as `[ACA-PLAN]` thoughts.

**Update protocol.** `upsert_note` overwrites in full, so the evening run must `read_note` first, merge, and write back. Test **S8** asserts the read preceded the write. Revision line at the foot, capped at the last ten entries. **As a measured value replaces a prior, delete the prior** — this note should shrink as it learns.

---

## 0. The two axes — read them together or not at all

**Minutes-survival alone has now ranked the measured days wrongly in four different directions.**

| Day | Minutes survival | Flags cleared | Outbound artifacts | Verdict |
|---|---|---|---|---|
| 2026-09-22 | 68.8% | 0 of 8 | — | high survival, lowest output |
| 2026-09-23 | 30.4% | **2 of 8**, both top-ranked | 2 emails | better than 9/22 |
| 2026-09-24 | 16.7% | 2 of 16, one red | 2 emails + 5 Slack + 1 Doc | worst survival, strong output |
| 2026-09-25 | 26.7% | **3 of 12** | 1 email + 1 Slack DM + 255 min new commitment | mid on both |
| 2026-09-28 | 58.3% | 2 of 14 | 1 email + 0 Slack, 330 min on one client thread | high survival, thin output, **two red deadlines untouched for a 7th day** |
| **2026-09-29** | **71.4%** | **3 of 18** + 4 staleness clocks reset | **5 emails + 1 Slack** | ⚠️ **the best day on BOTH axes at once** |

**A plan displaced by more urgent work of the same client is a successful displacement and must not train the scheduler toward smaller plans.** A day can be almost entirely unplanned and still be the most productive one measured. **Always report clearance and artifacts alongside survival.**

⚠️ **9/28's warning — "a high-survival day is not a good day either" — is now bounded rather than general.** On 9/29 the two axes agreed for the first time: highest survival AND highest output. The honest reading at n=6 is that **survival and output are uncorrelated, not anti-correlated.** Neither predicts the other; both must be reported.

⚠️ **And neither predicts the deadline.** On the best day ever measured, the 9/30-dated Mixmax audit backup took zero minutes for the **ninth** consecutive day. **A good day and a day that clears its deadlines are different things, and only the flag list tracks the second.**

## 1. What each number actually means

| Tag | Assumed planning minutes | Measured median | n | Drift |
|---|---|---|---|---|
| `1` | 30 | — | 0 | — |
| `2` | 90 | — | 0 | — |
| `3` | 165 | — | 0 | — |
| `4` | not schedulable | n/a | n/a | decompose marker, not a size |

Tags are readable only through Asana, unavailable on all **fourteen** runs to date. **Nothing in §1 can move until the connector is authorised.**

**Adjacent measurement that does not need tags** (n = 4): **externally-organised meetings run 100.6% of their booked minutes** — Kestrel 40/30, DeepScribe×Tabs 61/60, Attivo×Mixmax 45/30, **Attivo×ResFrac 15/40**. Pooled 161 of 160.

⚠️ **"TREAT A COUNTERPARTY'S BOOKING AS A FLOOR" IS WITHDRAWN** (2026-09-29(G)). It rested on three points that happened to agree. The 9/29 ResFrac check-in was booked 12:00–12:40 and shortened to 12:00–12:15 inside Michael's own log-burst — a record of what the meeting ran, not a re-booking — and took a three-point 121.7% figure to 100.6% in one observation. **At n=4 a counterparty's booking is an estimate with a wide TWO-SIDED error, 37.5% to 152% observed. Plan no cascade around an assumed overrun.**

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
| 2026-09-28 | 5 | 3 | 360 | 210 | **58.3%** ⬆ amended |
| **2026-09-29** | **6** | **3 + 1 partial** | **315** | **225** | **71.4%** — highest measured |
| **Pooled** | **27** | **14** | **1575** | **780** | **49.5%** |

⚠️ **9/28 was amended upward** (2026-09-29(I)): `ResFrac | New Update/Agenda Doc` was scored PENDING on 9/28 because its deferred 19:00–19:15 window fell after that run's 17:45 firing. On 9/29 Michael retro-filed it onto 9/28 15:15–15:30, resolving it as ran, 15 of 15. **345/195 → 360/210, 56.5% → 58.3%.** Per instrument error 5 a prior day's measurement is provisional; this is the first case where one *gained* evidence.

**49.5% is the working figure, and it has now moved 46.2 → 42.2 → 38.3 → 43.4 → 49.5 across five revisions — in both directions twice.** It is not converging and the band has widened to **16.7–71.4%**. **The honest statement is "roughly half, banded 17–71%." Do not hard-code 49 any more than 38 or 70.**

⚠️ **Survival is bimodal per block — 15 blocks, three days, ONE intermediate outcome, and that one is a decomposition** (2026-09-25(F), 2026-09-28(F), narrowed 2026-09-29(F)). 9/25: 100/100/0/0. 9/28: 125/100/0/0. 9/29: 0/0/100/100/100/**50**. The 50% is `Monthly Close Prep (...)`, 45 of 90 — **not a haircut**: Michael split it into two client-named blocks totalling 45 minutes and rolled the residue. **The partial equals the sum of its named pieces exactly.**

**Rule: a block runs whole or vanishes whole UNLESS IT IS DECOMPOSED.** Size at nominal. Shrinking every block to ~49% of nominal would produce a plan in which nothing is the right size. The prediction target is **which** blocks vanish, not by how much each shrinks.

### ⚠️ The title axis is CONTAMINATED — do not use it until it is re-derived

| Title type (scored at the morning snapshot) | Day-rates | Favours named? |
|---|---|---|
| Names a deliverable | 167%, 30%, 100%, 100%, 118%, **66.7%** | 4 of 6 days |
| Generic / topic only | 50%, 80%, 0%, 15.4%, 0%, **75.0%** | — |

**2026-09-28 promoted this axis to co-equal with `verb_class` on the strength of one day that isolated it (named 118%, generic 0%). 2026-09-29 re-ran the experiment on the identical two generic blocks at the identical 180 minutes and the axis INVERTED** (2026-09-29(A)).

**And the instrument is contaminated** (2026-09-29(B)). `Scanner | Updates` ran its full 90 minutes on 9/29 and Michael renamed it **`Scanner | Invoicing/Revenue Updates` at 12:07:47 — seven minutes after the block closed.** Same event id, same minutes, a title that now names its deliverable. **He retitles generic blocks into named ones once he knows what he did in them.** Every measurement before 9/29 was taken against the EOD calendar, so *"named blocks survive"* was partly reading the causation backwards.

**MANDATORY FROM 2026-09-29: score a block's title AS IT STOOD IN THE MORNING SNAPSHOT, never as it stands at EOD.** The six day-rates above are so scored only for 9/29; 9/22–9/28 need re-deriving against their own snapshots before the axis can be trusted at all.

**Neither of 9/29's named losses was about its title.** `Paulex | NIH Grant Research` rolled because a counterparty moved its venue; `ResFrac | New Update/Agenda Doc` vanished because the work had already happened. **On current evidence what decides a block's fate is what happens to the venue or the thread it serves, not how the block is titled.**

### `verb_class`

| `verb_class` | Blocks | Planned min | Logged min | **Rate** | Replicates? |
|---|---|---|---|---|---|
| **coordination** | 21 | 1275 | 630 | **49.4%** | **yes, n=6 days** — 50%, 30%, 44%, 27%, 58%, 89% |
| **production** | 5 | 360 | 285 | **79.2%** | n=2 days, 4 blocks — too thin to act on |

⚠️ **"Production is never pre-planned the evening before" is DELETED.** That narrowing was written on 9/28 and falsified within four hours: `Mixmax | Pricing Plan - Excel Model` was created **21:45:16 on 9/28 for a 13:15 start on 9/29**, 15 h 30 m ahead. It ran — shifted to 15:30 after Jason Tatum's 13:35 inbound evacuated its original window — and logged its full nominal 60 exclusive minutes. **Production is pre-planned, at any horizon, and when it runs it runs whole.**

**Scheduler rules from this section:**
1. Size a block at **nominal**, and expect it to run or vanish — not to shrink, unless it is decomposed.
2. **Anchor it to the venue that forces it.** ✅ **SUPPORTED at n=1** (2026-09-29(D)), promoted from *weakly supported, no live evidence*. Anh Le moved `Paulexbio <> Attivo Sync` to 9/30 at 09:15:08; Michael moved its prep block `Paulex | NIH Grant Research` to 9/30 at 13:56:12, preserving the ahead-of-meeting relationship. **Corollary: when a counterparty moves a meeting, look for a prep block anchored to it before treating the freed window as capacity.**
3. ~~Prefer a title that names its artifact.~~ **SUSPENDED** — see the contamination warning above. Do not encode it as a scheduler rule until the axis is re-derived against morning snapshots.
4. **Do not encode `verb_class` as a scheduler rule at n=6.** The *never propose production* rule was deleted on 9/28 after producing the wrong answer on its first test. Propose the window and name the artifact; leave the verb to Michael.

## 4. Switching cost

Seed rule: **maximum five distinct client contexts per day**, batched contiguously.

| Contexts in day | Days | Completion (minutes basis) |
|---|---|---|
| **5** | 1 | **71.4%** — the best day measured |
| 4 (+1 internal) | 1 | 79% |
| 3 (+1 internal) | 1 | 27% |
| 2 (+1 internal) | 3 | 30%, 17%, 58.3% |

⚠️ **The seed cap of five was reached for the first time on 2026-09-29 — and that was the highest-survival day in the corpus.** Six contexts were planned (Mixmax, Scanner, ResFrac, Paulex, DeepScribe, Kestrel), five carried logged minutes, and Mixmax was non-contiguous across a five-hour gap. **Six days, no relationship in either direction. Context count is not predictive of anything, and the cap is refuted rather than merely un-approached.** Keep G5 as a reporting line, not as a constraint on the scheduler.

## 5. Roll history

A task at three rolls stops being silently re-planned and becomes a flag (engine rule 9).

⚠️ `rolls:` has never been readable or writable — it is an Asana fenced-block field. **0 increments across fourteen runs, against 10 directly observed rolls.**

| Block / workstream | Observed rolls | Status |
|---|---|---|
| `Monthly Close Prep (...)` (`07b3d937if5c2v2dljba475qvf`) | **2** (9/28→9/29, 9/29→9/30) | ⚠️ **One below the flag threshold**, third placement already booked 9/30 15:15–16:15, shrunk 90→60. **No longer opaque** — decomposed in arrears on 9/29 into Scanner (15 min) + DeepScribe (30 min) |
| `Paulex \| NIH Grant Research` (`1co6khjiailhcme08eqg5okatk`) | **1** (9/29→9/30) | **Rolled WITH its venue**, not displaced — see §7 |
| `Scanner \| Updates` → `Scanner \| Invoicing/Revenue Updates` (`5k3hffa1uap4kj2p0h3qfho3u9`) | **2, frozen** | ✅ **RAN 9/29**, 90 of 90, two invoicing emails. Rule 9 stood down at the last placement before the threshold |
| `Client/Double Review (...)` (`7u71d6h0k1grovgju1jgeao76c`) | **3, final** | **DELETED 2026-09-25** at its fourth placement. **Rule 9's "cut it" is a real disposal mode**, reached by Michael independently |
| `Scanner \| Close: Aug Revenue` | 5 (as of 2026-09-15) | past threshold; unverifiable until the connector returns |
| Mixmax audit backup `C-20260917-05` · DeepScribe/Tabs `C-20260910-05` | **n/a — never placed** | **Worse than rolled.** Nine days flagged, zero blocks ever created. A never-placed item cannot roll, so the roll instrument is blind to the model's two most overdue items |

**Rolls are written when the displacing work takes the window** — usually, but not always, in the EOD burst. On 9/28 both were written mid-afternoon in flight; on 9/29 one at 13:56 (following a venue move) and one at 17:13. **None has ever been written inside `INBOX Review`.**

**Consequence for the 4:15 PM EOD Planner:** tomorrow's free windows are provisional, but **some rolls are already visible at 4:15 PM on most days**. Read the calendar; do not assume they cannot be there.

## 6. Tag-prediction accuracy

| | Proposed | Unchanged by MC | Corrected | Accuracy |
|---|---|---|---|---|
| Number | 5 | 0 | 0 | **unmeasurable** |
| Letter | 5 | 0 | 0 | **unmeasurable** |

⚠️ This stream cannot open until the EOD Planner runs once and Michael sets a real tag against an agent proposal. **No agent proposal has ever been taken up**, and the EOD Planner has still never fired.

**What is scoreable is the agent's own target selection — seven consecutive misses, and 9/29 localised the error to one dimension:**

| Day | Proposed | Result |
|---|---|---|
| 9/23 | `3H` (165 min) into a 120-minute window | violated G1 before Michael saw it; the deliverable took ~30 min |
| 9/24 | `2H` into a 105-minute window | not taken; wrong deliverable |
| 9/25 | `2M`, right client, right window | **wrong verb class** |
| 9/28 | `1L` coordination into the day's only free window | **right window**, filled with 180 min of production — wrong verb class, sign inverted |
| **9/29** | **`1L`, reply to Jennifer confirming the $14.8–15.0k range, into the only free window** | ⚠️ **client HIT, counterparty HIT, thread MISS.** Michael wrote to Jennifer twice that day and never touched the pricing thread. The free window went unused |

### ⚠️ THE RULE, REPLACING "TARGET THE NEWEST LIVE THREAD": ANSWERABILITY SELECTS THE THREAD

On 2026-09-29 five asks were live. Michael answered four and deferred one, and the ordering is not recency (2026-09-29(C)):

| Ask | Latency | What it asks for |
|---|---|---|
| Jason — *"fix this file and resend"* | **19 m 41 s** | a mechanical correction |
| Jennifer — PEO Q2, Nov 1 timing | **45 m 50 s** | a one-line judgement from knowledge |
| Anh — Kestrel DE tax estimate | **5 h 01 m** | review-and-approve someone else's work |
| Jennifer — PEO Q1, GAAP treatment | **17 h 58 m** | an explanation from knowledge |
| **Jennifer — *"is $14,800–$15,000 a reasonable monthly range?"*** | **27 h +, UNREAD** | **a number he must commit his firm to** |

The deferred one is the **oldest**, from the **fastest-responding counterparty in the corpus** (1 h 49 m), **starred**, and from the person he answered twice that day.

**He answers what he can answer from knowledge in one or two lines, roughly in arrival order. He defers what commits his firm to a price.** *Newest live thread* survives only as a predictor of **client**, which is where it has always been right. **At n=1 this is a hypothesis with a scheduled test: if the pricing question is answered on 9/30 while other one-line asks turn around inside a day, delete it.**

⚠️ **CHANNEL SILENCE IS A MEDIUM PREFERENCE, NOT UNRESPONSIVENESS.** On 9/29 Jason posted *"I just sent you an email"* in `#attivo-mixmax` at 13:40:31; Michael replied **by email at 13:54:55** and posted nothing to the channel, which now stands at 4 business days silent. **Never count channel staleness as an unanswered-counterparty flag when the same counterparty was answered in another medium the same day.** Flag the *ask*, not the channel — Jason's substantive 9/25 Gen 2 ask is genuinely unanswered at 3 bd, and that is the flag that belongs in the list.

**A displacement proposal is already stale if a counterparty posted after it was written.**

**And name the counterparty who must *receive* the artifact, not the one who produced it.**

⚠️ **A parameter written here but not read into the proposal is not part of the engine** (2026-09-24(K)). **Every displacement proposal must name which rule of this note it applied.**

## 7. Counterparty volatility and refill

| Disposal mode | 9/22 | 9/23 | 9/24 | 9/25 | 9/28 | **9/29** | Note |
|---|---|---|---|---|---|---|---|
| Cancelled by counterparty | 1 | 1 | 1 | 0 | 0 | 0 | |
| Moved by counterparty | 1 | 0 | 0 | 0 | 0 | **1** | Anh Le moved the Paulexbio sync to 9/30 |
| Deleted by Michael (containers) | 2 | 2 | 3 | 1 | 0 | 0 | |
| Moved within the day by Michael | — | — | 3 | 4 | 6 | **8** | **new maximum** |
| Evacuated by a competing client | 1 | 1 | 0 | 1 | 0 | 0 | |
| **Evacuated by the SAME client's other work** | — | — | — | — | 2 | **1** | replicates — Jason's inbound fix-request displaced the Mixmax Excel Model block |
| Rolled forward by Michael | 0 | 2 | 1 | 1 | 2 | **2** | |
| **Rolled WITH its venue** | — | — | — | — | — | **1** | **new** — the prep followed the meeting, not a lost contest. §3 rule 2 |
| Retro-filed onto a prior day | 0 | 1 | 0 | 0 | 0 | **1** | ⚠️ **REPLICATES** — 2 of 6 days, no longer "does not replicate" |
| Retro-filed onto a LATER day | — | — | — | 1 | 0 | 0 | |
| Disposed by scheduling a meeting | 0 | 0 | 1 | 0 | 1 | 0 | |
| Deleted outright at the roll threshold | 0 | 0 | 0 | 1 | 0 | 0 | see §5 |
| **Decomposed in arrears** | — | — | — | — | — | **1** | **new** — the only source of a partial survival, §3 |
| Deferred past 17:00 within the day | — | — | — | — | 2 | **2** | |

⚠️ **Block disposal is not primarily counterparty-driven.** Pooled: **6 of 44.**

**Discharge-by-meeting** (2026-09-24(F)), **narrowed 2026-09-25(L):** when a flagged item acquires a dated venue **with the counterparty in it**, it stops being overdue. **A solo prep block does not discharge anything.** Confirmed again 9/29: ResFrac at 8 business days was discharged by the 12:00 weekly check-in with Tristen, Carl, Garrett and aperez in the room.

⚠️ **ARRIVAL RECENCY BEATS DEADLINE PROXIMITY EVEN WHEN THE ARRIVING ITEM HAS NO DATE AND NO OWNER** — n=3 (2026-09-25, 2026-09-28(J), 2026-09-29). On the best day ever measured, five clients got minutes and **the 9/30-dated Mixmax audit backup got zero for the ninth consecutive day.** **This is the model's most reliable predictor of where a day's minutes go, and the scheduler cannot fix it — only the flag list can.**

**Refill: freed time is filled by re-pointing a block that already exists somewhere on the same day.** Latency 52–59 min at n=3, not re-measured since 9/24.

⚠️ **Size a capture block to the vacancy plus the soft time abutting it** (2026-09-24(E)). Declined, tentative and externally-organised blocks are not occupied time.

⚠️ **Focus blocks move in both directions and in three senses** — to another date, later within the day past 5:00 PM, and **earlier within the day** (new 9/29: `Mixmax | PEO Follow-up` moved 11:30 → 09:30 and ran there). The corpus rule that focus blocks move only later is dead.

---

## Known instrument errors

Seven measurement hazards that would otherwise corrupt this model silently.

1. **Retroactive blocks are work logs, not plans — the test is `updated` vs `end`, NOT `created` vs `start`** (revised 2026-09-25(C)). **An event whose last `updated` stamp post-dates its own `end` is retroactively placed and cannot be scored for plan adherence, however old its `created`.** Counts: 9/23 five of eleven, 9/24 four of seven, 9/25 four of ten, 9/28 one of seven, 9/29 **three pure logs plus one in-flight**.
   - **A block created *during* its own window is in-flight — treat it as a log, and say so.** 9/29's `Mixmax | Cash Flow Review` (created 17:32:09 onto 17:30–18:00) is the clean case. ⚠️ `prompts/evening-evaluation.md` STEP 3's two-row table has no row for this and was amended 2026-09-29 to match; **where a routine prompt and this note disagree on an instrument, this note is the later and better-evidenced document** (2026-09-29(J)).
   - ⚠️ **Apply the test to the block's position AT THE MOMENT IT IS SCORED, not to its current stamp.** A block that ran and was then re-timed within the same day fails the naive test although it was a genuine plan. **Anchor to the 07:30 snapshot: a block present there with `created` before its start is a plan, whatever happens to its stamps afterwards.**

2. **A retro block dates the work, not the output.** The correspondence lands *later* than the block's own window — **n=5, range 8 min to 3 h 45 m** (8 min 9/04, 27 min 9/25, 33 min and 1 h 25 m 9/29, 3 h 45 m 9/21). The send **always follows** the block, never precedes it. **Search forward from the block's end to the end of the next admin anchor; a same-window search returns a false negative.**

3. **Classify a burst by the dates it writes — per block, because a burst can be MIXED** (revised 2026-09-25(I)). A **log-burst** re-times *today* and follows an outbound message. A **plan-burst** writes *future* dates. 9/29's 12:07–12:10 burst was mixed: six re-times of today plus one plan-write for tomorrow.
   ⚠️ **The plan-burst does NOT sit inside `INBOX Review + Next Day Planning`** — falsified 2026-09-28(H), replicated 9/29 (seven bursts, none inside an anchor). **Search the whole day.**
   Also: **sort by start and subtract pairwise overlap before summing logged minutes, and report the overlap.** Trust a tidy log's sequence, not its durations.

4. **A block missing from today may have migrated in EITHER direction — match on event id, never on title or absence** (2026-09-23(G), 2026-09-24(G), reinforced 2026-09-29(I)). On 9/29 the "missing" `ResFrac | New Update/Agenda Doc` had moved **backwards onto 9/28**, and was found only by a targeted `fullText` query on the prior day. ⚠️ **Use the FULL event id**: a truncated id returns *"could not be found or has been deleted"* — indistinguishable from a real deletion.

5. **A scored block's calendar position is mutable after the run that scored it** (2026-09-25(D)). **Per-block minutes are provisional; anchor durable measurements to send timestamps, which do not move.** A prior measurement can lose its supporting event — or, as on 9/29, **gain one**: re-score it and say so rather than defending or deleting the rule it supported.

6. **Client work product is structurally invisible, so a production block's output can never be observed** (2026-09-28(K)). The Google Drive connector authenticates as `michael.p.christopher@gmail.com`, **not** the Attivo Workspace. Full-day sweeps on 9/28 and 9/29 returned only the agent's own run docs and Michael's personal files. **Record production output as unobservable, exactly as Suralink, Rippling, Ramp and the portal layer are. Never score a production block as having produced nothing.**

7. **⚠️ NEW — the umbrella block: a late-day extension can swallow other blocks, and its face duration double-counts them** (2026-09-29). `Mixmax | Pricing Plan - Excel Model` was extended at 17:33:01 to 15:30–18:00 — **150 face minutes** — and overlaps **90 minutes** of other logged blocks (`DeepScribe | Monthly Close Prep` 15, `Kestrel | DE Tax Review` 15, `INBOX Review` 30, `Mixmax | Cash Flow Review` 30). **Its exclusive minutes are 60, exactly its nominal planned size.** Taking the face duration would have scored it at 250% and moved pooled survival by nine points on one block. **When an extended block contains other named blocks, its EXCLUSIVE minutes are the honest figure** — error 3's overlap rule applied to the block being scored rather than to its neighbours.

---

*Lineage: seeded 2026-09-21 from the ACA v4 specification §6 and §8, cross-checked against the `[ACA]` corpus in [[Open Brain]]. Measurements 2026-09-22 to 2026-09-29 from calendar `created`/`updated` stamps diffed against each day's 7:30 AM snapshot and reconciled against Gmail sent, Slack read by channel id, and Drive. Asana has been unavailable on all fourteen runs, so §1, §2, §5 and §6 remain unmeasured; the EOD Planner has never run, so no agent-authored agenda has ever been scored.*

**Revisions** (last ten)

- 2026-09-21 — created, seeded with v4 priors. No measurements.
- 2026-09-22 — first measured values. §3 populated (n=1) and minutes-weighted columns added. §4 first row. New §7. Third instrument error added.
- 2026-09-23 — second measured day. `verb_class` replaces named/generic as §3's headline split. New §0. Containers excluded from the denominator. 70% cap superseded by 46.2%. §5 gains the EOD roll-burst finding. §6 gains the first scoreable sizing error. §7 narrowed; fourth instrument error added.
- 2026-09-24 — third measured day. Coordination replicates at 43.2%; the title split flips a third time. Pooled 46.2% → 42.2%. §6's thread-velocity rule promoted to n=3. §5 puts `Client/Double Review` at the threshold. §7 gains discharge-by-meeting and the soft-time-overflow rule. Instrument error 3 split into log- and plan-bursts; error 4 widened.
- 2026-09-25 — fourth measured day, and the first on which a prior measurement was withdrawn. Pooled 42.2% → 38.3%. The 140% production row deleted and replaced by *never propose production*. §3 gains the bimodal-survival warning; scheduler rule 2 demoted. §1 overrun 117% → 121.7%. §5: `Client/Double Review` deleted at its fourth placement. §6 restated as newest-live-thread, n=4. Instrument error 1 rewritten around `updated` vs `end`; new error 5.
- 2026-09-28 — fifth measured day, and the first on which the model's strongest claim was falsified. Pooled 38.3% → 43.4%. *"Production is never pre-planned"* narrowed to *"never the evening before"*; **the rule *never propose production* DELETED**. The title axis promoted to co-equal with `verb_class`. §3 bimodality at n=2 / 9 blocks. §5 roll-timing softened. §6 newest-live-thread narrowed to client and topic. §7 gains three disposal modes. Instrument error 3's plan-burst claim falsified; new error 6.
- **2026-09-29 — sixth measured day. The best day on both axes (71.4%, 5 emails + 1 Slack) and the day the title axis broke.** Pooled **43.4% → 49.5%**, band widened to 16.7–71.4%; coordination 44.0% → **49.4%**. **9/28 amended upward to 58.3%** after `ResFrac | New Update/Agenda Doc` resolved by retro-filing. **The title axis DEMOTED from co-equal to CONTAMINATED** — it inverted (generic 75%, named 66.7%) and Michael was caught renaming a generic block to a named one seven minutes after it closed; **titles are now scored at the morning snapshot only, and scheduler rule 3 is SUSPENDED**. *"Production never pre-planned the evening before"* **deleted** — falsified within four hours of being written. **Scheduler rule 2 PROMOTED to supported at n=1** (a prep block followed its venue to the next day). §1's 121.7% overrun collapsed to **100.6%** and *"treat a booking as a floor"* **withdrawn**. §3 bimodality narrowed to admit the decomposition exception (15 blocks, one partial). §4's five-context cap reached for the first time, on the best day — **refuted, not merely un-approached**. §5: `Scanner | Updates` frozen at 2 rolls having run; `Monthly Close Prep` to 2 and no longer opaque. §6's *newest live thread* **replaced by answerability**, and channel silence reclassified as medium preference. §7 gains *rolled with its venue*, *decomposed in arrears*, and the replication of retro-filing onto a prior day. Instrument error 1 gains the in-flight row and the snapshot anchor; error 2 at n=5; **new error 7, the umbrella block**.
