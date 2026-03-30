# NAO Shooting Game

This project is a ROS package that uses NAO robot capabilities to play a target-shooting game.
The robot scans its field of view, aligns itself with detected targets, and then shoots using a bow.

Because NAO has limited strength and mobility, one human-assisted step is required while preparing each shot.

## Demo Video

[![Watch the demo](https://img.youtube.com/vi/DQU9Ewwm3sM/hqdefault.jpg)](https://youtu.be/DQU9Ewwm3sM)

Direct link: https://youtu.be/DQU9Ewwm3sM

## Human Interaction Instructions

1. Insert an arrow into the front of the bow.
2. Help NAO pull the string using the attached 3D-printed tool and cloth piece on its left arm.
3. Pull the string back fully to store energy.
4. Touch NAO's head when ready.
5. NAO will move its left arm to release the tool and fire the arrow.

## Code Execution Instructions

1. Build the workspace:

```bash
catkin build
```

2. Source ROS and this project workspace.
3. Start NAO core nodes:

```bash
roslaunch nao_bringup nao_full_py.launch
```

4. Start speech, tactile, and LED modules:

```bash
roslaunch nao_apps speech.launch
roslaunch nao_apps tactile.launch
roslaunch nao_apps leds.launch
```

5. Start this project's service modules:

```bash
roslaunch PROJECT nao_service_modules.launch
```

6. Start the shooting game:

```bash
rosrun PROJECT main_engine.py
```

## Project Dependencies

The following ROS components are required:

```cmake
find_package(catkin REQUIRED COMPONENTS
  actionlib_msgs
  cv_bridge
  geometry_msgs
  image_transport
  message_generation
  naoqi_bridge_msgs
  roscpp
  rospy
  sensor_msgs
  std_msgs
  std_srvs
  tf
)
```

Additional Python dependencies:

- numpy
- cv2 (OpenCV)
- NAOqi API