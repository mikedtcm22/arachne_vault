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

> ⚠️ **PARTLY MEASURED.** Seeded 2026-09-21 from the priors in the v4 spec §6. **Measurements from five days — 2026-09-22, 23, 24, 25 and 28, 20 scoreable blocks** — are marked below; everything unmarked is still a guess recorded so it can be falsified. **2026-09-28 reversed the model's strongest claim at n=5, which is the clearest evidence yet that four days is enough to find a split and not enough to trust one.**

**What this note is.** Only the congealed structure — current parameter values and the rules they imply. It is integrated, maintained and small. It is **not a log**: nightly observations are atomic and stay in [[Open Brain]] as `[ACA-PLAN]` thoughts.

**Update protocol.** `upsert_note` overwrites in full, so the evening run must `read_note` first, merge, and write back. Test **S8** asserts the read preceded the write. Revision line at the foot, capped at the last ten entries. **As a measured value replaces a prior, delete the prior** — this note should shrink as it learns.

---

## 0. The two axes — read them together or not at all

**Minutes-survival alone has now ranked the measured days wrongly in four different directions.**

| Day | Minutes survival | Flags cleared | Outbound artifacts | Verdict |
|---|---|---|---|---|
| 2026-09-22 | 68.8% | 0 of 8 | — | highest survival, lowest output |
| 2026-09-23 | 30.4% | **2 of 8**, both top-ranked | 2 emails | better than 9/22 |
| 2026-09-24 | 16.7% | 2 of 16, one red | **2 emails + 5 Slack + 1 Doc** | **highest output measured** |
| 2026-09-25 | 26.7% | **3 of 12** (Carrie, Pilot books, Kestrel) | 1 email + 1 Slack DM + 255 min new commitment | mid on both |
| 2026-09-28 | **56.5%** | 2 of 14 (Jennifer ×2) | **1 email + 0 Slack**, 330 min on one client thread | high survival, thin output, **two red deadlines untouched for a 7th day** |

**A plan displaced by more urgent work of the same client is a successful displacement and must not train the scheduler toward smaller plans.** A day can be almost entirely unplanned and still be the most productive one measured. **Always report clearance and artifacts alongside survival.**

⚠️ **And the converse, new on 9/28: a high-survival day is not a good day either.** 56.5% survival was the second-best figure in the corpus, on a day whose only outbound artifact was one email, whose two generic-titled blocks both rolled, and on which the 9/30-dated audit backup took zero minutes for the seventh consecutive day.

## 1. What each number actually means

| Tag | Assumed planning minutes | Measured median | n | Drift |
|---|---|---|---|---|
| `1` | 30 | — | 0 | — |
| `2` | 90 | — | 0 | — |
| `3` | 165 | — | 0 | — |
| `4` | not schedulable | n/a | n/a | decompose marker, not a size |

Tags are readable only through Asana, unavailable on all **twelve** runs to date. **Nothing in §1 can move until the connector is authorised.**

**Adjacent measurement that does not need tags** (n = 3): **externally-organised meetings run 121.7% of their booked minutes** — Kestrel 40 against 30, DeepScribe×Tabs 61 against 60, Attivo×Mixmax 45 against 30. Pooled 146 of 120. **Treat a counterparty's booking as a floor, not a box — and expect the overrun to cascade.** On 9/25 a 15-minute extension pushed two downstream blocks 1h45m later.

⚠️ *Not* revised on 9/28. The 12:15 Kestrel sync's Fireflies recap arrived at 12:28:59, implying ~14 of 15 booked minutes (93%) — the first sub-100% observation. **Recap-email latency has never been calibrated**, so the recap timestamp is not a meeting-end timestamp and this observation is too weak to move a three-point figure. Recorded, not merged.

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
| 2026-09-28 | 4 resolved (+1 pending) | 2 | 345 | 195 | **56.5%** |
| **Pooled** | **20** | **9** | **1245** | **540** | **43.4%** |

