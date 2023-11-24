# ioc_ur_cb2_driver

ROS 2 node for Universal Robot CB2 Controller (https://github.com/jhu-bigss/Universal_Robots_CB2_ROS2_Driver).
It was modified and updated by Pol Ramon Canyameres and by Leopold Palomo-Avellaneda, with the aim to be adapted to the Robotics Lab of the IOC at UPC.

## Install and build the package
First create a workspace:
```
mkdir -p ws_arm/src | cd ws_arm/src
``` 
It is necessary to clone the following repositories:
```
git clone https://github.com/jhu-cisst/cisst -b devel
git clone https://github.com/jhu-cisst/cisstNetlib -b devel
```
And have installed:
```
sudo apt install ros-humble-xacro
sudo apt install ros-humble-ros2-control
sudo apt install ros-humble-ros2-controllers
sudo apt install ros-humble-controller-manager
sudo apt install ros-humble-ur-description
```
Finally, at the root of your ROS 2 workspace, build using:
```
colcon build --symlink-install
``` 

## Usage instruction
Once the code is compiled, and the workspace is set using:
```
source install/setup.bash
``` 
You can launch the driver using:
```
ros2 launch ur_cb2_bringup ur_control.launch.py ur_type:=<UR_TYPE> robot_ip:=<IP_OF_THE_ROBOT>
```

- <UR_TYPE> can be 'ur5' or 'ur10'. For e-Series robots, please use official Universal Robot driver.
- You can see all the launch arguments by `--show-args`
- If you are only running the driver for a CB2 UR5, then you can use this launch file instead:
    ```
    ros2 launch ur_cb2_bringup ur5.launch.py robot_ip:=XXX.XXX.XX.XXX
    ```

Once the robot driver is running, you can move the robot using the topics:
- Position controller case:
```
ros2 topic pub --once /forward_position_controller/commands std_msgs/msg/Float64MultiArray "layout:
  dim: []
  data_offset: 0
data: [#,#,#,#,#,#]"
```
- Velocity controller case:
```
ros2 topic pub --once /forward_velocity_controller/commands std_msgs/msg/Float64MultiArray "layout:
  dim: []
  data_offset: 0
data: [#,#,#,#,#,#]"
```
