---
layout: post
title: Linear Regression
tags: [supervised, machine-learning]
categories: notes
---

### Terminology

**Baseline prediction** In order to find out your learning algorithm is any good, you will typically measure performance in one way or another. Say, you get 75% accuracy. But is it any good? You can infer this meaning by comparing with a baseline's performance. A baseline is a method that uses heuristics, simple summary statistics, randomness, or machine learning to create predictions for a dataset. You can use these predictions to measure the baseline's performance (e.g., accuracy)-- this metric will then become what you compare any other machine learning algorithm against[(source)][3].

**SST** = total sum of squared errors from using the **baseline** prediction from the training set
```
SST = sum( (mean(train$Temp) - test$Temp)^2)
```
**SSE** = sum of squared errors (aka the difference between the actual value and the predicted)

*??? Why SST <= SSE always?*


### R<sup>2</sup>
R<sup>2</sup> is nice because it captures the values added by adding a feature to model. 

Note that, the model's R² value can *never* decrease from adding new variables to the model. This is due to the fact that it is always possible to set the coefficient for the new variable to zero in the new model, which would be the same as removing the variable from the model. The fact that the coefficient is not zero in the intial model means it must be helping the R² value, even if it is only a very small improvement. So, when we remove insignificant variables, the "Multiple R-squared" will always be worse, but only slightly worse. However, this small decrease is worth it to have a simpler model. 
Linear regression picks the coefficients to minimize the error terms, which is the same as maximizing the R² [(source)][1].
* On the contrary, when we remove insignificant variables, the **Adjusted R-squared** will frequently be better. This value accounts for the complexity of the model (the number of independent variables used relative to the number of data points), and thus tends to increase as insignificant variables are removed, and decrease as insignificant variables are added.
<p align="center">
  <img src="../../img/post-img/supervised/linear-reg/1.png" height="80%" width="80%">
</p>

In R, after obtaining the summary of the trained model, simply look at the p-values for all of the features that will signify the importance of that feature if < 0.05. The number of stars (from 1 to 3) on the last column also tells the exact same thing more quickly.

We are ultimately interested in models that have high explanatory power (as measured in training R<sup>2</sup>) and out of sample predictive power (as measured in testing R<sup>2</sup>).

Remember to convert numeric variable such as Month to factor variable because we would not want the numerical coding for Month (January = 1, February = 2, March = 3 and so on) to accidentally affect our predictions. For example, suppose that when the other variables are fixed, an additional 500 units are sold from June to December, relative to the other months. This type of relationship between the boost to the sales and the Month variable would look like a step function at Month = 6, which cannot be modeled as a linear function of Month.

### Correlation
* Measures whether and how strongly pairs of variables are related.
* Has values ranging from -1 to 1 with 0 being no correlation, 1 being positive correlation and so on.

### Multicolinarality
refers to the situation when two independent variables are highly correlated (typically |correlation| > 0.7).
    * Since coefficients are only interpretable in the presence of other variables being used, if a model has many independent variables with high correlation, the significant values of them might be really low when ALL are chosen to predict a dependent variable since including them all is tantamount to multiplying the scale of that feature. Dropping one of them **one at a time**(with the one with the largest "p-value" being removed first, or , or the one with the "t value" closest to zero) would increase R<sup>2</sup>. 

[1]: https://www.edx.org/course/analytics-edge-mitx-15-071x-3
[2]: https://stats.stackexchange.com/a/29326/165795
[3]: https://www.quora.com/What-does-baseline-mean-in-machine-learning/answer/Neal-Lathia?srid=ugxJO