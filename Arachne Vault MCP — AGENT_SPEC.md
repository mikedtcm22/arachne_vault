# Arachne Vault MCP — AGENT_SPEC

Machine-readable build spec for an Open Brain–style MCP extension that exposes the **Arachne Obsidian vault** to any MCP client (Claude.ai web, Desktop, Code). Written to be generated in roughly one pass by an agent that also has the OB1 repo (`NateBJones-Projects/OB1`) checked out for its template and primitives.

---

## 0. Operator pre-flight (HUMAN — do these before handing the package to Claude Code)

Claude Code can write all the code, install deps, deploy the function, set secrets, generate the access key, and run smoke tests. It **cannot** create accounts, click through credential UIs, or register a connector inside Claude.ai. Handle these and there are no mid-build stops:

1. **Vault repo (source of truth).** Create a **private** GitHub repo and get the vault markdown into it — push the `Arachne Vault` folder, or open it in Obsidian and enable the **Obsidian Git** plugin to commit/push. Record `owner/name` and the default branch. If the vault is the repo root, `VAULT_SUBPATH=""`; if it's a subfolder, record that path.
2. **GitHub PAT.** Create a **fine-grained** personal access token scoped to *only* that repo, permission **Contents: Read** (Phase 1) or **Read and write** (Phase 2). This becomes `GITHUB_TOKEN`. Token creation is a web-UI step Code can't perform.
3. **Supabase project — reuse, don't create.** No new project and no database setup needed. Reuse the **existing Open Brain project** and add a *second* Edge Function to it (an Edge Function is a project-level resource; the project's Postgres DB simply sits unused for this connector). Have the **project ref** ready and authenticate the CLI: `supabase login` (browser) or export `SUPABASE_ACCESS_TOKEN`. Spin up a separate project only if you want hard isolation.
4. **MCP access key.** Pick a long random string for `MCP_ACCESS_KEY` (or let Code generate one). You'll need it twice — as a function secret and when registering the connector — so save it where you can paste it later.
5. **OB1 in the workspace.** `git clone https://github.com/NateBJones-Projects/OB1` next to where Code will work, so it has the extension template and `primitives/{deploy-edge-function,remote-mcp}` to follow. (Code can do this itself if it has git access — listing it so nothing's assumed.)

**Only post-build human step:**

6. **Register the connector in Claude.ai** → Settings → Connectors → add the deployed function URL with the `MCP_ACCESS_KEY`. Code can't reach into Claude.ai's settings; it will hand you the URL + key to paste.

---

## 1. Purpose

Give AI clients the same one-mention seamlessness as "search my Open Brain," but for the curated, **pre-linked** Arachne vault — so the model reads the integrated structure (MOCs, `[[wikilinks]]`, `Up:` links, `pillar` properties) directly instead of re-deriving connections each time. Read first; later, write notes back to automate the Open Brain → vault promotion loop.

## 2. Core design decision (CONFIRM before building)

**Source of truth = the vault's GitHub repo (markdown).** The MCP reads/writes notes via the GitHub API. No database, no embeddings.

- Rationale: the vault is small (~31 notes) and already linked by hand in plaintext. Connections are pre-made; the model just follows them. Semantic search is unnecessary at this size.
- This is the one variable an agent must not silently change. If the owner instead wants to mirror notes into Supabase like the core brain (enables full-text/vector queries at scale), swap §6 (storage/parse) and add a `schema.sql` + sync — everything else in this spec stands.

## 3. Architecture

```
Obsidian (human editor)
   │  Obsidian Git plugin commits edits
   ▼
GitHub repo  ──────────  SOURCE OF TRUTH (markdown + frontmatter + [[wikilinks]])
   ▲   │ GitHub API (read tree + contents; write via contents PUT)
   │   ▼
Arachne Vault MCP  =  Deno + Hono + @hono/mcp, deployed as a Supabase Edge Function
   │  StreamableHTTPTransport, Authorization: Bearer MCP_ACCESS_KEY
   ▼
Claude.ai / Desktop / Code  (registered as a remote/custom connector)
```

Reuse from OB1: the Edge-Function + remote-MCP transport + access-key pattern (`primitives/deploy-edge-function`, `primitives/remote-mcp`, `extensions/_template`). Drop from OB1: Supabase content tables, pgvector, and OpenRouter (no embeddings/LLM calls in this extension).

## 4. Non-goals (do not build these)

- No embeddings, pgvector, or `OPENROUTER_API_KEY`. This extension makes zero model-API calls.
- No Supabase content tables / no DB mirror of the notes (git is the only source of truth).
- Do **not** atomize notes into thoughts, and do **not** use OB1's `recipes/obsidian-vault-import` — it flattens the vault into the `thoughts` table, destroying the structure this system exists to preserve.
- Do not reimplement Obsidian. Just read, traverse, and write markdown.

## 5. Output files (in `extensions/arachne-vault/`)

Follow `extensions/_template/AGENT_SPEC.md`, with these deltas:

| File | Notes |
|------|-------|
| `index.ts` | The Edge Function MCP server (tool surface in §7). |
| `deno.json` | Import map (see §6). |
| `metadata.json` | Per OB1 schema. `requires.open_brain: false`; `requires.services: ["GitHub API"]`; `requires_primitives: ["deploy-edge-function","remote-mcp"]`. |
| `README.md` | Per OB1 template, including the deploy table and the Claude.ai connect step. |
| `schema.sql` | **Omit** (no database in the chosen design). |

## 6. deno.json + parsing

Import map: keep `@hono/mcp@0.1.1`, `@modelcontextprotocol/sdk@1.24.3`, `hono@4.9.2`, `zod@4.1.13`. **Remove** `@supabase/supabase-js`. **Add** a frontmatter parser (`npm:gray-matter`). GitHub access uses plain `fetch` against `https://api.github.com` (no SDK required).

GitHub calls:
- Enumerate notes: `GET /repos/{owner}/{repo}/git/trees/{branch}?recursive=1`, filter to `*.md` under `VAULT_SUBPATH`.
- Read a note: `GET /repos/{owner}/{repo}/contents/{path}?ref={branch}` (base64) or raw.githubusercontent.com.
- Write a note (Phase 2): `PUT /repos/{owner}/{repo}/contents/{path}` with `{message, content(base64), branch, sha?}`.

Parsing rules:
- Frontmatter via gray-matter → `{type, pillar, status, tags, created, title}`.
- Wikilinks: regex `/\[\[([^\]]+)\]\]/g`; for each, take the part before `|` (alias) and before `#` (heading); trim. **Skip matches inside inline code or fenced code blocks** (the setup note contains literal `` `[[Wikilinks]]` `` examples that are not real links).
- Resolution is by **basename** across the whole vault (Obsidian semantics), so folders are irrelevant to link resolution.
- Build a per-invocation index: `name → path`, plus a reverse map for backlinks. Caching/ETags are a later optimization (non-goal now).

## 7. Tool surface

### Phase 1 — read (all `readOnlyHint: true`)

- `list_notes({ folder?, pillar?, type? })` → `[{title, path, type, pillar, status, tags}]`. Use to see what exists / scope a pillar.
- `read_note({ title? , path? })` → `{title, path, frontmatter, body, outgoing_links[]}`. Resolve `title` by basename. Use to read a specific note.
- `get_map({ name? })` → returns the named MOC's body plus its resolved members (`{title, type, pillar}`); when `name` is omitted, default to the home note **"Arachne — Overview"**. This is the primary entry point — one call returns the integrated map.
- `search_notes({ query, limit? })` → case-insensitive match over title + tags + body; return `[{title, path, snippet}]`. Plain text match (no embeddings).
- `get_backlinks({ title })` → `[{title, path}]` of notes whose body links to `title`.

Tool descriptions must say **when** to use each (the model reads these to choose). Lead descriptions with the trigger, e.g. `read_note`: "Use when the user references a specific Arachne note or system by name."

### Phase 2 — write (enable deliberately, after Phase 1 is trusted)

- `upsert_note({ path, frontmatter, body, message? })` → creates or updates a note and commits to the repo. Annotations: `readOnlyHint: false`, `openWorldHint: false`, `destructiveHint: false` for new files; treat an overwrite of an existing path as `destructiveHint: true`. Returns the commit URL.
  - This is what turns the promotion loop into a tool call: a thought-cluster firms up → the model drafts the system note, writes it under the right folder, and links it back.

## 8. Auth + transport (mirror OB1)

- One Hono app. Mount MCP on `app.all(...)` with `StreamableHTTPTransport`; `server.connect(transport)` then `transport.handleRequest(c)`.
- Before handling: read the `Authorization` header, compare against `Deno.env.get("MCP_ACCESS_KEY")`, return `401` on mismatch.
- Patch the `Accept` header to include `text/event-stream` if absent (same as OB1 extensions).
- `app.get("*")` health check returning `{status:"ok"}`.

## 9. Credentials — deploy-time vs runtime

Two distinct buckets. This matters: the **function never touches the Supabase database or Auth**, so there are no anon/service keys and no DB password anywhere.

**Deploy-time (Supabase CLI only — not stored on the function):**
```
SUPABASE_ACCESS_TOKEN   # personal access token from Supabase Dashboard → Account → Access Tokens
                        #   (lets the CLI deploy + set secrets non-interactively)
project ref             # gastsevmolxjrnwguatq  (reuse the existing Open Brain project — CONFIRM)
```

**Runtime (the only secrets set on the function):**
```
MCP_ACCESS_KEY   # bearer token MCP clients must send; generate with:  openssl rand -hex 32
GITHUB_TOKEN     # the fine-grained PAT (repo mikedtcm22/arachne_vault, Contents R/W)
GITHUB_OWNER     # mikedtcm22
GITHUB_REPO      # arachne_vault
GITHUB_BRANCH    # main
VAULT_SUBPATH    # ""   (push the vault's contents to the repo root, so the .md files sit at top level)
```
No `OPENROUTER_API_KEY`. No Supabase keys at runtime — Supabase is only the host.

## 10. Deploy + connect

Function name = `arachne-vault-mcp` (its code must live at `supabase/functions/arachne-vault-mcp/index.ts`; the deploy name matches the folder). Reuse the existing Open Brain Supabase project; authenticate the CLI by exporting `SUPABASE_ACCESS_TOKEN`.

1. **Deploy with JWT verification OFF.** The function self-authenticates via `MCP_ACCESS_KEY`, and external MCP clients can't present a Supabase JWT — so Supabase's default JWT gate must be disabled or it returns 401 before the request reaches the function:
   ```
   supabase functions deploy arachne-vault-mcp --project-ref gastsevmolxjrnwguatq --no-verify-jwt
   ```
2. **Set the runtime secrets:**
   ```
   supabase secrets set --project-ref gastsevmolxjrnwguatq \
     MCP_ACCESS_KEY=<openssl-rand-hex-32> \
     GITHUB_TOKEN=<fine-grained-PAT> \
     GITHUB_OWNER=mikedtcm22 \
     GITHUB_REPO=arachne_vault \
     GITHUB_BRANCH=main \
     VAULT_SUBPATH=""
   ```
3. **Resulting MCP URL:** `https://gastsevmolxjrnwguatq.supabase.co/functions/v1/arachne-vault-mcp`
4. In **Claude.ai → Settings → Connectors**, add that URL as a custom connector with the `MCP_ACCESS_KEY` as its bearer credential (same flow as the Open Brain connector). See OB1 `primitives/remote-mcp`.

> Verify against current docs (knowledge cutoff ~Jan 2026): the exact JWT-disable mechanism (`--no-verify-jwt` flag vs. `verify_jwt = false` in `supabase/config.toml`) and the Claude.ai connector-add UI may have shifted — have Code confirm via the current Supabase CLI and OB1's `remote-mcp` primitive.

## 11. Acceptance tests (smoke)

1. Connector shows as connected; tools listed.
2. "What's in my Arachne vault?" → `list_notes` returns ~31 notes across the folders.
3. "Read my Arachne overview." → `get_map()` returns the genesis note + its members.
4. "What links to Reclude?" → `get_backlinks({title:"Reclude"})` includes the Intelligence MOC, Active vs Passive AI Safety, AI-Powered Finance Builder.
5. `search_notes({query:"breakout accounts"})` finds the Finance Leadership Briefcase.
6. (Phase 2) "Promote this cluster into a note" → `upsert_note` commits; the new `[[link]]` resolves on next read.

## 12. Build order for the agent

1. Scaffold `extensions/arachne-vault/` from the template; write `deno.json`, `metadata.json`.
2. Implement GitHub read layer + parser + per-invocation index (§6).
3. Implement Phase 1 read tools (§7) with auth/transport (§8).
4. Deploy, set secrets, connect, run smoke tests 1–5.
5. Add `upsert_note` (Phase 2); re-run test 6.
6. Write `README.md` last, reflecting the actual env vars and deploy steps.

## 13. Passing credentials to Code (safely)

- Put secrets in a local, **gitignored** `.env` (or the shell env / a secrets manager) and tell Code where they are. Never commit them, and don't hardcode them in `index.ts` — they're read from `Deno.env` / Supabase secrets at runtime.
- Keep the PAT fine-grained and minimal-scope (that one repo, Contents only). It lives only as a Supabase function secret; rotate or revoke freely.
- Code sets the live secrets with `supabase secrets set …` (§10). The local `.env` is only for any local read-tests Code runs while building.
