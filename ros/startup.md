## ROBOT

### ros

> ROS (Robot Operating System, 机器人操作系统) 提供一系列程序库和工具以帮助软件开发者创建机器人应用软件。它提供了硬件抽象、设备驱动、库函数、可视化、消息传递和软件包管理等诸多功能。ROS 遵守 BSD 开源许可协议

- 建议边看http://wiki.ros.org/  中的 ros tutorial， 边跟着视频学习。 
- 当前我们的代码版本为 ros kinetic(Ubuntu16.04), 但准备迁移到最新的 ros noetic(Ubuntu20.04),所以建议学习noetic版本

- [ROS noetic版本入门视频教程(极其详细)](https://www.bilibili.com/video/BV1Ci4y1L7ZZ)

- [ROS melodic版本入门视频教程(较简略)](https://www.bilibili.com/video/BV1zt411G7Vn)

- [ROS机器人开发案例](https://www.bilibili.com/video/BV1vb41177qN) 

#### ros navigation
- [导航常用的ROS工具包](http://wiki.ros.org/navigation/) 
- 建议从move_base开始看，先了解导航系统的最经典架构方式，然后了解其中几个重要package的使用方式及算法原理，如 global_planner, dwa_local_planner, amcl, gmapping, cartography, map_server, costmap_2d 等重点学习
- 重点学习[tf](http://wiki.ros.org/tf/)，熟悉可视化工具[rviz](http://wiki.ros.org/rviz)的使用

#### KM-Filter（卡尔曼，粒子滤波）：

- 《概率机器人》前9章，建议先看概率机器人，看不懂再看[视频教程](https://www.bilibili.com/video/BV1CJ411N7xL)。

#### python robotics
- [python robotics](https://github.com/AtsushiSakai/PythonRobotics) 是经典导航算法的 python 代码合集, 非常易于理解，用来了解经典算法的思想和实现


##### 视觉slam

- 高翔，《视觉slam14讲》，另外 此书前几章对理解机器人**坐标系**挺有帮助。

##### 其它:

- [欠驱动机器人学](https://www.bilibili.com/video/BV1LA411v75c)



## 强化学习，机器学习，深度学习，等XX学习部分

#### Machine Learning:

- 吴恩达 https://www.bilibili.com/video/BV16J411t71N
- 李航《统计学习方法》
- 周志华《西瓜书》


#### Reinforcement Learning:

-  https://www.bilibili.com/video/BV1kt411D76e，David Silver 课程主页，有ppt和最新的视频：https://www.davidsilver.uk/teaching/


#### Deep Reinforcement Learning:

- 李宏毅课程主页：http://speech.ee.ntu.edu.tw/~tlkagk/courses.html，视频：https://www.bilibili.com/video/BV1JE411g7XF?from=search&seid=10163520251975319879

- 伯克利 cs294， https://www.bilibili.com/video/BV18b411e733

- 伯克利 cs285，http://rail.eecs.berkeley.edu/deeprlcourse/



学习建议：

建议先看李宏毅的深度学习，里面也有机器学习的一点部分，看完CNN，RNN，GAN这些，然后看David-sliver的传统强化学习，再看李宏毅的深度强化学习，再看伯克利cs294的深度强化学习。

机器学习算法部分，快速看一遍吴恩达视频，然后看《统计学习方法》。





#### 自动驾驶

- https://github.com/Autoware-AI/autoware.ai/wiki/Source-Build

- https://answers.ros.org/questions/scope:all/sort:activity-desc/tags:autoware/page:1/

- https://discourse.ros.org/c/autoware/46

#### apollo:

- https://apollo.auto/devcenter/courselist_cn.html?target=1

- https://www.bilibili.com/video/BV1M4411g7g3/

## 数学基础

- 强化学习基础：https://www.bilibili.com/video/BV1Et4y1C7co

- 应用数学基础：https://www.bilibili.com/video/BV13T4y1g7Bz

- 统计机器学习：https://www.bilibili.com/video/BV1Hi4y1s7iq

- 深度多任务和元学习：https://www.bilibili.com/video/BV15t4y127V1

- 神经网络与深度学习(书)：https://nndl.github.io/

