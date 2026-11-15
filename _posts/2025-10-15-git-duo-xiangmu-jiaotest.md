---
title: 查多个项目有没有git提交测试代码
date: 2025-10-15 15:33:46 +0800
---

问题：查多个项目有没有git提交测试代码

```cobol
@echo on

echo [INFO] Search git commit

cd %~dp0

set "CURRENT_DIR=%cd%"

del pull.log

del commit.log

SET DT="2025-10-01"

cd D:\data\project\xxx

git pull >> %CURRENT_DIR%\pull.log

git log --since=%DT% --name-only   -- src/test >> %CURRENT_DIR%\commit.log

git log --since=%DT% --name-only   -- src/test >> %CURRENT_DIR%\commit.log

git log --since=%DT% --name-only   -- src/test >> %CURRENT_DIR%\commit.log

cd D:\data\project\aaa

git pull >> %CURRENT_DIR%\pull.log

git log --since=%DT% --name-only   -- yy/src/test >> %CURRENT_DIR%\commit.log

git log --since=%DT% --name-only   -- yy/src/test >> %CURRENT_DIR%\commit.log

git log --since=%DT% --name-only   -- yy/src/test >> %CURRENT_DIR%\commit.log
```
