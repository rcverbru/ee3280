---
Version: "2.1"
---
# Lab 6 #
__Aim:__ This lab will work with the simulating and then running the turtlebots
working with turtlebots on 
1. Setting up workspace
2. Connection
3. Simulation
4. With the bots

## 1. Setting up the workspace ##
To start this lab we're going to first install all the packages necessary to connect, simulate, and run the turtlebots. If you want to install them all by hand here's, the list of all the packages:
```
sudo apt install \
	ros-noetic-turtlebot3-bringup \
	ros-noetic-turtlebot3-description \
	ros-noetic-turtlebot3-gazebo \
	ros-noetic-turtlebot3-msgs \
	ros-noetic-turtlebot3-navigation \
	ros-noetic-turtlebot3-simulations \
	ros-noetic-turtlebot3-slam \
	ros-noetic-joy \
	ros-noetic-teleop-twist-joy \
	ros-noetic-teleop-twist-keyboard \
	ros-noetic-laser-proc \
	ros-noetic-rgbd-launch \
	ros-noetic-depthimage-to-laserscan \
	ros-noetic-rosserial-arduino \
	ros-noetic-rosserial-python \
	ros-noetic-rosserial-server \
	ros-noetic-rosserial-client \
	ros-noetic-rosserial-msgs \
	ros-noetic-amcl \
	ros-noetic-map-server \
	ros-noetic-move-base \
	ros-noetic-urdf \
	ros-noetic-xacro \
	ros-noetic-compressed-image-transport \
	ros-noetic-rqt* \
	ros-noetic-gmapping \
	ros-noetic-navigation \
	ros-noetic-interactive-markers \
	ros-noetic-dynamixel-sdk \
	ros-noetic-turtlebot3-msgs
```
If you don't want to install it all by hand, download the week12_lab.zip file from canvas and unzip it with the unzip command. Then cd into the folder that it creates and run the `chmod +x week12_lab_setup.sh` command. Now you'll be able to run it.

If you want to know more about what each script does, open them while you're waiting for everything to install and read through them.

Once all of the installs have finished, we will need to write a quick script to allow us to easily connect to the turtlebots. In your scripts folder within your ee3280 directory, create a new script called turtlebot_setup.sh and copy the following code into it.
```
#!/bin/bash
export ROS_MASTER_URI=http://{name-of-robot}:11311/
export ROS_HOSTNAME=32.80.100.XXX
export TURTLEBOT3_MODEL=burger
```
Now, from the list below, take the ip address or name of your bot and put it in the script:
![[turtlebot_ipchart]]
Make sure to also update the ROS_HOSTNAME variable with the last three digits of your laptop's IP address in place of XXX.

Next up, create a new lab06 workspace within your ee3280 folder to hold the packages that we're going to build.

## 2. Starting the Simulation ##
Before we get too much further with connecting and moving the turtlebot, lets first make sure everything works in simulation. By doing this we can better troubleshoot any problems that we run into throughout the course of this lab. 

In order to run the following launch files, we first need to export our necessary environment variable. Run the following command in each terminal that is going to be used.
`export TURTLEBOT3_MODEL=burger`

Now that the environment is set up, start by launching the gazebo environment that we'll be working with.
`roslaunch turtlebot3_gazebo turtlebot3_empty_world.launch`

Once the command finishes running, gazebo will open with a simulated version of the turtlebot in a 3D plane. Next run the following command to open a way to interface with the simulated bot:
`roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch`

While you have the turtlebot3_teleop terminal up, you can move the simulated turtlebot in the gazebo environment. 
## 3. Connecting to the Turtlebot ##
Since we have successfully moved the simulated turtlebot with the teleop node, lets try to set up the physical turtlebots to do the same thing. Start by sourcing the script you made earlier with the following command.
`source ~/ee3280/scripts/turtlebot_setup.sh`

In a new terminal we are going to connect to the turtlebot so that we can start up the necessary nodes. To do this we're going to use ssh:

`ssh ubuntu@{robot-name}`
\password: turtlebot

Once the terminal fully pops up, check to make sure that the networking in the .bashrc is correct by opening it with your favorite text editor (ex. nano, vim, ...). At the bottom of the file you should see the same export commands as the ones in your turtlebot_setup.sh script. Make sure that for both `ROS_MASTER_URI` and `ROS_HOSTNAME` the ip matches the turtlebot's ip.

Next run the following command:
`roslaunch turtlebot3_bringup turtlebot3_robot.launch`
This will startup all of the nodes for the turtlebot so we can interact with it.
## 4. Working with ROS Topics ##
With the turtlebot running, let's switch back to your original terminal where you sourced the startup script. As long as the networking between your laptop and the turtlebot was set up correctly, you should be able to see all of the topics that are being put out when you run `rostopic list`. The topic that you should be most interested to see is `/cmd_vel`. This topic tells the robot what speed and direction to move in. Due to ROS's publisher/subscriber setup, we can easily tell the robot what to do. In some cases, we don't even need to set up a node.

In a new terminal, ssh into the turtlebot again and then run the following command after changing the linear x value. Make sure to keep the x value between -0.22 and 0.22.
```
rostopic pub /cmd_vel geometry_msgs/Twist "linear:
  x: 0.0
  y: 0.0
  z: 0.0
angular:
  x: 0.0
  y: 0.0
  z: 0.0"
```

--------------
__Tip:__
	If you double tap tab after typing `/cmd_vel` the message will auto-complete for you and then you can go back and edit what you want to publish.

--------------
After running the command the turtlebot will move forward once and then stop. This is due to the fact that we're only pushing out one message to the velocity topic. If we created a loop that continuously posted that message to the topic we would have an actual publisher.

__Extra Fun:__ Create a publisher that tells the turtlebot to continuously move forward.