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
### Downloading Turtlebot3 with rox-foxy on Ubuntu20.04.3 LTS
```
https://emanual.robotis.com/docs/en/platform/turtlebot3/quick-start/. #follow the video here.
https://emanual.robotis.com/docs/en/platform/turtlebot3/simulation/#gazebo-simulation
https://classic.gazebosim.org/tutorials?tut=ros2_installing&cat=connect_ros  
# /usr/share/gazebo/setup.sh

export TURTLEBOT3_MODEL=burger
ros2 launch turtlebot3_cartographer cartographer.launch.py use_sim_time:True
```

### Downloading Turtlebot3 with rox-noetic on Ubuntu20.04.2 LTS
1. Download VmwareFusion on Mac
https://www.youtube.com/watch?v=OH64IQNReCs

2. Getting Ros installed 
```
Ros Noetic Guide: http://wiki.ros.org/noetic/Installation/Ubuntu
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
sudo apt install curl # if you haven't already installed curl
curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo apt-key add -
sudo apt update
sudo apt install ros-noetic-desktop-full

GPG ERROR: https://github.com/ros2/ros2/issues/742. : If you face any GPG Erros
curl http://repo.ros2.org/repos.key | sudo apt-key add -

source /opt/ros/noetic/setup.bash
echo "source /opt/ros/noetic/setup.bash" >> ~/.bashrc
source ~/.bashrc
sudo apt install vim # Just to observe the above has been included in bash rc
vim ~/.bashrc. 

roscore #To verify ros is installed
```
3. Creating your ros workspace
```
Ros Create your own workspace: http://wiki.ros.org/catkin/Tutorials/create_a_workspace
source /opt/ros/noetic/setup.bash
mkdir -p ~/catkin_ws/src
cd ~/catkin_ws/
catkin_make
```
4. Getting turtlesim running 
```
http://wiki.ros.org/turtlesim

```
5. Connecting MACBOOK to VirtualMachine Network
```
https://www.youtube.com/watch?v=0RXxubgQQqc
by default, network should be in NAT. So your network MAC Network should be able to ping your Ubuntu Network
```

6. Setting up rosbridge & start the 
```
ssl: https://devopscube.com/create-self-signed-certificates-openssl/
rosbridge with ssl : https://github.com/UbiquityRobotics/Robot_Commander/blob/master/README.md
```
