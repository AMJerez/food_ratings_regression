# Exploring the Relationship Between Recipe Features and Ratings: A Predictive Modeling Approach
By Allison Jerez

## Introduction

The dataset used in this project consists of recipes and their corresponding user ratings from Food.com. This dataset includes various attributes for each recipe, such as the preparation time, ingredients, and user-submitted tags. 

**Question:** What is the relationship between the cooking time and average rating of recipes?

Readers should care about this dataset and question because understanding these relationships can help identify trends in user preferences and improve recipe recommendations. The dataset contains 83,782 rows with columns including `name`, `id`, `minutes`, `contributor_id`, `submitted`, `tags`, `nutrition`, `n_steps`, `steps`, `description`, `ingredients`, `n_ingredients`, and `rating`.

## Data Cleaning and Exploratory Data Analysis

### Data Cleaning

To clean the dataset, the following steps were taken:
1. **Fixing the 'nutrition' column:** The 'nutrition' column contained string representations of lists. These were converted to actual lists, and individual columns for `calories`, `total_fat`, `sugar`, `sodium`, `protein`, `saturated_fat`, and `carbohydrates` were created.
2. **Creating 'hours' column:** The `minutes` column was converted to hours for easier interpretation.
3. **Handling missing values:** Missing values in numerical columns were replaced with the median value of the respective column.

### Univariate Analysis

**Distribution of Cooking Time (Hours)**

[There goes a graph]

**Interpretation:** The histogram of cooking time (in hours) shows the distribution of how long it takes to prepare different recipes. Most recipes have a short cooking time.

**Distribution of Ratings**

[There goes a graph]

**Interpretation:** The histogram of ratings shows that most recipes tend to have high ratings, indicating user satisfaction.

### Bivariate Analysis

**Relationship Between Cooking Time and Rating**

[There goes a graph]

**Interpretation:** The scatter plot and box plot reveal the relationship between cooking time and ratings. It appears that recipes with shorter cooking times have a wide range of ratings, while longer cooking times might affect the ratings differently.

### Interesting Aggregates

**Average Rating and Cooking Time by Year**

[There goes a graph]

**Interpretation:** This grouped table shows the average rating and average cooking time by year. It helps understand how these attributes have changed over time.

## Assessment of Missingness

### NMAR Analysis

The `description` column in the dataset is likely NMAR (Not Missing At Random) because the presence or absence of descriptions may depend on whether the contributor chose to provide one. This behavior is inherent to the data generation process.

### Missingness Dependency

To analyze the dependency of missingness in the `description` column:
- **Dependent on `n_ingredients`**: The p-value of 0.002 indicates that the missingness of `description` depends on the number of ingredients.
- **Non-dependent on `rating`**: The p-value of 0.204 indicates that the missingness of `description` does not depend on the rating.

[There goes a graph for permutation tests]

## Hypothesis Testing

**Hypothesis Question:** What is the relationship between the cooking time and average rating of recipes?

- **Null Hypothesis (H0):** There is no significant difference in the average ratings of recipes that take less than an hour to prepare and those that take an hour or more.
- **Alternative Hypothesis (H1):** There is a significant difference in the average ratings of recipes that take less than an hour to prepare and those that take an hour or more.
- **Test Statistic:** The difference in mean ratings between the two groups.
- **Significance Level:** α = 0.05

[There goes a graph for permutation test results]

**Conclusion:** Since the p-value is 0.003, which is less than 0.05, we reject the null hypothesis. This suggests that there is a significant difference in the average ratings of recipes based on cooking time.

## Framing a Prediction Problem

**Prediction Problem:** Predict the rating of a recipe based on various features.

**Type:** Regression

**Response Variable:** `rating`

**Features:** `minutes`, `n_ingredients`, `n_steps`, `calories`, `total_fat`, `sugar`, `sodium`, `protein`, `saturated_fat`, `carbohydrates`, `year`

## Baseline Model

The baseline model uses `n_ingredients` and `n_steps` as features to predict the `rating`.

**Baseline Model Mean Absolute Error:** 0.4615540502473202

## Final Model

The final model improves upon the baseline model by engineering new features and using a Gradient Boosting Regressor.

**Best parameters for Gradient Boosting:** {'model__learning_rate': 0.1, 'model__max_depth': 3, 'model__n_estimators': 100}

**Final Model Mean Absolute Error:** 0.45911961152511016

## Fairness Analysis

To assess the fairness of the final model, we compare its performance for recipes that take less than an hour to prepare versus those that take an hour or more.

**Groups:** 
- **Group X:** Recipes that take less than 1 hour to prepare
- **Group Y:** Recipes that take 1 hour or more to prepare

**Evaluation Metric:** Mean Absolute Error (MAE)

**Null Hypothesis (H0):** The model's performance (MAE) for recipes that take less than an hour to prepare is roughly the same as for those that take an hour or more. Any differences are due to random chance.

**Alternative Hypothesis (H1):** The model's performance (MAE) for recipes that take less than an hour to prepare is different from those that take an hour or more.

**Test Statistic:** Difference in MAE between the two groups.

**Significance Level:** α = 0.05

**MAE for less than 1 hour:** 0.452053681287183  
**MAE for 1 hour or more:** 0.4756260071874309  
**Observed Difference in MAE:** 0.023572325900247937  
**P-value:** 0.094

Since the p-value is greater than 0.05, we fail to reject the null hypothesis. This suggests that there is no significant difference in the model's performance based on cooking time.



