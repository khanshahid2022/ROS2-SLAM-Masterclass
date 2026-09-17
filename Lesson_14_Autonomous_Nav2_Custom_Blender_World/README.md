# 🚀 Lesson 14: Autonomous Path Planning & Nav2 Integration in Custom Blender Worlds
Welcome to Module 14. In this industrial application milestone, we strip away manual teleoperation interfaces and grant our mobile robot absolute navigational autonomy. You will discover how to initialize the complete Nav2 stack over a custom-designed Blender workspace arena, configure global Costmap inflation grids to navigate around custom objects, execute the A* path planning engine, and stream autonomous start-to-goal waypoint transformations without human intervention.

---

## 💡 Why is this Lesson Critical? (Real-World Applications)
1. **Unsupervised Material Logistics:** In a commercial factory or lab warehouse environment, an AMR must calculate an optimal path from a docking station to a goal container completely on its own, avoiding custom structural barriers and newly added obstacles.
2. **Dynamic Costmap Adaptation:** Off-the-shelf simulator environments have flat grid rules. Importing a custom mesh requires highly precise tuning of the static and obstacle cost layers so the pathfinder can safely calculate clearances around complex geometry.
3. **Behavior Tree Execution:** Industrial autonomous fleets run on strict Nav2 Behavior Trees (BT). If a path is blocked by dynamic obstacles, the tree automatically triggers recovery behaviors (like spinning or backing up) to re-plan the trajectory.

---

## 🛠️ Step 1: Install Nav2 Navigation & Behavior Tree Plugins
To ensure your workstation layer has the full suite of costmap servers, recovery behaviors, and trajectory tracking controllers, install the binary software extensions:
```bash
cd ~/ros2_ws
sudo apt update
sudo apt install ros-humble-navigation2 ros-humble-nav2-bringup -y
```

---

## 🏗️ Step 2: Build the High-Performance Navigation Parameter Manifest
We must create a customized navigation parameters configuration file that targets our description package layout, hooks into the LiDAR `/scan` channel, and configures the `nav2_navfn_planner` to compute autonomous trajectories.

### 1. Create the Configuration Subfolder Layout
```bash
mkdir -p ~/ros2_ws/src/masterclass_description/config
code ~/ros2_ws/src/masterclass_description/config/nav2_blender_params.yaml
```

### 2. Insert the Parameters Core Matrix
Paste the following complete corporate standard parameter specifications directly inside the file:

```yaml
amcl:
  ros__parameters:
    use_sim_time: True
    alpha1: 0.2
    alpha2: 0.2
    alpha3: 0.2
    alpha4: 0.2
    base_frame_id: "base_footprint"
    global_frame_id: "map"
    odom_frame_id: "odom"
    scan_topic: "scan"

bt_navigator:
  ros__parameters:
    use_sim_time: True
    global_frame: map
    robot_base_frame: base_footprint
    odom_topic: /odom

controller_server:
  ros__parameters:
    use_sim_time: True
    controller_frequency: 20.0
    progress_checker_plugins: ["progress_checker"]
    goal_checker_plugins: ["goal_checker"]
    controller_plugins: ["FollowPath"]
    progress_checker:
      plugin: "nav2_controller::SimpleProgressChecker"
      required_movement_radius: 0.5
      movement_time_allowance: 10.0
    goal_checker:
      plugin: "nav2_controller::SimpleGoalChecker"
      xy_goal_tolerance: 0.25
      yaw_goal_tolerance: 0.25
    FollowPath:
      plugin: "nav2_dwb_controller::DWBController"

local_costmap:
  local_costmap:
    ros__parameters:
      use_sim_time: True
      global_frame: odom
      robot_base_frame: base_footprint
      rolling_window: true
      width: 4
      height: 4
      resolution: 0.05
      plugins: ["obstacle_layer", "inflation_layer"]
      inflation_layer:
        plugin: "nav2_costmap_2d::InflationLayer"
        inflation_radius: 0.45
      obstacle_layer:
        plugin: "nav2_costmap_2d::ObstacleLayer"
        observation_sources: scan
        scan:
          topic: /scan
          data_type: "LaserScan"

global_costmap:
  global_costmap:
    ros__parameters:
      use_sim_time: True
      global_frame: map
      robot_base_frame: base_footprint
      rolling_window: false
      plugins: ["static_layer", "obstacle_layer", "inflation_layer"]
      static_layer:
        plugin: "nav2_costmap_2d::StaticLayer"
        map_subscribe_transient_local: True
      inflation_layer:
        plugin: "nav2_costmap_2d::InflationLayer"
        inflation_radius: 0.60
      obstacle_layer:
        plugin: "nav2_costmap_2d::ObstacleLayer"
        observation_sources: scan
        scan:
          topic: /scan
          data_type: "LaserScan"

planner_server:
  ros__parameters:
    use_sim_time: True
    planner_plugins: ["GridBased"]
    GridBased:
      plugin: "nav2_navfn_planner::NavfnPlanner"
      tolerance: 0.5
      use_astar: true
```
*Save (Ctrl+S) and close the configuration file.*

