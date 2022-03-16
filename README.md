# example-causal-datasets
Example datasets formatted consistently with ground truth for purposes of causal analysis.
Formating conventions are here:

https://github.com/cmu-phil/example-causal-datasets/blob/main/formatting.txt

This ia work in progress--please complain, especially if the ground truth isn't right or if 
you know ground truth that isn't here. Also, if you can suggest further datasets to 
format in a uniform way with ground truth, please do.

Plot matrices were generated in R as follows (for example):

library(psych)

data2 <- read.table("[file path]/abalone.continuous.txt",sep="\t", header=TRUE)

pairs.panels(data2,
method = "pearson", # correlation method
hist.col = "#00AFBB",
density = TRUE,  # show density plots
ellipses = TRUE # show correlation ellipses
)
