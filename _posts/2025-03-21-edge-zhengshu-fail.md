---
title: Edge打不开证书失效的网站
date: 2025-03-21 +0800
---
错误：Edge打不开证书失效的网站

处理：Edge快捷方式加上参数

```bash
--test-type --ignore-certificate-errors --disable-web-security --user-data-dir
```

不生效的话看看edge进程有没有都关闭，打开 edge://version 看看参数加上了没
