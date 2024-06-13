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


This project takes a deep dive into the realm of recipe rating prediction. Involved in this analysis are hypothesis testing, missing value analysis and other types of statistical testing useful for a cooking that can be considered by some to be more of an art than a science. 

<!--  -->
## **Data Cleaning and Exploratory Data Analysis**

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


#### Head of the cleaned dataframe

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>id</th>
      <th>minutes</th>
      <th>contributor_id</th>
      <th>submitted</th>
      <th>tags</th>
      <th>n_steps</th>
      <th>steps</th>
      <th>description</th>
      <th>ingredients</th>
      <th>n_ingredients</th>
      <th>user_id</th>
      <th>recipe_id</th>
      <th>date</th>
      <th>rating</th>
      <th>review</th>
      <th>average_rating</th>
      <th>calories(number)</th>
      <th>total_fat(PDV)</th>
      <th>sugar(PDV)</th>
      <th>sodium(PDV)</th>
      <th>protein(PDV)</th>
      <th>saturated_fat(PDV)</th>
      <th>carbohydrates(PDV)</th>
      <th>average_step_length</th>
      <th>total_fat(proportion)</th>
      <th>sugar(proportion)</th>
      <th>sodium(proportion)</th>
      <th>protein(proportion)</th>
      <th>saturated_fat(proportion)</th>
      <th>carbohydrates(proportion)</th>
      <th>n_steps_average_step_length</th>
      <th>sugar</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1 brownies in the world    best ever</td>
      <td>333281</td>
      <td>40</td>
      <td>985201</td>
      <td>2008-10-27</td>
      <td>[60-minutes-or-less, time-to-make, course, main-ingredient, preparation, for-large-groups, desserts, lunch, snacks, cookies-and-brownies, chocolate, bar-cookies, brownies, number-of-servings]</td>
      <td>10</td>
      <td>[heat the oven to 350f and arrange the rack in the middle, line an 8-by-8-inch glass baking dish with aluminum foil, ... before cutting]</td>
      <td>these are the most; chocolatey, ... they're pure heaven!</td>
      <td>[bittersweet chocolate, unsalted butter, eggs, granulated sugar, unsweetened cocoa powder, vanilla extract, brewed espresso, kosher salt, all-purpose flour]</td>
      <td>9</td>
      <td>3.87e+05</td>
      <td>333281.0</td>
      <td>2008-11-19</td>
      <td>4.0</td>
      <td>These were pretty ... for My 3 Chefs.</td>
      <td>4.0</td>
      <td>138.4</td>
      <td>10.0</td>
      <td>50.0</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>19.0</td>
      <td>6.0</td>
      <td>12.80</td>
      <td>0.11</td>
      <td>0.55</td>
      <td>0.03</td>
      <td>0.03</td>
      <td>0.21</td>
      <td>0.07</td>
      <td>128.0</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1 in canada chocolate chip cookies</td>
      <td>453467</td>
      <td>45</td>
      <td>1848091</td>
      <td>2011-04-11</td>
      <td>[60-minutes-or-less, time-to-make, cuisine, preparation, north-american, for-large-groups, canadian, british-columbian, number-of-servings]</td>
      <td>12</td>
      <td>[pre-heat oven the ... and enjoy !]</td>
      <td>this is the recipe that we use at my school cafeteria for chocolate chip cookies. they must be the best chocolate chip cookies i have ever had! if you don't have margarine or don't like it, then just use butter (softened) instead.</td>
      <td>[white sugar, brown sugar, salt, margarine, eggs, vanilla, water, all-purpose flour, whole wheat flour, baking soda, chocolate chips]</td>
      <td>11</td>
      <td>4.25e+05</td>
      <td>453467.0</td>
      <td>2012-01-26</td>
      <td>5.0</td>
      <td>Originally I was gonna cut the recipe in half (just the 2 of us here), but then we had a park-wide yard sale, &amp; I made the whole batch &amp; used them as enticements for potential buyers ~ what the hey, a free cookie as delicious as these are, definitely works its magic! Will be making these again, for sure! Thanks for posting the recipe!</td>
      <td>5.0</td>
      <td>595.1</td>
      <td>46.0</td>
      <td>211.0</td>
      <td>22.0</td>
      <td>13.0</td>
      <td>51.0</td>
      <td>26.0</td>
      <td>12.33</td>
      <td>0.12</td>
      <td>0.57</td>
      <td>0.06</td>
      <td>0.04</td>
      <td>0.14</td>
      <td>0.07</td>
      <td>148.0</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>412 broccoli casserole</td>
      <td>306168</td>
      <td>40</td>
      <td>50969</td>
      <td>2008-05-30</td>
      <td>[60-minutes-or-less, time-to-make, course, main-ingredient, preparation, side-dishes, vegetables, easy, beginner-cook, broccoli]</td>
      <td>6</td>
      <td>[preheat oven to 350 degrees, ... cheese is bubbly , about 10 more minutes]</td>
      <td>since there are already 411 recipes for broccoli casserole posted to "zaar" ,i decided to call this one  #412 broccoli casserole.i don't think ... to "zaar" on may 28th,2008</td>
      <td>[frozen broccoli cuts, cream of chicken soup, sharp cheddar cheese, garlic powder, ground black pepper, salt, milk, soy sauce, french-fried onions]</td>
      <td>9</td>
      <td>2.98e+04</td>
      <td>306168.0</td>
      <td>2008-12-31</td>
      <td>5.0</td>
      <td>This was one of the best broccoli ... recipe shapeweaver. It was wonderful!  Going into my family's favorite Zaar cookbook :)</td>
      <td>5.0</td>
      <td>194.8</td>
      <td>20.0</td>
      <td>6.0</td>
      <td>32.0</td>
      <td>22.0</td>
      <td>36.0</td>
      <td>3.0</td>
      <td>15.33</td>
      <td>0.17</td>
      <td>0.05</td>
      <td>0.27</td>
      <td>0.18</td>
      <td>0.30</td>
      <td>0.03</td>
      <td>92.0</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3</th>
      <td>412 broccoli casserole</td>
      <td>306168</td>
      <td>40</td>
      <td>50969</td>
      <td>2008-05-30</td>
      <td>[60-minutes-or-less, time-to-make, course, main-ingredient, preparation, side-dishes, vegetables, easy, beginner-cook, broccoli]</td>
      <td>6</td>
      <td>[preheat oven to 350 degrees, ... 10 more minutes]</td>
      <td>since there are already ... to "zaar" on may 28th,2008</td>
      <td>[frozen broccoli cuts, cream of chicken soup, sharp cheddar cheese, garlic powder, ground black pepper, salt, milk, soy sauce, french-fried onions]</td>
      <td>9</td>
      <td>1.20e+06</td>
      <td>306168.0</td>
      <td>2009-04-13</td>
      <td>5.0</td>
      <td>I made this for my son's first birthday party this weekend. Our guests INHALED it! Everyone kept saying how delicious it was. I was I could have gotten to try it.</td>
      <td>5.0</td>
      <td>194.8</td>
      <td>20.0</td>
      <td>6.0</td>
      <td>32.0</td>
      <td>22.0</td>
      <td>36.0</td>
      <td>3.0</td>
      <td>15.33</td>
      <td>0.17</td>
      <td>0.05</td>
      <td>0.27</td>
      <td>0.18</td>
      <td>0.30</td>
      <td>0.03</td>
      <td>92.0</td>
      <td>False</td>
    </tr>
    <tr>
      <th>4</th>
      <td>412 broccoli casserole</td>
      <td>306168</td>
      <td>40</td>
      <td>50969</td>
      <td>2008-05-30</td>
      <td>[60-minutes-or-less, time-to-make, course, main-ingredient, preparation, side-dishes, vegetables, easy, beginner-cook, broccoli]</td>
      <td>6</td>
      <td>[preheat oven to 350 degrees, ... minutes]</td>
      <td>since there are already 411 ... on may 28th,2008</td>
      <td>[frozen broccoli cuts, cream of chicken soup, sharp cheddar cheese, garlic powder, ground black pepper, salt, milk, soy sauce, french-fried onions]</td>
      <td>9</td>
      <td>7.69e+05</td>
      <td>306168.0</td>
      <td>2013-08-02</td>
      <td>5.0</td>
      <td>Loved this.  Be sure to completely thaw the broccoli.  I didn&amp;#039;t and it didn&amp;#039;t get done in time specified.  Just cooked it a little longer though and it was perfect.  Thanks Chef.</td>
      <td>5.0</td>
      <td>194.8</td>
      <td>20.0</td>
      <td>6.0</td>
      <td>32.0</td>
      <td>22.0</td>
      <td>36.0</td>
      <td>3.0</td>
      <td>15.33</td>
      <td>0.17</td>
      <td>0.05</td>
      <td>0.27</td>
      <td>0.18</td>
      <td>0.30</td>
      <td>0.03</td>
      <td>92.0</td>
      <td>False</td>
    </tr>
  </tbody>
