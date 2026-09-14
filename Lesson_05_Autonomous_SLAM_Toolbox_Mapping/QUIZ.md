# 📝 Lesson 05: SLAM Engine Operations Assessment

Evaluate your structural understanding of mapping nodes inputs, map persistence outputs, and core spatial coordinate translations.

---

### Question 1: The Essential Dual Inputs of SLAM
To successfully calculate real-time spatial loop closures and paint an accurate occupancy grid map, what two distinct fundamental data topic channels does `slam_toolbox` actively intercept and require?

- [ ] A) Camera color video streams (`/image_raw`) and dynamic joystick parameters.
- [ ] B) Laser distance metrics scanner array lines (`/scan`) alongside continuous calculated wheel orientation movement odometry data transformations grids (`/odom`).
- [ ] C) GPU graphic processor utilization counters and internet connection speed metrics.
- [ ] D) Python executable configurations module names and workspace build file paths.

<details>
<summary><b>🔍 Click here for the Answer & Technical Reason</b></summary>

**Correct Answer: B**
* **Technical Reason:** Simultaneous Localization and Mapping requires balancing two sensor realities. Wheel odometry (`/odom`) tells the engine roughly how much the robot moved (but drifts over time), while LiDAR scanner vectors (`/scan`) track the relative positions of structural walls. The SLAM algorithm continually correlates both inputs via probability math to remove drift error.
</details>

---

### Question 2: The Core Anatomy of Saved Robotics Maps
When you execute the `map_saver_cli` utility handle, the server outputs two standalone files: a `.pgm` asset file and a `.yaml` asset file. What is the explicit technical purpose of the generated `.yaml` configuration file?

- [ ] A) It contains the raw C++ code scripts required to execute the robot's steering parameters.
- [ ] B) It stores user authentication logging profile parameters for cloud network updates.
- [ ] C) It holds highly critical spatial alignment calibration metadata metrics—such as real-world pixel-to-meter resolution ratios and frame origin coordinate translation data constants—allowing future navigation stacks to read the image accurately.
- [ ] D) It compresses the image package file footprint memory scale dynamically to free up disk storage space.

<details>
<summary><b>🔍 Click here for the Answer & Technical Reason</b></summary>

**Correct Answer: C**
* **Technical Reason:** A standalone grid image (`.pgm`) is just raw pixel colors. The companion `.yaml` configuration manifest file contains the absolute scaling parameters matrix that translates pixel coordinate array indices directly into physical real-world SI engineering tracking units (meters), which is mandatory for autonomous global path planners.
</details>