**43% is the working figure**, and it has now moved 46.2 → 42.2 → 38.3 → **43.4** across four revisions. It is not converging. **The honest statement is "well under half, banded 17–69%." Do not hard-code 43 any more than 38 or 70.**

⚠️ **Survival is bimodal per block, not a uniform haircut — now n=2 days, 9 blocks, ZERO intermediate outcomes** (2026-09-25(F), 2026-09-28(F)). 9/25: 100%, 100%, 0%, 0%. 9/28: 125%, 100%, 0%, 0%. **Size a block at its nominal length and expect it to run whole or vanish whole.** Shrinking every block to ~43% of nominal would produce a plan in which nothing is the right size. The prediction target is **which** blocks vanish, not by how much each shrinks — and §3's title split now answers that.

### The two splits, and what 2026-09-28 did to their ranking

| `verb_class` | Blocks | Planned min | Logged min | **Rate** | Replicates? |
|---|---|---|---|---|---|
| **coordination** | 18 | 1125 | 495 | **44.0%** | **yes, n=5 days** — 50%, 30%, 44%, 27%, 56.5% |
| **production, pre-planned** | 1 | 180 | 180 | **100%** | n=1 — first ever observed, 2026-09-28 |

| Title type | Day-rates | Favours named? |
|---|---|---|
| Names a deliverable | 167%, 30%, 100%, 100%, **118%** | **4 of 5 days** |
| Generic / topic only | 50%, 80%, 0%, 15.4%, **0%** | — |

**⚠️ 2026-09-28 IS THE FIRST DAY THAT COULD SEPARATE THE TWO AXES, AND IT SEPARATED THEM IN FAVOUR OF THE TITLE** (2026-09-28(D)). All five blocks in that morning's snapshot were coordination verbs, so `verb_class` was constant and could not discriminate at all. The title axis discriminated perfectly: named-deliverable blocks kept **195 of 165 planned minutes (118%)**; generic ones kept **0 of 180 (0%)** — `Scanner | Updates` and the opaque `Monthly Close Prep (...)`, both rolled to 9/29.

This runs **opposite to 2026-09-23(A)**, which separated the axes in favour of `verb_class`. Two clean separations, two different winners. **Promote the title axis to co-equal with `verb_class`; neither is the headline split.** Lesson 2026-09-02(A)'s 7-for-7 named-deliverable result is reinforced rather than merely un-refuted.

### ⚠️ Production IS pre-planned — just never the evening before

**This section previously read "never pre-planned — the strongest finding in the model." 2026-09-28 falsified that form of the claim and it has been rewritten** (2026-09-28(A)).

`Mixmax | Pricing Plan - Excel Model` was created at **10:42 CT for a 13:45 start** — 3 h 03 m ahead of its own window, so it passes the plan test — ran, was **extended in flight** at 16:09 from 15:45 to 16:45, and logged **180 of 180 minutes**. It is client-analysis production, not internal work. It is the first such block in the corpus.

**The surviving, narrower claim:** across five days Michael has pre-planned zero client-production blocks **in the previous evening's EOD burst**. What he does is plan production **same-day, hours ahead** — and when he does, **it wins**: both coordination blocks it collided with were rolled to 9/29 rather than the production block being cut.

**SCHEDULER RULE — REPLACED.** The old rule was *never propose production*. It produced the wrong answer on its first test: the 9/28 morning run, obeying it, proposed 45 minutes of `1L` coordination into 13:30–14:15, and Michael filled that exact window with 180 minutes of production. Right window, wrong verb class — the mirror image of 9/25's error. **The new rule is: propose the window, name the artifact, and do not encode verb class as a scheduler rule at n=5.** The agent has predicted the right window repeatedly and the right content never.

