---
layout: post
title: Markov Models
tags: [AI]
categories: notes
---
<!-- TOC -->

- [Chain Rule and Markov Models](#chain-rule-and-markov-models)
- [Mini-forward Algorithm](#mini-forward-algorithm)
- [Hidden MM](#hidden-mm)

<!-- /TOC -->
### Chain Rule and Markov Models

<p align="center">
    <img src="../../img/post-img/markov-models/1.png" height="80%" width="80%">
</p>

Past independent of Future = Future independent of Past ???
<p align="center">
    <img src="../../img/post-img/markov-models/2.png" height="80%" width="80%">
</p>
Note the last assumption, probably means transitions are unchanged for this type of problem.

$$
\begin{align}
P(X_{t}) & = \sum_{x_{t-1}} P(X_{t}, x_{t-1}) \\
 & = \sum_{x_{t-1}} P(X_{t}|x_{t-1}) \times P(x_{t-1})
\end{align}
$$

### Mini-forward Algorithm

### Hidden MM
special type of Bayes Net which keeps going on forever
comprised of 
- P($$X_{1}$$)
- transitions $$P(X_{t} \| P_{t-1})$$
- Emission P(E \| X)