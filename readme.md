# Interpretable Analysis of School Policy Data

This repository contains R markdown notebooks with code used to create aggregations of data for analysis and then doing analysis of these sets.

[First the data was processed and aggregated in NCES pre-processing.](NCES%20pre-processing.rmd) 
This joins several data sets together by date and school district, then aggregates interesting numeric variables by several summary statistic functions.

[Next the data was analyzed to find important variables using L-1 regularized models.](glmnet.rmd)
These models are compared against featureless baseline models, then the results are summarized by examining the frequency with which each variable is used, and its determined coefficient.

[Finally the data was analyzed with decision tree models, to see if these models found other trends that were not discovered with the linear models.](decisiontrees.rmd) Again baselines were created for comparison, as well as non-interpretable models to compare against. The generated decision tree models were then analyzed by examining how many times each variable was used, and in how many different trees it appeared.

Visualizations to view the correlation of different variables combined with their importance in the GLM LASSO were created, and are available [here](https://csaluski.github.io/interpretable_policy_animint/). 
The repository hosting these visualizations is located [here](https://github.com/Csaluski/interpretable_policy_animint).
They were created with the code available in the files of [coaching_correlation](./coaching_correlation.rmd) and [build_correlation_animint](./build_correlation_animint.rmd). 
Further visualizations can easily be built using the code from build_correlation_animint by following the code present in that file, which created the visualizations.