---
title: "The maze problem"
date: 2024-12-15
draft: true
summary: "Using different algorithms to solve the maze problem"
tags: ["study"]
---

As part of one of my courses on the foundations of Artificial Intelligence we are going through algorithms for problem solving and search. One of the assignments that we had was to solve the maze problem with the Simulated Annealing algorithm and the Tabu search algorithm.

### The maze problem
Imagine you have a maze and you want to find the most effective (i.e. the shortest in this case) path to get out of it. (!!! insert image)
One way to go through it is to represent the maze as an undirected graph, where each node is a possible place for you to step in, and each edge is a possible direction you can take (right, left, up or down). For simplicity I generated a grid graph with the very useful library networkx and eliminated the nodes that correspond to coordinates of walls. Now I don't need to penalize movements that step into walls as those edges are also nonexistent. Now I have the list of nodes and edges, which translate into the space we can walk around to find the exit.

### Initial solution
The implementation of simulated annealing and tabu search requires an initial solution to improve. In this case, I decided to go for Depth First Search (DFS), just because. Nothing very fancy, I set the priority of directions in the following order: right, up, left, down (i.e. we will try to go right first). By storing the explored cells we avoid stepping twice into a cell, which ensures we're one step closer to getting an efficient solution. In the frontier list we store the places we can visit based on the exploration in previous steps, so we can choose another direction if we get stuck with the initial path we chose.
I will not explain in detail the design of the algorithm, but check out this paper (!!! insert paper) talking about it and how it can be implemented.
A graphical explanation is easier to understand, so here you are (!!! insert animation).

### Implementing simulated annealing
This algorithm is based on the properties of atom allocation while welding metals, and this paper (!!! insert paper) walks you though how this algorithm was used for the allocation of cables in a electronic board.

### Implementing Tabu search