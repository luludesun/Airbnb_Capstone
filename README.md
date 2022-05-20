## Goals: The goals of this project is to: 
1. Measure the demand of Airbnb in LA; 
2. Performed spatial and time series analysis;
3. Build a model to predict the demand; 
4. Measure the impact of each variable on the demand of Airbnb in LA; 
5. NLP and topic modeling on review dataset


### 1. Measure the demand of Airbnb in LA

**Demand index 1: Price**

A natural metric for measuring the demand is to use price. However, measuring the demand of an Airbnb house soly using price will cause a problem. For example, house A, an entire house, has 1000 sqft with a rent price of $1000 per day, and house B, with only a single room, has 20 sqft with a rent price of $900 per day. If we only use price as the measurement for demand or “popularity”, we need to conclude that house A is more popular than house B. But by intuition, many may suggest house B has a higher demand than house A. Thus, comparing price for houses within a similar size would be a better estimator for demand. Another evidence for justifying using price per sqft is that, when comparing the demand for housing in different cities, we usually use price per sqft as the criteria instead of just using price.

One might oppose here that if we need to include house size for estimating the demand, we could apply the same reasoning to all of the variables, and no model can be built. However, after careful examination, one will notice that house size is the only variable that will cause this issue. For instance, geographical region will be a covariate for predicting demand but not a part of demand itself. If house A and house B have a similar size, then if house A is close to downtown while house B is in a poor neighborhood, and house A has a higher price than house B, we can conclude that a better neighborhood affects the demand positively. For cleaness, from paper “The impact of COVID-19 on short-term housing rentals”, the authors derive a way to quantify cleaness. If a cleaner Airbnb has a higher price per square foot than a less clean Airbnb, then it is also safe to claim that cleanliness affects demand.
Of course, using price per sqrt as the measure for Airbnb demand is also not optimal. We will discuss further to determine the demand metrics that best fit this data and our goal.

**Demand Index 2: Occupancy Rate**
	
Here, in the dataset, we can calculate the number of days an Airbnb was booked, the number of days it was open for booking for any given month. Thus, (# of days booked / # of days) open for booking for a given month for a given Airbnb would be a good estimator of demand.

### 2. Perform spatial and time series analysis; 
Perform spatial and time series to analyze the trend of demand over time. Then explore and visualize the variation of the spatial distribution of demand over time.

### 3. Build a model to predict the demand; 
Train supervised machine learning models including Gaussian Naive Bayes, Linear Regression, Logistics Regression, Tree-based methods and KNN, and apply regularization with optimal parameters to overcome overfitting. Then evaluate model performance of classification via 5-fold validation technique and analyze feature importance to identify top factors that influenced the results.
It is natural to see that tree-based methods might perform the best in this dataset, and linear regression might provide the best insights for this dataset. Thus, when building models, we can focus on those two.

Prior to modeling, we should minimize the seasonal effect on our dataset by 1. Using the residual of applying SARIMA to the demand index as our variable to be predicted. 2. Adjusting for a constant for each season, month, week or weekday.

For tree-based models, we will be choosing from bagging or boosting, and test each model in the cross-validation process. Intuitively, Bagging tends to help reduce the variance while boosting tends to reduce the bias. Thus, bagging would work better as the demand has many strong predictors, and the bias for the prediction would not be too significant.

In cross-validation, as the time-series effect in demand is expected to be important, we shall split the dataset through dividing our dataset into chunks by order in time instead of randomly sampling.

For linear regression, we should be avoiding using too many indicator variables as the purpose of applying linear regression is to find out each covariate’s contribution to predicting the demand. For indicator variables, we can perform ANOVA to test which variables are important.

### 4. Measure the impact of each variable on the demand of Airbnb in LA
When analyzing a particular variable’s impact on the demand, we can use some causal inference techniques.
As this is causal inference for observational data, the first step is to match treatment and control groups through propensity scores. Then, we should do a sensitivity analysis to examine the variance of our matching, and the validity of our results. In the end, we will include a table like Table 1 in https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2976021 (Page 9) for each covariate we consider interesting. 

One of the instructors of our course Sam Pimentel’s research focus is on causal inference in a large observational dataset. We also hope to get some advice from him. He “developed new ways to form matched comparison groups in large observational datasets using approaches from discrete optimization. These tools allow transparent and interpretable inferences about the effects of interventions, and provide opportunities to study the impact of potential unobserved confounding variables” (https://www.stat.berkeley.edu/~spi/).

### 5. NLP and topic modeling on review dataset
Cluster reviews into groups and discover the latent semantic structure. 
Then, preprocess review text by tokenization, stemming, removing stop words and extract features by TF-IDF. 
Train unsupervised learning models of K-means clustering and LDA. 
Last, Identified latent topic and keywords of each review for clustering.
