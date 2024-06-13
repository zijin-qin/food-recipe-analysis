# Food Recipe Analysis

by Bhagya Ram and Zijin Qin

## Introduction

Our dataset contains recipes and ratings from food.com. The recipes dataset contains recipes and their nutrition information, and the ratings dataset contains reviews and ratings of the recipes. We are working with a merged dataset of these two datasets, containing 234428 rows by 17 columns.

**Question:** Does the saturated fat content of the recipe influence its rating?

This is important because dietary choices play a significant role in overall health and well-being. We want to explore how the saturated fat content of a recipe influences its rating. Out of these 17 columns, relevant columns to our project are `nutrition`, which contains each recipe's nutrition information, and `rating`, which contains the rating given for each recipe. 

We cleaned the dataset to have individual columns for each nutritonal value such as `saturated fat`, which gives the saturated fat of the recipe in PDV (percentage of daily value). We also calculated the average rating for each recipe and put that in a column named `avg_rating`. Our question analyzes the connection between the average rating of a recipe with its saturated fat content.  

## Data Cleaning and Exploratory Data Analysis

### Data Cleaning

We took the following steps to clean our data for further analysis:
1. We dropped the `recipe_id` column from the RATINGS DataFrame because it contains the same information as `id` column from the RECIPES DataFrame in our merged DataFrame. We chose to keep only one column identifying each recipe for simplicity in our analysis. 
2. We then renamed the `id` column to `ID_recipe` to give it a meaningful name, emphasizing the information contained represents each recipe.
3. We cleaned the `nutrition` column, with each row containing the nutrition information of each recipe. We put each nutrition information into its own column. Since our question asks whether the saturated fat content of a recipe influence its average rating on the website, we only want to focus on analyzing saturated fat, not the entire nutrition information. With our cleaned data, we can focus on the saturated fat content of the recipe without overcomplicating our analysis process.
4. We then dropped the `nutrition` column because the nutrition information contained in the column is in their separate columns. Thus, we didn't need the `nutrition` column anymore. 

The first 5 rows of our DataFrame after cleaning, showing only columns relevant to our project:

| name                                 |   ID_recipe |   minutes | submitted   | tags                                                                                                                                                                                                                        | description                                                                                                                                                                                                                                                                                                                                                                       |          user_id | review                                                                                                                                                                                                                                                                                                                                           |   avg_rating |   saturated fat |
|:-------------------------------------|------------:|----------:|:------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------:|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------:|----------------:|
| 1 brownies in the world    best ever |      333281 |        40 | 2008-10-27  | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'for-large-groups', 'desserts', 'lunch', 'snacks', 'cookies-and-brownies', 'chocolate', 'bar-cookies', 'brownies', 'number-of-servings'] | these are the most; chocolatey, moist, rich, dense, fudgy, delicious brownies that you'll ever make.....sereiously! there's no doubt that these will be your fav brownies ever for you can add things to them or make them plain.....either way they're pure heaven!                                                                                                              | 386585           | These were pretty good, but took forever to bake.  I would send it ended up being almost an hour!  Even then, the brownies stuck to the foil, and were on the overly moist side and not easy to cut.  They did taste quite rich, though!  Made for My 3 Chefs.                                                                                   |            4 |              19 |
| 1 in canada chocolate chip cookies   |      453467 |        45 | 2011-04-11  | ['60-minutes-or-less', 'time-to-make', 'cuisine', 'preparation', 'north-american', 'for-large-groups', 'canadian', 'british-columbian', 'number-of-servings']                                                               | this is the recipe that we use at my school cafeteria for chocolate chip cookies. they must be the best chocolate chip cookies i have ever had! if you don't have margarine or don't like it, then just use butter (softened) instead.                                                                                                                                            | 424680           | Originally I was gonna cut the recipe in half (just the 2 of us here), but then we had a park-wide yard sale, & I made the whole batch & used them as enticements for potential buyers ~ what the hey, a free cookie as delicious as these are, definitely works its magic! Will be making these again, for sure! Thanks for posting the recipe! |            5 |              51 |
| 412 broccoli casserole               |      306168 |        40 | 2008-05-30  | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'side-dishes', 'vegetables', 'easy', 'beginner-cook', 'broccoli']                                                                        | since there are already 411 recipes for broccoli casserole posted to "zaar" ,i decided to call this one  #412 broccoli casserole.i don't think there are any like this one in the database. i based this one on the famous "green bean casserole" from campbell's soup. but i think mine is better since i don't like cream of mushroom soup.submitted to "zaar" on may 28th,2008 |  29782           | This was one of the best broccoli casseroles that I have ever made.  I made my own chicken soup for this recipe. I was a bit worried about the tsp of soy sauce but it gave the casserole the best flavor. YUM!                                                                                                                                  |            5 |              36 |
|                                      |             |           |             |                                                                                                                                                                                                                             |                                                                                                                                                                                                                                                                                                                                                                                   |                  | The photos you took (shapeweaver) inspired me to make this recipe and it actually does look just like them when it comes out of the oven.                                                                                                                                                                                                        |              |                 |
|                                      |             |           |             |                                                                                                                                                                                                                             |                                                                                                                                                                                                                                                                                                                                                                                   |                  | Thanks so much for sharing your recipe shapeweaver. It was wonderful!  Going into my family's favorite Zaar cookbook :)                                                                                                                                                                                                                          |              |                 |
| 412 broccoli casserole               |      306168 |        40 | 2008-05-30  | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'side-dishes', 'vegetables', 'easy', 'beginner-cook', 'broccoli']                                                                        | since there are already 411 recipes for broccoli casserole posted to "zaar" ,i decided to call this one  #412 broccoli casserole.i don't think there are any like this one in the database. i based this one on the famous "green bean casserole" from campbell's soup. but i think mine is better since i don't like cream of mushroom soup.submitted to "zaar" on may 28th,2008 |      1.19628e+06 | I made this for my son's first birthday party this weekend. Our guests INHALED it! Everyone kept saying how delicious it was. I was I could have gotten to try it.                                                                                                                                                                               |            5 |              36 |
| 412 broccoli casserole               |      306168 |        40 | 2008-05-30  | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'side-dishes', 'vegetables', 'easy', 'beginner-cook', 'broccoli']                                                                        | since there are already 411 recipes for broccoli casserole posted to "zaar" ,i decided to call this one  #412 broccoli casserole.i don't think there are any like this one in the database. i based this one on the famous "green bean casserole" from campbell's soup. but i think mine is better since i don't like cream of mushroom soup.submitted to "zaar" on may 28th,2008 | 768828           | Loved this.  Be sure to completely thaw the broccoli.  I didn&#039;t and it didn&#039;t get done in time specified.  Just cooked it a little longer though and it was perfect.  Thanks Chef.                                                                                                                                                     |            5 |              36 |

### Univariate Analysis

Distribution of Saturated Fat of Top 20 Recipes:
<iframe
  src="graphs/top_fig.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

This histogram shows the distribution of saturated fat content (in percent daily value) of the top 20 recipes. Most have between 20-60% daily value. 

Distribution of Saturated Fat of Worst 20 Recipes:
<iframe
  src="graphs/last_fig.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

The histogram shows the distribution of saturated fat content (in percent daily value) of the worst 20 recipes. While the graph only shows up to 120% daily value, there are recipes with saturated fat content above this threshold, unlike the top 20 recipes. 

### Bivariate Analysis

Distribution of Saturated Fat vs. Average Rating of All Recipes:
<iframe
  src="graphs/scatter_fig.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

This scatter plot shows the distribution of saturated fat content (in percent daily value) of all recipes in our dataset. The x-axis shows the saturated fat content, while the y-axis shows the average rating of each recipe. Most recipes have 0-200% daily value of saturated fat, and there is a higher proportion of recipes with 3-5 star ratings. 

### Interesting Aggregates

