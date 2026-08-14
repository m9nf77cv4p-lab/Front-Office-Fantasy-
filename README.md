# Front Office Fantasy Sync

This repository is the persistent Sleeper data bridge for Front Office Fantasy.

## Source of truth

- Sleeper league: `1312046495905628160`
- Sleeper 2026 rookie draft: `1312046495926620160`
- User team/manager: `TJS2025`
- Format: 12-team dynasty, PPR, Superflex

This repository is isolated to Front Office Fantasy. The sync validates the exact league ID,
league name, season, dynasty type, and 12-team roster count before it writes anything. It must
not be used as a source for GameTime or Game of Inches.

## Data files

- `data/front-office-fantasy-master.json` is the project-facing master record.
- `data/raw/` preserves the current Sleeper responses used to build it.
- `data/history/previous.json` preserves the prior master snapshot when source data changes.
- `reports/league-snapshot.md` summarizes the league.
- `reports/tjs2025-team-report.md` summarizes the user's roster and draft capital.

The master record includes league settings, manager/team mapping, complete rosters, starters,
reserve and taxi assignments, current drafts and picks, traded picks, transactions, matchups,
player metadata, and the prior-league chain.

## Refresh behavior

The GitHub Action runs every five minutes and can also be started manually. It runs unit tests
first, validates the Sleeper league identity and dynasty format, then writes only when source
data changes.

Run locally with Python 3.11 or newer:

```bash
python -m unittest discover -s tests -v
python scripts/sync_front_office_fantasy.py
```
