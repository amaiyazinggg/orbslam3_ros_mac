# ORB SLAM3 with ROS on Mac
Instructions on how to run ORB_SLAM3 with ROS on Apple Silicon Macs.

I have taken the files from [ORB-SLAM3-ROS](https://github.com/thien94/orb_slam3_ros) and made some changes to get it to run on MacOS. Tested on a M1 Macbook Air running MacOS Sonoma.

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
The version of [Pangolin](https://github.com/stevenlovegrove/Pangolin) in the original repo does not build on my system. However I was able to find one that does work - [Pangolin that works on mac](https://github.com/ZhaoqunZhong/Pangolin). 
```
# Get Pangolin
cd ~/your_fav_code_directory
git clone --recursive https://github.com/stevenlovegrove/Pangolin.git
cd Pangolin

# Install dependencies
./scripts/install_prerequisites.sh recommended

# Configure and build
cmake -B build
cmake --build build
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

## Summary of the changes made
- Changed -march=native to -mcpu=apple-m1 in `CMakeLists.txt`
- Removed `#include <tr1/..>` from everywhere since I was not able to load the library and it is not required
- Changed `stdint-gcc.h` to `stdint.h` since I am using clang and not gcc
- Changed type from `float` to `double` in `common.cc` because it led to some type casting issues.

## Issues
The above-mentioned fixes worked for me and may or may not work on your system. There might be missing dependencies and C++ library issues, which you might encounter. Raise an issue if any error pops up.
