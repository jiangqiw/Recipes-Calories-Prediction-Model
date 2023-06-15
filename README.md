# Recipes-Rating-Prediction-Model

This is the Project 3 under course DSC80

By Jiangqi Wu & Yuxuan Zhang

## Problem Identification

In this research project, we are aiming to accurately predict the caloric content ('calories') of a recipe based on its features such as cooking time (`minutes`), description (`description`), and other nutritional information (`nutrition`, `total fat (PDV)`, `sugar (PDV)`), the number of steps (`n_steps`), and the number of ingredients (`n_ingredients`) in a comprehensive recipe dataset.

This is a regression problem since we aim to predict a continuous outcome, the `calories`, which is a numeric value.

The significance of predicting the response variable, caloric content of a recipe, lies in its potential impact on various stakeholders in the culinary and health industry. It can serve as a valuable tool for recipe creators, dieticians, and health-conscious consumers, enabling them to understand what variables might influence the caloric content of their recipes. By identifying these variables, they can optimize their recipes for maximum nutritional efficiency, thereby assisting in maintaining a healthy lifestyle.

The model will be evaluated using the Root Mean Square Error (RMSE) and R^2 as key metrics. The choice of RMSE is based on its ability to amplify and hence, highlight large errors. This property of RMSE is valuable as we aim to design a prediction model where the importance of delivering consistent and accurate caloric information is crucial.

By using RMSE, our model is tuned to avoid large errors, thus supporting the reliability of nutritional information. The lower the RMSE, the more accurately our model predicts, enhancing the reliability of insights gained from this research, thereby enabling individuals to optimize their dietary choices effectively.

In addition to RMSE, we will also use R^2 (coefficient of determination) as a key metric to assess the performance of our model. R^2 represents the proportion of the variance for our dependent variable, the 'calories', that's predictable from the independent variables (features of the recipes).

R^2 is essential as it provides an intuitive measure of how much of the variation in our outcome can be explained by our model. In essence, a high R^2 indicates that our model can explain a large proportion of the variability in the caloric content, which is a desirable characteristic.

## Baseline Model

#### Brief Introduction

In the Baseline Model, we are using the number of steps in the recipes `n_steps` and then number of ingredients `n_ingredients` to predict the calories for the recipes. We will be using 2 quantitative variables, and no ordinal and nominal variable to build the regression model.

#### Data encoding

For the two random variable, we will be applying `StandardScaler` to standalize `n_steps` and directly use `ave_rating`.

#### Model Description and Performance

We will be using linear regression model in the `sklearn` to build up the regression model. The linear regression model will predict the calories of a recipe with a polynomial with at most degree of one.

The performance of your current model, as indicated by the R^2 value, is not very strong. The R^2 value of 0.0217 implies that only approximately 2.17% of the variability in the calorie content can be explained by the variables 'n_steps' and 'n_ingredients'. This suggests that these features might not be the most influential factors when it comes to predicting calorie content, or that the relationship between these features and calories might not be linear, as assumed by the linear regression model.

Additionally, the RMSE (Root Mean Squared Error) of the model is 26.447. The RMSE is a measure of the differences between the values predicted by the model and the actual values. This value is not low enough to guarantee a accurate model. 

Also, using the data visualization, we can have a look at the model.

The model can not correctly predic the calories of recipes since not enough feature and the recipes are clustered, making it hard to make precise prediction.


