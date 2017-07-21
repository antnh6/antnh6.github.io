---
layout: post
title: Logistic Regression
tags: [supervised, machine-learning]
categories: notes
---
**Logistic Regression** is a method to regress for the probability of a categorical outcome with the assumption that the relationship of the outcome and the independent variables is linear. Despite having "regression" in its name, Logistic Regression is a **Classifier**.

<p align="center">
  <img src="../../img/post-img/supervised/linear-reg/5.png" height="80%" width="80%">
</p>

Choosing a threshold of 0.5 as the cutoff for predicting classes, and using accuracy as one of our measures of model quality are good choices when we have no preference for different types of errors (false positives vs. false negatives), but other choices might be better if we assign a higher cost to one type of error. 

<p align="center">
  <img src="../../img/post-img/supervised/linear-reg/4.png" height="80%" width="80%">
</p>

Typically we would want a model with smaller AIC (Akaike Information Criterion).

A logistic regression model with a large number of features is particularly at risk for overfitting.

### Threshold value t

What should we pick for t? => using ROC curves 

### Confusion Matrix 
<p align="center">
  <img src="../../img/post-img/supervised/linear-reg/3.png" height="80%" width="80%">
</p>

### ROCR
To compare two different models it is often more convenient to have a single metric rather than several ones, we compute two metrics from the confusion matrix: the FPR (false positive rate) and the TPR (true positive rate).
<br>To combine two metrics above into one single metric, we first compute the two former metrics at many different threshold (for example 0.01, 0.02,..., 1.00) 

<p align="center">
  <img src="../../img/post-img/supervised/linear-reg/2.png" height="60%" width="60%">
</p>

ROC (receiver operating characteristic) curves are graphic representations of the relation existing between the **sensitivity** and the **specificity** of a test when we vary threshold. 

The AUC (area under the curve) is the percentage of time that our model will classify which is which correctly.
