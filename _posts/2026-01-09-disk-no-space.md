---
title: 磁盘没空间
date: 2026-01-09 11:06:08 +0800
---
问题：磁盘没空间

处理：

清理不用的文件

```bash
del /f/q/s %TEMP%

del /f/q/s %TMP%
```

把文件夹移到其他盘，然后创建符号链接

```bash
echo 创建文件软链接示例:

mklink "C:\Test1.txt" "D:\Test2.txt"

echo 创建目录软链接示例:

mklink /D "C:\Test1" "D:\Test2"
```

查链接到哪了：fsutil reparsepoint query C:\Test1

删除链接：rmdir /s /q C:\Test1
