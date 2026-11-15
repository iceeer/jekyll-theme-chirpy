---
title: 初始项目时gradle下载失败
date: 2025-07-04 13:49:42 +0800
---

问题：初始项目时gradle下载失败

解决：修改项目下`\gradle\wrapper\gradle-wrapper.properties`中

`https\://services.gradle.org/distributions/`

改为

`https\://mirrors.cloud.tencent.com/gradle/`

也可以手动下载，解压缩至`C:\Users\<你的用户名>\.gradle\wrapper\dists\gradle-<版本>-<类型>\<随机字符串>\`
