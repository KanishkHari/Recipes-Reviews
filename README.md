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


### Univariate Analysis
<iframe
  src="assets/univariate-protein.html"
  width="800"
  height="600"
  frameborder="0"></iframe>
