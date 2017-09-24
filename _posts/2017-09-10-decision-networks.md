---
layout: post
title: Decision Networks and VPI
tags: [AI]
categories: notes
---
Similar to a Bayes Net with a Utility node
Goal is to maximize the expected utility (MEU) given evidence
Similar to Expectimax/MDPs
# Value of (Perfect) Information (VPI)
The Value of Perfect Information is the expected gain in MEU from knowing that piece of information. 
<p align="center">
    <img src="../../img/post-img/decision-network/1.png" height="80%" width="80%">
</p>

# Value of Imperfect Information
<p align="center">
    <img src="../../img/post-img/decision-network/2.png" height="80%" width="80%">
</p>

# POMDPs
generalization of MDPs that in addition also include 
- Observatons Z
- Observation function (s, z) 
Instead of directly observing the current state, the state gives us an observation which provides a hint about what state it is in. The observations can be probabilistic; so we need to also specify the observation model. This observation model simply tells us the probability of each observation for each state in the model.

Although the underlying dynamics of the POMDP are still Markovian, since we have no direct access to the current state, our decisions require keeping track of (possibly) the entire history of the process, making this a non-Markovian process. The history at a given point in time is comprised of our knowledge about our starting situation, all actions performed and all observations seen.

in POMDPs our problem is to find a mapping from probability distributions (over states) to actions

**Belief state** = a probability distribution over states
**Belief space** = the entire probability space (the set of all possible probability distributions)
 With a two state POMDP, if we are given the probability for being in one of the states as being 'p', then we know that the probability of being in the other state must be '1-p'. Therefore the entire space of belief states can be represented as a line segment. The figure below shows this, though we have made the line segment have a significant width.

 Map from observations to actions