---
layout: post
title: Clustering
tags: [unsupervised]
categories: notes
---
### Definition
Clustering is an unsupervised algorithm. There are many types of them:
* K-Means (typically does a better job of identifying partially overlapping clusters)
    ![img]
* Hierachial 
    * Single-linkage is the most popular form of this type
* Baysian method 

### Why Clustering is hard [(source)][1]
* All of the afforementioned approaches are very computationally difficult to solve exactly for large datasets => as a result, we often resort to optimization heuristics that may or may not produce reasonable results.
* There is not a ground truth to refer to for answer if our algorithm is producing a "wrong" result as opposed to cases of supervised learning. 
* It's hard to determine the right number of clusters.
* It's also hard to cluster outliers.
* It's equally hard if not more to cluster overlapping data. 

### The ideal clustering function [(source)][2]

The ideal clustering function would achieve three properties:
* **scale-invariance** An ideal clustering function does not change its result when the data are scaled equally in all directions. 
![scale-invariance]
* **consistency** If we stretch the data so that the distances between clusters increases and/or the distances within clusters decreases, then the clustering shouldn’t change.
![consistency]
* **richness** An ideal clustering function would be flexible enough to produce all http://www.cs.fsu.edu/~ackerman/thesisPhD.pdfspossible partition/clusterings of this set.
![richness] 

As it turns out, such function does not exist IRL (**Kleinberg’s Impossibility Theorem**). By examining clustering functions that come close to satisfying the three axioms, I hope to get some intuition behind the proof (which I didn't quite get yet)
* Every functions needs a stopping condition, and Kleinberg outlines three different stopping conditions, each of which violates one of his three axioms, while satisfying the other two.
    * **k-cluster stopping condition** does not satisfy richness
    * **distance-r stopping condition** does not satisfy scale invariance
    * **some-fraction-of-max-distance-between-any-two-points** stopping condition does not satisfy consistency

Nevertheless, there are ways to circumvent the impossibility theorem, or are the axioms even desirable all the time? The axioms serve more as a reality check for us to not be too demanding of what a clustering function can do for us. 

### TOREAD
* http://www.cs.fsu.edu/~ackerman/thesisPhD.pdf

* http://alexhwilliams.info/itsneuronalblog/2015/11/18/clustering-is-easy/


[1]: http://alexhwilliams.info/itsneuronalblog/2015/09/11/clustering1/
[2]:
http://alexhwilliams.info/itsneuronalblog/2015/10/01/clustering2/ 
[3]:
http://alexhwilliams.info/itsneuronalblog/2015/11/18/clustering-is-easy/