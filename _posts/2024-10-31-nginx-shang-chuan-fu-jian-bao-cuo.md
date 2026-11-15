---
title: "通过nginx反向代理后上传附件报错"
date: 2024-10-31 19:16:38 +0800
---

错误："POST /api/system/file/upload HTTP/1.1" 500

[crit] 1672941#0: *91516 open() "/var/lib/nginx/tmp/client_body/0000000045" failed (13: Permission denied)

解决：

```bash
cd /var/lib

chmod -R 755 nginx
```

没文件夹的话创建下文件夹
