# 激光SLAM简介

## SLAM是什么

Localization:在给定地图的情况下，估计机器人的位姿

Mapping:在给定机器人位姿的情况下，估计环境地图



## SLAM分类

![image-20230403151349653](https://nrwflqzr.oss-cn-beijing.aliyuncs.com/typora-img/image-20230403151349653.png)

## SLAM框架

Graph-based SLAM

-   Graph: 表示SLAM的过程
-   Node：机器人的位姿
-   Edeg：节点之间的空间约束关系

Filter-based SLAM

-   状态预测(State Prediction)
-   测量预测(,easurement Prediction)
-   进行测量(Measurement)
-   数据关联(Data Association)
-   状态更新&地图更新(State&Map Update)



## 激光SLAM

![image-20230403152743179](https://nrwflqzr.oss-cn-beijing.aliyuncs.com/typora-img/image-20230403152743179.png)

### 帧间匹配算法

ICP（Iterative Closest Point)

PI-ICP(Point-to-Line Iterative Closest Point)

NDT(Normal Distribution Transfomation)

CSM(Correlation Scan Match)

### 回环检测

Scan-to-Scan

Scan-to-Map

Map-to-Map 