---

## 🏗️ Step 3: Register the Config Folder in the Compilation Pipeline
We must update our build script to export this new configuration folder to the system shared location.

### 1. Open the Manifest File
```bash
code ~/ros2_ws/src/masterclass_description/CMakeLists.txt
```

### 2. Update the Target Directories Array
Modify your `install(DIRECTORY ...)` block to include the `config` token cleanly:
```cmake
# Register the raw launch, urdf, models, worlds, and config resource arrays folders
install(DIRECTORY urdf models worlds launch config
  DESTINATION share/${PROJECT_NAME}
)
```
*Save (Ctrl+S) and close the file panel.*

---

## 🏗️ Step 4: Orchestrate the Autonomous Navigation Workstation Pipeline
To run autonomous map path calculations across your layers, manage these three dedicated terminal tabs sequentially:

### 🏠 Terminal Tab 1: Ignite the Master Simulation Environment
Launch the custom world and robot publisher stack simultaneously using our master handle:
```bash
# Target Location Context Initialization
cd ~/ros2_ws
source ~/.bashrc

# Compile updates and launch the integrated simulator framework
colcon build --packages-select masterclass_description
source install/setup.bash
ros2 launch masterclass_description master_sim_launch.py
```

### 📦 Terminal Tab 2: Ignite the Full Autonomous Nav2 Navigation Stack
Open a second terminal window to boot up the path planners, costmaps, and localization servers over our custom map blueprint generated in Lesson 05:
```bash
# Target Location Context Initialization
cd ~/ros2_ws
source ~/.bashrc

# Deploy Nav2 Bringup using our custom parameter matrix configuration
ros2 launch nav2_bringup bringup_launch.py \
    use_sim_time:=true \
    autostart:=true \
    params_file:=~/ros2_ws/src/masterclass_description/config/nav2_blender_params.yaml \
    map:=~/ros2_ws/src/my_first_robot_map.yaml
```

### 🎨 Terminal Tab 3: Launch RViz2 for Autonomous Command Driving
Open a third terminal window to view our costmaps and dispatch autonomous goal targets:
```bash
# Target Location Context Initialization
cd ~/ros2_ws
source ~/.bashrc

# Run the pre-configured navigation visualizer profile
ros2 launch nav2_bringup rviz_launch.py
```

---

## 🎮 Step 5: Executing Autonomous Waypoint Pathfinding Moves (RViz2 Control)

Once the tools populate your screen, complete these absolute execution protocols to achieve full autonomous locomotion around your custom Blender objects:

1. **Set the 2D Pose Estimate:** Inside your **RViz2 panel display**, click the **2D Pose Estimate** toolbar option. Click and drag the green arrow on the map grid to match the absolute origin location where your robot chassis sits inside the Gazebo workspace view.
2. **Observe Costmap Inflation Layers:** Watch your screen! The global costmap will instantly draw thick cost zones around your custom walls and columns, confirming that the planner recognizes the custom layout boundaries.
3. **Dispatch an Autonomous Navigation Goal:** Click the **Nav2 Goal** button on the top horizontal toolbar panel inside RViz2. Click any white open coordinate space on the far end of your custom Blender map layout.
4. **Watch the Autonomous Loop Work:**
   * An **A\* Global Path line Vector** will render instantly, threading perfectly through your high-contrast shapes without clipping any corners.
   * The **Controller Server** will compute continuous motor commands, and the robot will autonomously steer its chassis through the custom arena completely unmonitored.
   * As it hits the destination coordinate target, the machine will slow down gracefully and lock its final heading pose completely on its own!

---

## 🔬 Step 6: Cross-Audit Autonomous Planner Calculations (Terminal Tab 2 Verification)
Look directly at the runtime log tracking outputs inside your active **Terminal Tab 2** window while the platform is driving autonomously to verify the calculation loops:

### 1. Verify Global Path Generation Logs
```text
[planner_server]: Created global path of size 142 success.
[controller_server]: Received a new path tracking vector array.
[controller_server]: Reached the autonomous goal destination coordinates successfully!
```
*This cleanly verifies that the autonomous navigation logic is executing without matrix deviations or recovery-tree timeouts inside your custom workspace.*
