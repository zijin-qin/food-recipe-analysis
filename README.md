# Food Recipe Analysis

by Bhagya Ram and Zijin Qin

---

## Introduction

Provide an introduction to your dataset, and clearly state the one question your project is centered around. Why should readers of your website care about the dataset and your question specifically? Report the number of rows in the dataset, the names of the columns that are relevant to your question, and descriptions of those relevant columns.

Our dataset contains recipes and ratings from food.com. The recipes dataset contains recipes and their nutrition information, and the ratings dataset contains reviews and ratings of the recipes. We are working with a merged dataset of these two datasets, containing 234428 rows by 17 columns.

*Question:* Does the saturated fat content of the recipe influence its rating?

This is important because dietary choices play a significant role in overall health and well-being. We want to explore how the saturated fat content of a recipe influences its rating. Out of these 17 columns, relevant columns to our project are 'nutrition', which contains each recipe's nutrition information, and 'rating', which contains the rating given for each recipe. We cleaned the dataset to have individual columns for each nutritonal value such as 'saturated fat', which gives the saturated fat of the recipe in PDV (percentage of daily value). We also calculated the average rating for each recipe and put that in a column named 'avg_rating'. 