**Scheduler rules from this section:**
1. Size a block at **nominal**, and expect it to run or vanish (not to shrink).
2. **Anchor it to the venue that forces it.** ⚠️ Still **weakly supported** (2026-09-25(D)) — its single supporting observation was re-filed onto another day. Not falsified; no live evidence.
3. **Prefer a title that names its artifact.** This is now the best-supported single lever in the model: 4 of 5 days, and the only day that isolated it gave 118% against 0%.

## 4. Switching cost

Seed rule: **maximum five distinct client contexts per day**, batched contiguously.

| Contexts in day | Days | Completion (minutes basis) |
|---|---|---|
| 4 (+1 internal) | 1 | 79% |
| 3 (+1 internal) | 1 | 27% |
| 2 (+1 internal) | 3 | 30%, 17%, **56.5%** |

**Five days, no relationship — and 9/28 makes the null result sharper**: the same context count (2 + 1 internal) has now produced both the worst and the second-best day in the corpus. Contiguity has been violated on all five with no measurable cost. **Context count is not predictive of anything, and the seed limit of five has never been approached.**

## 5. Roll history

A task at three rolls stops being silently re-planned and becomes a flag (engine rule 9).

⚠️ `rolls:` has never been readable or writable — it is an Asana fenced-block field. **0 increments across twelve runs, against 7 directly observed rolls.**

| Block / workstream | Observed rolls | Status |
|---|---|---|
| `Client/Double Review (...)` (`7u71d6h0k1grovgju1jgeao76c`) | **3, final** | **DELETED 2026-09-25** at its fourth placement — `get_event` returns *deleted*. **Rule 9's "cut it" is a real disposal mode**, reached by Michael independently |
| `Scanner \| Updates` (`5k3hffa1uap4kj2p0h3qfho3u9`) | **2** (9/25→9/28, 9/28→9/29) | **One below the flag threshold.** Evacuated by Mixmax on both. Re-placed 9/29 09:00–10:30 |
| `Monthly Close Prep (...)` (`07b3d937if5c2v2dljba475qvf`) | **1** (9/28→9/29) | Re-placed 9/29 13:15–14:45. Title still opaque; may or may not be `Client/Double Review`'s successor |
| `Scanner \| Close: Aug Revenue` | 5 (as of 2026-09-15) | past threshold; unverifiable until the connector returns |
| Mixmax audit backup `C-20260917-05` · DeepScribe/Tabs `C-20260910-05` | **n/a — never placed** | **Worse than rolled.** Seven days flagged, zero blocks ever created. A never-placed item cannot roll, so the roll instrument is blind to the model's two most overdue items |

**Rolls are written when the displacing work takes the window — usually, but NOT always, in the EOD burst** (revised 2026-09-28(G); was "at EOD" at n=3). On 9/28 both rolls were written mid-afternoon, in flight: `Monthly Close Prep` at 15:07 CT and `Scanner | Updates` at 16:10 CT, each at the moment the overrunning Excel Model block took its slot, and both **before** `INBOX Review`.

**Consequence for the 4:15 PM EOD Planner:** tomorrow's free windows are still provisional, but on a day with a mid-afternoon collision **some rolls are already visible at 4:15 PM**. Read the calendar; do not assume they cannot be there.

## 6. Tag-prediction accuracy

| | Proposed | Unchanged by MC | Corrected | Accuracy |
|---|---|---|---|---|
| Number | 4 | 0 | 0 | **unmeasurable** |
| Letter | 4 | 0 | 0 | **unmeasurable** |

⚠️ This stream cannot open until the EOD Planner runs once and Michael sets a real tag against an agent proposal. **No agent proposal has ever been taken up**, and the EOD Planner has still never fired — not on its 2026-09-25 go-live day, not since.

**What is scoreable is the agent's own target selection, and it is the bigger error by far — six consecutive misses:**

