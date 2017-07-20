---
layout: post
title: Reinforcement Learning
tags: [reinforcement-learning]
categories: notes
--- 

### Deterministic vs. Stochastic Processes 
<p align="center">
  <img src="../../img/post-img/reinforcement/2.png" height="80%" width="80%">
</p>

### The "Markov" Property
<p align="center">
        <img src="../../img/post-img/reinforcement/7.png" height="90%" width="90%">
</p> [(source)][1]

### Markov Decision Process
A MDP includes: 
- Set of states S
- Start state s<sub>0</sub>
- Set of actions A
- Transitions T(s',s,a) or P(s'\|s,a) the probability of landing in state s' after taking action a in state s
- Rewards R(s,a,s') and discount \\( \gamma \\)

### Goal of MDP
is to return a **policy** (a choice of action for each state). An **optimal** policy would maximize the sum of discounted rewards (utility), thus depending on the reward for each state.
<p align="center">
  <img src="../../img/post-img/reinforcement/3.png" height="70%" width="70%">
</p>


### Discount \\( \gamma \\) is nice because
- It models the idea that sooner reward is better than later
<p align="center">
  <img src="../../img/post-img/reinforcement/4.png" height="60%" width="60%">
</p>
- It allows us to work with infinite horizons. Imagine two sequence of rewards that go on forever, cumulating the totals to infinity. It would not be possible to compare which sequence is better, because we cannot compare infinity. 
    * One way to fix this is to set a finite number of steps at which we stop the process. BUT this solution would give nonstationary policies (i.e. depending on the number of steps left, the policy might change)
    * Another way is to use the discount $$ \gamma $$ (usually has value within 0 and 1) that would converge the total to a finite amount (Geometric series) that we can then use to determine which sequence is better.
    <p align="center">
        <img src="../../img/post-img/reinforcement/5.png" height="90%" width="90%">
    </p>
- It's the only thing we have that works when we assume **stationary** preferences (once the optimal policy is found, it's forever optimal regardless of when it's used) 
    <p align="center">
        <img src="../../img/post-img/reinforcement/6.png" height="90%" width="90%">
    </p>


[1]: http://www0.cs.ucl.ac.uk/staff/d.silver/web/Teaching_files/MDP.pdf