# 179G-Organize

Team work-organizer app (Thai UI): "งานของฉัน" home page (each viewer's own jobs), calendar with drag-and-drop jobs, grouped project table, equipment, clients (logos + socials), post prep (captions/tags), and a built-in AI assistant with undo.

## Where it lives
- Published as a claude.ai Artifact: https://claude.ai/code/artifact/e01f171e-d2c3-49ea-b50c-d57ffc1a4fec
- The whole app is `index.html` (one self-contained file: markup, styles, script).

## Important: data is NOT in this repo
- All jobs/clients/equipment are stored in the Artifact's shared database via `window.claude.use("db")`.
- The AI assistant uses `window.claude.use("sample")`; file export uses `window.claude.use("downloads")`.
- These only work when the page runs as the published Artifact. Opening `index.html` locally shows the UI but no data and no AI.
- Never rename or reshape stored collections/fields without a migration path — existing records must keep loading.
- `localStorage` is only for per-viewer conveniences (theme `ruap-theme`, AI undo, which Crew member "me" is: `179g-me`).
- `sessionStorage` key `179g-intro` marks that the logo intro already played this session (intro markup + early inline script sit right after `<body>`). The intro shows the real logo PNGs from Drive folder "Logo 179G" (`logo 179G 2.png` dark theme, `logo 179G.png` light theme) — never redraw or alter the logo; the animated strokes are only a mask that reveals it.

## Permissions (by Crew position)
- `settings/permissions` = `{on, roles:{<position>|"__none"|"__guest":{pages,acts}}, links:{<user id>:<crew name>}}`; `members/<user id>` = a person's pending link request.
- Artifact Owner/Editor (`user.isOwner()/canEdit()`, db level `admin`) always have full access and manage it in Setting > สิทธิ์.
- Every db write function starts with `need("<act>")`; use `asAct("move"|"done"|"docs", fn)` when a write happens as a different action. New write paths must get a `need(...)` too.
- Server-side db rules (declared on publish; keep them when changing capabilities): `settings/permissions` write admin; `members` read view / write admin; `members/{self}` write interact. Per-position checks are UI-level only.
- Capabilities declared: `{db:{rules:[...]}, downloads:{}, sample:{}, user:{scopes:["profile"]}}`.

## How to ship a change
1. Edit `index.html`.
2. Publish it back to the SAME artifact URL above (Artifact tool, publish with `url`, keep existing capabilities). Never publish without `url` — that creates a new, empty app.
3. Commit the change to git with a short message.

## Conventions
- UI text is Thai; fonts Noto Sans Thai + Plus Jakarta Sans.
- Colors are CSS tokens on `:root:root:root`, with dark (default) / light themes switched by `data-app="light"` on `<html>`.
- Must stay usable at phone width.
