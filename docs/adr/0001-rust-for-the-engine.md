# 0001. Rust for the engine

**Status:** Accepted, 2026-10-18

## Context

The engine is a long-running network service that parses untrusted data from the internet and must ship as a small binary on Windows, macOS, Linux and ARM servers.

## Decision

Write the engine in Rust, using Tokio for async work and Axum for the local API.

## Consequences

Memory safety without a garbage collector, C++-level speed, single binaries per platform, and easy embedding of whisper.cpp, SQLite and torrent libraries. It also matches Tauri. The cost is a learning curve; Go was the faster-to-ship alternative.
