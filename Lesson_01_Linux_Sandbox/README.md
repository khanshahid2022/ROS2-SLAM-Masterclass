# ROS2-SLAM-Masterclass
A complete ground-up, visual, graphic-intensive ROS2 and SLAM learning journey.

# Installing Linux on your Windows
Run this single command inside your Administrator PowerShell or Command Prompt (CMD) to clean install a fresh, stable Ubuntu engine on your Windows System.

```Powershell
wsl --install -d Ubuntu-22.04
```

What to expect next:
- Windows will download and install the official Ubuntu 22.04 LTS kernel package.
- A completely separate new terminal window will automatically pop open, displaying Installing, this may take a few minutes.... It will ask you to type a New Username and Password for your Linux system.
- Write down whatever username and password you want (characters won't show on screen while typing passwords for security, just type it out and hit Enter).

# 🐧 Phase 1: Linux Interactive Sandbox (Learn While Doing It)

Welcome to the active sandbox training module. Do not just read—open your Ubuntu terminal window and execute this precise sequence to unlock your muscle memory.

### Step 1: Initialize the Learning Lab
Create a clean directory structure and install visual tracking tools (`tree`).
```bash
mkdir -p linux_basic_learning
sudo apt update && sudo apt install tree -y
```

### Step 2: Navigate and Build Script Stacks
Step inside your new directory and generate native Python and C++ source code file skeletons.
```bash
cd linux_basic_learning
touch camera_driver.py
touch laser_scanner.cpp
```

### Step 3: Copy, Move & Re-arrange Components
Create a sub-folder matrix, duplicate your Python driver, and shift the C++ scanner code inside the architecture.
```bash
mkdir -p internal_backup
cp camera_driver.py internal_backup/
mv laser_scanner.cpp internal_backup/
```

### Step 4: Verification & Permanent Cleanup
Step backward in your directory hierarchy, audit your folder topology visually, and then flush the cache safely.
```bash
cd ..
tree linux_basic_learning
rm -rf linux_basic_learning
```




# Notes for Phase-1
# 🐧 Phase 1: The 80:20 Linux Essentials for Robotics

You do not need to memorize the entire Linux Operating System to master ROS2 and SLAM. Focus on these 10 core command structures that drive 80% of daily robotics development workflows.

### 1. Navigation Matrix (Moving Around)
- `pwd`: Print Working Directory (Shows exactly where you are standing in the system tree).
- `ls -la`: List Files (Displays all standard and hidden configuration folders with permissions).
- `cd <directory_name>`: Change Directory (Move inside folders). Use `cd ..` to jump one step backward.

### 2. File & Space Manipulation
- `mkdir -p <folder_path>`: Make Directory (Creates nested structural directories cleanly without crashing).
- `rm -rf <file_or_folder>`: Remove Forcefully (Wipes targeted files or cached build paths permanently. *Use with extreme care!*).
- `cp -r <source> <destination>`: Copy Recursive (Duplicates directories completely across system structures).
- `mv <source> <destination>`: Move/Rename (Shifts files instantly or updates their semantic names).

### 3. Execution & Authorization Privileges
- `sudo <command>`: SuperUser Do (Executes targeted operations with administrative root access privileges).
- `chmod +x <filename>.py`: Change Mode Executable (Grants Linux security clearance to run a script file directly).
- `history | grep <keyword>`: Audit search (Scans previous terminal runs to extract forgotten syntax commands).

# Short Notes
[80:20 INTERACTIVE LINUX CHEAT SHEET]
--------------------------------------------------------------------------------
1. Setup Sandbox:    mkdir -p linux_basic_learning
2. Visual Inspect:   tree linux_basic_learning (Requires: sudo apt install tree)
3. Step Inside:      cd linux_basic_learning
4. Create Files:     touch file_name.py / file_name.cpp
5. Copy/Paste Tool:  cp source_path destination_path
6. Move/Shift Tool:  mv source_path destination_path
7. Return Path:      cd ..
8. Nuke/Delete:      rm -rf folder_name
--------------------------------------------------------------------------------


