# 🎮 Lesson 04: High-Performance 3D Simulation (Gazebo & Rviz Ignition)

Welcome to Module 4. In this segment, we bridge the gap between abstract code and full-scale 3D visual environments. You will learn why simulation is the lifeblood of advanced robotics, launch a virtual mobile robot inside a simulated physics world, and evaluate real-time laser scanner (LiDAR) data streams graphically without any lagging.

---

## 💡 Why is this Lesson Critical? (Real-World Applications)
1. **Crash Prevention:** Testing self-driving car logic or Visual SLAM pipelines on real hardware without simulation can lead to devastating physical collisions and equipment failure.
2. **Infinite Data Generation:** Simulation allows you to generate virtual testing tracking layouts (like mazes, factories, or houses) instantly to train your mapping algorithms before hardware integration.

---

## 🛠️ Step 1: Install Official Simulated Robot Dependencies
Open your standard workstation terminal window screen and execute package extractions:
```bash
cd ~/ros2_ws
sudo apt update
sudo apt install ros-humble-turtlebot3-gazebo ros-humble-turtlebot3-teleop -y
```

---

## 🛰️ Step 2: Configure the Digital Hardware Profile
ROS2 simulation stacks need to know which robot chassis model profile to allocate. We enforce the stable, dual-wheel LiDAR setup parameter globally:
```bash
cd ~/ros2_ws
echo "export TURTLEBOT3_MODEL=burger" >> ~/.bashrc
source ~/.bashrc
```

---

## 🎮 Step 3: Launch the 3D Physics Simulation World (Multi-Terminal Flow)

To ensure high-performance execution metrics without timeout boundary collisions, follow the sequential multi-terminal path matrix exactly:

### 🏠 Terminal Tab 1: Physics Engine Ingestion
```bash
# Target Location Context Initialization
cd ~/ros2_ws
source ~/.bashrc

# Ignition Launch
ros2 launch turtlebot3_gazebo turtlebot3_world.launch.py
```
*(If the spawn script parameters hit service timeouts on slower hardware frames, close the terminal loop and execute the manual split protocol below):*
```bash
# Alternative Split Ingestion Method if Service Timeouts occur:
ros2 launch gazebo_ros gazebo.launch.py
# (Then run in an independent terminal window to force drop model blueprints):
ros2 run gazebo_ros spawn_entity.py -entity burger -file /opt/ros/humble/share/turtlebot3_gazebo/models/turtlebot3_burger/model.sdf -x 0.0 -y 0.0 -z 0.01
```

### 🕹️ Terminal Tab 2: Remote Keyboard Teleoperation Control
Open a secondary terminal window/tab inside VS Code to handle movement parameters control grids:
```bash
# Target Location Context Initialization
cd ~/ros2_ws
source ~/.bashrc

# Run Keyboard Driving Node Handle
ros2 run turtlebot3_teleop teleop_keyboard
```
*Keep this terminal window context active. Use W, A, S, D, X elements to navigate the simulated robot body structure smoothly.*

### 📡 Terminal Tab 3: Sensor Stream Pipeline Auditing
Open a third terminal window/tab inside VS Code to check tracking data lines natively without GUI lagging:
```bash
# Target Location Context Initialization
cd ~/ros2_ws
source ~/.bashrc

# Audit Topic Channels Velocity
ros2 topic list
ros2 topic hz /scan
```
