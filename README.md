# HRS Lecture Workspace

# Setup
- copy the https link in the top right under "clone"
- clone with git into local folder: ```$ git clone <address>```
- open with "Visual Studio Code"
- vs code should have the "Remote Development" extension installed
- there should be a pop-up asking if you want to reopen in devcontainer -> click yes
- wait for the devcontainer to be set up (you can click on the log printout)
- open a terminal in vs code and source ROS: ```$ source /opt/ros/kinetic/setup.bash```

# Settings
- change the NAO_IP in the "Dockerfile" to the one your robot tells you 
- for rendering pass-through to work, you need to tell the xserver on the host to accept connections from the devcontainer with: ```$ xhost local:root``` (in a host terminal, only tested on ubuntu)

# Recommendations
- use the ROS extension in vs code for more features
- Catkin Tools are preinstalled so you can build faster with ```$ catkin build``` instead of ```$ catkin-make```
- if you want to install packages or do other permanent changes in your container, test them first in the running devcontainer terminal, and if it works, add the change to the bottom of the "Dockerfile" so that they persist over devvontainer rebuilds
