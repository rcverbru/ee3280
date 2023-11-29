# Lab 7 - SLAM #
In this lab we're going to be working with the turtlebots and the laser scanner that it has on top. The aim is to make it so that the turtlebot is able to map the room and then navigate autonomously.
### Note: Working with groups ###
If you are working with someone else, rock, paper, scissors to see who gets to act as the rosmaster. The rosmaster will be the person to start roscore on their system for the turtlebot to work off of. The person who isn't the rosmaster can then set the global ROS_MASTER_URI variable of their system to be the same as the rosmaster's ip, which will allow them to also interact and communicate with the bot. This means that between your two (or more) laptops, you can run the nodes to interact with the turtlebot (i.e. one person can run the slam node while the other runs the teleop node).
## Turtlebot IP Chart ##
![[turtlebot_ipchart]]

## 1. Setting up the workspace ##
__Terminal 1:__ In your *ee3280/* directory, create a new workspace called *lab07/* along with the accompanying *src/* folder inside of it. (Hint: use the -p flag when creating a set of nested directories to make both at the same time.)

Once you finish creating the initial workspace, cd into the source folder (*src/*) and clone two repo's with the following commands:
```
git clone -b melodic-devel https://github.com/ROBOTIS-GIT/turtlebot3_simulations.git

git clone https://github.com/turtlebot/turtlebot.git
```
Now cd back to the root of the workspace and run the `catkin_make` command to build everything you just cloned. Now we're going to leave this terminal open and switch to a new one.
## 2. Network and Global Variable Setup ##
Since we have the workspace ready for us to use, we now need to set up our networking to make sure the turtlebot will know what ip to look for. To do this we're going to reuse the turtlebot_setup script from the previous labs.

__Terminal 2:__ In a new terminal, cd to your *scripts/* directory in *ee3280/* and edit your turtlebot_setup.sh scrip using your favorite editor. Once it opens you should see something like this:
![[turtlebot_setup.sh]]
Make sure that your ROS_MASTER_URI and ROS_HOSTNAME variables both match with your laptop's current ip. Save and close the file once you're done and then source it using the `source` command. Now go ahead and start roscore.
## 3. Setting up the turtlebot ##
Now that our system is set up to work with the turtlebots, lets move on to setting them up to work with our system.
__Terminal 3:__ In a new terminal, ssh into the turtlebot using the following command:
```
ssh ubuntu@{IP.ADDRESS.OF.TURTLEBOT}
```
Same as before, pick your favorite non-graphical (vim or nano) text editor and open the turtlebot's .bashrc file. At the bottom of the file you will see the same two lines as you had in the script. Make sure that the ROS_MASTER_URI variable matches with your system's ip and that the ROS_HOSTNAME variable matches with your robot's ip (as shown below). 
```
export ROS_MASTER_URI=http://{remote-system-ip}:11311/
export ROS_HOSTNAME={ip-of-the-robot}
```
Save and close the file once you're finished and then source the turtlebot's .bashrc with the `source` command. Now, we are going to start up the first launch file on the turtlebot to start up the turtlebot's sensors and motors. Run the following command while making sure to hit tab as you're writing it out so as to help auto-complete as you go.
```
roslaunch turtlebot3_bringup turtlebot3_robot.launch
```
__Terminal 4:__ In another terminal we're going to ssh into the turtlebot again but this time start up the lidar driver with the following command:
```
rosrun ld08_driver ld08_driver
```
## 4. Physical Turtlebot SLAM ##
Before we get too much further with SLAM, let's first set the turtlebot down somewhere so it can freely move and map out an area.

__Terminal 1:__ Now lets go back to Terminal 1 where we originally started and launch the SLAM node. Local source your lab07 package and use the following command to launch the slam node while making sure to input gmapping as the method that you're going to use. 
```
roslaunch turtlebot3_slam turtlebot3_slam.launch slam_methods:={slam-method}
```
This command will probably take a little bit to start up and once it does, you should be able to see rviz open up on your screen. As time goes on, you should see that the pixelated map of where your turtlebot is will slowly fill in based on the readings from the laser scanner. 

__Terminal 5:__ Once you see that the SLAM node finished starting up, we're going to open a new terminal and launch the teleoperation node so you can move the turtlebot around the room. Local source your lab07 package again, and use the following command to startup the node.
```
roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch
```

Drive the turtlebot around the room to build a map of the area. Avoid changing speed or turning too quickly and make sure to get a complete map of the walls. After the map is complete, ctrl-C the teleoperation node then save the map.
```
rosrun map_server map_saver -f ~/map5
```
## 5. Autonomous Movement Using SLAM - WIP ##
Similar to section 2, we are going to use the map we created to allow the turtlebot to autonomously navigate through the maze.
```
roslaunch turtlebot3_navigation turtlebot3_navigation.launch map_file:=$HOME/map5.yaml
```
Once Rviz opens, click the 2D Pose Estimate button.
![](https://lh7-us.googleusercontent.com/6ppXVRuFCu8BC409XDe8_a-BvDNbrFAed8Sux8lkaE-2jTCh_HxnsjRStmq2xHh5nIGSW9EanWYRiruIgggxP0YsdQthojX_TqqNwXxGPZgkYwncNKAFOW-UDhQMmK2WZ8--5__KKIqIqBWAri_hGQ)
This will put a green arrow on the map with the turtlebot. Drag the arrow over to the direction the robot is facing. Repeat the steps of clicking the 2D Pose Estimate then dragging the arrow a few times.
Next we need to move the robot back and forth some to allow for a more precise initial pose estimate. Launch the teleoperation node then move the turtlebot a small amount back and forth.
```
roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch
```
Ctrl-C the teleoperation node when you are done. Now that the initial pose is set, we can give the turtlebot a navigational end point. Click the 2D Nav Goal.
![](https://lh7-us.googleusercontent.com/WA34EmoGfai5ZbJ5lNxl-fRS0mbn0hufY3RVt4RDlYgTVaPGIhFRzQ7x50xWQjx5nG7Q2uBV8L2p81qtRlt3XMLIFraMX-ATRv6GXPUF4fBldKbOGmg_7_1ZaCMxESkq3FT_FZnSI1g51nEjZD7CkQ)
Now click on the map to tell the robot and end point. Once you click you will see a green arrow pop up. Rotate the arrow to tell the turtlebot the desired rotational position. Once you let go of the green arrow, the turtlebot should automatically move to the navigation goal. 