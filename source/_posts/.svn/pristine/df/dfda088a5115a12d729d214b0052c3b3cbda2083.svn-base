---
title: socket
date: 2022-04-08 15:37:29
tags: 学无止境
---
## Socket(套接字)

### Define

TCP/IP的上层接口
有两种传输文件的方式
1、TCP 数据流传输，需要定义主机和客机
2、UDP 报文传输，不稳定，但是实时性强

```python
import socket

# 服务器
with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:   # AF_INET:使用IPv4;SOCK_STREAM:TCP协议
    s.bind(('', 1234))   # 关联网卡和端口
    s.listen()   #开始监听
    conn, addr = s.accept()   # 接受客户端链接，返回客户端ip(addr)和新的socket(conn) 
    # *socket s用于监听连接，c用于和客户端通信
    with conn:
        print('Connected by', addr)
        while True:
            data = conn.recv(1024)  # 接受客户端传递的信息，一次最大信息量为1024字节
            if not data:
                break
            conn.sendall(data)  # 发送数据给客户端
            print(data)

# 客户端
with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
    s.connect(('localhost', 1234))   # 链接服务器地址和端口号
    s.sendall(b'Hello, world')
    data = s.recv(1024)
    print(data)
```