# Interpretable Analysis of School Policy Data

This repository contains R markdown notebooks with code used to create aggregations of data for analysis and then doing analysis of these sets.

[First the data was processed and aggregated in `DCI pre-processing`.](DCI%20pre-processing.rmd) 
This joins several data sets together by date and school district, then aggregates interesting numeric variables by several summary statistic functions.

[Then aggregation and summarization of the coaching logs](coaching_aggregation.Rmd) 
was conducted, which was originally written by Balaji Senthilkumar, and then revised by Charles Saluski.

[Next the data was analyzed to find important variables using L-1 regularized models.](glmnet.rmd)
These models are compared against featureless baseline models and other non-interpretable models to compare their accuracy, then the results are summarized by examining the frequency with which each variable is used, and its determined coefficient.

The GLM models were found to be the most accurate out of the utilized models, as can be seen in [this visualization](img_out/glmnet/regr.loss.mse.all.png).

It was found that the `CFA_avg` variable from the CWIS data set had a very high level of correlation with the `ETLP_avg` variable, also from the CWIS data set. Another set of analyses were done, one excluding the `CFA_avg` from the variables used to predict the `ETLP_avg`, and another attempting to predict the `CFA_avg` by other variables. In both of these, the `PD_avg` and `DBDM_avg` were found to be the most influential, as well as a minor positive coefficient for the `year` variable.

The output from these models is located [here](./img_out/glmnet/).

[The data was next analyzed with decision tree models, to see if these models found other trends that were not discovered with the linear models.](decisiontrees.rmd) Again baselines were created for comparison, as well as non-interpretable models to compare against. The generated decision tree models were then analyzed by examining how many times each variable was used, and in how many different trees it appeared.

These trees enable a different interpretation of their results, where bins for the training samples are created by creating decision points based on a threshold value. This allows these models to account for an amount of variable interaction that GLM models are not capable of. 

These models found similar results to the GLM models of the previous step, with the `CFA_avg` variable being highly correlated with the `ETLP_avg`, along with other variables from the CWIS data set. When the other variables sourced from the CWIS data were removed from the models, the predictive power of the models regressed to that of the baseline models. 

Their output is located [here](./img_out/decision_trees/).

Visualizations to view the correlation of different variables combined with their importance in the GLM LASSO were created, and are available [here](https://csaluski.github.io/interpretable_policy_animint/). 
The repository hosting these visualizations is located [here](https://github.com/Csaluski/interpretable_policy_animint).
They were created with the code available in [build_correlation_animint.rmd](./build_correlation_animint.rmd). 
Further visualizations can easily be built by following the code present in that file and `glmnet.rmd`, which output the the coefficients used in the visualizations.

A large number of tasks attempting to predict ELA MAP results for 3rd grade students were then created, aimed at trying to identify factors that lead to improvements in the test results of IEP and SSG students. 
The code used to create these visualizations is [here](./super_subgroup_prediction.rmd), and the results are [here](./img_out/iep_analysis/). Only the models which had an improvement over the baseline models were output, as the models which show the  Unfortunately there were no significant results found that remained between cross validation rounds.

A simple comparison of schools participating in the DCI program in the year prior and after the outbreak of the Covid-19 pandemic was then conducted, aiming to examine which schools suffered more or less greatly during the year where most instruction was online. 

MAP scores, discipline rates, and attendance rates were examined by the number of years in the DCI programs, both before and after the pandemic year. The code is [here](./groups_comparisons.rmd), and the results can be found [here](./img_out/by_iep_groups/).

An attempt was made to predict MAP scores state wide by utilizing GLM and decision tree models with the available NCES data, using the code in [this file](./general_map_prediction.rmd); however no significant results were found in the results, seen [here](./img_out/map_prediction/).