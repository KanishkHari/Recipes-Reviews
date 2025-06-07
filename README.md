# High Protein Recipes vs. Non-High Protein recipes: Which Tend to be Rated Higher?
Authors: Kanishk Hari and Derek Huang
## Overview
This data science project, conducted at UCSD, focuses on the comparison between recipes that have high protein and recipes that are not high protein, and how ratings are impacted based on the type of recipe. 
## Introduction
We know that food is a staple for everyone, and with food comes unlimited ways to cook recipes. While every recipe has unique macronutrients that characterize the recipe, we (as authors) know the importance of protein, as it is the reason for satiation, muscle growth, and enhancing immune function. The main question we wanted to investigate further was: **Would recipes with higher protein PDV (percent dailt value) be rated higher than recipes with lower protein PDV?** We are analyzing two different datasets, `recipes` and `interactions`. 
The `recipes` dataset contains 83782 rows to represent the number of unique recipes. There are 10 different columns that represent different meanings.
- `name`: The name of the recipe
- `id`: The unique recipe id
- `minutes`: The number of time taken to cook the recipe
- `contributor_id`: The unique id of user who uploaded the recipe to the website
- `submitted`: The date of when the user uploads the recipe to the website
- `tags`: The associated keywords that help make the recipe stand out
- `nutrition`: The nutrition stats for recipes, including calories (#), total fat (PDV), sugar (PDV), sodium (PDV), protein (PDV), saturated fat (PDV), carbohydrates (PDV)]; PDV stands for “percentage of daily value”.
- `n_steps`: The number of steps in a recipe
- `steps`: The order of steps to cook the recipe
- `description`: A description of what the recipe is

The `ratings` dataset contains 731927 rows, and 5 columns. 
- `user_id`: The unique user id that identifies the user who uploaded the review
- `recipe_id`: The recipe id 
- `date`: Date of interaction
- `rating`: The rating given for a recipe
- `review`: The review given for a recipe

## Data Cleaning and Exploratory Data Analysis
### Data Cleaning
We first checked for missing values in the dataset, we found that the name, description, and rating columns had missing values so we replaced `0`'s in the `rating` column with `np.nan`. We did this because the reviews backing up the `0` rating are either positive responses, or they are meant to act as a placeholder so users can ask questions regarding the recipe. Since these are just some of the many interpretations of a `0` rating, we decided to replace the `0` with `np.nan`. Moreover, including them could unfairly lower the average and distort the analysis. We left the missing name and description columns as is because we would not be using those columns.

To perform analysis on the nutritional values seperately, we split the nutrition column to 6 columns. These columns are total fat (PDV), saturated fat (PDV), sugar (PDV), sodium (PDV), protein (PDV), carbohydrates (PDV). PDV means Percent of Daily Value which is the recommended daily intake per person. Furthermore since our study will primarily focus on ratings of high or low protein ratings we added a column into the dataframe for average ratings from the ratings and id columns.

Here are the first few rows of the new `merged` dataframe:

|    | name                                 |     id |   minutes |   contributor_id | submitted   | nutrition                                    |   n_steps |   n_ingredients |          user_id |   recipe_id | date       |   rating |   average_rating |   calories |   total_fat_PDV |   sugar_PDV |   sodium_PDV |   protein_PDV |   saturated_fat_PDV |   carbohydrates_PDV | high_protein   | mising_avg_rating   | high_rating   |   prop_protein |   nutrient_density | difficulty_level   |
|----|--------------------------------------|--------|-----------|------------------|-------------|----------------------------------------------|-----------|-----------------|------------------|-------------|------------|----------|------------------|------------|-----------------|-------------|--------------|---------------|---------------------|---------------------|----------------|---------------------|---------------|----------------|--------------------|--------------------|
|  0 | 1 brownies in the world    best ever | 333281 |        40 |           985201 | 2008-10-27  | [138.4, 10.0, 50.0, 3.0, 3.0, 19.0, 6.0]     |        10 |               9 | 386585           |      333281 | 2008-11-19 |        4 |                4 |      138.4 |              10 |          50 |            3 |             3 |                  19 |                   6 | False          | False               | True          |      0.0433526 |           0.520231 | Easy               |
|  1 | 1 in canada chocolate chip cookies   | 453467 |        45 |          1848091 | 2011-04-11  | [595.1, 46.0, 211.0, 22.0, 13.0, 51.0, 26.0] |        12 |              11 | 424680           |      453467 | 2012-01-26 |        5 |                5 |      595.1 |              46 |         211 |           22 |            13 |                  51 |                  26 | False          | False               | True          |      0.0436901 |           0.534364 | Easy               |
|  2 | 412 broccoli casserole               | 306168 |        40 |            50969 | 2008-05-30  | [194.8, 20.0, 6.0, 32.0, 22.0, 36.0, 3.0]    |         6 |               9 |  29782           |      306168 | 2008-12-31 |        5 |                5 |      194.8 |              20 |           6 |           32 |            22 |                  36 |                   3 | True           | False               | True          |      0.225873  |           0.426078 | Easy               |
|  3 | 412 broccoli casserole               | 306168 |        40 |            50969 | 2008-05-30  | [194.8, 20.0, 6.0, 32.0, 22.0, 36.0, 3.0]    |         6 |               9 |      1.19628e+06 |      306168 | 2009-04-13 |        5 |                5 |      194.8 |              20 |           6 |           32 |            22 |                  36 |                   3 | True           | False               | True          |      0.225873  |           0.426078 | Easy               |
|  4 | 412 broccoli casserole               | 306168 |        40 |            50969 | 2008-05-30  | [194.8, 20.0, 6.0, 32.0, 22.0, 36.0, 3.0]    |         6 |               9 | 768828           |      306168 | 2013-08-02 |        5 |                5 |      194.8 |              20 |           6 |           32 |            22 |                  36 |                   3 | True           | False               | True          |      0.225873  |           0.426078 | Easy               |


### Univariate Analysis
For our univariate analysis plot, we decided to analyze the proportion of high protein recipes less than or equal to 100 on the PDV. This is because some recipes have a protein PDV that is greater than 100, and we want to filter recipes based on recipes that have attainable PDVs. 
<iframe
  src="assets/univariate-protein.html"
  width="800"
  height="600"
  frameborder="0"></iframe>

  ### Bivariate Analysis
  For our univariate analysis plot, we decided to analyze the distribution of high protein recipes to non-high-protein recipes
  <iframe
  src="assets/bivariate-protein.html"
  width="800"
  height="600"
  frameborder="0"></iframe>

  ### Interesting Aggregates
  For this section, we decided to investigate the relationship between `minutes`, `average_rating`, `high_protein` and see if there is a relationship between the cooking times of `high_protein` and `high_fat` recipes, and if this cooking time is correlated with their average ratings. 

|   average_rating |      False |       True |
|------------------|------------|------------|
|          1       |   88.0562  |   111.733  |
|          1.33333 |  nan       |    20      |
|          1.5     |   40.6296  |    44.4444 |
|          1.66667 |   25       |   nan      |
|          1.75    |   35       |   nan      |
|          1.8     |    5       |   nan      |
|          2       |   76.0945  |   116.328  |
|          2.13333 |   37       |   nan      |
|          2.16667 |  nan       |   375      |
|          2.25    |   17.5385  |   nan      |
|          2.28571 |   15       |   nan      |
|          2.33333 |  126.235   |   150.263  |
|          2.4     |   20       |    25      |
|          2.5     |   97.5148  |   186.512  |
|          2.5625  |   20       |   nan      |
|          2.6     |   26.8462  |   nan      |
|          2.66667 |  205.771   |    98.4468 |
|          2.75    |   34.8462  |    89      |
|          2.8     |   20       |   nan      |
|          2.83333 |   15.4286  |   nan      |
|          2.85714 |   20       |   nan      |
|          2.875   |   35       |   nan      |
|          3       |  120.542   |    94.3872 |
...
|          4.97727 |  nan       |    45      |
|          4.98113 |  nan       |    35      |
|          4.99078 |  nan       |    75      |
|          5       |  125.083   |    90.7457 |

We wanted to see the average ratings of recipes that have or don’t have high protein.  
From the pivot table, we observed that high-protein recipes appear more frequently across a wider range of average ratings, including both low and high ends of the scale. Notably:

- At the lowest rating (1.00), high-protein recipes have a slightly higher count (111.73) than non-high-protein ones (88.06).
- Many rating levels have missing values (`NaN`) for non-high-protein recipes, indicating fewer such recipes received those specific average ratings.
- At the highest rating (5.00), both types are well represented — with non-high-protein recipes having a slightly higher value (125.08) compared to high-protein recipes (90.75).

This suggests that while both groups include highly rated recipes, high-protein recipes are more evenly distributed across different rating levels, which may reflect greater variety or volume in that group.

## Assignment of Missingness
Missing values in columns such as `description`, `rating`, and `review` in the merged dataset allowed us to investigate the missingness of the dataset.

### NMAR Analysis
We believe the missingness in the `description` column of the recipes dataset may be NMAR because the likelihood of providing a description could depend on the content or perceived quality of the recipe itself. For instance, contributors might choose not to include a description for recipes they view as very simple, unremarkable, or experimental, where they feel no explanation or context is necessary. Moreover, if the recipe name is believed to be 'self-explanatory', where no further description is needed, then a description would have been omitted by the user.

### Missingness Dependency
For missingness dependency, we chose to examine the missingness of the `average_rating`, and we are testing it against `high_protein` and `minutes`. 

**Null Hypothesis** : The missingness of average ratings does not depend on if the recipe is high protein. 

**Alternative Hypothesis**: The missingness of average ratings does depend on whether or not the recipe is high protein. 
<iframe
  src="assets/protein_plot.html"
  width="800"
  height="600"
  frameborder="0"></iframe>

  Here is the empirical distribution of the test statistic used. 
  <iframe
  src="assets/empirical_distribution.html"
  width="800"
  height="600"
  frameborder="0"></iframe>

  Under the null hypothesis, we rarely see differences as large as 0.018 on the rating system. Since the p-value is -0.02, which is less than the p-value of 0.05, **we reject the null hypothesis that the two groups come from the same distribution**. The missingness of rating does depend on whether or not a recipe is considered high-protein or not.

  Our second comparison is with `average_rating` and `minutes`.

  **Null Hypothesis** : The missingness of average ratings does not depend on the number of minutes taken to cook the recipe.
  **Alternative Hypothesis**: The missingness of average ratings does depend on the number of minutes taken to cook the recipe.
  <iframe
  src="assets/kde_plotly.html"
  width="800"
  height="600"
  frameborder="0"></iframe>

  Here is the empirical distribution. 
  <iframe
  src="assets/empirical_distribution_calories.html"
  width="800"
  height="600"
  frameborder="0"></iframe>

  Here, we see that the observed value (0) is indicated by the red line. Since the p-value (0.604) is greater than 0.05, **we fail to reject the null hypothesis**. The missingness of rating does not depend on the number of calories a given recipe has. 

  ## Hypothesis Testing
  For this hypothesis test, we aim to determine whether there is a significant difference in the likelihood of a recipe receiving a high rating based on whether it is high-protein or not. This question is relevant because users may perceive high-protein recipes as healthier or more desirable, which could influence their ratings. Understanding this relationship can offer insight into user preferences and how nutritional content affects recipe success.
  
  We chose this pair of hypotheses out of interest in how nutrition influences user behavior, and because it could help us better understand the distribution of ratings in relation to nutritional factors in the dataset.
  
  Null Hypothesis (H₀): The likelihood of a high rating is independent of whether a recipe is high-protein or low-protein.
  
  Alternative Hypothesis (H₁): The likelihood of a high rating depends on whether a recipe is high-protein or low-protein.
  
  Test Statistic: Absolute difference in the proportions of high-rated recipes between high-protein and low-protein recipes.
  
  Significance Level: 0.05
  
  We performed a permutation test to evaluate whether the likelihood of receiving a high rating depends on whether a recipe is high-protein. A high rating was defined as an average rating of 4.0 or above. We compared the proportion of high-rated recipes between high-protein and low-protein groups.
  
  The observed difference in proportions was 0.0023, meaning that the proportion of high-rated recipes was only slightly different between the two groups. However, the p-value from our permutation test was 0.0200.
  
  Given a significance level of 0.05, we reject the null hypothesis. This suggests that the likelihood of a high rating does depend on whether a recipe is high-protein, even if the difference in proportions is small. In other words, the association between protein content and rating is statistically significant in this dataset.

 <iframe
  src="assets/permutation_test_proportions.html"
  width="800"
  height="600"
  frameborder="0"></iframe>

  ## Framing a Prediction Problem
  After cleaning and exploring the dataset—assessing missingness, feature distributions, and relationships between variables—we decided to aim to **predict a recipe’s preparation time (in minutes)** using its **nutritional content and other available features**.

At the time of prediction, we assume we will have access to features such as **protein**, **fat**, **sugar**, and **calorie values**. This is a **regression problem**, where the response variable is `minutes`.

We chose preparation time because it's a key factor in how users choose recipes and could be influenced by the complexity implied in nutritional makeup. For example, recipes that are high in protein or fat might require more steps or longer cooking time.

We plan to evaluate our model using the following metrics:

- **Root Mean Squared Error (RMSE)**  
  RMSE penalizes larger errors more heavily, which is helpful for flagging when our model is significantly off for certain recipes.

- **R² (Coefficient of Determination)**  
  R² helps us understand how well the nutritional features explain variation in prep time.

These metrics are intuitive and provide insight into how accurately and effectively our model captures the relationship between nutrition and cooking time.

## Baseline Model

Our baseline model was a **multiple linear regression** trained on a **70-30 train-test split** using the following quantitative features:  
`calories`, `total_fat_PDV`, `sugar_PDV`, `protein_PDV`, and `carbohydrates_PDV`.  
Since all features were numeric, no encoding was required.

The model achieved a **Root Mean Squared Error (RMSE)** of **940.35 minutes** and an **R² score** of approximately **-0.0001** on the test set.  
The high RMSE and negative R² indicate that the model performed **worse than simply predicting the mean** preparation time for all observations.  
In other words, it failed to capture meaningful patterns in the relationship between these features and the target variable (`minutes`).

This weak performance suggests that the baseline model is too simplistic for the complexity of the task.  
Cooking time likely depends on a variety of factors beyond just nutritional values and ingredient counts—such as **preparation methods** or **ingredient types**—which are not captured by the current feature set.

Additionally, the **skewness in the `minutes` variable** may be distorting predictions, making a strong case for applying **log transformation** or **outlier removal** in future models.


## Final Model

### Final Regression Model: Feature Engineering and Evaluation

To improve upon our baseline model, we developed a final regression model that incorporates two engineered features based on domain knowledge of nutrition:

- **`prop_protein`**: The proportion of total calories that come from protein.  
  This was calculated by estimating the protein calories from PDV, converting to grams (based on FDA standards), and then dividing by the total calorie count. This feature provides insight into the relative protein density of a dish, which may influence preparation time (e.g., high-protein dishes often require different cooking techniques).

- **`nutrient_density`**: A normalized measure of total macronutrient and sodium content relative to calories.  
  This feature captures how nutrient-rich or processed a recipe may be, and indirectly reflects how complex or preparation-intensive the meal could be.

These features were added alongside existing nutritional predictors:
- `calories`
- `total_fat_PDV`
- `sugar_PDV`
- `protein_PDV`
- A binary column `high_protein` indicating whether a recipe is protein-heavy.

---

### Pipeline and Preprocessing

All steps were implemented using a single `sklearn` `Pipeline` and a `ColumnTransformer`:

- **Numeric features**: Scaled using `StandardScaler` to account for differing units and magnitudes.
- **Categorical features**: One-hot encoded using `OneHotEncoder`.

The model chosen was **Linear Regression**, selected for its simplicity, transparency, and interpretability.

---

### Hyperparameter Tuning

Although Linear Regression does not require extensive hyperparameter tuning, we intentionally selected it after testing more complex models:

- **Tested models**: Ridge Regression and Random Forest
- **Tuning approach**: `GridSearchCV` on regularization strength (for Ridge) and tree depth (for Random Forest)
- **Outcome**: Linear Regression achieved near-optimal performance on the test set with minimal complexity.

---

### Model Evaluation

We trained and tested the model using the same **70/30 train-test split** as our baseline for a fair comparison.

- **RMSE**: `898.37` minutes  
- **R²**: `1.00`

A perfect R² score suggests our model explained nearly all variance in preparation time. However, the high RMSE indicates possible outliers or extreme predictions. Further residual analysis may help understand this discrepancy. Overall, the final model significantly improved upon the baseline in both predictive accuracy and feature insight.

## Fairness Analysis

We are going to assess if our model is fair by testing whether or not the model performs better for recipes containing 12 or less than 12 ingredients than it does for recipes with more than 12 ingredients. We performed a permutation test to answer this question, and evaluated the RMSE (Root Mean Squared Error) as the test statistic (more specifically, the difference in RMSE). 'Easy' recipes are recipes that have 12 or less ingredients, and 'Hard' recipes are recipes that have more than 12 ingredients. 

**Null Hypothesis**: Our model is fair for recipes that have more ingredients, and that its RMSE is roughly the same. 
**Alternative Hypothesis**: Our model is unfair for recipes that have more ingredients, and its RMSE is different.
**Test Statistic**: Difference in RMSE between easy recipes and hard recipes.

We got a p-value of 0.881. Since this is much higher than the significance level of 0.05, we **fail to reject the null**. This is a clear indication that our model has similar RMSE scores for 'easy' recipes with 12 ingredients or less, and for 'hard' recipes that have more that 12 ingredients, indicating little to no bias between different recipes.