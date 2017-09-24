---
layout: post
title: Expectimax and Non-Zero Sum Games
tags: [AI]
categories: notes
---
- **Utility(X)** = how much you actually value this X
- **Lottery L(0.3, 5; 0.7, 10)** = $$0.3\times{Utility(5)} + 0.7\times{Utility(10)}$$

### Expectimax
- Still zero-sum games
- But in this case, our opponent is not adversarial i.e. non-optimal, and will pick next action based on some probability. Therefore, instead of alternating between max/min levels, we alternate between max/chance levels where each chance node is a weighted average of all the children, with the weight being the probability that that child is reached.
- Minimax is insensitive to monotonic transformations, which means states with better evaluations stay better after the transformations. This is not the case with expectimax.
<p align="center">
    <img src="../../img/post-img/reinforcement/non-adversarial/1.png" height="50%" width="50%">
</p>
<p align="center">
    <img src="../../img/post-img/reinforcement/non-adversarial/2.png" height="50%" width="50%">
</p>
- This model renders the Alpha-Beta pruning useless
- Minimax is too pessimitic and is worst when the world is random, while expectimax is too optimistic, thus worst when the world is adversarial.


### Expectiminimax
- Seen in games such as Backgammon where the environment can be seen as another player.
- Combines Minimax and Expectimax

### Non-Zero Sum Games
- Cooperation might emerge 
- Terminals are in tuple form.
- Similar to Expectimax, the Alpha Beta pruning does not apply here.