</table>




<iframe
  src="assets/corr_mat.html"
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


> Based on the box plot it appears the amount of calories in the recipe and the rating are not correlated.














#### Interesting Aggregates


<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>saturated_fat(PDV)</th>
    </tr>
    <tr>
      <th>rating</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1.0</th>
      <td>46.68</td>
    </tr>
    <tr>
      <th>2.0</th>
      <td>42.88</td>
    </tr>
    <tr>
      <th>3.0</th>
      <td>40.09</td>
    </tr>
    <tr>
      <th>4.0</th>
      <td>36.43</td>
    </tr>
    <tr>
      <th>5.0</th>
      <td>39.23</td>
    </tr>
  </tbody>
</table>


The saturated fat content appears to be higher in recipes with lower ratings on average.

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>calories(number)</th>
      <th>n_ingredients</th>
      <th>n_steps</th>
    </tr>
    <tr>
      <th>rating</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1.0</th>
      <td>486.60</td>
      <td>8.91</td>
      <td>10.63</td>
    </tr>
    <tr>
      <th>2.0</th>
      <td>446.60</td>
      <td>9.23</td>
      <td>10.70</td>
    </tr>
    <tr>
      <th>3.0</th>
      <td>425.79</td>
      <td>9.20</td>
      <td>9.99</td>
    </tr>
    <tr>
      <th>4.0</th>
      <td>405.05</td>
      <td>9.10</td>
      <td>9.58</td>
    </tr>
    <tr>
      <th>5.0</th>
      <td>415.21</td>
      <td>9.05</td>
      <td>9.98</td>
    </tr>
  </tbody>
