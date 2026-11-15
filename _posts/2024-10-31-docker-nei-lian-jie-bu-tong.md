---
title: "docker内程序连其他程序不通"
date: 2024-10-31 19:18:02 +0800
---

问题：docker容器连不上某个IP端口

调查：

```bash
docker exec <container_id_or_name> ping -c 3 <服务器IP>

docker exec <container_id_or_name> curl <服务器IP>:<port>
```

还可以进容器：

```bash
docker exec -it <container_id_or_name> /bin/bash
```
