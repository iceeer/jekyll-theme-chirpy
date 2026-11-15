---
title: 达梦SYADBA用户创建物化视图失败
date: 2025-12-31 09:18:38 +0800
---
问题：达梦SYADBA用户创建物化视图失败

解决：先排除SYSDBA在这个数据库服务器没有这个权限，然后运行

```sql
GRANT CREATE MATERIALIZED VIEW TO <DBNAME>;

GRANT CREATE TABLE TO <DBNAME>;
```

SYSDBA再运行创建物化视图，还不行看看数据库所有者，用所有者登录再创建试试
