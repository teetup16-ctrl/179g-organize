# 179G-Organize

Team work-organizer app (Thai UI): calendar with drag-and-drop jobs, grouped project table, equipment, clients (logos + socials), post prep (captions/tags), and a built-in AI assistant with undo.

## Where it lives
- Published as a claude.ai Artifact: https://claude.ai/code/artifact/e01f171e-d2c3-49ea-b50c-d57ffc1a4fec
- The whole app is `index.html` (one self-contained file: markup, styles, script).

## Important: data is NOT in this repo
- All jobs/clients/equipment are stored in the Artifact's shared database via `window.claude.use("db")`.
- The AI assistant uses `window.claude.use("sample")`; file export uses `window.claude.use("downloads")`.
- These only work when the page runs as the published Artifact. Opening `index.html` locally shows the UI but no data and no AI.
- Never rename or reshape stored collections/fields without a migration path — existing records must keep loading.
- `localStorage` is only for per-viewer conveniences (theme `ruap-theme`, AI undo).

## How to ship a change
1. Edit `index.html`.
2. Publish it back to the SAME artifact URL above (Artifact tool, publish with `url`, keep existing capabilities). Never publish without `url` — that creates a new, empty app.
3. Commit the change to git with a short message.

## Conventions
- UI text is Thai; fonts Noto Sans Thai + Plus Jakarta Sans.
- Colors are CSS tokens on `:root`, with light/dark themes (`data-theme`).
- Must stay usable at phone width.
