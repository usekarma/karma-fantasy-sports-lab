# EXP-001 — Architect discovery: weekly NFL fantasy baseline

**Status:** PROPOSED / human review required  
**Date:** 2026-10-15  
**Owner:** UseKarma project owner (human)  
**Tracking issue:** [#2](https://github.com/usekarma/karma-fantasy-sports-lab/issues/2)

## Decision requested

Approve, revise, or reject the *research design* below. This document is not an authorization to implement, download datasets, pay for services, merge code, run autonomous agents, or deploy anything. The existing `specs/` examples and their acceptance mappings remain untouched.

## 1. Business question and falsifiable hypothesis

Can a rolling average of a wide receiver's **three most recent completed, actually played NFL games** predict the receiver's **next played game's PPR fantasy points** more accurately than simply using the last played game's points?

- **Candidate method:** mean of fantasy points over the previous three eligible games.
- **Baseline:** last played game's fantasy points (persistence).
- **Primary metric:** mean absolute error (MAE) on exactly the same eligible player-game predictions.
- **Secondary metrics:** RMSE, bias, sample size, coverage, seasonal/weekly breakdown, and per-player distribution of errors.
- **Proposed success criterion:** candidate MAE at least 5% below baseline on a held-out 2025 season, *and* no material data-leakage or source-rights issues. Treat a smaller gain or inconclusive evidence as a learning outcome, not as success.
- **Uncertainty:** neither method nor result has been executed or verified.

This is an intentionally modest forecasting experiment, not a claim of competitive or profitable fantasy recommendations.

## 2. Candidate source and data-rights checklist

| Candidate | What is documented | What is still unverified |
| --- | --- | --- |
| [nflverse/nflverse-data](https://github.com/nflverse/nflverse-data) release assets | Repository documents NFL data releases distributed in CSV/parquet and accessible via release links; its [LICENSE.md](https://github.com/nflverse/nflverse-data/blob/main/LICENSE.md) contains Creative Commons Attribution 4.0 text. | Confirm the selected **player_stats** release asset, years, schema, source attribution, whether its underlying third-party inputs have restrictions that are not cured by the repository-level license, and any redistribution limits. |
| [nflreadpy](https://nflreadpy.nflverse.com/) | Current nflverse Python access package; [nfl_data_py](https://github.com/nflverse/nfl_data_py) states it is deprecated in favor of nflreadpy. | Confirm exact supported function/season options and hash or version pinning before implementation. |

**Rights gate:** The presence of a CC BY 4.0 license in the data-hosting repository is evidence of the *repository's published license*, not a blanket legal determination for every upstream statistic or usage. Do not ingest data until selected assets, terms, required attribution, and any relevant third-party rights have been reviewed. Do not commit bulk source data to the repo.

**Evidence as of this review:** only public source documentation and repository contracts were inspected; no file-level column audit, data download, or backtest was run.

## 3. Proposed evaluation protocol

1. **Scope:** one position (WR), standard full-PPR scoring initially, regular season only, historical completed games; exclude the ongoing 2026 season. Scoring proposal: 1 point/reception; 0.1 point/rushing or receiving yard; 6 points/rushing or receiving TD; -2 points/lost fumble. Confirm all required components are available in the chosen asset before locking this formula; record any departures explicitly.
2. **Data contract:** identify each observation by player identifier, season, NFL week/game, and source snapshot. Validate uniqueness, stable identifiers, units, completeness, data revisions, and availability of completed-game records. Flag rather than silently repair invalid/ambiguous rows.
3. **Time-aware split:** develop methodology using 2021–2023; evaluate design choices on 2024; hold 2025 untouched for the final comparison. These windows are proposed and depend on verified dataset coverage. Never select methods using 2025 results.
4. **Prediction time:** produce forecast before the predicted game's kickoff using only **earlier completed games and information available at the decision cutoff**. No same-week final stats, season-to-date aggregates containing future games, later roster statuses, hindsight player filtering, or revised observations that violate as-of availability.
5. **Eligibility:** both methods predict the *same* next played games, with at least three historical eligible played games. This conditional sample is **not** a full-week lineup forecast. Record exclusions, injury/nonappearance cases, and byes separately; do not mistake omitted games for zero points. Report coverage and selection bias.
6. **Reproducibility:** before execution, freeze asset URL/version/hash, source timestamp, selection logic, scoring rules, code revision, environment, and output artifacts. Record rows excluded and why.
7. **Evaluation:** compare per-row paired errors; show global MAE, RMSE, bias and season/week slices, plus uncertainty estimates using blocks or resampling that respect player/game temporal dependence. Explicitly report any methodology changes made after looking at holdout results as exploratory, not confirmatory.

## 4. Proposed acceptance evidence (not yet executable)

- **EXP-001-AC-01:** source asset documented, selected fields verified, rights/attribution reviewed.
- **EXP-001-AC-02:** PPR scoring formula and invalid/missing-input behavior fixed with boundary examples.
- **EXP-001-AC-03:** chronological leakage tests demonstrate that future games cannot influence earlier predictions.
- **EXP-001-AC-04:** baseline and candidate evaluate identical eligible cases, with exclusion counts.
- **EXP-001-AC-05:** 2025 holdout error metrics and provenance are reproducible from a pinned dataset and code revision.
- **EXP-001-AC-06:** reviewer independently records findings, limitations, and human go/revise/stop decision.

These are **research acceptance IDs**, not replacements for the template's worked-example `specs/acceptance.json`. At implementation time, create the domain spec, real tests, and test-node mappings in a separately reviewed PR.

## 5. Risks, failure rules, and the smallest review/demo

- **Source rights uncertain:** stop before ingesting; document findings and obtain human decision.
- **Missing/incorrect weekly stats or identifiers:** fail input validation; do not fabricate observations.
- **Scoring fields absent:** revise and re-approve scoring, or reject the asset.
- **Temporal leakage:** reject results and fix the evaluation before reporting predictive performance.
- **Coverage bias from predicting only played games:** keep conclusions explicitly conditional, and do not claim full fantasy lineup value.
- **Weak/no improvement:** record negative result; do not redefine success after examining holdout.
- **External side effects:** prohibited at this stage.

**Smallest human review today:** read this proposal and decide whether to permit a subsequent, explicitly scoped **dataset inventory / schema and rights verification** step. A future demo would be a reproducible table of baseline versus candidate errors on a held-out sample, with source links, excluded-row counts, and no contest automation.

## 6. Template process status

| Stage | State |
| --- | --- |
| Discover / Architect | This proposal prepared for human review |
| Specify | Pending source/schema/rights decisions |
| Prototype / Builder | Not authorized |
| Verifier / Reviewer / Security / Operations | No domain execution evidence yet |
| Release / production | Out of scope |

No implementation, real-data analysis, dataset downloads, payments, wagering, Dot tasks, AWS activity, or merge was performed in this step.
