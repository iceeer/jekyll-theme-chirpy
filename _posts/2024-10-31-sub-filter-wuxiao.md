---
title: sub_filter无效解决
date: 2024-10-31 19:12:42 +0800
---

问题：nginx中设置了sub_filter无效

解决：第一次反代时增加gzip off;设置项，以输出无压缩的内容，第二次反代sub_filter就能生效了
