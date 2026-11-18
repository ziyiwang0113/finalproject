# BST260 Final Project Proposal

**To:** BST260 Teaching Team, Fall 2026

## 1. Project Overview

This project aims to apply statistical and computational methods
introduced in BST260 to investigate two public health research questions
using publicly available datasets. The project will emphasize
reproducible data processing, exploratory data analysis, statistical
inference, and interpretation of uncertainty.

Two analyses will be conducted. The first will investigate the
association between body mass index (BMI) and systolic blood pressure
using the National Health and Nutrition Examination Survey (NHANES). The
second will examine seasonal patterns in reported waterborne disease
outbreaks in the United States using CDC outbreak surveillance data.

The analyses will be presented as two reproducible Quarto vignettes
within an R package and published through a pkgdown website.

## 2. Vignette 1: Association Between BMI and Systolic Blood Pressure

### 2.1 Research Question

How is body mass index (BMI) associated with systolic blood pressure
among U.S. adults, after adjusting for age and sex?

### 2.2 Data Source and Study Population

The analysis will use publicly available NHANES data provided through
the R `NHANES` package.

The study population will consist of adults aged 20 years or older with
available BMI and systolic blood pressure measurements. The unit of
analysis will be an individual survey participant.

### 2.3 Variables

- **Exposure:** BMI, treated as a continuous variable.
- **Outcome:** Systolic blood pressure, measured in mmHg and treated as
  a continuous variable.
- **Potential confounders:** Age and sex, selected based on their
  potential relationships with both BMI and blood pressure.

Additional covariates may be considered based on subject-matter
justification and data availability.

### 2.4 Proposed Statistical Analysis

1.  Conduct exploratory data analysis to summarize the distributions of
    BMI, systolic blood pressure, and relevant demographic variables.
2.  Visualize the association between BMI and systolic blood pressure
    using scatterplots and fitted regression lines.
3.  Fit a simple linear regression model to estimate the unadjusted
    association between BMI and blood pressure.
4.  Fit a multivariable linear regression model adjusting for age and
    sex, and compare the estimated BMI coefficients across models.
5.  Report regression coefficients, 95% confidence intervals, and
    relevant model diagnostics.
6.  Examine potential nonlinearity and discuss the limitations of
    interpreting observational associations.

Missing values will be identified and summarized before modeling. A
complete-case analysis may be used as an initial approach, with
potential selection bias discussed. The need for survey weights and
other survey-design adjustments will be evaluated according to the
selected NHANES data and the intended scope of inference.

## 3. Vignette 2: Seasonal Patterns of Waterborne Disease Outbreaks in the United States

### 3.1 Research Question

Do reported waterborne disease outbreaks in the United States exhibit
seasonal patterns, and are these patterns consistent across different
historical periods?

### 3.2 Data Source and Study Population

The analysis will use CDC outbreak surveillance data available through
the `waterborne` dataset in the `finalproject` R package.

The dataset includes reports from 1971 through 2023. Preliminary
exploration identified 3,106 records with `primary_mode == "Water"`.

The original unit of observation is an outbreak report. For the primary
statistical analysis, outbreak reports will be aggregated into
year-month counts.

### 3.3 Variables

- **Primary exposure:** Calendar month, represented as a categorical
  variable with 12 levels.
- **Secondary exposure:** Summer (June-August) versus non-summer months.
- **Outcome:** Number of reported waterborne disease outbreaks per
  year-month, treated as count data.
- **Potential adjustment variables:** Calendar year and observation time
  (number of days per month).

Historical periods will also be considered for stratified analyses to
investigate whether seasonal patterns are consistent over time.

### 3.4 Preliminary Data Exploration

Initial data exploration identified 3,106 waterborne outbreak records
between 1971 and 2023, with no missing year or month values detected in
the selected records.

Of these records, 1,487 (approximately 47.9%) occurred during June,
July, and August. July had the highest number of reported outbreaks,
with 624 records.

Annual outbreak counts varied substantially across the study period,
suggesting that temporal variation in reporting should be considered
when interpreting seasonal patterns.

These observations are descriptive and do not establish statistical
significance or differences in population-level infection risk.

### 3.5 Proposed Statistical Analysis

1.  Transform the original nested-list data into a tidy dataset and
    retain records classified as waterborne outbreaks.
2.  Summarize and visualize monthly and annual outbreak counts.
3.  Construct a year-month count dataset and examine the empirical
    distribution of outbreak counts, including the mean, variance, and
    frequency of zero counts.
4.  Explore the Poisson distribution as a candidate model for count data
    and assess its assumptions.
5.  Use a chi-square goodness-of-fit test to assess whether the observed
    monthly distribution differs from the expected distribution under a
    constant daily reporting frequency, accounting for differences in
    month length.
6.  Estimate the ratio of reported outbreak frequencies between summer
    and non-summer periods, together with a 95% confidence interval.
7.  Compare seasonal patterns across historical periods and consider
    year-level bootstrap resampling to assess uncertainty.

If appropriate, Poisson regression adjusting for calendar year and
observation time may be explored as an extension.

### 3.6 Missing Data and Limitations

The analysis will distinguish between fields that are missing because
they are not applicable to non-waterborne events and fields that are
missing within the selected waterborne records.

The completeness and validity of year and month variables will be
verified before analysis. Year-month combinations with no recorded
outbreaks will be examined carefully before being interpreted as zero
counts.

Potential limitations include changes in surveillance practices,
reporting completeness, dependence among reported events, and
differences in exposure opportunities across seasons.

Therefore, findings will be interpreted as patterns in **reported
outbreak frequency**, rather than causal effects of season or direct
estimates of individual infection risk.

## 4. Expected Deliverables

The final project will include:

1.  A valid and installable R package containing reusable
    data-processing and analysis functions.
2.  Two reproducible Quarto vignettes documenting data provenance,
    descriptive statistics, statistical methods, results, and
    limitations.
3.  Visualizations and statistical summaries illustrating the main
    findings.
4.  A publicly accessible pkgdown website hosted through GitHub Pages.

The overall goal is to demonstrate how methods learned in BST260 can be
applied to real public health data, while clearly communicating
statistical uncertainty, analytical assumptions, and limitations.
