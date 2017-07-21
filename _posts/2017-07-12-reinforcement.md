---
layout: post
title: MDP & Reinforcement Learning
tags: [mdp, reinforcement-learning]
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

### Markov Decision Process (MDP)
A MDP includes: 
- Set of states S
- Start state s<sub>0</sub>
- Set of actions A
- Transitions T(s',s,a) or P(s'\|s,a) the probability of landing in state s' after taking action a from state s. Transitions are also called model, dynamics.
- Rewards R(s,a,s') and discount \\( \gamma \\)

### Goal of a MDP
is to return a **policy** (a choice of action for each state). An **optimal** policy, denoted \\( \pi \\)* would maximize the sum of discounted rewards (**utility**), thus depending on the reward for each state.
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
- It's the only thing we have that works **if** we assume **stationary** preferences (once the optimal policy is found, it's forever optimal regardless of when it's used). However, that does not mean our preferences always have to be stationary.
    <p align="center">
        <img src="../../img/post-img/reinforcement/6.png" height="90%" width="90%">
    </p>

### Solving MDPs
#### Important Terminology
- **Q\*(s,a)** is the average utility over all possible states s' that you can fall in after performing action a from current state s, then acting optimally from s' onward. For example, you're a robot in a Grid World. You want to move East, but will only land on the East state with 0.8 probability, 0.1 probability you will land on the other perpendicular States (North and South). Q\*(s, East) will be the average (discounted*Value + Reward(next State)) over all possible next States (East, North, and South in this case). 
- **V\*(s)** is is the expected max among all Q\*(s,a) i.e. for each state, you'd have a bunch of Q-values, V\*(s) would be the max among them. Continuing on the above example, V\*(s) would be the max among Q*(s, East), Q\*(s, West), Q\*(s,North), and Q\*(s, South).
- Note that **\*** here denotes that we are following the optimal policy. It could be substituted with \\( \pi \\) to mean some specific policy (need not be optimal) that looks like this Q<sup>\\( \pi \\)</sup>(s,a).

#### Bellman Equation
aka Value Iteration

#### Policy Evaluation 
#### Policy Iteration 
consists of Policy Evaluation (to figure out the values) and One-Step-Look ahead (to actually update the policy)
- Achieves the exact same thing that Value Iteration does, but numberOfActions faster because at each State

### Reinforcement Learning
The distinction between MDP and RL is that IRL we are not given the transitions or rewards for next state beforehand. We have to actually **act** to learn those probabilities. 
<p align="center">
    <img src="../../img/post-img/reinforcement/8.png" height="90%" width="90%">
</p>
 There are two approaches to the issue: 

| |Model-based | Model-free |	
|:---:|:---:|:---:|
|**Overview**| Step 1: Learn and formulate an empirical MDP model from experiences
| |Step 2: Solve for values as if the model was correct|
|**Limitations**|- It's hard to draw the line where to stop learning and start solving | 	|
| |- We'd only know what we have experienced | 
|**Example**| <img src="../../img/post-img/reinforcement/9.png"> | 

### Passive RL
#### Direct Evaluation
Every time you enter a state, record the Value for that State. After acting for quite some time over many episodes, you'd get the average and that's the value for each state under some policy. Why does this work?Same way things that have higher weight in the transitions would occur more often in the episodes.

?? state connections

[1]: http://www0.cs.ucl.ac.uk/staff/d.silver/web/Teaching_files/MDP.pdf