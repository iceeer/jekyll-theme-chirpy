---
title: VMWare内NAT方式连接的虚拟机网连不上
date: 2025-03-22 +0800
---
问题：VMWare内NAT方式连接的虚拟机网连不上

解决：重启服务VMware NAT Service

```bash
net stop "VMware NAT Service" && net start "VMware NAT Service"
```
