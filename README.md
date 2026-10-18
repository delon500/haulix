# Haulix

**The download manager that's smart about everything around the download.**

Haulix pairs fast, resumable downloads and media extraction from thousands of
sites with automation, remote control from any device, and a searchable
library of everything you save. It will run on Windows, macOS and Linux.

> **Status: pre-alpha.** The project is just starting. Nothing is built yet;
> this README describes the plan for the first release (v0.1).

## What Haulix will do

- **Download anything, fast:** segmented downloads with resume that survives crashes, reboots and dropped connections.
- **Save media from websites:** video and audio from thousands of sites (via yt-dlp), including just a clip of a long video.
- **Work for you:** rules, subscriptions and schedules decide what downloads, when, and where it goes.
- **Run anywhere:** the engine can live on a laptop, home server or NAS, controlled from desktop, browser or phone.
- **Make downloads useful:** transcribe, organise and search inside what you've saved.

## How it fits together

One background engine does all the work. Every interface is a client of its
local REST and WebSocket API:

```
 Desktop app    Web dashboard    Phone app    Browser extension
      \               |              |               /
       '------ local API (REST + WebSocket) --------'
                              |
                    haulixd (Rust engine)
                              |
           yt-dlp · ffmpeg · whisper.cpp · SQLite
```

## Planned repository layout

| Path | What it will be |
| --- | --- |
| `crates/haulix-core` | Types shared by the engine and its clients |
| `crates/haulixd` | The engine: a background service with the local API |
| `apps/desktop` | Desktop app: Tauri 2, React, TypeScript, Tailwind |
| `apps/extension` | Browser extension for Chrome and Firefox (WXT) |
| `docs` | Product overview, feature catalogue, planning data and architecture decisions: start at [docs/README.md](docs/README.md) |

## Tech stack

| Layer | Choice |
| --- | --- |
| Engine | Rust (Tokio, Axum) |
| Desktop shell | Tauri 2 |
| UI | React, TypeScript, Tailwind CSS |
| Browser extension | WXT (Manifest V3) |
| Media | yt-dlp and ffmpeg, bundled as helper programs |
| Local data | SQLite |

## Prerequisites

- Rust (stable), installed with [rustup](https://rustup.rs)
- Node.js 22 and pnpm 10
- Tauri's system dependencies for your OS: see [tauri.app/start/prerequisites](https://tauri.app/start/prerequisites/)
- Git

## Roadmap

| Release | Focus |
| --- | --- |
| v0.1 Foundation | Fast downloads, media, clips; Windows and macOS; Chrome and Firefox |
| v0.5 Beta | Rules, subscriptions, Linux, plain-language errors |
| v1.0 Launch | Transcribe and search videos, send from phone, Pro tier |
| v2.0 Everywhere | Server and NAS mode, web dashboard, metered-data tools |
| v3.0 Intelligence | Summaries, meaning-based search, plain-English commands |
| v4.0 Ecosystem and Teams | Plugins, API, integrations, team features |

## Contributing

Contributions will be welcome once the foundation is in place. Haulix is open
core, so contributors will sign a contributor licence agreement (CLA) on their
first pull request.

## Licence

The engine, desktop app and browser extension will be licensed under the
GNU General Public License v3.0 only (GPL-3.0-only).
