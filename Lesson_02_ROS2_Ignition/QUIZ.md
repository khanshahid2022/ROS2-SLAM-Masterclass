# 📝 Lesson 02: ROS2 Ignition Performance Assessment

Evaluate your understanding of package repositories, environment structures, and path settings before moving forward.

---

### Question 1: Auto-Sourcing Automation Mechanics
Why do we append the string line `source /opt/ros/humble/setup.bash` directly inside the hidden configuration file `~/.bashrc`?

- [ ] A) It downloads new robotics packages automatically from the cloud database every morning.
- [ ] B) It forces the Linux terminal shell environment to dynamically load and register ROS2 executable commands instantly every time a new window session is booted up.
- [ ] C) It cleans the colcon workspace build cache automatically to prevent memory leaks.
- [ ] D) It accelerates the GPU graphic card rendering frequency for Gazebo rendering pipelines.

<details>
<summary><b>🔍 Click here for the Answer & Technical Reason</b></summary>

**Correct Answer: B**
* **Technical Reason:** The `~/.bashrc` script is executed automatically by the Bash shell layer whenever a new interactive shell session opens. Appending the sourcing command guarantees that your custom terminal path variables (`$PATH`, `$LD_LIBRARY_PATH`) are mapped to target ROS2 binary paths out-of-the-box.
</details>

---

### Question 2: Desktop Full Variant vs Base Engine
What is the structural consequence of installing `ros-humble-desktop` instead of `ros-humble-ros-base` on your robotics operating system workstation?

- [ ] A) The Base installation disables C++ modules and forces pure Python workflows.
- [ ] B) The Desktop installation completely bundles core network libraries alongside highly critical visual graphic rendering stacks like Rviz interfaces and Gazebo link simulations.
- [ ] C) The Base version can only run on real hardware chips and fails inside virtual containers.
- [ ] D) Desktop installation disables multi-robot DDS communication middleware layer protocols.

<details>
<summary><b>🔍 Click here for the Answer & Technical Reason</b></summary>

**Correct Answer: B**
* **Technical Reason:** `ros-humble-desktop` is a highly inclusive multi-package metapackage structure designed for developer workstations. It bundles visualization software frameworks (`rviz2`), UI display environments, and default simulation bindings alongside the fundamental communication core engines contained inside `ros-base`.
</details>
