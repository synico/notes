
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
用于生成堆转存储快照，一般称为heapdump或dump文件。除此之外还可以设置-XX:+HeapDumpOnOutOfMemoryError参数，让虚拟机在OOM异常出现之后自动生成dump文件。或在Linux系统下通过kill -3命令发送进程退出信号。

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
