# ICRA 2020
Recreating navigation performance results in _egoTEB: Ego-centric, Perception Space Navigation Using Timed-Elastic-Bands_. 
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

3. Initialize `wstool` workspace
```
wstool init src
```

3. Add necessary packages to your catkin workspace:
```
wstool merge -t src https://github.com/ivalab/NavBench/blob/master/ICRA2020/rosinstall
wstool update -t src -j8
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

## Running Benchmarks

### Demo 
To run a single navigation experiment of _TEB_ navigating in a room populated with random obstacles, run the following command:
```bash
rosrun nav_scripts gazebo_master_demo.py
```
By default, the simulation gui is hidden. To display it, set the argument `gui` in   ```navigation_test/configs/launch/gazebo_turtlebot_empty_room_20x20_world.launch``` to `true`. 

### Run Comprehensive Benchmark
A benchmark comparing navigation performance of _DWA_, _TEB_, and _egoTEB_ can be run as follows:

1. Create directory `~/simulation_data` for logging test outcomes.

2. (Optional) Set the number of concurrent experiments to run using the `num_instances` variable at the beginning of the `main` function at the bottom of the `navigation_test/scripts/scripts/gazebo_master.py` file. For most systems, this should be left at 1. For reference, a 24 hardware thread Intel Xeon E5-2640x2 @ 2.50GHz (Single Core Passmark 1468, Multi-Threaded score of 9512) can generally run up to 3 concurrent experiments without issue. Overloading your system can negatively impact the experiments.

3. ```rosrun nav_scripts gazebo_master.py``` and wait for complete.

4. Replace `~/simulation_data/results_...` in ```navigation_test/scripts/scripts/analyze_results.py``` with the full path of your results file. ```rosrun nav_scripts analyze_results.py``` to generate a markdown table of results.

