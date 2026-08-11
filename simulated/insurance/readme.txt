https://github.com/stedy/Machine-Learning-with-R-datasets (insurance.csv)

Lantz, B. (2013). Machine Learning with R. Packt Publishing.

Simulated medical insurance billing data (1338 cases, 7 variables),
constructed by the author using demographic statistics from the US Census
Bureau. Variables: age (years), sex, bmi (kg/m^2), children (count of
dependents), smoker (yes/no), region (US census region), charges (annual
medical costs billed, USD). No missing values. Rows 196 and 582 are exact
duplicates of each other in the source data and are retained here for
fidelity; analysts may wish to drop one.

The generating process is not published as a graph, so no ground-truth DAG
is provided; the knowledge file gives a defensible temporal tier ordering
only. The dataset is known for a strong smoker effect on charges with a
smoker-by-bmi interaction, making it a useful small test of nonlinear
scores versus linear-Gaussian ones.
