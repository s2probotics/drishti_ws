# Point-LIO-ROS2 (with Unitree Unilidar L1/L2 support)
## Point-LIO: Robust High-Bandwidth Lidar-Inertial Odometry


## **1. Prerequisites**

### **1.1 Ubuntu and [ROS](https://www.ros.org/)**
We tested our code on Ubuntu 22.04 with Humble. Other versions may have problems of environments to support the Point-LIO, try to avoid using Point-LIO in those systems.

Additional ROS package is required:

- For ROS2 Humble:
    ```bash
    sudo apt-get install ros-humble-pcl-ros
    sudo apt-get install ros-humble-pcl-conversions
    sudo apt-get install ros-humble-visualization-msgs
    ```

### **1.2 Eigen**
Following the official [Eigen installation](eigen.tuxfamily.org/index.php?title=Main_Page), or directly install Eigen by:
```bash
sudo apt-get install libeigen3-dev
```

### **1.3 `Livox-SDK2`**
Please follow the guidance of installation from [Livox-SDK2/README.md](https://github.com/Livox-SDK/Livox-SDK2/blob/master/README.md).


### **1.4 `unilidar_sdk2`**

For using lidar `L2`, you should download [unilidar_sdk2](https://github.com/unitreerobotics/unilidar_sdk2) in the home directory:

```bash
cd
git clone https://github.com/unitreerobotics/unilidar_sdk2.git
```

## 4. Build
Clone the repository and colcon build:

```bash
    cd
    git clone git@github.com:s2probotics/drishti_ws.git
    cd drishti_ws
    export VERSION_ROS2="ROS2"  # Important
    export ROS_DISTRO="humble"  # Important
    colcon build --cmake-args -DROS_EDITION=${VERSION_ROS2} -DDISTRO_ROS=${ROS_DISTRO} --symlink-install  # Important
    source install/setup.bash
```
- If you want to use a custom build of PCL, add the following line to ~/.bashrc
```export PCL_ROOT={CUSTOM_PCL_PATH}```

## 5. Directly run

### 5.1 For Unitree LiDAR (L1 as an example)

Step A: Run below
```
    cd ~/drishti_ws
    source install/setup.bash
    ros2 launch point_lio mapping_unilidar_l2.launch.py
```

Step B: Run LiDAR's ros driver in a new terminal
```
    cd ~/drishti_ws
    source install/setup.bash
    ros2 launch unitree_lidar_ros2 launch.py
```

### 5.2 PCD file save

Set ``` pcd_save_enable ``` in launchfile to ``` 1 ```. All the scans (in global frame) will be accumulated and saved to the file ``` Point-LIO/PCD/scans.pcd ``` after the Point-LIO is terminated. ```pcl_viewer scans.pcd``` can visualize the point clouds.

*Tips for pcl_viewer:*
- change what to visualize/color by pressing keyboard 1,2,3,4,5 when pcl_viewer is running. 
```
    1 is all random
    2 is X values
    3 is Y values
    4 is Z values
    5 is intensity
```
