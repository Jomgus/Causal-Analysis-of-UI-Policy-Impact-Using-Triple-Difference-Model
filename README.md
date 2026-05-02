![UTA Data Science Logo](UTA-DataScience-Logo.png)

# Causal Analysis of UI Policy Impact Using a Triple-Difference Model

## Business Problem / Motivation

In 2021, a subset of U.S. states ended federal pandemic unemployment benefits before the national September expiration. Supporters argued that ending benefits early would push unemployed workers back into jobs faster. This project studies whether that effect was the same across wage groups.

The focus is on a narrower question than a general policy average: did lower-wage workers benefit as much as higher-wage workers after early termination?

## Project Overview

This repository contains a state-level and individual-level causal analysis built around Current Population Survey microdata and supporting policy and COVID context files.

- Goal: estimate whether early UI termination had a different effect on low-wage workers than on higher-wage workers
- Baseline: two-way fixed-effects reference model on aggregate employment data
- Main model: triple-difference model on CPS microdata
- Main result: the preferred triple-difference coefficient is negative, indicating weaker post-policy job-finding outcomes for lower-wage workers relative to the comparison group

## Data

### Sources

- Current Population Survey (CPS) microdata from IPUMS CPS: https://cps.ipums.org/cps/
- COVID case data: tracked in `data/raw/COVID - State - Daily.csv`
- Employment tracker data: tracked in `data/raw/Employment - State - Weekly.csv`
- Oxford COVID-19 Government Response Tracker: tracked in `data/raw/OxCGRT_US_latest.csv`
- Policy timing file: tracked in `data/raw/Policy Milestones - State.csv`

### Type

- Individual-level monthly labor-market observations from CPS
- State-level policy timing and COVID controls
- County-level supporting covariates for auxiliary checks

### Size

Tracked inputs used by the main workflow include:

- `data/raw/COVID - State - Daily.csv`
- `data/raw/Employment - State - Weekly.csv`
- `data/raw/OxCGRT_US_latest.csv`
- `data/raw/Policy Milestones - State.csv`
- `data/processed/processed_panel_2018.csv`
- `data/processed/processed_panel_2021.csv`

The main notebook and scripts also use CPS-based analysis inputs that are not fully tracked in normal Git history.

### Key features

- `STATEFIP`: state identifier used for treatment assignment
- `MONTH`: policy timing and pre/post construction
- `AGE`: age-based subgroup restrictions
- `EDUC`: education-based subgroup restrictions
- `IND`: industry-based low-wage classification
- `EMPSTAT`: employment status used to construct job-finding outcomes
- `LNKFW1MWT`: survey weights used in the CPS regressions

## Data Preprocessing

Main preprocessing steps:

- construct treatment timing from the policy milestones file
- identify unemployed workers and link adjacent monthly observations
- derive the `found_job` transition outcome
- classify low-wage workers using industry-based definitions
- merge monthly COVID and stringency controls
- build subgroup-restricted slices such as prime-age, no-college, and prime-age without college

County-side preprocessing is handled separately for supporting analysis:

- build the county panel with `prepare_panel_for_twfe.py`
- merge HDPulse-style county covariates
- standardize county-level supporting variables for interaction checks

## Exploratory Data Analysis (EDA)

Key visuals are kept in `figures/`:

- `figures/figure_1_treatment_map.svg`
  Treatment and control states under the early-exit design
- `figures/figure_4_the_gap.svg`
  Main gap visual used to show relative subgroup movement
- `figures/figure_4_ddd_vs_placebo.svg`
  Main estimate versus placebo comparison
- `figures/ddd_state_event_study_2021_lowwage_vs_other-wage.png`
  Event-study view of subgroup divergence

These figures are used to show the treatment setup, the subgroup gap, and the timing pattern around the policy cutoff.

## Modeling Approach

### Baseline model

`analysis/reference/baseline_model.ipynb`

This notebook provides a two-way fixed-effects reference model on aggregate employment outcomes. It serves as a baseline comparison rather than the main evidentiary result.

### Advanced model

`analysis/main/SignificanceHolzerStyle.ipynb`

This notebook contains the main triple-difference specification. The core term is the interaction between:

- treatment state
- post-policy period
- low-wage subgroup

That setup isolates whether the post-policy change differed for lower-wage workers relative to higher-wage workers and relative to control states.

### Supporting models

- `scripts/main_claim_robustness_suite.py`
  Core timing, trend, placebo, and low-wage-definition checks
- `scripts/slice_ddd_corrected.py`
  Subgroup slice estimates such as prime-age and no-college
