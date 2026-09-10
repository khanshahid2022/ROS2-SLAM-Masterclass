# 🚀 Lesson 02: ROS2 Humble & VS Code Graphical Core Ignition

Welcome to the foundation installation module. In this lesson, we will deploy the official ROS2 Humble Hawksbill core software stack, configure high-performance development environments using Visual Studio Code, and verify the background transport engines.

---

## 🛠️ Step 1: Visual Studio Code & Remote WSL Setup

To get complete graphical rendering and visual file tracking directly from Windows into our fresh Linux system layout:

1. **Download VS Code:** If not already installed, download the official installer on your Windows system from [Visual Studio Code Windows](https://visualstudio.com). 
2. **Crucial Installation Tick:** During Windows installation, ensure you check the box that says **"Add to PATH"**.
3. **Open Terminal:** Open your fresh Ubuntu 22.04 terminal screen window and type:
   ```bash
   code .
   ```
   *Windows will automatically inject the downstream VS Code Server architecture inside your Linux environment kernel.*
4. **Install the Extension:** Inside the VS Code window that pops open, press `Ctrl + Shift + X` (Extensions tab), search for **"WSL"** (by Microsoft), and click **Install**.

---

## 🛰️ Step 2: UTF-8 Language Locale Verification

ROS2 communication networks require strict UTF-8 environment parameters authorization. Run this code block sequentially to enforce system configurations:

```bash
sudo apt update && sudo apt install locales -y
sudo locale-gen en_US en_US.UTF-8
sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
export LANG=en_US.UTF-8
```

---

## 📦 Step 3: Official ROS2 Apt Repositories Integration

Authorize your system manager to securely fetch binary Debian data streams from open-source robotics networks:

```bash
# 1. Enable the Ubuntu Universe repository profile matrix
sudo apt install software-properties-common -y
sudo add-apt-repository universe

# 2. Download and authorize the genuine ROS2 GPG network security keys
sudo apt update && sudo apt install curl -y
sudo curl -sSL https://githubusercontent.com -o /usr/share/keyrings/ros-archive-keyring.gpg

# 3. Add the structural mirror repository down your apt sources list layout
echo "deb [arch=\$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://ros.org \((source /etc/os-release && echo\)UBUNTU_CODENAME) main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null
```

---

## 🏗️ Step 4: Full Desktop Graphic Stack Installation

Refresh cache parameters, execute software engine updates, and download the full desktop layout bundle (Includes Core Libraries, Rviz, and dynamic Gazebo interface engines):

```bash
sudo apt update
sudo apt upgrade -y
sudo apt install ros-humble-desktop ros-dev-tools -y
```
*(Warning: This extraction contains heavy graphics data processing layers, it will allocate around 2.5GB to 4GB space and may take 5 to 10 minutes depending on your internet bandwidth network).*

---

## 🔄 Step 5: Automation Environment Sourcing Configuration

To completely avoid typing `source /opt/ros/humble/setup.bash` every single time a fresh workstation terminal window launches:

```bash
echo "source /opt/ros/humble/setup.bash" >> ~/.bashrc
source ~/.bashrc
```

---

## 🏁 Step 6: The Ultimate Sanity Pipeline Verification (Demo)

To instantly prove your ROS2 engine is working perfectly without compilation bugs:

1. **Launch a Publisher Node (Talker):**
   ```bash
   ros2 run demo_nodes_cpp talker
   ```
2. **Open a New Terminal Tab and Launch a Subscriber Node (Listener):**
   ```bash
   ros2 run demo_nodes_py listener
   ```
*If lines of text successfully publish and intercept across screens, your environment layer is officially 100% stable!*
