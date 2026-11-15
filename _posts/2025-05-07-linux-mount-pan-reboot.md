---
title: linux下挂载的盘重启后没了
date: 2025-05-07 +0800
---
问题：linux下挂载的盘重启后没了

解决：mount只是临时的

需要修改/etc/fstab

添加UUID=87ee3580-39cd-4b8c-a1f4-d77568b0accf /data xfs defaults 0 0

UUID通过blkid命令获取

验证：mount -a然后看df -h
