# Lab1
## Description

DOL(Distributed Operation Layer)是一个处理并行程序的开发环境。本次实验使用ubuntu14.04(32位)，安装SystemC和DOL。

## How to Install
1.安装一些必要的环境

    sudo apt-get install update
    sudo apt-get install ant
    sudo apt-get install openjdk-7-jdk

其中最后一个是java的开发环境。

2.下载DOL和SystemC的压缩包。使用wget命令。

    sudo wget [url]

下载后解压缩到同一个根目录下。

3.编译systemc

    cd systemc-2.3.1
    mkdir objdir
    cd objdir
    ../configure CXX=g++ --disable-async -updates
    sudo make install
    cd ..
    pwd

命令pwd是为了显示当前的绝对路径，这个路径等会要用到。

![path](https://cl.ly/1s0u203x2k3n/download/02.png)

4.编译dol
    
    cd ../dol
    vi build_zip.xml

将其中的<property name="system.inc"\>和<property name="system.lib"\>修改如下：

![change](https://cl.ly/181F1M001A0K/download/03.png)

这里用到了之前的绝对路径。

之后用ant编译：
    
    ant -f build_zip.xml all

编译成功后运行第一个例子

    cd build/bin/main
    ant -f runexample.xml -Dnumber=1

成功后结果如下：

![result](https://cl.ly/0R2k0G1B0R3O/download/01.png)

## Experimental experience

- 增加了linux开发的经验。
- 接触到新的领域，即并行处理的环境。