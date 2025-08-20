---
title: SQL Learning
date: 2020-08-11 13:57:39
tags: 学无止境
---
## Mysql

### 一、基础用法

#### 1.增、删、改、查

##### 查询--Select

```mysql
Select * from [Table]                       //查询整个表
select * from [Table] where [Project]='A' and [Equipment Number]='b' and ……   //查询Project下内容为A的数据
select distinct program FROM A            //相同的program会被合并

SELECT column_name(s) FROM table_name WHERE column_name BETWEEN value1 AND value2
```

##### 增加--Insert

```mysql
Insert into [Table]([表头]，[表头]，[表头]) values('值','值','值')，('值','值','值')，('值','值','值')    
Olecmd.ExecuteNonQuery();//写入表
```

##### 修改--Update

```mysql
update [Table] set [列]='value' where [Project]='" + comboBox1.Text + "'and [Equipment Name]='" + comboBox2.Text + "'and [Model]='" + comboBox3.Text + "'"
```

##### 删除--Delete

```mysql
delete from [table] where……;
delete from [table] limit num;  //删除固定几行
```

##### Replace

replace可以起到Insert和Update的效果，但是使用需要注意

#### 2.数据库操作

#### 3.常见方法

```sql
order by
group by
desc
count
sum
case when then else end
having
```

#### 4.实例

##### 查询每组数据的前几个

（例如：每班前三名的同学）

查询每个人最近20次点检用时：

```sql
SELECT c.DRI,c.pmTime,c.Date
FROM pmhistory c
WHERE(SELECT count(1) AS ID FROM pmhistory a WHERE a.DRI = c.DRI AND a.Date >= c.Date) <= 20
ORDER BY c.DRI,c.Date desc
```

### 二、Mysql进阶

#### 1.EXPLAIN的使用与分析

#### 2.Case When

```sql
select Fixture_ID,
SUM(CASE `Status` WHEN 'Backend ME' then 1 end )AS 'Backend ME',
SUM(CASE `Status` WHEN 'Production Line' then 1 end) AS 'Production Line'
from fixturelist where Fixture_ID in(
select fixture_id from fixture where Department='TE' AND Project="FATP Common")
```

#### 3.时间比较

now()函数返回的是当前时间的年月日时分秒，如：2008-12-29 16:25:46

CURDATE()函数返回的是年月日信息： 如：2008-12-29

CURTIME()函数返回的是当前时间的时分秒信息，如：16:25:46

```sql
SELECT TIMESTAMPDIFF(MONTH,'2012-10-01','2013-01-13');  //Day
select DATEDIFF('2013-01-13','2012-10-01');
```

#### 4.创建存储过程

```sql
delimiter $
create PROCEDURE Update_FxitureBinCount()

BEGIN
    DECLARE  FixtureID1  varchar(50); -- FixtureID
    DECLARE  Bin1  varchar(32); -- Bin
    DECLARE  BinQTY INT(11);   -- QTY
    -- 遍历数据结束标志
    DECLARE done INT DEFAULT FALSE;
    -- 游标
    DECLARE cur_account CURSOR FOR select Fixture_ID,`Status` AS BIN,COUNT(*) as QTY from fixturelist GROUP BY Fixture_ID,`Status`;
    -- 将结束标志绑定到游标
    DECLARE CONTINUE HANDLER FOR NOT FOUND SET done = TRUE;

    -- 打开游标
    OPEN  cur_account;     
    -- 遍历
    read_loop: LOOP
            -- 取值 取多个字段
            FETCH  NEXT from cur_account INTO FixtureID1,Bin1,BinQTY;
            IF done THEN
                LEAVE read_loop;
             END IF;

        -- 你自己想做的操作
        UPDATE fixturebin_count set qty = BinQTY where Fixture_ID=FixtureID1 and bin=Bin1;

    END LOOP;
    CLOSE cur_account;
END $
```

#### 5.根据特殊字符，将一行内容拆分为多行

```sql
--使用 mysql.help_topic 库
select distinct substring_index(substring_index(a.column1,',',b.help_topic_id+1),',',-1)
from table1 a join mysql.help_topic b on b.help_topic_id<(length(a.column1)-LENGTH(REPLACE(a.column1,',',''))+1)
```
