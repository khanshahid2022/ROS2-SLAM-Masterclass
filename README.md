# ROS2-SLAM-Masterclass
A complete ground-up, visual, graphic-intensive ROS2 and SLAM learning journey.
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
