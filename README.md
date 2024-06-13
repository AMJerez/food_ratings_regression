# Exploring the Relationship Between Recipe Features and Ratings: A Predictive Modeling Approach

## Introduction

The dataset used in this project consists of recipes and their corresponding user ratings from Food.com. This dataset includes various attributes for each recipe, such as the preparation time, ingredients, and user-submitted tags. 

**Question:** What is the relationship between the cooking time and average rating of recipes?

Readers should care about this dataset and question because understanding these relationships can help identify trends in user preferences and improve recipe recommendations. The dataset contains 83,782 rows with columns including:
- `name`
- `id`
- `minutes`
- `contributor_id`
- `submitted`
- `tags`
- `nutrition`
- `n_steps`
- `steps`
- `description`
- `ingredients`
- `n_ingredients`
- `rating`

## Data Cleaning and Exploratory Data Analysis

### Data Cleaning

To clean the dataset, the following steps were taken:
1. **Fixing the 'nutrition' column:** The 'nutrition' column contained string representations of lists. These were converted to actual lists, and individual columns for `calories`, `total_fat`, `sugar`, `sodium`, `protein`, `saturated_fat`, and `carbohydrates` were created.
2. **Creating 'hours' column:** The `minutes` column was converted to hours for easier interpretation.
3. **Handling missing values:** Missing values in numerical columns were replaced with the median value of the respective column.

**Head of the DataFrame**

| name                             | id     | minutes | contributor_id | protein | saturated_fat | carbohydrates | hours |
|----------------------------------|--------|---------|----------------|---------|---------------|---------------|-------|
| 1 brownies in the world best ever| 333281 | 40      | 985201         | 3.0     | 19.0          | 6.0           | 0.67  |
| 1 in canada chocolate chip cookies| 453467 | 45      | 1848091        | 13.0    | 51.0          | 26.0          | 0.75  |
| 412 broccoli casserole           | 306168 | 40      | 50969          | 22.0    | 36.0          | 3.0           | 0.67  |
| millionaire pound cake           | 286009 | 120     | 461724         | 20.0    | 123.0         | 39.0          | 2.00  |
| 2000 meatloaf                    | 475785 | 90      | 2202916        | 29.0    | 48.0          | 2.0           | 1.50  |


### Univariate Analysis

<center><strong>Distribution of Ratings</strong></center>

<iframe
  src="assets/distribution_of_ratings.html"
  width="800"
  height="600"
  frameborder="0"
  style="display: block; margin: 0 auto; padding: 0;"
></iframe>
**Interpretation:** The histogram of ratings shows that most recipes tend to have high ratings, indicating user satisfaction.

### Bivariate Analysis

<center><strong>Relationship Between Cooking Time and Rating</strong></center>

<iframe
  src="assets/cooking_time_and_rating.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
**Interpretation:** The scatter plot reveal the relationship between cooking time and ratings. It appears that recipes with shorter cooking times have a wide range of ratings, while longer cooking times might affect the ratings differently.

### Interesting Aggregates

<center><strong>Average Rating and Cooking Time by Year</strong></center>

|   year |   average_rating |   average_cooking_time |
|-------:|-----------------:|-----------------------:|
|   2008 |          4.60849 |                1.72976 |
|   2009 |          4.63412 |                1.54804 |
|   2010 |          4.65191 |                2.10875 |
|   2011 |          4.68762 |                3.93305 |
|   2012 |          4.6829  |                1.66085 |

**Interpretation:** This grouped table shows the average rating and average cooking time by year. It helps understand how these attributes have changed over time. It goes from 2008 all the way to 2018, this just includes the head.

## Assessment of Missingness

### NMAR Analysis

The `description` column in the dataset is likely NMAR (Not Missing At Random) because the presence or absence of descriptions may depend on whether the contributor chose to provide one. This behavior is inherent to the data generation process. Additional data that could explain the missingness might include the length of the recipe or the contributor's activity level on the platform, which could make the missingness MAR (Missing At Random).

### Missingness Dependency

To analyze the dependency of missingness in the `description` column, permutation tests were performed.

#### Dependent on `n_ingredients`
The p-value of 0.002 indicates that the missingness of `description` depends on the number of ingredients. This suggests that recipes with more ingredients are less likely to have missing descriptions, possibly because more complex recipes encourage contributors to provide detailed descriptions.

#### Non-dependent on `rating`
The p-value of 0.189 indicates that the missingness of `description` does not depend on the rating. This suggests that whether a recipe has a description or not is independent of how users rate the recipe.

**Permutation Test Results:**

**Test for Dependency on `n_ingredients`:**
- Observed Difference: -1.4723927615771073
- P-value: 0.002

**Test for Non-Dependency on `rating`:**
- Observed Difference: -0.09867670120509064
- P-value: 0.189

**Graph of Permutation Test for `n_ingredients`:**
<iframe
  src="assets/dependency_n_ingredients.html"
  width="800"
  height="600"
  frameborder="0"
  style="display: block; margin: 0 auto; padding: 0;"
></iframe>

