# Lab00  - Installation and Setup #
In this lab, you will be using two different USB's. In order to provide a better idea of which one you are using, we are going to use two separate names for each.

__Install USB:__ The USB that we will use to install ubuntu on the boot USB. This USB will be the smaller storage USB. 

__Boot USB:__ The USB that is going to be used to boot to once we install the full version of Ubuntu to it. This drive will be the larger storage and faster read/write speed USB.

# READ BEFORE DOING ANYTHING #
It is __EXTREMELY__ important that you read and follow everything in this lab. If you do not do exactly as is written or told to you by Ryan or Erik, there is a chance that you could accidentally delete your windows system and loose all of your files. Back up your computer before doing this lab if you are extremely concerned about this happening. Otherwise, make sure to ask Erik or Ryan to confirm you have everything correct during the storage set up in part __ .

https://www.youtube.com/watch?v=4BcVJT8eLv8&t=28s&ab_channel=AgileDevArt
# 1. Creating the bootable drive from an ISO #
One of the first things that you know when working with Linux and ROS, is how to create the bootable usb drive for installing Linux to your computers. This is a fairly simple process and where we are going to start in this lab. To start this process, jump down to your laptop's current OS.

## Windows ##
Creating a bootable drive is fairly easy to do on Windows. To begin this process, search "rufus bootable usb download" or go to https://rufus.ie/en/ and download the latest version of rufus.
Rufus is a program that allows you take any operating system's iso file and create a bootable installer on any usb that you give it. 

Balena - https://github.com/balena-io/etcher/releases/download/v1.18.11/balenaEtcher-Setup-1.18.11.exe
## Mac ##

Balena - https://github.com/balena-io/etcher/releases/download/v1.18.11/balenaEtcher-1.18.11-x64.AppImage

## Linux ##
I'm currently too lazy to write this section so if you have Linux as your base computer, you'd better know how to create a bootable Linux drive on your own. If you have the audacity to ask Ryan or Erik why I (ryan) didn't write this section we will ruthlessly make fun of your lack of linux knowledge when most of you have taken SAT2711. 

Balena - https://github.com/balena-io/etcher/releases/download/v1.18.11/balenaEtcher-1.18.11-x64.AppImage

Once you finish building 

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
# 3. Finding your drives names #
Once your install USB finishes booting up you will be given two options, "Try Ubuntu" or "Install Ubuntu". Pick the "Try Ubuntu" option and give it a minute or so to boot into something called a live boot instance. Live boot instances are single use systems that allow you to do everything that you would want to in a Linux environment, but once you shut them down, all of the files and any other work you were doing on it gets removed and re-set back to being a blank copy. Because of this, we are going to use the second USB drive to act as the standard boot drive you'd see in a normal system.

Once Ubuntu finishes loading up, open a terminal and type in the following command:
```
lsblk
```
This command lists every block device on your system along with where it is located. An example output from this command will look like this:
```
rcv@Hashbrown:~$ lsblk
NAME        MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
loop0         7:0    0     4K  1 loop /snap/bare/5
loop1         7:1    0 164.8M  1 loop /snap/gnome-3-28-1804/194
loop2         7:2    0  73.9M  1 loop /snap/core22/864
...
sda           8:0    1  28.9G  0 disk 
├─sda1        8:1    1   4.1G  0 part /media/rcv/Ubuntu 20.04.6 LTS amd64
└─sda2        8:2    1     4M  0 part 
nvme0n1     259:0    0 465.8G  0 disk 
├─nvme0n1p1 259:1    0   3.8G  0 part [SWAP]
├─nvme0n1p2 259:2    0   110G  0 part /
└─nvme0n1p3 259:3    0 350.2G  0 part /home
nvme1n1     259:4    0 953.9G  0 disk 
├─nvme1n1p1 259:5    0   300M  0 part /boot/efi
├─nvme1n1p2 259:6    0   128M  0 part 
├─nvme1n1p3 259:7    0 931.2G  0 part 
├─nvme1n1p4 259:8    0   900M  0 part 
└─nvme1n1p5 259:9    0  21.4G  0 part 
```
The two that we currently care about are going to be listed at the bottom. As you can see in the above example the two listed devices are nvme0n1 and nvme1n1. If you remember from SAT2711, we learned that when a device is listed as nvme its generally a m.2 storage device. 


The other option that you might see is sdx where x is any letter in the alphabet starting from a. In this case we should be expecting at least one of these sdx drives showing up in your list as that is what your install usb will be listed as. Take note to check how big the drive is so that you can compare it to the 4th row in your lsblk output to make sure you grab the right drive. For example, if your install drive is 32GB you should be able to see a line with about "32G" in the 4th column. Make sure to grab whichever sdx name that it is and save this for later.

Now that you have the install drive's block name, plug in your boot drive and run the lsblk command again and make sure to grab and set aside the sdx name.

## 4.  ##

storage setup - sign off

500 MB efi
ext4 /
## 5. Installing ROS ##

# 5. TBD #