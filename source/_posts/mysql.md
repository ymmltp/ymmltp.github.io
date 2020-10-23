---
title: mysql Learning
date: 2020-08-11 13:57:39
tags: 学无止境
---

## Mysql基础用法

### 1.增、删、改、查

#### 查询--Select

```mysql
Select * from [Table]                       //查询整个表
select * from [Table] where [Project]='A' and [Equipment Number]='b' and ……   //查询Project下内容为A的数据
select distinct program FROM A            //相同的program会被合并

SELECT column_name(s) FROM table_name WHERE column_name BETWEEN value1 AND value2
```

#### 增加--Insert

```mysql
Insert into [Table]([表头]，[表头]，[表头]) values('值','值','值')    
Olecmd.ExecuteNonQuery();//写入表
```

#### 修改--Update

```mysql
update [Table] set [列]='value' where [Project]='" + comboBox1.Text + "'and [Equipment Name]='" + comboBox2.Text + "'and [Model]='" + comboBox3.Text + "'"
```

#### 删除--Delete

```mysql
delete from [table] where……;
delete from [table] limit num;  //删除固定几行
```

#### Replace

replace可以起到Insert和Update的效果，但是使用需要注意

### 2.数据库操作

### 3.常见方法

```mysql
order by
desc

```

### 4.实例

##### 查询每组数据的前几个

（例如：每班前三名的同学）

查询每个人最近20次点检用时：

```mysql
SELECT c.DRI,c.pmTime,c.Date
FROM pmhistory c
WHERE(SELECT count(1) AS ID	FROM pmhistory a WHERE a.DRI = c.DRI AND a.Date >= c.Date) <= 20
ORDER BY c.DRI,c.Date desc
```



## Mysql进阶

### 1.EXPLAIN的使用与分析