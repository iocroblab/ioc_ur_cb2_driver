# ioc_ur_cb2_driver

ROS 2 node for Universal Robot CB2 Controller (https://github.com/jhu-bigss/Universal_Robots_CB2_ROS2_Driver).
It was modified and updated by Pol Ramon Canyameres and by Leopold Palomo-Avellaneda, with the aim to be adapted to the Robotics Lab of the IOC at UPC.

## Install and build the package
First create a workspace:
```
mkdir -p ws_madar/src | cd ws_madar/src
``` 
Second it is necessary to clone/link the following repositories:
```
git clone https://github.com/jhu-bigss/Universal_Robots_ROS2_Description.git -b ros2
git clone https://github.com/jhu-cisst/cisst -b devel
git clone https://github.com/jhu-cisst/cisstNetlib -b devel
git clone https://github.com/jhu-cisst/ros2_cisst_msgs.git -b main
git clone https://github.com/jhu-cisst/cisst_ros2_bridge.git -b main
git clone https://github.com/collaborative-robotics/ros2_crtk_msgs.git -b main
git clone https://github.com/jhu-cisst/cisst_ros2_crtk.git -b main
git clone https://github.com/jhu-saw/sawConstraintController.git -b devel
```
Inside the ur_description package the urdf/ur.ros2_control.xacro file must be modified from:
```
<plugin>ur_robot_driver/URPositionHardwareInterface</plugin>
```
to:
```
<plugin>ur_cb2_robot_driver/URPositionHardwareInterface</plugin>
```
Finally, at the root of your ROS 2 workspace, build using:
```
colcon build --symlink-install
source install/setup.bash
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

Once the robot driver is running, you can launch the Moveit2 to plan the robot's motion in Rviz2:
```
ros2 launch ur_cb2_moveit_config ur_moveit.launch.py ur_type:=<UR_TYPE>
```
