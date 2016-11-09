# Lab3
## Description

- 使用DOL编译运行一些多进程的小样例(example1和example2)。
- 理解c和xml代码。
- 修改样例，得到不一样的结果。

## Steps

####1.修改example2减少一个平方模块。
example2.xml中定义了一个整型变量：

    <variable value="3" name="N"/>

接下来，又定义了1个generator进程，1个consumer进程，和N个square进程；以及N+1条线，2N+2个连接。

可以看出，N就是平方模块的个数。所以直接修改其value值即可。

####2.修改example1使得输出从二次方变为三次方。
这一题就不是修改xml了，因为xml已经确定了框架，是两个进程，用一条线连起来。

正确方法是修改square.c代码。原本，平方模块向输出端口写的是：

    i ＝ i * i;
    DOL_write((void*)PORT_OUT, &i, sizeof(float), p);

现在只需改为：
    
    i = i * i * i;
即可。

##Results
* example2修改后结果如下:

![result1](https://cl.ly/0D1g0T1L181N/download/snapshot4.png)

* example1修改后结果如下:

![result2](https://cl.ly/473g360q2g1C/download/snapshot5.png)

##Thoughts

对于怎样编写多进程程序有了一个初步的认识。居然可以用xml来定义各个进程间的关系，这真是我意想不到的。而且，对于重复的定义，可以用iterator(即循环)的方式，非常方便地做到，不需要一个个定义进程和连线。