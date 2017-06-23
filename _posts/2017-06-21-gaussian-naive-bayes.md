---
layout: post
title: Gaussian Naive Bayes
tags: [supervised, machine-learning]
categories: notes
---


### Conditional Probability
 
### Bayes Rule
### Naive Bayes 
In reality, we have to predict an outcome given **multiple evidences**. In that case, the math gets very complicated. To get around that complication, one approach is to 'uncouple' multiple pieces of evidence, and to treat each piece of evidence as independent. This approach is why this is called **naive** Bayes.

Then, just run the formula above for all possible outcomes and pick one with the highest probability.



### Version Space

* The version space is a subset of the hypothesis space, which is a space of all possible hypotheses. It contains those hypotheses such that they correctly predict the training data you have (essentially a 100% model fit). For example:
> ![Version Space](https://github.com/antnh6/udacity-machine-learning/blob/master/supervised/gaussian-naive-bayes/version-space.png?raw=true){:height="70%" width="70%"}

