# GLIM-converter

## Dependencies
sudo apt install -y nlohmann-json3-dev

## Documentation
```shell
https://koide3.github.io/glim/
```

For common depenedecies
```shell
https://koide3.github.io/glim/installation.html
```

## Intended use 

This small toolset allows to integrate SLAM solution provided by [GLIM](https://github.com/koide3/glim) with [HDMapping](https://github.com/MapsHD/HDMapping).
This repository contains ROS 2 workspace that :
  - submodule to tested revision of GLIM
  - a converter that listens to topics advertised from odometry node and save data in format compatible with HDMapping.


## Building

Clone the repo
```shell
mkdir -p /test_ws/src
cd /test_ws/src
git clone https://github.com/marcinmatecki/GLIM-to-HDMapping.git --recursive
cd ..
colcon build
```

## Usage - data SLAM:

Prepare recorded bag with estimated odometry:

In first terminal record bag:
```shell
ros2 bag record /glim_ros/aligned_points_corrected /glim_ros/odom_corrected
```

and start odometry:
```shell 
cd /test_ws/
source ./install/setup.sh # adjust to used shell
ros2 run glim_ros glim_rosbag <path_to_rosbag>
```

## Usage - conversion:

```shell
cd /test_ws/
source ./install/setup.sh # adjust to used shell
ros2 run glim-to-hdmapping listener <recorded_bag> <output_dir>
```

## Example:

Download the dataset from [GitHub - ConSLAM](https://github.com/mac137/ConSLAM) or 
directly from this [Google Drive link](https://drive.google.com/drive/folders/1TNDcmwLG_P1kWPz3aawCm9ts85kUTvnU). 
Then, download **sequence2**.

## Convert(If it's a ROS1 .bag file):

```shell
rosbags-convert --src {your_downloaded_bag} --dst {desired_destination_for_the_converted_bag}
```

## Record the bag file:

```shell
ros2 bag record /glim_ros/aligned_points_corrected /glim_ros/odom_corrected {your_directory_for_the_recorded_bag}
```

## GLIM Launch:

```shell
cd /test_ws/
source ./install/setup.sh # adjust to used shell
ros2 run glim_ros glim_rosbag {path_to_bag_file} 
```

## During the record (if you want to stop recording earlier) / after finishing the bag:

```shell
In the terminal where the ros record is, interrupt the recording by CTRL+C
Do it also in ros launch terminal by CTRL+C.
```

## Usage - Conversion (ROS bag to HDMapping, after recording stops):

```shell
cd /test_ws/
source ./install/setup.sh # adjust to used shell
ros2 run glim-to-hdmapping listener <recorded_bag> <output_dir>
```
