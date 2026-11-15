---
title: VS新版本不让安装.net4.0
date: 2025-12-23 21:38:10 +0800
---
问题：VS新版本不让安装.net4.0

解决：下载nuget的包，后缀改成zip后解压缩，然后拷到C:\Program Files (x86)\Reference Assemblies\Microsoft\Framework\.NETFramework

[4.0链接](https://www.nuget.org/api/v2/package/Microsoft.NETFramework.ReferenceAssemblies.net40/1.0.3 "4.0链接")

[4.5链接](https://www.nuget.org/api/v2/package/Microsoft.NETFramework.ReferenceAssemblies.net45/1.0.3 "4.5链接")
