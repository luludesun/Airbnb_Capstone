## Section 1 - Goals

### Goals: The goals of this project is to: 
1. Measure the demand of Airbnb in LA; 
2. Performed spatial and time series analysis;
3. Build a model to predict the demand; 
4. Measure the impact of each variable on the demand of Airbnb in LA; 
5. NLP and topic modeling on review dataset


#### 1. Measure the demand of Airbnb in LA

* Demand index 1: Price * 
A natural metric for measuring the demand is to use price. However, measuring the demand of an Airbnb house soly using price will cause a problem. For example, house A, an entire house, has 1000 sqft with a rent price of $1000 per day, and house B, with only a single room, has 20 sqft with a rent price of $900 per day. If we only use price as the measurement for demand or “popularity”, we need to conclude that house A is more popular than house B. But by intuition, many may suggest house B has a higher demand than house A. Thus, comparing price for houses within a similar size would be a better estimator for demand. Another evidence for justifying using price per sqft is that, when comparing the demand for housing in different cities, we usually use price per sqft as the criteria instead of just using price.
One might oppose here that if we need to include house size for estimating the demand, we could apply the same reasoning to all of the variables, and no model can be built. However, after careful examination, one will notice that house size is the only variable that will cause this issue. For instance, geographical region will be a covariate for predicting demand but not a part of demand itself. If house A and house B have a similar size, then if house A is close to downtown while house B is in a poor neighborhood, and house A has a higher price than house B, we can conclude that a better neighborhood affects the demand positively. For cleaness, from paper “The impact of COVID-19 on short-term housing rentals”, the authors derive a way to quantify cleaness. If a cleaner Airbnb has a higher price per square foot than a less clean Airbnb, then it is also safe to claim that cleanliness affects demand.
Of course, using price per sqrt as the measure for Airbnb demand is also not optimal. We will discuss further to determine the demand metrics that best fit this data and our goal.
