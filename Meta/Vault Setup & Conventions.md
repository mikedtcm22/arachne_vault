---
title: Vault Setup & Conventions
type: meta
status: active
tags: [arachne, meta, obsidian, setup]
created: 2026-06-08
---

# Vault Setup & Conventions

First-time Obsidian setup for this second-brain vault.

## Opening the vault
Obsidian works on folders. Point it at this folder with **Open folder as vault** — it creates a hidden `.obsidian` config folder and you're live. Everything here is plain Markdown, so it stays yours and portable.

## How linking works (the key idea)
`[[Wikilinks]]` resolve by **note name**, anywhere in the vault — folders are irrelevant to them. So the folder layout below is purely for human browsing; you can move notes between folders freely and links won't break. Build with links first; use folders lightly.

## Folder layout (organizational only)
- **(root)** — entry points: [[Arachne — Overview]], [[Arachne Finance]], and the two pillar MOCs.
- **Frameworks/** — the reusable IP.
- **Tools/** — built systems.
- **Positioning/** — career-advantage and content notes.
- **On-Chain/** — the experimentation pillar's projects.
- **Meta/** — this note and [[Open Brain ↔ Arachne]].
- **Templates/** — note skeletons.

## MOCs over folders
The navigation backbone is **Maps of Content** — index notes like [[Arachne Intelligence]] that link out to their members. Start at [[Arachne — Overview]] and follow links. This scales better than deep folders and matches how a second brain is actually traversed.

## Properties (frontmatter)
Every note opens with YAML properties Obsidian reads as **Properties**: `type`, `pillar`, `status`, `tags`, `created`. Keep them consistent — they're what lets you auto-generate indexes later.

## Conventions
- **A note is a system or playbook** — integrated, structured, worth maintaining. Atomic thoughts stay in [[Open Brain]].
- **Up-links.** Every note links *up* to its MOC (`Up: [[...]]`) and sideways to what it relates to.
- **Promotion.** Notes here grow from an Open Brain cluster; link back to it. See [[Open Brain ↔ Arachne]].
- **Boundary.** The billable work and ordinary life don't get notes here.
- **Naming.** Title Case, human-readable; the filename *is* the link target.

## Plugins worth turning on
Core (Settings → Core plugins): **Backlinks**, **Outgoing links**, **Graph view**, **Templates**. **Daily notes** is optional — capture mostly lives in Open Brain, so you may not need it.

Community (Settings → Community plugins → Browse) — two that earn their place in a second brain:
- **Dataview** — live queries that auto-list notes by property (e.g., everything where `pillar = Arachne Intelligence`). Replaces hand-maintained map lists. Each MOC already has a ready query block under "Auto-index."
- **Templater** — richer templates than the core plugin (auto-filled dates, prompts). The `Templates/` folder here works with either.

Nice-to-have later: **Iconize** (folder/note icons), **Style Settings** (theme tweaks).

## Backup
It's all local Markdown — version it with **Git** (fits the privacy ethos and your repo habit) or use **Obsidian Sync** for cross-device without managing a remote.

## Start here
1. Open this folder as a vault.
2. Open [[Arachne — Overview]] and read down.
3. Turn on Dataview; swap the manual MOC lists for the query blocks if you like them.
4. Fill stubs as you work — promote from [[Open Brain]] when a cluster firms up.
