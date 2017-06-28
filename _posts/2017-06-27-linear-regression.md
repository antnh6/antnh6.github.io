---
layout: post
title: Linear Regression
tags: [supervised, machine-learning]
categories: notes
---

## R<sup>2</sup>

* **baseline prediction** is the average of all dependent values.

* **SST** = total sum of squared errors
from using the **base line** prediction

* **SSE** = sum of squared errors

??? Why SST <= SSE always? 

R<sup>2</sup> is nice because it captures the values added by adding a linear regression
 
* The model's R² value can never decrease from adding new variables to the model. This is due to the fact that it is always possible to set the coefficient for the new variable to zero in the new model. However, this would be the same as the old model. So the only reason to make the coefficient non-zero is if it improves the R² value of the model, since linear regression picks the coefficients to minimize the error terms, which is the same as maximizing the R². [(Source)][1]
    * Only out-of-sample(test set) R<sup>2</sup> can be negative.

> ![img](../../img/post-img/supervised/lin-reg/1.png)

* Adjusted R-squared adjusts the R-squared value to account for the number of independent variables used relative to the number of data points.

### Correlation
measures whether and how strongly pairs of variables are related.
    * Has values ranging from -1 to 1 with 0 being no correlation, 1 being positive correlation, and -1 negative

### Multicolinarality
refers to the situation when two independent variables are highly correlated (typically |correlation| > 0.7).
    * Since coefficients are only interpretable in the presence of other variables being used, if a model has many independent variables with high correlation, the significant values of them might be really low. Dropping one of them **one at a time** might increase R<sup>2</sup>. 

[1]: https://www.edx.org/course/analytics-edge-mitx-15-071x-3