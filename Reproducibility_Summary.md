# Reproducibility Summary

The original notebook had several reproducibility problems: a hardcoded, machine-specific data path with a filename mismatch that would fail on any other computer; no package versions; an unseeded random sample and bootstrap estimate that produced different results on every run; missing data disguised as literal 0 values that a standard null check would not detect; and generic, unlabeled statistical notation not tied to this dataset's actual variables.

I fixed each of these: replaced the hardcoded path with a relative path, with a public GitHub URL as an automatic fallback if the local file is missing; pinned exact package versions in `requirements-lock.txt`, verified by an actual install; set one fixed random seed reused everywhere sampling occurs; added explicit checks for disguised missing values and corrected them with outcome-group-specific median imputation before any analysis; and rewrote the statistical and machine learning notation using this dataset's real variable names and dimensions.

I verified reproducibility by rebuilding the notebook from scratch and executing it end to end twice, independently, then programmatically comparing every text output between runs; they were identical.

# Reproducibility Changes Log

A full list of changes made to improve this notebook's reproducibility, documentation, and correctness.

## Environment & Dependencies
- Documented and pinned exact package versions (`requirements.txt`, then a fuller `requirements-lock.txt` covering dependencies too)
- Added a fixed random seed (`random.seed` + `np.random.seed`) reused everywhere sampling occurs, so results don't change between runs
- Provided two setup paths: manual (`pip install -r requirements-lock.txt`) and an automatic dependency-check-and-install cell, for different environments (local vs. Colab)
- Added the missing "clone the repository" step to Setup, previously assumed but never stated

## Data Loading & Provenance
- Replaced a hardcoded, machine-specific absolute path (a Google Colab `/content/...` path) with a relative path
- Added a fallback: if the local CSV isn't found, the notebook downloads it from a public GitHub URL, printing which source was actually used
- Added explicit dataset provenance documentation: source, columns, and appropriate scope of use (methodological demonstration, not real patient data)

## Data Validation & Preparation
- Added explicit checks for disguised missing data (literal `0` values in five columns) that a standard `.isna()` check would miss entirely
- Added checks for duplicate rows, valid `Outcome` values, and plausible `Age` values
- Added a full Data Preparation section (didn't exist originally): converts disguised zeros to true missing values, then imputes using outcome-group-specific medians, with the limitation of that choice documented
- Added a derived `BMI_Category` feature used later in analysis

## Statistical Notation & Analysis
- Fixed broken LaTeX rendering for the mean/standard deviation formulas
- Replaced generic template notation (`var1`, `var2`, `target`) with this dataset's actual variables and dimensions ($n=768$, $p=8$)
- Added a second inferential test (chi-square test of independence) alongside the existing t-test, each with formal notation, description, results, and dataset-specific interpretation
- Added a full pairwise correlation matrix and heatmap with interpretation

## Visualizations
- Added two required bivariate visualizations: a Sankey diagram (BMI category to diagnosis) and a ridgeline plot (Glucose distribution by diagnosis)

## Documentation & Organization
- Reorganized the notebook into the required 10-section structure
- Added markdown throughout explaining each section's purpose, required setup actions, and how to interpret outputs

## Verification
- Rebuilt and executed the notebook end to end, twice, independently, and programmatically compared every output; they matched
