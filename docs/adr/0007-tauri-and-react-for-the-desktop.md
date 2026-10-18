# 0007. Tauri 2 with React for the desktop app

**Status:** Accepted, 2026-10-18

## Context

The desktop UI must be light (against IDM's small footprint) and reusable as the web dashboard.

## Decision

Use Tauri 2 with React, TypeScript and Tailwind CSS. Flutter was the main alternative.

## Consequences

Installers of around 10 MB instead of Electron's 100+ MB, a Rust-native shell, and one web UI for desktop and dashboard. Rendering differs slightly between each OS's WebView, especially on Linux, so the UI needs testing on all three.
