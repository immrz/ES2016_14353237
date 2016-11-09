# DeadLock
## 对synchronized的解释
用关键字'synchronized'修饰的方法或代码块，都是上了锁的。当它们被某个线程执行时，具备以下性质:

1. 这个方法或代码块无法同时被其它线程访问。
2. 同一个对象的其它用synchronized修饰的方法、代码块，也无法被其它线程访问。

## 对代码的理解，产生死锁的原因

A类和B类都有两个synchronized方法，并且互相调用。

程序创建了A类和B类的对象a,b，以及两个线程。线程一，调用A类的方法a.methodA(b)，间接调用了B类的方法b.last()。线程二，调用B类的方法b.methodB(a)，间接调用了A类的方法a.last()。此时，如果线程一和线程二各自占据了a和b的锁，那么程序就会出现死锁现象。

## 对代码的修改

原本产生死锁是一个概率事件，因为不确定什么时候正好线程一和线程二各自占有了a和b的锁。所以我修改了原来的代码，如下:

    synchronized void methodA(B b) {
        try {Thread.sleep(1000);} catch (Exception e) {e.printStackTrace();}
        b.last();
    }

    synchronized void methodB(A a) {
        try {Thread.sleep(1000);} catch (Exception e) {e.printStackTrace();}
        a.last();
    }

这样就保证了：线程一占有了a的锁，休眠1秒，这段时间里线程二占有了b的锁，二者互相等待。于是只要运行一次就会死锁。如下所示:

![deadlock](https://cl.ly/2s3Y3w1O2829/download/deadlock.png)

## 死锁的四个条件

1. 互斥条件：一个资源每次只能被一个进程使用。
2. 请求与保持条件：一个进程因请求资源而阻塞时，对已获得的资源保持不放。
3. 不剥夺条件:进程已获得的资源，在未使用完之前，不能强行剥夺。
4. 循环等待条件:若干进程之间形成一种头尾相接的循环等待资源关系。