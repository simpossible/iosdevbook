# Socket

## 简介

* 什么是socket
* socket 有什么用
* socket api

### 什么是socket

```
          socket 对于我们程序员来说 就是一套api 的称呼，和openGL 一样。但是在编码中，我们常会说：创建一个socket，或者

创建一个套接字。这里的socket 就是socket 这套api 的设计中的理念来。socket 在英文中的概念是“插座”、“孔”。不过可以这样理

解：一次数据交换至少发生在双方之间。那么这次交换的任意一方就是一个socket。socket 的数据交换可以发生在两个进程之间。这两个进程

可以是本机的两个进程，也可以是任何两台联通的电脑的进程。在ios 上可以使用 socket 来进行进程间通讯。

```

### socket 有什么用

```
      计算机网络中一书中，网络的传输一般我们分为5层：
                   ****************
      物理层 链路层  * 网络层 传输层  *     应用层
                   *  ip  tcp/udp *   http/rtmp/
                    *****socket****
      socket 工作在网络层以及传输层。提供一组原语操作：
      LISTEN CONNECT ACCEPT RECEIVE SEND DISCONNECT ---
      根据这些原语可以组成我们的服务，比如常见的IM 服务。HTTP 服务.等
```

### socket api

* 创建socket
  int socket = socket\(AF\_INET, SOCK\_STREAM, IPPROTO\_TCP\);

* 绑定端口
* 监听
* 连接
* 发送数据
* 接收数据
* 

