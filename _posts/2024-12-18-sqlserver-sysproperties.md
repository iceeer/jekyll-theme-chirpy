---
title: SQL Server报"对象名 'sysproperties' 无效"的错误的解决办法
date: 2024-12-18 +0800
---
错误：SQL Server报"对象名 'sysproperties' 无效"的错误的解决办法

处理：缺sysproperties系统表导致

```sql
CREATE TABLE [dbo].[sysarticles] (
  [artid] int  IDENTITY(1,1) NOT NULL,
  [creation_script] nvarchar(255) COLLATE Chinese_PRC_CI_AS  NULL,
  [del_cmd] nvarchar(255) COLLATE Chinese_PRC_CI_AS  NULL,
  [description] nvarchar(255) COLLATE Chinese_PRC_CI_AS  NULL,
  [dest_table] sysname  NOT NULL,
  [filter] int  NOT NULL,
  [filter_clause] ntext COLLATE Chinese_PRC_CI_AS  NULL,
  [ins_cmd] nvarchar(255) COLLATE Chinese_PRC_CI_AS  NULL,
  [name] sysname  NOT NULL,
  [objid] int  NOT NULL,
  [pubid] int  NOT NULL,
  [pre_creation_cmd] tinyint  NOT NULL,
  [status] tinyint  NOT NULL,
  [sync_objid] int  NOT NULL,
  [type] tinyint  NOT NULL,
  [upd_cmd] nvarchar(255) COLLATE Chinese_PRC_CI_AS  NULL,
  [schema_option] binary(8)  NULL,
  [dest_owner] sysname  NULL,
  [ins_scripting_proc] int  NULL,
  [del_scripting_proc] int  NULL,
  [upd_scripting_proc] int  NULL,
  [custom_script] nvarchar(2048) COLLATE Chinese_PRC_CI_AS  NULL,
  [fire_triggers_on_snapshot] bit DEFAULT ((0)) NOT NULL
)
GO

ALTER TABLE [dbo].[sysarticles] SET (LOCK_ESCALATION = TABLE)
GO


-- ----------------------------
-- Auto increment value for sysarticles
-- ----------------------------
DBCC CHECKIDENT ('[dbo].[sysarticles]', RESEED, 1)
GO
```

```sql
CREATE TABLE [dbo].[sysschemaarticles] (
  [artid] int  NOT NULL,
  [creation_script] nvarchar(255) COLLATE Chinese_PRC_CI_AS  NULL,
  [description] nvarchar(255) COLLATE Chinese_PRC_CI_AS  NULL,
  [dest_object] sysname  NOT NULL,
  [name] sysname  NOT NULL,
  [objid] int  NOT NULL,
  [pubid] int  NOT NULL,
  [pre_creation_cmd] tinyint  NOT NULL,
  [status] int  NOT NULL,
  [type] tinyint  NOT NULL,
  [schema_option] binary(8)  NULL,
  [dest_owner] sysname  NULL
)
GO

ALTER TABLE [dbo].[sysschemaarticles] SET (LOCK_ESCALATION = TABLE)
GO
```
