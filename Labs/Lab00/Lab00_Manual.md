# Lab00  - Installation and Setup #
In this lab, you will be using two different USB's. In order to provide a better idea of which one you are using, we are going to use two separate names for each.

__Install USB:__ The USB that we will use to install ubuntu on the boot USB. This USB will be the smaller storage USB. 

__Boot USB:__ The USB that is going to be used to boot to once we install the full version of Ubuntu to it. This drive will be the larger storage and faster read/write speed USB.

# READ BEFORE DOING ANYTHING #
It is __EXTREMELY__ important that you read and follow everything in this lab. If you do not do exactly as is written or told to you by Ryan or Erik, there is a chance that you could accidentally delete your windows system and loose all of your files. Back up your computer before doing this lab if you are extremely concerned about this happening. Otherwise, make sure to ask Erik or Ryan to confirm you have everything correct during the storage set up in part __ .
https://www.youtube.com/watch?v=4BcVJT8eLv8&t=28s&ab_channel=AgileDevArt
# 1. Creating the bootable drive from an ISO#
One of the first things that you know when working with Linux and ROS, is how to create the bootable usb drive for installing Linux to your computers. This is a fairly simple process and where we are going to start in this lab. To start this process, jump down to your laptop's current OS.

## Windows ##
Creating a bootable drive is fairly easy to do on Windows. To begin this process, search "rufus bootable usb download" or go to https://rufus.ie/en/ and download the latest version of rufus.
Rufus is a program that allows you take any operating system's iso file and create a bootable installer on any usb that you give it. 
## Mac ##

## Linux ##
I'm currently too lazy to write this section so if you have Linux as your base computer, you'd better know how to create a bootable Linux drive on your own. If you have the audacity to ask Ryan or Erik why I (ryan) didn't write this section we will ruthlessly make fun of your lack of linux knowledge when most of you have taken SAT2711. 

# 2. Booting to your Install USB #
Once you finish making your install usb, shutdown your laptop and plug in your install usb. Now restart your laptop while hitting the button to enter your laptop's boot menu. In the chart below, find your system's manufacturer and use the hotkey to enter the boot menu.

| Manufacturer | Hotkey |
| -- | -- |
| Acer | F12 |
| Apple | Press and hold option while rebooting
| Asus | F8 |
| Dell | F12 |
| HP | Esc |
| Intel | F10 |
| Lenovo | F12, F8, F10 or Fn + F11 |
| Samsung | Esc |
| Sony | F11 or F10 |
| Toshiba | F12 |

Once you enter the boot menu you should be greeted with a few boot options. The first one will probably be your system's main boot drive (i.e. Windows or Mac) and the second should be the USB install drive that you have plugged in. If you do not see your install USB, press and hold the power button to shut it down and try to re-seat your install USB. If this still doesn't work, talk to Ryan or Erik to help with trying to troubleshoot this problem.
# 3. Installing to your Boot USB #
Once your install USB finishes booting up you will be given two options, "Try Ubuntu" or "Install Ubuntu". Pick the "Try Ubuntu" option and give it a minute or so to boot into something called a live boot instance. 