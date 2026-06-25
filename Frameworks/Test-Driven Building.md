---
created: '2026-06-08'
pillar: Arachne Intelligence
status: stub
tags:
  - framework
  - tdb
  - ai
  - modeling
title: Test-Driven Building
type: framework
---
# Test-Driven Building

Up: [[Arachne Intelligence]]

**TDB** — applying TDD principles to AI-assisted financial modeling. Specify the test assertions upfront (statement ties, revenue-shape properties, zero-output detection), and the human leaves the inner iteration loop: a human-gated cycle becomes a **test-gated** one the AI closes autonomously.

## Why it matters
- Sits in the AI-in-Finance content pillar; framed within the [[12-Month Lag Theory]].
- A differentiating piece of IP and content (case study + LinkedIn post).
- Pairs with [[Change-Log Model Discipline]]: tests prove a model is right *within* a version; the change-log proves what moved *between* versions.

## Concrete build patterns (from Case Study 1)
**The 4-tab pattern:** (1) Tests dashboard, (2) Assumptions (single source of truth), (3) a build tab (e.g. Headcount Plan), (4) Projections output. The Tests tab is the heart — each test is a live formula: column E computes "Actual", column F is `=IF(…,"PASS","FAIL")` — grouped by phase, cumulative, starting all-RED, with "model not built" guards so empty ranges read FAIL rather than a premature PASS.

**Test taxonomy (7 categories):** scaffold · identity · tie-out · sanity/bound · driver-traceability · integrity · toggle/mode.

**Failure-modes checklist:** anchor month serials from a canonical tab (date-serial drift); verify every source row/col and lock period columns (mapping errors); weight %-row FY totals and skip them in the FY=sum test; prefer SUMPRODUCT and explicit cell writes over INDEX/N, TRANSPOSE, OFFSET-SUBTOTAL (fragile, esp. Mac Excel); write flat references explicitly rather than copy-filling (copyToRange shifts).

## Open threads
- Build the canonical assertion library (the taxonomy above is its seed).
- Ship the case-study write-up via [[Finance Content]].

*Lineage: build patterns distilled from three Open Brain thoughts (6/10), via the 2026-06-24 dream.*
