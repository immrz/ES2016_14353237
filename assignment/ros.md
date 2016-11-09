# Lab5

ROS(Robot Operating System)集成了一系列用于机器人开发的软件和框架。

本次试验的内容就是安装ROS以及一套SLAM(同步定位与建图)算法——cartographer。

参照网上的教程，很容易就可以完成ROS的安装。但安装cartographer时遇到一些小问题，ceres solver下载不了。可能国外教程的链接失效了，所以我百度了一下，换了国内的一个安装教程。

也很简单，首先在github上下载ceres solver。

    git clone https://github.com/hitcm/ceres-solver-1.11.0.git

顺便查了一下这个ceres solver，原来是google的一个算法库，用来解决大型复杂非线性最小二乘问题。我想，cartographer作为一个定位和建模算法，肯定需要进行数据的拟合。所以，可能就是以ceres solver为基础的吧。这学期的人工智能课程也用到了最小二乘的知识，这也启发了我，数值分析的算法对于数据分析真的很重要。

从github下载好之后，做如下操作：

    mkdir build
    cd build
    cmake ..
    make
    sudo make install

这样，ceres solver就安装好了。

接着，安装cartographer，仍是先从github下载，然后make。

    git clone https://github.com/hitcm/cartographer.git
    (安装若干dependencies...)
    mkdir build
    cd build
    cmake .. -G Ninja
    ninja
    ninja test (这一步test所有测试都通过了)
    sudo ninja install

最后，在~目录下新建catkin_ws文件夹，在里面新建src文件夹。然后下载cartographer_ros。

    mkdir -p ~/catkin_ws/src
    git clone https://github.com/hitcm/cartographer_ros.git
    cd ..
    catkin_make

安装成功。