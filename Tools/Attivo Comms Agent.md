---
title: Attivo Comms Agent
type: tool
pillar: Arachne Intelligence
status: active
created: '2026-06-08'
tags:
  - tool
  - ai
  - email
  - aca
  - planning
---
# Attivo Comms Agent

Up: [[Arachne Intelligence]]

**ACA** — an AI agent that learns my email-handling and delegation patterns to cut the morning inbox slog. A predict / evaluate learning loop over consulting email; it knows, for instance, which client threads I lead versus where I'm only CC'd for visibility.

An Augmentation tool: it serves the consulting work, yet it's something I *built to make myself better* — distinct from the consulting itself. Posts in the Arachne Finance Slack workspace.

## v4 — from drafting to task & time management

**As of 2026-09-21 the product changed.** v3 produced reply drafts wrapped in a prediction document. v4 produces **a next-day agenda and a live inventory of everything on my plate**, with Asana as the system of record. The drafting layer (Gate 1 triggers A–I, the draft ledger, the two draft sections) retires; the comms sweep, the evening evaluation and the `[MC]` inline-notes loop are retained and **re-pointed at plan adherence** instead of reply accuracy.

The learning loop keeps its shape and gains a cleaner signal: **the agenda is the falsifiable prediction.** v3 predicted what I would do and scored itself against my Sent folder. v4 proposes what I *should* do and scores itself against my calendar-as-worked and my Asana completions — direct evidence rather than inference.

Four scheduled runs replace the three: Morning Delta (7:30), Midday Re-plan (12:30), EOD Planner (4:15, the centrepiece), Evening Evaluation (7:30).

The compounding artifact is [[Capacity Model]] — how much work actually survives a day, and where in the day each kind survives. It is seeded entirely with assumptions and is the thing that has to be *measured* rather than reasoned about.

**The uncomfortable part of the design, recorded honestly:** the scheduler places work into self-scheduled focus blocks, and four months of this loop's own lessons say those are the schedule's shock absorber — the first thing sacrificed, and moved later rather than earlier. The countervailing finding is 2026-09-02(A): a block *naming a personally-authored deliverable* went 7-for-7, while generic blocks evaporate. So the whole design leans on naming the output rather than the topic, and the first thing the Capacity Model should establish is whether that split is real.

## Purpose & direction
Two goals, and the second is the larger one:
1. **Mimicry** — enumerate how I actually work across email so AI can eventually draft responses the way I would myself.
2. **Improvement** — make me a *better* communicator with stakeholders. Every observation in the learning loop should also pass through the lens of *"how could this habit be improved against an ideal communication workflow?"* Phase 2 and beyond aim at an improved overall email cadence — powered by AI, not merely imitated by it.

## Learned behavior model
The generalized prediction rules the eval loop has surfaced (individual dated lessons stay atomic in [[Open Brain]]). Read each descriptively *and* against the improvement lens above — every rule is also a candidate habit to refine:
- **Task-type governs slip, not client gravity.** Quick replies / clarifications / re-sends clear same-day regardless of whether that client has a calendar block; *build-a-deliverable* items slip until they have a block titled for that deliverable or an external hard deadline.
- **Forcing functions force same-day sends** even without a block: an imminent external/contractual deadline, a fresh nudge with a near-term trigger, or a commitment made in a recent MOR/board review. A same-day meeting on a deliverable forces a morning pre-read, not a substitute for the email.
- **Deferred-expectation exception.** Once I've verbally deferred ("connect next week") and the deliverable has no near-term deadline, the follow-up clears this-week, not today — regardless of nudge count or a dedicated block.
- **Meeting-saturation discount.** On 3+ meetings plus dense focus blocks, same-day confidence for directly-addressed CEO asks drops (HIGH→~MEDIUM), the defer fork widens, and any same-day acknowledgment lands at the EOD (~5 PM) anchor.
- **Roster-ownership deferral.** Roster ownership (not by-name tagging) governs replies; for an off-roster item a teammate already owns, expect no observable email even with a self-scheduled block + a partner escalation.
- **Re-litigation deferral.** A client re-asking an already-settled question doesn't inherit same-day urgency; I defer or hold the line firmly (esp. compliance/tax) rather than softening to "your call" — unless an imminent external deadline forces it.
- **Open-period reporting.** For as-of / period-end deliverables whose period hasn't closed, my same-day reply is a scope-and-timing acknowledgment proposing a post-close working session, not an execution commitment.
- **Weekday holiday ≠ weekend.** On a holiday/OOO, reactive threads stay no-response, but proactive/self-directed work tied to a named focus block still ships.
- **Enumeration rule.** A directly-addressed message from a named decision-maker with a concrete question or deadline keyword is always HIGH / respond-today and must be enumerated — never auto-filtered as noise. The morning scan should also surface recent live-meeting (MOR/board) commitments, not just open email threads.
- **Automated-digest immunity — and why it holds.** Platform task/payroll digests (e.g. Rippling) are FYI-only template noise, not tasks I own — even when they carry "[ACTION REQUIRED]," "overdue," or a stated same-day deadline. Predict no-response at HIGH confidence and never fork to forward-to-team on these, regardless of urgency language in the subject/body, unless I or a named teammate is the explicit responsible approver on that entity. The real driver is scope, not urgency: most of these are out-of-scope-of-engagement calls. If I'm not responding to or forwarding a Rippling item for a given client (e.g. DeepScribe payroll administration), it's because that function sits outside Attivo's engagement scope for that client altogether — I'm cc'd purely as an FYI, and no follow-up is expected. Read "confidence" on these predictions as a scope question first, not a calibration question.

