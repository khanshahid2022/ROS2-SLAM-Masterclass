# 📝 Lesson 07: Custom Robot URDF Modeling Operations Assessment
Evaluate your structural understanding of links, joint tracking arrays, rigid body parameters, and transform tree mechanics.

---

### Question 1: Distinct Structural Anatomy of Links vs. Joints
When architecting physical hardware descriptions within a custom URDF manifest file, what is the explicit operational difference between a `<link>` structural label and a `<joint>` structural label?

- [ ] A) A link contains software package descriptions, while a joint controls cloud network logging frameworks.
- [ ] B) A link defines a distinct rigid body coordinate envelope (mass, visual shape, collision boundary), while a joint calculates the spatial frame translation, rotation limitations, and kinematic parent-child link relationships connecting those bodies together.
- [ ] C) A link intercepts the `/scan` topic, while a joint manages velocity parameters over `/cmd_vel`.
- [ ] D) Links are written exclusively in Python code scripts, while joints are generated using binary C++ compiler systems.

<details><summary><b>🔍 Click here for the Answer & Technical Reason</b></summary>

**Correct Answer: B**
* **Technical Reason:** A URDF models a robot as an acyclic graph of rigid frames. The `<link>` segment strictly stores properties about the physical body section itself (how long it is, what color it displays, how its mass is weighted). The `<joint>` segment acts as the mathematical link vector that calculates exactly how one body frame moves or shifts relative to another parent frame reference point.
</details>

---

### Question 2: Decoupled Multi-Joint Tracking Types
In the constructed custom robot configuration, the wheel components are specified with `type="continuous"`, while the main body assembly is locked using `type="fixed"`. What mathematical tracking rule separates these configurations inside the `/tf` matrix?

- [ ] A) A fixed joint lacks parent definitions, while continuous joints completely ignore coordinate boundaries.
- [ ] B) Fixed joints maintain static geometric offset transform metrics permanently on the `/tf_static` bus, while continuous joints accept dynamic angular state rotations that shift orientation fields over a single rotational axis on the active `/tf` bus.
- [ ] C) Fixed joints only activate during simulator ignition cycles, while continuous joints operate exclusively inside localized hardware matrices.
- [ ] D) A continuous joint requires physical internet loop connections to calculate alignment bounds.

<details><summary><b>🔍 Click here for the Answer & Technical Reason</b></summary>

**Correct Answer: B**
* **Technical Reason:** Fixed joints describe structural assemblies that never bend or slide (e.g., a chassis frame bolted directly onto its baseline). Because the transform math never changes, ROS2 optimizes computation by broadcasting it to `/tf_static`. A continuous joint allows infinite 360-degree rotation (like wheel axles or motor shafts), meaning its mathematical frame angles change dynamically over time based on joint encoder updates, requiring continuous processing on the active `/tf` stream.
</details>
