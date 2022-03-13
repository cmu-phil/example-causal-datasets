# example-causal-datasets
Example datasets formatted consistently with ground truth for purposes of causal analysis

This ia work in progress--please complain, especially if the ground truth isn't right! Also,
if you can suggest further datasets to add, please do.

Plot matrices were generated in R as follows (for example):

library(psych)

data2 <- read.table("[file path]/abalone.continuous.txt",sep="\t", header=TRUE)

pairs.panels(data2,
method = "pearson", # correlation method
hist.col = "#00AFBB",
density = TRUE,  # show density plots
ellipses = TRUE # show correlation ellipses
)
