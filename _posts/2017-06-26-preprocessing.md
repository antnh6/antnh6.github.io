---
layout: post
title: Preprocessing Data
tags: [data-analysis]
categories: notes
---
### For Highly Skewed Continuous Data
For continuous variables with highly skewed distributions, it is common practice to apply a **logarithmic transformation** on the data so that the very large and very small values do not negatively affect the performance of a learning algorithm. Using a logarithmic transformation significantly reduces the range of values caused by outliers. Care must be taken when applying this transformation however: The logarithm of 0 is undefined, so we must translate the values by a small amount above 0 to apply the the logarithm successfully.

For example:
```python
features_raw['capital_gain'] = data['capital gain'].apply(lambda x: np.log(x + 1))
```

### Feature Scaling
It is often good practice to perform some type of scaling on numerical features. Applying a scaling to the data does not change the shape of each feature's distribution; however, normalization ensures that each feature is treated equally when applying supervised learners. Note that once scaling is applied, observing the data in its raw form will no longer have the same original meaning, i.e. the values are relative to one another in the same column.
 * z-score standardization
 * min max scaler [(souce)][3]
Note that not all algorithms will benefit from this type of transformation, such as linear reg, and CART won't.

```python
# Import sklearn.preprocessing.StandardScaler
from sklearn.preprocessing import MinMaxScaler

# Initialize a scaler, then apply it to the features
scaler = MinMaxScaler()
numerical = numpy.array([[144.], [155.], [166.]]
rescaled = scaler.fit_transform(numerical)
```

The 'age' column has been normalized to:  
|   |age(before)   |age(after) |
|:---:   |:---:    |:---:    |
|1 |30   |0.354  | 
|2 |45   |0.427  |  

### One-hot Encoding Scheme 

Typically, learning algorithms expect input to be numeric, which requires that non-numeric features (called categorical variables) be converted. One popular way to convert categorical variables is by using the one-hot encoding scheme. One-hot encoding creates a "dummy" variable for each possible category of each non-numeric feature. 


| |someFeature	| |	someFeature_A| someFeature_B|	someFeature_C|
|---|:---:|---|:---:|:---:|:---:|
|0|	B|	|0|	1|	0|
|1|	C|	----> one-hot encode ---->|	0|	0|	1|
|2|	A|	|	1|	0|	0|

* Use pandas.get_dummies() to perform one-hot encoding 

### Feature Selection
is used to pick out the best features from a large set of features. Two ways of "picking":
* Filtering: independent of the learning algorithm and is generally a pre-processing step. This leads to a faster training pipeline but it is possible the features we picked in the pre-processing step doesn't work very well downstream in the actual learning algorithm. Decision tree is sort of a filtering algorithm, so we could use it to find the "optimal" set of features and train the data with those features using the actual learning algo.
* Wrapping: the subset selection takes place based on the learning algorithm used to train the model itself. Every subset that is proposed by the subset selection measure is evaluated in the context of the learning algorithm. Obviously, this means that computationally intensive learning algorithms cannot be used. Backward and Forward

In sklearn, there are SelectKBest and SelectPercentile

### Feature Transformation
refer to PCA/ICA 
### Relevance vs. Usefulness
* A feature is strongly relevant if it helps improve/worsen the Bayes Optimal Classifier. A feature is deemed weakly relevant if it is only relevant in a strict subset of all features. 
* A classifier is Bayes optimal if no other classifier can classify with a lower expected misclassification error.  Essentially it means that all of the classification error is due to genuine noise in the data.[(source)][4]
* 
The usefulness of a feature is defined by how useful it is to a *particular* algorithm!
[3]: http://sebastianraschka.com/Articles/2014_about_feature_scaling.html
[4]: https://www.quora.com/What-is-meant-by-Bayes-Optimal-solution/answer/Justin-Rising?srid=ugxJO