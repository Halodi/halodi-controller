# Eve Controller Workspace Setup with Gazebo simulation

Instructions maintained by: will@halodi.com

![eve_gazebo](./images/eve_gazebo_sim_ss.png)


## Documentation

- [API Documentation](https://github.com/Halodi/halodi-messages)


## Simulation Construction Set Quick start

[Simulation Construction Set](https://github.com/ihmcrobotics/simulation-construction-set)  is a simulation developed by IHMC with physics tuned to balance control development. Manipulation support is lacking. We use this simulator internally.

To use, download the latest release for your platform [here](https://github.com/Halodi/halodi-controller/releases), unpack and run "halodi-controller" or "halodi-controller.exe". The archive is self-contained and should run on any recent Windows and Linux system.

After starting, there are four options to choose from:

- SCSEveSimulation: Simulation of the whole robot
- SCSEveUpperBodySimulation: Simulation of just the upper body
- EveVisualizer: Allows connection to the robot and inspect the controller variables online.
- SCSVisualizer: Allows connection to the robot and inspect the controller variables online. This application is also able to connect to the controller plugin.

To communicate with the robot, use the API found at [halodi-messages](https://github.com/Halodi/halodi-messages). This simulator has built-in ROS2 support.

## ROS2/Gazebo Quick start installation

Prerequisites:
* Ubuntu 18.04
* A machine with graphics acceleration capability
* Internet connectivity (to download the JDK dependencies)
* (Optional) An ssh-key for your Github account on your machine. If you haven't set one up, see [these instructions](https://help.github.com/en/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)

The following steps describe the process for setting up your ROS 2 workspace to
develop with the EVE Gazebo simulation.

1. Install [ROS 2 - Eloquent](https://index.ros.org/doc/ros2/Installation/Eloquent/)
2. Install the following:
  ```bash
  sudo apt update
  sudo apt install git python3-colcon-common-extensions python3-vcstool swig3.0 xsltproc gazebo9 ros-eloquent-gazebo-ros-pkgs 
  ```
3. Create ROS 2 a workspace:
  ```bash
  mkdir -p ~/eve_ws/src
  cd ~/eve_ws/src
  ```
4. In your workspace src directory, import the libraries
  ```bash
  wget https://raw.githubusercontent.com/Halodi/halodi-controller/master/eve_ws_https.repos .
  vcs import < ./eve_ws_https.repos
  ```
  OR (If you use ssh-keys with your GitHub account)
  ```bash
  wget https://raw.githubusercontent.com/Halodi/halodi-controller/master/eve_ws.repos .
  vcs import < ./eve_ws.repos
  ```
5. Download the the lastest ROS2 Workspace Eve controller [here](https://github.com/Halodi/halodi-controller/releases) to your Downloads folder. Choose the latest Linux version.
6. Extract it to your workspace:
  ```bash
  cd ~/eve_ws/src
  tar -xzf ~/Downloads/halodi-controller-linux64-0.1.0.tar.gz
  ````
7. Build and source the workspace:
  ```bash
  cd ~/eve_ws
  colcon build
  . install/setup.bash
  ```
8. Launch the EVE Gazebo sim:
```bash
ros2 launch halodi-controller-gazebo halodi-controller-gazebo.launch.py
```

## Required ROS2 packages

To run the simulation, you need the following packages in your ROS2 workspace.

- [halodi-controller-simulation-api](https://github.com/Halodi/halodi-controller-simulation-api) Branch: develop
- [halodi-messages](https://github.com/Halodi/halodi-messages) Branch: master
- [halodi-robot-modles](https://github.com/Halodi/halodi-robot-models)  Branch: master
- [IHMC Pub Sub Group](https://github.com/ihmcrobotics/ihmc-pub-sub-group) Branch: feature/FB-288-ihmc-pub-sub-is-updated-to-latest-fast-rtps-release

