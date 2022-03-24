# interactive_slam

```cpp
// *参考：https://github.com/SMRT-AIST/interactive_slam/issues/15
// glfwWindowHint(GLFW_CONTEXT_VERSION_MAJOR, 3);
// glfwWindowHint(GLFW_CONTEXT_VERSION_MINOR, 0);

glfwWindowHint(GLFW_CONTEXT_VERSION_MAJOR, 3);
glfwWindowHint(GLFW_CONTEXT_VERSION_MINOR, 3);
glfwWindowHint(GLFW_OPENGL_PROFILE, GLFW_OPENGL_CORE_PROFILE);
```

***interactive_slam*** is an open source 3D LIDAR-based mapping framework. In contrast to existing automatic SLAM packages, we aim to develop a semi-automatic framework which allows the user to interactively and intuitively correct mapping failures (e.g., corrupted odometry, wrong loop detection, distorted map, etc) with minimal human effort. This framework provides several map correction features:
  - [Manual & Automatic] Loop closing
  - [Manual] Plane-based map correction
  - [Manual] Multiple map merging
  - [Automatic] Pose edge refinement


![Screenshot_20191016_182424](https://user-images.githubusercontent.com/31344317/66906208-3f2e0880-f042-11e9-8366-c178f9c00b65.png)
[[video]](https://youtu.be/vAqo6YkbKpU)


This package is built on top of the ROS ecosystem. You can start building a map with a pose graph constructed by [hdl_graph_slam](https://github.com/koide3/hdl_graph_slam) or a customized [LeGO-LOAM](https://github.com/koide3/LeGO-LOAM-BOR), or odometry data generated by any ROS package.

This package has been tested on Ubuntu 18.04 & ROS melodic or later.

[![Build](https://github.com/SMRT-AIST/interactive_slam/actions/workflows/build.yml/badge.svg)](https://github.com/SMRT-AIST/interactive_slam/actions/workflows/build.yml)

## Installation
***interactive_slam*** depends on the following libraries:

  - [GL3W](https://github.com/skaslev/gl3w)
  - [GLFW](https://www.glfw.org/)
  - [Dear ImGui](https://github.com/ocornut/imgui)
  - [portable-file-dialog](portable-file-dialog)
  - [OpenMP](https://www.openmp.org/)
  - [PCL](https://github.com/skaslev/gl3w)
  - [g2o](https://github.com/RainerKuemmerle/g2o)


```bash
# for ROS melodic
sudo apt-get install libglm-dev libglfw3-dev
sudo apt-get install ros-melodic-geodesy ros-melodic-pcl-ros ros-melodic-nmea-msgs ros-melodic-libg2o
```

```bash
cd ~/catkin_ws/src
git clone https://github.com/koide3/ndt_omp
# on melodic
# git clone https://github.com/koide3/ndt_omp -b melodic
git clone https://github.com/koide3/hdl_graph_slam
git clone https://github.com/koide3/odometry_saver
git clone https://github.com/SMRT-AIST/fast_gicp --recursive
git clone https://github.com/SMRT-AIST/interactive_slam --recursive

cd ~/catkin_ws
catkin_make -DCMAKE_BUILD_TYPE=Release
```

***ROS Kinetic users***  
This package cannot be built using gcc and ld on Ubuntu 16. If you are on Ubuntu 16 and ROS kinetic, try the LLVM toolchain. Note: we recommend to use this package on melodic because we do only build-test but not run-test on kinetic.

```bash
sudo apt install clang-6.0 lld-6.0
sudo update-alternatives --install /usr/bin/ld ld /usr/bin/ld.lld-6.0 50
sudo update-alternatives --install /usr/bin/clang clang /usr/bin/clang-6.0 50
sudo update-alternatives --install /usr/bin/clang++ clang++ /usr/bin/clang++-6.0 50
cd ~/catkin_ws && rm -rf build devel    # be aware of that this command removes build and devel directories
CC=clang CXX=clang++ catkin_make -DCMAKE_BUILD_TYPE=Release
```

## Examples

### Example1 - Basic usage with hdl_graph_slam

In this example, we edit a map (pose graph) constructed by [hdl_graph_slam](https://github.com/koide3/hdl_graph_slam).  [See more](https://github.com/koide3/interactive_slam/wiki/Example1).
![Screenshot_20191016_175924 png](https://user-images.githubusercontent.com/31344317/66904272-c11c3280-f03e-11e9-9420-078d75c5c0e9.jpg)

### Example2 - Generating odometry with external ROS package

In this example, we create a map with odometry data generated from a rosbag file with LeGO-LOAM. [See more](https://github.com/koide3/interactive_slam/wiki/Example2).

### Example3 - Plane-based map correction & Map merging

In this example, we correct a largely bent map with plane constraints and merge it with another map. [See more](https://github.com/koide3/interactive_slam/wiki/Example3).

![Screenshot_20191016_182955 png](https://user-images.githubusercontent.com/31344317/66906642-fe82bf00-f042-11e9-9373-f810337f4d97.jpg)

## Graph/Odometry file format

You can feed graph/odometry files generated by your program to ***interactive_slam***. [See more](https://github.com/koide3/interactive_slam/wiki/Format)

## FAQ

[FAQ](https://github.com/koide3/interactive_slam/wiki/FAQ)

## License
***interactive_slam*** is released under GPLv3 license.

## Related packages

- [hdl_graph_slam](https://github.com/koide3/hdl_graph_slam)
- [hdl_localization](https://github.com/koide3/hdl_localization)
- [hdl_people_tracking](https://github.com/koide3/hdl_people_tracking)

## Papers
Kenji Koide, Jun Miura, Masashi Yokozuka, Shuji Oishi, and Atsuhiko Banno, Interactive 3D Graph SLAM for Map Correction, IEEE Robotics and Automation Letters (RA-L), 2020 [DOI](https://doi.org/10.1109/LRA.2020.3028828)

## Contact
[発展版機能について](https://github.com/SMRT-AIST/interactive_slam/wiki/%E7%99%BA%E5%B1%95%E7%89%88%E6%A9%9F%E8%83%BD%E3%81%AB%E3%81%A4%E3%81%84%E3%81%A6)

Kenji Koide, k.koide@aist.go.jp, https://staff.aist.go.jp/k.koide

Mobile Robotics Research Team  
National Institute of Advanced Industrial Science and Technology (AIST), Japan  [\[URL\]](https://unit.aist.go.jp/hcmrc/mr-rt/index.html)
