---
layout: post
title: Clustering
tags: [unsupervised]
categories: notes
---


### Definition
There are many types of Clustering:
* K-Means (typically does a better job of identifying partially overlapping clusters)
    ![img]
* Hierachial (no need to select number clusters a priori, but hard to use with large datasets because of pair-wise distance calculation)
    * Single-linkage is the most popular form of this type
* [Soft Clustering (Expectation Maximization)](http://annwin.me/notes/2017-07-13-softclustering/)

### Collaborative vs. Content Filtering

### Why Clustering is hard [(source)][1]
* All of the aforementioned approaches are very computationally difficult to solve exactly for large datasets => As a result, we often resort to optimization heuristics that may or may not produce reasonable results.
* There is not a ground truth to refer to for answer to know if our algorithm is producing a "wrong" result as opposed to supervised learning. 
* It's hard to determine the right number of clusters.
* It's also hard to cluster outliers.
* It's equally hard if not more to cluster overlapping data. 

### The ideal clustering function [(source)][2]

An ideal clustering function would have these three properties:
* **scale-invariance** An ideal clustering function does not change its result when the data are scaled equally in all directions. 
![scale-invariance]
* **consistency** If we stretch the data so that the distances between clusters increases and/or the distances within clusters decreases, then the clustering shouldn’t change.
![consistency]
* **richness** An ideal clustering function would be flexible enough to produce all possible partition/clusterings of this set.
![richness] 

As it turns out, such function does not exist IRL (**Kleinberg’s Impossibility Theorem**). By examining clustering functions that come close to satisfying a;l three axioms, I hope to gain some intuition behind the proof for the theorem.
* Every functions needs a stopping condition, and Kleinberg outlines three different stopping conditions, each of which violates one of his three axioms, while satisfying the other two.
    * **k-cluster stopping condition** does not satisfy richness
    * **distance-r stopping condition** does not satisfy scale invariance
    * **some-fraction-of-max-distance-between-any-two-points** stopping condition does not satisfy consistency

Nevertheless, there are ways to circumvent this Impossibility Theorem, but more importantly are all 3 axioms even desirable all the time? The axioms serve more as a reality check for us to not be too demanding of what a clustering function can do for us. 

### TOREAD
* http://www.cs.fsu.edu/~ackerman/thesisPhD.pdf

* http://alexhwilliams.info/itsneuronalblog/2015/11/18/clustering-is-easy/

When the number of clusters is not known a priori, there is no guarantee that a given number of clusters best segments the data, since it is unclear what structure exists in the data — if any. However, we can quantify the "goodness" of a clustering by calculating each data point's silhouette coefficient. The silhouette coefficient for a data point measures how similar it is to its assigned cluster from -1 (dissimilar) to 1 (similar). Calculating the mean silhouette coefficient provides for a simple scoring method of a given clustering.

[1]: http://alexhwilliams.info/itsneuronalblog/2015/09/11/clustering1/
[2]:http://alexhwilliams.info/itsneuronalblog/2015/10/01/clustering2/ 
[3]:http://alexhwilliams.info/itsneuronalblog/2015/11/18/clustering-is-easy/

