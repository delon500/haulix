# Planning data

Plain CSV exports of the planning spreadsheet, so they can be read, diffed and searched. Open them in any spreadsheet app.

| File | What's in it |
| --- | --- |
| [features.csv](features.csv) | All 130 features: category, version, tier, status, differentiator, `Doc #` (number in the feature catalogue) and Pro scope (Desktop, or Cloud: free when self-hosted) |
| [releases.csv](releases.csv) | What each release adds, by platform |
| [platforms.csv](platforms.csv) | Every platform: role, minimum version, architecture, distribution, first release |
| [tech-stack.csv](tech-stack.csv) | Every component: recommended choice, alternative, reason, first release, licence |

Update the `Status` column in `features.csv` as work progresses (Planned, In progress, Done, Cut).
