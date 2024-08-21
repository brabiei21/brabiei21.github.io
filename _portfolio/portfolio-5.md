---
title: "Motion Planning"
excerpt: "The overall objective of this assignment was to find valid paths from a starting point to an endpoint in a variety of environments. The project 1) implements a collision checker to ensure your path does not collide with any obstacles, 2) implements a search-based algorithm to find a path, and 3) implements a sampling-based algorithm to find a path. <br/><img src='/images/flappy_bird_b_2.png'>"
collection: portfolio
---
[Full Report](/files/Project_2_ECE_276B.pdf)

*Full code can be provided upon request*

## Introduction
Autonomous robotic navigation is a critical aspect of modern robotics, enabling robots to operate independently in complex environments. The development of advanced navigation systems leverages sensors, algorithms, and learning techniques to enhance safety, reduce human labor, and extend the range of tasks robots can perform. These advancements are particularly valuable in hazardous or inaccessible areas, where human intervention is impractical or dangerous.

### Search-Based Path Planning
Search-based path planning involves navigating a robot from one point to another by mapping the environment into a grid or graph. Algorithms like Dijkstra's or A* (A-star) are used to find the most efficient route while avoiding obstacles. This method is effective in structured environments where the layout is well-defined, allowing for precise movement planning.

### Sampling-Based Path Planning
Sampling-based path planning is a strategy used in complex or high-dimensional spaces where traditional grid-based methods may be impractical. Algorithms like Rapidly-exploring Random Trees (RRT) or Probabilistic Roadmaps (PRM) randomly generate points to form a roadmap of possible paths, connecting safe, navigable paths and avoiding obstacles. This approach is beneficial in large or unstructured environments, offering flexibility and computational efficiency.

### Project Objectives
The project aims to develop and evaluate motion planning algorithms in 3-D environments with rectangular obstacles. The objectives include implementing a collision-checking algorithm for safety in 3-D space, creating a search-based planning algorithm with efficient collision detection, and either developing a sampling-based planning algorithm like RRT or utilizing established motion planning libraries.

## Problem Formulation

### Path Planning in a 3D Environment

**Given:**
- A 3D space \( \mathbb{R}^3 \) with a starting point \( s \), an endpoint \( e \), and a boundary \( B \).
- A set of axis-aligned bounding box obstacles \( \{O_1, O_2, \dots, O_n\} \).

**Objective:**
Find a path \( P: [0, 1] \rightarrow \mathbb{R}^3 \) such that:
- \( P(0) = s \) and \( P(1) = e \).
- \( P(t) \) remains within \( B \) and avoids all obstacles \( O_i \).

**Mathematical Formulation:**
- **Continuity Constraint:** \( P \) should be continuous.
- **Boundary Constraint:** \( P(t) \in B \) for all \( t \).
- **Obstacle Avoidance:** \( P(t) \not\in O_i \) for all \( t \) and \( i \).
- **Path Optimality (optional):** Minimize \( \int_0^1 \lVert \frac{dP}{dt} \rVert \, dt \).

### Collision Detection between Line Segments and AABBs in 3D Space
The problem is to determine whether a line segment intersects any axis-aligned bounding boxes (AABBs) in 3D space, essential for ensuring path safety.

**Given:**
- An AABB characterized by its minimum and maximum corners.
- A line segment specified by two endpoints.

**Objective:**
Determine if the line segment intersects any AABB within the 3D space by:
- Parameterizing the segment and checking for intersections with the bounding limits of each AABB.

## Technical Approach

### Pybullet's Collision Detection
We used the PyBullet library's \texttt{rayTest()} function for collision detection. This function uses broadphase and narrowphase detection to efficiently identify potential intersections between a ray and objects in the simulation environment. The function returns detailed hit information, facilitating various applications in robotics and interactive environments.

### A-Star Algorithm
The A* algorithm finds the shortest path by minimizing the cost function \( f(n) = g(n) + h(n) \), where \( g(n) \) is the actual cost from the start node, and \( h(n) \) is a heuristic estimate to the goal.

**Key Components:**
- **Heuristic Function:** Uses Euclidean distance for estimation.
- **Motion Possibilities:** Determines valid movements from the current node while checking for collisions and boundary constraints.
- **Path Reconstruction:** Backtracks from the goal to the start node to yield the complete path.

### Bi-Directional RRT Algorithm
The Bi-Directional Rapidly-exploring Random Trees (Bi-Directional RRT) algorithm builds two trees, one from the start and the other from the goal, to find paths in high-dimensional spaces.

**Key Components:**
- **Step Size:** Defines the distance between nodes in the trees.
- **Goal Bias:** Adjusts how often the random node is set to the goal.
- **Maximum Iterations:** Sets a stopping condition for the algorithm.

## Results
The results indicate that Bi-Directional RRT generally finds shorter paths than A* but takes longer in environments with many obstacles. A* provides smoother paths in complex environments, while Bi-Directional RRT is more effective in simpler environments. The number of samples required by Bi-Directional RRT varies with environmental complexity, affecting runtime.

**Figure 1:** Single Cube Map.
<table>
  <tr>
    <td><img src="/images/single_cube_a.png" alt="map" width="200" /></td>
    <td><img src="/images/single_cube_b_2.png" alt="map" width="200"/></td>
  </tr>
</table>

**Figure 2:** Maze Map.
<table>
  <tr>
    <td><img src="/images/maze_a.png" alt="map" width="200" /></td>
    <td><img src="/images/maze_b_2.png" alt="map" width="200"/></td>
  </tr>
</table>

**Figure 3:** Flappy Bird Map.
<table>
  <tr>
    <td><img src="/images/flappy_bird_a.png" alt="map" width="200" /></td>
    <td><img src="/images/flappy_bird_b_2.png" alt="map" width="200"/></td>
  </tr>
</table>

**Figure 4:** Monza Map.
<table>
  <tr>
    <td><img src="/images/monza_a.png" alt="map" width="200" /></td>
    <td><img src="/images/monza_b_2.png" alt="map" width="200"/></td>
  </tr>
</table>

**Figure 5:** Window Map.
<table>
  <tr>
    <td><img src="/images/window_a.png" alt="map" width="200" /></td>
    <td><img src="/images/window_b_2.png" alt="map" width="200"/></td>
  </tr>
</table>

**Figure 6:** Tower Map.
<table>
  <tr>
    <td><img src="/images/tower_a.png" alt="map" width="200" /></td>
    <td><img src="/images/tower_b_2.png" alt="map" width="200"/></td>
  </tr>
</table>

**Figure 7:** Room Map.
<table>
  <tr>
    <td><img src="/images/room_a.png" alt="map" width="200" /></td>
    <td><img src="/images/room_b_2.png" alt="map" width="200"/></td>
  </tr>
</table>


## Conclusion
The project successfully developed and evaluated motion planning algorithms in 3-D environments with rectangular obstacles. The collision-checking algorithms ensured path safety, while search-based and sampling-based planning algorithms were tested for their efficiency and adaptability. A* was found to be more effective in complex environments, while Bi-Directional RRT excelled in simpler settings, underscoring the importance of algorithm selection based on specific environmental challenges.
