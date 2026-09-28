# Gazebo 学习

### 1. Gazebo介绍与安装：

#### 介绍：

Gazebo 是一个**集成了物理引擎、渲染引擎、传感器模型和通信接口的完整仿真平台**。

它内部确实有一个物理引擎（负责算重力、碰撞、浮力），但同时它还有：

- **渲染引擎**：负责显示三维画面（虽然比较简陋）。
- **传感器模型**：模拟摄像头、激光雷达（LiDAR）、IMU 等，并输出逼真的数据流。
- **插件系统**：允许你编写代码去控制模型，或者给模型添加新功能（比如水动力学）。

所以，Gazebo 不是简单的物理计算器，它是一个可以让你搭建一个完整虚拟世界（包含机器人和环境）的软件。

#### 安装：（通过 ROS2 安装，需要翻墙）

```shell
sudo apt update
sudo apt install ros-jazzy-ros-gz

source /opt/ros/jazzy/setup.bash

# 检查 Gazebo 版本，应显示 8.x.x (Harmonic)
gz sim --versions

# 检查 ROS 2 桥接包是否已安装
ros2 pkg list | grep ros_gz

# 设置 GZ_VERSION环境变量 为 harmonic
export GZ_VERSION=harmonic
```

#### 运行 测试

```shell
# 运行简单的官方案例
gz sim shapes.sdf
```

# VRX 学习

## VRX仿真平台（海洋）

### 1. VRX 下载、安装、运行

- 作用：给 Gazebo 加入海洋环境

- 下载：

  ```shell
  # 进入 vrx_ws 工作空间 安装与下载
  mkdir ~/Project/vrx_ws/src
  cd ~/Project/vrx_ws/src
  
  # 下载
  git clone https://gitcode.com/gh_mirrors/vr/vrx
  
  # 安装
  ## 回到工作空间根目录
  cd ~/Project/vrx_ws
  ## 安装依赖并编译
  rosdep install --from-paths src --ignore-src -r -y
  colcon build --symlink-install
  ```

- 运行：

  ```shell
  # 配置环境变量（每次打开新终端都要 source 一下，或者写进 ~/.bashrc）
  source /opt/ros/jazzy/setup.bash
  
  # 回到工作空间根目录
  cd ~/Project/vrx_ws
  source install/setup.bash
  ## 或者
  source ~/Project/vrx_ws/install/setup.bash
  
  # 运行
  ros2 launch vrx_gz competition.launch.py world:=sydney_regatta
  ```
  

### 2. 改变环境

#### （1）加入波浪

```shell
gz topic -t /vrx/wavefield/parameters -m gz.msgs.Param -p 'params:{key:"gain",value:{type:DOUBLE,double_value:2.0}},params:{key:"period",value:{type:DOUBLE,double_value:4.0}}'
```

- `gain`：波浪的增益/高度比例
- `period`：波浪周期（单位秒，数值越小浪越急促）



## VRX 使用

### 1. Topic话题

- 查看话题：`ros2 topic list`
  - **传感器数据（Sensors）**：如 GPS、IMU、双目/单目相机、激光雷达等
  - **推进器控制（Actuators）**：用于控制无人船两舷推进器的推力大小及转向角度。

#### （1）传感器数据（Sensors）

- 查看 GPS 定位：

  ```shell
  ros2 topic echo /wamv/sensors/gps/gps/fix
  ```

- 查看 IMU 姿态/加速度：

  ```shell
  ros2 topic echo /wamv/sensors/imu/imu/data
  ```

#### （2）推力 话题（thrusters）

用于 发布 推力，控制船运动

##### 话题

- 推力：`/wamv/thrusters/.../thrust`
- 角度转向：`/wamv/thrusters/.../pos`

##### 发布：

- 发布消息：`ros topic pub 话题`

  ```shell
  # 左推进器
  ros2 topic pub /wamv/thrusters/left/thrust std_msgs/msg/Float64 "{data: 50.0}"
  
  # 右推进器
  ros2 topic pub /wamv/thrusters/right/thrust std_msgs/msg/Float64 "{data: 50.0}"
  ```

- **消息接口**：`std_msgs/msg/Float64`

  - `std_msgs`：基础功能包名称，存放了 ROS 官方定义的一系列“最基础、最通用的数据类型”（比如整数、浮点数、字符串、布尔值等）
  - `msg`：话题消息（Message），用于节点之间单向发布/订阅数据。
  - `Float64`：具体的类型名称，指 64 位浮点数（即双精度浮点数 double）

