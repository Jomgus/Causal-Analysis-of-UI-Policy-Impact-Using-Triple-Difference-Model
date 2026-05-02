# Causal Analysis of UI Policy Impact Using a Triple-Difference Model

This repository contains a capstone analysis of the 2021 early termination of federal pandemic unemployment benefits.

The main question is whether lower-wage workers benefited as much as higher-wage workers after some states ended benefits early.

## Main conclusion

Across the core specifications preserved in the main analysis path, the evidence supports rejecting the idea that lower-wage workers benefited just as much as higher-wage workers.

The preferred state-level triple-difference estimates are negative in the main specification, and the direction remains negative across the core timing and trend checks collected in the evidence folders.

## Repository structure

- `analysis/`
  Main notebooks and reference notebooks.
- `evidence/`
  Saved tables, summaries, and diagnostics organized by analytical role.
- `figures/`
  Figures used to present the treatment setup, subgroup gap, placebo contrast, event-study pattern, and leave-one-state-out stability.
- `scripts/`
  Reusable scripts for robustness checks, corrected slice models, county-side supporting checks, and saved-result extraction.
- `data/`
  Raw and processed inputs used by the analysis.

## Analysis layout

- `analysis/main/SignificanceHolzerStyle.ipynb`
  Primary notebook for the preferred triple-difference results and supporting diagnostics.
- `analysis/reference/baseline_model.ipynb`
  Baseline reference notebook.
- `analysis/supporting/county_hdpulse_covariates.ipynb`
  Supporting county-side notebook.

## Evidence layout

- `evidence/main_claim/`
  Core saved outputs for the main claim, including robustness tables and corrected slice estimates.
- `evidence/county_support/`
  County-side supporting outputs.
- `evidence/event_study/`
  Saved event-study and subgroup diagnostics tied to the state-level analysis.

## Recommended review path

1. `analysis/main/SignificanceHolzerStyle.ipynb`
2. `evidence/main_claim/summary.md`
3. `evidence/main_claim/robustness_checks.csv`
4. `evidence/main_claim/slice_ddd_corrected.csv`
5. `evidence/county_support/summary.md`

## Data used by the main workflow

Tracked inputs include:

- `data/raw/COVID - State - Daily.csv`
- `data/raw/Employment - State - Weekly.csv`
- `data/raw/OxCGRT_US_latest.csv`
- `data/raw/Policy Milestones - State.csv`
- `data/processed/processed_panel_2018.csv`
- `data/processed/processed_panel_2021.csv`

The main notebook and several scripts also use CPS-based analysis inputs that are not fully tracked in standard Git history.

## Minimal setup

```bash
python3 -m venv .venv
source .venv/bin/activate
python3 -m pip install -r requirements.txt
```

## Scope

- The main causal argument is carried by the state-level CPS triple-difference design.
- County-side materials are included as supporting evidence rather than the primary identification strategy.
- The most direct reading of the project should come from the primary notebook and the `evidence/main_claim/` outputs.
