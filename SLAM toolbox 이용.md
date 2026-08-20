# 1. Launch the Gazebo World

- Open a terminal and start your robot model in a simulated world
 
``` bash
export TURTLEBOT3_MODEL=waffle
ros2 launch turtlebot3_gazebo turtlebot3_world.py
```

# 2. Start SLAM Toolbox

- In a second terminal, start the SLAM mapping node and ensure you pass the simulation time argument:

``` bash
ros2 launch slam_toolbox online_async_launch.py use_sim_time:=True
```

# 3. Open RViz2 for Visualization

``` bash
ros2 run rviz2 rviz2
```
## - Set the Fixed Frame to map
## - Add a Map display topic (/map) alongside LaserScan (/scan).

# 4. Drive the Robot (Teleoperation)

- In a fourth terminal, use your keyboard to move the robot around the environment so SLAM can process the sensor data
``` bash
export TURTLEBOT3_MODEL=waffle
ros2 run turtlebot3_teleop teleop_keyboard
```

# 5. Save the Generated Map

``` bash
ros2 run nav2_map_server map_saver_cli -f ~/map
```


# 6 Nav2

``` bash
ros2 launch turtlebot3_navigation2 navigation2.launch.py use_sim_time:=true map:=./map.yaml
```

