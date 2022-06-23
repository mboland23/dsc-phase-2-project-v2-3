# House Sale Price Strategy
In this project description we will cover:
* House sale price introduction
* Data set and descriptive statistics
* Data process 
* Regression models and results
* Conclusion

The GitHub repository accompanying the project contains the following: 
* JupyterNotebook: Data analysis process and corresponding code
  Data analysis process and corresponding code
* Images folder
* Presentation
* Data Folder 


## Introduction

The housing market is an integral indicator of both local and national economic performance. As of late, the US housing market has exploded since the onset of the COVID-19 global pandemic. Home sales reach a record 15 year peak in 2021 with more than 6 million homes sold, according to the National Association of Realtors (NAR). Likewise, housing prices have skyrocketed. In Q3 2021, the NAR reported that home sale prices were up a staggering 20% year-over-year. Sales are also happening at an incredibly quick rate. The average time from listing to accepted offer was 22 days in 2021, according to Ellie Mae Origination Insight Report. In some markets this time was reduced further. The Seattle area saw an average days on the market of just 5 days, according to Redfin.

A heated housing market makes pricing decisions even more important for multiple reasons. First, the shortened time on market means that there is not much time to adjust prices. If a realtor overprices a property, it may sit on the market for longer leading buyers to overlook the property. Longer time on the market increases costs for realtors and sellers alike. On the otherhand, underpriced houses (not usually an issue in a heated housing market but none the less a concernt) run the risk of damaging realtors reputation — a large concern for a referral based business.

Statistical inferential analysis can help alleviate pricing risks and serve as a model for pricing future listings. To create a stastical inferential pricing model, we examined [data]("./data/kc_house_data.csv") from King County House Sales dataset. The data covers over 20,000 house sales from 2014-2015 in Kings County, Washington (Greater Seattle area) and includes 20 characteristics of these observations. From the dataset we worked to create a pricing model that would best capture how these various characteristics explained the variation in house sale price. The "Best Fit" inferential model that we determined seves as a past template to help realtors determine pricing strategy for home sales.

## Data Set and Descriptive Statistics
Opening the data file we see that we have 21,597 observations on house sales and 21 variables with information about the houses. The mean sale price of houses in our dataset is 540,296 with a standard deviation of 367,368. The target variable of house sale price ranges from 78,000 to 7,700,000.  We cleaned our dataset to only include variables of interest and those that were highly correlated to our variable of interest. Our final data table included 10 variables of interest and the same number of observations (21, 597) of our original dataset.

## Data Science Process : An iterative approach 
In order to determine what characteristics most impact house price sale we used an interative modeling process, where we started with a baseline model (a basic linear regression of the highest correlated variable - sqft living area - on house sale price) and moved to a more complex model. In order to do this we followed this process: 
1) Data cleaning 
2) Data transformation on categorical variables
3) Set up dummy regression and train/test split
4) Iterative models
5) Cross validated the models to find best fit
6) Created visualizations to explain our best fit model

## Model One: Basic Linear Regression of Square Foot Living Area on House Sale Price
First, we ran a simple linear regression model on price and square foot living area. Since there were issues with adhering to the error assumptions, we logged both the price and sqft_living. 

The simple linear regression model with both price (our target variable) and sqft_living (our independent variable of interest)revealed that a 1% increase in square footage of a house, leads to an approx 0.83% increase in price. This is statistically significant with an alpha of 0.05 as exhibited with a p value of 0.00 and a t-stat greater than 2.

However, our R^2 reveals that our model only explains 45.6% of the variation in price. This is relatively low, leading us to believe that a multilinear regression model may better explain fluctuations in price.

## Model Two: Adding in Bathrooms Feature

After looking at the correlations of our target variable and variables of interest we noticed that bathrooms is highly correlated with sale price. So we included this variable in our model. Our regression revealed that a adding another bathroom, increases our sale price by 6.3%. This is statistically significant with an alpha of 0.05 as exhibited with a p value of 0.00 and a t-stat greater than 2. The R^2 of Model 2 tells us that our model explains 45.8% of the variation in price. 

 Because we want to see the effect of both bathrooms and housing square footage on housing price, which have very different units of measurement, we standardized the variables. Standardization shows us how many standard deviations from the mean each observation is. In an OLS regression model, coefficients on standardized variables tells us the effect (in standard deviations) on the dependent variable of increasing the independent variable by one standard deviation. We see that the log of the square foot living area has a greater magnitude effect on price than bathrooms variable. 

