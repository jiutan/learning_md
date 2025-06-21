# Linux python Code
## 1. 查看代码文件:[cat]
```c
    cat hello.py    // 查看hello.py文件的内容
    或者
    ./hello.py	    // 需升级权限，才能够直接运行。且需在内容开头加入：#!/程序位置(usr/bin/python3)
```
## 2. 查看程序在那：[whereis]
```c
    whereis python3 // 查看python3在哪个文件中 
```
## 3. 当文件权限不够时，无法直接查看文件（./文件）【使用 chmod】
```c
    chmod a+x 文件名	// 将文件名升级权限（由白变绿）
```

# Linux C++ Code
## 1. Shell中执行程序
```c
    g++ hello.cpp	// use g++ to compile cpp文件,生成 a.out可执行文件
    
    ./a.out		// 通过该命令，直接输出a.out文件
```
## 2. 使用CMakeList.txt编译C++文件
```c
    // 1.声明CMake文件：CMake版本最低是3.8
    cmake_minimum_required(VERSION 3.8)

    // 2.工程的配置：主要配置工程的名字
    project(<工程名字>)

    // 3.添加可执行executable文件：将cpp文件 编译 生成 该可执行文件
    add_executable(<待生成的可执行文件的名字> <待编译的cpp文件名字>)

```
4. 使用`cmake <txt所在路径>`：将CMakeList.txt文件转换成 MakeFile文件（一般是**cmake .**）
5. 再使用`make`指令：生成可执行文件
6. 最后，再运行该可执行文件，使用`./<可执行文件名>`来运行该可执行文件。