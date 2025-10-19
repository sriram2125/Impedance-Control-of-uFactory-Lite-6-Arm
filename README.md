
# ROS 2 Impedance Control for uFactory Lite 6 with Gazebo Simulation

## Objective

[cite\_start]This project's goal is to develop a ROS 2 node-based pick-and-place application for the uFactory Lite 6 arm. [cite: 6] [cite\_start]It features model-based impedance control for compliant manipulation. [cite: 7] This setup uses the Gazebo simulator to test the control and manipulation stack without requiring physical hardware.

This documentation covers the setup of the ROS 2 workspace and the Gazebo simulation environment. The impedance controller and pick-and-place application will be added in future updates.

-----

## 1\. Setup and Installation

These instructions will guide you through setting up the complete ROS 2 workspace and Gazebo simulation environment.

### Prerequisites

  * A physical machine or a properly configured VM with 3D graphics acceleration enabled.
  * Ubuntu 22.04
  * ROS 2 Humble (Desktop version recommended).

### Step 1: Create the ROS 2 Workspace

```bash
# Create the workspace and a source folder inside it
mkdir -p ~/ufactory_ws/src
```

### Step 2: Install System Dependencies

Install all required ROS 2 packages for control, simulation, and visualization, as well as necessary development tools like Git.

```bash
# Update package lists
sudo apt update

# Install all dependencies in one command
sudo apt install -y \
  ros-humble-moveit \
  ros-humble-realsense2-camera \
  ros-humble-ros2-control \
  ros-humble-ros2-controllers \
  ros-humble-gazebo-ros-pkgs \
  git \
  git-lfs
```

### Step 3: Download Robot Source Code

I'm using the Humble, so if you are using any other version, change Humble to your respective version.

```bash
# Navigate to your workspace's source folder
cd ~/ufactory_ws/src

# Download the repository ZIP for the Humble branch
wget git clone https://github.com/xArm-Developer/xarm_ros2.git --recursive -b humble.zip

# Unzip the archive
unzip humble.zip

# Rename the folder for a cleaner path
mv xarm_ros2-humble xarm_ros2
```

### Step 4: Build the Workspace

Compile all the packages in your workspace using `colcon`.

```bash
# Navigate back to the root of your workspace
cd ~/ufactory_ws

# Build the packages
colcon build
```

-----

## 2\. Running the Simulation

To launch the Gazebo simulation, you must first source the Gazebo setup script in your terminal. This loads the necessary environment variables for ROS 2 and Gazebo to communicate.

### Step 1: Configure Environment and Launch

```bash
# Open a new terminal and run these commands

# 1. Source the Gazebo environment script
source /usr/share/gazebo/setup.sh

# 2. Source your newly built workspace
source ~/ufactory_ws/install/setup.bash

# 3. Launch the simulation
ros2 launch xarm_gazebo xarm_beside_table_gazebo.launch.py
```

### Expected Outcome

This command will launch two applications:

1.  **Gazebo**: A 3D simulator window showing the Lite 6 arm in a simple world.
2.  **RViz**: A visualization tool for interacting with the robot's ROS 2 topics and planning with MoveIt.

### Making the Setup Permanent (Recommended)

To avoid sourcing the Gazebo script in every new terminal, you can add it to your shell's startup file.

```bash
echo "source /usr/share/gazebo/setup.sh" >> ~/.bashrc
```

After running this, every new terminal you open will be automatically configured for Gazebo.


### I'm Currently trying to do the Force impedance on pyBullet i'll update the steps as I do it 




