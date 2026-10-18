# 0005. One public repository from day one

**Status:** Accepted, 2026-10-18

## Context

A solo developer benefits from one place for code, issues and CI; building in public attracts early interest and trust.

## Decision

Use one public repository with Cargo and pnpm workspaces for the engine, desktop app and extension. Closed parts get a separate private repository when they start (from v0.5).

## Consequences

Shared types and one CI pipeline. Early, rough work is visible, and contributions can arrive immediately, so the CLA bot is on from the first commit.