## Model Three: Adding in Waterfront Feature
From our correlation matrix, we see that the Waterfront variable also has a higher correlation with price than other variables in our dataset. We will add the waterfront variable to our regression and see if it improves R^2.

As a note, the waterfront variable is a categorical variable where 1 = Waterfront Property and 0 = Non Waterfront Variable. Thus the coefficient from our regression captures the effect of Waterfront Property on Logged Price relative to non-waterfront properties.

The regression results show us that waterfront properties have 78% higher sale prices than non waterfront properties, holding all else equal. This was statistically significant with a 0.05 alpha as exhibited by a p value of 0.00 and t-stat greater than 2. 

## Model Four: Adding in Conditions Features
Conditions were also correlated with our target variable, price. This makes sense that the condition that a house is in will help explain variation in price. As a reminder, our transformation of this categorical feature means that the coefficients on these condition variables are the change in price relative to the left out condition variable, "average".

We see that the condition variables all have statistically significant impact on price as exhibited by low P-values (lower than our threshold of 0.05). An as expected the variables that indicate worse condition than average, "fair" and "poor" decrease the price relative to houses in average condition, holding all else equal. Likewise, the variables that indicate better conditions than average "good" and "very good" increase the sale price of the house relative to average, holding all else equal.

We also notice that our Adjusted R^2 has improved again - suggesting that including these variables have helped increase the variation in price that is explained by our model.

## Model Five: Adding in Square Foot Living Area per Bedroom Feature
Finally, one would think that the amount of living area per bedroom in a house is indicative of price. For example, a house with 3 bedrooms, but small living area is expected to be cheaper than a house with 3 bedrooms and a large living area, holding all else equal. Creating a ratio of living area to bedroom count would help account for this in our model.

Our regression results tell us that a 1% increase in square foot/bedroom increases price by 0.31%. After scaling our variables, the regression results from the scaled model we can infer that the square foot living area of a house (x1), the squaret foot living area per bedroom, number of bathrooms, and whether or not the house was on the waterfront have the highest impact on the logged price of the house. Another strong indicator from our model is whether the house is in "Very Good" condition or not.

## Best Fit Model - Cross Validation Scores
From conducting cross validation scores we determined that the final model was the best fit model for our train data. The Root Mean Squared Error shows that our model is, on average, $252,991 off the price of a house. While this is still quite high, it is less than the dummy model, and thus better predicts our house prices.

## Recommendations
Through our iterative process we were able to find a model that better explained the variation in house sales price in King's County, Washington as exemplified by our increasing Adjusted R^2 and lower RMSE than the base model of a simple linear regression of square foot of living area on house sale prices.

However, there are significant limitations to our model and anyone who plans to use the model as a pricing strategy should be aware of these.

First, the overall R^2 of our best fit model is still low - only explaining 50% of the variation in house price. Ideally, we could incorporate other data including geolocation data (the zipcode variable) to help explain variation in price. We expect this variable would drive up the R^2.

Second, we know there are multicollinearty problems in the model, particularly between the sqft_living and living_area_per_bedroom variables. This makes sense as there is a relationship between the size of the living area of a house and the ratio of living area to bedroom.

Finally, while we were able to lower the Root Mean Squared Error from the base model, in real terms it is still quite high. Our predictions are off by almost  250,000.𝑊ℎ𝑒𝑛𝑡ℎ𝑒𝑚𝑒𝑎𝑛ℎ𝑜𝑢𝑠𝑒𝑠𝑎𝑙𝑒𝑝𝑟𝑖𝑐𝑒𝑜𝑓𝑡ℎ𝑒𝑑𝑎𝑡𝑎𝑠𝑒𝑡𝑖𝑠 540,296 this can be quite a big difference.

We recommend further analysis on other variables in order to improve on our best model, including using geolocation. We also recommend parsing out higher valued & larger homes to see if stratisfying our dataset in this way could better explain variations in price as these observations tended to be outliers in our data.

