# ROS2学习
## 一、ROS2安装与rosdep环境的配置
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


## 二、环境变量的妙用
### 1.配置环境变量
注意：每次**打开新的工程 或 编译工程时**，都要进行环境变量的配置与检查
- 环境配置文件：`.bashrc`文件(在home文件夹下，被隐藏了)
- 当更改环境配置文件后，要*重新打开终端*。（因为可能该终端已经运行过该文件了）

### 2.想修改打印出来的 基础提示内容（如：行号，时间辍等）
1. 在shell命令中，输入：
```c
	// 将 输出内容的前缀 改为： <运行命令的 行数>:<输出内容>
	export RCUTILS_CONSOLE_OUTPUT_FORMAT=[{function_name}:{line_number}]:{message}
```

## 三、Shell命令代码
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
#### printenv 与 grep: 打印环境变量 中查找的内容
**printenv 是打印环境变量内的信息**
```c
    printenv | grep <需要查找的内容部分>		// 打印出环境变量 含查找部分的 内容
```
### 2.找出文件【export】
```c

    export <文件名>

```

### 3.ROS2 命令
#### run：运行命令[通过环境变量查找文件]
```c
    ros2 run <功能包的名字> <可执行文件的名字>          // 本质：就是 运行可执行文件
```
注意：ros2 run 是通过**环境变量（AMENT_PREFIX_PATH=/opt/ros/humble）来查找功能包以及可执行文件的**（不是在当前目录）
查找文件步骤：
（1）通过环境变量：AMENT_PREFIX_PATH
（2）查找：lib/package_name(功能包名)/exacuteable_name(可执行文件名)
#### source：添加 环境变量

#### node list：查看 当前节点列表
```c
    ros2 node list		// 查看当前 正在运行 的节点
```


## 四、节点node学习
### 1.基础内容
1. **python**的node初始化
```python
import rclpy			    # 引入 rclpy库
from rclpy.node import Node         # 从 rclpy库中的node类 导入到 Node中

# 定义 main函数：ROS2节点的基础步骤（python）
def main():
    rclpy.init()                    # 1.初始化工作，分配资源
    
    node = Node('pyhton_node')      # 2.创建节点的实例对象（创建一个节点名字python_node，将 Node类的 python_node这个实例（对象） 赋值给了 node变量）
    
    # 在这里 插入功能语句
    
    rclpy.spin(node)                # 3.循环的运行检测节点，直到节点关闭为止（只要不打断，不会打断）
    
    rclpy.shutdown()                # 4.关闭并清理节点（推出后，需清理节点资源）

# 定义模块：如果该模块是主模块（__main__），则运行 main()函数. 用于判断当前脚本是直接运行还是作为模块被导入到其他脚本中执行
if __name__=='__main__':            
    main()
```
### 2.日志打印【 node.get_logger() 】
#### 参数

#### 程序
- python程序：(在 `rclpy.spin(node)`前执行)
```pythoin
    
    node.get_logger().info('Hello World!')  # 获取并使用get_logger日志管理模块，打印info级别的提示

```
#### 输出
输出内容：`[级别] [时间辍] [节点名字] : [打印内容]`
  - 级别：（1）info：普通级别；（2）warn：警告级别
  - 时间辍：从1970年至今的 秒数






# ROS2常见的错误
## package '...' not found：可能没有配置环境变量 或 环境变量下没有该功能包
解决办法：
（1）查看环境变量（AMENT_PREFIX_PATH）下的文件有没有该功能包
（2）若没有，则添加功能包 或者 使用source添加环境变量
