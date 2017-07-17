---
layout: post
title: Useful Python commands for Data Analysis
tags: [python]
categories: notes
---

* display(df.head(n=3))


## Scikit Learn

* Choose a scikit-learn classifier (e.g., adaboost, random forests) that has a feature_importance_ attribute, which is a function that ranks the importance of features according to the chosen classifier.
* from sklearn.decomposition import **PCA**
    * fit
    * explained_variance_ratio_  to get % of variances, how much variance within the data is explained by that dimension alone
    * components_ to get dimensions of PCs
    * transform
    * inverse_transform


* np.**percentile**(feature,percentile)

* data.**drop**(data.index[outliers]).reset_index(drop = True) to drop rows with those indices in outliers 