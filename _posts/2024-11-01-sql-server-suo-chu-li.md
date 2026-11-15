---
title: "SQL Server锁处理"
date: 2024-11-01 10:46:04 +0800
---

问题：出现查询超时的情况

解决：查查是不是有锁了

查询锁：

```sql
select request_session_id spid,

OBJECT_NAME(resource_associated_entity_id) tableName,request_type ,request_owner_type,request_mode,request_status

from sys.dm_tran_locks where resource_type='OBJECT'
```

看看有没有IX类型的锁

模拟锁：

```sql
BEGIN TRANSACTION;

UPDATE t_data SET test_fiels = '' WHERE id = 1;

WAITFOR DELAY '00:01:050'; -- 等待1分钟

COMMIT;
```

测试下是否有锁：运行select * from t_data

删锁：kill <锁ID>

查进程：sp_who2 <锁ID>

也可以忽略锁进行查询：

```sql
select * from t_data WITH (NOLOCK)

。。。。。t_data INNER JOIN WITH (NOLOCK)
```

如果是视图，可以修改视图定义，表后面加上nolock，不需要代码里改sql

*nolock 只能和 select 一起用，不能和 update,delete,insert
