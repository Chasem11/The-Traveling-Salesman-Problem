# Traveling Salesman Problem Using Ant Colony Optimization (ACO)

## Overview
This project applies **Ant Colony Optimization (ACO)** to the **Traveling Salesman Problem (TSP)**, a well-known NP-hard optimization challenge. The objective in TSP is to compute the shortest possible path that visits all cities exactly once and returns to the origin. Because the problem becomes computationally expensive as the number of cities increases, metaheuristic solutions like ACO provide a practical alternative to exact algorithms.

The ACO approach used here models decision-making behavior observed in natural ant colonies. Virtual ants traverse a graph of cities while probabilistically selecting routes based on pheromone strength and heuristic desirability. Over multiple iterations, pheromone evaporation and reinforcement guide the algorithm toward shorter, more optimal solutions.

This notebook implements the full ACO process, supports experiment-driven parameter tuning, and visualizes performance outcomes.

## Project Scope
* **Implement** a customizable ACO algorithm for solving the TSP.
* **Compare** the performance impact of different parameter configurations.
* **Visualize** both initial and optimized solutions using plotted city graphs.
* **Evaluate** the algorithm’s effectiveness based on percent improvement from initial random routes.

## Methodology

### Algorithm Structure
The system is implemented using an object-oriented design consisting of several core components:

| Component | Function |
| :--- | :--- |
| **City** | Stores coordinate positions and computes Euclidean distances. |
| **PheromoneMatrix** | Maintains pheromone concentrations for each directed path. |
| **ProbabilityCalculator** | Calculates transition probabilities using pheromone influence ($\alpha$) and heuristic distance influence ($\beta$). |
| **Ant** | Simulates a full traversal of the route using probabilistic movement. |
| **ACO** | Coordinates the algorithm lifecycle, iteration loop, pheromone updates, and best-path tracking. |

### Route Construction and Transition Logic
Ants begin from randomly selected cities and build a complete tour using weighted probabilities. The probability of moving from one city to another is proportional to:

$$P \propto (\text{pheromone}^\alpha) \times \left( \frac{1}{\text{distance}^\beta} \right)$$

This mechanism integrates both **historical success** (pheromone trails) and **spatial efficiency** (distance).

### Pheromone Update Strategy
After all ants complete their tours:
1. **Evaporation:** Pheromone values decay by a specified evaporation factor.
2. **Reinforcement:** New pheromone is added inversely proportional to tour length, reinforcing shorter routes.

The balance between evaporation and reinforcement prevents premature convergence and maintains exploration.

### Termination Condition
The algorithm stops after a fixed number of iterations. The shortest path observed across all iterations is recorded as the final result.

---

## Experiments and Findings
Three focused experiments were conducted to measure how varying parameters affect solution quality. Each experiment was repeated multiple times and analyzed using average percent improvement over the initial random path.

### 1. Number of Ants
* **Tested values:** 10, 20, 30
* **Result:** Increasing ant count generally improved the solution.
* **Observation:** **30 ants** produced the highest average improvement across trials.

### 2. Evaporation Rate
* **Tested values:** 0.25, 0.50, 0.75
* **Result:** Higher evaporation values performed better.
* **Best performing value:** **0.75**
* **Interpretation:** Stronger evaporation reduces stagnation and helps prevent early bias toward suboptimal paths.

### 3. Pheromone Deposit Factor
* **Tested values:** 0.50, 0.75, 1.0
* **Result:** Differences were smaller, but **0.75** produced the most optimal and consistent outcomes across runs.

## Results Summary
* The algorithm consistently generated shorter routes than the initial randomized tour.
* The percent improvement metric demonstrated clear sensitivity to parameter selection.
* The best performing configuration included:
    * Higher ant counts
    * Higher evaporation rate
    * Moderate pheromone deposit factor
* Visual comparisons confirmed that refined routes eliminated unnecessary travel branching and produced tighter loops.

## Conclusion
This project demonstrates that Ant Colony Optimization is an effective metaheuristic approach for approximating high-quality solutions to the Traveling Salesman Problem. The algorithm successfully reduced travel distance relative to initial random routes and responded predictably to parameter adjustments.
