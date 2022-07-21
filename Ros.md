# Ros Notes
This follow the course: https://www.udemy.com/course/ros-essentials/learn/lecture/22078052#overview

## Ros
```
Sense <-> Think<-> Act

Ros Architecture
- Nodes & Ros Master Node 

Running Ros
1. Start the roscore `roscore`
2. Run the ros nodes `rosrun turtlesim turtle`

rosnode list 
rostopic list
rostopic echo /turtle1/cmd_vel


Ros Communication Paradigms
1. Topics / Services/ ActionLib

Ros Path Planning & Navigation 
- Global Path Planner (dijkstra algorithm)
- Local Path Planner 
* Uses the TF module

```
## ROS Workspace & ROS PACKAGE
```
1. You must always run setup.bash in a workspace for your ros command to work
2. Create your own workspace : http://wiki.ros.org/catkin/Tutorials/create_a_workspace
3. Create your ros packages

roscd
roscore

```

## ROS Computation Graph
```
Deep dive into Ros Communication Paradigms
1. Topics / Services/ ActionLib
2. Ros messages 
3. A 2d turtle sim and how to control it with ur key <-> how to control it 
```

## ROS TOPICS
## ROS MESSAGES 
## ROS SERVICE
## ROS Motions
## ROS Tools & Utilies 
## Turtlebot3 Simulation
```
https://emanual.robotis.com/docs/en/platform/turtlebot3/quick-start/. #follow the video here.
https://emanual.robotis.com/docs/en/platform/turtlebot3/simulation/#gazebo-simulation
https://classic.gazebosim.org/tutorials?tut=ros2_installing&cat=connect_ros  
# /usr/share/gazebo/setup.sh

export TURTLEBOT3_MODEL=burger
ros2 launch turtlebot3_cartographer cartographer.launch.py use_sim_time:True
```

### Downloading Turtlebot3 with rox-noetic on Ubuntu20.04.2.iso
```

```
