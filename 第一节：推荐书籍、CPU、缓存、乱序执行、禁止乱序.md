# 相关书籍推荐

读书的原则：不求甚解，观其大略

你如果进到庐山里头，二话不说，蹲下头来，弯下腰，就对着某棵树某棵小草猛研究而不是说先把庐山的整体脉络跟那研究清楚了，那么你的学习方法肯定效率巨低而且特别痛苦，最重要的还是慢慢地还打击你的积极性，说我的学习怎么那么不happy啊，怎么那么特没劲那，因为你的学习方法错了，大体读明白，先拿来用，用着用着，很多道理你就明白了

▪《编码：隐匿在计算机软硬件背后的语言》---入门

《计算机是怎么跑起来的？》--写的一般    


▪《深入理解计算机系统》--比较难

▪语言：C JAVA 《C程序设计语言》(K&R)  《C Primer Plus》---这两本程序员必读

▪ 数据结构与算法： -- 毕生的学习 leetCode---程序员必读

    –《Java数据结构与算法》(只有PDF，不更新了)  《算法》
    
    –《算法导论》《计算机程序设计艺术》--难

▪操作系统：Linux内核源码解析  Linux内核设计与实现 30天自制操作系统
    
    大学课程难，课程内容是：怎么做一个操作系统

▪网络：机工《TCP/IP详解》卷一 翻译一般--强烈推荐

▪编译原理：机工 龙书--《编译原理》 《编程语言实现模式》

▪数据库：SQLite源码  Derby--JDK自带数据库

# 硬件基础知识

关于底层的细节：

适度打开

很多情况下保持黑箱即可，因为打开这个黑箱，你就会发现黑箱会变成黑洞，吞噬你所有的精力和时间，有可能使你偏离原来的方向，陷入到不必要的细节中无法自拔。

### CPU的制作过程

