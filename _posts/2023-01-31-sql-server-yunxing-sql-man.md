---
title: SQL Server运行SQL慢
date: 2023-01-31 10:44:42 +0800
---

问题：SQL Server运行SQL慢

解决：

建索引：

```cobol
--缺失的索引

SELECT  avg_total_user_cost * avg_user_impact * ( user_scans + user_seeks ) AS PossibleImprovement , 

        last_user_seek , 

        last_user_scan , 

        [statement] AS [Object] , 

        'CREATE INDEX [IDX_' + CONVERT(VARCHAR(32), GS.group_handle) + '_' 

        + CONVERT(VARCHAR(32), D.index_handle) + '_' 

        + REPLACE(REPLACE(REPLACE([STATEMENT], ']', ''), '[', ''), '.', '') 

        + ']' + ' ON ' + [statement] + ' (' + ISNULL(equality_columns, '') 

        + CASE WHEN equality_columns IS NOT NULL 

                    AND inequality_columns IS NOT NULL THEN ',' 

               ELSE '' 

          END + ISNULL(inequality_columns, '') + ')' + ISNULL(' INCLUDE (' 

                                                              + included_columns 

                                                              + ')', '') AS Create_Index_Syntax 

FROM    sys.dm_db_missing_index_groups AS G 

        INNER JOIN sys.dm_db_missing_index_group_stats AS GS ON G.index_group_handle = GS.group_handle 

        INNER JOIN sys.dm_db_missing_index_details AS D ON G.index_handle = D.index_handle 

ORDER BY statement,PossibleImprovement desc
```

查无用索引：

```cobol
--无用的索引

SELECT  ind.index_id , 

        obj.name AS TableName , 

        ind.name AS IndexName , 

        ind.type_desc , 

        indUsage.user_seeks , 

        indUsage.user_scans , 

        indUsage.user_lookups , 

        indUsage.user_updates , 

        indUsage.last_system_seek , 

        indUsage.last_user_scan , 

        'drop index [' + ind.name + '] ON [' + obj.name + ']' AS DropIndexCommand 

FROM    sys.indexes AS ind 

        INNER JOIN sys.objects AS obj ON ind.object_id = obj.object_id 

        LEFT JOIN sys.dm_db_index_usage_stats indUsage ON ind.object_id = indUsage.object_id 

                                                          AND ind.index_id = indUsage.index_id 

WHERE   ind.type_desc <> 'HEAP' 

        AND obj.type <> 'S' 

        AND OBJECTPROPERTY(obj.object_id, 'isusertable') = 1 

        AND ( ISNULL(indUsage.user_seeks, 0) = 0 

              AND ISNULL(indUsage.user_scans, 0) = 0 

              AND ISNULL(indUsage.user_lookups, 0) = 0 

            ) 

ORDER BY obj.name , 

        ind.name
```

查询索引碎片语句

```sql
SELECT OBJECT_NAME(ind.OBJECT_ID) AS TableName,

ind.name AS IndexName, indexstats.index_type_desc AS IndexType,

indexstats.avg_fragmentation_in_percent

FROM sys.dm_db_index_physical_stats(DB_ID(), NULL, NULL, NULL, NULL) indexstats

INNER JOIN sys.indexes ind

ON ind.object_id = indexstats.object_id

AND ind.index_id = indexstats.index_id

WHERE indexstats.avg_fragmentation_in_percent > 30

ORDER BY indexstats.avg_fragmentation_in_percent DESC
```

重建索引语句

```sql
Use [数据库名称]

Go

DECLARE @DBCCString NVARCHAR(1000)

DECLARE @TableName VARCHAR(100)

DECLARE Cur_Index CURSOR

FOR

SELECT Name AS TblName

FROM sysobjects

WHERE xType='U'

ORDER BY TblName

FOR READ ONLY

OPEN Cur_Index

FETCH NEXT FROM Cur_Index

INTO @TableName

WHILE @@FETCH_STATUS=0

BEGIN

SET @DBCCString = 'DBCC DBREINDEX(@TblName,'''')WITH NO_INFOMSGS'

EXEC SP_EXECUTESQL @DBCCString,N'@TblName VARCHAR(100)', @TableName

PRINT '重建表' + @TableName +'的索引........OK!'

FETCH NEXT FROM Cur_Index INTO @TableName

END

CLOSE Cur_Index

DEALLOCATE Cur_Index

PRINT '操作完成！'

go

DBCC UPDATEUSAGE(0);
```

还可以升级下SQL Server的版本，Enterprise版本确实比Web版本快，升级方式：运行安装文件，里面有个升级功能，输入相关版本的SN就可以升了

[使用数据库引擎优化顾问](https://learn.microsoft.com/zh-cn/sql/tools/dta/lesson-2-using-database-engine-tuning-advisor?view=sql-server-ver17 "使用数据库引擎优化顾问")

参考：[在SQLSERVER中查找缺失和无用的索引SQL](https://www.e-com-net.com/article/643.htm "在SQLSERVER中查找缺失和无用的索引SQL")
