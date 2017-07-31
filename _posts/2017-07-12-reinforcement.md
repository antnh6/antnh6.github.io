---
layout: post
title: MDP & Reinforcement Learning
tags: [mdp, reinforcement-learning]
categories: notes
use-math: true
--- 
- [Markov Decision Process (MDP)](#markov-decision-process-mdp)
        - [Deterministic vs. Stochastic Processes](#deterministic-vs-stochastic-processes)
        - [The "Markov" Property](#the-markov-property)
    - [Goal of MDPs](#goal-of-mdps)
    - [Discount \\( \gamma \\) is nice because](#gamma)
    - [Important Terminology](#important-terminology)
    - [Solving finite-state MDPs](#solving-finite-state-mdps)
        - [1. Value Iteration](#1-value-iteration)
        - [2. Policy Iteration](#2-policy-iteration)
- [Reinforcement Learning](#reinforcement-learning)
    - [1. Model-based](#1-model-based)
    - [2. Model-free](#2-model-free)
        - [Passive RL](#passive-rl)
            -[Direct Evaluation]()
            -[Temporal Difference Learning]()
        - [Active RL (Q-learning)](#active-rl-q-learning)
            - [Q-learning](#q-learning)
<!--         - [How to pick actions](#how-to-pick-actions)
        - [Uninformed Search](#uninformed-search)
        - [Cost = 1](#cost-1)
        - [When cost is involved](#when-cost-is-involved)
        - [TODO](#todo)
        - [References](#references) -->

# Markov Decision Process (MDP) 
A MDP includes: 
- Set of states S
- Start state s<sub>0</sub>
- Set of actions A
- **Transitions** T(s',s,a) or P(s,a,s') the probability of landing in state s' after taking action a from state s. Transitions are also called model, dynamics.
- **Immediate Reward** R(s,a,s') for leaving state s and **discount** \\( \gamma \\)

### Deterministic vs. Stochastic Processes 
<p align="center">
  <img src="../../img/post-img/reinforcement/2.png" height="55%" width="55%">
</p>

### The "Markov" Property 
[^1]
<p align="center">
        <img class = "img-responsive" src="../../img/post-img/reinforcement/7.png" height="60%" width="60%">
</p>
## Goal of MDPs
is to return an optimal **policy** (a choice of action for each state). An **optimal** policy, denoted \\( \pi \\)* would maximize the sum of discounted rewards (**utility**), ie long term rewards over instaneous. 
<p align="center">
  <img src="../../img/post-img/reinforcement/3.png" height="50%" width="50%">
</p>

<a id="gamma"></a>

## Discount \\( \gamma \\) is nice because
- It models the idea that sooner reward is better than later.
<p align="center">
  <img src="../../img/post-img/reinforcement/4.png" height="50%" width="50%">
</p>
- It allows us to work with infinite horizons. Imagine two sequence of rewards that go on forever, cumulating the totals to infinity. It would not be possible to compare which sequence is better, because we cannot compare infinity. 
    * One way to fix this is to set a finite number of steps at which we stop the process. BUT this solution would give nonstationary policies (i.e. depending on the number of steps left, the policy might change)
    * Another way is to use the discount $$\gamma$$ (usually has value within 0 and 1) that would converge the total to a finite amount (Geometric series) that we can then use to determine which sequence is better.
    <p align="center">
        <img src="../../img/post-img/reinforcement/5.png" height="60%" width="60%">
    </p>
- It's the only thing we have that works **if** we assume **stationary** preferences (once the optimal policy is found, it's forever optimal regardless of when it's used). However, that does not mean our preferences always have to be stationary.
    <p align="center">
        <img src="../../img/post-img/reinforcement/6.png" height="55%" width="55%">
    </p>

## Important Terminology
- **Q\*(s,a)** is the average utility over all possible states s' that you can fall in after performing action a from current state s, then acting optimally from s' onward. For example, you're a robot in a Grid World. You want to move East, but will only land on the East state with 0.8 probability, 0.1 probability you will land on the other perpendicular States (North and South). Q\*(s, East) will be the average (discounted*Value + Reward(next State)) over all possible next States (East, North, and South in this case). 
- **V\*(s)** is is the expected max among all Q\*(s,a). That is, for each state, you would have a bunch of Q-values, V\*(s) would be the max among them. Continuing on the above example, V\*(s) would be the max among Q\*(s, East), Q\*(s, West), Q\*(s,North), and Q\*(s, South).
- Note that **\*** here denotes that we are following the optimal policy. It could be substituted with \\( \pi \\) to mean some specific policy (need not be optimal) that looks like this $$Q^{\pi}(s,a)$$.
- The **Bellman equations** for $$V^\pi$$ expresses a recursive relationship between the value of a state and the value of its successor states.
\begin{equation}
    V^\*(s) = \max_{a}Q^*(s,a) 
\end{equation}

\begin{equation}
    Q^\*(s) = R(s) + \gamma\sum_{s'}P(s,a,s')V^*(s')
\end{equation}

which can be written in one line as follows
\begin{equation}
    V^\*(s) = R(s) + \max_{a}\gamma\sum_{s'}P(s,a,s')V^\pi(s')
\end{equation}

## Solving finite-state MDPs
Below are two efficent algorithms for doing so. They are basically the same, all variations of Bellman updates.
### 1. Value Iteration
- Algorithm
    1. Assign random value to each state ???? Need values for states with 0 time steps
    2. Use the Bellman equation above to update the values
    3. Repeat step 2 until values converge (i.e. they no longer change much, or the change is under some pre-defined threshold)
- Efficiency is O($$a*s^2$$) per iteration because we have to visit each state to do the updates and at each state, there's potentially s number of states because all of the states could be interconnected.
- Limitations:
    - Can take a long time to converge, and policy usually converges way before values do. See demo [here]().
    - Once we have the optimal values, they do not right away tell us what action to take unless we do **Policy Extraction** for every state 
    \begin{equation}
        \pi^\*(s) = arg\max_{a}(R(s) + \gamma\sum_{s'}P(s,a,s')V^\*(s'))
    \end{equation}
    Knowing Q-values will be easier to select actions than knowing values!
    \begin{equation}
        \pi^\*(s) = arg\max_{a}(R(s) + \gamma*Q^\*(s,a)
    \end{equation}
- In this example, the triangles represent the state values with 0, 1, 2 time steps left bottom up and the circles represent the corresponding Q-values
    <p align="center">
        <img src="../../img/post-img/reinforcement/18.png" height="75%" width="75%">
    </p>

### 2. Policy Iteration
- **Policy Evaluation** calculates values for a fixed policy $$\pi$$
    \begin{equation}
        V_0^\pi(s) = 0 
    \end{equation}
    \begin{equation}
        V_{k+1}^\pi(s) = R(s) + \gamma\sum_{s'}P(s,a,s')V_k^\pi(s')
    \end{equation}     
- Algorithm
    1. Create a random policy by selecting a random action for each state
    2. Run Policy Evaluation until values converge
    3. Do Policy Extraction to update the policy  
    4. Repeat 2 and 3 until policy converges 
- Efficiency of Policy Evaluation is O($$s^2$$) per iteration because we have to visit each state to do the updates and at each state, there's at most s states to land on if all states are interconnected. 
<a name="rl"></a>
This algorithm achieves the exact same thing (the optimal values) as Value Iteration, but in most cases faster thanks to step 2, which begs a question: Why would we ever use Value Iteration? The answer is that it's simpler than PI, so when we only have a small number of actions, we might as well just do it. 

-------------------------------------------------------------------

# Reinforcement Learning 

In real life, we are not given the transitions or rewards beforehand. That is we do NOT know the MDP. We have to actually **act** to get information about those parameters, i.e. **Online learning** vs. **Offline learning** where we know all of the parameters beforehand.

There are two approaches to the issue:

## 1. Model-based
- **Algorithm **
1. Learn and formulate an empirical/approx. MDP model from experiences
    - Estimate P(s,a,s')
    - Discover R(s,a,s')
2. Solve for values by using VI or PI as if the model was correct
- **Limitations**
    - It's hard to draw the line where to stop learning and start solving
    - We'd only know what we have experienced 
- **Example** 
<p align="center">
    <img src="../../img/post-img/reinforcement/9.png" height="65%" width="65%">
</p>

## 2. Model-free
### Passive RL
learn the values under a fixed policy
- **Direct Evaluation** 
    1. Run through the grid world following a fixed policy and record value for each state
    2. Repeat step 1 over many episodes. 
    3. Calculate the average value for each state
    - **Why does this work?** Same way things that have higher weight in the transitions would occur more often in the episodes.
    - **Example**
    <p align="center">
        <img src="../../img/post-img/reinforcement/10.png" height="65%" width="65%">
    </p>
    - **Limitation** It wastes information about state connections.
    <p align="center">
        <img src="../../img/post-img/reinforcement/17.png" height="20%" width="20%">
    </p>
**However**, this method is not practical because we cannot just rewind time to get sample after sample from state s.
- **Temporal Difference Learning** 
a model-free way to do Policy Evaluation
    1. Assign random value to each state
    2. Experience to get empirical value, then move old value a little bit toward this newly acquired value: running average
    - **Why does this work?** Likely outcomes will contribute updates more often.
    - $$\alpha$$ is called a **learning rate**
        <p align="center">
            <img src="../../img/post-img/reinforcement/11.png" height="60%" width="60%">
        </p>
    - The exponential running average effectively makes recent samples more important (forgets about the past).
        <p align="center">
            <img src="../../img/post-img/reinforcement/12.png" height="35%" width="35%">
        </p>
    - **Example**
<p align="center">
    <img src="../../img/post-img/reinforcement/13.png" height="60%" width="60%">
</p>

However, we still cannot infer actions from these values because the transitions are still unknown. 

### Active RL (Q-learning)
We still don't know the transactions and rewards BUT get to choose actions now (no fixed policy). Goal is to learn the state values AND the optimal policy.
#### Q-learning
to compute $$V^*$$, $$Q^*$$, $$\pi^*$$
    \begin{equation}
        Q_{k+1}(s,a) \leftarrow \sum_{s'}P(s,a,s')[R(s,a,s') + \gamma\max_{a'}Q_{k}(s',a')]
    \end{equation}
#### Value learning
to evaluate a fixed policy $$\pi$$

### How to pick actions
- do some fixed set of actions every time => won't learn
- randomly => won't use what it's learnt
- random start once it gets low Q-value => reinforce local min
Solution: **Exploration vs. Exploitation** using \\( \epsilon \\)-greedy algorithm (**simulated annealing**)


 

### Uninformed Search

**World State** = all possible configurations of the world
**State space**

Solving search problems
- State space graphs (a math concept that this problem can be solved by drawing out all the configurations lol)
- Search trees 

Search algorithm properties:
- Optimal: least cost path
- Complete
- Time complexity 
- Space complexity 

### Cost = 1
DFS 
- LIFO stack
- Time complexity O(\\(b^m\\))
- Space complexity O(\\(b*m\\))
- Optimal: not guaranteed
- Works better when solution is deep + to the left

BFS
- FIFO queue
- Time complexity O($$b^s$$) 
- Space complexity O($$b^s$$)
- Optimal: yes if cost = 1
- Works better when solution is shallow + to the right and in most cases

Iterative Deepening
DFS with a twist that exploits the space complexity of DFS and time of BFS

### When cost is involved 
Uniform Cost Search is similar to BFS, but it does return the least cost path
- priority queue
- hmm i still need to understand this


### TODO 
try running GridWorld yourself

Cost-sensitive Search
### References
These are all the sources I used to make this post.

[^1]: http://www0.cs.ucl.ac.uk/staff/d.silver/web/Teaching_files/MDP.pdf