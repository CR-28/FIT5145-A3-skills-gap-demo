# FIT5145 Assignment 3: Regional Skills-Gap Early-Warning System (Demonstration)

This repository hosts the data and R Markdown analysis supporting the Demonstration
section of a FIT5145 (Foundations of Data Science) Assignment 3 project: a regional
skills-gap early-warning system for Australian VET planning. It combines job vacancy
demand with training completion supply into a single directional "divergence score".

The demonstration uses **Electricians (ANZSCO 3411)** as a worked example to show
that the approach is feasible.

Author: Chinni Raja Ammela (Student ID 36309591), Master of Artificial Intelligence, Monash University

## Contents

| File | Description |
|---|---|
| `ChinniRaja_36309591_Assignment3.Rmd` | Full R Markdown analysis: data import, coverage check, harmonisation, divergence score, trend fitting and plots |
| `ChinniRaja_36309591_Assignment3.html` | Knitted output of the above |
| `data/internet_vacancies_anzsco4_occupations_jsa_remoteness_and_northern_australia_classification_-_august_2026.xlsx` | Jobs and Skills Australia Internet Vacancy Index (IVI) extract: monthly online job advertisements, by ANZSCO occupation and JSA Remoteness classification |
| `data/Total_VET_students_and_courses_2025.xlsx` | NCVER DataBuilder export: program completions for the Electrotechnology training package (UEE, UTE, UTL), by remoteness region and year, 2019 to 2025 |

## Original data sources

| Dataset | Source | Access |
|---|---|---|
| Internet Vacancy Index | Jobs and Skills Australia | Free, no login, direct Excel download: https://www.jobsandskills.gov.au/data/internet-vacancy-index |
| Total VET students and courses 2025: program completions | NCVER DataBuilder | Free, no login, interactive table export: https://www.ncver.edu.au/research-and-statistics/data/databuilder |

Both files in `data/` are the original, unmodified downloads or exports from these
sources. The NCVER file is a filtered export (Training package = Electrotechnology,
rows = Remoteness region, columns = Year), because DataBuilder does not provide a
static download URL for filtered views.

## Reproducing the analysis

1. Clone this repository, or download it as a ZIP.
2. Open `ChinniRaja_36309591_Assignment3.Rmd` in RStudio.
3. Install the required packages (one time):

```r
   install.packages(c("readxl", "dplyr", "tidyr", "lubridate", "ggplot2",
                      "knitr", "kableExtra", "rmarkdown"))
```

4. Knit the document (Ctrl+Shift+K, or Cmd+Shift+K on Mac).

The Rmd is self-contained. If there is no local `data/` folder, it downloads both
data files from this repository automatically, so it can be run on its own with an
internet connection.

## Summary of findings

The divergence score is vacancy growth minus completion growth, in percentage points.
For Electricians it shows a large positive spike in 2021 (vacancies rebounded faster
than training completions after the 2020 COVID dip), then falls and turns negative from
2024 onward in both Major City and Regional areas. This means completions have been
growing faster than vacancies. The fitted linear trend is negative in both regions
(about -6.4 and -6.6 percentage points per year), but with only six annual growth
observations per region neither slope is statistically significant (p = 0.52 and 0.31).
The result is a directional, feasibility-level indicator, not a forecast.

See `ChinniRaja_36309591_Assignment3.html` for the full tables, plots and caveats.

## Limitations

- VET completions are a proxy for labour supply, not a direct measure.
- The IVI counts online job advertisements (as a three-month moving average), not all vacancies.
- Seven NCVER remoteness classes are collapsed to two (Major City and Regional) to match the IVI.
- The Electrotechnology package covers more occupations than Electricians alone.
- Licence and attribution terms of the source data should be checked before redistribution.
