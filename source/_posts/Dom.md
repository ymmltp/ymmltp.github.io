---
title: Dom指令
date: 2020-09-22 09:48:05
tags: 学无止境
---

## 服务器相关

| CODE                        | MEAN                     |
| :-------------------------- | :----------------------- |
| netstat -aon\|findstr "9050 | //查看port是否被占用     |
| netstat -ano                | //查看系统正在使用的port |

## 通信相关

| CODE               | MEAN |
| ------------------ | ---- |
| telnet   [IP]      |      |
| ping  [IP]  [port] |  测试ip通讯    |
|                    |      |

## 进程相关

### 关闭进程

```dos
//========= CMD强制关闭进程 =========//
taskkill /PID 2788 /F
```