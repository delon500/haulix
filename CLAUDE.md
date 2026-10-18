# CLAUDE.md

Guidance for Claude Code when working in this repository.

## Project

Haulix is a cross-platform download manager (Windows, macOS, Linux). One Rust
background engine (`haulixd`) does all the work; the desktop app, browser
extension and, later, a web dashboard and phone app are clients of its local
REST + WebSocket API. The project is pre-alpha and is being built up by hand.

## How to work with me

- I'm building the folder structure and code myself, and I'm learning Rust as I go. Explain what you're doing and why, in plain language, especially for Rust concepts (ownership, lifetimes, async, error handling).
- Prefer small, reviewable steps. Don't create many files or scaffold whole projects unless I ask; propose the plan first.
- When there's a real choice, give me the options and a recommendation instead of silently picking one.
- If something contradicts the decisions below, point it out rather than working around it.

## Environment

- Windows, PowerShell. Project root: `D:\A Downloader Project\Haulix`.
- Give commands in PowerShell syntax (e.g. `$env:RUST_LOG="debug"`, not `export`).
- The path contains spaces: always quote paths.

## Decisions already made

1. **Engine in Rust**, using Tokio (async) and Axum (local API).
2. **Engine runs as a separate background service** (`haulixd`), started by the desktop app as a Tauri sidecar. Downloads keep running when the window closes.
3. **Every client talks to the engine through its local API** (`/api/v1`), never Tauri commands. This lets the web dashboard reuse the desktop UI later.
4. **One repository** with a Cargo workspace (Rust) and a pnpm workspace (TypeScript).
5. **Open core, GPL-3.0-only.** This repo is public from day one; Pro features, cloud backend and mobile apps live in a separate private repo later. Contributors sign a CLA.
6. **Desktop app:** Tauri 2 with React, TypeScript and Tailwind CSS.
7. **Browser extension:** WXT, Manifest V3. It never downloads media itself; it hands links to the app (browser store rules).
8. **Media extraction:** yt-dlp and ffmpeg run as bundled helper programs, never reimplemented.
9. **No telemetry** unless the user opts in.

## Documentation

Read these before proposing features or architecture changes:

- `docs/product/overview.md`: what we're building, for whom, roadmap, boundaries.
- `docs/product/feature-catalogue/`: all 130 features, one file per release, each with a user story and acceptance criteria. Use the acceptance criteria as the definition of done and as test cases.
- `docs/product/personas.md`: Maya, Diego, Priya, Sam, Lerato.
- `docs/planning/features.csv`: every feature's version, tier and status. Update `Status` when a feature is started or finished.
- `docs/adr/`: why things are built the way they are. When a decision changes, add or update an ADR.

`docs/private/` is git-ignored and holds pricing and business notes. Never copy its contents into public files, commits or code comments.

## Planned layout

```
Cargo.toml              Cargo workspace root
package.json            pnpm workspace root
crates/haulix-core/     shared types (API data shapes)
crates/haulixd/         the engine and its local API
apps/desktop/           Tauri 2 + React app (src-tauri/ for the Rust shell)
apps/extension/         WXT browser extension
docs/                   product docs, planning CSVs, ADRs (see Documentation)
```

## Engine API rules (security)

- Listen on `127.0.0.1` only, default port `7432` (override with `HAULIX_PORT`).
- Reject requests whose `Host` header isn't the local machine (blocks DNS rebinding).
- CORS: allow only the app's origins (`tauri://localhost`, `http://tauri.localhost`, `https://tauri.localhost`) and the Vite dev server (`http://localhost:1420`).
- Before any endpoint can start, change or delete downloads, require a per-install access token.
- Never open or execute downloaded files automatically. Sanitise filenames so they can't escape the download folder.

## Code conventions

- Rust: edition 2024, `unsafe_code = "forbid"`, `cargo fmt` and `cargo clippy -- -D warnings` clean. Use `Result` and `?` rather than `unwrap()` outside tests.
- Shared API types live in `haulix-core`; the TypeScript mirror lives in the desktop app until types are generated from Rust.
- TypeScript: strict mode; no `any`.
- UI copy: plain language, no raw error codes shown to users.
- Accessibility from the start: keyboard navigation, labels for screen readers, no meaning by colour alone.

## Checks before committing

```powershell
cargo fmt --all --check
cargo clippy --all-targets -- -D warnings
cargo test
pnpm typecheck
pnpm build
```

Add or update tests for any behaviour you change.

## Current focus: v0.1 spikes

1. Tauri app runs a bundled yt-dlp and shows its progress.
2. Chrome extension sends a link to the app through native messaging.
3. Rust program downloads one file in parallel segments and resumes after being killed.

## Git

- Default branch `main`. Small commits with plain, descriptive messages.
- Never commit secrets, `.env` files, `target/` or `node_modules/`.
