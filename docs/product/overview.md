# Product Overview: What We're Building

*Last updated: 18 October 2026*

We're building Haulix, a cross-platform download manager that goes beyond downloading: it pairs IDM-class speed and yt-dlp's site coverage with automation, remote control from any device, and a searchable library of everything you save.

## The problem

Every existing download tool is good at one job and weak at the rest. Nobody combines fast general downloads, deep media extraction and a clean, trustworthy experience on every platform.

| Tool | Strong at | Falls short on |
| --- | --- | --- |
| IDM | Fast segmented downloads, browser capture | Windows only, closed source, dated interface, paid |
| yt-dlp | Media from thousands of sites | Command line only, steep learning curve |
| JDownloader 2 | File hosts, bulk link handling | Heavy, cluttered, installer bundles adware |
| FDM, AB Download Manager | Free, cross-platform | No deep automation, no remote use, no library |

They also share three blind spots. Every tool stops at "file saved", so nothing helps users find what's inside their downloads. None can be controlled from a phone while the work happens at home. And none adapts to expensive data, unreliable power or a shared, busy network, which is everyday reality for many users worldwide.

## The product

**Pitch:** the download manager that's smart about everything around the download, not just the download itself.

It is one app, on every device, that does four jobs:

1. **Downloads anything, fast.** Any file over HTTP, FTP or BitTorrent at full speed, plus video and audio from thousands of sites, with resume that survives crashes, reboots and dropped connections.
2. **Works for you automatically.** Rules, subscriptions and schedules decide what downloads, when, in what quality and where it goes.
3. **Runs anywhere, controlled from anywhere.** The engine can live on a laptop, a home server or a NAS, and users manage it from the desktop, a browser or their phone.
4. **Makes downloads useful.** It transcribes, organises and indexes what users save, so they can search inside videos and documents and jump to the exact moment.

We don't compete on raw speed or site coverage, where IDM, aria2 and yt-dlp are already excellent. We use them (or match them) under the hood, and compete on everything around them.

## Who it's for

Five personas guide every feature in the [Feature Catalogue](feature-catalogue/README.md).

| Persona | Who they are | What they need most |
| --- | --- | --- |
| Maya | University student | Lectures offline, clips and transcripts for study, saving storage |
| Diego | Video creator and editor | High-quality source footage, large files, batch work, automation |
| Priya | Remote worker who travels | Downloads that survive bad connections, control over data costs |
| Sam | Power user with a home server | Privacy, self-hosting, scripting, keyboard-driven control |
| Lerato | IT manager at a 200-person company | Central control, security policies, easy rollout to staff |

The first four drive the consumer product (v0.1 to v3.0). Lerato drives the business features in v4.0.

## What makes it different

13 of the 130 planned features are differentiators: things current download managers lack or do badly. They are what the product is sold on.

| ID | Differentiator | Why it matters | Release |
| --- | --- | --- | --- |
| F-008 | Clip downloads | Save just the part of a video you need | v0.1 |
| F-022 | No telemetry, open core | Trust, against adware-laden free tools | v0.1 |
| F-043 | Rules engine | Downloads file and name themselves | v0.5 |
| F-054 | Plain-language errors with one-click fixes | Non-technical users solve problems alone | v0.5 |
| F-059 | Local transcription | Speech in every video becomes text, offline | v1.0 |
| F-060 | Full-text search across downloads | Find anything said or written in your library | v1.0 |
| F-061 | Jump to the moment from search | Results open the video at the exact second | v1.0 |
| F-063 | Send from phone, download at home | Use home internet, not mobile data | v1.0 |
| F-079 | LAN sharing | Download once, share to every device in the house | v2.0 |
| F-081 | Metered connection detection | Never burn mobile data by accident | v2.0 |
| F-082 | Cost preview in your currency | See what a download costs before starting | v2.0 |
| F-087 | Polite mode | Steps aside for video calls and games automatically | v2.0 |
| F-090 | Outage schedule plugins | Plans downloads around scheduled power cuts | v2.0 |

IDs refer to the Feature Catalogue.

## How it works

One background engine does all the real work, and every interface is a client that talks to it over the same API. That single choice is what lets the same engine run on a laptop, a NAS or a cloud server, and be controlled from anywhere.

