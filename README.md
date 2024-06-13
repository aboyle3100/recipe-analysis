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


<!--  -->
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
10. Convert ratings columns to ints to be later used in model evaluation
11. Include a sugar feature which returns true if there is sugar in the name

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

The distribution of amounts of ingredients per recipe looks roughly normal, however K-S hypothesis testing could be done to confirm.










#### Bivariate Analysis
<iframe
  src="assets/calories-by-rating.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>


> Based on the box plot it appears the amount of calories in the recipe and the rating are not correlated 














#### Interesting Aggregates


(dataframe of saturated fat and rankings together in a grouped table)
The saturated fat content appears to be higher in recipes with lower ratings on average.

(pivot table indexed by ratings with columns showing mean calories, ingredients, and steps per rating)
Calorie counts tend to go down as ratings increase while ingredients stays the same. Additionally, mean stpes decreases on average as rating goes down 

<!--  -->
 STILL NEED TO ADD PLOTS FOR THIS TO GO ALONG. USE PLOT_KDE
## **Assignment of Missingness**

NMAR Definition: The missingness of a column is dependent on another column in a dataset

MAR Definition: The missingness of a column is dependent on the missing values themselves
<!--  -->












#### NMAR Analysis
Testing whether review missingness is dependent on rating.
    
#### Procedure:    
Using K-S Statistic as test statistic,    
##### Null Hypothesis:    
- Missingness of review is not dependent on rating. They have the same distribution.    
##### Alternative Hypothesis:   
- The distribution of ratings is different for columns missing reviews.   

With a p-value of 0.9989, we fail to reject the null hyporthesis that distributions of rating is different for columns missing reviews. This indicates that missingness of review not dependent on rating.
<!--  -->





#### Missingness Dependency

Procedure:    
Using K-S Statistic as test statistic,    
##### Null Hypothesis:    
- Missingness of steps is not dependent on rating. They have the same distribution.    
##### Alternative Hypothesis:   
- The distribution of steps is different for columns missing reviews.   

With a p-value of 0.9989, we fail to reject the null hyporthesis that distributions of rating is different for columns missing reviews. This indicates that missingness of review does not dependent on rating.




<!--  -->






## **Hypothesis Testing**

#### Recipe Time

#### Procedure: 
Using permutation testing with absolute difference of means as the test statistic

##### Null Hypothesis:
- Longer recipes are rated the same as shorter recipes

##### Alternative Hypothesis:
- Longer and shorter recipes are rated differently

<iframe
  src="assets/longer_shorter_ratings.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

With a p value of 0.00, we reject the null hypothesis in favor of the alternative that longer recipes are rated differently than shorter recipes.





#### Protein as proportion and Recipe Rating

##### Null Hypothesis:
- Recipes with higher protein proportions have the same rating as recipes with lower protein proportions

##### Alternative Hypothesis:
- Recipes with higher protein proportions have lower ratings than recipes with lower protein proportions

<iframe
  src="assets/protein proportion and rating.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

With a p value of 0.00, we reject the null hypothesis in favor of the alternative that recipes with higher protein proportions have lower ratings than recipes with lower protein proportions.

<!--  -->

## **Framing a Prediction Problem**

I am going to make two prediction problems trying to solve similar problems. I will use one Classification and One Linear Regression Model. Both models try to predict the rating based on features. 

#### Regression Problem
Metric: RMSE
This regression model will predict average rating of a recipe. This would be as opposed to using rating which differs accross the same recipes. RMSE would be used here for its easier interpretability as compared to the MSE. 


#### Classification Problem
Metric: F1-Score    
This would be a multiclass classification problem which predicts ratings based on the features in the dataset. I will utilize both GridSearchCV as well as a random forest to make these predictions. I would choose the F1 Score in this case because there is a large presence of one rating in the training data. The combination this and using accuracy as a metric leads to a model that is incentivized to predict one rating every time. F1 score also captures a good ratio of precision and recall


<!--  -->

## **Baseline Model**

#### Regression Model
RMSE Score: 0.49, R^2: 0.0002369  
Features: 'calories(number)' (quantitative), 'minutes' (quantitative)   
Predicting: Average Rating

#### Classification Problem

F1_score: .674, .676 for training and testing sets respectively
Features: 'calories(number)' (quantitative), 'minutes' (quantitative)   
Predicting: Rating

## **Final Model**

#### Regression Model

RMSE Score: 0.4925110755228968, 0.4943589840553027 for train and test data respectively
Features: 'calories(number)' (quantitative), 'n_steps' (quantitative), 'sugar' (categorical), 'minutes' (quantitative), 'protein(proportion)' (quantitative), 'n_steps_average_step_length' (quantitative)     
Predicting: Average Rating

#### Classification Model 

F1_score: 0.6748, 0.6728 for training and testing sets respectively
Features: 'calories(number)' (quantitative), 'n_steps' (quantitative), 'sugar' (categorical), 'minutes' (quantitative), 'protein(proportion)' (quantitative), 'n_steps_average_step_length' (quantitative)   
Predicting: Rating

Best Parameters: 'class_weight': {1: 4, 2: 4, 3: 4, 4: 5, 5: 6}, 'max_depth': 10

## **Fairness Analysis**

## Modeling rating by calories 

