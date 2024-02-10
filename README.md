# Mobile-Robot-with-2-Axis-Arm
## Overview
This project simulates a mobile robot with a 2-axis robotic arm in Gazebo, a powerful 3D robotics simulator. The project aims to demonstrate the capabilities and functionalities of the robot in a virtual environment. The robot can move along the x-axis until it reaches the room walls, and control the arm joints using ROS2 topics. The project also uses a camera plugin to replicate the physical camera sensor in Gazebo.

## Project Justification
The project is necessary to learn and practice the basics of robotics simulation using Gazebo and ROS2. The project can help the user understand how to create and spawn a robot model, how to use different plugins to control and monitor the robot, and how to visualize the robot’s state and pose using tf2 tools. The project can also serve as a foundation for further development and experimentation with more complex robot models and tasks.

## Objectives
The project has the following objectives:

  - To create a simple mobile robot model with a 2-axis arm using URDF and SDF formats.
  - To spawn the robot in a virtual room created in Gazebo.
  - To use the gazebo_ros_diff_drive plugin to control the movement of the robot along the x-axis.
  - To use the gazebo_ros_joint_state_publisher plugin to publish the arm position data to the /joint_states topic.
  - To use the gazebo_ros_joint_pose_trajectory plugin to make the robot arm move to a particular position.
  - To use the gazebo_ros_camera plugin to replicate the physical camera sensor in Gazebo.
  - To visualize the TF tree of the robot using tf2 tools.
# Phases of Work
The project can be divided into the following phases:

  - Phase 1: Robot Model Creation. In this phase, the user will create the robot model using URDF and define the links, joints, and plugins for the robot.
  - Phase 2: Robot Spawning and Control. In this phase, the user will spawn the robot in the virtual room using a launch file, and control the robot movement and arm position using ROS2 topics.
  - Phase 3: Robot Visualization and Monitoring. In this phase, the user will use the camera plugin to view the robot’s surroundings, and use the tf2 tools to view the robot’s TF tree.



https://github.com/Abhi-0212000/Mobile-Robot-with-2-Axis-Arm/assets/70425157/f005b779-46cd-4126-8e69-1d8fed519d6c



# Software Requirements
  - Ubuntu 22.04
  - ROS2 Humble
  - Python 3.10
  - Gazebo classic (11.10.2)
  - tf2 tools

# Installation
To install Gazebo classic, run the following commands on the Linux terminal:

```bash
sudo apt install gazebo
sudo apt install ros-humble-gazebo-ros-pkgs
sudo apt install ros-humble-gazebo*
```

To install tf2 tools, run the following command on the Linux terminal:

```bash
sudo apt install ros-humble-tf2-tools
```

# Environment Setup
Create a ROS2 workspace:
```bash
mkdir ros2_ws
cd ros2_ws
mkdir src
colcon build
```
If colcon is not installed, run:
```bash
sudo apt update
sudo apt install python3-colcon-common-extensions
```
Add the ROS2 workspace to your ~/.bashrc:
```bash
echo "source ~/ros2_ws/install/setup.bash" >> ~/.bashrc
source ~/.bashrc
```
# Organize Your Folders
Place the following folders inside the src folder:
  - my_robot_bringup
  - my_robot_description
# Build Your Workspace
```bash
cd ros2_ws
colcon build –symlink-install
source ~/.bashrc
```
# Usage
To launch/spawn the robot in the Gazebo environment, run the following command in a new terminal:

```bash
ros2 launch my_robot_bringup my_robot_gazebo.launch.xml
```

To make the robot move along the x-axis with a speed of 0.5 m/s, run the following command in another terminal:

```bash
ros2 topic pub /cmd_vel geometry_msgs/msg/Twist "{linear:{x: 0.5}}"
```

To visualize the TF tree of the robot, run the following command in another terminal:
```bash
ros2 run tf2_tools view_frames -o my_robot_frame
```
A TF tree PDF file will be created with the name my_robot_frame.pdf in the same working directory from which you have executed the above command.

To make the robot arm move to a particular position, run the following command in another terminal. Note: we are making the arm move to {0.3, 0.0} and because of gravity in Gazebo, the arm will eventually come to {0.0, 0.0}. We are not trying to lock the robot arm at a particular position.
```bash
ros2 topic pub -1 /set_joint_trajectory trajectory_msgs/msg/JointTrajectory '{header: {frame_id: arm_base_link}, joint_names: [arm_base_forearm_joint, forearm_hand_joint], points: [ {positions: {0.3, 0.0}} ]}'
```
# rqt_graph
![image](https://github.com/Abhi-0212000/Mobile-Robot-with-2-Axis-Arm/assets/70425157/3b28b51b-b34a-471a-9377-b507675f8798)

# TF view
![image](https://github.com/Abhi-0212000/Mobile-Robot-with-2-Axis-Arm/assets/70425157/64d3576a-d3e9-45c0-941b-eab7aaf93728)
