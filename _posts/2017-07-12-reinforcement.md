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
            - [Policy Extraction](#policy-extraction)
        - [2. Policy Iteration](#2-policy-iteration)
            - [Policy Evaluation](#policy-evaluation)
- [Reinforcement Learning](#reinforcement-learning)
    - [1. Model-based](#1-model-based)
    - [2. Model-free](#2-model-free)
        - [Passive RL](#passive-rl)
            - [Direct Evaluation]()
            - [Temporal Difference Learning]()
        - [Active RL](#active-rl)
            - [Q-learning](#q-learning)
            - [Value-learning](#value-learning)

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
    1. Assign random value to each state (usually 0)
    2. Use the Bellman equation above to update the values
    3. Repeat step 2 until values converge (i.e. they no longer change much, or the change is under some pre-defined threshold)
- Efficiency is O($$a*s^2$$) per iteration because we have to visit each state to do the updates and at each state, there's potentially s number of states because all of the states could be interconnected.
- Limitations: <a id="policy-extraction"></a>
    - Can take a long time to converge, and policy usually converges way before values do. See demo [here]().
    - Once we have the optimal values, they do not right away tell us what action to take unless we do **Policy Extraction** for every state 
        - from values
    \begin{equation}
        \pi^\*(s) = arg\max_{a}(R(s) + \gamma\sum_{s'}P(s,a,s')V^\*(s'))
    \end{equation}
        - from Q-values
    \begin{equation}
        \pi^\*(s) = arg\max_{a}(R(s) + \gamma*Q^\*(s,a)
    \end{equation}
- In this example, the triangles represent the state values with 0, 1, 2 time steps left bottom up and the circles represent the corresponding Q-values
    <p align="center">
        <img src="../../img/post-img/reinforcement/18.png" height="75%" width="75%">
    </p>
<a id="policy-evaluationgamma"></a>
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
- **Algorithm**
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
- **Temporal Difference learning of Values** 
The name is from the difference between two adjacent states 
    1. Assign random value (usually 0) to each state
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

### Active RL
We still don't know the transactions and rewards BUT get to choose actions now (no fixed policy). Goal is to learn the state values AND the optimal policy.
#### Q-learning
aka the Temporal Difference learning of Q-values. This is superior to the TD of values because we can extract the policy directly by taking $$\pi{s}$$ = argmax_{a}Q(s,a)
- **Overview**:
    1. "Receive" a sample Q(s,a)
    2. This sample suggests 
    \begin{equation}
        Q(s,a) = sample \approx R(s,a,s') + \gamma\max_{a'}Q(s',a')
    \end{equation}
    3. Average over samples from (s,a) by keeping a running average
    \begin{equation}
        Q(s,a) \leftarrow (1 - \alpha)Q(s,a) + \alpha[r + \gamma\max_{a'}Q(s',a')]
    \end{equation}
- **Off-policy learning** The great thing about Q-learning is that we can still learn the optimal policy while behaving suboptimally every now and then, compared to other techniques aforementioned in which one suboptimal move affects the state values directly. See [demo]().
- Caveats: keep learning rate small but not decreasing too quickly
- **Schemes for forcing exploration**
    - **$$\epsilon$$-greedy**
        - At every time step, flip a coin
        - With (small) probability $$\epsilon$$, act randomly
        - With (high) probability $$1-\epsilon$$, act on current policy
        - Lower $$\epsilon$$ over time to avoid unnecessary explorations once learning is done
        Simply speaking, it means when choosing the best action, select the best action with a probability of (1 - $$\epsilon$$) and a random action with a probability of $$\epsilon$$. When we decay $$\epsilon$$, the model starts taking fewer and fewer random actions after each trial and it slowly transitions from exploration to exploitation.
    - **Using Exploration functions** is the idea of exploring areas whose badness is not (yet) established.
    <p align="center">
        <img src="../../img/post-img/reinforcement/19.png" height="80%" width="80%">
    </p>
- **Regret** = the difference between the (expected) rewards including youthful suboptimality, and optimal (expected) rewards.

### Value learning

### Feature-based Q-learning
When we have a lot of states and lots of actions to choose from, it is too much to hold in memory so we switch to feature-based representation.

## 2. Policy Search

### References
I used the sources below to make this post.

- [RL by David Silver](http://www0.cs.ucl.ac.uk/staff/d.silver/web/Teaching_files/MDP.pdf)
- [CS 188 AI](https://www.youtube.com/watch?v=W1S-HSakPTM&list=PLIZQvCoJVokgKBNx210mkXEk4FeSOGfWu)