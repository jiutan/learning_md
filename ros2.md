# ROS2学习
## 一、ROS2安装与环境配置
### 1.使用小鱼 ROS2 一件安装
1. 下载脚本并执行脚本（脚本运行完会自动删除）
```c
    wget http://fishros.com/install -O fishros && . fishros
```
2. 选择ROS相关： 1 ROS安装
3. 选择选择是否换源： 1 更换系统源再继续安装
4. 选择是否清理第三方源： 2 更换系统源并清理第三方源
5. 选择ROS版本： 1 humble版本
6. 选择具体版本： 1 桌面版
7. 若显示加入学习交流群，则说明安装成功
### 2.配置rosdep
1. 下载脚本并执行脚本（脚本运行完会自动删除）
```c
    wget http://fishros.com/install -O fishros && . fishros
```
2. 选择ROS相关： 3 配置rosdep
3. 等待安装
4. 检验配置是否成功：在终端输入`rosdepc update`
### 3.配置环境变量
注意：每次**打开新的工程 或 编译工程时**，都要进行环境变量的配置与检查
- 环境配置文件：`.bashrc`文件(在home文件夹下，被隐藏了)
- 当更改环境配置文件后，要*重新打开终端*。（因为可能该终端已经运行过该文件了）

## 二、Shell命令代码
### 1.输出打印指令【echo】【$的用途】
#### echo:输出与打印 内容
```c

    echo Hello_World		// 打印 Hello_World

```
#### $+<程序名>：终端会找到 $ 之后的字符 对应的环境变量后，用该环境变量替换 $ 字符
```c
    
    echo $ROS_VERSION		// 查看ROS的版本：ROS1 OR ROS2
    
    echo $ROS_DISTRO		// 查看ROS2当前程序的版本

    printenv                // 查看Linux下 所有的环境列表

```
### 2.ROS2 命令
#### run：运行命令[通过环境变量查找文件]
```c
    ros2 run <功能包的名字> <可执行文件的名字>          // 本质：就是 运行可执行文件
```
注意：ros2 run 是通过**环境变量（AMENT_PREFIX_PATH=/opt/ros/humble）来查找功能包以及可执行文件的**（不是在当前目录）
查找文件步骤：
（1）通过环境变量：AMENT_PREFIX_PATH
（2）查找：lib/package_name(功能包名)/exacuteable_name(可执行文件名)
#### source：添加 环境变量


# ROS2常见的错误
## package '...' not found：可能没有配置环境变量 或 环境变量下没有该功能包
解决办法：
（1）查看环境变量（AMENT_PREFIX_PATH）下的文件有没有该功能包
（2）若没有，则添加功能包 或者 使用source添加环境变量