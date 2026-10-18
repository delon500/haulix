# 0003. The engine runs as a separate background service

**Status:** Accepted, 2026-10-18

## Context

Downloads must keep running when the window is closed, and the same engine must later run headless on a NAS, Raspberry Pi or server (v2.0).

## Decision

The engine is its own program, `haulixd`, which the desktop app starts (as a Tauri sidecar) rather than code running inside the app's process.

## Consequences

One engine binary serves every deployment. The app can quit or crash without stopping downloads. It adds process management work (starting, stopping, updating the sidecar), which spike 1 covers.
