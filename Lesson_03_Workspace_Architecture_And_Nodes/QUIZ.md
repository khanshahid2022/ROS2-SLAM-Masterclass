# 📝 Lesson 03: Workspace Topology & Logic Mapping Assessment

Test your architectural knowledge regarding colcon compilers, package paths, script mappings, and multi-terminal parameters configuration.

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
* **Technical Reason:** The assignment syntax strictly structures targets: `'terminal_run_command = package_directory_folder.python_filename:function_entry_block'`. The name `core_telemetry_node` maps directly to your physical source file asset path on disk.
</details>

---

### Question 2: Multi-Terminal Execution Logic
Why do we need a separate third terminal tab window to run the `ros2 param set` command while testing active ROS2 node configurations?

- [ ] A) Parameters can only communicate with the system kernel when run inside odd-numbered terminal structures.
- [ ] B) Running parameters inside a busy publishing terminal forces the underlying DDS communication middleware layer to crash.
- [ ] C) Terminal Tab 1 is dedicated to running the executable node loop process, and Terminal Tab 2 is actively blocking to print continuous echo topics; hence a fresh decoupled workspace terminal context handle is mandatory to issue asynchronous CLI runtime tuning commands.
- [ ] D) The third terminal window acts as a localized temporary cache system folder for `colcon build`.

<details>
<summary><b>🔍 Click here for the Answer & Technical Reason</b></summary>

**Correct Answer: C**
* **Technical Reason:** ROS2 executable runs (like spinning a node or echo streaming topics) are blocking operations that hold the terminal's thread execution handle open. Intercepting or tuning parameters on-the-fly requires opening an independent operational workspace terminal window context path to speak with the active network node architecture.
</details>
