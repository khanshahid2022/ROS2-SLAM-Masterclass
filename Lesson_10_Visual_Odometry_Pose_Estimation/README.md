# 📷 Lesson 10: Visual Odometry & 3D Pose Estimation (Epipolar Geometry & Feature Matching)
Welcome to Module 10. In this lesson, we transition from single-frame feature extraction to multi-frame geometric tracking. You will discover how a robot calculates its absolute spatial displacement purely from two consecutive image frames, implement Epipolar Geometry constraints to filter optical noise, compute the Essential Matrix ($E$), and orchestrate a high-performance OpenCV Python node that calculates real-world camera trajectory vector changes ($R$ and $t$) live.

---

## 💡 Why is this Lesson Critical? (Real-World Applications)
1. **GPS-Denied Navigation Pipelines:** Drones flying indoors or planetary rovers traversing barren landscapes cannot access global position anchors. Visual Odometry (VO) continuously integrates incremental camera frame movements to map coordinate trajectories.
2. **Wheel Odometry Drift Compensation:** Mechanical wheel sensors slip over loose mud, metal shavings, or slick warehouse floors, causing position estimation systems to drift rapidly. Visual tracking frames isolate changes through static pixels to correct errors.
3. **The Foundation of Bundle Adjustment:** Before complex 3D graphs optimization solvers can execute global bundle adjustment backend loops, the front-end tracking pipeline must supply accurate relative pose estimations from image pairs.

---

## 🛠️ Step 1: Install Geometry Solvers & Matrix Math Libraries
To ensure our workstation node has the exact mathematical tooling to run matrix decomposition algorithms (SVD) and geometry computations, install these libraries:
```bash
cd ~/ros2_ws
sudo apt update
sudo apt install python3-scipy python3-numpy -y
```

---

## 🏗️ Step 2: Develop the Visual Odometry Frame Tracker Script
We will now create a custom computer vision tracking node. This script caches consecutive image frames, performs Flann-based feature descriptor matching, calculates the Essential Matrix using RANSAC outlier rejection, and extracts the physical Rotation ($R$) and Translation ($t$) matrices.

### 1. Create the Script File Layout
```bash
code ~/ros2_ws/src/masterclass_description/masterclass_description/visual_odometry.py
```

### 2. Insert the Code Base Matrix
Paste the following complete Python implementation directly inside the file:

