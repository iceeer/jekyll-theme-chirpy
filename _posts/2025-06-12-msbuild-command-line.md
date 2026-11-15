---
title: msbuild
date: 2025-06-12 +0800
---

问题：不想打开VS构建VS项目

解决：

```bat
call "msbuild.exe"  project.sln /p:Configuration=Debug /l:FileLogger,Microsoft.Build.Engine;logfile=Manual_MSBuild_DebugVersion_LOG.log
```

msbuild默认可能不在PATH里，需要加下环境变量PATH，加上C:\Program Files\Microsoft Visual Studio\2022\Enterprise\MSBuild\Current\Bin，具体按照VS版本加
