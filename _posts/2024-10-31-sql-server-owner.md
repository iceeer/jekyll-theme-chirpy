---
title: "SQL Server属性 Owner 不可用于 数据库"
date: 2024-10-31 19:22:37 +0800
---

问题：SQL Server属性 Owner 不可用于 数据库

解决：

```sql
exec sp_changedbowner 'sa'
```
