1. -Xss 设置每个线程栈空间大小
2. -Xms 用于表示堆区的起始内存，等价于-XX:InitialHeapSize
3. -Xmx 用于表示堆区的最大内存，等价于-XX:MaxHeapSize
4. -XX:NewRatio 配置新生代与老年代在堆结构的占比 默认为2，即新生代占1，老年代栈2
5. -XX:SurvivorRatio 调整新生代中Eden空间和另外两个Survivor空间所占比例，默认是8:1:1
6. 