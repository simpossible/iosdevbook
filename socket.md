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
      LISTEN CONNECT ACCEPT RECEIVE SEND DISCONNECT BIND ---
      根据这些原语可以组成我们的服务，比如常见的IM 服务。HTTP 服务.等
```

### socket api

* 创建socket

  > int socket\( int af, int type, int protocol\);
  > 
  > example
  > 
  > int socket = socket\(AF\_INET, SOCK\_STREAM, IPPROTO\_TCP\);
  > 
  > @param af 这个是socket 类型 参数目前固定为 AF\_INET
  > 
  > @param type  数据的传输方式。可选值 SOCK\_DGRAM  SOCK\_STREAM  SOCK\_RAW  SOCK\_RDM   SOCK\_SEQPACKET
  > 
  > @param IPPROTO\_TCP TCP 协议，当然还有udp rdp 等协议

* 绑定端口

  > int bind\(int sockfd, struct sockaddr \* my\_addr, int addrlen\)
  > 
  > example
  > 
  > int state = bind\(\_socket, \(struct sockaddr \*\)&addr, addr.sin\_len\);
  > 
  > @param sockfd 上一步创建socket 得到的返回值。socket
  > 
  > @param my\_addr 绑定的网络地址。 sockaddr\_in  与 sockaddr 本质上是同一类型。一般用强转方式使用
  > 
  > @param addrlen my\_addr 的对象大小 用sizeof 进行传入就ok了。

* 监听

  > int listen\( int sockfd, int backlog\);
  > 
  > example
  > 
  > int state = listen\(\_socket, number\)
  > 
  > @param sockfd 创建socket 得到的返回值
  > 
  > @param backlog 等待连接队列的最大长度

* 连接

  > 服务端
  > int accept\(int sockfd, struct sockaddr \*addr, socklen\_t \*addrlen\);
  > 客户端
  > int connect\(int s, const struct sockaddr \* name, int namelen\);

* 发送数据

  > 面向连接
  > 
  >        size\_t send\(int sockfd, const void \*buff, size\_t nbytes, int flags\)
  > 
  >        @param sockfd accept 的返回值\(服务端\)，或者 创建的socket\(客户端\)
  > 
  > 无连接
  > 
  >        int sendto\(int sockfd, const void \* buffer, int len, unsigned int flags, const struct sockaddr \* to, int addrlen\)
  > 
  >        @param sockfd 创建的socket 
  > 
  >        @param buffer 发送的数据
  > 
  >        @param len 发送的数据长度
  > 
  >        @param flag 暂时写 0 其他值的话，发送方式会发生改变

* 接收数据

  > 面向连接
  > 
  > int recv\(\_In\_ SOCKET s, \_Out\_ char \*buf, \_In\_ int len, \_In\_ int flags\);
  > 
  > 无连接
  > 
  > ssize\_t recvfrom\(int sockfd, void \*buff, size\_t buffsize, int flag, struct sockaddr \*senderaddr , socklen\_t \*addrlen\)


### 附加说明

SOCK\_STREAM：这个的数据会以流的方式进行,只有在面向连接的socket 上才有用，如TCP

