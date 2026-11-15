---
title: "SQL Server对等发布出错:执行一批命令时出错。正在重试单个命令"
date: 2024-10-31 19:26:19 +0800
---

错误：SQL Server对等发布出错:执行一批命令时出错。正在重试单个命令

![图片](https://i-blog.csdnimg.cn/direct/fc48f575cf1743ad85ed7807f2f36d99.png)

在事务 ID 为 0x00000000ce0f5800 的对等方 100 (传入)和事务 ID 为 0x00000000ce0faa8c 的对等方 2 (在磁盘上)之间的对等方 2 处检测到类型为 'Update-Update' 的冲突

![图片](https://i-blog.csdnimg.cn/direct/ba8e73df53354e6097391e0f5037688e.png)

发布服务器运行

```sql
sp_helpsubscriptionerrors 'publisher', 'publisher_db', 'publication', 'subscriber', 'subscriber_db'
```

再运行

```sql
exec distribution.dbo.sp_browsereplcmds '0x00067945000066B0000300000000','0x00067945000066B0000300000000'
```

注意：

1、不要用触发器修改数据，会导致两边数据冲突

2、尽量就用一台数据库做写的操作，不然容易冲突

参考：

[Troubleshoot error 20598 - SQL Server | Microsoft Learn](https://learn.microsoft.com/en-US/troubleshoot/sql/database-engine/replication/troubleshoot-error-20598)

[sp_helpsubscriptionerrors (Transact-SQL) - SQL Server | Microsoft Learn](https://learn.microsoft.com/zh-cn/sql/relational-databases/system-stored-procedures/sp-helpsubscriptionerrors-transact-sql?redirectedfrom=MSDN&view=sql-server-ver16)

[「链接」](https://blog.51cto.com/u_16532032/9366509)
