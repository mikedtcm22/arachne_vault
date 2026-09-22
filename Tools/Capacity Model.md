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

> ⚠️ **EVERYTHING BELOW IS AN ASSUMPTION, NOT A MEASUREMENT.** Seeded 2026-09-21 from the priors in the v4 spec §6. Every number here is a guess drawn from the lesson corpus, recorded so it can be falsified. Expect the first two weeks of agendas to be mediocre and the `[MC]` notes to do most of the work. Nothing here should be trusted until its "measured" column is populated.

**What this note is.** Only the congealed structure — current parameter values and the rules they imply. It is integrated, maintained and small. It is **not a log**: nightly observations are atomic and stay in [[Open Brain]] as `[ACA-PLAN]` thoughts, per the vault's own promotion rule.

**Update protocol.** `upsert_note` overwrites in full, so the evening run must `read_note` first, merge, and write back. Test **S8** asserts the read preceded the write. Revision line at the foot, capped at the last ten entries.

---

## 1. What each number actually means

| Tag | Assumed planning minutes | Measured median | n | Drift |
|---|---|---|---|---|
| `1` | 30 | — | 0 | — |
| `2` | 90 | — | 0 | — |
| `3` | 165 | — | 0 | — |
| `4` | not schedulable | n/a | n/a | decompose marker, not a size |

`3` is the shakiest of the three: the underlying convention is "~2.5–3 hrs" and 165 simply splits it. Expect this one to move first.

## 2. What each letter actually means

Completion rate for `H` / `M` / `L` by time-of-day window. This is the "when am I primed for what" model, and it should end up empirical rather than asserted.

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

| Client | Planned blocks | Ran as planned | Shifted | Rolled | Dropped | Survival |
|---|---|---|---|---|---|---|
| — | 0 | 0 | 0 | 0 | 0 | — |

**Expect the 70% cap to prove optimistic.** The scheduler places work into self-scheduled focus blocks, which the lesson corpus repeatedly identifies as the schedule's shock absorber — the first thing sacrificed when same-day work arrives, and moved *later* rather than earlier:

- **2026-08-13(A)** — "a calendar block for unscheduled analysis work is the schedule's shock absorber, not a commitment."
- **2026-08-17(E)** — one block placed **seven times in five business days**, never run.
- **2026-08-28(A)** — self-scheduled blocks are deferrable and fixed commitments are not, so a day made mostly of focus blocks can be moved wholesale, and on 8/28 it was.
- **2026-06-09(B)**, **2026-06-11(A)** — a dedicated block is a weak signal even against a partner-level escalation.

**The countervailing finding, and the one to instrument first: 2026-09-02(A)** — a block *naming a personally-authored deliverable* produced same-day output **7 times out of 7**, and explicitly bounds 2026-08-28(A) to days whose blocks are **generic**. So the split to measure is not "did the block survive" but **"did a block with a named output survive, versus one with a generic title."** If that split is as sharp as 09-02(A) suggests, it is worth more than every other parameter in this note.

**Secondary split** (**2026-09-17(G)**): the block's verb. *Finalize / build / update* are production work whose product is a file — the day goes quiet. *Prep / admin / review / requests / close* are coordination work whose product **is** correspondence. Recorded per task as `verb_class:`.

| Title type | Planned | Survived | Rate |
|---|---|---|---|
| Names a deliverable | 0 | 0 | — |
| Generic / topic only | 0 | 0 | — |
| `verb_class: production` | 0 | 0 | — |
| `verb_class: coordination` | 0 | 0 | — |

## 4. Switching cost

Client-context count per day against completion rate. Seed rule: **maximum five distinct client contexts per day**, batched contiguously.

| Contexts in day | Days observed | Mean completion |
|---|---|---|
| — | 0 | — |

## 5. Roll history

Which Workstreams chronically fail to survive — diagnostic of **scoping**, not of discipline. A task at three rolls stops being silently re-planned and becomes a flag.

| Workstream | Rolls | Status |
|---|---|---|
| Scanner \| Close: Aug Revenue | 5 (as of 2026-09-15) | would have flagged on the first run |

## 6. Tag-prediction accuracy

How often the agent's proposed tag pair survives Michael's review. A second prediction stream running alongside plan adherence, costing nothing extra to collect.

| | Proposed | Unchanged by MC | Corrected | Accuracy |
|---|---|---|---|---|
| Number | 0 | 0 | 0 | — |
| Letter | 0 | 0 | 0 | — |

⚠️ The connector cannot write tags, so every agent proposal lives in the fenced `--- agent ---` block as `tags:` + `tag_source: agent`, and Michael's correction is observed by comparing the native tag against that field.

---

## Known instrument errors

Two measurement hazards that would otherwise corrupt this model silently.

1. **Retroactive blocks are work logs, not plans.** Michael creates named calendar blocks *after* doing the work — Lesson 2026-09-04(C) found one created eight minutes after the artifact it names was emailed, and Lesson 2026-09-21(E) found a 1:30–2:00 PM block created at 5:20 PM. So "calendar-as-worked" is partly post-hoc reconstruction. The evening run must split blocks created *before* their start (a plan, scoreable for adherence) from those created *after* their end (a log, evidence that work happened but not that it was planned). Scoring the second kind as plan adherence measures nothing.

2. **A retro block dates the work, not the output.** Per 2026-09-21(E), the correspondence that came out of a retro block usually lands *later* than the block's own window — 3h45m later in the observed case. Searching the same window returns a false negative.

---

*Lineage: seeded 2026-09-21 from the priors in the ACA v4 specification §6 and §8, cross-checked against the `[ACA]` lesson corpus in [[Open Brain]]. Every value is an assumption pending measurement; the survival-rate and named-vs-generic splits in §3 are the first to instrument.*

**Revisions** (last ten)

- 2026-09-21 — created, seeded with v4 priors. No measurements yet.
