---
layout: post
title: Gaussian Naive Bayes
tags: [supervised, machine-learning]
categories: notes
---
# Definition
- **Bayes Rules**
\begin{equation}
P(A|B) =\frac{P(B|A) \times P(A)} {P(B|A) \times P(A)+P(B|\sim A) \times P(\sim A)}
\end{equation}
- We call P(A) the **prior probability** and P(A\|B) the **posterior probability** 

- **Naive Bayes**  
In reality, we have to predict an outcome given **multiple evidences**. In that case, the math gets very complicated. To get around that complication, one approach is to 'uncouple' multiple pieces of evidence, and to treat each piece of evidence as independent, thus the name **Naive** Bayes. [(source)][2]
\begin{equation}
 P(Outcome|Multiple Evidence) = \frac{P(Evidence1|Outcome) * P(Evidence2|Outcome) * ... * P(EvidenceN|Outcome) * P(Outcome)} {P(Multiple Evidence)}
\end{equation}

Knowing the **Joint Distribution** over a collection of random variables tells us absolutely *everything* there is to know probabilistically about the relationships among those random variables including the solution to learning F: X $$\rightarrow$$ Y, or P(Y\|X).
- Problem: It's not obvious how to estimate the joint distributions once we start scaling up to a reasonable number of variables. For example,
<p align="center">
    <img src="../../img/post-img/supervised/gaussianNB/1.png" height="80%" width="80%">
</p>

# Principles for Estimating Probabilities
- Principle 1 (maximum likelihood or MLE)

- Principle 2 (maximum a posteriori prob. or MAP)
We would choose this principle over principle 1 when we have good priors. Principle 1 = Principle 2 when we have infinite data.
<p align="center">
    <img src="../../img/post-img/supervised/gaussianNB/3.png" height="60%" width="60%">
</p>



- Conjugate prior: P(theta) 




### Version Space
* The version space is a subset of the hypothesis space, which is a space of all possible hypotheses. It contains those hypotheses such that they correctly predict the training data you have (essentially a 100% model fit). For example:
<p align="center">
    <img src="../../img/post-img/supervised/gaussianNB/2.png" height="50%" width="50%">
</p>



[1]: https://stackoverflow.com/a/10062702/7704870 
[2]: https://stackoverflow.com/a/20556654/7704870