```python
#!/usr/bin/env python3
import rclpy
from rclpy.node import Node
from sensor_msgs.msg import Image
from cv_bridge import CvBridge
import cv2
import numpy as np

class VisualOdometryNode(Node):
    def __init__(self):
        super().__init__('visual_odometry')
        self.subscription = self.create_subscription(
            Image,
            '/masterclass_camera/image_raw',
            self.image_callback,
            10)
        self.br = CvBridge()
        self.orb = cv2.ORB_create(nfeatures=1000)
        
        # Define the FLANN Matcher parameters tailored for binary descriptors (ORB)
        FLANN_INDEX_LSH = 6
        index_params = dict(algorithm=FLANN_INDEX_LSH, table_number=6, key_size=12, multi_probe_level=1)
        search_params = dict(checks=50)
        self.matcher = cv2.FlannBasedMatcher(index_params, search_params)
        
        # Hardcoded Camera Intrinsic Matrix (K) derived from Lesson 09 configuration
        self.K = np.array([[476.701,   0.0,   320.0],
                           [  0.0,   476.701, 240.0],
                           [  0.0,     0.0,     1.0]], dtype=np.float32)
        
        self.prev_gray = None
        self.prev_kp = None
        self.prev_des = None
        self.get_logger().info('Visual Odometry 3D Pose Estimator initialized. Computing Epipolar matrices...')

    def image_callback(self, data):
        current_frame = self.br.imgmsg_to_cv2(data, desired_encoding='bgr8')
        gray_frame = cv2.cvtColor(current_frame, cv2.COLOR_BGR2GRAY)
        
        # Extract features for the current visual frame array
        kp, des = self.orb.detectAndCompute(gray_frame, None)
        
        if self.prev_gray is None:
            # Seed the cache matrices on the first frame ignition
            self.prev_gray = gray_frame
            self.prev_kp = kp
            self.prev_des = des
            return

        # Check if enough valid feature arrays exist across the tracking window
        if des is not None and self.prev_des is not None and len(kp) > 20 and len(self.prev_kp) > 20:
            try:
                # Execute K-Nearest Neighbors matching loop
                matches = self.matcher.knnMatch(des, self.prev_des, k=2)
                
                # Apply Lowe's Ratio Test to reject ambiguous feature noise
                good_matches = []
                for m_n in matches:
                    if len(m_n) == 2:
                        m, n = m_n
                        if m.distance < 0.7 * n.distance:
                            good_matches.append(m)

                if len(good_matches) > 15:
                    # Construct coordinate vector matrices for matched target pairs
                    pts_curr = np.float32([kp[m.queryIdx].pt for m in good_matches])
                    pts_prev = np.float32([self.prev_kp[m.trainIdx].pt for m in good_matches])
                    
                    # Compute the Essential Matrix (E) utilizing RANSAC outlier filtering bounds
                    E, mask = cv2.findEssentialMat(pts_curr, pts_prev, self.K, method=cv2.RANSAC, prob=0.999, threshold=1.0)
                    
                    if E is not None and E.shape == (3, 3):
                        # Decompose the Essential Matrix into relative physical rotation (R) and translation (t)
                        _, R, t, _ = cv2.recoverPose(E, pts_curr, pts_prev, self.K, mask=mask)
                        
                        # Extract the yaw angle parameter from the rotation translation array
                        yaw = np.arctan2(R[1, 0], R[0, 0]) * 180.0 / np.pi
                        self.get_logger().info(f"VO Motion Captured -> Yaw Delta: {yaw:6.2f}° | dx: {t[0][0]:6.3f} | dz: {t[2][0]:6.3f}")
                
                # Render visual verification track lines display matrix window panel
                match_img = cv2.drawMatches(current_frame, kp, self.prev_gray, self.prev_kp, good_matches[:20], None, flags=2)
                cv2.imshow("Epipolar Geometric Feature Tracking Matrix", match_img)
                cv2.waitKey(30)
                
            except Exception as e:
                pass

        # Shift frame matrix states inside the tracking history buffers
        self.prev_gray = gray_frame
        self.prev_kp = kp
        self.prev_des = des

def main(args=None):
    rclpy.init(args=args)
    node = VisualOdometryNode()
    try:
        rclpy.spin(node)
    except KeyboardInterrupt:
        pass
    cv2.destroyAllWindows()
    node.destroy_node()
    rclpy.shutdown()

if __name__ == '__main__':
    main()
```
*Make the geometry node executable across your workspace directories handles:*
```bash
chmod +x ~/ros2_ws/src/masterclass_description/masterclass_description/visual_odometry.py
```

---

## 🏗️ Step 3: Orchestrate the Visual Odometry Workstation Pipeline
To evaluate mathematical pose calculation metrics safely across your layers, manage these four distinct terminal window spaces:

### 🏠 Terminal Tab 1: Physics Simulator Core Ignition
```bash
# Target Location Context Initialization
cd ~/ros2_ws
source ~/.bashrc

# Deploy simulation world space configuration environment
ros2 launch gazebo_ros gazebo.launch.py
```
*(As established in Lesson 09, make sure to use the toolbar drop menus to place 2–3 structured high-contrast obstacles like cubes or cylinders close to the origin center map grid).*

### 📦 Terminal Tab 2: Broadcast Description & Spawn Chassis
```bash
# Target Location Context Initialization
cd ~/ros2_ws
source ~/.bashrc

# 1. Update active Robot Description state parameters down the network
ros2 run robot_state_publisher robot_state_publisher \
    --ros-args -p robot_description:="$(cat ~/ros2_ws/src/masterclass_description/urdf/custom_bot.urdf)" &

# 2. Wait 5 seconds to guarantee the parameter parsing sequence is locked down
sleep 5

# 3. Spawn the custom camera-enabled model onto the grid layout ground plane
ros2 run gazebo_ros spawn_entity.py -topic robot_description -entity custom_masterclass_bot
```

