# Causal-analysis-of-bank-disintermediation on financial stability using propensity score matching

README
======

Project: Banking Panel Data Analysis, Propensity Score Matching and Logistic Regression

1. OVERVIEW
-----------
This project contains Python code for analysing panel data for banks. The script includes:

- Data loading from Excel files.
- Panel-data sorting by bank and quarter.
- Construction of lagged banking variables.
- Logistic regression models.
- Propensity score estimation and matching.
- Average Treatment Effect on the Treated (ATT) analysis.
- Covariate balance diagnostics.
- Robustness checks.
- Multicollinearity and model diagnostic checks.
- Trend analysis and descriptive statistics by bank type.
- Visualisation of banking and profitability indicators.

The notebook/script appears to use datasets covering 25 banks and analyses variables related to bank performance, non-performing assets, advances, income and industry lending.

2. INPUT DATA
-------------
The code loads Excel datasets with names including:

- 25 Banks Data (2).xlsx
- python data set.xlsx
- Python_25 Banks (3) (2).xlsx

Some file paths are written for Google Colab, for example:

/content/python data set.xlsx

Before running the code locally, these paths should be changed to the correct location of the Excel files.

3. MAIN DATA STRUCTURE
----------------------
The analysis uses panel data where observations are organised by:

- bankid
- quarter

The code sorts observations using bankid and quarter before constructing lagged variables.

Important variables appearing in the script include:

Outcome / treatment-related variables:
- y
- rcorp
- treatment
- Ind_Loan

Profitability variables:
- roa
- roe

Non-performing asset variables:
- inpa
- snpa
- anpa
- rnpa

Banking and lending variables:
- gross advances
- gross_advances
- igva
- sgva
- agva
- industry loan share to gross advanves

Income and other variables:
- nii
- cf

Classification variables:
- type of bank
- bank_type
- bankid

The exact availability and definitions of these variables should be checked in the corresponding Excel dataset.

4. REQUIRED PYTHON PACKAGES
---------------------------
The code uses the following libraries:

pandas
numpy
matplotlib
seaborn
statsmodels
scikit-learn


5. DATA PREPARATION
-------------------
The main data-preparation steps are:

1. Load the Excel dataset using pandas.
2. Sort observations by bankid and quarter.
3. Convert quarterly data to an appropriate quarterly/date format where required.
4. Rename variables containing spaces for use in regression formulas.
5. Construct lagged explanatory variables using groupby(bankid).shift(1).
6. Create a year variable from the quarter variable where time effects are required.
7. Remove or otherwise handle missing observations.

Example lagged variables created in the script include:

- L_inpa
- L_snpa
- L_anpa
- L_rnpa
- L_gross_advances
- L_igva
- L_sgva
- L_agva

6. PROPENSITY SCORE MATCHING (PSM)
---------------------------------
The script contains a propensity score matching workflow.

Main steps include:

Step 1: Define treatment and control groups
The code constructs or uses a binary treatment variable. In one section, rcorp is used as the basis for defining treatment status.

Step 2: Estimate propensity scores
A logistic regression model is used to estimate the probability of receiving treatment based on selected covariates.

Step 3: Common support
The code checks the overlap between propensity scores of treated and control observations and trims observations outside the overlapping region.

Step 4: Nearest-neighbour matching
Nearest-neighbour matching is implemented. The script also contains references to matching with a caliper.

Step 5: ATT estimation
The matched sample is used to estimate treatment effects for profitability outcomes including:

- ROE
- ROA

Step 6: Bootstrap uncertainty
The code includes a bootstrap procedure for ATT estimation by repeatedly resampling and rematching observations.

Step 7: Covariate balance
Balance is assessed using Standardized Mean Differences (SMD) before and after matching.

Step 8: Robustness checks
The script includes or discusses:

- Radius matching.
- Alternative logit specifications.
- Sensitivity to hidden confounders / Rosenbaum-bounds-style analysis.

7. LOGISTIC REGRESSION
----------------------
The project contains several logistic regression specifications using statsmodels.

An example specification in the script is:

y ~ gross_advances
    + L_inpa
    + L_rnpa
    + nii
    + L_igva



8. MODEL DIAGNOSTICS
--------------------
The script contains diagnostic checks including:

- Dependent-variable checks.
- Missing-value checks.
- Multicollinearity analysis using Variance Inflation Factors (VIF).
- Correlation matrix analysis.
- Class-balance checks.
- ROC curve and Area Under the Curve (AUC).
- Common-support checks.
- Kernel-density visualisation.
- Pseudo R-squared.
- Odds ratios.
- Marginal effects.

9. DESCRIPTIVE STATISTICS
-------------------------
The code calculates descriptive statistics by type of bank.

Statistics include:

- Count
- Mean
- Median
- Standard deviation
- Minimum
- Maximum

Variables analysed in descriptive-statistics sections include:

- ROA
- ROE
- NII
- CF

Results are saved to Excel files such as:

Descriptive_Statistics_BankType.xlsx

10. TREND ANALYSIS
------------------
The script generates quarterly trends by bank type for several indicators.

These include:

- Average ROA over time.
- Average ROE over time.
- Average ANPA over time.
- Average RNPA over time.
- Non-Interest Income (NII) trends.
- Average industry loan share to gross advances.

The quarter variable is converted using pandas PeriodIndex where the quarter is stored in a format such as YYYYQx.

11. BANK-LEVEL VISUALISATION
----------------------------
The project also plots indicators for individual banks.

Examples include:

- RNPA trends for foreign banks.
- ROA trends for individual banks.
- NII trends for individual banks.
- Rcorp trends over time for each bank.

Matplotlib and seaborn are used for these visualisations.

12. OUTPUT FILES
---------------
Depending on which sections are run, the code can produce:

- Regression summaries.
- Propensity scores.
- Odds-ratio tables.
- ATT estimates.
- Balance statistics.
- Diagnostic plots.
- Trend graphs.
- Descriptive-statistics Excel files.



13. HOW TO RUN
-------------
A. Using Google Colab

1. Upload the Python script or open the notebook equivalent.
2. Upload the required Excel dataset(s).
3. Update the file paths if necessary.
4. Install any missing packages.
5. Run the cells/sections sequentially.

B. Running locally

1. Install Python.
2. Install the required packages.
3. Place the Excel datasets in the project directory.
4. Update the file paths in the script.
5. Run:




