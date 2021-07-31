# Readme
Recreating navigation performance results in _Potential Gap: Using Reactive Policies to Guarantee Safe Navigation_. 
## System Requirements and Dependencies
- [Ubuntu 16.04](http://releases.ubuntu.com/16.04/)
- [ROS Kinetic](http://wiki.ros.org/kinetic/)
- [catkin workspace](http://wiki.ros.org/catkin/Tutorials/create_a_workspace)

| Note: If you encounter any problems, please create an issue. |
| --- |


## Setting up Workspace

1. Install [wstool](http://wiki.ros.org/wstool) and other system dependencies
```
sudo apt-get install python-rosdep  python-wstool  build-essential python-rosinstall-generator python-rosinstall
```

2. Navigate to the root of your catkin workspace

3. Initialize `wstool` workspace and download all packages
```
wstool init src https://raw.githubusercontent.com/ivalab/NavBench/master/Arxiv2021/rosinstall 
```

4. Install any missing system dependencies:
```
rosdep install --from-paths src -i -y
```

5. Compile and source the workspace
```
catkin build
source devel/setup.sh
```

6. (Optional but recommended) Periodically check for updates to this demo:
```
wstool merge -t src https://raw.githubusercontent.com/ivalab/NavBench/master/Arxiv2021/rosinstall
wstool update -t src
```

## Running Benchmarks

### Run Navigation Benchmark
A benchmark comparing navigation performance of _DWA_, _TEB_, and _egoTEB_ can be run as follows:

1. Create directory `~/simulation_data` for logging test outcomes.

2. (Optional) Set the number of concurrent experiments to run using the `num_instances` variable at the beginning of the `main` function at the bottom of the `navigation_test/scripts/scripts/gazebo_master.py` and or `stdr_master.py` file. For most systems, this should be left at 1. For reference, a 16 hardware thread AMD 3800X can generally run up to 3 concurrent Gazebo experiments, 25 concurrent STDR experiment without issue. Overloading your system can negatively impact the experiments.

3. ```rosrun nav_scripts gazebo_master.py``` and wait for it to complete. _If something goes wrong and the process does not exit cleanly, try `rosrun nav_scripts killall.sh`_

4. Replace `~/simulation_data/results_...` in ```navigation_test/scripts/scripts/analyze_results.py``` with the full path of your results file. ```rosrun nav_scripts analyze_results.py``` to generate a markdown table of results.
