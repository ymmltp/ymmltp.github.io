---
title: SVN
date: 2025-04-07 20:55:38
tags: 学无止境
---

## SVN

### SVN地址

https://cnwuxg0te01.corp.jabil.org/svn/FATPSW/

### 将远程仓储的副本检出到本地

CMD 命令行：
`svn checkout <repository_url> --username SW --password Jabil12345`

### 同步远程仓储

<b style="color:red">需要再包含 .svn的目录下执行该操作</b>

CMD 命令行：`svn update`

### 添加新文件

逐个添加文件：`svn add <file_name1> <file_name2> <file_name3>`
批量添加同类型文件：`svn add *.txt`
添加文件夹：`svn add <file_folder>`

### 移除某个文件

* 需要再包含 .svn的目录下执行该操作

逐个添加文件：`svn delete <file_name1>`
添加文件夹：`svn delete <file_folder>`

### 提交文件

`svn commit -m "add new file"`  

如果你只想提交某个特定目录及其子目录下的所有变化，可以指定该目录：
`svn commit <directory_path> -m "Commit changes in directory"`

### 查看版本历史

`svn log`

### 版本回溯

1. 回溯尚未commit的修改项：
   * 先使用`svn status` 查看修改过的文件
   * 再使用`svn revert <file_name1> <file_name2> <file_name3>`回溯特定文件
2. 回溯到服务器上的历史版本
   * 回溯该版本下的所有提交内容 `svn merge -r HEAD:26 .` （注意最后需要带一个 .）

### 安装TortoiseSVN

[TortoiseSVN 官网](https://tortoisesvn.net/downloads.html)

可以使用该工具进行SVN的管理

### 在VSCode安装SVN工具
