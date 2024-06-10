# Food Recipe Analysis

by Bhagya Ram and Zijin Qin

## Introduction

Our dataset contains recipes and ratings from food.com. The recipes dataset contains recipes and their nutrition information, and the ratings dataset contains reviews and ratings of the recipes. We are working with a merged dataset of these two datasets, containing 234428 rows by 17 columns.

**Question:** Does the saturated fat content of the recipe influence its rating?

This is important because dietary choices play a significant role in overall health and well-being. We want to explore how the saturated fat content of a recipe influences its rating. Out of these 17 columns, relevant columns to our project are `nutrition`, which contains each recipe's nutrition information, and `rating`, which contains the rating given for each recipe. 

We cleaned the dataset to have individual columns for each nutritonal value such as `saturated fat`, which gives the saturated fat of the recipe in PDV (percentage of daily value). We also calculated the average rating for each recipe and put that in a column named `avg_rating`. Our question analyzes the connection between the average rating of a recipe with its saturated fat content.  

## Data Cleaning and Exploratory Data Analysis

We took the following steps to clean our data for further analysis:
1. We dropped the `recipe_id` column from the RATINGS dataframe because it contains the same information as `id` column from the RECIPES dataframe in our merged dataframe. We chose to keep only one column identifying each recipe for simplicity in our analysis. 
2. We then renamed the `id` column to `ID_recipe` to give it a meaningful name, emphasizing the information contained represents each recipe.
3. We cleaned the `nutrition` column, with each row containing the nutrition information of each recipe. We put each nutrition information into its own column. Since our question asks whether the saturated fat content of a recipe influence its average rating on the website, we only want to focus on analyzing saturated fat, not the entire nutrition information. With our cleaned data, we can focus on the saturated fat content of the recipe without overcomplicating our analysis process.
4. We then dropped the `nutrition` column because the nutrition information contained in the column is in their separate columns. Thus, we didn't need the `nutrition` column anymore. 