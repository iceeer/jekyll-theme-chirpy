---
title: 更新麒麟连不上外网
date: 2025-06-23 +0800
---

问题：更新麒麟连不上外网

处理：本地建个下载地址

建立文件夹/root/x86.rpm，子文件夹：Packages、repodata，和在线站点建的一样：[Index of /NS/V10/V10SP1.1/os/adv/lic/base/x86_64/](https://update.cs2c.com.cn/NS/V10/V10SP1.1/os/adv/lic/base/x86_64 "Index of /NS/V10/V10SP1.1/os/adv/lic/base/x86_64/")，然后就下载这两个文件夹里的文件，repodata都下载，Packages按需下载。

然后在/etc/yum.repos.d建个文件local.repo

```ini
[local]
name=Kylin-Local
baseurl=file:///root/x86.rpm
enabled=1
gpgcheck=0
```