### 👁️ Terminal Tab 3: Launch Custom Visual Odometry Engine Node
Run our custom motion matrix tracking node to compute epipolar vectors live:
```bash
# Target Location Context Initialization
cd ~/ros2_ws
source ~/.bashrc

# Execute relative pose estimation algorithm handle
python3 ~/ros2_ws/src/masterclass_description/masterclass_description/visual_odometry.py
```
*(A dashboard tracking window titled "Epipolar Geometric Feature Tracking Matrix" will open, displaying real-time vector correlation tracks linking matching features across successive image caches).*

### 🕹️ Terminal Tab 4: Command Twist Vectors & Audit Matrix Tracking
Open a fourth terminal layout interface to pass steering velocity commands:
```bash
# Target Location Context Initialization
cd ~/ros2_ws
source ~/.bashrc

ros2 run teleop_twist_keyboard teleop_twist_keyboard
```

---

## 🏗️ Step 4: Deploying Spatial Objects & Watching the Vision Matrix Magic

Jab aap pehli baar **Terminal Tab 3** ke node execution engine script ko run karenge, tab aapko screen context par direct koi alag visual tracking tracking window popup hota hua nahi dikhega. 

Aapko lag raha hoga ki yaha to koi computer vision jaisa tracking pipeline execution engine process hi nahi ho raha hai. Lekin yahi real-world Visual SLAM algorithms ka absolute core mathematical filter mechanism hai! **The system demands features to process spatial variables.**

Ab real magic dekhne ke liye apne physics simulator workstation setup ko side-by-side scale kijiye aur ye visual moves execute kijiye:

### 1. Dynamic Environment Landscape Ingestion
1. Apne **Gazebo Simulator window** ko frame control foreground me laiye.
2. Top horizontal navigation menu control utility toolbar par jajiye aur geometric solid shapes ko select kijiye: **Cube ◼️**, **Sphere 🔮**, ya **Cylinder 🧪**.
3. In parameters object shapes ko drag karke robot ke visual camera module sensor range spectrum ke path layers me drop karna shuru kijiye (Chassis assembly ke strict alignment view blocks ke exact samne).

### 2. The Matrix Awakening Activation Loop
* **The Instant Trigger:** Jaise hi aap robot ke optical camera target fields ke safe visibility parameter regions me pehla object block mount karenge, tracking software logic live structural lines cross-match framework build kar lega.
* **Tracking Display Engine Ignition:** Ek clean window pop-up call call engine ignite hoga jiska layout label name hoga: **"Epipolar Geometric Feature Tracking Matrix"**. Niche control terminal tab me live trajectory estimation array feedback metrics transform hona start ho jayenge!
* **The Reality Check Observation:** Agar robot move karte hue kisi bilkul plain space matrix ya blank flat grey texture boundaries area ke samne aayega jaha koi structural patterns ya obstacles absent hain, to processing frames visualization system instantly freeze/stop ho jayega. Yeh tabhi reactive update cycle trace karta hai jab physical links machine ke optical center frames me active spatial objects input nodes update kar rahe hon!

---

## 🔬 Step 5: Cross-Audit Motion Matrix Telemetry Vectors (Terminal Tab 3 Log Inspection)

Look directly at the log streams printing out inside your active **Terminal Tab 3** interface as you drive the vehicle using your keyboard tracking inputs. Verify that the tracking backend is running geometric equations correctly without throwing runtime exceptions:

### 1. Verify Inter-Frame Rotation and Translation Calculations
```text
[INFO] [visual_odometry]: VO Motion Captured -> Yaw Delta:  -0.10° | dx: -0.035 | dz:  0.999
[INFO] [visual_odometry]: VO Motion Captured -> Yaw Delta:  -0.20° | dx:  0.436 | dz:  0.900
```
*You will cleanly verify the structural `Yaw Delta` output values matching your rotation adjustments along with normalized `dx` and `dz` spatial translation vector directions. This proves that the underlying Epipolar Matrix solver is extracting physical relative movements completely from raw image data arrays.*

