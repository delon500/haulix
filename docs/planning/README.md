# Planning data

Planning data as plain CSV, so it can be read, diffed and searched. Open the files in any spreadsheet app. These files are the source of truth; the original spreadsheet is no longer used.

| File | What's in it |
| --- | --- |
| [features.csv](features.csv) | All 130 features: `ID` (e.g. F-008, as used in the feature catalogue and everywhere else), `Sheet row` (original spreadsheet order only; never use it to refer to a feature), category, version, tier, status, differentiator and Pro scope (Desktop, or Cloud: free when self-hosted) |
| [releases.csv](releases.csv) | What each release adds, by platform |
| [platforms.csv](platforms.csv) | Every platform: role, minimum version, architecture, distribution, first release |
| [tech-stack.csv](tech-stack.csv) | Every component: recommended choice, alternative, reason, first release, licence |

Update the `Status` column in `features.csv` as work progresses (Planned, In progress, Done, Cut).
