# Chapter 1 - ROS简介

## 本章节将会介绍ROS的基本概念、ROS的历史以及ROS的特点，让大家对ROS产生基本的认识

![](https://sychaichangkun.gitbooks.io/ros-tutorial-icourse163/content/pics/happy-bot.jpeg)

### 1.1 什么是ROS
随着技术进步，机器人产业分工开始走向细致化、多层次化，如今的电机、底盘、激光雷达、摄像头、机械臂等等元器件都有不同厂家专门生产。而各个部件的集成就需要一个统一的软件平台，在机器人领域，这个平台就是机器人操作系统ROS。ROS是一个适用于机器人编程的框架，这个框架把原本松散的零部件耦合在了一起，为他们提供了通信架构。ROS虽然叫做操作系统，但并非**Windows**、**Mac**那样通常意义的操作系统，它只是连接了操作系统和用户开发的ROS应用程序，所以它也算是一个中间件，基于ROS的应用程序之间建立起了沟通的桥梁，所以也是运行在Linux上的运行时环境，在这个环境上，机器人的感知、决策、控制算法可以更好的组织和运行。

ROS 运行时的“蓝图”是一种基于ROS通信基础结构的松耦合点对点进程网络。ROS实现了几种不同的通信方式，包括基于同步RPC样式通信的服务（services）机制，基于异步流媒体数据的话题（topics）机制以及用于数据存储的参数服务器（Parameter Server）。

![avatar](https://www.ros.org/wp-content/uploads/2013/12/ros_equation.png)

![](https://www.researchgate.net/profile/Ms-Achmad/publication/319566597/figure/fig2/AS:667605232787467@1536180899683/Nodes-communication-model-in-the-ROS-environment-Fig-5-describes-the-proposed-ROS.png)

[![RaVTaD.jpg](https://z3.ax1x.com/2021/06/29/RaVTaD.jpg)](https://imgtu.com/i/RaVTaD)

![](https://image.slidesharecdn.com/rosintroduction-181204014417/95/ros-10-638.jpg?cb=1543887932)

![](https://www.ros.org/wp-content/uploads/2013/12/user_map.jpg)

### 1.2 ROS的特点
- 分布式 点对点</br>
ROS采用了分布式的框架，通过点对点的设计让机器人的进程可以分别运行，便于模块化的修改和定制，提高了系统的容错能力

-  多种语言支持</br>
ROS支持多种编程语言。C++、Pyhton和已经在ROS中实现编译，是目前应用最广的ROS开发语言

- 开源社区</br>
ROS具有一个庞大的社区ROS WIKI(http://wiki.ros.org/ )，这个网站将会始终伴随着你ROS开发，无论是查阅功能包的参数、搜索问题。当前使用ROS开发的软件包已经达到数千万个，相关的机器人已经多达上千款。此外，ROS遵从BSD协议，对个人和商业应用及修改完全免费。这也促进了ROS的流行


### 1.3 ROS的历史
ROS系统是起源于2007年斯坦福大学人工智能实验室的项目与机器人技术公司Willow Garage的个人机器人项目（Personal Robots Program）之间的合作，2008年之后就由Willow Garage来进行推动。随着PR2那些不可思议的表现，譬如叠衣服，插插座，做早饭，ROS也得到越来越多的关注。Willow Garage公司也表示希望借助开源的力量使PR2变成“全能”机器人。

![pr2-cooking.jpg](https://www.razorrobotics.com/images/pr2/pr2-cooking.jpg)

![28yYPe.png](https://z3.ax1x.com/2021/06/04/28yYPe.png)

</br></br></br>

# Chapter 2 - ROS与机械臂开发

## 本章节将会介绍ROS与机械臂开发相关的程序包，以及相关的软件架构

![](https://media.onlinecoursebay.com/2019/07/10020618/2389042_e263_3-750x405.jpg)

### 2.1 Moveit!是什么？

![](https://camo.githubusercontent.com/8dc96fd1c0547dcf77efe1b4fa579dd628bc4069b91cdb401b56da570064b115/68747470733a2f2f6d6f766569742e726f732e6f72672f6173736574732f6c6f676f2f6d6f766569745f6c6f676f2d626c61636b2e706e67)

MoveIt! 是ROS系统中集合了与移动操作相关的组件包的运动规划库。它包含了运动规划中所需要的大部分功能：

- (1)move_group: move_group是MoveIt!的核心部分，它的功能在于集成机器人的各独立模块并为用户提供一系列的动作指令和服务。其本身并不具备太多的功能，只完成各功能包和插件的集成。

- (2)场景规划（Planning Scene）: 通过场景规划，用户可以创建一个具体的工作环境或者加入障碍物。

- (3)运动规划（motion panning): 在MoveIt!中，运动规划器起的作用是实现运动规划算法，其以插件的方式通过ROS的pluginlib接口完成信息的通讯，根据需求可制作或选用不同的规划算法。

- (4)运动学（Kinematics）： 运动学算法是机械臂控制算法中的核心内容，其中包括正运动学算法和逆运动学算法，在MoveIt!中，运动学算法同样以插件的形式完成于ROS的集成，因此可根据实际需求，编写自己的运动学算法来控制机器人。

- (5)碰撞检测（collision checking）：  为避免机器人自身或者和环境发生干涉导致意外的发生，在进行运动规划时碰撞检测是必不可少的一部分，在MoveIt!中，采用FCL（Flexible  Collision Library）进行对象碰撞的运算。

- (6)开源运动规划库（open motion planning library）: OMPL是一个的开源的C++库，主要用于运动规划，其中包含了大量用于运动规划的先进算法。该库中的算法以采样规划算法为主，通过其可以实现不同目标点之间的路径规划。

  [![28cEp4.png](https://z3.ax1x.com/2021/06/04/28cEp4.png)](https://imgtu.com/i/28cEp4)



### 2.2 ROS机械臂开发软件架构
![avatar](https://pic4.zhimg.com/80/v2-951870aa51903e7e3afcd4f0fc1a6ef0_1440w.jpg?source=1940ef5c)
从软件架构图中可以很清楚的看到，机械臂的软件层主要由三个部分组成，从下到上依次为：硬件接口层、运动规划层和任务决策层。

### 2.2.1 硬件接口层
ROS Control是ROS提供的软件与硬件之间进行数据通信的中间件，它对硬件进行了抽象，统一了数据通信的接口，并通过插件的形式封装了一些常用的运动控制算法，为建立机器人软硬件模块之间的数据通路提供了便捷。

[![RaeRnx.png](https://z3.ax1x.com/2021/06/29/RaeRnx.png)](https://imgtu.com/i/RaeRnx)

### 2.2.2 运动规划层
运动规划层在机械臂的自主抓取中扮演了非常重要的角色。而对于运动规划本身来说，里面涉及了非常多的专业知识，比如运动学正逆解算、碰撞检测算法、3D环境感知、动作规划算法等，以上任何一个方面都需要我们长时间的积累才能理解清楚，而对于那些想立马上手机械臂的初学者来说，这简直就是一个灾难。幸运的是，ROS提供了强大且易用的MoveIt!包，它可以让你在较短的时间内实现仿真乃至实体机械臂的运动学规划演示。

- URDF：
  **move_group**需要机械臂的URDF文件来进行运动规划。URDF(Unified Robot Description  Format)，统一机器人描述格式，是一种特殊的xml格式，用来描述一个机器人.  在ROS中，urdf功能包包含一个urdf格式文件的C++解析器，这样，任何通过统一编码格式设计的机器人都可以通过该解析器得到一个可视化的模型。

![28256J.png](https://z3.ax1x.com/2021/06/04/28256J.png)

- 用户接口
用户可以使用C++、Python或者GUI来访问move_group。

[![286SIO.png](https://z3.ax1x.com/2021/06/04/286SIO.png)](https://imgtu.com/i/286SIO)

[![286CJe.png](https://z3.ax1x.com/2021/06/04/286CJe.png)](https://imgtu.com/i/286CJe)

- 运动规划结果：
  **move_group**节点最终将会根据上面的运动规划请求，生成一条运动轨迹。这条轨迹可以使机械臂移动到预想的目标位置。请注意：**move_group**输出的是一条轨迹，而不是路径。对于机械臂来说，路径是使末端执行器移动到目标位置的过程中，中间所经历的一系列独立的位置点。而轨迹则是在路径的基础上，通过加入速度、加速度约束以及时间参数来使机械臂运动的更加平滑。

[![28cEp4.png](https://z3.ax1x.com/2021/06/04/28cEp4.png)](https://imgtu.com/i/28cEp4)

### 2.2.3 **3D Perception**
简单来说，3D Perception使用插件来获取点云和深度图像数据，并据此生成OctoMap，为之后机械臂的碰撞检测提供基础。

![avatar](https://blog.pal-robotics.com/wp-content/uploads/2018/01/rviz_octomap_interact-ros-tiago-pal-robotics-moveit.png)

![](https://answers.ros.org/upfiles/15247497757466605.png)

### 2.2.4 **Planning Scene**

Planning Scene用来表示机械臂周围的外部世界并且保存机械臂自己本身的状态。它通过监听对应的Topic来获取关节状态信息、传感器信息。并可以根据传感器信息和用户的输入，生成机器人周围3D世界空间的表示。

![avatar](https://pic1.zhimg.com/80/v2-49e65c49c427b63fe20e70a220c84151_1440w.jpg?source=1940ef5c)

![](https://robotnik.eu/wp-content/uploads/2020/12/galeria-4.jpg)

### 2.2.5 **Collision Checking**
MoveIt!使用CollisionWorld对象进行碰撞检测，采用FCL(Flexible Collision Library)功能包。碰撞检测是运动规划中最耗时的运算，往往会占用90%左右的时间，为了减少计算量，可以通过设置ACM(Allowed Collision Matrix)来进行优化。
[![28WDZn.png](https://z3.ax1x.com/2021/06/04/28WDZn.png)](https://imgtu.com/i/28WDZn)

### 2.3 总结
[![Raerh4.png](https://z3.ax1x.com/2021/06/29/Raerh4.png)](https://imgtu.com/i/Raerh4)

</br></br></br>

# Chapter 3 - ROS Examples

## 本章节将介绍与ROS相关的实际案例，将让大家了解实际的使用ROS开发的机器人应用

[![RaZSZ8.jpg](https://z3.ax1x.com/2021/06/29/RaZSZ8.jpg)](https://imgtu.com/i/RaZSZ8)


### 3.1 PR2 Willow Garage

PR2（Personal Robot 2，个人机器人2代）是Willow Garage公司设计的机器人平台，其中数字2代表第二代机器人。PR2有两条手臂，每条手臂七个关节，手臂末端是一个可以张合的夹爪；PR2依靠底部的四个轮子移动，在头部、胸部、肘部、夹爪上分别安装有高分辨率摄像头、激光测距仪、惯性测量单元、触觉传感器等丰富的传感设备。在PR2的底部有两台八核电脑作为机器人各硬件的控制和通信中枢，并且都安装了Ubuntu和ROS系统。PR2和ROS有千丝万缕的关系，可以说ROS产生于PR2，也促成了PR2。ROS原本是Willow Garage为复杂的PR2机器人平台设计的软件框架，依靠强大的ROS，PR2可以独立完成多种复杂的任务，例如PR2可以自己开门、找到插头给自己充电、打开冰箱取出啤酒、打简单的台球等等。只不过PR2价格高昂，而且能力还达不到商业应用的要求，如今主要用于学术研究。
![](https://pic1.zhimg.com/80/v2-bf0b4735e30f39f2a2d31c7ef69fa430_1440w.jpg)

[![RaZVs0.jpg](https://z3.ax1x.com/2021/06/29/RaZVs0.jpg)](https://imgtu.com/i/RaZVs0)

[![RaZndU.jpg](https://z3.ax1x.com/2021/06/29/RaZndU.jpg)](https://imgtu.com/i/RaZndU)

### 3.2 Cocktail Bot 4.0 FZI
视频中的五款机器人组成一个柔性生产线，可以为客户提供定制化的饮料服务。
[![RaZQJJ.png](https://z3.ax1x.com/2021/06/29/RaZQJJ.png)](https://imgtu.com/i/RaZQJJ)

### 3.3 Universal Robot FZI

[![RaZNdO.png](https://z3.ax1x.com/2021/06/29/RaZNdO.png)](https://imgtu.com/i/RaZNdO)

### 3.4 功夫手(Kungfu Arm)  深圳星河智能科技
这是在2016年底深圳高交会上展示的项目，在该视频中，Kungfu Arm通过一系列复杂的动作，完成了泡制功夫茶的全部过程。该展示中的Kungfu Arm集成了视觉、触觉等多种传感器，不仅可以通过摄像头确定茶杯、茶球等物体的位置，还可以使用不同的力度抓取不同的物体。

[![RaZ0Wd.png](https://z3.ax1x.com/2021/06/29/RaZ0Wd.png)](https://imgtu.com/i/RaZ0Wd)

在视觉、触觉的基础上，该公司还为机器人增加了听觉。丰富的外界信息提高了整个系统的智能化，适合更多应用场景。

[![RaZyOP.png](https://z3.ax1x.com/2021/06/29/RaZyOP.png)](https://imgtu.com/i/RaZyOP)

这是2017年底深圳高交会展示的项目，改造了电机生产流水线中的一个重要工序——平衡。结合Kungfu Arm设计了一套自动化上下料工作单元，替代了工人的重复劳动，并且取得了较好的效果。

[![RaZhWj.png](https://z3.ax1x.com/2021/06/29/RaZhWj.png)](https://imgtu.com/i/RaZhWj)

</br></br></br>

# Chapter 4 - Who?

## 本章节将介绍ROS当前的主力使用人群

![](https://hackaday.com/wp-content/uploads/2014/01/ros.png?w=620)

### 4.1 ROS Wiki年度观察报告(2020)
[![Raem6I.png](https://z3.ax1x.com/2021/06/29/Raem6I.png)](https://imgtu.com/i/Raem6I)

### 4.2 Companies

![](https://pic4.zhimg.com/80/v2-ac8797da56eabbddf1676b518878b93b_1440w.jpg)

![](https://docplayer.net/docs-images/42/19797190/images/page_1.jpg)

![](https://developer-blogs.nvidia.com/wp-content/uploads/2021/05/ros-ros2-architecture.jpg)

![](https://bucket-download.slamtec.com/c5b5c30da8750dc83657f63c6d10d56bd05980f9/Banner-phone-en.png)

![](https://static.generation-robots.com/16394-large_default/intel-realsense-depth-camera-d455-with-tripod.jpg)

[![Rae3tg.png](https://z3.ax1x.com/2021/06/29/Rae3tg.png)](https://imgtu.com/i/Rae3tg)

[![Rae8hQ.png](https://z3.ax1x.com/2021/06/29/Rae8hQ.png)](https://imgtu.com/i/Rae8hQ)

[![Raetcn.png](https://z3.ax1x.com/2021/06/29/Raetcn.png)](https://imgtu.com/i/Raetcn)

[![Raean0.png](https://z3.ax1x.com/2021/06/29/Raean0.png)](https://imgtu.com/i/Raean0)
