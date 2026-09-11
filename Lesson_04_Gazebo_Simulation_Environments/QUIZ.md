# 📝 Lesson 04: Simulation Environments Performance Assessment

Evaluate your logical understanding of split-ignition simulation protocols, robot spawning mechanics, and real-time sensor stream evaluations.

---

### Question 1: The Multi-Terminal Split Spawning Strategy
Why do pro robotics developers launch the empty `gazebo.launch.py` environment container in Terminal Tab 1 first, before running the `spawn_entity.py` command inside a separate Terminal Tab 2 session?

- [ ] A) Split spawning automatically increases the dual-wheel motor velocity by 20%.
- [ ] B) The physics simulation server (`gzserver`) requires initialization boot time; running a combined script can trigger service timeout boundaries if the model drops before the core plugins finish registering.
- [ ] C) Spawning scripts can only execute when run inside even-numbered terminal structures.
- [ ] D) The split protocol transforms the underlying database compilation system from Python into CMake files.

<details>
<summary><b>🔍 Click here for the Answer & Technical Reason</b></summary>

**Correct Answer: B**
* **Technical Reason:** The ROS2 Gazebo factories require structural synchronization handshakes. Launching the empty engine container first guarantees that the background factory services are completely up, active, and responsive, allowing the subsequent entity script to drop the robot blueprints smoothly into coordinates space without hitting timeout drops.
</details>

---

### Question 2: Environmental Global Flag Injection (`TURTLEBOT3_MODEL`)
Why do we inject the variable assignment configuration `export TURTLEBOT3_MODEL=burger` directly inside the system's `~/.bashrc` file during setup?

- [ ] A) It accelerates internet connection domain resolution download pipelines.
- [ ] B) It forces the ROS2 launch engine to automatically know the exact structural definitions, kinematics dimensions, and sensor topologies of the target robot chassis configuration during ignition.
- [ ] C) It automatically deletes malicious temporary build configuration cache directories.
- [ ] D) It switches the programming framework compilation type from Python to C++.

<details>
<summary><b>🔍 Click here for the Answer & Technical Reason</b></summary>

**Correct Answer: B**
* **Technical Reason:** Launch scripts rely on system environment variables to isolate package nodes profiles dynamically. Defining the structural keyword string locks the framework into processing calculations matching the small dual-wheel `burger` robotics profile automatically across terminal window sessions.
</details>
