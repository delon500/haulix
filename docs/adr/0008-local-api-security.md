# 0008. Securing the local API

**Status:** Accepted, 2026-10-18

## Context

Any website a user visits can send requests to `localhost`, so a local API is an attack surface.

## Decision

The engine listens on `127.0.0.1` only; rejects requests whose Host header isn't the local machine (blocking DNS rebinding); and lets only the Haulix app's origins read responses (CORS allow-list). A per-install access token will be required before the API can start, change or delete downloads.

## Consequences

The basics are in place and tested from the first commit. The token is a known gap to close before v0.1's write endpoints.
