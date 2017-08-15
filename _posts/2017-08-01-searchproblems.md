---
layout: post
title: Search Problems
tags: [AI, reinforcement-learning]
categories: notes
use-math: true
--- 
# Uninformed Search

**Uninformed** here means while exploring the search trees, we do not know if we are getting closer to a goal or not.

**Fringe**: nodes waiting in a queue to be explored.

### Depth-first Search (DFS) 
- LIFO queue, push to front, pop from front
- Time complexity O(\\(b^m\\)) where b is the branching factor
- Space complexity O(\\(b*m\\))
- Optimal: not guaranteed
- Works better when solution is deep + to the left

### Breath-first Search (BFS)
- FIFO queue, push to front, pop from back
- Time complexity O($$b^s$$) 
- Space complexity O($$b^s$$)
- Optimal: yes if cost = 1
- Works better when solution is shallow + to the right and in most cases

### Iterative Deepening
DFS with a twist that exploits the space complexity of DFS and the time complexity of BFS by imposing depth limit at each iteration.

### Uniform Cost Search (UCS)
- now edges are labeled with costs
- priority queue, push so-far path cost, pop cheapest path
- stay as low total cost as possible 
- UCS == BFS when costs are all equal.


# Informed Search
Uses a heuristic to tell if we've moved closer to a goal after every move.
### Heuristic
 A **heuristic** gives an estimate of how close we are to a goal and is designed for a particular search problem. Usually denoted as $$h(x)$$. 
 
 States that are closer to the goal have a lower heuristic value and the goal state has a heuristic value of 0.

### Greedy Search 
- follows heuristic, completely ignores costs
- therefore, it is not always be optimal

### A* Tree Search
- **Idea**: combines UCS and Greedy: methodically check everything that might be optimal but can prove that sth is suboptimal before heading that direction too deep thanks to a heuristic.
    - Example: 
        <p align="center">
            <img src="../../img/post-img/reinforcement/search/1.png" height="50%" width="50%">
        </p>
- **NOTE:** We only stop when we deque a goal from a fringe, not prematurely  when we enqueue a goal.

<p align="center">
        <img src="../../img/post-img/reinforcement/search/2.png" height="40%" width="40%">
    </p>

- UCS is a special case where h(every node) = 0

- **Optimality** A* is only optimal when the heuristic is **admissible**, i.e. it slows down bad plans but the estimated cost from a state is never more than the the actual cost incurred from the shortest path to a goal from that state.

    In the example below, A* would give us the lower path, which is not optimal. What went wrong is that the estimated cost h(A) = 6 is higher than the actual cost of 3 to get to the goal. 
<p align="center">
    <img src="../../img/post-img/reinforcement/search/3.png" height="40%" width="40%">
</p> 

- **Inadmissible** heuristics are often useful in determining a path to a goal fast because A* now behaves more like greedy.
- We want to pick a heuristic that expands the least amount of nodes but does not take too much time to compute.

### A* Graph Search
- **Improvement**: never expand a state twice
- **Implementation**:
    - A* Tree search + set of expanded states("closed set")
    - Before expanding a node, check to see if it has been expanded before, i.e. if it is in the closed set
    - If yes, skip it, if new, add to closed set
- **BUT** A* graph search might wreck optimality. In the example below, since we have already expanded C, we would not expand it again on the left, thus forgoing the optimal path. 
    <p align="center">
        <img src="../../img/post-img/reinforcement/search/4.png" height="60%" width="60%">
    </p> 
$$\rightarrow$$ Heuristic used also needs consistency which is stronger than admissibility for search to be optimal.
- **Consistency** heuristic "arc" cost $$\leqslant$$ actual cost for each arc
\begin{equation}
    h(A)-h(C) \leqslant cost (A to C)
\end{equation}
Example of a heuristic being inconsistent.
    <p align="center">
        <img src="../../img/post-img/reinforcement/search/5.png" height="20%" width="20%">
    </p> 
which leads to this huge "discovery" that **the f value along a path never decreases** because
\begin{equation}
    h(A) \leqslant cost (A to C) + h(C)
\end{equation}
and that A* graph search is optimal.