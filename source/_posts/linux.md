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
|cat|访问文件|
|man|搜索命令的相关文档 https://linux.die.net|
|pwd|显示当前路径|
|mkdir|创建新目录|
|rmdir|删除一个空目录|
|cp|复制文件或者目录|
|mv|移动文件或目录|
|rm|移除文件或目录|

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

#### Linux文本编辑器 Vim

```batch
//打开
vim 文件

//插入模式：
i

//命令模式
:
```
