# 1. Setup your sources.list
```
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
```
# 2. Set up your keys
```
sudo apt install curl # if you haven't already installed curl
```
```
curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo apt-key add -
```
# 3. Installation
```
sudo apt update
```
```
sudo apt install ros-noetic-desktop-full
```
```
sudo apt install ros-noetic-ros-base
```
- 添加其他包:
- sudo apt install ros-noetic-PACKAGE
# 4. Environment setup
- setup ~/.bashrc
```
# >>>>>>>> ROS noetic <<<<<<<< 
source /opt/ros/noetic/setup.bash
```
# 5.Dependencies for building packages
```
sudo apt install python3-rosdep python3-rosinstall python3-rosinstall-generator python3-wstool build-essential
```