```
 Desktop app    Web dashboard    Phone app    Browser extension
      \               |              |               /
       '------ local API (REST + WebSocket) --------'
                              |      (phone, when away: encrypted relay)
                    haulixd (Rust engine)
   Downloader · Queue and scheduler · Rules and automation
   Library and search · Network and power · Local API server
                              |
     yt-dlp, gallery-dl · ffmpeg · whisper.cpp, llama.cpp · SQLite
```

On the same network, clients talk to the engine directly; away from home, the phone reaches it through our end-to-end encrypted relay. Downloads themselves never pass through our servers.

## Where it runs and how it's built

It is a desktop app first, an always-on server second, with phones and browsers as remote controls everywhere else.

| Where | Role | From |
| --- | --- | --- |
| Windows 10/11, macOS 10.15+ | Engine + desktop app | v0.1 |
| Linux (AppImage, Flatpak, .deb, .rpm) | Engine + desktop app | v0.5 |
| Chrome, Firefox, then Edge, Brave, Safari | Extension that hands links to the engine | v0.1 to v3.0 |
| Android and iOS | Share target and remote control, later a full app | v1.0 |
| Docker, NAS, Raspberry Pi, VPS | Engine only, always on | v2.0 |
| Any browser | Web dashboard | v2.0 |

**Core technology:**

- **Engine:** Rust (Tokio, Axum), with its own segmented downloader; aria2 as a stand-in for v0.1.
- **Media:** yt-dlp, ffmpeg and gallery-dl as bundled helper programs, updated separately from the app.
- **Desktop UI:** Tauri 2 with React, TypeScript and Tailwind; the same UI serves the web dashboard.
- **Data and search:** SQLite with full-text search, plus sqlite-vec for meaning-based search.
- **AI:** whisper.cpp for transcription and llama.cpp for summaries, running locally; cloud AI optional for Pro.
- **Cloud:** a small backend for accounts, licensing, payments and an end-to-end encrypted relay. Downloads never pass through our servers.

The full component list, alternatives and licences are in [`docs/planning/tech-stack.csv`](../planning/tech-stack.csv).

## Roadmap

The product ships in six releases, each usable on its own, with paid launch at v1.0, roughly 10 to 12 months in for one developer.

| Release | Rough length (solo) | Delivers | Gate at the end |
| --- | --- | --- | --- |
| v0.1 Foundation | 3 to 4 months | Fast downloads, media, clips; Windows, macOS, 2 browsers | Private alpha |
| v0.5 Beta | About 3 months | Rules, subscriptions, Linux, plain-language errors | Public beta |
| v1.0 Launch | 4 to 5 months | Transcribe and search videos; send from phone; Pro tier | Paid launch |
| v2.0 Everywhere | 5 to 6 months | Server, NAS, web dashboard; metered data, polite mode | |
| v3.0 Intelligence | 3 to 4 months | Summaries, meaning search, plain-English commands | |
| v4.0 Ecosystem and Teams | Ongoing | Plugins, API, integrations; teams, SSO, admin console | |

Reaching v2.0 takes about 15 to 18 months solo, less with one or two more developers. Six further ideas are kept unscheduled until users ask for them. Every feature, with its user story and acceptance criteria, is in the [Feature Catalogue](feature-catalogue/README.md).

## How it makes money

Haulix is open core. The core downloader is free; Pro, Family, Team and Enterprise plans pay for automation, intelligence, remote use and team control. Safety, privacy and accessibility are never paywalled. Which features are Free or Pro is shown in each feature-catalogue entry; plan details and limits are kept outside this repository.

## Boundaries

Some lines are deliberate, either to stay legal and distributable or to keep the product focused.

**What we will not build:**

- **No DRM circumvention.** We won't download from Netflix, Spotify or other Widevine-protected streams. It's legally risky in most countries, and the media button simply doesn't appear on protected content.
- **No rebuilt engines.** We won't write our own site extractors or media tools; yt-dlp, gallery-dl and ffmpeg do that, and we keep them updated.
- **No adware, bundled offers or hidden tracking.** Trust is part of the product.

**Constraints we design around:**

