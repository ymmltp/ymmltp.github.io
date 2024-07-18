---
title: SqlServer
date: 2023-03-02 10:52:59
tags: 学无止境
---

# SQL Server

## 触发器 （Triggers）

```sql
-- 创建 Trigger

USE [e_DMS]
GO
/****** Object:  Trigger [dbo].[updateWeekLength]    Script Date: 3/2/2023 11:03:17 AM ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
-- =============================================
-- Author: Adele lu
-- Create date: 2023-03-02
-- Description:	确保 Calender 中的周别都是两位，不足两位的，在前面补 0
-- =============================================
ALTER TRIGGER 触发器名字
   ON 作用的表格或者视图 FOR [INSERT/Update/Delete]
AS 
    declare @weekNo varchar
    select @weekNo = [Week] from inserted
    if(len(@weekNo)<2)  --触发条件
BEGIN
    -- 执行过程
update Calendar set [Week] =RIGHT('00'+ @weekNo,2) where [Week]=@weekNo
	-- SET NOCOUNT ON added to prevent extra result sets from
	-- interfering with SELECT statements.
	SET NOCOUNT ON;
    -- Insert statements for trigger here
END

```

## Update 回撤

```sql
BEGIN TRANSACTION;

UPDATE your_table SET column1 = 'new_value' WHERE id = 1;

-- 如果您想要撤销更新，请使用以下命令：
ROLLBACK TRANSACTION;
```

## Select 一个新表

```sql

select *  into new_table from old_table --将old_table的内容复制到new_table中，会创建一个新表
select *  into #new_table from old_table --将old_table的内容输入到一个临时表new_table中，会话结束时，自动删除。

```