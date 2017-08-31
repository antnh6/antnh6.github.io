---
layout: post
title: Adversarial Search (Minimax)
tags: [AI]
categories: notes
---
- **Determinisitc**, **zero-sum** games, e.g. checkers, chess, tic-tac-toe, etc. 
- Pure competition, one player **maximizes** result, one **minimizes**

- **Minimax values**
<p align="center">
    <img src="../../img/post-img/reinforcement/adversarial/1.png" height="70%" width="70%">
</p>

- Implementation: 
just like exhaustive DFS 
<p align="center">
    <img src="../../img/post-img/reinforcement/adversarial/2.png" height="70%" width="70%">
</p>

$$\rightarrow$$ In realistic games, we cannot search to leaves (computation cost).

$$\rightarrow$$Solution: **depth-limited search**
- Search only to a limited depth in the tree
- Replace terminal utilities with an **evaluation function** for non-terminal positions (use iterative deepening for an anytime algorithm). 

IRL, we typically use a weighted linear sum of many evaluation functions. An evaluation function is similar to a heuristic in a way that it is customized to each problem.
<p align="center">
    <img src="../../img/post-img/reinforcement/adversarial/3.png" height="70%" width="70%">
</p>
$$\rightarrow$$ An important example of the tradeoff between complexity of features and complexity of computation, i.e. going deeper into the tree is better, but it costs more.

### Minimax downfall
It turns out that depth matters a lot here, but the computation gets ugly really fast with every level down
$$\rightarrow$$ Pruning is this notion that for some nodes, we got to look at all of its children, for some, we don't.
<p align="center">
    <img src="../../img/post-img/reinforcement/adversarial/4.png" height="70%" width="70%">
</p>

### Alpha-Beta Pruning
Minimax works but it is awfully slow, especially once we get to a depth that can produce reasonable result in practice (at the leaf level there's $$branching factor^depth$$ evaluations).
This is where alpha-beta pruning comes in. It's Minimax with a flourish to help with efficiency by expanding fewer nodes that needs evaluating.
<p align="center">
    <img src="../../img/post-img/reinforcement/adversarial/5.png" height="70%" width="70%">
</p>
<p align="center">
    <img src="../../img/post-img/reinforcement/adversarial/6.png" height="70%" width="70%">
</p>


### Iterative/Progressive Deepening
DFS with iterative depth