- 9/23: `3H` (165 min) into a 120-minute window — violated G1 before Michael saw it; the deliverable took ~30 min.
- 9/24: `2H` into a 105-minute window (G1-conforming) — not taken; wrong deliverable.
- 9/25: `2M` into 90 of a 120-minute hold — not taken. Right client, right window, **wrong verb class**.
- 9/28: `1L` coordination into the day's only free window — **the window was right, and Michael filled it at 13:45.** He filled it with 180 minutes of production. **Wrong verb class again, with the sign inverted.**

**THE RULE, AT n=5: TARGET THE NEWEST LIVE THREAD — not the nearest deadline, not an older live thread.** It held again on 9/28: Jason Tatum's 9/25 12:04 Gen 2 ask took **330 of the day's 375 logged self-scheduled minutes**.

⚠️ **But the rule predicts the CLIENT and the TOPIC, not whether the output is a message or a file** (2026-09-28(C)). Michael spent five hours inside Jason's thread and **posted nothing to `#attivo-mixmax` all day**; the ask stands unanswered at 2 business days. Use thread recency to choose the client and the window. Never infer from it that the block's output will be correspondence, and never let "the thread got minutes" clear a flag that says "the counterparty is still owed a reply."

**A displacement proposal is already stale if a counterparty posted after it was written.**

**And name the counterparty who must *receive* the artifact, not the one who produced it.**

⚠️ **A parameter written here but not read into the proposal is not part of the engine** (2026-09-24(K)). **Every displacement proposal must name which rule of this note it applied.**

## 7. Counterparty volatility and refill

| Disposal mode | 9/22 | 9/23 | 9/24 | 9/25 | 9/28 | Note |
|---|---|---|---|---|---|---|
| Cancelled by counterparty | 1 | 1 | 1 | 0 | 0 | |
| Moved by counterparty | 1 | 0 | 0 | 0 | 0 | |
| Deleted by Michael (containers) | 2 | 2 | 3 | 1 | 0 | |
| Moved within the day by Michael | — | — | 3 | 4 | **6** | highest measured |
| Evacuated by a competing client | 1 | 1 | 0 | 1 | 0 | |
| **Evacuated by the SAME client's other work** | — | — | — | — | **2** | **new** — both rolls caused by one Mixmax production block |
| Rolled forward by Michael | 0 | 2 | 1 | 1 | **2** | on 9/28 written mid-afternoon, not at EOD |
| Retro-filed onto a prior day | 0 | 1 | 0 | 0 | 0 | **does not replicate** — 1 for 4 |
| Retro-filed onto a LATER day | — | — | — | 1 | 0 | |
| Disposed by scheduling a meeting | 0 | 0 | 1 | 0 | **1** | 9/28: the PaulexBio NIH question |
| Deleted outright at the roll threshold | 0 | 0 | 0 | 1 | 0 | see §5 |
| **Deferred past 17:00 within the day** | — | — | — | — | **2** | **new** — `INBOX Review` → 18:30, `ResFrac` → 19:00 |

⚠️ **Block disposal is not primarily counterparty-driven.** Pooled: **5 of 36.** On 9/28 it was **entirely** self-inflicted — one client's production block displaced that same client's coordination block and an internal one.

**Discharge-by-meeting** (2026-09-24(F)), **narrowed 2026-09-25(L):** when a flagged item acquires a dated venue **with the counterparty in it**, it stops being overdue. **A solo prep block does not discharge anything.** Confirmed twice more on 9/28: the Kestrel bi-weekly ran at 12:15 and closed Kestrel; the PaulexBio NIH scope question acquired `Paulexbio <> Attivo Sync` (9/29 11:00, Justin Vogel in the room) within 4 h 21 m of arriving.

⚠️ **ARRIVAL RECENCY BEATS DEADLINE PROXIMITY EVEN WHEN THE ARRIVING ITEM HAS NO DATE AND NO OWNER** — now n=2 (2026-09-25, 2026-09-28(J)). Miguel Sanjuan's undated grant-scope question got a 30-minute research block and a next-day venue inside four and a half hours, on the seventh consecutive day the 9/30-dated Mixmax audit backup got zero minutes. **This is the model's most reliable predictor of where a day's minutes go, and the scheduler cannot fix it — only the flag list can.**

