# 🤖 Lesson 07: Custom Robot Synthesis (URDF Joint Frames Matrix & Kinematic Transformation Trees)
Welcome to Module 7. In this lesson, we break free from pre-built models and construct a custom mobile robot chassis from scratch. You will master the Unified Robot Description Format (URDF), define coordinate rigid bodies (Links) and physical intersections (Joints), orchestrate the foundational `/tf` (Transformation Tree) publisher pipelines, and audit your kinematic frame matrices live inside RViz2.

---

## 💡 Why is this Lesson Critical? (Real-World Applications)
1. **Custom Hardware Integration:** Industrial automation firms rarely use off-the-shelf educational chassis. To write autonomous code for a custom warehouse AMR, tow tractor, or robotic arm, you must explicitly describe its physical geometry to ROS2.
2. **The Backbone of Localization (`/tf`):** Sensors (LiDAR, Cameras) are physically mounted at different coordinates relative to the center of the wheels. URDF generates the explicit transform trees required to map laser distance metrics instantly back to the robot's center axis.
3. **Physics Engine Alignment:** Without highly precise inertial matrices and center-of-mass definitions in your model, simulators like Gazebo will experience collision clipping errors, tipping over, or friction simulation failures.

---

## 🛠️ Step 1: Install Robot Modeling & Joint Visualizers
To verify our custom kinematic structures dynamically without writing custom Python UI nodes, install the official joint state interfaces and parsing software expansions:
```bash
cd ~/ros2_ws
sudo apt update
sudo apt install ros-humble-joint-state-publisher-gui ros-humble-robot-state-publisher -y
```

---

## 🏗️ Step 2: Initialize Package Topology & Build Custom URDF Manifest Blueprint
To match our strict workspace directory layout rules, we will generate a dedicated configuration package inside our source tree before writing the raw XML structural framework data.

### 1. Generate Description Package Workspace
```bash
# Navigate to the workspace source area and create a clean CMake description package
cd ~/ros2_ws/src
ros2 pkg create --build-type ament_cmake masterclass_description

# Construct the dedicated internal URDF sub-module folder
mkdir -p ~/ros2_ws/src/masterclass_description/urdf
```

### 2. Save the URDF Geometric Parameters File
Create a new file named `custom_bot.urdf` inside your package layout:
```bash
code ~/ros2_ws/src/masterclass_description/urdf/custom_bot.urdf
```
Copy and paste this standard configuration directly inside `~/ros2_ws/src/masterclass_description/urdf/custom_bot.urdf`:

```xml
<?xml version="1.0"?>
<robot name="custom_masterclass_bot">

  <!-- Material Palette Colors Definition -->
  <material name="blue"><color rgba="0 0 0.8 1"/></material>
  <material name="black"><color rgba="0 0 0 1"/></material>

  <!-- 1. Base Footprint Projection (Ground Reference Frame Target) -->
  <link name="base_footprint"/>

  <!-- 2. Base Link Rigid Body Box Chassis Frame -->
  <link name="base_link">
    <visual>
      <geometry><box size="0.4 0.3 0.15"/></geometry>
      <material name="blue"/>
    </visual>
  </link>

  <joint name="base_footprint_to_base_link_joint" type="fixed">
    <parent link="base_footprint"/>
    <child link="base_link"/>
    <origin xyz="0 0 0.1"/>
  </joint>

  <!-- 3. Left Traction Driving Wheel Actuator Link -->
  <link name="left_wheel">
    <visual>
      <geometry><cylinder length="0.05" radius="0.08"/></geometry>
      <material name="black"/>
    </visual>
  </link>

  <joint name="left_wheel_joint" type="continuous">
    <parent link="base_link"/>
    <child link="left_wheel"/>
    <origin xyz="0 0.175 -0.02" rpy="-1.5708 0 0"/>
    <axis xyz="0 0 1"/>
  </joint>

  <!-- 4. Right Traction Driving Wheel Actuator Link -->
  <link name="right_wheel">
    <visual>
      <geometry><cylinder length="0.05" radius="0.08"/></geometry>
      <material name="black"/>
    </visual>
  </link>

  <joint name="right_wheel_joint" type="continuous">
    <parent link="base_link"/>
    <child link="right_wheel"/>
    <origin xyz="0 -0.175 -0.02" rpy="1.5708 0 0"/>
    <axis xyz="0 0 1"/>
  </joint>

</robot>
```

---

## 🏗️ Step 3: Orchestrate the URDF Workstation Pipeline
To execute and inspect your custom kinematic frames tree across your system environment layers, manage these three dedicated terminal window spaces:

### 🏠 Terminal Tab 1: Ignite the Robot State Publisher Matrix
This node parses the text-based XML URDF architecture file from our exact package deployment path and systematically broadcasts structural frame coordinate calculations onto the `/tf` and `/tf_static` network buses:
```bash
# Target Location Context Initialization
cd ~/ros2_ws
source ~/.bashrc

# Run Core State Publisher Engine over the exact package deployment location path
ros2 run robot_state_publisher robot_state_publisher \
    --ros-args -p robot_description:="\$(cat ~/ros2_ws/src/masterclass_description/urdf/custom_bot.urdf)"
```
*(Keep this active. It continuously outputs physical joint translation metrics down the communication layer).*

### 🕹️ Terminal Tab 2: Deploy Joint State Slider Controls Panel
Open a second terminal window/tab inside VS Code to inject artificial rotation angles dynamically into your moving components:
```bash
# Target Location Context Initialization
cd ~/ros2_ws
source ~/.bashrc

# Launch Graphical Input Interface Control Handle
ros2 run joint_state_publisher_gui joint_state_publisher_gui
```
*(A separate small utility UI panel containing slider lines representing `left_wheel_joint` and `right_wheel_joint` will populate the screen).*

### 🎨 Terminal Tab 3: RViz2 Hardware Verification Audit Terminal
Open a third terminal window/tab inside VS Code to display the physical link structures and structural frames tree:
```bash
# Target Location Context Initialization
cd ~/ros2_ws
source ~/.bashrc

# Ignite Clean Workspace Visualization Matrix
rviz2
```

---

## 🎮 Step 4: Calibrate Visualizations & Audit Kinematic Trees (RViz2 Moves)

Once the tools are running, perform these interactive moves sequentially to verify your structural setup:
1. Inside the left panels tree of **RViz2**, locate the **Fixed Frame** field and change it from `map` to `base_footprint`.
2. Click the **Add** button at the bottom-left panel, switch to the *By Display Type* index tab, select **RobotModel**, and click OK. Your custom blue box chassis alongside both black wheels will load instantly.
3. Click **Add** again, select **TF** (Transforms Frame Tree Display), and click OK.
4. **Watch the Matrix Work:** Arrange the window interfaces side by side. Drag the sliders inside your **Joint State UI Panel**. You will see the coordinate axes of the wheel links actively spin live in RViz2, confirming that the continuous math matrices are tracking without errors!

---

## 🔬 Step 5: Cross-Audit Kinematic Frame Transforms (Terminal Tab 4)
Open a fourth terminal tab window to double-check the real-time geometric network values:

### 1. Audit Live Transformation Tree Registries
```bash
source ~/.bashrc
ros2 run tf2_ros tf2_echo base_link left_wheel
```
*You will cleanly verify the exact spatial position matrix coordinates and quaternion rotational orientation structures tracking your joint configuration updates.*
