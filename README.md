# Title: Exploring the Relationship Between Recipe Features and Ratings: A Predictive Modeling Approach

### Author: Allison Jerez

## Introduction
Provide an introduction to your dataset, and clearly state the one question your project is centered around. Why should readers of your website care about the dataset and your question specifically? Report the number of rows in the dataset, the names of the columns that are relevant to your question, and descriptions of those relevant columns.

## Data Cleaning and Exploratory Data Analysis
Describe the data cleaning steps you took and how they affected your analyses. The steps should be explained in reference to the data generating process. Show the head of your cleaned DataFrame. Look at the distributions of relevant columns separately by using DataFrame operations and drawing at least two relevant plots. Embed at least one plotly plot you created in your notebook that displays the distribution of a single column. Include a 1-2 sentence explanation about your plot, making sure to describe and interpret any trends present.

## Assessment of Missingness
State whether you believe there is a column in your dataset that is NMAR. Explain your reasoning and any additional data you might want to obtain that could explain the missingness (thereby making it MAR). Make sure to explicitly use the term “NMAR.” Present and interpret the results of your missingness permutation tests with respect to your data and question. Embed a plotly plot related to your missingness exploration; ideas include:
- The distribution of column Y when column X is missing and the distribution of column Y when column X is not missing.
- The empirical distribution of the test statistic used in one of your permutation tests, along with the observed statistic.

## Hypothesis Testing
Clearly state a pair of hypotheses and perform a hypothesis test or permutation test that is not related to missingness. Clearly state your null and alternative hypotheses, your choice of test statistic and significance level, the resulting p-value, and your conclusion. Justify why these choices are good choices for answering the question you are trying to answer. Optional: Embed a visualization related to your hypothesis test.

## Framing a Prediction Problem
Clearly state your prediction problem and type (classification or regression). If you are building a classifier, make sure to state whether you are performing binary classification or multiclass classification. Report the response variable (i.e. the variable you are predicting) and why you chose it, the metric you are using to evaluate your model and why you chose it over other suitable metrics (e.g. accuracy vs. F1-score). Justify what information you would know at the “time of prediction” and only train your model using those features.

## Baseline Model
Describe your baseline model and state the features in your model, including how many are quantitative, ordinal, and nominal, and how you performed any necessary encodings. Report the performance of your model and whether or not you believe your current model is “good” and why. Include the MAE of your baseline model.

## Final Model
State the features you added and why they are good for the data and prediction task. Describe the modeling algorithm you chose, the hyperparameters that ended up performing the best, and the method you used to select hyperparameters and your overall model. Describe how your Final Model’s performance is an improvement over your Baseline Model’s performance. Optional: Include a visualization that describes your model’s performance.

## Fairness Analysis
Conduct a fairness analysis of your model. Identify and explain any potential biases that may affect your model’s predictions. Propose and test at least one method for mitigating bias in your model. Report on the effectiveness of your bias mitigation strategy and any trade-offs involved. Optional: Include a visualization related to your fairness analysis.

