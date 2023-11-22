# Local Lab WiFi Setup #
The WiFi that we have set up for the lab is not like normal networks that you'd see in usual places such as eduroam or our MichiganTech networks. This network is a small internal Local Area Network (LAN) that we us for allowing all of the robots in the lab to communicate with each other and whoever needs to use them. So when connecting to this network remember that you won't be able to connect to the internet to pull up any browser related items or install packages through the terminal. If you want to do any of those listed items make sure to connect back to the main network to do what you need to do.
## Login Details ##
WiFi Name: ee3280_roslab
Password: not_pizza

----------------------
# Connecting to the Robots in the Lab #
In this lab we're going to be working with mainly two specific robots, one being a Turtlebot and the other being a Niryo Ned2 Arm. 
## Turtle Bots ##
### SSH ###
username: ubuntu
password: turtlebot
### Lab WiFi ###

![[turtlebot_ipchart]]
### Ethernet ###
## Niryo Ned Arm ##
### SSH ###
username: niryo
password: robotics
### Hotspot  ###
The hotspot name varies for each arm but for the 4 arms that are in this lab, we have the following names:

![[niryo_ned_hotspot]]

Password: niryorobot
IP Address: 10.10.10.10
### Lab WiFi ###
![[niryo_ned_ipchart]]
### Ethernet ###
IP Address: 169.254.200.201