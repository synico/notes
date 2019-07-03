
### JDK工具箱
#### jps
类似UNIX的ps命令，列出正在运行的虚拟机进程，并显示虚拟机执行主类名称以及这些进程的本地虚拟机唯一LVMID (Local Virtual Machine Identifier) 。

参数|含义
:--|:--
-q|只输出进程ID
-m|输出传入main方法的参数
-l|输出完整的包名，应用主类名
-v|输出jvm参数

#### jmap
* 用于生成堆转存储快照，一般称为heapdump或dump文件。
* 除此之外还可以设置-XX:+HeapDumpOnOutOfMemoryError参数，让虚拟机在OOM异常出现之后自动生成dump文件。或在Linux系统下通过kill -3命令发送进程退出信号。
* 在创建heap dump文件的过程中，所有的java程序都将暂停，不要在系统执行过程中创建该文件。

生成堆快照
```
jmap -dump:live,format=b,file=dump.hprof $PID
```
查看指定进程堆信息
```
jmap -heap $PID
```

参数|含义
:--|:--
-heap pid|

#### jstat
用于监视虚拟机各种运行状态信息的命令行工具。可以显示本地或远程虚拟机进程中的类装载，内存，垃圾收集，JIT编译等运行数据。
#### jinfo
实时查看和调整虚拟机各项参数。

#### jstack
用于生成虚拟机当前时刻的线程快照，一般称为threaddump或者javacore文件。线程快照就是当前虚拟机内每一条线程正在执行的方法堆栈的集合，可用来定位线程出现长时间停顿的原因，如线程死锁，死循环，请求外部资源导致的长时间等待都是导致线程长时间停顿的常见原因。
#### jconsole
#### visualvm
***

### JVM参数
#### GC内存配置
参数|描述
:-|:-
-Xms (-XX:InitialHeapSize) |启动JVM时堆内存的大小，即堆空间初始值
-Xmx (-XX:MaxHeapSize) |堆内存最大限制
-Xmn|新生代空间大小
-XX:NewSize|新生代空间初始值
-XX:MaxNewSize|新生代空间最大值
-XX:PermSize|永久代空间的初始值 (before JDK7)
-XX:MaxPermSize|永久代空间的最大值 (before JDK7)
-XX:MetaspaceSize|永久代空间的初始值 (JDK8)
-XX:MaxMetaspaceSize|永久代空间的最大值 (JDK8)

#### GC类型配置
配置|描述
:--|:--
-XX:+UseSerialGC|串行垃圾回收器
-XX:+UseParallelGC|并行垃圾回收器
-XX:+UseParNewGC|使用ParNew和Serial Old垃圾回收器组合
-XX:+UseConcMarkSweepGC|并发标记扫描垃圾回收器
-XX:ParallelCMSThreads=N|并发标记扫描垃圾回收器使用的线程数量
-XX:+UseG1GC|G1垃圾回收器

***
