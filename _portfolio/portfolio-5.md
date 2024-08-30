---
title: "Motion Planning (Click Here!)"
excerpt: "The overall objective of this assignment was to find valid paths from a starting point to an endpoint in a variety of environments. The project 1) implements a collision checker to ensure your path does not collide with any obstacles, 2) implements a search-based algorithm to find a path, and 3) implements a sampling-based algorithm to find a path. <br/><img src='/images/flappy_bird_b_2.png'>"
collection: portfolio
---
[Full Report](/files/Project_2_ECE_276B.pdf)

*Full code can be provided upon request*

## Introduction
Autonomous robotic navigation is essential in modern robotics, allowing robots to function independently in complex environments. Advanced navigation systems combine sensors, algorithms, and learning techniques to enhance safety, reduce human involvement, and broaden the range of tasks robots can perform. These advancements are especially valuable in dangerous or hard-to-reach areas where human presence is either impractical or risky.

### Search-Based Path Planning
Search-based path planning involves guiding a robot from one location to another by representing the environment as a grid or network. Algorithms like Dijkstra's or A* (A-star) are used to determine the most efficient route while avoiding obstacles. This method is effective in well-structured environments with clearly defined layouts, enabling precise movement planning.

### Sampling-Based Path Planning
Sampling-based path planning is used in complex or multi-dimensional spaces where traditional grid-based methods might not be practical. Algorithms like Rapidly-exploring Random Trees (RRT) or Probabilistic Roadmaps (PRM) randomly generate points to create a network of potential paths, linking safe, navigable paths while avoiding obstacles. This approach is particularly useful in large or unstructured environments, offering flexibility and computational efficiency.

### Project Objectives
The project focuses on developing and evaluating motion planning algorithms in three-dimensional environments with rectangular obstacles. The objectives include implementing a collision-checking algorithm to ensure safety in 3-D space, creating a search-based planning algorithm with efficient collision detection, and either developing a sampling-based planning algorithm like RRT or utilizing existing motion planning libraries.

## Problem Formulation

### Path Planning in a 3D Environment

**Scenario:**
- A three-dimensional space with a defined starting point, an endpoint, and boundaries.
- A set of rectangular obstacles that are aligned with the axes.

**Goal:**
Identify a path that:
- Starts at the given point and ends at the target location.
- Remains within the defined boundaries and avoids all obstacles.

**Requirements:**
- The path must be continuous and within the boundaries.
- The path must avoid all obstacles.
- Optionally, the path should be optimized to minimize the total distance traveled.

### Collision Detection between Line Segments and Rectangular Obstacles in 3D Space
This involves determining whether a line segment intersects with any rectangular obstacles in three-dimensional space, which is crucial for ensuring the path's safety.

**Scenario:**
- A rectangular obstacle defined by its minimum and maximum corners.
- A line segment defined by its two endpoints.

**Goal:**
Determine if the line segment intersects any rectangular obstacles in the 3D space by:
- Describing the segment and checking for intersections with the boundaries of each obstacle.

## Technical Approach

### Pybullet's Collision Detection
We utilized the PyBullet library’s collision detection function for determining potential intersections between a ray and objects in the simulation environment. This function efficiently identifies possible intersections and provides detailed information, which is valuable in robotics and interactive environments.

### A-Star Algorithm
The A* algorithm finds the shortest path by minimizing a cost function that combines the actual cost from the start and an estimated cost to the goal.

**Key Elements:**
- **Heuristic Function:** Estimates the distance to the goal.
- **Movement Options:** Identifies valid movements from the current position while checking for collisions and boundary constraints.
- **Path Reconstruction:** Traces back from the goal to the start to produce the complete path.

### Bi-Directional RRT Algorithm
The Bi-Directional Rapidly-exploring Random Trees (Bi-Directional RRT) algorithm builds two trees, one starting from the initial point and the other from the goal, to find paths in complex spaces.

**Key Elements:**
- **Step Size:** Sets the distance between points in the trees.
- **Goal Bias:** Adjusts how often the random point is directed toward the goal.
- **Maximum Iterations:** Determines when the algorithm should stop.

## Results
The results showed that Bi-Directional RRT generally produces shorter paths than A-star, though it takes longer in environments with many obstacles. A-star tends to create smoother paths in complex environments, while Bi-Directional RRT is more effective in simpler settings. The number of samples required by Bi-Directional RRT varies with environmental complexity, influencing the time it takes to find a solution.

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
The project successfully developed and evaluated motion planning algorithms in three-dimensional environments with rectangular obstacles. The collision-checking algorithms ensured path safety, while the search-based and sampling-based planning algorithms were tested for their efficiency and adaptability. A* was found to be more effective in complex environments, while Bi-Directional RRT excelled in simpler settings, highlighting the importance of choosing the right algorithm based on the specific challenges of the environment.



