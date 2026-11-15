---
title: 删文件提示系统找不到指定的文件
date: 2025-06-25 +0800
---

问题：系统找不到指定的文件

解决：

```bat
DEL /F /A /Q \\?\D:\test_folder
RD /S /Q \\?\D:\test_folder
```
