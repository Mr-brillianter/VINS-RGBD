## RGBD-Inertial Trajectory Estimation and Mapping for Small Ground Rescue Robot
Based one open source SLAM framework [VINS-Mono](https://github.com/HKUST-Aerial-Robotics/VINS-Mono).
## Paper
来源：Shan, Zeyong, Ruijian Li, and Sören Schwertfeger. "RGBD-inertial trajectory estimation and mapping for ground robots." Sensors 19.10 (2019): 2251.

# environment: ubuntu 20.04 ros NEOTIC 



neotic use OPENCV4, 而vins - rgbd 使用opencv3，要修改源码

１．在camera_model包中的头文件Chessboard.h中添加
```
#include <opencv2/imgproc/types_c.h>
#include <opencv2/calib3d/calib3d_c.h>
```

２在CameraCalibration.h中添加
```
#include <opencv2/imgproc/types_c.h>
#include <opencv2/imgproc/imgproc_c.h>
```
３．看着哪里报错，ｒｇｂ２ｇｒａｙ改成ｃｖ＿ｃｏｌｏｒ

４．可能出现sophus不兼容，看着改成.hpp

５. 项目编译运行方式：

（1）在catkin_ws的src文件夹内放入[VINS-RGBD](https://link.zhihu.com/?target=https%3A//github.com/STAR-Center/VINS-RGBD)工程

（2）catkin_make

（３）terminal １主程序　ｒｏｓｌａｕｎｃｈ　ｎｏ longer need roscore

​      source devel/setup.bash

​      roslaunch vins_estimator realsense_color.launch

（４）terminal２　ｒｖｉｚ窗口

​    source devel/setup.bash

​    roslaunch vins_estimator vins_rviz.launch

（５）terminal ３放数据包

​    rosbag play Simple.bag

​    rosbag play Normal.bag

​    rosbag play "With more rotation.bag.bag"

参考：

知乎：https://zhuanlan.zhihu.com/p/245193211

ｃｓｄｎ：https://blog.csdn.net/xiaojinger_123/article/details/121517771（尽管说的是ｖｉｎｓ－ｆｕｓｉｏｎ但依然有效）
















The approach contains
+ Depth-integrated visual-inertial initialization process.
+ Visual-inertial odometry by utilizing depth information while avoiding the limitation is working for 3D pose estimation.
+ Noise elimination map which is suitable for path planning and navigation.

the proposed approach can also be applied to other application like handheld and wheeled robot.

This dataset is part of the dataset collection of the [STAR Center](https://star-center.shanghaitech.edu.cn/), [ShanghaiTech University](http://www.shanghaitech.edu.cn/eng): https://star-datasets.github.io/

A video showing the data is available here: https://robotics.shanghaitech.edu.cn/datasets/VINS-RGBD




    @article{shan2019rgbd,
      title={RGBD-inertial trajectory estimation and mapping for ground robots},
      author={Shan, Zeyong and Li, Ruijian and Schwertfeger, S{\"o}ren},
      journal={Sensors},
      volume={19},
      number={10},
      pages={2251},
      year={2019},
      publisher={Multidisciplinary Digital Publishing Institute}
    }


## 1. Prerequisites
1.1. **Ubuntu** 16.04 or 18.04.

1.2. **ROS** version Kinetic or Melodic fully installation

1.3. **Ceres Solver**
Follow [Ceres Installation](http://ceres-solver.org/installation.html)

1.4. **Sophus**
```
  git clone http://github.com/strasdat/Sophus.git
  git checkout a621ff
```


## 2. Datasets
Recording by RealSense D435i. Contain 9 bags in three different applicaions:
+ [Handheld](https://star-center.shanghaitech.edu.cn/seafile/d/0ea45d1878914077ade5/)
+ [Wheeled robot](https://star-center.shanghaitech.edu.cn/seafile/d/78c0375114854774b521/) ([Jackal](https://www.clearpathrobotics.com/jackal-small-unmanned-ground-vehicle/))
+ [Tracked robot](https://star-center.shanghaitech.edu.cn/seafile/d/f611fc44df0c4b3d936d/)

Note the rosbags are in compressed format. Use "rosbag decompress" to decompress.

Topics:
+ depth topic: /camera/aligned_depth_to_color/image_raw
+ color topic: /camera/color/image_raw
+ imu topic: /camera/imu




## 3. Licence
The source code is released under [GPLv3](http://www.gnu.org/licenses/) license.
