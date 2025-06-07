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
