---
title: windows时间不对
date: 2024-11-15 +0800
---
问题：

处理：

配置与时间服务器同步

检查时间是否和时间同步服务器一致

```bash
w32tm /stripchart /computer:time.windows.com /samples:30
```

强制同步

```bash
w32tm /resync
```

如果是虚拟机，还要看下虚拟机所在的主机时间
