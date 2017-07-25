---
layout: post
title: MDP & Reinforcement Learning
tags: [mdp, reinforcement-learning]
categories: notes
use-math: true
--- 
<!-- TOC -->

- [Deterministic vs. Stochastic Processes](#deterministic-vs-stochastic-processes)
- [The "Markov" Property](#the-markov-property)
- [Markov Decision Process (MDP)](#markov-decision-process-mdp)
- [Goal of MDPs](#goal-of-mdps)
- [Discount \\( \gamma \\) is nice because](#discount-\\-\gamma-\\-is-nice-because)
- [Solving MDPs](#solving-mdps)
    - [Important Terminology](#important-terminology)
    - [Bellman Equation](#bellman-equation)
- [Reinforcement Learning](#reinforcement-learning)
    - [Model-based](#model-based)
- [Passive RL](#passive-rl)
    - [Direct Evaluation (how is this related to passive RL)](#direct-evaluation-how-is-this-related-to-passive-rl)
- [Model-free](#model-free)
    - [Temporal Difference Learning (Value Learning)](#temporal-difference-learning-value-learning)
    - [Active RL (Q-learning)](#active-rl-q-learning)
- [How to pick actions](#how-to-pick-actions)
- [Game Theory](#game-theory)
    - [MiniMax = MaxiMin](#minimax--maximin)
    - [Von Neumann algorithm](#von-neumann-algorithm)
- [Nash Equilibrium (Non-Zero Sum)](#nash-equilibrium-non-zero-sum)
- [Stochastic Games](#stochastic-games)


### Deterministic vs. Stochastic Processes 
<p align="center">
  <img src="../../img/post-img/reinforcement/2.png" height="80%" width="80%">
</p>

### The "Markov" Property
<p align="center">
        <img src="../../img/post-img/reinforcement/7.png" height="90%" width="90%">
</p> [(source)][1]


### Markov Decision Process (MDP) 

<a name="mdp"></a>

A MDP includes: 
- Set of states S
- Start state s<sub>0</sub>
- Set of actions A
- Transitions T(s',s,a) or P(s'\|s,a) the probability of landing in state s' after taking action a from state s. Transitions are also called model, dynamics.
- Rewards R(s,a,s') and discount \\( \gamma \\)

### Goal of MDPs
is to return an optimal **policy** (a choice of action for each state). An **optimal** policy, denoted \\( \pi \\)* would maximize the sum of discounted rewards(**utility**), ie long term rewards over instaneous. 
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
If we know the MDP, then we can always apply **Value Iteration** to compute V*, Q\*, \\( \pi \\)\* exactly and **Policy Evaluation** to get the value for each state under a fixed policy.

consists of Policy Evaluation (to figure out the values) and One-Step-Look ahead (to actually update the policy)
- Achieves the exact same thing that Value Iteration does, but numberOfActions faster because at each State

<a name="rl"></a>

### Reinforcement Learning 

IRL we are not given the transitions or rewards for each state beforehand. That is we do NOT know the MDP. We have to actually **act** to learn those probabilities. 
<p align="center">
    <img src="../../img/post-img/reinforcement/8.png" height="90%" width="90%">
</p>

There are two approaches to the issue: 
- Model-based
- Model-free 	

#### Model-based
- **Overview**
> Step 1: Learn and formulate an empirical MDP model from experiences
> <br>
> Step 2: Solve for values as if the model was correct
- **Limitations**
> It's hard to draw the line where to stop learning and start solving
> <br>
> We'd only know what we have experienced 

- **Example** 
<p align="center">
    <img src="../../img/post-img/reinforcement/9.png" height="90%" width="90%">
</p>

### Passive RL
Similar to watching and learning from another robot = fixed policy, unknown rewards, unknown transitions
#### Direct Evaluation (how is this related to passive RL)
Since we don't have the rewards and transitions, we'll just run through the Grid World multiple times and record the Value for each State every time. After acting for quite some time over many episodes, you'd get the average and that's the value for each state. Why does this work? Same way things that have higher weight in the transitions would occur more often in the episodes.

?? state connections

<p align="center">
    <img src="../../img/post-img/reinforcement/10.png" height="90%" width="90%">
</p>

Limitations:
- We assume that we can revisit s many times 

### Model-free

#### Temporal Difference Learning (Value Learning)
Key idea: a model-free way to do policy evaluation by mimicking Bellman to update running sample average.
=> Still under fixed policy, update the value while we are running => **running average** (introducing \\( \alpha \\), learning rate)
<p align="center">
    <img src="../../img/post-img/reinforcement/11.png" height="90%" width="90%">
</p>
 which is usally about 0.1 so recently obtained values weigh more than old ones. Using this method, we would only need to update state value for the state we've just left and it only.
<p align="center">
    <img src="../../img/post-img/reinforcement/12.png" height="90%" width="90%">
</p>

Example:
<p align="center">
    <img src="../../img/post-img/reinforcement/13.png" height="90%" width="90%">
</p>

Limitations:
- We've now computed the state values, but still cannot infer which action to do at each state. In order to get actions, we need the one-step look ahead step (aka Q-value)

#### Active RL (Q-learning)
- Still don't know transactions and rewards
- BUT get to choose actions now
- To learn optimal policy and state values


<p align="center">
    <img src="../../img/post-img/reinforcement/13.png" height="90%" width="90%">
</p>

### How to pick actions
- do some fixed set of actions every time => won't learn
- randomly => won't use what it's learnt
- random start once it gets low Q-value => reinforce local min
Solution: **Exploration vs. Exploitation** using \\( \epsilon \\)-greedy algorithm (**simulated annealing**)

### Game Theory
A game tree can also be represented as a matrix
#### MiniMax = MaxiMin 
There always exists an *optimal **pure strategy** for each player in a game with
- 2-player
- zero-sum
- deterministic 
- perfect information

with **optimal** being defined as everyone is trying to maximize their own reward

#### Von Neumann algorithm 
non-deterministic

hidden info, i.e. info is not avail to all players => mixed strategies
ex: mini poker game
<p align="center">
    <img src="../../img/post-img/reinforcement/14.png" height="90%" width="90%">
</p>

Because everyone is acting rationally, in order to maximize with the mixed strategy, A would have to go with P = 0.4
<p align="center">
    <img src="../../img/post-img/reinforcement/15.png" height="50%" width="50%">
</p>

### Nash Equilibrium (Non-Zero Sum)
Given that you have a set of strategies \\( S_1^* \\)$,\\(S_2^* \\),\\(S_3^* \\), ...,\\(S_n^*\\) we know that they are in (John) Nash Equilibrium iff allowing a chance to switch strategies, a random player would have no reason to do it.

If the number of players and strategies are finite, then there always exists at least one Nash Equilibrium.
<p align="center">
    <img src="../../img/post-img/reinforcement/16.png" height="70%" width="70%">
</p>
n games => n repeated N.E.

### Stochastic Games

### TODO 
try running GridWorld yourself


[1]: http://www0.cs.ucl.ac.uk/staff/d.silver/web/Teaching_files/MDP.pdf