# EXP-001 — NFL data-source options and decision gate

**Status:** Architect desk review only; no data rights or ingestion approval  
**Reviewed:** October 15, 2026  
**Related:** [Issue #2](https://github.com/usekarma/karma-fantasy-sports-lab/issues/2), [Architect design](exp-001-architect-discovery.md), [source-rights review](exp-001-source-rights-and-schema.md)

## Recommendation

Retain **nflverse `stats_player` weekly statistics** as the leading *technical candidate*, not an approved data source. Continue seeking clarity on rights and permitted use for the exact data assets. Keep real-data ingestion, modeling, and lineup optimization blocked. If rights cannot be established, ask the owner to authorize a separate synthetic-only exercise to test the scoring, prediction-evaluation, and verification workflow without NFL data.

**Scope:** wide receivers (WR), regular-season completed games, proposed 2021–2023 development / 2024 validation / 2025 untouched holdout, full-PPR subject to actual field availability. No 2026 season data.

## Public evidence and alternatives

| Candidate | Evidence | Limitations and disposition |
| --- | --- | --- |
| **nflverse-data weekly player stats** | [`stats_player` release](https://github.com/nflverse/nflverse-data/releases/tag/stats_player); [CC BY 4.0 repository license](https://github.com/nflverse/nflverse-data/blob/main/LICENSE.md); [nflreadpy loading documentation](https://nflreadpy.nflverse.com/api/load_functions/) | **Best documented technical fit, but not cleared.** The repository-level license does not prove every upstream rights holder authorized all use of underlying fields. [Specific upstream licensing question #101](https://github.com/nflverse/nflverse-data/issues/101) closed without visible clarification; closure is neither permission nor denial. No exact file versions, completeness or schemas inspected. |
| **FantasyPros weekly historical scores** | [Historical weekly PPR scores](https://www.fantasypros.com/nfl/reports/leaders/ppr.php); [terms of use](https://www.fantasypros.com/legal/) | Human-readable scoring reference. Site terms restrict copying/reusing material beyond specified permissions. **Not authorized as a bulk training or validation feed** merely because scores are publicly viewable. |
| **Sports Reference / Pro-Football-Reference** | [Terms](https://www.sports-reference.com/termsofuse.html); [data use page](https://www.sports-reference.com/data_use.html) | Terms expressly restrict use of content to train/support AI/ML prediction and creation of competing datasets, as well as certain automated access. **Do not ingest into the proposed ML lab without express permission.** |
| **Synthetic, locally authored fixtures** | Generated from a declared scoring contract; no external player records | Best fallback for testing engineering contracts, time-leakage safeguards, and agent workflow, but **cannot validate real-NFL predictive value**. Any coding/build must still be separately authorized. |

This is a research inventory, **not legal advice or an exhaustive rights determination**. Verify any new provider's exact license, upstream rights, conditions and provenance before use.

## Proposed next actions — within Architect authority

1. **Rights clarification (desk review):** collect explicit asset-specific license statements, attribution requirements, data-provider terms and provenance for nflverse `stats_player` 2021–2025. Seek an authoritative response when public documentation remains ambiguous; do not treat nonresponse as permission.
2. **Schema inspection plan (proposal only):** specify a minimal private/offline inspection of exact year-specific asset headers and metadata. Before any actual retrieval, require a recorded owner decision that the use is acceptable given identified rights; list exact URLs and purpose.
3. **If approved separately**, the bounded inspection should capture retrieval date, version/hash, row count, column names/types, nulls, year/week coverage, identifier consistency and PPR input fields. No bulk raw data commit, public redisplay, training, contests or cloud operations. This PR **does not** authorize or perform that inspection.
4. **If rights are not clear**, return for owner decision: continue clarification, choose a newly vetted source, or authorize a synthetic-only engineering experiment. Never quietly substitute a source or broaden use.

## Explicit owner decision gate

- **Option A — further rights review (recommended now):** continue documentation-only work and seek source/asset-specific clarification. No download or build.
- **Option B — consider a bounded private/offline asset inventory:** only after the owner explicitly accepts the documented rights assessment and inspection scope. This document is *not* the authorization.
- **Option C — synthetic-only first:** separately approve a limited implementation using wholly generated data, with no empirical NFL predictive-performance claims.
- **Option D — stop or change source.**

**Acceptance status:** EXP-001-AC-01 remains **NOT MET** until actual chosen source permissions and required fields have been verified. EXP-001-AC-02 through AC-06 remain **NOT EXECUTED**. All implementation is on hold.

## Execution statement

Documentation-only work. No dataset downloaded, code changed, model trained, benchmark run, AWS activity, paid services, fantasy or wagering integration, deployment, autonomous Dot delegation, or merge performed. Draft for human review only.
