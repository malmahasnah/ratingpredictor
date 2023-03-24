# rating predictor
This is the final project for DSC 80.

## Framing the Problem

We are predicting the ratings of recipes (using linear regression) and we are using the rating column which tells us what the recipe ratings are. We did some data cleaning so that the rating column tells us what the average rating of each recipe is. We used RMSE because ..

The information we know about a certain recipe when we are predicting its rating consist of the recipe's nutrition information, the number of ingredients, the number of steps and number of minutes (i.e how long it takes to make the recipe).


> Our exploratory data analysis on this dataset can be found [here](https://hunterbrownell.github.io/recipe_project/)


## Baseline Model

Our model uses eight quantitative features, seven of which we took out of the `nutrition` column; we extracted each one so that we had `calories`, `total fat`, `sugar`, `sodiuum`, `protein`, `saturated fat`, and `carbohydrates`. We standardized each column according to its group (i.e we standardized the `calories` column using only the values in it); so for that we created our own helper function, since there is no built in `sklearn` function that standardizes each category according to its group. We also used the number of steps; we binarized the `n_steps` column and used the median as a threshold. our RMSE was 0.6408576663883866. We think that this model is good/bad, because...


## Final Model 

For our final model, we added two quantitative features: the number of minutes and number of reviews, and we also used the ingredients; we approached this by picking the top `n` most common ingredients in all the recipes. We thought using the `minutes` column would better help us predict because intuitively, the amount of time it would take to make a recipe plays a role in how a person might judge that recipe (i.e recipes that take a shorter amount of time to make and end up being good are more likely to receive a better review, and a recipe that takes longer to make and turns out mediocre is less likely to receive a good review). using the `num_reviews` column would also improve our model, since the number of reviews each recipe has would impact its average rating! (e.g if a recipe only has one five star review it should be treated differently from a recipe that has 100 reviews with an average of 3.7). 
We used `StandardScaler` for the `num_reviews` column, and `QuantileTransformer` for the `minutes` column. 
We used a `DecisionTreeRegressor` and used Grid Search in order to find the best hyperparamters between `max_depth` and `min_samples_split`. the best hyperparameters ended up being `{'max_depth': 4, 'min_samples_split': 30}`. Our RMSE this time was ..., which is an improvement from our Baseline model considering the features we added and the hyperparameters we used.

## Fairness Analysis

For our fairness analysis, our two groups were the group of recipes with only one rating, and the group of recipes with more than one rating. Our evaluation metric was once again the RMSE. our hypotheses were:
>> null hypothesis: the RMSE is the same for recipes with 1 review and for recipes with more than 1 review and the difference is is due to random chance.
>> alternative hypothesis: RMSE is lower for recipes with one review than it is for recipes with more than one review.

For our test statistic we used the difference in RMSEs for the two groups. We chose 0.05 for our significance level.

Our *p*-value was ... That told us that we should reject the null hypothesis, which means our model is **not fair** and generally performs better on groups of recipes with more than one rating.