## Scheduling behaviour model (v4)
A separate axis from the reply-prediction rules above: what the corpus says about how my *time* behaves. These are the inputs to [[Capacity Model]].
- **A named-deliverable block predicts output; a generic block predicts nothing.** 7-for-7 as of 2026-09-02(A). The generic "(AI/Team Mgmt & Admin Tasks)" hold carries **no** information about content and must be read as UNKNOWN, never as "no deliverable work."
- **The block's verb discriminates.** *Finalize / build / update* is production work whose product is a file — the day goes quiet. *Prep / admin / review / requests / close* is coordination work whose product **is** correspondence (2026-09-17(G)).
- **A self-scheduled block is reprioritizable slack**, not a commitment — it moves later, and on a light-meeting day the whole day can move wholesale (2026-08-13(A), 2026-08-28(A)).
- **I create blocks retroactively to log work already done** (2026-09-04(C), 2026-09-21(E)). A block created after its own end time is a work log, and the correspondence from it usually lands *later* than the block's window. This is a measurement hazard for any plan-adherence score.
- **Work scheduled after ~6 PM is a deferral to the next business day**, not a plan for tonight (2026-08-14(H)).

## Proactive-send patterns
The rules above are all reactive — predicting responses to inbound mail. This is a separate axis: predicting *unprompted* sends.
- **Proactive-build forcing function.** On days with a strategic-finance/FP&A focus block for a given client — especially Fridays — expect an unprompted, client-facing BUILD deliverable (a model, a pricing tool, even a prototype web asset) to ship same-day to that client's exec/GTM contacts, independent of any inbound trigger. Surface it as a candidate proactive send during the morning scan, rather than folding it into the day's no-response defaults.

## Open threads
- Track prediction accuracy / eval over time.
- Build the **improvement layer**: turn each learned habit into a suggested better-practice, working toward the Phase-2 AI-powered communication cadence.
- Decide how far to extend it beyond triage.
- **Measure the [[Capacity Model]] priors.** Everything in it is currently an assumption: 30/90/165 minutes, the 70% capacity cap, the 3-hour `H` budget, `H`-in-the-morning. The named-vs-generic survival split is the first to instrument.
- **Renew or drop the Asana Starter plan.** Upgraded to a 14-day trial 2026-09-21, expiring ~2026-10-05 — ten days after v4 goes live. `start_at`, dependencies, custom fields and task search all revert to `402` on expiry. The engine is built so nothing hard-depends on them, but the decision is live.

## Closed threads
- **Learning-loop reliability gap — RESOLVED 2026-09-21.** For 69 consecutive runs every session cloned a `main` that nothing was ever merged back into, so each run re-derived its base from a sibling branch and periodically reset to "first run." Root cause was correctly diagnosed 2026-08-04 and then observed 65 more times without being actioned, because the scheduled runs correctly refuse to self-authorise a merge and no one was running a build session to do it for them. Fixed by fast-forwarding `main` from `8bb5b56` to `4181dc8`: 22 files → 161, 25 lessons → 359, and the 2,637-line commitment register recovered from the evening lineage. Two corrections to the record while closing it: the corpus said "stale since 2026-05-29" for 69 consecutive entries, but `8bb5b56` is an **August 1** commit — `main` was stale by 51 days, not four months; and the defect was never a permissions problem, since three commits reached `main` directly on 2026-08-01 from build sessions.

*Lineage: distilled from the `[ACA] Lesson` cluster in Open Brain (6/10–6/23), via the 2026-06-24 dream; extended with the 6/24–6/30 cluster (automated-digest/scope rule, proactive-send axis, learning-loop reliability gap) via the 2026-07-01 dream; extended 2026-09-21 with the v4 task-and-time pivot, the scheduling behaviour model drawn from the 8/13–9/21 lesson cluster, and the closure of the persistence gap.*
