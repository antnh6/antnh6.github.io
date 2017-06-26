---
layout: post
title: Gaussian Naive Bayes
tags: [supervised, machine-learning]
categories: notes
---
### Prior Probability [(source)][1]

>![Prior probability](../../img/post-img/supervised/gaussianNB/1.png)

### Posterior Probability

### Conditional Probability 
is the probability of something given something else has happened.
 
### Bayes Rule
```
$$\binom{n}{k} = \frac{n!}{k!(n-k)!}$$
```
### Naive Bayes 
In reality, we have to predict an outcome given **multiple evidences**. In that case, the math gets very complicated. To get around that complication, one approach is to 'uncouple' multiple pieces of evidence, and to treat each piece of evidence as independent. This approach is why this is called **naive** Bayes. [(source)][2]
```
 P(Outcome|Multiple Evidence) =
 P(Evidence1|Outcome) * P(Evidence2|Outcome) * ... * P(EvidenceN|Outcome) * P(Outcome)
 scaled by P(Multiple Evidence)
```
### Why is NB so popular?
When it all comes down to it, we only need to do counting and multiplication in order for this algorithm to work: run the formula above to get the probabilities for all possible outcomes and pick one with the highest probability.


### Version Space
* The version space is a subset of the hypothesis space, which is a space of all possible hypotheses. It contains those hypotheses such that they correctly predict the training data you have (essentially a 100% model fit). For example:
> ![Version Space](https://github.com/antnh6/udacity-machine-learning/blob/master/supervised/gaussian-naive-bayes/version-space.png?raw=true){:height="70%" width="70%"}


[1]: https://stackoverflow.com/a/10062702/7704870 
[2]: https://stackoverflow.com/a/20556654/7704870
