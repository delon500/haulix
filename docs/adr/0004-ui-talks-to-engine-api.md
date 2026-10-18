# 0004. Every client uses the engine's local API

**Status:** Accepted, 2026-10-18

## Context

The desktop app could call the engine through Tauri's built-in messaging, but the web dashboard and phone app (v1.0, v2.0) cannot.

## Decision

From day one the desktop UI talks to the engine only through its local REST and WebSocket API (`/api/v1`). Types live in `haulix-core` and are mirrored in TypeScript until they are generated from Rust.

## Consequences

The web dashboard can reuse the desktop UI unchanged, and remote access is the same API over the encrypted relay. The cost is having to secure a local API from the start (see 0008).
