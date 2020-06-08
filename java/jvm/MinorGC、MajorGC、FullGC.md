* 部分收集
  - 新生代收集（Minor GC / Young GC）：只有新生代的（Eden\S0，S1）的垃圾收集
  - 老年代收集（Major GC/Old GC）：只是老年代的垃圾收集
    - 目前，只有CMS GC会有单独收集老年代行为
  - 混合收集（Mixed GC）：收集整个新生代以及部分老年代的垃圾收集
    * 目前只有G1 GC会有这种行为
* 整堆收集（Full GC）：收集整个java堆和方法区的垃圾收集。

