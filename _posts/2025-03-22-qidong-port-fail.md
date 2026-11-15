---
title: 启动程序时监听端口失败
date: 2025-03-22 +0800
---
问题：启动程序时监听端口失败

解决：使用软件看下是哪个进程占用的，比如：[CurrPorts: Monitoring TCP/IP network connections on Windows](https://www.nirsoft.net/utils/cports.html#google_vignette)

80端口的话，可以看看IIS默认站点，服务BrandCache,可以运行这个脚本看看

```bash
netsh http show urlacl
```
