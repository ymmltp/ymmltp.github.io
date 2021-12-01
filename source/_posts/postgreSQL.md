---
title: PostgreSQL Learning
date: 2021-10-13 16:57:39
tags: 学无止境
---

## PostgreSQL

###1、注意点：
> 1、大写(A)的名字，需要用双引号（"A"）,使其生效，否者会报错： column "a" does not exist 
2、Trigger怎么写？？？？语法错误

###2、postgreSql in VS .net
> 选择 .net 4.6.1
1、安装插件 Npgsql PostgreSQL Integration
2、安装 EF框架 无框架限制
3、安装 Npgsql 注意.net版本
4、安装 EF6 for Npgsql 提供postgresql的ADO模型，要匹配：.net 以及 2,3 的版本


###2、postgreSql in VS .net Core
>1、安装插件 Npgsql PostgreSQL Integration
2、安装 EF框架：Microsoft.EntityFrameworkCore
3、Microsoft.EntityFrameworkCore.Tools
4、安装 Npgsql: Npgsql.EntityFrameworkCore.PostgreSQL
5、Npgsql.EntityFrameworkCore.PostgreSQL.Design
6、cmd->cd 进入工程文件.csproj所在的文件夹 -> 
dotnet ef dbcontext scaffold "Host=cnwuxm1medb01;Database=FOF;Username=FOFUser;Password=Jabil123" Npgsql.EntityFrameworkCore.PostgreSQL -o Model