![image](https://raw.githubusercontent.com/musictaste/os/master/image/101.png)

Intel cpu的制作过程

https://haokan.baidu.com/v?vid=11928468945249380709&pd=bjh&fr=bjhauthor&type=video


CPU是如何制作的（文字描述）

https://www.sohu.com/a/255397866_468626

### CPU的原理（需要了解）



计算机需要解决的最根本问题：如何代表数字

晶体管是如何工作的：

https://haokan.baidu.com/v?vid=16026741635006191272&pd=bjh&fr=bjhauthor&type=video

晶体管的工作原理：

https://www.bilibili.com/video/av47388949?p=2

![image](https://raw.githubusercontent.com/musictaste/os/master/image/102.png)

    计算机中增加了机械部件----运十原理

    cpu64位，是cpu一次能读多少位数据
    
    cpu多少位，跟总线的位数没有密切关系，如果总线不到64根，cpu多次读数据
    
    
    让计算机看懂计算：01000010 + 00101100 ...
        cpu的针脚通电来代表0/1
        
    手工输入：纸带计算机
        bug的来源，有一个小孔被小虫子堵住了
    
    助记符：01000010  - mov  sub
        汇编语言
        
    高级语言 -> 编译器 -> 机器语言
    
    编译：编译完的代码放到内存中就是机器码，cpu可以直接执行
    解释：java的二进制码，交给JVM，解释为机器码，cpu执行

### 汇编语言（机器语言）的执行过程

汇编语言的本质：机器语言的助记符 其实它就是机器语言

计算机通电 -> CPU读取内存中程序（电信号输入）

->时钟发生器不断震荡通断电 ->推动CPU内部一步一步执行

（执行多少步取决于指令需要的时钟周期）

->计算完成->写回（电信号）->写给显卡输出（sout，或者图形）

        时钟发生器震荡一次，CPU执行一步
        时钟发生器，现在是Ghz，几十亿次/秒
        

### 量子计算机

量子比特，同时表示1 0

薛定谔的猫

![image](https://raw.githubusercontent.com/musictaste/os/master/image/104.png)

![image](https://raw.githubusercontent.com/musictaste/os/master/image/105.png)


---
# java相关的硬件知识

![image](https://raw.githubusercontent.com/musictaste/os/master/image/103.png)

    最核心：CPU+内存
        
    上面的硬件插在主板上

    问题1：内存中的东西怎么发给显卡的
    cpu发布指令  DMA机制（Direct Memory Access，直接存储器访问）
    从内存中将数据通过总线发送到显卡，显卡中有缓冲区
    每一个小缓冲区对应是显示器的一个像素
    显示器有刷新率，40HZ，144HZ，不停的从显卡里读数据到屏幕
    
    问题2:java的bytecode(二进制码)
        bytecode是java的汇编语言
        cpu机器码 和 java代码 的中间码
        二进制码，通过不同系统的jvm，解释编译为不同操作的机器码
        
    问题3：AI芯片
        相比CPU更适合做AI计算

### CPU的基本组成

    PC -> Program Counter 程序计数器 （记录当前指令地址）
    
    Registers 寄存器 -> 暂时存储CPU计算需要用到的数据
        上学的时候有16个寄存器，现在的计算机，寄存器很多，具体多少需要查
        cpu64位，是说寄存器可以存储64位的数据
        registers和ALU之间通信也是64位的
        
    
    ALU -> Arithmetic & Logic Unit 运算单元
    
    CU -> Control Unit 控制单元
    
    MMU -> Memory Management Unit 内存管理单元
    
    cache

### 缓存cache

![image](https://raw.githubusercontent.com/musictaste/os/master/image/106.png)
    
    超线程
        线程切换
        8核16线程，可以同时执行8个线程，因为ALU只有8个，CPU可以读取16个线程，但是同时并行执行的8个线程

![image](https://raw.githubusercontent.com/musictaste/os/master/image/107.png)
![image](https://raw.githubusercontent.com/musictaste/os/master/image/108.png)
![image](https://raw.githubusercontent.com/musictaste/os/master/image/109.png)

    存储器的层次结构
        高速缓存


![image](https://raw.githubusercontent.com/musictaste/os/master/image/111.png)

    一致性协议：https://www.cnblogs.com/z00377750/p/9180644.html
        总线锁
        缓存锁：MESI  MSI  MOSI   Synapse  FireFly   Dragon

    按块读取
    程序局部性原理，可以提高效率
    充分发挥总线、CPU针脚等一次性读取更多数据的能力
    
![image](https://raw.githubusercontent.com/musictaste/os/master/image/110.png)    
    
    缓存行：
        缓存行越大，局部性空间效率越高，但读取时间慢
        缓存行越小，局部性空间效率越低，但读取时间快

        取一个折中值，目前多用：
        64字节
        
    下面有程序可以验证
        原先的代码作废，下面是新的代码
        在我本机运行结果差不多，别人机器上是1：3

```
package com.mashibing.juc.c_028_FalseSharing;

public class T03_CacheLinePadding {

    public static volatile long[] arr = new long[2];

    public static void main(String[] args) throws Exception {
        Thread t1 = new Thread(()->{
            for (long i = 0; i < 10_0000_0000L; i++) {
                arr[0] = i;
            }
        });

        Thread t2 = new Thread(()->{
            for (long i = 0; i < 10_0000_0000L; i++) {
                arr[1] = i;
            }
        });

        final long start = System.nanoTime();
        t1.start();
        t2.start();
        t1.join();
        t2.join();
        System.out.println((System.nanoTime() - start)/100_0000);
    }
}
```


```
package com.mashibing.juc.c_028_FalseSharing;

public class T04_CacheLinePadding {

    public static volatile long[] arr = new long[16];

    public static void main(String[] args) throws Exception {
        Thread t1 = new Thread(()->{
            for (long i = 0; i < 10000_0000L; i++) {
                arr[0] = i;
            }
        });

        Thread t2 = new Thread(()->{
            for (long i = 0; i < 10000_0000L; i++) {
                arr[8] = i;
            }
        });

        final long start = System.nanoTime();
        t1.start();
        t2.start();
        t1.join();
        t2.join();
        System.out.println((System.nanoTime() - start)/100_0000);
    }
}
```

![image](https://raw.githubusercontent.com/musictaste/os/master/image/112.png) 

    缓存行对齐：对于有些特别敏感的数字，会存在线程高竞争的访问，为了保证不发生伪共享，可以使用缓存行对齐的编程方式
        应用：disruptor--cursor游标

    JDK7中，很多采用long padding提高效率
    
==JDK8，加入了@Contended注解（实验）需要加上：JVM -XX:-RestrictContended, 会根据底层的CPU自动缓存行对齐==
            
采用disruptor的p1,p2,p3,p4,p5,p6,p7这种编程方式，可能只对于intel CPU管用
        

```
public class T05_contened {
    @Contended
    volatile long x;
    @Contended
    volatile long y;

    public static void main(String[] args) throws InterruptedException {
        T05_contened t  = new T05_contened();
        Thread t1 = new Thread(()->{
            for (long i = 0; i < 1_0000_0000; i++) {
                t.x = i;
            }
        });

        Thread t2 = new Thread(()->{
            for (long i = 0; i < 1_0000_0000; i++) {
                t.x = i;
            }
        });

        final long start = System.nanoTime();
        t1.start();
        t2.start();
        t1.join();
        t2.join();
        System.out.println((System.nanoTime() - start)/100_0000);
    }

}
```



### 乱序执行

![image](https://raw.githubusercontent.com/musictaste/os/master/image/202.png) 


乱序执行的证明：

国外博客的位置：

https://preshing.com/20120515/memory-reordering-caught-in-the-act/

```
程序：jvm/jmm/Disorder.java
public class T04_Disorder {
    private static int x = 0, y = 0;
    private static int a = 0, b =0;

    public static void main(String[] args) throws InterruptedException {
        int i = 0;
        for(;;) {
            i++;
            x = 0; y = 0;
            a = 0; b = 0;
            Thread one = new Thread(new Runnable() {
                public void run() {
                    //由于线程one先启动，下面这句话让它等一等线程two. 读着可根据自己电脑的实际性能适当调整等待时间.
                    //shortWait(100000);
                    a = 1;
                    x = b;
                }
            });

            Thread other = new Thread(new Runnable() {
                public void run() {
                    b = 1;
                    y = a;
                }
            });
            one.start();other.start();
            one.join();other.join();
            String result = "第" + i + "次 (" + x + "," + y + "）";
            if(x == 0 && y == 0) {
                System.err.println(result);
                break;
            } else {
                //System.out.println(result);
            }
        }
    }


    public static void shortWait(long interval){
        long start = System.nanoTime();
        long end;
        do{
            end = System.nanoTime();
        }while(start + interval >= end);
    }
}

执行结果：第2728842次(0,0)
第113299次(0,0)
```

乱序执行可能会产生问题：

DCL单例为什么要加volatile？

![image](https://raw.githubusercontent.com/musictaste/os/master/image/203.png)
![image](https://raw.githubusercontent.com/musictaste/os/master/image/204.png)

### 禁止乱序

![image](https://raw.githubusercontent.com/musictaste/os/master/image/205.png)
![image](https://raw.githubusercontent.com/musictaste/os/master/image/206.png)

==**CPU层面：Intel -> 原语(mfence(mixed) lfence sfence) 或者锁总线**==

==volatile的汇编命令：lock addl 0x0(加0)==

==synchronidez的汇编命令：lock cmpxchg==


![image](https://raw.githubusercontent.com/musictaste/os/master/image/207.png)
![image](https://raw.githubusercontent.com/musictaste/os/master/image/208.png)
![image](https://raw.githubusercontent.com/musictaste/os/master/image/209.png)

==JVM层级：8个hanppens-before原则 4个内存屏障 （LL LS SL SS）、as-if-serial==

volatile的jvm实现：使用内存屏障，实现比较保守

volatile修饰对象，是锁定这个对象，不是内存地址

hanppens-before原则(不需要背)，JLS中有，第17章4.5节

==as-if-serial : 不管硬件什么顺序，单线程执行的结果不变，看上去像是serial==

==面试题：有一个系统，有很多请求，使用线程池，想要请求顺序执行，应该怎么做==？

    使用singleThreadPool，里面有队列

### 合并写（不重要）

Write Combining Buffer

一般是4个字节

由于ALU速度太快，所以在写入L1的同时，写入一个WC Buffer，满了之后，再直接更新到L2

![image](https://raw.githubusercontent.com/musictaste/os/master/image/210.png)


```
public final class WriteCombining {

    private static final int ITERATIONS = Integer.MAX_VALUE;
    private static final int ITEMS = 1 << 24;
    private static final int MASK = ITEMS - 1;

    private static final byte[] arrayA = new byte[ITEMS];
    private static final byte[] arrayB = new byte[ITEMS];
    private static final byte[] arrayC = new byte[ITEMS];
    private static final byte[] arrayD = new byte[ITEMS];
    private static final byte[] arrayE = new byte[ITEMS];
    private static final byte[] arrayF = new byte[ITEMS];

    public static void main(final String[] args) {

        for (int i = 1; i <= 3; i++) {
            System.out.println(i + " SingleLoop duration (ns) = " + runCaseOne());
            System.out.println(i + " SplitLoop  duration (ns) = " + runCaseTwo());
        }
    }

    public static long runCaseOne() {
        long start = System.nanoTime();
        int i = ITERATIONS;

        while (--i != 0) {
            int slot = i & MASK;
            byte b = (byte) i;
            arrayA[slot] = b;
            arrayB[slot] = b;
            arrayC[slot] = b;
            arrayD[slot] = b;
            arrayE[slot] = b;
            arrayF[slot] = b;
        }
        return System.nanoTime() - start;
    }

    public static long runCaseTwo() {
        long start = System.nanoTime();
        int i = ITERATIONS;
        while (--i != 0) {
            int slot = i & MASK;
            byte b = (byte) i;
            arrayA[slot] = b;
            arrayB[slot] = b;
            arrayC[slot] = b;
        }
        i = ITERATIONS;
        while (--i != 0) {
            int slot = i & MASK;
            byte b = (byte) i;
            arrayD[slot] = b;
            arrayE[slot] = b;
            arrayF[slot] = b;
        }
        return System.nanoTime() - start;
    }
}
```


### NUMA

![image](https://raw.githubusercontent.com/musictaste/os/master/image/211.png)

==UMA:同一内存访问    多个cpu通过总线直接访问内存==

==Non Uniform Memory Access：非同一内存访问（就近访问原则），对于自己主板插槽上的内存具有优先访问权==

ZGC - NUMA aware ,分配内存会优先分配该线程所在CPU的最近内存

