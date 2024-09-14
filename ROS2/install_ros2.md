#  **install ros2 in ubuntu22**

## set locale
- Make sure you have a locale which supports `UTF-8`
```
locale  # check for UTF-8
```
```
sudo apt update && sudo apt install locales
sudo locale-gen en_US en_US.UTF-8
sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
export LANG=en_US.UTF-8
```
```
locale  # verify settings
```

## setup source
- First ensure that the [Ubuntu Universe repository](https://help.ubuntu.com/community/Repositories/Ubuntu) is enabled.
```
sudo apt install software-properties-common
sudo add-apt-repository universe
```

- Now add the ROS 2 GPG key with apt.
```
sudo apt update && sudo apt install curl -y
sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg
```

- Then add the repository to your sources list.
```
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(. /etc/os-release && echo $UBUNTU_CODENAME) main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null
```

## install ros2 packages
- Update your apt repository caches after setting up the repositories.
```
sudo apt update
```

- ROS 2 packages are built on frequently updated Ubuntu systems. It is always recommended that you ensure your system is up to date before installing new packages.
```
sudo apt upgrade
```
```
sudo apt install ros-humble-desktop
```
```
sudo apt install ros-humble-ros-base
```
```
sudo apt install ros-dev-tools
```

## environment setup
- Set up your environment by sourcing the following file.
- Add the following statement to the ~/.bashrc file
```
source /opt/ros/humble/setup.bash
```