# 📝 Lesson 14: Autonomous Path Planning & Nav2 Stack Operations Assessment
Evaluate your structural understanding of A* path planning mechanics, static vs obstacle costmap layers, and behavior tree autonomous loops.

---

### Question 1: The A* Pathfinding Cost Function Mechanics
During autonomous navigation inside our custom Blender sandbox environment, the `nav2_navfn_planner` utilizes an A* search heuristic option (f(n) = g(n) + h(n)) to calculate paths. What do the parameters g(n) and h(n) represent mathematically inside the grid?

- [ ] A) g(n) controls the total current limits sent to wheels, while h(n) counts background compiler warning logs.
- [ ] B) g(n) represents the absolute accumulated cost to travel from the start node to the current node, while h(n) represents the estimated heuristic cost vector matching the distance from the current node straight to the target goal coordinates.
- [ ] C) g(n) monitors transform tree data packets over `/tf`, while h(n) parses camera byte matrices.
- [ ] D) Both parameters function exclusively to handle network buffering latency delays during data packet drops.

<details><summary><b>🔍 Click here for the Answer & Technical Reason</b></summary>

**Correct Answer: B**
* **Technical Reason:** The A* algorithm optimizes path planning efficiency by balancing historical path cost with forward projection. The function g(n) guarantees the pathfinder tracks the exact cost accumulated to reach the present position index. The heuristic function h(n) estimates the remaining line distance to the destination target. Combining them ensures the global planner selects the mathematically shortest, obstacle-free route across the costmap grid.
</details>

---

### Question 2: Resolving Layered Costmap Data Intersections
When Nav2 builds its spatial grid matrix arrays, it merges a `static_layer` and an `obstacle_layer` into a master costmap. What explicit functional difference separates these two information layers during live navigation?

- [ ] A) The static layer logs hardware profiles to disk, while the obstacle layer manages code compilation rules.
- [ ] B) The static layer processes permanent geometric layouts derived directly from the pre-saved blueprint map file, while the obstacle layer continuously intercepts high-frequency sensor streams (like LiDAR `/scan`) to dynamically insert or remove new temporary obstacles from the path tracking frame.
- [ ] C) The static layer executes exclusively inside C++ packages, while the obstacle layer functions inside Python scripts.
- [ ] D) The static layer manages ground plane physics, while the obstacle layer controls visual lighting features.

<details><summary><b>🔍 Click here for the Answer & Technical Reason</b></summary>

**Correct Answer: B**
* **Technical Reason:** Autonomous mobile systems must navigate around known structures while dynamically avoiding unexpected hazards. The `static_layer` provides the static foundation map (walls, pillars, structural contours) that doesn't change. The `obstacle_layer` processes real-time sensory tracking inputs (like laser distance readings), overlaying temporary obstacles (like boxes, equipment, or workers) onto the grid map so the local controller can safely deviate from the global plan to prevent a physical collision.
</details>
