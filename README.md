# FirmPanelPropensityScoreMatching
A collection of code to implement a custom approach to PSA. Match each firm on a year-by-year basis, within the same industry.

The given example pertains to a sample of European firms, where one might be interested to measure the effect of family ownership (treatment is family firm status) on the outcome variable (in this case, financial sustainability). The script will match treatment and control observations 1:1, and export the matched sample. It also implements some tests of matching quality and measures the total treatment effects.

This implementation of PSA assumes analysis of a firm-year structured panel, with firm characteristics (covariates) which are used to estimate propensity scores. It assumes that there exists a binary indicator of the treatment vs. control group. Moreover, it assumes the presence of industry and country categories (fixed effects).

One must declare in the script constants section the details of the data set structure to identify which variables disclose this infomration.

  * DATA_DIR - Location relative to script where to find the input dataset
  * YEAR_VAR - Variable to represent the panel year dimension
  * INDUSTRY_VAR - Variable to represent industry categories (e.g., ff 12 - https://mba.tuck.dartmouth.edu/pages/faculty/ken.french/Data_Library/det_12_ind_port.html)
  * COUNTRY_VAR - Variable to represent country categories
  * PANEL_ID_VAR - Variable to represent firm id
  * PANEL_NAME_VAR - Variable to represent firm name
  * OUTCOME_VAR - Variable of interest (i.e., we expect to see a significant treatment effect on this variable). Performance, sustainability, investment...
  * TREATMENT_VAR - Variable to split treatment and control groups. Must be binary! In this example, "ff" represents a famly firm classification dummy
  * COVARIATES - List of variables used to estimate propensity scores
  * ADDITIONAL_VARIABLES - Other variables which will not be used in the matching procedure but will be exported in matched sample output
  * PSCORE_MATHOD - Indication of probit or logit estimation of pscores
  * CALIPER - Specification of maximum difference between a given treatment and control observation to allow a match
  * FE_SUFFIX - Suffix added to industry/country fixed effects dummy variables
  * RANDOM_STATE - Set a random state for reproducability
  * MAX_TRIES - Technical specification of the probit/logit estimator. This likely needs not adjustment
  * TREATMENT_COLOR = For graphs of distributions of pscores. Set the color of treatment group density curve
  * CONTROL_COLOR = For graphs of distributions of pscores. Set the color of control group density curve

There are some useful functions in this script.

generate_all_fe_dummies - Creates unique dummy variables for each specified fixed effects variable.
drop_fe_dummies_and_obs - Drops specified dummy columns and their corresponding observations if there is no variation in the treatment variable when the dummy is 1. Optionally reports if a base dummy was dropped.
