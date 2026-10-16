# EXP-001 — Source rights and schema desk review

**Status:** Documentation-only desk review; upstream-rights gate **OPEN / not cleared**  
**Reviewed:** 2026-10-15  
**Related:** [EXP-001 Architect plan](exp-001-architect-discovery.md), [Issue #2](https://github.com/usekarma/karma-fantasy-sports-lab/issues/2)

## Purpose and boundary

Identify one candidate historical, weekly NFL player-stat dataset and distinguish what public documentation establishes from what requires file-level inspection or rights confirmation. This note **does not approve ingestion or implementation**. No data was downloaded, imported, processed, or redistributed. No modeling or tests were run; no AWS, Dot, contests, spending, or deployment were involved.

## Candidate and published evidence

| Question | Publicly documented evidence | Assessment |
| --- | --- | --- |
| Source | [nflverse-data](https://github.com/nflverse/nflverse-data) publishes automated data releases, including [Player Summary Stats / `stats_player`](https://github.com/nflverse/nflverse-data/releases/tag/stats_player). | Candidate identified; **no particular asset has been acquired or pinned**. |
| Weekly granularity | The `stats_player` release is described as having player stats at different summary levels; the public [nflreadpy API](https://nflreadpy.nflverse.com/api/load_functions/) documents `load_player_stats(seasons=[...], summary_level="week")`. | Weekly acquisition path **documented**, not executed. |
| Date coverage | The intended research windows are **2021–2023 development, 2024 validation, 2025 untouched holdout**; `stats_player_week_<season>.csv` is a documented release naming pattern (see linked upstream issue #101). | **Presence, completeness, revision history and stability of each exact file remain unchecked**. Exclude 2026 from this retrospective design. |
| Identifiers/required fields | The public [nflreadr player-stats data dictionary](https://nflreadr.nflverse.com/articles/dictionary_player_stats.html) describes player ID, position, season, week, season type, and offensive statistics. [The load function docs](https://nflreadr.nflverse.com/reference/load_player_stats.html) include example columns such as `player_id`, `season`, `week`, `season_type`, and `game_id`. | **Schema documentation only**. Actual asset columns, types, missingness and all required PPR scoring inputs have **not** been inspected. |
| Published license | The repository publishes a [Creative Commons Attribution 4.0 International license](https://github.com/nflverse/nflverse-data/blob/main/LICENSE.md). CC BY 4.0 permits licensed uses subject to its terms, including attribution and notices when sharing. | **Published repository license verified**, but not proof that every upstream input/field is licensed by its original rights holder. |
| Upstream rights | [nflverse-data issue #101](https://github.com/nflverse/nflverse-data/issues/101), opened 2026-09-12, directly asks whether `stats_player` fields/years and commercial reuse are covered, and about upstream rights/attribution. It was closed **not planned** on 2026-10-02, without an answer visible in that thread. | **Unresolved**; closure is not permission, a denial, or a legal ruling. Distinguish noncommercial offline research from any future paid or redistributed use, but do not assume that makes all upstream terms irrelevant. |

## Licensing assessment (not legal advice)

1. Record the published `nflverse-data` CC BY 4.0 terms, with links and any required credit, link, and modification notice if data or adapted material is shared.
2. A repository-level CC BY license cannot by itself establish authority over every underlying NFL statistic, collection, or third-party-supplied field. The visible issue #101 did **not** resolve that question.
3. For this first lab, propose **private/offline research only**, with no redistribution of bulk source data, public statistical dashboards, paid product, contest integration, or marketing implying an NFL endorsement.
4. **Gate remains open:** before ingestion, an owner should decide whether the documented rights and the precise proposed use are sufficient, or obtain a more definitive upstream-rights review. A paid/public product requires fresh evaluation rather than inheriting a research approval.

## Minimum file/schema verification needed before EXP-001-AC-01 can pass

This checklist is **proposed only**; not an executed audit:

- Specify the exact `stats_player` weekly 2021–2025 release asset URLs, time retrieved, checksums, update timestamps, provenance and published notices. Avoid mutable `latest` without saved hashes.
- Inspect exact asset headers, row counts and nulls across each year for `player_id`, `position`, `season`, `week`, `season_type`, `game_id` (if present), `receptions`, `receiving_yards`, `receiving_tds`, `rushing_yards`, `rushing_tds`, and the appropriate **lost-fumble** field(s). Do not assume documented columns all occur or have identical meanings in every file.
- Verify whether position `WR` is snapshot-correct, how games played and nonappearances are represented, and whether games/rows are uniquely identified by `player_id` + `game_id` or a documented alternative.
- Confirm full-PPR scoring and missing-input behavior against verified fields (including touchdown, lost-fumble, and possible two-point-conversion handling); change and reapprove scoring if unavailable.
- Determine the as-of availability of historical stats and any retroactive revisions, so a historical 'before kickoff' predictor cannot use information published later.
- Preserve a license/source inventory and owner sign-off **before** downloading data; do not commit bulk raw data to GitHub.

## Recommendation / next human decision

**Proceed only with further rights clarification or a narrowly approved, documented file/header inventory. Do not authorize modeling yet.** The next owner decision is whether a private offline schema inspection is acceptable given the unresolved third-party rights, or whether the lab should switch to a different source or synthetic fixtures first.

Research acceptance status:

- **EXP-001-AC-01 (source/fields/rights): NOT MET** — source and repository license documented; asset-level schema and upstream permissions unresolved.
- **EXP-001-AC-02 through AC-06: NOT EXECUTED** — no scoring, leakage, model, holdout, or human-outcome verification performed.

### Sources checked

- https://github.com/nflverse/nflverse-data
- https://github.com/nflverse/nflverse-data/releases/tag/stats_player
- https://github.com/nflverse/nflverse-data/blob/main/LICENSE.md
- https://github.com/nflverse/nflverse-data/issues/101
- https://nflreadpy.nflverse.com/api/load_functions/
- https://nflreadr.nflverse.com/articles/dictionary_player_stats.html
- https://nflreadr.nflverse.com/reference/load_player_stats.html
