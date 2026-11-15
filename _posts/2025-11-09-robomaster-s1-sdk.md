---
title: Robomaster S1更新后没有sdk功能了
date: 2025-11-09 16:12:56 +0800
---
问题：Robomaster S1更新后没有sdk功能了

处理：当前固件版本：00.06.0521

试一下连机器人IP的40923端口通不通，不通那就是不能用sdk控制机器人了，需要破解下

先准备一根USB数据线（别用只能充电的充电线）

用robomaster客户端，实验室，写一段python运行，运行完别管客户端

```python
def root_me(module):

    __import__=rm_define.__dict__['__builtins__']['__import__']

    return __import__(module,globals(),locals(),[],0)

builtins=root_me('builtins')

sub_process=root_me('sub'+'process')

proc=sub_process.Popen('/system/bin/adb_en.sh',shell=True,executable='/system/bin/sh',stdout=sub_process.PIPE,stderr=sub_process.PIPE)
```

然后USB连上机器人，使用andorid sdk中的adb运行命令

adb.exe devices 看连没连山

然后运行一堆命令，附件资料里有说明

```bash
adb shell rm -rf /data/dji_scratch/sdk

adb push dji_scratch/sdk /data/dji_scratch/.

adb push dji_scratch/bin/dji_scratch.py /data/dji_scratch/bin/.

adb push dji.json /data/.

adb push dji_hdvt_uav /data/.

adb shell chmod 755 /data/dji_hdvt_uav

adb push patch.sh /data/.
```

然后就是重启机器人

然后就可以用sdk试试了

链接：

[RoboMaster-SDK Github](https://github.com/dji-sdk/RoboMaster-SDK "RoboMaster-SDK Github")

[RoboMaster Developer Guide 文档](https://robomaster-dev.readthedocs.io/zh-cn/latest/introduction.html "RoboMaster Developer Guide 文档")

[S1 fw downgrade to get sdk](https://www.reddit.com/r/ROBOMASTER/comments/1lbc4a6/s1_fw_downgrade_to_get_sdk/ "S1 fw downgrade to get sdk")

[Robomaster S1 SDK Hack](https://www.reddit.com/r/RobomasterS1/comments/lwx45c/robomaster_s1_sdk_hack/ "Robomaster S1 SDK Hack")
