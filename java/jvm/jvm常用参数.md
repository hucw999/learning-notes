### JVM

1. -Xss 设置每个线程栈空间大小
2. -Xms 用于表示堆区的起始内存，等价于-XX:InitialHeapSize
3. -Xmx 用于表示堆区的最大内存，等价于-XX:MaxHeapSize
4. -Xmn 用于设置新生代大小
5. -XX:NewRatio 配置新生代与老年代在堆结构的占比 默认为2，即新生代占1，老年代栈2
6. -XX:SurvivorRatio 调整新生代中Eden空间和另外两个Survivor空间所占比例，默认是8:1:1
7. -XX:PrintGCDetails 打印垃圾回收信息
8. -XX:+EliminateAllocations可以开启标量替换
9. -XX:+PrintCommandLineFlags查看命令行相关参数（包含使用的垃圾收集器）



### jinfo

1. jinfo -flag 参数 进程id     查看参数值

