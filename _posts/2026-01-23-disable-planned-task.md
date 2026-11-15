---
title: 禁用计划任务提示没有禁用此任务的权限
date: 2026-01-23 09:15:52 +0800
---
问题：禁用计划任务提示没有禁用此任务的权限

处理：

cmd管理员运行，使用Sysinternals PsTools工具包中的psexec.exe以SYSTEM权限运行任务计划程序

```bash
psexec.exe -i -s %windir%\system32\mmc.exe /s taskschd.msc
```
