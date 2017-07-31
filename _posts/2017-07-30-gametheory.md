---
layout: post
title: Game Theory
tags: [reinforcement-learning]
categories: notes
use-math: true
--- 
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
