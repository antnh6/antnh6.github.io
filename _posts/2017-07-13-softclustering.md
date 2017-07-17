---
layout: post
title: Gaussian Mixture Model 
tags: [unsupervised]
categories: notes
---
### Motivation

Using k-Means, each data point can only be assigned to one group or another, but never both (**Hard** clustering). By using the **Gaussian Mixture Model**, we allow for points to be in multiple groups based on their probability to be in that group, hence the name **Soft** clustering.

### The What
Gaussian Mixture Model (GMM) is a probabilistic model, and can be understood as a Mixture of Gaussians. Imagine each centroid as a mean of a Gaussian distribution with its own variance and coefficient. We will then calculate the posteriors for each data point and assign it to groups accordingly. Now a point can have a gradation of colors.

In the reassignment step where we have to update new means, EM (**expectation maximization**) says that a point will give a bit of its mass to every centroid, but it will give more to centroids that it's more associated with. In the case of k-Means, these b<sub>i</sub>'s would just be binary. In essence, kMeans is a just a special case of GMM.

<p align="center">
  <img src="../../img/post-img/unsupervised/clustering/1.png" height="80%" width="80%">
</p>[(source)][1]

[1]: https://www.youtube.com/watch?v=iQoXFmbXRJA


