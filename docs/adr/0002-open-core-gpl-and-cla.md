# 0002. Open core under GPL-3.0, with a CLA

**Status:** Accepted, 2026-10-18

## Context

Trust is a selling point against adware-laden free tools, but Pro features and cloud services need to stay closed to fund the product.

## Decision

The engine, desktop app and browser extension are open source under GPL-3.0-only. Pro-only features, the cloud backend and the mobile apps live in a separate private repository. Every outside contributor signs a contributor licence agreement (CLA) through a GitHub bot.

## Consequences

GPL stops others from closing a fork of the engine. Because the maintainer holds the copyright, closed editions remain possible; the CLA keeps that true once outside code is merged. The CLA text needs legal review before the first outside contribution is merged.
