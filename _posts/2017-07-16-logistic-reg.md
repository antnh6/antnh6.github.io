---
layout: post
title: Logistic Regression
tags: [supervised, machine-learning]
categories: notes
---
One of the most widely-used **classifiers** along with **linear discriminant analysis**, and **K-nearest neighbors**.

### Logistic Regression 
Logistic regression is another generalized linear model (GLM) procedure using the same basic formula, but instead of the continuous Y, it is regressing for the **probability** of a categorical outcome. In simplest form, this means that we're considering just one outcome variable and two states of that variable- either 0 or 1 [(source)][2].

Typically we would want a model with smaller AIC (Akaike Information Criterion).

A logistic regression model with a large number of features is particularly at risk for overfitting.

### Threshold value t

What should we pick for t? => using ROC curves 

### Confusion Matrix 

![confusion-matrix](../../img/post-img/supervised/linear-reg/3.png){:height="80%" width="80%"}


### ROCR
Since to compare two different models it is often more convenient to have a single metric rather than several ones, we compute two metrics from the confusion matrix: the FPR(false positive rate) and the TPR(true positive rate) , which we will later combine into one
<br>To combine the into one single metric, we first compute the two former metrics with many different threshold (for example 0.00;0.01,0.02,…,1.000.00;0.01,0.02,…,1.00) 

![ROCR](../../img/post-img/supervised/linear-reg/2.png){:height="60%" width="60%"}

ROC (receiver operating characteristic) curves are graphic representations of the relation existing between the sensitivity and the specificity of a test when we vary threshold. 

The AUC (area under the curve) is the percentage of time that our model will classify which is which correctly.
