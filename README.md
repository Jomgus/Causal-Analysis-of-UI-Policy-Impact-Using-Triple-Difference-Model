# Causal Analysis of UI Policy Impact Using a Triple-Difference Model

This repository contains the cleaned analysis package for a capstone on the 2021 early termination of federal pandemic unemployment benefits.

The central question is whether lower-wage workers benefited as much as higher-wage workers after some states ended benefits early.

## Main conclusion

Across the core specifications kept in this repo, the evidence supports rejecting the idea that lower-wage workers benefited just as much as higher-wage workers.

The preferred state-level triple-difference estimates are negative in the main analysis path, and the sign remains negative across the core timing and trend checks retained here.

## What is kept here

This version of the repo keeps only the files needed to understand and defend the final analysis:

- `notebooks/SignificanceHolzerStyle.ipynb`
  Main notebook for the preferred DDD results and supporting diagnostics.
- `baseline_model.ipynb`
  Baseline reference notebook.
- `scripts/`
  Scripts used for the robustness suite, corrected slice checks, county-side auxiliary checks, and result extraction.
- `data/outputs/main_robustness_suite/`
  Core robustness outputs for the main claim.
- `data/outputs/county_aside/`
  County-side supporting outputs.
- `notebooks/figure_1_treatment_map.svg`
- `notebooks/figure_4_the_gap.svg`
- `notebooks/figure_4_ddd_vs_placebo.svg`
- `notebooks/ddd_state_event_study_2021_lowwage_vs_other-wage.png`
- `notebooks/LOO_Robustness_Check.png`

## Main files for review

If someone only opens a few files, the shortest path is:

1. `notebooks/SignificanceHolzerStyle.ipynb`
2. `data/outputs/main_robustness_suite/summary.md`
3. `data/outputs/main_robustness_suite/robustness_checks.csv`
4. `data/outputs/main_robustness_suite/slice_ddd_corrected.csv`
5. `data/outputs/county_aside/summary.md`

## Data used by the kept workflow

Tracked inputs in this repo include:

- `data/raw/COVID - State - Daily.csv`
- `data/raw/Employment - State - Weekly.csv`
- `data/raw/OxCGRT_US_latest.csv`
- `data/raw/Policy Milestones - State.csv`
- `data/processed/processed_panel_2018.csv`
- `data/processed/processed_panel_2021.csv`

The main notebook and some scripts also expect CPS-based analysis inputs that are not all tracked in normal Git history.

## Minimal setup

```bash
python3 -m venv .venv
source .venv/bin/activate
python3 -m pip install -r requirements.txt
```

## Notes

- This repo is intentionally narrower than the full working directory used during the project.
- Exploratory notebook history, temporary deployment files, and presentation-only app code were removed from the public version.
- The retained files are the ones most directly tied to the conclusions presented in the final project.