</table>

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

<iframe
  src="assets/missing review rating.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>



#### Missingness Dependency

Procedure:    
Using K-S Statistic as test statistic,    
##### Null Hypothesis:    
- Missingness of steps is not dependent on rating. They have the same distribution.    
##### Alternative Hypothesis:   
- The distribution of steps is different for columns missing reviews.   

With a p-value of 0.01462006091994894, we reject the null hyporthesis in favor of the alternative hypothesis that the missingness of steps is dependent on rating.


<iframe
  src="assets/missing rating steps.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>



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



I include calories and minutes as base features in both models which could be potential factors in creating a rating for a recipe. If a recipe is overly long, it makees sense that it would receive a worse score. 

## **Final Model**

#### Regression Model

RMSE Score: 0.4925110755228968, 0.4943589840553027 for train and test data respectively
Features: 'calories(number)' (quantitative), 'n_steps' (quantitative), 'sugar' (categorical), 'minutes' (quantitative), 'protein(proportion)' (quantitative), 'n_steps_average_step_length' (quantitative)     
Predicting: Average Rating

The RMSE stayed roughly the same as the original model. This leads me to believe that adding additionaly features to the model may not help lower the RMSE. 

#### Classification Model 

F1_score: 0.6835064424796619, 0.6777402884352648 for training and testing sets respectively
Features: 'calories(number)' (quantitative), 'n_steps' (quantitative), 'sugar' (categorical), 'minutes' (quantitative), 'protein(proportion)' (quantitative), 'n_steps_average_step_length' (quantitative)   
Predicting: Rating

Best Parameters: 'class_weight': {1: 4, 2: 4, 3: 4, 4: 5, 5: 6}, 'max_depth': 10

Instead of Using the default accuracy as a scorer, I introduced a new way to score the model using the sklearn F1-Score and make scorer methods. This should allow for a model that works more fairly and as intended. Some of the features I've included include an interaction feature 'n_steps_average_step_length' which is a product of the two features. My reason for doing this has to do with domain experience in that more complicated and longer recipes are more likely to be rated lower. This model has a marginally higher f1_score than the baseline model.


## **Fairness Analysis**

Fairness analysis for long recipes:
First must binarize column by taking values above and below the mean n_steps. 

Procedure:    
Using absolute difference of means as test statistic,    
##### Null Hypothesis:    
- Our model is fair. There is not a difference in f1_score for long and short recipes   
##### Alternative Hypothesis:   
- Our model is unfair. There is a difference in f1_score for long and short recipes   

With a p value of     we fail to reject the null hypothesis. As such our model is fair for long recipes. 

