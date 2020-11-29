GC机制
===========
Garbage Collector

1. 什么是垃圾?
-----------------
手动回收C++
* C语言申请内存
* C++ new/delete
* Java, new

Java自动回收内存,编程上简单,系统不容易出错.

容易出现两类型错误
(1) 忘记回收 --> 内存泄漏,溢出
(2) 多次回收

如果一个对象,没有任何指针指向他了,这个对象就是垃圾.(循环引用)
一堆对象--一堆垃圾


2. 如何找到垃圾?
----------------
* reference count(引用计数)
* Root Searching根可达算法
GC roots--线程栈变量、静态变量、常量池、JNI指针

3. 常见的垃圾回收算法
-----------
* 标记清除 Mark-sweep, 位置不连续,产生碎片
* 拷贝 copying 没有碎片,浪费空间
* 标记压缩 Mark-compact 整理,把空白的区域全部连在一起,没有碎片,效率偏低

4. JVM内存分代算法(用于垃圾回收算法)
------------
新生代---new-young
* 存活对象少
* 使用copy算法,效率高

老年代old
* 垃圾少
* 一般使用mark compact
* old

永久代1.7,元数据区1.8 Metaspace
1. 都是装class
2. 永久代可以指定大小限制,元数据区无上限,可以设置也可以不设置.(受限于物理内存)
3. 字符串常量 1.7 永久代, 1.8 堆
4. 方法区MethodArea逻辑概念,永久代,元数据(用于理解)

堆内存逻辑分区
eden/survivor/survivor/tenured终身
8:1:1
* 新生代= Eden 和两个survivor区,进行一次YGC后,大多数对象会被清理,活着的进入s0-----会用Coping方法
* s0--再次YGC----->进入s1区.
* 再次YGC---> eden+ s1 ->s0
* 年龄足够,进入老年代 (15/CMS 6)
* s区装不下-->老年代


4. 老年代满了之后,	
	* Full GC
5. GC Tuning(Generation)
	* 尽量减少FGC,FGC频率越低越好
	* MinorGC = YGC
	* MajorGC = FGC

	
5. 常见的垃圾回收器
-----------------
十种
Serial --> Serial Old
a stop-the-world, coping collector which uses a single GC thread.
1. Serial 年轻代,单进程的,串行回收

2. parallel PS, 并行回收,年轻代
3. ParNew, 和CMS配合使用的并行回收,年轻代

4. SerialOld
5. ParalleOld

6. Concurrent mask sweep (CMS),回收时程序也可以运行,并发的,老年代,降低STW的时间(200ms)

7. G1 (10ms)
8. ZGC(1ms)
9. Shenandoah
10. Eplison

**调优集中于前五个,1,2,4,5

1.8 默认的垃圾回收: PS+ParallelOld


6.JVM调优的第一步,了解生产环境下的垃圾回收器组合
-----------------
JVM命令行参考:
https://docs.oracle.com/javase/8/docs/technotes/tools/unix/java.html

JVM参数分类:
标准: -开头,所有的Hotspot都支持
非标准: -X
不稳定: -XX:+PrintFlagsFinal
如何设置:
java -XX:+UseG1GC
-XX:+PrintFlagsFinal
 * 最终参数值
-XX:PrintFlagsInitial 
 * 显示默认值
-XX:+PrintCommandLineFlags
 * 命令行参数



GC
===========
熟悉GC的常用算法,熟悉常见垃圾收集器,具有实际的JVM调优实战经验

什么是垃圾?
------------
1. 程序的栈(stack frame)和堆
栈