The aggregated statistics of `review` count and `avg_rating` mean per `user_id`, the contributor of each rating, of 5 users:

|   review |   avg_rating |
|---------:|-------------:|
|       79 |      4.34616 |
|        1 |      5       |
|        2 |      4.13462 |
|        2 |      5       |
|        1 |      5       |

The represented data is significant because it shows that the number of reviews and the average rating may not be correlated. It also shows that there are more active users who leave many reviews, and there are less active users to rarely leave reviews. However, both seem to have similar average ratings of recipes. 

## Assessment of Missingness

### NMAR Analysis

There are 3 columns with missing values: `name`, `description`, and `review`. Of these 3 columns, the column `description` is not missing at random (NMAR). The missingness of the `description` column depends on the `tags` column, which contains the Food.com tags for the recipe. Recipes of well-known foods with similar tags may be missing descriptions because many people know what food the recipe is about.

### Missingness Dependency

We ran a permutation test under the following hypotheses:

- **Null Hypothesis:** Average ratings of null reviews and non-null reviews come from the same distribution
- **Alternative Hypothesis:** Average ratings of non-null reviews are higher than average ratings of null reviews
- **Test Statistic:** Difference in group means

Our p-value was greater than 0.05, which meant we failed to reject the null hypothesis. This means the missingness of the `review` column might depend on the values in the `avg_rating` column. The missingness of recipe reviews might not depend on the average rating of the recipe.

This graph shows the relationship between missingness of the `review` column and the `avg_rating` column:
<iframe
  src="graphs/fig_bar.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

The difference between the average rating of those missing and those that have reviews is negligible, which is also reflected in our permutation test.

## Hypothesis Testing

- **Null Hypothesis:** There is no difference between the saturated fat content of the top 20 rated recipes and bottom 20 rated recipes. 
- **Alternative Hypothesis:** There IS a difference between the saturated fat content of the top and bottom 20 recipes. 

- **Test Statistic:** Difference in means of saturated fat content of both groups.
- **Significance Level:** 0.05 (If p-value < 0.05, we reject the null hypothesis. Otherwise, we fail to reject it.)

We ran a permutation test based on the above. These are good choices because we are trying to determine whether the distribution of the two samples, the saturated fat content of the best-rated 20 recipes and worst-rated 20 recipes, are draws from the same population. Since we want to determine that, we want to use difference in means of saturated fat content of both groups as the test statistic because the saturated fat content is a quantitative variable. 

Our p-value was 0.1433, which meant our p-value > 0.05. We failed to reject the null hypothesis. This shows that there could be no difference between the saturated fat content of the top 20 rated recipes and bottom 20 rated recipes.

## Framing a Prediction Problem

### Problem Identification

- **Our prediction question:** The number of minutes (`minutes`) it takes to prepare a recipe given the recipe rating (`avg_rating`).
- **Type of problem:** Regression
- **Response variable:** We chose the response variable `minutes` because understanding the correlation between it and the recipe rating can help users plan their time more efficiently.
- **Evaluation:** RMSE: RMSE penalizes larger errors more than smaller ones, which is crucial in providing accurate and reliable predictions for recipe preparation times.

## Baseline Model

We built a pipeline to predict `minutes` using `avg_rating` and `tags`. Our categorical features are `avg_rating` (ordinal) and `tags` (nominal). Our quantitative feature is `minutes`, which we aim to predict. We preprocess the data by one-hot-encoding `tags`. We then fit a linear regression model and evaluate its performance using RMSE and R^2.

Our model performs at an RMSE of 713.4. The RMSE is the square root of the average squared error. The median number of minutes (`minutes`) it takes to make a recipe is 39 mins. An RMSE of 713.4 indicates that the model's predictions will differ from the actual values by approximately 713.4 minutes, or ~11.90 hours. This is a rather large difference from the average recipe's cook time, so our model doesn't perform satisfactorily. To improve it for the final model, we plan on transforming existing features and fine-tuning our hyperparameters. 


## Final Model

## Fairness Analysis