# Diabetes Risk Factor Analysis

## Purpose
This project explores risk factors associated with a diabetes diagnosis using a patient level dataset with nine clinical and demographic variables. It was prepared so that the data science team at another clinical site can obtain the project files, understand the workflow, execute the notebook independently, and reproduce the results without contacting the original author.

## What this analysis does
The notebook loads and validates the dataset, corrects a dataset specific missing data issue, produces descriptive statistics and visualizations (a Sankey diagram and a ridgeline plot), computes a correlation matrix, runs two inferential statistical tests (an independent samples t test and a chi square test of independence), frames the problem as a formal statistical and machine learning problem, and confirms that all steps involving random sampling are reproducible.

## Dataset
`Example_Dataset_Diabetes.csv`, included in this repository. It contains 768 patient records with the following columns: `Pregnancies`, `Glucose`, `D_BP`, `Skin_Thickness`, `Insulin`, `BMI`, `Pedigree`, `Age`, and `Outcome` (1 indicates a diabetes diagnosis, 0 indicates no diagnosis).

This dataset is provided for methodological demonstration. Results describe patterns within this dataset only and should not be treated as validated clinical findings without further review.

**Known data quality issue:** several columns use a literal 0 as a placeholder for missing data rather than a true measurement. The notebook detects and corrects this in the Data Validation and Data Preparation sections. Do not use the raw CSV for any purpose without that correction.

## Required software and libraries
* Python 3.10 or later
* `pandas`, `numpy`, `matplotlib`, `seaborn`, `scipy`, `plotly`

Two ways to set this up, see Setup and Environment in the notebook for full detail:
* **Option 1 (manual):** `pip install -r requirements-lock.txt`, a fully pinned dependency tree verified by actually running this notebook end to end.
* **Option 2 (automatic):** run the "Automatic dependency check" cell near the top of the notebook; it installs anything missing for you. Recommended for Google Colab, where most of these packages are already preinstalled.

## Running the notebook
1. Clone this repository: `git clone https://github.com/<org>/<repo>.git`, then `cd` into it. This gives you the notebook, `Example_Dataset_Diabetes.csv`, `requirements.txt`, and `requirements-lock.txt` all in one place, run the setup commands below from inside this folder.
2. Follow Setup and Environment in the notebook (Option 1 or Option 2) to install dependencies.
3. Open the notebook and run all cells top to bottom (e.g. "Restart session and run all" in Jupyter or Google Colab).
4. The notebook validates its own inputs as it runs. If a cell raises an assertion error, stop and follow the message before continuing.

## Expected outputs
* Printed data validation checks confirming dataset shape, column names, and disguised missing values.
* Descriptive statistics, two histograms, a Sankey diagram (BMI category to diagnosis, colored by outcome), and a ridgeline plot (Glucose distribution by diagnosis), plus a correlation heatmap.
* Results of a t test comparing Glucose by diagnosis, and a chi square test comparing BMI category by diagnosis, each with a written interpretation.
* A reproducibility check confirming a random sample and a bootstrap estimate return the same values on every run.
* A Results section and a Conclusions section summarizing findings and limitations.

## Dataset requirements
The notebook expects exactly the columns listed above, in that order, with no missing header row. If your copy of the dataset differs, the notebook's built in checks will raise a clear error rather than silently producing incorrect results.

## Assumptions and limitations
* Missing data was imputed using outcome group specific medians, a transparent but simple approach. Consider a more advanced imputation method before any higher stakes use of these results.
* The two statistical tests used here each examine one relationship at a time and do not account for interactions between predictors.
* The Sankey diagram uses `plotly`, which renders as an interactive widget, not a static image. It may not display in viewers without JavaScript support (e.g. some GitHub previews).
* This dataset is for methodological demonstration. Any adaptation of this workflow to real patient data from our health system requires confirming IRB approval and data governance requirements first.

## Programming environment used for validation
This notebook was executed end to end, twice, from a clean state, confirming identical outputs both times.
