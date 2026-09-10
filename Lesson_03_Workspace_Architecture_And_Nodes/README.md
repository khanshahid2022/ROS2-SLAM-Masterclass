# 🏗️ Lesson 03: Workspace Topology & Multi-Language Node Architecture

Welcome to Module 3. In this segment, we transition from global binary packages into creating our own custom robotics software infrastructure. You will master the ROS2 Workspace layout rules, build standalone Python and C++ processing engines (Nodes), and unlock dynamic parameter runtime injection.

---

## 📐 Step 1: The Core Workspace & Package Design

ROS2 does not allow you to write random code anywhere. Your logic must live inside a structured directory hierarchy compiled by the `colcon` engine.

### 1. Initialize the Directories
Open your Ubuntu terminal and deploy the foundational robotics folder matrix:
```bash
mkdir -p ~/ros2_ws/src
cd ~/ros2_ws/src
```

### 2. Generate a Python Production Package
Create an automated Python package structure using the standard configuration patterns:
```bash
ros2 pkg create --build-type ament_python --node-name core_telemetry_node project_vision_pkg
```

---

## 📝 Step 2: Develop a Production-Grade Python Publisher Node

We will write a clean, high-performance background script that continuously streams tracking health status and precision counts down the local communication grid interface.

1. Open VS Code directly inside your custom workspace:
   ```bash
   code ~/ros2_ws
   ```
2. Navigate to `src/project_vision_pkg/project_vision_pkg/core_telemetry_node.py`, wipe any default dummy lines, and type out this precise production logic:

```python
import rclpy
from rclpy.node import Node
from std_msgs.msg import String

class TelemetryPublisher(Node):
    def __init__(self):
        # Initialize the internal node identity registry name
        super().__init__('telemetry_engine_node')
        
        # 80:20 Rule: Declare runtime dynamic string parameters
        self.declare_parameter('operation_mode', 'SLAM_OPTIMAL')
        
        # Create a communication pipeline channel over topic '/robot_logs'
        self.my_publisher = self.create_publisher(String, '/robot_logs', 10)
        
        # Deploy a 1.0-second loop timing engine callback
        self.timer = self.create_timer(1.0, self.timer_callback)
        self.cycle_counter = 1

    def timer_callback(self):
        msg = String()
        # Query the active parameter variable state instantly without re-compiling
        current_mode = self.get_parameter('operation_mode').get_parameter_value().string_value
        
        msg.data = f"Mode: [{current_mode}] | Processing Cycle Count: {self.cycle_counter}"
        
        self.my_publisher.publish(msg)
        self.get_logger().info(f"Pushed to Grid: {msg.data}")
        self.cycle_counter += 1

def main(args=None):
    rclpy.init(args=args)
    node = TelemetryPublisher()
    try:
        rclpy.spin(node)
    except KeyboardInterrupt:
        pass
    node.destroy_node()
    rclpy.shutdown()

if __name__ == '__main__':
    main()
```

---

## 🛰️ Step 3: Verify the Package Router Configuration

Open `src/project_vision_pkg/setup.py` and inspect how the console script mappings connect the global command-line calls directly to your custom execution loop block modules:

```python
    entry_points={
        'console_scripts': [
            'core_telemetry_node = project_vision_pkg.core_telemetry_node:main'
        ],
    },
```

---

## 🏗️ Step 4: Topological Workspace Compilation & Execution

To compile custom source files into active environment binary components safely, always trigger the workspace compiler directly from the underlying workspace root directory path layer:

```bash
# 1. Step back to workspace root path anchors
cd ~/ros2_ws

# 2. Build targeted client packages directly
colcon build --packages-select project_vision_pkg

# 3. Source the localized overlay directory mappings
source install/setup.bash

# 4. Ignite your custom background tracking node engine (Terminal Tab 1 will become busy)
ros2 run project_vision_pkg core_telemetry_node
```

---

## 🏁 Step 5: Advanced Zero-GUI Telemetry Tuning Check (Multi-Terminal Sync)

To observe and manipulate our data stream natively without shutting down the core robot brain, we will orchestrate the workspace across multiple dedicated terminal windows:

### Window 1 (Active Engine - Terminal Tab 1)
Leave your `core_telemetry_node` running here. It will continuously display increasing processing cycle count logs.

### Window 2 (Live Network Echo - Terminal Tab 2)
Open a brand-new second terminal window/tab inside VS Code, source your environment overlay path, and listen to raw network data lines:
```bash
source ~/ros2_ws/install/setup.bash
ros2 topic echo /robot_logs
```
*(You will see the continuous string arrays output streaming directly in real time).*

### Window 3 (Dynamic Parameter Injection - Terminal Tab 3)
Open a third terminal window/tab inside VS Code to act as your operational control deck. Source the paths, and trigger runtime variable changes instantly on the fly without stopping your background processes:
```bash
source ~/ros2_ws/install/setup.bash

# 1. Inspect live active parameters linked to your worker node
ros2 param list

# 2. Tune tracking configurations dynamically without code recompilation
ros2 param set /telemetry_engine_node operation_mode "WARNING_VISION_DRIFT"
```

*Look closely back at **Terminal Tab 1** and **Terminal Tab 2** the exact split-second you run this parameter command! Notice how the tracking string modes update on the fly instantly without terminating or interrupting your main script execution grid runtime matrix!*
