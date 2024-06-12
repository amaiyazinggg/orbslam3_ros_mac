# ORB SLAM3 with ROS on Mac
Instructions on how to run ORB_SLAM3 with ROS on Apple Silicon Macs. I have made the required changes in the files from [ORB-SLAM3-ROS](https://github.com/thien94/orb_slam3_ros) to get it to run on MacOS and tested on a M1 Macbook Air running MacOS Sonoma.

## Installing ROS on Mac (skip ahead if already done)
Follow the steps given here: [Installing ROS on Mac](https://atom-robotics-lab.github.io/wiki/markdown/ros/ROS_installation/installation_on_mac.html)

## Installing ORB-SLAM 3
The installation would require [`homebrew`](https://brew.sh) to be installed.

### Install `homebrew`
```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
## 1. Prerequisites
Make sure to install all these in the ROS environment that you created while installing ROS.
### Eigen
```
brew install eigen
```
### Pangolin
```
add here
```
### OpenCV
Check the OpenCV version on your computer (required at least 3.0):
```
python3 -c "import cv2; print(cv2.__version__)"
```
### `hector-trajectory-server`
Install `hector-trajectory-server` to visualize the real-time trajectory of the camera/imu. Note that this real-time trajectory might differ from the keyframes' trajectory.
```
conda install ros-noetic-hector-trajectory-server
```
## 2. Installation
```
cd ~/catkin_ws/src
git clone https://github.com/amaiyazinggg/orbslam3_ros_mac.git
cd ../
catkin build
```
## 3. Run Examples
Refer to [ORB-SLAM3-ROS](https://github.com/thien94/orb_slam3_ros) for instructions on how to run examples and further details.

## Issues
The above mentioned fixes worked for me and may or may not work on your system. Raise an issue if any error pops up.
