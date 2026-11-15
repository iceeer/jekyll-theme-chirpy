---
title: SQL Server CPU高
date: 2024-11-12 +0800
---
问题：SQL Server进程的CPU很高

解决：

查看正在执行的 sql 状态

```sql
SELECT  
 der.[session_id],der.[blocking_session_id],  
 sp.lastwaittype,sp.hostname,sp.program_name,sp.loginame,  
 der.[start_time] AS '开始时间',  
 der.[status] AS '状态',  
 dest.[text] AS 'sql语句',  
 DB_NAME(der.[database_id]) AS '数据库名',  
 der.[wait_type] AS '等待资源类型',  
 der.[wait_time] AS '等待时间',  
 der.[wait_resource] AS '等待的资源',  
 der.[logical_reads] AS '逻辑读次数'  
 FROM sys.[dm_exec_requests] AS der  
 INNER JOIN master.dbo.sysprocesses AS sp ON der.session_id=sp.spid  
 CROSS APPLY  sys.[dm_exec_sql_text](der.[sql_handle]) AS dest
```

此时可以关注下查询编译以来 cpu 耗时总量最多的前 50 条 (Total_woker_time)

```sql
select
'total_worker_time(ms)'=(total_worker_time/1000),
q.[text], DB_NAME(dbid),OBJECT_NAME(objectid),
execution_count,
'max_worker_time(ms)'=(max_worker_time/1000),
'last_worker_time(ms)'=(last_worker_time/1000),
'min_worker_time(ms)'=(min_worker_time/1000),
'max_elapsed_time(ms)'=(max_elapsed_time/1000),
'min_elapsed_time(ms)'=(min_elapsed_time/1000),
'last_elapsed_time(ms)'=(last_elapsed_time/1000),
total_physical_reads,
last_physical_reads,
min_physical_reads,
max_physical_reads,
total_logical_reads,
last_logical_reads,
max_logical_reads,
creation_time,
last_execution_time
from
(select top 50 qs.* from sys.dm_exec_query_stats qs order by qs.total_worker_time desc)
as highest_cpu_queries cross apply sys.dm_exec_sql_text(highest_cpu_queries.plan_handle) as q
order by highest_cpu_queries.total_worker_time DESC
```

查询连接数

```sql
select loginame,count(1) as Nums
from sys.sysprocesses
group by loginame
order by 2 desc
```

查sql日记

```sql
SELECT TOP 1000
    --创建时间
    QS.creation_time,
    --查询语句
    SUBSTRING(ST.text, (QS.statement_start_offset / 2)+1, ((CASE QS.statement_end_offset WHEN -1 THEN DATALENGTH(ST.text)ELSE QS.statement_end_offset END-QS.statement_start_offset)/ 2)+1) AS statement_text,
    --执行文本
    ST.text,
    --执行计划
    QS.total_worker_time, QS.last_worker_time, QS.max_worker_time, QS.min_worker_time, QS.*
FROM sys.dm_exec_query_stats QS
     --关键字
     CROSS APPLY sys.dm_exec_sql_text(QS.sql_handle) ST
WHERE QS.creation_time BETWEEN '2023-04-18 16:00:00' AND '2023-04-18 17:00:00'
--AND ST.text LIKE '%%'
ORDER BY QS.creation_time DESC;
```

[解决 SQL Server 中 CPU 使用率过高的问题](https://learn.microsoft.com/zh-cn/troubleshoot/sql/database-engine/performance/troubleshoot-high-cpu-usage-issues)
