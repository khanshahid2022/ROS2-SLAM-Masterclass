# 📝 Lesson 03: Workspace Topology & Logic Mapping Assessment

Test your architectural knowledge regarding colcon compilers, package paths, script mappings, and parameters interaction.

---

### Question 1: The `setup.py` Entry Point Anatomy
In a ROS2 python package, look at this routing registration line inside `setup.py`:  
`'telemetry_shortcut = project_vision_pkg.core_telemetry_node:main'`  
What does the component text parameter value `core_telemetry_node` directly represent?

- [ ] A) The internal network identity lookup ID displayed inside `ros2 node list`.
- [ ] B) The exact physical file name of the Python script (`.py` file) stored inside your package source folder vault directory.
- [ ] C) The default name string identifier assigned to topic communication channels.
- [ ] D) The standard compilation library dependency macro inside CMake platforms.

<details>
<summary><b>🔍 Click here for the Answer & Technical Reason</b></summary>

**Correct Answer: B**
* **Technical Reason:** The assignment syntax strictly structure targets: `'terminal_run_command = package_directory_folder.python_filename:function_entry_block'`. The name `core_telemetry_node` maps directly to your physical source file asset path on disk.
</details>

---

### Question 2: The Critical Dynamic Parameter Advantage
Why do pro robotics developers utilize ROS2 Parameters (`self.declare_parameter`) instead of hardcoding raw string or numeric variables directly inside loop equations blocks?

- [ ] A) Parameters automatically boost system thread processing speed configurations by 50%.
- [ ] B) Hardcoded elements crash instantly when running inside graphic simulation containers.
- [ ] C) It grants full operational capabilities to modify, inject, or tune threshold logic variables dynamically at runtime from external CLI commands without terminating or re-building software packages code layers.
- [ ] D) Parameters force the `colcon build` tool to clean temporary caches files automatically during runtime execution handshakes.

<details>
<summary><b>🔍 Click here for the Answer & Technical Reason</b></summary>

**Correct Answer: C**
* **Technical Reason:** Parameters act as a native configuration microservice. They expose selected state definitions variables openly across the distributed computing graph network layer, allowing fast on-the-fly tuning operations (like shifting laser calibration thresholds or camera visual matching metrics targets) instantly from the CLI.
</details>
