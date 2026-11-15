---
title: "ERROR 2002 (HY000) Can't connect to local MySQL server through socket"
date: 2024-11-04 +0800
---
错误：允许mysql -u root -p报错

ERROR 2002 (HY000): Can't connect to local MySQL server through socket '/var/lib/mysql/mysql.sock'

处理：是不是mysql不是安装再本机

通过docker安装的话，试试进容器

```bash
docker exec -it /bin/bash
```

再运行mysql -u root -p，有时候docker安装后默认设置了root只能localhost登录，也可以进入docker后连接
