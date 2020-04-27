### cgroups作用

1.资源限制：cgroups 可以对任务是要的资源总额进行限制。比如设定任务运行时使用的内存上限，一旦超出就发 OOM。

2.优先级分配：通过分配的 CPU 时间片数量和磁盘 IO 带宽，实际上就等同于控制了任务运行的优先级。

3.资源统计：cgoups 可以统计系统的资源使用量，比如 CPU 使用时长、内存用量等。这个功能非常适合当前云端产品按使用量计费的方式。

4.任务控制：cgroups 可以对任务执行挂起、恢复等操作。

### cgroups组成

- task

  在Cgroups中，task就是一个系统进程

- cgroup

  Cgroups中的资源控制都是以cgroup为单位实现的。cgroup表示按照某种资源控制标准分成的任务组，包含一个或多个子系统。一个任务可以加入某个cgroup，也可以从某个cgroup移到另外一个cgroup

- subsystem

  subsystem相当于一个资源控制调度器。比如cpu子系统可以控制cpu时间分配，内存子系统可以控制内存使用量

- hierarchy

  hierarchy由一系列cgroup以一个树状结构组成，每个hierarchy通过绑定对应的subsystem进行资源调度。hierarchy中的cgroup节点可以包含零或多个子节点，子节点继承父节点的属性。整个系统可以有多个hierarchy。

#### 组件中的关系

1、同一个hierarchy能够附加一个或多个subsystem。
如下图，将cpu和memory subsystems(或者任意多个subsystems)附加到同一个hierarchy。

![clipboard.png](https://segmentfault.com/img/bVbs5F3?w=614&h=313)

2、一个subsystem只能附加到一个hierarchy上。
如下图，cpu subsystem已经附加到了hierarchy A，并且memory subsystem已经附加到了hierarchy B。因此cpusubsystem不能在附加到hierarchy B。

![clipboard.png](https://segmentfault.com/img/bVbs5F5?w=622&h=293)

3、系统每次新建一个hierarchy时，该系统上的所有task默认构成了这个新建的hierarchy的初始化cgroup，这个cgroup也称为root cgroup。对于你创建的每个hierarchy，task只能存在于其中一个cgroup中，即一个task不能存在于同一个hierarchy的不同cgroup中，但是一个task可以存在在不同hierarchy中的多个cgroup中。如果操作时把一个task添加到同一个hierarchy中的另一个cgroup中，则会从第一个cgroup中移除。
如下图，cpu和memory被附加到cpu_mem_cg的hierarchy。而net_cls被附加到net_cls hierarchy。并且httpd进程被同时加到了cpu_mem_cg hierarchy的cg1 cgroup中和net hierarchy的cg3 cgroup中。并通过两个hierarchy的subsystem分别对httpd进程进行cpu,memory及网络带宽的限制。

![clipboard.png](https://segmentfault.com/img/bVbs5Gb?w=689&h=328)

4、系统中的任何一个task(Linux中的进程)fork自己创建一个子task(子进程)时，子task会自动的继承父task cgroup的关系，在同一个cgroup中，但是子task可以根据需要移到其它不同的cgroup中。父子task之间是相互独立不依赖的。
如下图，httpd进程在cpu_and_mem hierarchy的/cg1 cgroup中并把PID 4537写到该cgroup的tasks中。之后httpd(PID=4537)进程fork一个子进程httpd(PID=4840)与其父进程在同一个hierarchy的统一个cgroup中，但是由于父task和子task之间的关系独立不依赖的，所以子task可以移到其它的cgroup中。

![clipboard.png](https://segmentfault.com/img/bVbs5Gc?w=684&h=323)