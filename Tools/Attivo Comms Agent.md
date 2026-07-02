---
created: '2026-06-08'
pillar: Arachne Intelligence
status: active
tags:
  - tool
  - ai
  - email
  - aca
title: Attivo Comms Agent
type: tool
---
ated: 2026-06-08
pillar: Arachne Intelligence
status: active
tags: [tool, ai, email, aca]
title: Attivo Comms Agent
type: tool
---

# Attivo Comms Agent

Up: [[Arachne Intelligence]]

**ACA** — an AI agent that learns my email-handling and delegation patterns to cut the morning inbox slog. A predict / evaluate learning loop over consulting email; it knows, for instance, which client threads I lead versus where I'm only CC'd for visibility.

An Augmentation tool: it serves the consulting work, yet it's something I *built to make myself better* — distinct from the consulting itself. Posts in the Arachne Finance Slack workspace.

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

## Proactive-send patterns
The rules above are all reactive — predicting responses to inbound mail. This is a separate axis: predicting *unprompted* sends.
- **Proactive-build forcing function.** On days with a strategic-finance/FP&A focus block for a given client — especially Fridays — expect an unprompted, client-facing BUILD deliverable (a model, a pricing tool, even a prototype web asset) to ship same-day to that client's exec/GTM contacts, independent of any inbound trigger. Surface it as a candidate proactive send during the morning scan, rather than folding it into the day's no-response defaults.

## Open threads
- Track prediction accuracy / eval over time.
- Build the **improvement layer**: turn each learned habit into a suggested better-practice, working toward the Phase-2 AI-powered communication cadence.
- Decide how far to extend it beyond triage.
- **Learning-loop reliability gap (open, in progress).** `learnings/accumulated.md` doesn't persist across ephemeral morning/evening session containers — evening runs write lessons to Open Brain + Drive but the repo commit doesn't push — so morning runs periodically reset to "first run" and repeat mistakes the loop already corrected (a scored miss on 6/29, a near-miss on 6/25). Fix in progress: (a) backfill + commit `accumulated.md` from Open Brain, (b) point the morning routine at Open Brain semantic search as the system of record and forbid the "empty learnings" self-declaration when Open Brain holds prior [ACA] lessons, (c) ensure evening runs commit + push every time. Close this out after two consecutive clean mornings.

*Lineage: distilled from the `[ACA] Lesson` cluster in Open Brain (6/10–6/23), via the 2026-06-24 dream; extended with the 6/24–6/30 cluster (automated-digest/scope rule, proactive-send axis, learning-loop reliability gap) via the 2026-07-01 dream.*
