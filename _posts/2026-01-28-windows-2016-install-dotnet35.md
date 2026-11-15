---
title: Windows 2016安装.net 3.5
date: 2026-01-28 14:30:16 +0800
---

问题：Windows 2016安装SQL Server 2012时 提示缺.net 3.5。

处理：拷贝NetFx3.cab到windows目录下，执行命令

```bash
dism /online /Enable-Feature /all /FeatureName:NetFx3 /Source:"%windir%" /LimitAccess
```
