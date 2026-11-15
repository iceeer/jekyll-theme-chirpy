---
title: SQL Server切至备机后提示主键已存在（双向发布订阅）
date: 2024-11-08 +0800
---
问题：SQL Server切至备机后出错提示主键已存在（双向发布订阅）

```cobol
com.microsoft.sqlserver.jdbc.SQLServerException: 违反了 PRIMARY KEY 约束“PK_T_XXXXX”。不能在对象“dbo.t_xxxxx”中插入重复键。重复键值为 (33291882)
```

原因：SQL Server发布订阅的时候没有同步数据库表自增ID值

处理：修改表自增ID值

查当前数据库中所有有自增ID的表

```sql
SELECT 
    TABLE_NAME, 
    COLUMN_NAME, 
	IDENT_CURRENT(TABLE_NAME)
FROM 
    INFORMATION_SCHEMA.COLUMNS
WHERE COLUMNPROPERTY(OBJECT_ID(TABLE_NAME), COLUMN_NAME, 'IsIdentity') = 1 
AND TABLE_NAME NOT LIKE 'syncobj%'
AND TABLE_NAME NOT LIKE 'MSpeer_%'
AND TABLE_NAME NOT LIKE 'sys%'
AND TABLE_NAME NOT LIKE 'v_%'
AND TABLE_NAME NOT LIKE 'MSsub%'
```

修改表自增ID值

```sql
DBCC CHECKIDENT('表名', RESEED, 新的id值)
```
