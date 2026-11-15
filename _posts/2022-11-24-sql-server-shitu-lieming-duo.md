---
title: SQL Server 为视图或函数 指定的列名比其定义中的列多
date: 2022-11-24 20:49:08 +0800
---

问题：com.microsoft.sqlserver.jdbc.SQLServerException: 为视图或函数 指定的列名比其定义中的列多。

原因：因为修改了表字段（新增、移除、修改），并且视图或函数中使用了 select * 的语法

解决方案： 删除视图或函数
