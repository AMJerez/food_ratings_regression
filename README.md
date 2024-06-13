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

| name                                 |     id |   minutes |   contributor_id | submitted   | tags                                                                                                                                                                                                                                                                                               |   n_steps | steps                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | description                                                                                                                                                                                                                                                                                                                                                                       | ingredients                                                                                                                                                                                                                             |   n_ingredients |   rating |   calories |   total_fat |   sugar |   sodium |   protein |   saturated_fat |   carbohydrates |    hours |
|:-------------------------------------|-------:|----------:|-----------------:|:------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------:|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------:|---------:|-----------:|------------:|--------:|---------:|----------:|----------------:|----------------:|---------:|
| 1 brownies in the world    best ever | 333281 |        40 |           985201 | 2008-10-27  | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'for-large-groups', 'desserts', 'lunch', 'snacks', 'cookies-and-brownies', 'chocolate', 'bar-cookies', 'brownies', 'number-of-servings']                                                                        |        10 | ['heat the oven to 350f and arrange the rack in the middle', 'line an 8-by-8-inch glass baking dish with aluminum foil', 'combine chocolate and butter in a medium saucepan and cook over medium-low heat , stirring frequently , until evenly melted', 'remove from heat and let cool to room temperature', 'combine eggs , sugar , cocoa powder , vanilla extract , espresso , and salt in a large bowl and briefly stir until just evenly incorporated', 'add cooled chocolate and mix until uniform in color', 'add flour and stir until just incorporated', 'transfer batter to the prepared baking dish', 'bake until a tester inserted in the center of the brownies comes out clean , about 25 to 30 minutes', 'remove from the oven and cool completely before cutting']                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   | these are the most; chocolatey, moist, rich, dense, fudgy, delicious brownies that you'll ever make.....sereiously! there's no doubt that these will be your fav brownies ever for you can add things to them or make them plain.....either way they're pure heaven!                                                                                                              | ['bittersweet chocolate', 'unsalted butter', 'eggs', 'granulated sugar', 'unsweetened cocoa powder', 'vanilla extract', 'brewed espresso', 'kosher salt', 'all-purpose flour']                                                          |               9 |        4 |      138.4 |          10 |      50 |        3 |         3 |              19 |               6 | 0.666667 |
| 1 in canada chocolate chip cookies   | 453467 |        45 |          1848091 | 2011-04-11  | ['60-minutes-or-less', 'time-to-make', 'cuisine', 'preparation', 'north-american', 'for-large-groups', 'canadian', 'british-columbian', 'number-of-servings']                                                                                                                                      |        12 | ['pre-heat oven the 350 degrees f', 'in a mixing bowl , sift together the flours and baking powder', 'set aside', 'in another mixing bowl , blend together the sugars , margarine , and salt until light and fluffy', 'add the eggs , water , and vanilla to the margarine / sugar mixture and mix together until well combined', 'add in the flour mixture to the wet ingredients and blend until combined', 'scrape down the sides of the bowl and add the chocolate chips', 'mix until combined', 'scrape down the sides to the bowl again', 'using an ice cream scoop , scoop evenly rounded balls of dough and place of cookie sheet about 1 - 2 inches apart to allow for spreading during baking', 'bake for 10 - 15 minutes or until golden brown on the outside and soft & chewy in the center', 'serve hot and enjoy !']                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | this is the recipe that we use at my school cafeteria for chocolate chip cookies. they must be the best chocolate chip cookies i have ever had! if you don't have margarine or don't like it, then just use butter (softened) instead.                                                                                                                                            | ['white sugar', 'brown sugar', 'salt', 'margarine', 'eggs', 'vanilla', 'water', 'all-purpose flour', 'whole wheat flour', 'baking soda', 'chocolate chips']                                                                             |              11 |        5 |      595.1 |          46 |     211 |       22 |        13 |              51 |              26 | 0.75     |
| 412 broccoli casserole               | 306168 |        40 |            50969 | 2008-05-30  | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'side-dishes', 'vegetables', 'easy', 'beginner-cook', 'broccoli']                                                                                                                                               |         6 | ['preheat oven to 350 degrees', 'spray a 2 quart baking dish with cooking spray , set aside', 'in a large bowl mix together broccoli , soup , one cup of cheese , garlic powder , pepper , salt , milk , 1 cup of french onions , and soy sauce', 'pour into baking dish , sprinkle remaining cheese over top', 'bake for 25 minutes or until cheese is lightly browned', 'sprinkle with rest of french fried onions and bake until onions are browned and cheese is bubbly , about 10 more minutes']                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | since there are already 411 recipes for broccoli casserole posted to "zaar" ,i decided to call this one  #412 broccoli casserole.i don't think there are any like this one in the database. i based this one on the famous "green bean casserole" from campbell's soup. but i think mine is better since i don't like cream of mushroom soup.submitted to "zaar" on may 28th,2008 | ['frozen broccoli cuts', 'cream of chicken soup', 'sharp cheddar cheese', 'garlic powder', 'ground black pepper', 'salt', 'milk', 'soy sauce', 'french-fried onions']                                                                   |               9 |        5 |      194.8 |          20 |       6 |       32 |        22 |              36 |               3 | 0.666667 |
| millionaire pound cake               | 286009 |       120 |           461724 | 2008-02-12  | ['time-to-make', 'course', 'cuisine', 'preparation', 'occasion', 'north-american', 'desserts', 'american', 'southern-united-states', 'dinner-party', 'holiday-event', 'cakes', 'dietary', 'christmas', 'thanksgiving', 'low-sodium', 'low-in-something', 'taste-mood', 'sweet', '4-hours-or-less'] |         7 | ['freheat the oven to 300 degrees', 'grease a 10-inch tube pan with butter , dust the bottom and sides with flour , and set aside', 'in a large mixing bowl , cream the butter and sugar with an electric mixer and add the eggs one at a time , beating after each addition', 'alternately add the flour and milk , stirring till the batter is smooth', 'add the two extracts and stir till well blended', 'scrape the batter into the prepared pan and bake till a cake tester or knife blade inserted in the center comes out clean , about 1 1 / 2 hours', 'cool the cake in the pan on a rack for 5 minutes , then turn it out on the rack to cool completely']                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | why a millionaire pound cake?  because it's super rich!  this scrumptious cake is the pride of an elderly belle from jackson, mississippi.  the recipe comes from "the glory of southern cooking" by james villas.                                                                                                                                                                | ['butter', 'sugar', 'eggs', 'all-purpose flour', 'whole milk', 'pure vanilla extract', 'almond extract']                                                                                                                                |               7 |        5 |      878.3 |          63 |     326 |       13 |        20 |             123 |              39 | 2        |
| 2000 meatloaf                        | 475785 |        90 |          2202916 | 2012-03-06  | ['time-to-make', 'course', 'main-ingredient', 'preparation', 'main-dish', 'potatoes', 'vegetables', '4-hours-or-less', 'meatloaf', 'simply-potatoes2']                                                                                                                                             |        17 | ['pan fry bacon , and set aside on a paper towel to absorb excess grease', 'mince yellow onion , red bell pepper , and add to your mixing bowl', 'chop garlic and set aside', 'put 1tbsp olive oil into a saut pan , along with chopped garlic , teaspoons white pepper and a pinch of kosher salt', 'bring to a medium heat to sweat your garlic', 'preheat oven to 350f', 'coarsely chop your baby spinach add to your heated pan , stir frequently for approximately 5 min to wilt', 'add your spinach to the mixing bowl', 'chop your now cooled bacon , and add it to the mixing bowl', 'add your meatloaf mix to the bowl , with one egg and mix till thoroughly combined', 'add your goat cheese , one egg , 1 / 8 tsp white pepper and 1 / 8 tsp of kosher salt and mix till thoroughly combined', 'transfer to a 9x5 meatloaf pan , and cook for 60 min or until the internal temperature is at least 160f', 'let stand for 5min', 'melt 1tbsp unsalted butter into a frying pan , and cook up to three eggs at a time', 'crack each egg into a separate dish , in order to prevent egg shells from reaching the pan , then add salt and pepper to taste', 'wait until the egg whites are firm looking , but slightly runny on top before flipping your eggs', 'after flipping , wait 10~20 seconds before removing each egg and placing it over your slices of meatloaf'] | ready, set, cook! special edition contest entry: a mediterranean flavor inspired meatloaf dish. featuring: simply potatoes - shredded hash browns, egg, bacon, spinach, red bell pepper, and goat cheese.                                                                                                                                                                         | ['meatloaf mixture', 'unsmoked bacon', 'goat cheese', 'unsalted butter', 'eggs', 'baby spinach', 'yellow onion', 'red bell pepper', 'simply potatoes shredded hash browns', 'fresh garlic', 'kosher salt', 'white pepper', 'olive oil'] |              13 |        5 |      267   |          30 |      12 |       12 |        29 |              48 |               2 | 1.5      |

### Univariate Analysis

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

[(Optional) There goes a graph for permutation test results]

**Conclusion:** Since the p-value is 0.003, which is less than 0.05, we reject the null hypothesis. This suggests that there is a significant difference in the average ratings of recipes based on cooking time.

## Framing a Prediction Problem

**Prediction Problem:** Predict the rating of a recipe based on various features.

**Type:** Regression

**Response Variable:** `rating`

**Features:** `minutes`, `n_ingredients`, `n_steps`, `calories`, `total_fat`, `sugar`, `sodium`, `protein`, `saturated_fat`, `carbohydrates`, `year`

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

[(Optional) There goes a graph]

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



