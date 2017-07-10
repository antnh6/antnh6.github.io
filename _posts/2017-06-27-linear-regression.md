---
layout: post
title: Linear + Logistic Regression
tags: [supervised, machine-learning]
categories: notes
---

## R<sup>2</sup>

* **baseline prediction** In order to find out your learning algorithm is any good, you will typically measure performance in one way or another. Say, you get 75% accuracy. But what does this mean? You can infer this meaning by comparing with a baseline's performance. 

A baseline is a method that uses heuristics, simple summary statistics, randomness, or machine learning to create predictions for a dataset. You can use these predictions to measure the baseline's performance (e.g., accuracy)-- this metric will then become what you compare any other machine learning algorithm against.

If you are dealing with a specific domain of machine learning (such as recommender systems), then you will typically pick baselines that are current state-of-the-art approaches - since you will usually want to demonstrate that your approach does better than these [(source)][3].

* **SST** = total sum of squared errors
from using the **base line** prediction

```
SST = sum( (mean(train$Temp) - test$Temp)^2)
```

* **SSE** = sum of squared errors

??? Why SST <= SSE always? 

R<sup>2</sup> is nice because it captures the values added by adding a linear regression
 
* The model's R² value can never decrease from adding new variables to the model. This is due to the fact that it is always possible to set the coefficient for the new variable to zero in the new model. However, this would be the same as the old model. So the only reason to make the coefficient non-zero is if it improves the R² value of the model, since linear regression picks the coefficients to minimize the error terms, which is the same as maximizing the R². [(Source)][1]
    * Only out-of-sample(test set) R<sup>2</sup> can be negative.
    * In other words, when we remove insignificant variables, the "Multiple R-squared" will always be worse, but only slightly worse. This is due to the nature of a linear regression model. It is always possible for the regression model to make a coefficient zero, which would be the same as removing the variable from the model. The fact that the coefficient is not zero in the intial model means it must be helping the R-squared value, even if it is only a very small improvement. So when we force the variable to be removed, it will decrease the R-squared a little bit. However, this small decrease is worth it to have a simpler model.
    * On the contrary, when we remove insignificant variables, the "Adjusted R-squred" will frequently be better. This value accounts for the complexity of the model, and thus tends to increase as insignificant variables are removed, and decrease as insignificant variables are added.
> ![img](../../img/post-img/supervised/linear-reg/1.png)

After obtaining the output of the model summary, simply look at the p-values of all of the variables in the output (the right-most column, labeled "Pr(>|t|)"). It turns out that none of them are significant.

 we are ultimately interested in models that have high explanatory power (as measured in training R-Squared) and out of sample predictive power (as measured in testing R-Squared

 Month is an ordinary numeric variable. In fact, we must convert Month to a factor variable before adding it to the model. The previous subproblem essentially showed that for every month that we move into the future (e.g, from January to February, from February to March, etc.), our predicted sales go up by 110.69. This isn't right, because the effect of the month should not be affected by the numerical coding, and by modeling Month as a numeric variable, we cannot capture more complex effects. For example, suppose that when the other variables are fixed, an additional 500 units are sold from June to December, relative to the other months. This type of relationship between the boost to the sales and the Month variable would look like a step function at Month = 6, which cannot be modeled as a linear function of Month.



* Adjusted R-squared adjusts the R-squared value to account for the number of independent variables used relative to the number of data points.

### Correlation
* Measures whether and how strongly pairs of variables are related.
* Has values ranging from -1 to 1 with 0 being no correlation, 1 being positive correlation and so on.

### Multicolinarality
refers to the situation when two independent variables are highly correlated (typically |correlation| > 0.7).
    * Since coefficients are only interpretable in the presence of other variables being used, if a model has many independent variables with high correlation, the significant values of them might be really low when ALL are chosen to predict a dependent variable since including them all is tantamount to multiplying the scale of that feature. Dropping one of them **one at a time**(with the one with the largest "p-value" being removed first, or , or the one with the "t value" closest to zero) would increase R<sup>2</sup>. 
### Logistic Regression 
Logistic regression is another generalized linear model (GLM) procedure using the same basic formula, but instead of the continuous Y, it is regressing for the **probability** of a categorical outcome. In simplest form, this means that we're considering just one outcome variable and two states of that variable- either 0 or 1 [(source)][2].

Typically we would want a model with smaller AIC (Akaike Information Criterion).
### Threshold value t

What should we pick for t? => using ROC curves 

### Confusion Matrix 

![confusion-matrix](../../img/post-img/supervised/linear-reg/3.png){:height="80%" width="80%"}


### ROCR
Since to compare two different models it is often more convenient to have a single metric rather than several ones, we compute two metrics from the confusion matrix: the FPR(false positive rate) and the TPR(true positive rate) , which we will later combine into one
<br>To combine the into one single metric, we first compute the two former metrics with many different threshold (for example 0.00;0.01,0.02,…,1.000.00;0.01,0.02,…,1.00) 

![ROCR](../../img/post-img/supervised/linear-reg/2.png){:height="60%" width="60%"}

ROC (receiver operating characteristic) curves are graphic representations of the relation existing between the sensitivity and the specificity of a test when we vary threshold. 

The AUC (area under the curve) is the perecentage of time that our model will classify which is which correctly.

[1]: https://www.edx.org/course/analytics-edge-mitx-15-071x-3
[2]: https://stats.stackexchange.com/a/29326/165795
[3]: https://www.quora.com/What-does-baseline-mean-in-machine-learning/answer/Neal-Lathia?srid=ugxJO