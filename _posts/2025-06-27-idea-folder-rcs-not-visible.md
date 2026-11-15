---
title: 项目里建了个文件夹rcs，但是IDEA里看不到这个文件夹
date: 2025-06-27 +0800
---

问题：项目里建了个文件夹rcs，但是IDEA里看不到这个文件夹

建包名叫rcs时报错Trying to create a package with an ignored name ('rcs’); the result will not be visible

解决：IDEA 设置File -> File Types > Ignored Files and Folders，然后移除"rcs"
