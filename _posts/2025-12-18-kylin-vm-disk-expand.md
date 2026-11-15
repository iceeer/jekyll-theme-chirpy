---
title: 麒麟虚拟机原盘扩容后没看到
date: 2025-12-18 16:26:18 +0800
---
问题：麒麟虚拟机原盘扩容后没看到

解决：

lsblk  
fdisk -l  
df -Th  
blkid

fdisk /dev/sda

partprobe  
pvcreate /dev/vda6  
vgextend klas /dev/vda6

lvextend -l +100%FREE /dev/mapper/klas-root #全部分配/root分区

xfs_growfs /dev/mapper/klas-root

参考链接：[https://blog.51cto.com/dongjianting/4916661](https://blog.51cto.com/dongjianting/4916661 "https://blog.51cto.com/dongjianting/4916661")