- **Browser stores:** the Chrome Web Store bans YouTube downloader extensions, so our extensions hand links to the app rather than downloading media themselves.
- **Mobile stores:** iOS and Google Play restrict media downloaders, so the phone apps are remote controls; any on-device engine for Android would ship outside Google Play.
- **Terms of service:** downloading from some platforms breaches their terms. That's mainly a platform risk rather than a criminal one, but it's why we keep downloads off our servers wherever possible.
- **Cloud add-on:** downloads there do run on our servers, so it needs clear acceptable-use rules and a takedown process before launch.
- **Code signing:** download managers are often flagged by antivirus and SmartScreen, so signed, notarised builds are required from the first public release.

This isn't legal advice; the terms of service, privacy policy and takedown process need a lawyer's review before v1.0.

## Open decisions

- [x] **Engine language:** Rust.
- [x] **Open-source scope:** open core. The engine, browser extensions and self-hosted relay are open source under GPL-3.0; Pro features, our cloud services and the mobile apps are closed. Outside contributions will need a contributor licence agreement (CLA).
- [x] **Self-hosting and Pro:** remote features (web dashboard, sync, full mobile app) are free when self-hosted, and Pro only when using our relay.
- [x] **Download history:** added to v0.1.
- [x] **Product name:** Haulix (working name). Check domains and the CIPC, USPTO and EUIPO trademark registers before committing.
- [x] **Free limits:** recorded privately, outside this repository.
- [x] **Desktop vs cloud scope of the lifetime licence.** Marked in a new Pro scope column: 33 desktop features are covered by the lifetime licence; 7 cloud features need a subscription, or are free when self-hosted.
- [ ] **Prices.** Deferred: set before v1.0, after researching what comparable paid tools charge.

**Setup decisions**

- [x] **Engine process:** a separate background service that the desktop app starts; downloads continue when the window closes, and the same program later runs on servers.
- [x] **UI to engine:** the desktop UI uses the engine's own local REST and WebSocket API from day one, so the web dashboard and phone app reuse it.
- [x] **Repository layout:** one public repository (Cargo and pnpm workspaces) for the engine, desktop app and extension. A second, private repository holds Pro-only features, the cloud backend and mobile apps once they start (from v0.5).
- [x] **Visibility:** public from day one, with a CLA bot (such as CLA Assistant) enabled before the first outside contribution.

## Before we start

Most prerequisites are decisions and setup, not money. The first group blocks writing code; the second only needs to be done before the public beta.

**Before day 1**

- [x] Pick a working product name and check the domain and trademark (it goes into app IDs, the repo and store listings).
- [x] Choose Rust or Go for the engine.
- [x] Choose what is open source and under which licence.
- [x] Add download history to v0.1.
- [ ] Learn Rust basics: ownership, errors, async with Tokio (about 3 to 6 weeks part-time).
- [ ] Work through the Tauri 2 tutorial, including bundled helper programs (sidecars).
- [ ] Learn browser extension basics: Manifest V3 and native messaging.
- [ ] Spike 1: a Tauri app that runs bundled yt-dlp and shows its progress.
- [ ] Spike 2: a Chrome extension that sends a link to that app through native messaging.
- [ ] Spike 3: a Rust program that downloads one file in parallel segments and resumes after being killed.
- [ ] Set up a Windows PC and access to a Mac (a used Mac mini is enough).
- [ ] Install the Rust toolchain, Node.js, Git, VS Code with rust-analyzer, ffmpeg and yt-dlp.
- [ ] Create the GitHub repository with GitHub Actions builds.

**Before the public beta (v0.5)**

- [ ] Join the Apple Developer Program ($99 a year) for macOS notarisation.
- [ ] Get Windows code signing: an OV certificate or Azure Trusted Signing, if available to you.
- [ ] Register the domain and put up a simple website with downloads, docs and the privacy policy.
- [ ] Open Chrome Web Store ($5 once) and Firefox Add-ons developer accounts.
- [ ] Register a company before taking payments (in South Africa, a private company through CIPC).
- [ ] Draft terms of service, a privacy policy and a takedown contact, for a lawyer to review before v1.0.
- [ ] Confirm Paddle or Lemon Squeezy supports South African payouts.
- [ ] Recruit 10 to 20 alpha testers who match the personas.

Prices, self-hosting pricing, cloud hosting, mobile developer accounts and team features can wait until later releases.
