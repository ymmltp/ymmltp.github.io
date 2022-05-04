---
title: linux
date: 2022-05-04 18:39:31
tags:
---

## Linux

### 常见指令:

|指令|描述|
|--|--|
|ls|查看文件|
|ls -al|查看所有文件和权限|
|chmode|修改用户权限(用数字表示权限:chmod 777 fileName)(chmod ug=rwx,o=x fileName)(用加减法表示权限的增加和删除:chmod ugo+r fileName)(chmod ug+w,o-w fileName)(a:all;u:user;g:group;o:other)|

#### linux 文件类型:

|指令|描述|
|--|--|
|d|目录|
|-|文件|
|l|链接文档(link file)|
|b|可随机存取装置|
|c|串行端口设备|

#### linux 文件权限类型:

|指令|描述|
|--|--|
|-r|读取|
|w|写入|
|x|执行|