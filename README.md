# Recipes-Calories-Prediction-Model

This is the Project 5 under course DSC80

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

### Brief Introduction

In the Baseline Model, we are using the number of steps in the recipes `n_steps` and then number of ingredients `n_ingredients` to predict the calories for the recipes. We will be using 2 quantitative variables, and no ordinal and nominal variable to build the regression model.

### Data encoding

For the two random variable, we will be applying `StandardScaler` to standalize `n_steps` and directly use `ave_rating`.

### Model Descriptions and Performance

We will be using linear regression model in the `sklearn` to build up the regression model. The linear regression model will predict the calories of a recipe with a polynomial with at most degree of one.

The performance of your current model, as indicated by the R^2 value, is not very strong. The R^2 value of 0.0217 implies that only approximately 2.17% of the variability in the calorie content can be explained by the variables 'n_steps' and 'n_ingredients'. This suggests that these features might not be the most influential factors when it comes to predicting calorie content, or that the relationship between these features and calories might not be linear, as assumed by the linear regression model.

Additionally, the RMSE (Root Mean Squared Error) of the model is 26.447. The RMSE is a measure of the differences between the values predicted by the model and the actual values. This value is not low enough to guarantee a accurate model. 

Also, using the data visualization, we can have a look at the model.

The model can not correctly predic the calories of recipes since not enough feature and the recipes are clustered, making it hard to make precise prediction.

## Final Model

### Model Chosen

In the final model, we are choose Lasso regression model. The Lasso model, short for Least Absolute Shrinkage and Selection Operator, is a type of linear regression that uses shrinkage, where data values are shrunk towards a central point like the mean. This is particularly useful in this problem because it not only helps in avoiding overfitting but also performs feature selection. By shrinking some of the coefficients to zero, it effectively removes the less important features, thus making the model simpler and interpretable, which is crucial for understanding the relationships between recipe characteristics and calorie content.

### Features Added

In the final model, we are introducing the following new features that could be related to predicting the calories.

- `minutes`: The recipes cooking minutes could be related to the calories of a recipes. This is based on the idea that longer cooking times, often linked to complex dishes, may result in higher calorie counts, thus aiding in accurate prediction.

- `n_ingredients`: The number of ingredient could be related to the food calories. For example, a recipes with more ingredients could be a huge meal that could be enjoyed by multiple people, therefore resulting in high calories.

- `total fat (PDV)`: Total fat as one important part of the nutrition that could impact the calculation of calories. Food with more total fat often tend to have more calories

- `sugar (PDV)`: The quantity of sugar is a critical factor that significantly contributes to a recipe's calorie count. Typically, recipes with higher sugar levels tend to have greater caloric values due to sugar's high energy content.

- `sodium (PDV)`: Although sodium doesn't directly contribute to the calorie count, it's often associated with processed and high-calorie foods, including pizza and smoked meet. Therefore, a high sodium content may indicate a higher calorie count.

- `protein (PDV)`: Recipes with high protein content could potentially have more calories. Protein-rich ingredients like meat and dairy products often contribute significantly to the total calorie count of a recipe.

- `saturated fat (PDV)`: Saturated fats are a major source of calories. Recipes with a high proportion of saturated fats, such as those involving fatty meats or full-fat dairy products, usually have higher calorie content.

- `carbohydrates (PDV)`: Carbohydrates are a primary energy source and contribute significantly to a recipe's calorie count. Dishes with high carbohydrate content, like pasta or baked goods, tend to have a higher number of calories.

To better fit the Lasso model, we are also doing transformation on the features. We mainly apply `StandardScaler` to our new features, including `n_ingredients`, `total fat (PDV)`, `sugar (PDV)`, `sodium (PDV)`, `protein (PDV)`, `saturated fat (PDV)`, `carbohydrates (PDV)`. We also done `QuantileTransformer` on `minutes`. This is to create better features for the Lasso model since it need to shrink some coefficients, and balance the weights of all variables before training.

### Choice of Hyperparameters

For the Lasso model, we are working on the `lasso__alpha` as hyperparameter. The alpha for the model is important since it controls the amount of shrinkage. This would directly impact the coefficients for the parameter. The higher the alpha value is, the more the model would shrink the coefficient to make it less overfitted while keeping the high RMSE and R^2 with fewer features (often not important features). We are using `GridSearchCV`, which could conduct Grid Search on the hyperparameter while using cross validation to avoid overfitting problem. 

After Grid Search, we find out the best value for `lasso_alpha` is 0.1.

### Model Interpretation and Performance



# Fairness Analysis

In general, we are thinking about whether the different numbers of ingredients in our recipes will make our final model perform differently to predict calories. Thus, we draw a distribution of ‘n_ingredients’ column in the recipe data frame and then we take the median number 9 of ingredients in recipes as the threshold to classify all recipes into two groups: Group X has the number of ingredients below or equal to 9 and Group Y has the number of ingredients above 9.

My null hypothesis is that the performance of our model to predict calories in the Group X is as the same as the performance of our model to predict calories in the Group Y. 

My alternative hypothesis is that the performance of our model to predict calories in the Group X is different from the performance of our model to predict calories in the Group Y. 

In test statistics, we utilize the difference between root mean square errors(RMSE) of Group X and Group Y. In general, we take 0.05 as the significance threshold. Our observed statistics is the true difference of RMSE between Group X and Group Y.  To test our hypothesis, we run permutation test by permute ‘n_ingredients’ column , and use our already fitted model to predict the corresponding calories. Finally we calculate the RMSE differences in two groups and repeat this process 1000 times. The p-value of these 1000 simulations is almost 0. Thus, we reject the null hypothesis that the performance of our model to predict calories in the Group X is as the same as the performance of our model to predict calories in the Group Y. It is not truly fair. 