**Refill: freed time is filled by re-pointing a block that already exists somewhere on the same day.** Latency 52–59 min at n=3. Not re-measured 9/25 or 9/28 — on 9/28 nothing was freed; the day was over-filled rather than vacated.

⚠️ **Size a capture block to the vacancy plus the soft time abutting it** (2026-09-24(E)). Declined, tentative and externally-organised blocks are not occupied time.

⚠️ **Focus blocks move in both directions**, and on 9/28 they moved **later within the day past 5:00 PM** rather than to another date — a third direction. The corpus rule that focus blocks move only later is narrowed to client analysis displaced by incoming client work.

---

## Known instrument errors

Six measurement hazards that would otherwise corrupt this model silently.

1. **Retroactive blocks are work logs, not plans — the test is `updated` vs `end`, NOT `created` vs `start`** (revised 2026-09-25(C)). **An event whose last `updated` stamp post-dates its own `end` is retroactively placed and cannot be scored for plan adherence, however old its `created`.** On 9/23 five of eleven executed blocks were logs; on 9/24, four of seven; on 9/25, four of ten; on 9/28, one of seven (`Paulex | NIH Grant Research`, created 15:43 onto a 13:45–14:15 window). **A block created *during* its own window is in-flight — treat it as a log, and say so.** ⚠️ **The test must be applied to the block's position AT THE MOMENT IT IS SCORED, not to its current stamp** — a block that ran and was then re-timed within the same day will fail the naive test although it was a genuine plan (see error 5).

2. **A retro block dates the work, not the output.** The correspondence lands *later* than the block's own window — 27 minutes later on 9/25. A same-window search returns a false negative.

3. **Classify a burst by the dates it writes — per block, because a burst can be MIXED** (revised 2026-09-25(I)). A **log-burst** re-times *today* and follows an outbound message (latencies 13 s to 3 m 24 s across 6 bursts). A **plan-burst** writes *future* dates.
   ⚠️ **The plan-burst does NOT reliably sit inside `INBOX Review + Next Day Planning`** — falsified 2026-09-28(H) after holding at n=3. On 9/28 Michael re-timed his day in **five** bursts (12:48, 15:07, 15:42–15:48, 16:09–16:10, 16:51–16:52 CT), **none** inside the anchor, and then moved the anchor itself from 16:30 to **18:30–19:00**. The anchor is where planning lands on a quiet afternoon; on a day with a mid-afternoon collision, planning is distributed across the collision points. **Search the whole day, not the anchor.**
   Also: sort by start and subtract pairwise overlap before summing logged minutes, and report the overlap. **Trust a tidy log's sequence, not its durations.**

4. **A block missing from today may have migrated in either direction — match on event id, never on title or absence** (2026-09-23(G), 2026-09-24(G)). On 9/28 both "missing" blocks had **rolled to 9/29**, not been deleted. ⚠️ **Use the FULL event id**: a truncated id (`07b3d937` for `07b3d937if5c2v2dljba475qvf`) returns *"could not be found or has been deleted"* — indistinguishable from a real deletion, and a false positive for the disposal table.

5. **A scored block's calendar position is mutable after the run that scored it** (2026-09-25(D)). **Per-block minutes are provisional; anchor durable measurements to send timestamps and Doc `createdTime`s, which do not move.** When a prior day's measurement loses its supporting event, demote the rule it supported rather than deleting or defending it.

