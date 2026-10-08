# Cybercrime Data Analysis

## Team members

| Team member         | Student ID |
| ------------------- | ---------- |
| Senay Teweldebrhan  | 9120588    |
| Juan Camilo Chirivi | 9115141    |
| Zeynep Ozdemir      | 9045142    |

## Project purpose

Analyze how police-reported cybercrime rates vary across Canadian metropolitan-area entries in 2025. Compare Ontario entries with entries elsewhere using the same variable: cybercrime incidents per 100,000 people.

## Workflow followed

**Set Up → Import → Inspect → Select and Clean → Check Duplicates → Summarize and Plot → Standardize and Normalize → Test Normality → Compare Variances → Compare Means → Interpret and Document**

| Step                      | What the notebook does                                                                                                                                  |
| ------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Set up                    | Checks required packages, imports libraries, and defines the year and significance level.                                                               |
| Import                    | Reads the embedded copy of the supplied CSV, or downloads the current official table when enabled.                                                      |
| Inspect                   | Examines the dataset's dimensions, columns, sample rows, missing values, and measurement types.                                                         |
| Select and clean          | Selects 2025 metropolitan-area rates; excludes overlapping geographic totals; converts rates to numeric values and removes missing or non-finite rates. |
| Check duplicates          | Checks for repeated area/year records and stops if any exist. No duplicates were found in the selected snapshot, so none were removed.                  |
| Summarize and plot        | Calculates descriptive statistics and draws overall and group histograms.                                                                               |
| Standardize and normalize | Calculates Z-scores and Min–Max values. These change scale without making the distribution normal.                                                      |
| Test normality            | Uses QQ-plots and Shapiro–Wilk tests for all entries and each comparison group.                                                                         |
| Compare variances         | Applies a two-sided F-test and a supplementary median-centered Levene test.                                                                             |
| Compare means             | Calculates Welch's two-sample t-score, p-value, and confidence interval.                                                                                |
| Interpret and document    | Explains the findings, assumptions, limitations, and presentation plan.                                                                                 |

The notebook uses one source, so no merge is performed. Inspection is a one-time data-quality assessment rather than ongoing monitoring. Process configuration occurs during setup; statistical data standardization occurs later during the Z-score calculations.

## Data source

Statistics Canada, Table **35-10-0002-01**: _Police-reported cybercrime, number of incidents and rate per 100,000 population, Canada, provinces, territories, Census Metropolitan Areas and Canadian Forces Military Police_.

- [Official table and notes](https://www150.statcan.gc.ca/t1/tbl1/en/tv.action?pid=3510000201)
- [Complete English CSV download](https://www150.statcan.gc.ca/n1/tbl/csv/35100002-eng.zip)
- [Dataset DOI](https://doi.org/10.25318/3510000201-eng)

The supplied CSV contains 1,356 rows covering 2014–2025. The analysis selects 41 metropolitan-area entries in 2025: 15 in Ontario and 26 elsewhere. Ottawa–Gatineau's Ontario and Quebec parts remain separate entries as reported. The selected snapshot contains no missing rates or duplicate area/year records.

## How to run

1. Open `Cybercrime_Data_Analysis.ipynb` in VS Code or Jupyter.
2. Select a Python environment and run the cells from top to bottom.
3. The setup cell installs missing analysis packages. Internet access is required if packages need installation.
4. Leave `DOWNLOAD_FRESH = False` to reproduce the supplied snapshot. Its data is embedded in the notebook; a separate CSV is not required.
5. Set `DOWNLOAD_FRESH = True` to download the current official table. Internet access is required. If the data changes, rerun all cells and revise the fixed Markdown interpretations.

The analysis uses pandas, NumPy, Matplotlib, and SciPy. The significance level is `ALPHA = 0.05`.

## Notebook contents

- Team information, research question, setup, data source, and cleaning explanations.
- Descriptive statistics and histograms.
- Z-score standardization, Min–Max normalization, and a 100-word Z-score interpretation.
- QQ-plots, Shapiro–Wilk results, and a 100-word normality interpretation.
- F-test results, supplementary Levene results, and a 50-word variance interpretation.
- Welch t-score results and a 50-word interpretation, plus an expanded 100-word interpretation for slide 35's activity.
- A 100-word overall p-value assessment.
- Findings, limitations, and a five-minute notebook presentation guide.

## Main findings

The overall distribution is right-skewed. Shapiro–Wilk rejects normality for the overall entries and the elsewhere group at the 0.05 level. The F-test does not reject equal variances (`F ≈ 0.688`, `p ≈ 0.470`), but non-normality limits its interpretation. Welch's t-test does not reject equal group means (`t ≈ -0.137`, `p ≈ 0.892`). Ontario's average is approximately 295.04 incidents per 100,000 people, compared with 302.58 elsewhere.

## Interpretation limits

These are police-reported area statistics, not all cybercrime incidents or individual risk estimates. The area averages are unweighted and are not national population-weighted rates. The entries are not independent random samples, and spatial relationships may affect inference. Treat the statistical tests as an exploratory classroom exercise. Failure to reject a hypothesis does not prove equality; high Z-scores do not prove data errors or establish causes.

## Before presenting or submitting

Replace the team-name and ID placeholders. Review the complete assigned Unit 1 and Unit 3 slide ranges; only four slide images were supplied when this notebook was prepared. Every member should understand the filters, plots, formulas, p-values, and limitations, rehearse the five-minute presentation, and check their classroom projector connection.
