# An Analysis of the Relationship Between Food Recipes and Their Ratings 

by Jason Kim

## Project Overview

This project is for DSC 80 at UCSD. The dataset that we used is from [food.com](https://www.food.com) and contains recipes and reviews from 2008.


## Introduction

Food is an essential resource that we as humans need in order to survive. With the introduction of the internet, food recipes are now able to be made and shared at a rate that has never been seen before. As mentioned in the Project Overview, our dataset contains data from the recipes and reviews that are posted on the website. Our goal with this project is to look through the data that we have and make predictions and draw conclusions based on what we observe. The question that we will be focusing on is: **Is there a correlation between the number of calories and the average rating that a recipe has?**

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