6. **⚠️ NEW — client work product is structurally invisible, so a production block's output can never be observed** (2026-09-28(K)). The Google Drive connector authenticates as `michael.p.christopher@gmail.com`, **not** the Attivo Workspace account: a full-day `modifiedTime` sweep on 9/28 returned only the agent's own two run docs and two personal files, and Jason's shared Gen 2 doc returns *"Requested entity was not found."* `Mixmax | Pricing Plan - Excel Model` logged 180 minutes and produced no observable artifact — **an instrument limit, not a null result.** Record production output as **unobservable**, exactly as Suralink, Rippling, Ramp and the portal layer already are. **Never score a production block as having produced nothing**, and never let the absence of an artifact count as evidence against a production measurement.

---

*Lineage: seeded 2026-09-21 from the ACA v4 specification §6 and §8, cross-checked against the `[ACA]` corpus in [[Open Brain]]. Measurements 2026-09-22 to 2026-09-28 from calendar `created`/`updated` stamps diffed against each day's 7:30 AM and 12:30 PM snapshots and reconciled against Gmail sent, Slack read by channel id, and Drive. Asana has been unavailable on all twelve runs, so §1, §2, §5 and §6 remain unmeasured; the EOD Planner has never run, so no agent-authored agenda has ever been scored.*

**Revisions** (last ten)

- 2026-09-21 — created, seeded with v4 priors. No measurements.
- 2026-09-22 — first measured values. §3 populated (n=1) and minutes-weighted columns added. §4 first row. New §7. Third instrument error added.
- 2026-09-23 — second measured day. `verb_class` replaces named/generic as §3's headline split. New §0. Containers excluded from the denominator. 70% cap superseded by 46.2%. §5 gains the EOD roll-burst finding. §6 gains the first scoreable sizing error. §7 narrowed; fourth instrument error added.
- 2026-09-24 — third measured day. Coordination replicates at 43.2%; the title split flips a third time. Pooled 46.2% → 42.2%. §6's thread-velocity rule promoted to n=3. New §6 warning: a parameter read but not applied is not part of the engine. §5 puts `Client/Double Review` at the threshold. §7 gains discharge-by-meeting, tightens refill to 52–59 min, adds the soft-time-overflow rule. Instrument error 3 split into log- and plan-bursts; error 4 widened.
- 2026-09-25 — fourth measured day, and the first on which a prior measurement was withdrawn. Pooled survival 42.2% → 38.3%; coordination 43.2% → 38.5%. The 140% production row deleted and replaced by "production is pre-planned on 0 of 4 days" plus the rule *never propose production*. §3 gains the bimodal-survival warning; scheduler rule 2 demoted. §1 externally-organised overrun 117% → 121.7%. §5: `Client/Double Review` deleted at its fourth placement. §6 restated as newest-live-thread, n=4. Instrument error 1 rewritten around `updated` vs `end`; error 3 gains the mixed-burst case; new error 5.
- 2026-09-28 — **fifth measured day, and the first on which the model's strongest claim was falsified.** Pooled survival 38.3% → **43.4%**; coordination 38.5% → **44.0%** (band 27–57%). **"Production is never pre-planned" narrowed to "never pre-planned the evening before" after the first genuinely pre-planned client-production block (180 of 180 min), and the rule *never propose production* DELETED** — it produced the wrong answer on its first test, the exact mirror of 9/25's error. **The title axis promoted to co-equal with `verb_class`** after the first day that could isolate it (named 118%, generic 0%, verb_class constant). §3 bimodality upgraded to n=2 / 9 blocks / 0 intermediate outcomes. §5 roll-timing softened from "at EOD" to "when the displacing work takes the window." §6 newest-live-thread at n=5, narrowed to predict client and topic but not output form; sixth consecutive agent proposal untaken. §7 gains three disposal modes (same-client evacuation, deferral past 17:00, meeting-disposal) and the undeadlined-ask finding at n=2. **Instrument error 3's plan-burst-in-`INBOX Review` claim falsified; error 4 gains the truncated-event-id false positive; new error 6: client work product is invisible to the Drive connector.**
