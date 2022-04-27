---
title: Entity Framework
date: 2021-11-10 09:48:05
tags: 学无止境
---
## EntityFramwork

### 1、查询语句

可以使用linq语句，或者EF结构

``` C
动态条件查询
var item = db.pmsheets.ToList();
    if (!string.IsNullOrEmpty(department))
        item = item.Where(e => e.department == department).ToList();
    if (!string.IsNullOrEmpty(project))
        item = item.Where(e => e.project == project).ToList();
    var items = item.Select(e => new {
        paras = e.station
    }).Distinct().ToList();

```

### 2、EF 链接各类型数据库

#### 2.1、Core EF 链接SQL Server

```C
Scaffold-DbContext "data source=cnwuxg0te01;initial catalog=dbName;persist security info=True;user id=sa;password=Jabil12345;MultipleActiveResultSets=True;App=EntityFramework" Microsoft.EntityFrameworkCore.SqlServer -OutputDir Models -Tables Employee
```

#### 2.2、.net EF 链接postgreSql

> 选择 .net 4.6.1
1、安装插件 Npgsql PostgreSQL Integration
2、安装 EF框架 无框架限制
3、安装 Npgsql 注意.net版本
4、安装 EF6 for Npgsql 提供postgresql的ADO模型，要匹配：.net 以及 2,3 的版本


#### 2.3、Core EF 链接postgreSql

>1、安装插件 Npgsql PostgreSQL Integration
2、安装 EF框架：Microsoft.EntityFrameworkCore
3、Microsoft.EntityFrameworkCore.Design;
   Microsoft.EntityFrameworkCore.Tools
4、安装 Npgsql: Npgsql.EntityFrameworkCore.PostgreSQL
5、Npgsql.EntityFrameworkCore.PostgreSQL.Design
6、cmd->cd 进入工程文件.csproj所在的文件夹 -> 
dotnet ef dbcontext scaffold "Host=cnwuxm1medb01;Database=EC;Username=ECUser;Password=Jabil123" Npgsql.EntityFrameworkCore.PostgreSQL -o Models

- Use dotnet build to see the errors
    >程序编译出错了，要保证程序能够正常运行的基础上，更新数据库cs文件
- Use the Force flag to overwrite these files
    >dotnet ef dbcontext scaffold "Host=cnwuxm1medb01;Database=FOF;Username=FOFUser;Password=Jabil123" Npgsql.EntityFrameworkCore.PostgreSQL -o Model -f

#### 2.4、Core EF 链接MySQL

>1.安装 EF框架：Microsoft.EntityFrameworkCore
>2.Microsoft.EntityFrameworkCore.Tools
>3.安装 Mysql.Data
>4.安装 Pomelo.EntityFrameworkCore.MySql(官方插件有问题，使用这个社区版本)
>5.cmd->cd 进入工程文件.csproj所在的文件夹 -> 
Scaffold-DbContext "server=cnwuxg0te01;uid=root;pwd=Jabil12345;port=3306;database=sparepart_current;" Pomelo.EntityFrameworkCore.MySql -OutputDir Models -f