# 🚀 Lesson 06: Autonomous Navigation 2 (Path Planning, Costmaps, and Nav2 Stack Exploration)
Welcome to Module 6. In this lesson, we transform our static occupancy grids into fully reactive spatial cost environments. You will discover why the Nav2 stack is mandatory for production-grade mobile platforms, orchestrate the architectural pipelines that generate Global Paths and Local Steering Commands, configure layered Costmaps to guarantee hardware crash safety, and execute multi-terminal pathfinding operations directly inside your workstation workstation layer.

---

## 💡 Why is this Lesson Critical? (Real-World Applications)
1. **The Core of Autonomy:** Moving safely from point A to point B without human monitoring is the foundational goal of mobile robotics. Nav2 maps raw engineering goals into smooth velocity commands.
2. **Industrial Distribution Logistics:** Autonomous Mobile Robots (AMRs) inside smart fulfillment centers utilize layered costmaps to calculate paths dynamically around workers, pallets, and dynamic warehouse traffic.
3. **Safety & Asset Protection:** Unconfigured navigation parameters cause physical hardware destruction. Costmap inflation layers act as a digital safety shield that keeps multi-million dollar platforms from grinding against walls.

---

## 🛠️ Step 1: Install Production-Grade Navigation Packages
To ensure our workspace layer has full access to the complete industrial standard Nav2 stack, reference libraries, and pre-built visualization configurations, pull the binary software extensions:
```bash
cd ~/ros2_ws
sudo apt update
sudo apt install ros-humble-navigation2 ros-humble-nav2-bringup -y
```

---

## 🏗️ Step 2: Orchestrate the Autonomous Workstation Pipeline
To execute dual-loop path planning (Global Routing + Local Obstacle Avoidance) safely across your system environment layers, manage these four dedicated terminal window spaces:

### 🏠 Terminal Tab 1: Physics Simulator Ignition (Core World)
```bash
# Target Location Context Initialization
cd ~/ros2_ws
export TURTLEBOT3_MODEL=burger
source ~/.bashrc

# Launch Core Simulated Environment
ros2 launch turtlebot3_gazebo turtlebot3_world.launch.py
```
*(Wait 5 seconds until the full 3D graphics world layout stabilizes on your screen before proceeding).*

### 🗺️ Terminal Tab 2: Nav2 Architecture & Custom Map Ignition
Open a second terminal window/tab inside VS Code, source the environment paths, and ignite the navigation stack. We feed the system the precise parameter templates alongside the permanent map blueprints we generated during Lesson 05:
```bash
# Target Location Context Initialization
cd ~/ros2_ws
export TURTLEBOT3_MODEL=burger
source ~/.bashrc

# Ignite Nav2 Stack with Custom Map Blueprint
ros2 launch nav2_bringup bringup_launch.py \
    use_sim_time:=true \
    map:=\$HOME/ros2_ws/src/my_first_robot_map.yaml
```
*Look at the terminal output logs! The Nav2 initialization manager will systematically boot the Planner Server, the Controller Server, AMCL Localization, and the Behavior Tree Navigator into a live operational loop!*

### 🎨 Terminal Tab 3: RViz2 Visualization & Localization Calibration
Open a third terminal window/tab inside VS Code to display the robot's sensory mind, costmaps, and path vectors visually:
```bash
# Target Location Context Initialization
cd ~/ros2_ws
export TURTLEBOT3_MODEL=burger
source ~/.bashrc

# Launch Pre-configured Nav2 RViz Viewer Profile
ros2 launch nav2_bringup rviz_launch.py
```

---

## 🎮 Step 3: Calibrate Localization & Drive Pathfinding Goals (Interactive Moves)

Once your screens are populated with Gazebo and RViz2, complete these absolute execution protocols in sequence to achieve successful cross-auditing verification:

### 1. Execute 2D Pose Estimation Alignment
Look closely at your RViz2 screen. The mapped walls are loaded, but the robot might be misplaced, surrounded by a green cloud of particle arrays.
- Click the **2D Pose Estimate** button located on the top toolbar panel inside RViz2.
- Click on the map grid at the exact coordinate matching the robot's physical position inside Gazebo, and **drag the green vector arrow** to point in the robot's true heading direction.
- The Adaptive Monte Carlo Localization (AMCL) engine will snap into position, and your laser array lines will align tightly with your blueprint walls!

### 2. Drive Your First Autonomous Pathfinding Array
Now, let the mathematical path planning planners compute real-world steering inputs completely unsupervised:
- Click the **Nav2 Goal** button on the top toolbar panel inside RViz2.
- Click anywhere on the open white spaces of your map grid and drag an arrow to set the desired destination orientation.
- **Watch the Matrix Work:** 
  1. A pink/global path line will generate instantly from the **Planner Server**, routing around static obstacles.
  2. The **Local Costmap** will display a rolling inflation field around the chassis.
  3. The **Controller Server** will compute continuous velocity calculations and send them over the `/cmd_vel` channel.
  4. The robot will autonomously navigate, slow down gracefully as it hits its target zone, and stop precisely at the target pose!

---

## 🔬 Step 4: Cross-Audit Navigation Topic Arrays (Terminal Tab 4)
While the robot is driving autonomously, execute real-time telemetry inspection inside a fourth terminal tab to understand where the ROS2 magic happens:

### 1. Audit the Underlying Steering Command Stream
```bash
source ~/.bashrc
ros2 topic echo /cmd_vel --once
```
*You will cleanly verify the linear and angular velocity matrices outputs generated by the local controller tracking loops.*

### 2. Inspect Active Navigation Costmap Frames
```bash
ros2 topic list | grep costmap
```
*You will verify `/global_costmap/costmap` and `/local_costmap/costmap` are actively broadcasting grid arrays. This proves that the multi-layered spatial cost infrastructure is successfully running in the background.*
