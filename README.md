# ros2_gazebo_setup


## versions
**OS**: Ubuntu 20.04 LTS <br>
**g++**: (Ubuntu 9.3.0-17ubuntu1~20.04) 9.3.0 <br>
**clang-format**: 12 <br>
**cmake**: 3.16.3 <br>
**ROS2**: galactic <br>
**Gazebo**: 11.10.0 <br>


# Install ROS2 and Gazebo11

## install ROS2:
install ROS-Base: https://docs.ros.org/en/galactic/Installation/Ubuntu-Install-Debians.html <br>

## install Gazebo11:
install Gazebo: 
```sh
curl -sSL http://get.gazebosim.org | sh
```

# Dependencies:
```sh
sudo apt update
```
install colcon, vcstool and rosdep: 
```sh
sudo apt install -y python3-colcon-common-extensions python3-vsctool python3-rosdep
```


# import and install dependencies
git repo dependencies of your workspace in ```dependencies.repos```:
```
repositories:
  # interfaces
  common_interfaces:
    type: git
    url: git@github.com:ros2/common_interfaces.git
    version: galactic
  
  # ros utils
  rclcpp:
    type: git
    url: git@github.com:ros2/rclcpp.git
    version: galactic
  
  # gazebo
  gazebo_ros_pkgs:
    type: git
    url: git@github.com:ros-simulation/gazebo_ros_pkgs.git
    version: galactic
```

clone dependencies (git repos) into ```src``` directory:
```sh
vcs import ./src < dependencies.repos
```

setup rosdep

```sh
sudo rosdep init
```
```sh
rosdep update
```

install dependencies from all ROS packages in ```src``` directory:
```sh
rosdep install --from-paths src --ignore-src -r -y
```

# Build ROS packages with colcon
source underlaying ros:
```bash
source /opt/ros/galactic/setup.bash
```
>you may change galactic with your ROS2 version


build all ROS packages in ```src``` directory:
```bash
colcon build --symlink-install
```

now source your overlaying ROS environment:
```bash
source install/setup.bash
```