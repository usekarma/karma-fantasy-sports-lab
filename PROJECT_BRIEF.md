# Karma Fantasy Sports Lab — Project Brief

## Business problem

Fantasy football predictions are often evaluated using intuition, selective examples, or unverified claims. We want a reproducible way to assess whether historical NFL data supports useful fantasy predictions.

## Desired outcome

Establish an evidence-based research experiment that tests fantasy-football prediction hypotheses against historical outcomes and simple baselines. The experiment also tests whether the Agent Business Solution Template generalizes beyond infrastructure and IoT.

## Users / stakeholders

- Primary user and business owner: UseKarma project owner
- Technical owner: designated by the human owner before implementation
- Downstream consumers: reviewers of reproducible research evidence

## Current process

No validated fantasy prediction pipeline or baseline has been established for this experiment. Start with data discovery and an evaluation plan, not an assumed model or operational product.

## Constraints

- Security/compliance: use lawful, appropriately licensed data; document data rights and provenance; protect credentials and private information.
- Cost: no spending or paid services without prior human authorization.
- Latency/SLA: none for the offline research phase.
- Data volume: bounded historical samples for the first experiment.
- Deployment environment: offline/local analysis only initially; no AWS or live deployment.
- Existing systems: preserve template verification, evidence, and human decision boundaries.

## Inputs

Potential inputs include historical NFL statistics, schedules, player availability, and published fantasy scoring rules. Dataset selection and coverage are research tasks, not established facts.

## Outputs

- Dataset inventory with provenance and usage restrictions
- A narrowly scoped, falsifiable hypothesis
- A chronological offline evaluation plan with a no-leakage rule
- Baselines and metrics for measuring error or predictive performance
- Reproducibility notes and evidence for a human go/no-go decision

## Failure expectations

Treat missing data, scoring changes, leakage, licensing uncertainty, and nonreproducible results as explicit evaluation limitations. Do not silently fill gaps or report favorable results without baseline comparisons.

## Out of scope

- Wagering, paid contests, monetary transactions, or automated contest entry
- Automation against fantasy or gambling platforms
- Live recommendations or claiming profitability
- Production infrastructure or deployment
- Implementation before review of the initial research plan

## Success metrics

- Every proposed dataset has documented provenance and permitted use.
- The initial evaluation has a specified time-aware split and leakage safeguards.
- At least one simple baseline and defined metrics accompany the proposed hypothesis.
- Research can be reproduced from documented inputs and procedures.
- A human records a decision to iterate, stop, or proceed.

## Discovery and experiment

- Hypothesis and smallest stakeholder demo: research historical data availability, identify one testable prediction question, and propose a small offline retrospective evaluation.
- Current baseline and measurable target: to be established before modeling.
- Assumptions with validation owner and deadline: document after source discovery; no arbitrary deadline.
- Prototype decision: human-owned decision after reviewing evidence.
- Data classification and permitted synthetic fixtures: public/licensed historical data or clearly labeled synthetic data; validate source rights first.
- Production owner and release decision maker: human owner; no production phase authorized.

Use `specs/` for subsequent contracts and `docs/prototype-review.md` for observed feedback. Until explicitly authorized, this phase is planning only: no coding, spending, deployments, external side effects, or autonomous Dot work.
