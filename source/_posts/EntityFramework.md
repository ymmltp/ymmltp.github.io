---
title: Entity Framework
date: 2021-11-10 09:48:05
tags: 学无止境
---
## EntityFramwork

### 1、EF 链接各类型数据库

[Scaaffold-DbContext指令解释](https://www.cnblogs.com/mhc860217/articles/11919563.html)

#### 1.1、.net EF 链接postgreSql

> 选择 .net 4.6.1
>1. 安装插件 Npgsql PostgreSQL Integration
>2. 安装 EF框架 无框架限制
>3. 安装 Npgsql 注意.net版本
>4. 安装 EF6 for Npgsql 提供postgresql的ADO模型，要匹配：.net 以及 2,3 的版本

#### 1.2、Core EF 链接postgreSql

>1. 安装插件 Npgsql PostgreSQL Integration
>2. 安装 EF框架：Microsoft.EntityFrameworkCore
>3. Microsoft.EntityFrameworkCore.Design;
   Microsoft.EntityFrameworkCore.Tools
>4. 安装 Npgsql: Npgsql.EntityFrameworkCore.PostgreSQL
>5. Npgsql.EntityFrameworkCore.PostgreSQL.Design
>6. cmd->cd 进入工程文件.csproj所在的文件夹 -> 
dotnet ef dbcontext scaffold "Host=cnwuxm1medb01;Database=EC;Username=ECUser;Password=Jabil123" Npgsql.EntityFrameworkCore.PostgreSQL -o Models

- Use dotnet build to see the errors
    >程序编译出错了，要保证程序能够正常运行的基础上，更新数据库cs文件
- Use the Force flag to overwrite these files
    >dotnet ef dbcontext scaffold "Host=cnwuxm1medb01;Database=FOF;Username=FOFUser;Password=Jabil123" Npgsql.EntityFrameworkCore.PostgreSQL -o Model -f

#### 1.3、Core EF 链接 MySQL

>1. 安装 EF框架：Microsoft.EntityFrameworkCore
>2. Microsoft.EntityFrameworkCore.Tools
>3. 安装 Mysql.Data
>4. 安装 Pomelo.EntityFrameworkCore.MySql(官方插件有问题，使用这个社区版本)
>5. cmd->cd 进入工程文件.csproj所在的文件夹 -> 
Scaffold-DbContext "server=cnwuxg0te01;uid=root;pwd=Jabil12345;port=3306;database=sparepart_current;" Pomelo.EntityFrameworkCore.MySql -OutputDir Models -f

#### 1.4、Core EF 链接 SQL Server

> 通过数据库结构建立实体：
> 1. Install-Package Microsoft.EntityFrameworkCore.SqlServer
Install-Package Microsoft.EntityFrameworkCore.Tools
Install-Package Microsoft.EntityFrameworkCore.SqlServer.Design
> 2. cmd->cd 进入工程文件.csproj所在的文件夹 -> 
Scaffold-DbContext 'Data Source=cnwuxm0lsql01;Initial Catalog=PMMS;User ID=pmms_readonly;Password=Jabil123;MultipleActiveResultSets=True;Connection Timeout=120' Microsoft.EntityFrameworkCore.SqlServer -OutputDir Models\PMMS -Table EQ,PMrecord,PMItems

Scaffold-DbContext "Data Source=cnwuxg0te01;Initial Catalog=Apps;User ID=sa;Password=Jabil12345;MultipleActiveResultSets=True;Connection Timeout=120;TrustServerCertificate=true" Microsoft.EntityFrameworkCore.SqlServer -OutputDir Models\Common -Table Calendar

> 更新数据库：
>1. add-migration AddUserDetails 
>2. update-database AddUserDetails 


### 2、查询语句

可以使用linq语句，或者EF结构

#### 动态条件查询

```C#
var item = db.pmsheets.ToList();
    if (!string.IsNullOrEmpty(department))
        item = item.Where(e => e.department == department).ToList();
    if (!string.IsNullOrEmpty(project))
        item = item.Where(e => e.project == project).ToList();
    var items = item.Select(e => new {
        paras = e.station
    }).Distinct().ToList();
```

#### 两表链接

```C#
var pmitems = db.PMItems
        .Join(db.EQs, pm => pm.EQID, eq => eq.EQID, (pm, eq) => new { 
            pmid=pm.pmid,
            EQID=pm.pmid,
            owner = eq.Owners,
        })
        .Where(e => pmid.Contains(e.pmid)).ToList();
```

#### Where 不执行

```C#
pmms pmmsdb = new pmms();
inspect db = new inspect();
var eqwhere = pmmsdb.EQs.Where(e => true);
if (department.Length>0) eqwhere = eqwhere.Where(e => department.Contains(e.Department));
if (line.Length > 0) eqwhere = eqwhere.Where(e => line.Contains(e.Line));
if (project.Length > 0) eqwhere = eqwhere.Where(e => project.Contains(e.Workcell));
var eqlist = eqwhere.Select(e => new {
    Line = e.Line,
    EQID = e.EQID
}).ToList();
```

#### EF 实现sql中的方法

```C#
using Microsoft.EntityFrameworkCore;
EF.Functions
```

```C#
EF 中 Equals方法，只能用于引用类型(例如：string)，不能用于值类型(例如：int)
```
