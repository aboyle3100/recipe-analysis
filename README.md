# **Inner Machinations of a Good Recipe**

Andrew Boyle 

DSC 80 Final Project UCSD

## **Introduction**

The dataset used is the recipes and ratings dataset.    

The original dataset is made up of 10 features.
<table>
  <thead>
    <tr>
      <th style="text-align: left">Column</th>
      <th style="text-align: left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align: left"><code class="language-plaintext highlighter-rouge">'name'</code></td>
      <td style="text-align: left">Recipe name</td>
    </tr>
    <tr>
      <td style="text-align: left"><code class="language-plaintext highlighter-rouge">'id'</code></td>
      <td style="text-align: left">Recipe ID</td>
    </tr>
    <tr>
      <td style="text-align: left"><code class="language-plaintext highlighter-rouge">'minutes'</code></td>
      <td style="text-align: left">Minutes to prepare recipe</td>
    </tr>
    <tr>
      <td style="text-align: left"><code class="language-plaintext highlighter-rouge">'contributor_id'</code></td>
      <td style="text-align: left">User ID who submitted this recipe</td>
    </tr>
    <tr>
      <td style="text-align: left"><code class="language-plaintext highlighter-rouge">'submitted'</code></td>
      <td style="text-align: left">Date recipe was submitted</td>
    </tr>
    <tr>
      <td style="text-align: left"><code class="language-plaintext highlighter-rouge">'tags'</code></td>
      <td style="text-align: left">Food.com tags for recipe</td>
    </tr>
    <tr>
      <td style="text-align: left"><code class="language-plaintext highlighter-rouge">'nutrition'</code></td>
      <td style="text-align: left">Nutrition information in the form [calories (#), total fat (PDV), sugar (PDV), sodium (PDV), protein (PDV), saturated fat (PDV), carbohydrates (PDV)]; PDV stands for “percentage of daily value”</td>
    </tr>
    <tr>
      <td style="text-align: left"><code class="language-plaintext highlighter-rouge">'n_steps'</code></td>
      <td style="text-align: left">Number of steps in recipe</td>
    </tr>
    <tr>
      <td style="text-align: left"><code class="language-plaintext highlighter-rouge">'steps'</code></td>
      <td style="text-align: left">Text for recipe steps, in order</td>
    </tr>
    <tr>
      <td style="text-align: left"><code class="language-plaintext highlighter-rouge">'description'</code></td>
      <td style="text-align: left">User-provided description</td>
    </tr>
  </tbody>
</table>

Number of Rows: 234429    

Relevant Columns (4):
- nutrition
  - Contains information on calories, sugar, sodium, protein, saturated fat, and carbohydrates
  - Can be used to analyze the recipes by type of nutrition in the recipe
- n_steps
  - helpful to use as an interaction variable later
- rating
  - helps train the model to predict a rating of a recipe
- steps
  - contains textual data formulating the steps taken in the recipe
  - could be used as a proxy for a complexity feature  



## **Data Cleaning and Exploratory Data Analysis**
Describe, in detail, the data cleaning steps you took and how they affected your analyses. The steps should be explained in reference to the data generating process. Show the head of your cleaned DataFrame (see Part 2: Report for instructions).

<iframe
  src="assets/calories-by-rating.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

#### Data Cleaning
1. Merge relevant data from the raw interactions and raw recipes dataset
2. Add a feature for average rating indicating the average rating received by that recipe
3. assign recipes with ratings of 0 to nan
4. Add feature for each unique element (5) in the nutrition column corresponding with the relevant nutrition fact
5. Convert columns with dates as strings to date time objects
6. Convert columns of list strings to lists
7. Create columns for nutrition related columns as proportion makeup of the recipe
8. Create column for average step length
9. Create column for interaction between n_steps and average_step_length

<iframe
  src="assets/cleaned_df.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

#### Univariate Analysis
ADD MORE IN Future with different types

<iframe
  src="assets/ingredients_per_recipe.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

The distribution of amounts of ingredients per recipe looks roughly normal, however K-S hyporthesis testing could be done to confirm


#### Bivariate Analysis
<iframe
  src="assets/calories-by-rating.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

> Based on the box plot it appears the amount of calories in the recipe and the rating are not correlated 

#### Interesting Aggregates

## **Assignment of Missingness**

#### NMAR Analysis

#### Missingness Dependency

## **Hypothesis Testing**

## **Framing a Prediction Problem**

#### Problem Identification

## **Baseline Model**

## **Final Model**

## **Fairness Analysis**

## Modeling rating by calories 

