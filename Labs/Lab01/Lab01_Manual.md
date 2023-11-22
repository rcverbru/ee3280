# Linux and ROS Basics #
## 1. Setup ##
Linux is a huge portion of working with ROS which is why to be good with ROS you first need to become comfortable with working in the terminal. Using the terminal is one of the most important steps in becoming fluent and quick within ROS environments. Although it is entirely possible to do a lot of these labs within the GUI (Graphical User Interface), it'll take far less time if you learn a few easy commands.

To start off lets begin with the command, mkdir. This command is short for "make directory" and it does exactly as its name suggests. Run the following command in a fresh terminal.
```
mkdir ee3280
```
Once that command is run, you should notice that there is no feed back from the terminal. Now lets run the command again to see what happens. Hit the up arrow key once and you'll be able to cycle through all of your previously run commands. 

When you run the previous command again, you should receive the following error message:
`mkdir: cannot create directory ‘ee3280’: File exists`
As stated in the error, the directory already exists and can't be re-created. This is one of the many examples of errors that you'll probably run into while working with Linux and ROS. Make sure to read through the errors you get as many of the responses will provide ways to solve them.

Now comes the next two most important commands to know. These should be your go to whenever you approach a terminal. Lets begin with `cd` or "change directory." Now this is going to be very surprising but this command changes your location in your terminal to the input directory. Lets test it out:
```
cd ee3280
```
After running this command you should notice two things,
1. The blue lettering next to your user name and computer name changes to be the current working directory
2. There is no feed back from the terminal besides for the above change.

__1.1.1__ Q. Why might you receive the following error?
```
rcv@Hashbrown:~$ cd ee3280/
bash: cd: ee3280/: No such file or directory
```

## 2. Beans##
Q. What does it mean to source globally and when should you do it?

Q. What does it mean to source locally and when should you do it?