# Readme
Instructions for preparing a workspace to run the experiments in our ICRA 2023 submission: _AeriaLPiPS: A Local Planner for Aerial Vehicles with Geometric Collision
Checking_.

After you have finished preparing the workspace, you can run the experiments by following [these instructions](https://github.com/ivaros/aerial_pips).

## System Requirements and Dependencies
- [Ubuntu 20.04](http://releases.ubuntu.com/20.04/)
- [ROS Noetic](http://wiki.ros.org/noetic/): Full desktop install

Note: You can install the python3 dependencies using either `apt-get install python3-<package name>` or `pip3` (you can use a `venv` if you wish, just remember to activate it).

## Setting up

1. Install [wstool](http://wiki.ros.org/wstool) and other build-related dependencies.
```
sudo apt-get install build-essential python3-rosdep python3-wstool python3-rosinstall-generator python3-rosinstall python3-catkin-tools
```

2. Create a new catkin workspace. For example:
```
mkdir ~/catkin_ws
cd ~/catkin_ws
catkin init
```

3. Download required packages using`wstool`:
```
wstool init src https://raw.githubusercontent.com/ivalab/NavBench/master/ICRA2023/rosinstall 
```

4. Satisfy package dependencies:
- The following is a non-exhaustive list of python packages you will need: `numpy`, `matplotlib`, `scipy`, `skimage`
- As a debugging aid, everything is known to work in an environment containing the packages listed in the included [`requirements.txt`](https://raw.githubusercontent.com/ivalab/NavBench/master/ICRA2023/requirements.txt) file. However, you should not need every package in the list nor necessarily the same exact versions.
- Running the command `rosdep check --from-paths src -i -y` from the root of your workspace may help identify missing dependencies. I don't recommend using the related `install` command:
  - It only detects `apt` installed packages, so don't use if you prefer using `pip3`
  - The packages `ros-noetic-mavros` and `ros-noetic-mavros-msgs` are not actually required for our purposes

5. Compile the workspace
```
catkin build
```
_Install missing dependencies as needed_


| Note: If you encounter any problems (unlisted dependencies, compile errors, etc), please create an issue. |
| --- |
