---
title: Gallery Increments
description: Historical increment records — one file per gallery app-count expansion.
generated_at: 2026-08-26
---

# Gallery Increments

Each expansion of the gallery app count produces a separate record file under this directory.

## Naming Convention

`YYYY-MM-DD-A-to-B.md` — UTC date plus the gallery size before and after the expansion.

Examples:

- `2026-06-03-500-to-550.md`
- `2026-07-15-550-to-600.md`

## Frontmatter Schema

| Field | Required | Description |
|---|---|---|
| `date` | yes | UTC date when the increment was recorded (YYYY-MM-DD). |
| `from` | yes | Gallery total before the expansion. |
| `to` | yes | Gallery total after the expansion. |
| `count` | yes | Number of apps added in this increment. |
| `commit` | no | Git commit hash that introduced the apps. |
| `commit_message` | no | Title of the commit that introduced the apps. |
| `source_csv` | no | Source manifest path. Defaults to `data/apps.csv`. |
| `pipeline_version` | no | Increment pipeline version that produced this file. |

## Records

| Date | Range | Added | File |
|------|------|-----:|------|
| 2026-08-26 | 1110 → 1160 | 50 | [2026-08-26-1110-to-1160.md](2026-08-26-1110-to-1160.md) |
| 2026-08-19 | 1060 → 1110 | 50 | [2026-08-19-1060-to-1110.md](2026-08-19-1060-to-1110.md) |
| 2026-08-12 | 1010 → 1060 | 50 | [2026-08-12-1010-to-1060.md](2026-08-12-1010-to-1060.md) |
| 2026-08-05 | 960 → 1010 | 50 | [2026-08-05-960-to-1010.md](2026-08-05-960-to-1010.md) |
| 2026-07-29 | 910 → 960 | 50 | [2026-07-29-910-to-960.md](2026-07-29-910-to-960.md) |
| 2026-07-22 | 860 → 910 | 50 | [2026-07-22-860-to-910.md](2026-07-22-860-to-910.md) |
| 2026-07-15 | 800 → 860 | 60 | [2026-07-15-800-to-860.md](2026-07-15-800-to-860.md) |
| 2026-07-08 | 750 → 800 | 50 | [2026-07-08-750-to-800.md](2026-07-08-750-to-800.md) |
| 2026-07-02 | 700 → 750 | 50 | [2026-07-02-700-to-750.md](2026-07-02-700-to-750.md) |
| 2026-06-28 | 650 → 700 | 50 | [2026-06-28-650-to-700.md](2026-06-28-650-to-700.md) |
| 2026-06-17 | 600 → 650 | 50 | [2026-06-17-600-to-650.md](2026-06-17-600-to-650.md) |
| 2026-06-12 | 550 → 600 | 50 | [2026-06-12-550-to-600.md](2026-06-12-550-to-600.md) |
| 2026-06-03 | 500 → 550 | 50 | [2026-06-03-500-to-550.md](2026-06-03-500-to-550.md) |

## How a New Increment Is Recorded

The generator detects new apps by diffing the current manifest against the previous app-id snapshot stored at `data/.app-snapshot.json` in the gallery repo. On every run:

1. Load the previous snapshot (or seed a baseline on the first run).
2. Compute the set of new app IDs in the current manifest.
3. If the diff is non-empty, write `YYYY-MM-DD-A-to-B.md` and prepend a row to this index.
4. Persist the new snapshot for the next run.

Rebuild runs (`RUN_MODE=rebuild`) skip increment generation and reset the snapshot to the current manifest.
