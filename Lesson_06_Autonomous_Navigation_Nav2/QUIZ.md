# 📝 Lesson 06: Autonomous Navigation & Costmaps Operations Assessment
Evaluate your structural understanding of dual-loop path planning pipelines, multi-layered costmap arrays, and system navigation safety mechanisms.

---

### Question 1: The Global Planner vs. Local Controller Dichotomy
During an autonomous navigation mission, the global planner (`navfn_planner`) and local controller (`dwb_controller`) perform distinct physical roles. What is the explicit architectural difference between their computational outputs?

- [ ] A) The Global Planner generates raw wheel voltages, while the Local Controller generates high-level map metadata grids.
- [ ] B) The Global Planner calculates the complete, macro obstacle-free route from start to target using the static map, while the Local Controller processes high-frequency real-time updates to generate immediate linear/angular `/cmd_vel` steering inputs.
- [ ] C) The Global Planner updates the transformation tree inside `/tf`, while the Local Controller directly commands the physical LiDAR lasers.
- [ ] D) The Global Planner acts as a backup system only when the local behavior trees crash due to network drops.

<details><summary><b>🔍 Click here for the Answer & Technical Reason</b></summary>

**Correct Answer: B**
* **Technical Reason:** Mobile robotics operates on a hierarchical execution pipeline. The Global Planner evaluates the entire static macro environment once to create an overall reference track line (A* or Dijkstra math). However, it cannot handle instantaneous sensor changes. The Local Controller runs at a much higher execution loop rate (e.g., 20Hz), actively reading immediate laser ranges to avoid dynamic obstacles and convert the global line into accurate physical steering variables.
</details>

---

### Question 2: The Critical Anatomy of Costmap Inflation Layers
In Nav2 costmap configurations (`global_costmap` and `local_costmap`), what is the precise mathematical and engineering purpose of tuning the `inflation_radius` parameter array?

- [ ] A) It compresses the memory scale of the underlying `.pgm` graphic array to increase network upload bandwidth.
- [ ] B) It accelerates the clock update rate (`use_sim_time`) inside the simulation engine environment.
- [ ] C) It expands an artificial obstacle cost boundary outwards around static walls, matching or exceeding the robot's physical radius, ensuring path planning algorithms do not treat the platform as a single dimensionless point and collide the physical chassis.
- [ ] D) It generates automatic loop closures to reset errors building up inside wheel odometry profiles.

<details><summary><b>🔍 Click here for the Answer & Technical Reason</b></summary>

**Correct Answer: C**
* **Technical Reason:** Standard robotic grid pathfinders reduce the robot's footprint to a single point index for rapid calculation. If the map walls were left uninflated, the path planner would route a line right next to a brick wall. When the physical robot tracks that path, half of its physical body would smash into the wall. The `inflation_radius` builds a proactive gradient cost barrier that forces planners to calculate paths that respect the real-world geometry of the machine.
</details>
