### zookeeper监听器原理

1.首先要有一个main（）线程

2.在main（）线程创建zookeeper客户端，这时就会创建两个子线程，一个负责网络连接通信（connect），一个负责监听（listener）

3.通过connect线程将注册的监听事件发送给zookeeper服务端

4.在zookeeper服务端的注册监听器列表中将注册的监听事件添加到列表中

5.zookeeper服务端在监听到数据或路径有变化时，就会将这个消息发给客户端的listener线程

6.listener线程内部调用process方法进行相应处理

![](/Users/huchuanwen/Desktop/学习资料/snapshotPics/WX20200427-165802@2x.png)

