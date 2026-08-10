https://archive.ics.uci.edu/ml/machine-learning-databases/housing/

Thanks to https://www.cmu.edu/dietrich/causality/projects/causal_learn_benchmarks/
for the pointer.

https://www.tandfonline.com/doi/full/10.1080/07350015.2019.1624293

1. Title: Boston Housing Data

2. Sources:
   (a) Origin:  This dataset was taken from the StatLib library which is
                maintained at Carnegie Mellon University.
   (b) Creator:  Harrison, D. and Rubinfeld, D.L. 'Hedonic prices and the
                 demand for clean air', J. Environ. Economics & Management,
                 vol.5, 81-102, 1978.
   (c) Date: July 7, 1993

3. Past Usage:
   -   Used in Belsley, Kuh & Welsch, 'Regression diagnostics ...', Wiley,
       1980.   N.B. Various transformations are used in the table on
       pages 244-261.
    -  Quinlan,R. (1993). Combining Instance-Based and Model-Based Learning.
       In Proceedings on the Tenth International Conference of Machine
       Learning, 236-243, University of Massachusetts, Amherst. Morgan
       Kaufmann.

4. Relevant Information:

   Concerns housing values in suburbs of Boston.

5. Number of Instances: 506

6. Number of Attributes: 13 continuous attributes (including "class"
                         attribute "MEDV"), 1 binary-valued attribute.

7. Attribute Information:

    1. CRIM      per capita crime rate by town
    2. ZN        proportion of residential land zoned for lots over
                 25,000 sq.ft.
    3. INDUS     proportion of non-retail business acres per town
    4. CHAS      Charles River dummy variable (= 1 if tract bounds
                 river; 0 otherwise)
    5. NOX       nitric oxides concentration (parts per 10 million)
    6. RM        average number of rooms per dwelling
    7. AGE       proportion of owner-occupied units built prior to 1940
    8. DIS       weighted distances to five Boston employment centres
    9. RAD       index of accessibility to radial highways
    10. TAX      full-value property-tax rate per $10,000
    11. PTRATIO  pupil-teacher ratio by town
    12. B        1000(Bk - 0.63)^2 where Bk is the proportion of blacks
                 by town
    13. LSTAT    % lower status of the population
    14. MEDV     Median value of owner-occupied homes in $1000's

8. Missing Attribute Values:  None.
=====================================================================
boston-housing-corrected.mixed.maximum.92.txt
=====================================================================

A corrected, town-identified variant of the same 506 census tracts, added
2026-08-10. Provenance: Gilley, O.W. and Pace, R.K., "On the Harrison and
Rubinfeld Data," J. Environ. Economics & Management 31, 403-405 (1996),
who audited the original against the 1970 census; their corrected file
(StatLib, boston_corrected.txt) is distributed as BostonHousing2 in the R
package mlbench, from which this file was generated. Row order is
identical to boston-housing.continuous.txt (verified column-by-column).

Columns (tab-delimited; 1 discrete + 1 binary discrete + 15 continuous):

    TOWN     town name (92 levels, spaces hyphenated, e.g.
             Boston-Back-Bay); tracts of a town are contiguous in file
             order
    LON,LAT  tract point coordinates (Gilley & Pace)
    CRIM ... LSTAT  as in boston-housing.continuous.txt
    CHAS     Charles River indicator, here typed discrete (0/1)
    CMEDV    the Gilley-Pace corrected median home value; differs from
             MEDV in 8 rows (rows 8, 39, 191, 241, 438, 443, 455, 506 of
             the data). MEDV itself is omitted to avoid an exact near-
             duplicate column. CMEDV remains top-coded (censored) at 50
             in 16 rows.

Deliberate choices, made for this repository and open to revision: the
identifier columns OBS., TOWN# and TRACT are omitted (TOWN carries the
grouping information in readable form); MEDV is omitted in favor of
CMEDV; CHAS is typed discrete here (it is continuous in the .continuous
file).

Why this variant exists. The rows of this dataset are not i.i.d., in two
distinct ways, and the town column makes both auditable:

1. Multilevel structure. ZN, INDUS, RAD, TAX and PTRATIO are constant
   within towns - they are town-level attributes repeated across tracts,
   with effectively ~92 observations, not 506. Tetrad's data audit
   (SERIAL_DEPENDENCE check with TOWN as the serial grouping variable)
   identifies them automatically: they are skipped within towns for lack
   of within-group variance while showing pooled lag-1 autocorrelations
   of 0.81-0.98 in file order.

2. Spatial dependence among neighboring tracts. Within towns, lag-1
   autocorrelations remain substantial for NOX (0.72), DIS (0.48), LON/
   LAT (~0.40), B (0.35), LSTAT (0.32), CMEDV (0.28) and AGE (0.26), so
   tracts are not exchangeable even inside a town. CRIM (0.10) and RM
   (0.09) are close to exchangeable within towns; their pooled
   autocorrelations were the sorting, not the process.

Analyses that treat the 506 rows as i.i.d. will be anticonservative,
severely so for edges involving the town-level variables. Options include
aggregating to town level, analyzing tract-level variables against an
honest effective sample size, hierarchical/multilevel treatment, or using
TOWN as the serial grouping variable in Tetrad's data audit to document
the structure. TOWN itself is a grouping/nesting variable, not a
substantive causal variable, and is not recommended as a search variable
(the audit will flag its 92 levels via DISCRETE_MANY_LEVELS).
