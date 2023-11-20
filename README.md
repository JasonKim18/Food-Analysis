# An Analysis of the Relationship Between Food Recipes and Their Ratings 

by Jason Kim

## Project Overview

This project is for DSC 80 at UCSD. The dataset that we used is from [food.com](https://www.food.com) and contains recipes and reviews from 2008.


## Introduction

Food is an essential resource that we as humans need in order to survive. With the introduction of the internet, food recipes are now able to be made and shared at a rate that has never been seen before. As mentioned in the Project Overview, our dataset contains data from the recipes and reviews that are posted on the website. Our goal with this project is to look through the data that we have and make predictions and draw conclusions based on what we observe. The question that we will be focusing on is:
**Is there a correlation between the number of calories and the average rating that a recipe has?**

Analyzing this dataset can prove to be useful as most people make conscious decisions about the dietary choices that they make for a varitey of reasons. Understading the correlation that exists between calories and recipe ratings can help guide users to making healtheir choices. Additionally it can also help chefs and people that make the recipes better understand the feedback given to them from the reviewers.

The first dataset that we will be looking at contains information regarding many unique recipes and some important information about them. Below is a table of the column names as well as a short description:

| Column          | Description                                                  |
| --------------- | ------------------------------------------------------------ |
| 'name'           | Recipe name                                                  |
| 'id'             | Recipe ID                                                    |
| 'minutes'        | Minutes to prepare recipe                                    |
| 'contributor_id' | User ID who submitted this recipe                            |
| 'submitted'      | Date recipe was submitted                                    |
| 'tags'           | Food.com tags for recipe                                     |
| 'nutrition'      | Nutrition information in the form [calories (#), total fat (PDV), sugar (PDV), sodium (PDV), protein (PDV), saturated fat (PDV), carbohydrates (PDV)]; PDV stands for “percentage of daily value” |
| 'n_steps'        | Number of steps in recipe                                    |
| 'steps'          | Text for recipe steps, in order                              |
| 'description'    | User-provided description                                    |

The Recipes dataset contains 83,782 rows, which represents the number of recipes that are on the website

The next dataset that we will be looking at contains information on the rating as well as the review that a commenter had to say regarding a specific recipe. Below is a table of the column names as well as a short description:

| Column     | Description          |
|------------|----------------------|
| 'user_id'  | User ID              |
| 'recipe_id'| Recipe ID            |
| 'date'     | Date of interaction  |
| 'rating'   | Rating given         |
| 'review'   | Review text          |

The Reviews dataset contains 731,927 rows, which represents the number of reviews that are on the website

## Cleaning and EDA (Exploratory Data Analysis)

### Data Cleaning
In order to ensure that the data that we had was in a usable format, we had to go through a series of steps to clean out our dataset and here are the steps that we took:

1. **Left merge the recipes and interactions datasets together.** This combines our two datasets into 1 that we can use to easily compare the information.
2. **Fill all ratings of 0 with np.nan.** Some people might not include a number in the rating so it is automatically filled in as 0. This would mess up our data since we don't know the real rating that the user felt about the food so we simply replace it with np.nan to ensure our calculations don't get skewed.
3. **Add a column for the average rating given for each recipe.** We combine the ratings given for each recipe by finding the mean. This is further justification for why we had to replace the 0's in the dataset so our average ratings wouldn't get dragged down in the case that someone left the rating section empty.
4. **Convert the nutrition column from a list of strings to their own columns.** We had to convert the strings of nutrition to floats of their respective values to make our data more usable. The new columns go as follow: 
['calories', 'total fat', 'sugar', 'sodium', 'protein', 'saturated fat', 'carbohydrates']
5. **Convert the 'submitted' column from a string into the datetime format.** This wasn't a necessary step as we don't need the time data, but we still converetd the times from a string to the datetime format in case we needed to use the data in the future
6. **Drop any unnecessary columns that we don't need.** We only kept the columns containing data that was relavent to our investigation

Here is what the first 5 lines of our cleaned dataframe look like after making the changes:

| name                                  | id     | rating | calories | total fat | sugar | sodium | protein | saturated fat | carbohydrates |
|---------------------------------------|--------|--------|----------|-----------|-------|--------|---------|---------------|---------------|
| 1 brownies in the world best ever     | 333281 | 4.0    | 138.4    | 10.0      | 50.0  | 3.0    | 3.0     | 19.0          | 6.0           |
| 1 in canada chocolate chip cookies    | 453467 | 5.0    | 595.1    | 46.0      | 211.0 | 22.0   | 13.0    | 51.0          | 26.0          |
| 412 broccoli casserole                | 306168 | 5.0    | 194.8    | 20.0      | 6.0   | 32.0   | 22.0    | 36.0          | 3.0           |
| millionaire pound cake               | 286009 | 5.0    | 878.3    | 63.0      | 326.0 | 13.0   | 20.0    | 123.0         | 39.0          |
| 2000 meatloaf                         | 475785 | 5.0    | 267.0    | 30.0      | 12.0  | 12.0   | 29.0    | 48.0          | 2.0           |

### Univariate Analysis

<iframe src="assets/fig_rating.html" width=800 height=600 frameBorder=0></iframe>

This plot shows that the distribution of ratings is heavily skewed to the left with most of the rating being between 4.5 and 5 stars

### Bivariate Analysis

<iframe src="assets/fig_scatter.html" width=800 height=600 frameBorder=0></iframe>

This plot shows the relationship between the number of calories and the average rating that a recipe has. Something to note is that we left out recipes that were an outlier as they had more than 5000 calories. From this, we can see that most of the data points are below 200 calories, and there is a big chunk of the data at the top left, which means they are rated highly and have low calories

### Interesting Aggregates

| rating_section | calories     | protein     |
|-----------------|--------------|-------------|
| (0, 1]          | 445.615110   | 29.485569   |
| (1, 2]          | 462.407825   | 31.687011   |
| (2, 3]          | 436.940372   | 33.454647   |
| (3, 4]          | 426.950824   | 35.281046   |
| (4, 5]          | 426.305842   | 32.656086   |

For this pivot table we had to make sections that divided up the recipes by the ranges of their ratings. This allowed us to view the means of the calories and protein for each individuial section. Seeing this we can see that while there are slight differneces, they are generally pretty even across the differnt ratings.

## Assessment of Missingness

### NMAR Analysis

From our dataset, a column that could be missing values due to NMAR is 'review.' This is because the reviewrs might not include a reivew in their comment as they don't feel too strongly or have any opinions to voice. But if they did have a big complaint or thought that the recipe was really good, they would usually include a review in their response. As a result, the conscious chpoice of users to not write a review based on their lack of strong opinions would lead to the 'review' column being NMAR.

## Missingness Dependency

To look at the dependency of missing values in the 'rating' section, we willl first be comparing it to the 'protein' column. 

Null Hypothesis: There is no significant difference between the 'rating' and the 'protein' of a recipe
Alternative Hypothesis: There is a significant difference between the 'rating' and the 'protein' of a recipe

We shuffle our data 1000 times to compare the differnce of means and the results that we get are shown below:

<iframe src="assets/permutation_test.html" width=800 height=600 frameBorder=0></iframe>

After running a permutation test on our data, we found that the p-value to equal 0.2010. The P-value is greater than our significance level of 0.05 so we fail to reject the null hypothesis. This means there is **NO** significant evidence that missingness in 'rating' **depends** on values in 'protein' 


To look at the dependency of missing values in the 'rating' section, we willl first be comparing it to the 'protein' column. 

Null Hypothesis: There is no significant difference between the 'rating' and the 'calories' of a recipe
Alternative Hypothesis: There is a significant difference between the 'rating' and the 'calories' of a recipe

We shuffle our data 1000 times to compare the differnce of means and the results that we get are shown below:

<iframe src="assets/permutation_test_2.html" width=800 height=600 frameBorder=0></iframe>

After running a permutation test on our data, we found that the p-value to equal 0.0. The P-value is less than our significance level of 0.05 so we reject the null hypothesis. This means there **IS** evidence that missingness in 'rating' **depends** on values in 'calories' 

## Hypothesis Testing

The question that we will be looking at for this hypothesis test is the same as the one listed at the very beginning:
Is there a correlation between the number of calories and the average rating that a recipe has?

But the only differnece is that to specify the difference in calories, we define a "large meal" as a meal that has over 600 calories. So we will make this distinction going forward with the rest of our hypothesis test.

Null Hypothesis: There is no correlation between the average rating of large meals (meals above 600 calories) and small meals (meals less than or equal to 600 calories).
Alternative Hypothesis: There is a correlation between the average rating of large meals (meals above 600 calories) and small meals (meals less than or equal to 600 calories).

For this hypothesis test, we had to create a new column that was the boolean value of if each recipe was a large meal or not. We then took 1000 random shuffles of this column to calculate if there is differnece in means. The results that we found from this simulation are found below:

<iframe src="assets/hypothesis_test.html" width=800 height=600 frameBorder=0></iframe>

From this test, we found that the P-value of the test to be 0.5570. The P-value is greater than our significance level of 0.05 so we fail to reject the null hypothesis. This means is **NO** significant evidence that that there is a correlation between the number of calories and the average rating of a recipe.