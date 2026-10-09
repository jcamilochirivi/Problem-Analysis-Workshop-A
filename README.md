# Group 2 — Problem Analysis Workshop A

**Course:** PROG8431 — Data Analysis, Mathematics, Algorithms and Modeling  
**Project:** Police-Reported Cybercrime in Canada  
**Notebook:** `Workshop A.ipynb`

## Team members

| Team member         | Student ID |
| ------------------- | ---------- |
| Senay Teweldebrhan  | 9120588    |
| Juan Camilo Chirivi | 9115141    |
| Zeynep Ozdemir      | 9045142    |

## Project overview

This project examines police-reported cybercrime rates across Canadian metropolitan areas in 2025. It investigates the distribution of rates and compares their variances and means between Ontario metropolitan areas and metropolitan areas elsewhere in Canada.

The analyzed variable is **cybercrime incidents per 100,000 people**. Rates allow comparisons between areas with different population sizes. Each selected area receives equal weight in the statistical analysis.

## Data source

The data comes from **Statistics Canada, Table 35-10-0002-01**, _Police-reported cybercrime, number of incidents and rate per 100,000 population, Canada, provinces, territories, Census Metropolitan Areas and Canadian Forces Military Police_.

- [Official table and documentation](https://www150.statcan.gc.ca/t1/tbl1/en/tv.action?pid=3510000201)
- [Download the complete English CSV ZIP](https://www150.statcan.gc.ca/n1/tbl/csv/35100002-eng.zip)

The supplied `35100002.csv` contains 1,356 rows covering 2014–2025. It includes incident counts and rates, which are analyzed separately rather than mixed into one distribution. The notebook reads the CSV locally; it does not download data automatically.

`35100002_MetaData.csv`, if included with the downloaded table, provides documentation and is not a second observation dataset to merge.

## File organization

Place these files in your project folder:

| Path                         | Purpose                                                                |
| ---------------------------- | ---------------------------------------------------------------------- |
| `Workshop A.ipynb`           | Analysis code, charts, statistical tests, and written interpretations. |
| `README.md`                  | Project overview and instructions.                                     |
| `data/35100002.csv`          | Required Statistics Canada dataset.                                    |
| `data/35100002_MetaData.csv` | Optional source documentation.                                         |

The notebook also checks for the CSV in the parent folder's `data` directory or beside the notebook.

## Installation and execution

Use Python with VS Code's Python and Jupyter extensions, or a Jupyter environment.

Install the required packages in the Python environment used by your notebook:

```bash
python -m pip install numpy pandas matplotlib scipy ipython ipykernel
```

1. Download and extract the source CSV, or use the supplied `35100002.csv`.
2. Place the CSV in the project's `data` folder.
3. Open `Workshop A.ipynb` and select the Python environment containing the packages.
4. Run all cells from top to bottom.

The setup cell imports libraries and configures output formatting. It does not install packages. The analysis year is controlled by `ANALYSIS_YEAR = 2025`; the significance level is `ALPHA = 0.05`. Changing the year requires rerunning the analysis and reviewing the written interpretations.

## Workflow followed

**Set Up → Import Local CSV → Inspect → Select and Clean → Check Duplicates → Histograms → QQ-Plots and Shapiro–Wilk → F-Test → Welch t-Test → Interpret and Document**

| Step                   | Implementation                                                                                                                             |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| Set up                 | Import libraries and configure the year, significance level, tables, and charts.                                                           |
| Import                 | Locate and read the local CSV.                                                                                                             |
| Inspect                | Display sample rows, available years, measurements, missing values, and exact duplicate counts.                                            |
| Select and clean       | Convert year and values to numeric types; select 2025 rates and five-digit metropolitan codes; exclude provincial parts and missing rates. |
| Check duplicates       | Assert that no selected metropolitan area appears twice; duplicates are not automatically removed.                                         |
| Histograms             | Plot the overall distribution and both regional groups using common bins.                                                                  |
| Test normality         | Create QQ-plots and calculate Shapiro–Wilk statistics and p-values; display a p-value chart.                                               |
| Compare variances      | Calculate a two-sided F-test and supplement it with median-centered Levene's test.                                                         |
| Compare means          | Calculate Welch's t-statistic manually, verify it with SciPy, and report a confidence interval.                                            |
| Interpret and document | Include the normality, variance, mean-comparison, and overall p-value interpretations.                                                     |

Only one observation dataset is used, so no merge is performed. The selected data contains **39 entries: 14 Ontario and 25 elsewhere**. The Ontario and Quebec parts of Ottawa–Gatineau are excluded by the provincial-part filter.

## Main findings

For the supplied 2025 dataset:

| Measure                                      | Result                                                                                           |
| -------------------------------------------- | ------------------------------------------------------------------------------------------------ |
| Ontario mean rate                            | Approximately 303.26 incidents per 100,000 people.                                               |
| Other Canadian metropolitan areas' mean rate | Approximately 303.79 incidents per 100,000 people.                                               |
| Normality assessment                         | The overall and other-Canada distributions reject normality at 0.05; Ontario does not reject it. |
| F-test                                       | `F ≈ 0.683`, `p ≈ 0.479`; do not reject equal variances.                                         |
| Welch t-test                                 | `t ≈ -0.009`, `p ≈ 0.993`; do not reject equal means.                                            |

The distributions are right-skewed overall. The non-normal other-Canada group limits the reliability of the classical F-test. Welch's method allows unequal variances, but it does not eliminate all assumptions or limitations.

## Interpretation limits

These figures describe **police-reported cybercrime**, not every cybercrime that occurred. Reporting practices and local conditions can affect observed rates. The averages are unweighted across metropolitan areas and are not national population-weighted rates. Areas may be spatially related and are not a random sample. Interpret the tests as exploratory, rather than causal or definitive population-wide findings. A nonsignificant p-value does not prove equal means or variances.

## Slide 35 activity and presentation

The notebook adapts the food-price activity to cybercrime, covering distributions, normality testing, mean comparisons, and p-value interpretation. It contains a 100-word normality interpretation, 50-word F-test and t-score summaries, and a 100-word p-value reflection.

The slide-35 table mentions Z-scores, but the current notebook does **not** calculate them or include the requested 100-word Z-score interpretation. Min–Max normalization is also not implemented.
