# Recipes-Rating-Prediction-Model

This is the Project 3 under course DSC80

By Jiangqi Wu & Yuxuan Zhang

## Problem Identification

Can we accurately predict the average rating ('ave_rating') of a recipe based on its features such as cooking time ('minutes'), nutritional information ('nutrition', 'calories', 'total fat (PDV)', 'sugar (PDV)'), number of steps ('n_steps'), and number of ingredients ('n_ingredients') in a comprehensive recipe dataset?

This is a regression problem since we aim to predict a continuous outcome, the 'ave_rating', which is a numeric value ranging from 0 to 5.

The significance of predicting the response variable, average rating of a recipe, lies in its potential impact on various stakeholders in the culinary industry. It can serve as a valuable tool for recipe creators and chefs, enabling them to understand what variables might influence the perceived quality and popularity of their recipes. By identifying these variables, they can optimize their recipes for maximum satisfaction, thereby increasing their popularity and reach. For culinary websites and platforms, this predictive model can inform system design to promote recipes with higher predicted ratings, enhancing user engagement and overall platform success.

The model will be evaluated using the Root Mean Square Error (RMSE) anr R^2 as a key metric. The choice of RMSE is predicated on its ability to magnify and hence, draw particular attention to large errors, given its computation involves squaring the error term. This property of RMSE is valuable as we aim to design a prediction model for recipe creators and website operators where the importance of delivering consistently high-quality, popular recipes is crucial.

Consistent accuracy in predicting recipe ratings is a significant strategic consideration for these stakeholders. For recipe creators, a large deviation in predicted and actual ratings could mean a mismatch between the efforts invested in the recipe and the response received, thereby affecting their reputation and follower engagement. For website operators, erroneous prediction could lead to poor recipe recommendations, adversely impacting user experience and engagement on their platform.

By using RMSE, our model is tuned to avoid large errors, thus supporting the stability of the recipe design process and subsequent user experience. The lower the RMSE, the more accurately our model predicts, enhancing the reliability of insights gained from this research, thereby enabling recipe creators to optimize their recipes effectively and culinary platforms to deliver superior user experience.

In addition to RMSE, we will also use R^2 (coefficient of determination) as a key metric to assess the performance of our model. R^2 represents the proportion of the variance for our dependent variable, the 'ave_rating', that's predictable from the independent variables (features of the recipes).

R^2 is essential as it provides an intuitive measure of how much of the variation in our outcome can be explained by our model. In essence, a high R^2 indicates that our model can explain a large proportion of the variability in the recipe rating, which is a desirable characteristic.

## Baseline Model

In the Baseline Model, we are using the `minutes` and `ingredients` to predict average rating for a recipe. We are using a polynomial model to predict.

In the model, we are using quantitative data including 
