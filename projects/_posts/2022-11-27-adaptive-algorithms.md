---
layout: projects
title: Some Adaptive and Cooperative Algorithms
tag: Software
description: A handful of search/optimizer algorithm implementations in Python
tools: Python
img: /Media/projects/ece457a/ant_colony_optimization.png
---

In my 4A term at UWaterloo, I took ECE457A: Cooperative and Adaptive Algorithms, which required the implementation of several deterministic and heuristic-based optimization methods. This post will show results for some of the more interesting trajectory and population based algorithms applied to ill-structured problems.

## Simulated Annealing
<a href="https://gist.github.com/andrewmourcos/42f20d542be6df6dc22cf2ffbeaf38bc">Implementation.</a>

This trajectory-based algorithm extends typical hill-climbing optimizers by introducing the idea of an acceptance function. As the algorithm evaluates nearby candidate states, it uses a probabilistic acceptance function to choose whether to move to the next state or not - in particular this was used:

$$
  P_{accept}=\begin{cases}
    1, & \text{if better state}.\\
    e^{-\text{(how much worse)}/T}, & \text{if worse state}.
  \end{cases}
$$

Where T is the "annealing temperature" (experimented with a fixed, geometrically decreasing, and linearly decreasing T). The idea behind allowing worse states is to allow the optimizer the chance to escape local minima and promote exploration.

## Tabu Search
<a href="https://gist.github.com/andrewmourcos/ddea08fd1c717c4db01c33150933fd95">Implementation.</a>

This is another trajectory-based optimization method, although its approach is quite different from simulated annealing. It operates on the principle of avoiding repeated moves by tracking them in a "tabu structure" for some predefined tenure. The optimizer evaluates all neighbouring solution candidates, but is restricted from accepting solutions that are in the tabu structure (with some exceptions, referred to as "aspirations"). In the code snippet, I ran a few experiments to optimize for a quadratic assignment problem. In general, it performed well but it's a bit tricky to find suitable hyperparameters for different problems.

## Genetic Algorithm
<a href="https://gist.github.com/andrewmourcos/35147543e5b4ad812f9d24f5f715340e">Implementation.</a>

This was a pretty neat evolutionary algorithm. In essence, a population of candidate solutions are generated and evaluated based on their "fitness". The best candidates become "parents" to child solutions (made via cross-over of two parents with randomized mutations) and the cycle restarts. Ideally, every generation is better than the last by promoting the most fit individuals and their offspring.

## Ant Colony Optimization
<a href="https://gist.github.com/andrewmourcos/9af91ae014dba563fdc50dfbc9eb2eab">Implementation.</a>

Here, I implemented an ant colony algorithm to optimize a 29-city traveling salesman problem. I used a pseudo-random proportional rule for transitions (as proposed by Gambardella & Dorigo) and an online delayed pheromone update rule - hoping to balance exploration and exploitation of the search algorithm. A nice thing about this implementation is that ant populations could be spawned in parallel - so I used the opportunity as multi-threading practice.
<img src="/Media/projects/ece457a/ant_colony_optimization.png">
*Ant colony optimization on Traveling Salesman Problem*

Well, the algorithm evidently worked, achieving a minimum round-trip distance of 8845.61km after less than 100 iterations. Note that the optimal solution had a trip distance of 8782.60km - so pretty close.

## Particle Swarm Optimization
<a href="https://gist.github.com/andrewmourcos/515e4cde3beddad154f9c2736183e80d">Implementation.</a>

This was probably my favourite adaptive/cooperative algorithm to implement - it's both easy to code and can provide some very satisfying animations as shown below.

<img src="/Media/projects/ece457a/particle_swarm.gif">
*Particle swarm optimizer applied to a 2D Camelback function; Red dot = global best*

Here, particles are initialized to random locations in the search space. Each record local and global "bests" to which surrounding particles are attracted in hopes of converging to a global optimum (candidate exploitation). An inertial term is added to the velocity update equations for particle motion to encourage exploration and avoid convergence to local optima.