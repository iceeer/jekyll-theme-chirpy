---
title: 达梦dm.key放好了还授权无效
date: 2024-10-31 19:12:00 +0800
---

问题：授权不成功

处理：

看日记  
/opt/dmdbms/log/dm_unknown_**.log

[WARNING] database **** file dm.key not found, use default license!

可能是文件dm.key权限不够，使用chmod修改下权限
