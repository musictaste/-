

### 启动过程（不重要）

图片213

《30天自制操作系统》

BIOS：英文全称

UEFI：英文全称，升级版

通电 -> bios uefi 工作 -> 自检 -> 到硬盘固定位置加载bootloader -> 读取可配置信息 -> CMOS

bootloaer：引导程序，在硬盘上的位置也是固定的，在硬盘的第一个扇区上（Master Boot Record）

CLH病毒

CMOS：英文全称，互补氧化半导体
    
    配置信息在CMOS上，开机密码也在CMOS上，主板上有电池给CMOS供电
    
    0x7c00，操作系统启动的位置
    

----

## OS

图片214

鸿蒙harmony

### 内核分类

图片215

==聊操作系统，是指linux系统==

推荐书：《linux内核设计与实现》

图片216

图片217  218

宏内核 - PC phone

    都在一块内存
    访问效率高

微内核 - 弹性部署 5G IoT

    核心在一个内存上，其他不在
    灵活、可插拔
    弹性部署
    万物互联
    物联网
    跟windows不是一个概念
    

外核 - 科研 实验中 为应用定制操作系统 (阿里的多租户 request-based GC JVM)

图片219

VMM

图片220


### 用户态与内核态

dos只能跑一个程序，程序自己跟硬盘、网卡、显示器打交道；病毒的天堂

cpu分不同的指令级别

cpu-CPL->0 1 2 3

linux只使用了0和3

linux内核跑在ring 0级， 用户程序跑在ring 3，对于系统的关键访问，需要经过kernel的同意，保证系统健壮性

内核执行的操作 - > 200多个系统调用 sendfile read write pthread fork 

JVM -> 站在OS老大的角度，就是个普通程序

### 进程 线程 纤程 中断

![image](https://raw.githubusercontent.com/musictaste/os/master/image/201.png)

面试高频：进程和线程有什么区别？

答案：进程就是一个程序运行起来的状态，线程是一个进程中的不同的执行路径。专业：进程是OS分配资源的基本单位，线程是执行调度的基本单位。分配资源最重要的是：独立的内存空间，线程调度执行（线程共享进程的内存空间，没有自己独立的内存空间）

面试题：线程和纤程的区别：

纤程(协程)：用户态的线程，线程中的线程，切换和调度不需要经过OS

优势：1：占有资源很少 OS : 线程1M Fiber：4K 2：切换比较简单 3：启动数量多，启动很多个10W+

目前2020 3 22支持内置纤程的语言：Kotlin Scala Go Python(lib)... Java? （open jdk : loom）

线程的切换发生在内核空间，切换比较重



### Java中对于纤程的支持：没有内置，盼望内置

利用Quaser库（不成熟）

纤程的运行，需要设置javaagent:（讲object的内存大小的时候，提到了agent代理）


```
工程：HelloFiber

<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
​
    <groupId>mashibing.com</groupId>
    <artifactId>HelloFiber</artifactId>
    <version>1.0-SNAPSHOT</version>
​
    <dependencies>
        <!-- https://mvnrepository.com/artifact/co.paralleluniverse/quasar-core -->
        <dependency>
            <groupId>co.paralleluniverse</groupId>
            <artifactId>quasar-core</artifactId>
            <version>0.8.0</version>
        </dependency>
    </dependencies>
​
</project>
```


```
import co.paralleluniverse.fibers.Fiber;
import co.paralleluniverse.fibers.SuspendExecution;
import co.paralleluniverse.strands.SuspendableRunnable;
​
public class HelloFiber {
​
    public static void main(String[] args) throws  Exception {
        long start = System.currentTimeMillis();
        Runnable r = new Runnable() {
            @Override
            public void run() {
                calc();
            }
        };
​
        int size = 10000;
​
        Thread[] threads = new Thread[size];
        for (int i = 0; i < threads.length; i++) {
            threads[i] = new Thread(r);
        }
​
        for (int i = 0; i < threads.length; i++) {
            threads[i].start();
        }
​
        for (int i = 0; i < threads.length; i++) {
            threads[i].join();
        }
​
        long end = System.currentTimeMillis();
        System.out.println(end - start);
​
​
    }
​
    static void calc() {
        int result = 0;
        for (int m = 0; m < 10000; m++) {
            for (int i = 0; i < 200; i++) result += i;
​
        }
    }
}
运行结果：
    6000ms左右
```


```
import co.paralleluniverse.fibers.Fiber;
import co.paralleluniverse.fibers.SuspendExecution;
import co.paralleluniverse.strands.SuspendableRunnable;
​
public class HelloFiber2 {
​
    public static void main(String[] args) throws  Exception {
        long start = System.currentTimeMillis();
​
​
        int size = 10000;
​
        Fiber<Void>[] fibers = new Fiber[size];
​
        for (int i = 0; i < fibers.length; i++) {
            fibers[i] = new Fiber<Void>(new SuspendableRunnable() {
                public void run() throws SuspendExecution, InterruptedException {
                    calc();
                }
            });
        }
​
        for (int i = 0; i < fibers.length; i++) {
            fibers[i].start();
        }
​
        for (int i = 0; i < fibers.length; i++) {
            fibers[i].join();
        }
​
        long end = System.currentTimeMillis();
        System.out.println(end - start);
​
​
    }
​
    static void calc() {
        int result = 0;
        for (int m = 0; m < 10000; m++) {
            for (int i = 0; i < 200; i++) result += i;
​
        }
    }
}
运行结果：
    1500ms左右
```

作业：目前是10000个Fiber -> 1个JVM线程，想办法提高效率，10000Fiber -> 10份 -> 10Threads

### 纤程的应用场景

纤程 vs 线程池：很短的计算任务，不需要和内核打交道，并发量高！

### 僵尸进程


```
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <string.h>
#include <assert.h>
#include <sys/types.h>
​
int main() {
        pid_t pid = fork();
​
        if (0 == pid) {
                printf("child id is %d\n", getpid());
                printf("parent id is %d\n", getppid());
        } else {
                while(1) {}
        }
}
```

### 孤儿进程


```
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <string.h>
#include <assert.h>
#include <sys/types.h>
​
int main() {
        pid_t pid = fork();
​
        if (0 == pid) {
                printf("child ppid is %d\n", getppid());
                sleep(10);
                printf("parent ppid is %d\n", getppid());
        } else {
                printf("parent id is %d\n", getpid());
                sleep(5);
                exit(0);
        }
}
```

---

## 进程调度

2.6采用CFS调度策略：Completely Fair Scheduler

按优先级分配时间片的比例，记录每个进程的执行时间，如果有一个进程执行时间不到他应该分配的比例，优先执行

默认调度策略：

实时 （急诊） 优先级分高低 - FIFO (First In First Out)，优先级一样 - RR（Round Robin）
普通： CFS

### 中断

硬件跟操作系统内核打交道的一种机制

软中断（80中断） ==  系统调用

系统调用：int 0x80 或者 sysenter原语

通过ax寄存器填入调用号

参数通过bx cx dx si di传入内核

返回值通过ax返回

 

java读网络 – jvm read() – c库read() - > 

内核空间 -> system_call() （系统调用处理程序）

-> sys_read()