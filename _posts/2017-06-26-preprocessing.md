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

### Normalizing Numerical Features
 It is often good practice to perform some type of scaling on numerical features. Applying a scaling to the data does not change the shape of each feature's distribution; however, normalization ensures that each feature is treated equally when applying supervised learners. Note that once scaling is applied, observing the data in its raw form will no longer have the same original meaning, i.e. the values are relative to one another in the same column.

 ```python
# Import sklearn.preprocessing.StandardScaler
from sklearn.preprocessing import MinMaxScaler

# Initialize a scaler, then apply it to the features
scaler = MinMaxScaler()
numerical = ['age', 'education-num', 'hours-per-week']
features_raw[numerical] = scaler.fit_transform(features_raw[numerical])

 ```
 
The 'age' column has been normalized to: 
> 
>|   |age(before)   |age(after) |
>|:---:   |:---:    |:---:    |
>|1 |30   |0.354  | 
>|2 |45   |0.427  |  

### One-hot Encoding Scheme 

Typically, learning algorithms expect input to be numeric, which requires that non-numeric features (called categorical variables) be converted. One popular way to convert categorical variables is by using the one-hot encoding scheme. One-hot encoding creates a "dummy" variable for each possible category of each non-numeric feature. 


| |someFeature	| |	someFeature_A| someFeature_B|	someFeature_C|
|---|:---:|---|:---:|:---:|:---:|
|0|	B|	|0|	1|	0|
|1|	C|	----> one-hot encode ---->|	0|	0|	1|
|2|	A|	|	1|	0|	0|

* Use pandas.get_dummies() to perform one-hot encoding 