- `scripts/holzer_style_robustness.py`
  Additional event-study and subgroup diagnostics
- `scripts/county_aside_heterogeneity.py`
  County-side supporting checks

## Model Training

This project is an econometric workflow rather than a tuned predictive pipeline.

- Tools: `pandas`, `numpy`, `statsmodels`, Jupyter notebooks
- Estimation: weighted least squares / fixed-effects-style regression workflow
- Inference: clustered standard errors at the state level where applicable
- Design choices: state-level treatment timing, subgroup construction, placebo checks, and robustness grids

There are no hyperparameters in the usual machine-learning sense. The key modeling choices are specification choices: treatment timing, subgroup definition, controls, and sample restrictions.

## Results

### Main reported quantities

For this project, the important reported quantities are:

- coefficient size and sign
- standard error
- p-value
- sample size
- stability across robustness checks
- placebo results

These were used because the project is testing a causal contrast, not maximizing prediction accuracy.

### Main result

The preferred triple-difference estimate is negative in the primary analysis path, indicating weaker job-finding outcomes for lower-wage workers after early termination relative to the comparison group.

### Model comparison

- Baseline aggregate TWFE model: weaker and less informative for subgroup heterogeneity
- Main CPS triple-difference model: primary result
- Slice-specific DDD results: show where the negative effect is strongest
- Placebo and trend checks: used to test whether the result is likely to be spurious

Key saved outputs:

- `evidence/main_claim/robustness_checks.csv`
- `evidence/main_claim/slice_ddd_corrected.csv`
- `evidence/main_claim/summary.md`
- `evidence/event_study/summary.md`

## Model Interpretation

This project uses interpretation through robustness structure rather than feature-importance methods from predictive modeling.

Interpretation layers include:

- subgroup slice comparisons in `evidence/main_claim/subgroup_dd_slices.csv`
- placebo checks in `evidence/main_claim/robustness_checks.csv`
- leave-one-state-out stability shown in `figures/LOO_Robustness_Check.png`
- event-study outputs in `evidence/event_study/`
- county-side supporting interactions in `evidence/county_support/`

These materials are used to answer:

- whether the sign changes across core specifications
- whether the result survives timing changes
- whether the effect is concentrated in particular slices
- whether placebo designs stay near zero

## Key Insights

- The aggregate baseline is not the strongest way to study this question.
- The CPS-based triple-difference design is better suited to subgroup heterogeneity.
- The negative differential effect is strongest in several core subgroup slices, especially prime-age and no-college combinations.
- Placebo checks do not show a competing significant effect in the opposite direction.

## Conclusion

The retained analysis path supports the conclusion that lower-wage workers did not benefit as much as higher-wage workers after early UI termination.

The main result is not carried by a single artifact. It is supported by the primary notebook, the corrected slice outputs, the main robustness suite, and the placebo structure.

## Future Work

- pin a final environment for exact reproduction
- standardize every remaining path assumption around repo-relative inputs
- export final publication-ready tables directly from the scripts
- narrow the county-side evidence further if it is kept in a public-facing version

## How to Run

### 1. Set up the environment

```bash
python3 -m venv .venv
source .venv/bin/activate
python3 -m pip install -r requirements.txt
```

### 2. Build the county panel if needed

```bash
python3 prepare_panel_for_twfe.py
```

### 3. Run the main analysis

Open:

- `analysis/main/SignificanceHolzerStyle.ipynb`

### 4. Run the supporting scripts

```bash
python3 scripts/main_claim_robustness_suite.py
python3 scripts/slice_ddd_corrected.py
python3 scripts/holzer_style_robustness.py
python3 scripts/county_aside_heterogeneity.py
```

## Repository Structure Explanation

- `analysis/`
  Contains the notebooks used for the main, baseline, and supporting analytical paths.
- `analysis/main/`
  Primary notebook for the final claim.
- `analysis/reference/`
  Baseline comparison notebook.
- `analysis/supporting/`
  Supporting county-side notebook.
- `evidence/main_claim/`
  Main robustness tables, corrected slices, and summary text used to defend the central claim.
- `evidence/event_study/`
  Saved event-study and subgroup diagnostics.
- `evidence/county_support/`
  County-side supporting outputs.
- `figures/`
  Presentation and inspection figures used in the write-up.
- `scripts/`
  Reusable scripts for robustness checks and supporting analysis generation.
- `data/raw/`
  Raw policy, COVID, employment, and CPS-related inputs available in the repo.
- `data/processed/`
  Processed panel files used by the retained workflow.

## Requirements

Install dependencies with:

```bash
pip install -r requirements.txt
```
