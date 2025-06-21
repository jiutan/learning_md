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

```
