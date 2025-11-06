# CI2025_lab2

## Overview

This repository contains my solution for **Lab 2** of the course *Computational Intelligence (CI2025/26)*. It consists in solving several instances of the **Traveling Salesman Problem (TSP)** using **Evolutionary Computation (EC)**.

---

## Problem definition

The TSP is a classical combinatorial optimization problem. where a set of cities must be visited exactly once and the goal is to find the **shortest possible tour** returning to the starting city.

Given a set of `n` cities and a distance matrix `D`, the goal is to find the shortest possible tour that visits each city exactly once and returns to the starting point.

The distance matrix may contain positive or negative weights, allowing exploration of both standard and modified TSP variants.

---

## Representation of solutions

Each solution (tour) is represented as a **permutation** of integers from `0` to `N-1`, where `N` is the number of cities:

```
tour = [0, 4, 2, 1, 3]
```

This represents visiting city 0 → 4 → 2 → 1 → 3 → 0.

---

## Algorithm description

### 1. Initialization (tour creation and initial population)

The algorithm begins with an initial population of tours, initialized partly at random and partly using a **greedy heuristic** (nearest neighbor).  
This hybrid approach seems to be the best working one.
I tried with a random tour at first but I obtained much worse results. The functions for it are still part of the code, so it's possible to compare the two.

---

### 2. Evolutionary process

The main evolutionary loop repeats for a fixed number of generations:

1. **Fitness evaluation** — Each tour’s total length is computed.
2. **Selection** — Parents are selected via **tournament selection**, favoring shorter tours (with k=3).
3. **Crossover** — Two parents generate offspring using **Ordered Crossover (OX)**. Also **Inver-Over Crossover** was tried, but it made computing time much longer.
4. **Mutation** — Offspring are randomly perturbed through **inversion** mutation, that worked better then both **swap** and **insert** mutation.
5. **Elitism** — The best individuals from the previous generation are preserved, with a growing percentage (from 2% to 5%). This seemed to work better than a fixed %.

All of the functions that were tried during the process are still part of the code even though they're not used.
I used ChatGPT to help writing the inver_over_crossover and inver_over_crossover_fast functions.

---

## Experimental Results

For each instance, the best tour and computation time are recorded, along with the corresponding convergence plot.

```
![Best distance evolution for problem_g_10](results/problem_g_10_plot.png)
![Best distance evolution for problem_g_20](results/problem_g_20_plot.png)
![Best distance evolution for problem_g_50](results/problem_g_50_plot.png)
![Best distance evolution for problem_g_100](results/problem_g_100_plot.png)
![Best distance evolution for problem_g_200](results/problem_g_200_plot.png)
```

---

**Author:** [Riccardo Dattena (helped by ChatGPT for a couple of lines)]  
**Course:** Computational Intelligence (CI2025/26)  
**Lab 2 — Traveling Salesman Problem (EC)**
