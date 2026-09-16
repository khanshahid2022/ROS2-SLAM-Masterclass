```markdown
# 📝 Lesson 10: Visual Odometry & 3D Pose Estimation Assessment
Evaluate your structural understanding of Epipolar Geometry constraint equations, Essential Matrix composition parameters, and RANSAC geometric filtering loops.

---

### Question 1: The Core Mechanical Essence of Epipolar Geometry Constraints
When tracking spatial points across consecutive camera frame arrays inside a Visual Odometry tracking system, what is the precise geometric function of applying the Epipolar Constraint equation ($p_2^T E p_1 = 0$)?

- [ ] A) It regulates current consumption limits sent down to physical electric motors.
- [ ] B) It forces a pixel point in the first image frame to map exclusively onto a specific line vector path (the epipolar line) inside the subsequent second image frame, reducing matching computation searches from a 2D surface search area down to a 1D linear channel path.
- [ ] C) It transforms raw distance metrics collected by virtual LiDAR lasers over `/scan`.
- [ ] D) It calculates network synchronization bandwidth metrics targeting cloud server logs.

<details><summary><b>🔍 Click here for the Answer & Technical Reason</b></summary>

**Correct Answer: B**
* **Technical Reason:** Epipolar geometry describes the structural relationship between two camera perspectives looking at a mutual space point. The equation $p_2^T E p_1 = 0$ mathematically dictates that a point viewed in the first camera lens frame restricts where that identical point can exist inside the second view. It must lie on the projected epipolar line, meaning tracking algorithms don't have to look through the whole image to find a feature match; they just look along a single line vector path.
</details>

---

### Question 2: Decomposing the Essential Matrix Matrix Array
The Essential Matrix ($E = t^{\wedge} R$) is calculated live by processing matching local points across images. When we execute Singular Value Decomposition (SVD) loops over this matrix layout, what absolute physical properties are extracted?

- [ ] A) The exact thickness index of the camera glass cover housing.
- [ ] B) The compiler configuration names running the workspace setup files.
- [ ] C) The relative transformation parameters defining the three-dimensional Rotation matrix ($R$) and translation direction vector ($t$) separating the two camera frame capture viewpoints.
- [ ] D) The precise global coordinate position values referencing the root `map` origin frame.

<details><summary><b>🔍 Click here for the Answer & Technical Reason</b></summary>

**Correct Answer: C**
* **Technical Reason:** The Essential Matrix encapsulates the relative geometric displacement of the camera sensor frame across an increment of time. By decomposing it using Singular Value Decomposition matrix math, we isolate the fundamental geometric matrices: Rotation ($R$) and translation vector trajectory direction ($t$). This tells the tracking engine exactly how many degrees the platform turned and the direction axis it traveled between those two video frame frames.
</details>