**Graph of Permutation Test for `rating`:**
<iframe
  src="assets/nondependency_rating.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
The results of these tests are significant for `n_ingredients`, indicating that the missingness of the `description` column is dependent on the number of ingredients but not on the rating. This insight helps in understanding the data generation process and can guide further data cleaning and analysis steps.

## Hypothesis Testing

**Hypothesis Question:** What is the relationship between the cooking time and average rating of recipes?

- **Null Hypothesis (H0):** There is no significant difference in the average ratings of recipes that take less than an hour to prepare and those that take an hour or more.
- **Alternative Hypothesis (H1):** There is a significant difference in the average ratings of recipes that take less than an hour to prepare and those that take an hour or more.
- **Test Statistic:** The difference in mean ratings between the two groups.
- **Significance Level:** α = 0.05


**Conclusion:** Since the p-value is 0.003, which is less than 0.05, we reject the null hypothesis. This suggests that there is a significant difference in the average ratings of recipes based on cooking time.

## Framing a Prediction Problem

**Prediction Problem:** Predict the rating of a recipe based on various features.

**Type:** Regression

**Response Variable:** `rating` - The rating given to a recipe by users. This is chosen because the goal is to understand what factors influence the perceived quality of recipes as rated by users.

**Features:** 
- `minutes` - The time taken to prepare the recipe.
- `n_ingredients` - The number of ingredients used in the recipe.
- `n_steps` - The number of steps required to prepare the recipe.
- `calories` - The calorie content of the recipe.
- `total_fat` - The total fat content of the recipe.
- `sugar` - The sugar content of the recipe.
- `sodium` - The sodium content of the recipe.
- `protein` - The protein content of the recipe.
- `saturated_fat` - The saturated fat content of the recipe.
- `carbohydrates` - The carbohydrate content of the recipe.
- `year` - The year the recipe was submitted.

**Metric for Evaluation:** Mean Absolute Error (MAE) - This metric is chosen because it provides a straightforward measure of the average magnitude of errors in predictions, without considering their direction. MAE is suitable for regression problems as it is easy to interpret and understand.

**Justification of Features:** The features selected are all available at the time the recipe is submitted. We are not using any features that would only be known after the recipe has been rated (e.g., number of reviews). This ensures that our model is trained using information that would be available at the time of prediction, making it a fair and realistic prediction task.

## Baseline Model

The baseline model is a simple linear regression model that uses `n_ingredients` and `n_steps` as features to predict the `rating`. These features were chosen because they are indicative of the complexity of a recipe and could potentially influence user ratings.

**Features:**
- `n_ingredients` (Quantitative): Number of ingredients in the recipe.
- `n_steps` (Quantitative): Number of steps required to prepare the recipe.

No ordinal or nominal features were included in this baseline model, and thus no encoding was necessary.

The data was split into training and testing sets using an 80-20 split. The model was trained using the training set, and its performance was evaluated on the test set.

**Baseline Model Mean Absolute Error (MAE):** 0.4615540502473202

**Evaluation:**
The baseline model's performance, with a MAE of 0.4615540502473202, serves as a reference point for further model improvements. While this MAE indicates a reasonable level of accuracy, there is potential for improvement by incorporating additional features and more complex modeling techniques. Therefore, I believe the current model is a good starting point, but further enhancements are necessary to achieve better predictive performance.

## Final Model

### Features Added
For the final model, additional features were engineered and included in the model to capture more information about the recipes:
- `log_minutes` (Quantitative): The log transformation of the `minutes` feature, which helps to normalize the distribution and reduce the effect of outliers.
- `hours` (Quantitative): The `minutes` feature converted to hours for easier interpretation.
- `year` (Quantitative): The year the recipe was submitted, which can capture trends over time.
- Polynomial features of `n_steps` and `hours`: Interaction terms and polynomial features were included to capture non-linear relationships between these features and the rating.

These features were chosen because they provide a more comprehensive understanding of the recipes' characteristics and their potential impact on user ratings.

### Modeling Algorithm
The final model chosen was a Gradient Boosting Regressor, which is an ensemble learning method that builds multiple decision trees in a sequential manner to improve performance.

**Hyperparameters Tuned:**
- `n_estimators`: Number of boosting stages to be run.
- `max_depth`: Maximum depth of the individual regression estimators.
- `learning_rate`: Step size at each iteration while moving toward a minimum of the loss function.

**Best Parameters Found:**
- `model_learning_rate`: 0.1
- `model_max_depth`: 3
- `model_n_estimators`: 100

These parameters were selected using GridSearchCV, which performed an exhaustive search over specified parameter values for an estimator.

### Performance
**Final Model Mean Absolute Error (MAE):** 0.45911961152511016

**Evaluation:**
The final model's performance, with a MAE of 0.45911961152511016, shows a slight improvement over the baseline model's MAE of 0.4615540502473202. This improvement, though modest, indicates that the additional features and the use of a more sophisticated modeling algorithm have helped capture more information about the recipes, leading to better predictions. The Gradient Boosting Regressor, with its ability to handle complex interactions and non-linearities, contributed to this improved performance.


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



