# ICRA 2020
Recreating navigation performance results in _egoTEB: Ego-centric, Perception Space Navigation Using Timed-Elastic-Bands_. 
## Requirement and Dependencies
- [Ubuntu 16.04](http://releases.ubuntu.com/16.04/)
- [ROS Kinetic](http://wiki.ros.org/kinetic/)
- [catkin workspace](http://wiki.ros.org/catkin/Tutorials/create_a_workspace)
- [navigation_test (missing link + branch + commit)](link), checkout to commit `6fecd60df2ebf12a52a8531e0aaa413eb2e6175c`
- [gazebo_fake_localization](https://github.com/TurtlebotAdventures/gazebo_fake_localization)

Clone `navigation_test` and `gazebo_fake_localization` into your catkin workspace, build the packages and source the workspace.

## Running Benchmarks
| Note: This is still WiP, please check back frequently for more features. |
| --- |

### Demo 
To run a single navigation experiment of _TEB_ navigating in a room populated with random obstacles, run the following command:
```bash
rosrun nav_scripts gazebo_master_demo.py
```
To visualize the process, edit ```navigation_test/configs/launch/gazebo_turtlebot_empty_room_20x20_world.launch``` that argument `gui` is true. 

### Run Comprehensive Benchmark
A benchmark of _DWA_ and _TEB_ is currently available, (_egoTEB_ is on the way):
1. Make sure argument `gui` is revert to `false`.
2. Create directory `~/simulation_data` for logging test outcomes.
3. `navigation_test` launches multiple Gazebo simulation to benchmark algorithms concurrently. On average 4 cores per individual Gazebo is needed on our Intel Xeon E5-2640 @ 2.50GHz (Single Core Passmark 1468, Multi-Threaded score of 9512). Set an appropriate number of GazeboMaster to `MultiMasterCoordinator` constructor in `navigation_test/scripts/scripts/gazebo_master.py` main function.
4. ```rosrun nav_scripts gazebo_master.py``` and wait for complete.
5. Acquire testing outcome file name, edit ```navigation_test/scripts/scripts/analyze_results.py``` to read in the correct test. ```rosrun nav_scripts analyze_results.py``` to generate a readme table style output.
