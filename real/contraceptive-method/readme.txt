Contraceptive Method Choice (CMC)
https://archive.ics.uci.edu/ml/datasets/Contraceptive+Method+Choice

Source: 1987 National Indonesia Contraceptive Prevalence Survey. Subjects are
married women who were not pregnant (or did not know they were pregnant) at the
time of interview. N = 1473, no missing values.

Columns (in UCI order):

  wife-age         Wife's age (years)                          continuous
  wife-educ        Wife's education     1=low .. 4=high        ordinal
  husb-educ        Husband's education  1=low .. 4=high        ordinal
  num-child        Number of children ever born                continuous (count)
  wife-relig       Wife's religion      0=Non-Islam, 1=Islam   binary
  wife-working     Wife now working?    0=Yes, 1=No            binary
  husb-occ         Husband's occupation 1,2,3,4                nominal
  sol-index        Standard-of-living index 1=low .. 4=high    ordinal
  media-exp        Media exposure       0=Good, 1=Not good     binary
  contrac-method   Contraceptive method 1=No-use, 2=Long-term, nominal
                                        3=Short-term

History: an earlier version of this file in this repository had only 9 columns
with the UCI column order intact but the last four headers shifted left by one
(husb-occ/sol-index/media-exp/contrac-method labels sat over the wife-working/
husb-occ/sol-index/media-exp values), and the contraceptive-method column was
absent. Corrected 2026-08-25 against the UCI original.
