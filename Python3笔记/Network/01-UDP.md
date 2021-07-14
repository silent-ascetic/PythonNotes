# UDP协议

> Internet 协议集支持一个无连接的传输协议，该协议称为用户数据报协议（UDP，User Datagram Protocol）。UDP 为应用程序提供了一种无需建立连接就可以发送封装的 IP 数据包的方法。

## socket

> python中用于程序间网络通信的模块，[官方文档](https://docs.python.org/zh-cn/3/library/socket.html?highlight=socket)

### 发送数据

```py
import socket

# AF_INET：使用ipv4，SOCK_DGRAM：使用udp协议
udpSocket = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)

# 第一个参数为发送的信息（必须为字节类型）元组存储接收端的ip和post
udpSocket.sendto(b'The message', ('192.168.18.112', 1200))
# 每次发送信息时系统为套接字随机分配一个端口
udpSocket.sendto(b'The message', ('192.168.18.112', 1200))
# 关闭套接字资源
udpSocket.close()

```

### 绑定固定

```py
import socket

udpSocket = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)

# 设置发送时使用的端口号,元组第一个值为本机的一个ip（可写可不写），第二个为要绑定的端口号
udpSocket.bind(('', 1020))

# 元组存储接收端的ip和post
udpSocket.sendto(b'The message', ('192.168.18.112', 1200))
# 每次发送信息时系统为套接字随机分配一个端口
udpSocket.sendto(b'The message', ('192.168.18.112', 1200))

udpSocket.close()


```

### 接收数据

```py
import socket

udpSocket = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
# 接收方必须绑定端口
udpSocket.bind(('', 1020))

# 参数表示最大接收字节数
message = udpSocket.recvfrom(1024)
udpSocket.close()

# 知道接收到信息才会继续向下运行
print(message)

'''
打印结果：
(b'The message', ('192.168.181.25', 1020))
其中IP是发送端的IP，端口是发送端的端口
'''
```

```py
import socket

udpSocket = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)

udpSocket.bind(('', 1020))
# 将字符串转换成字节
udpSocket.sendto('发送的消息'.encode('utf-8'), ('192.168.18.16', 1020))
udpSocket.sendto('发送的消息'.encode('gb2312'), ('192.168.18.5', 1020))
# 参数表示最大接收字节数
message = udpSocket.recvfrom(1024)
udpSocket.close()

# 将字节转换成字符串
print(message[0].decode())
print(message[0].decode('gb2312'), f'{message[1][0]}:{message[1][1]}')
```

### 发送广播

    广播：发送方所在网段下所有设备都能收到，发送端将数据发给交换机，交换机将数据发送给网段下的所有设备。只能用于udp，tcp不能广播
```py
import socket

udpSocket = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
# 进行此设置之后才能发送广播
udpSocket.setsockopt(socket.SOL_SOCKET, socket.SO_BROADCAST, 1)
udpSocket.bind(('', 1021))
'''
<broadcast>表示所在网段的广播地址，也可以写xxx.xxx.xxx.255，但不通用
端口号要写想要接收到此广播的程序的端口
'''
udpSocket.sendto('臭傻逼'.encode('utf-8'), ('<broadcast>', 1020))
```

## 附加知识点

> 网络通信中的名词

### 单工

只能发送或接收，类似收音机，只能接收信息

### 半双工

可接收也可发送，但两者不可同时运行，类似对讲机

### 全双工

可以同时发送或接收信息，类似电话
网络是全双工

### 单播

点对点，发送方只发给一个接收方

### 多播

一对多，发送方发给多个接收方

### 广播

一对所有，发送方将数据发送给当前网段下的所有设备
