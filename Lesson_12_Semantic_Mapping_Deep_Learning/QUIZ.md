# 📝 Lesson 12: Semantic Mapping & Deep Learning Integration Assessment
Evaluate your structural understanding of Semantic SLAM pipelines, neural network inference layers, and bounding box coordinate geometry.

---

### Question 1: The Core Distinction Between Geometric SLAM and Semantic SLAM
Traditional SLAM architectures (like `slam_toolbox` or pure Visual VO) process the environment as spatial point coordinate clouds. What is the explicit technical value of upgrading a mobile system to execute **Semantic SLAM** pipelines?

- [ ] A) It reduces the power consumption of electric traction drive wheelchair chassis motors.
- [ ] B) It combines structural coordinate calculations with deep learning classification filters, allowing the robot to map spatial coordinates while simultaneously recognizing the true object categories (labels) of surrounding obstacles.
- [ ] C) It forces the operating system kernel to delete temporary files inside build directories automatically.
- [ ] D) It moves the transformation tree tracking array parameters from C++ onto cloud servers.

<details>
<summary><b>🔍 Click here for the Answer & Technical Reason</b></summary>

**Correct Answer: B**

* **Technical Reason:** Geometric SLAM only provides spatial structures (e.g., "there is a boundary at coordinates X, Y, Z"). It does not understand what that boundary is. Semantic SLAM combines deep learning models (like YOLO) with spatial filters. This lets the tracking engine attach semantic parameters to the generated map grid, giving the platform true context awareness of its surroundings.
</details>

---

### Question 2: Resolving Dynamic Feature Tracking Drift via Classification Labels
When operating an autonomous self-driving AMR inside a highly crowded train terminal or fulfillment center, how do semantic label detections protect the robot's localization loop from experiencing massive position tracking errors?

- [ ] A) The model speeds up the clock update rate inside the simulation physics server.
- [ ] B) The system locks the wheel encoders to prevent any physical movement variations.
- [ ] C) The tracking frontend can read the classification tags to actively filter out and ignore feature points found on dynamic labels (like "person" or "moving vehicle"), ensuring the SLAM alignment engine calculates tracking changes using only static landmarks.
- [ ] D) The inference system compresses image footprints down to raw text arrays to free up disk storage space.

<details>
<summary><b>🔍 Click here for the Answer & Technical Reason</b></summary>

**Correct Answer: C**

* **Technical Reason:** Standard SLAM backends assume the world is perfectly static. If a group of people walks past a visual robot, the tracking loops will lock onto those moving pixels, causing the localization engine to think the robot itself is spinning or drifting. By running a semantic processor node, the system can instantly identify dynamic labels (like "person") and discard those feature vectors, using only static background data (like walls and pillars) to maintain pixel-perfect tracking consistency.
</details>
