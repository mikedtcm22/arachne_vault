---
title: Advisory Circle
type: tool
pillar: Arachne Intelligence
status: active
tags: [tool, ai, advisory-circle]
created: 2026-06-08
---

# Advisory Circle

Up: [[Arachne Intelligence]]

A custom local web app (v4.0) — a multi-agent AI advisory board for Sunday-morning strategic meetings.

## Personas
- **Arachne** — Visionary Builder / Life-Alignment
- **Balaji Srinivasan** — Strategist / Systems
- **Jason Fried** — Work Philosophy / Sustainability
- **Claire Hughes Johnson** — Finance Leadership / Stewardship
- **Marcus Aurelius** — Philosopher / Inner Sovereignty

## Mechanics
- **Response modes:** solo (one speaker), perspectives (two complementary angles), debate (exam → cross-examination → redirect, courtroom-style) — controlled by an invisible moderator.
- **Posture system** (set per meeting, changeable mid-meeting): Open · Execution Support · Stress Test · Exploration — injected into each persona's listening/response protocol.
- Agenda generation from uploaded docs, secretary-selected board minutes, shared-history synthesis, mid-meeting file upload, @-poke menu, voice-rotation to prevent single-persona dominance.

## Stack
FastAPI + WebSocket streaming, single-file HTML chat UI, runs at `localhost:8000`. Sonnet for previews/moderator; Opus for full responses.

## Open threads
- Archive meeting minutes here; note which decisions came from the Circle.
