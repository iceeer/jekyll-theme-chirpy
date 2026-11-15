---
title: Windows系统安装arm麒麟系统
date: 2025-09-29 12:32:08 +0800
---

问题：Windows系统安装arm麒麟系统

处理：

下载[qemu](https://qemu.weilnetz.de/w64/ "qemu")并安装

下载[AArch64 UEFI固件镜像](https://releases.linaro.org/components/kernel/uefi-linaro/16.02/release/qemu64/ "AArch64 UEFI固件镜像")

下载[ARM版麒麟系统](https://iso.kylinos.cn/web_pungi/download/cdn/ni3tIfZoEKLDglszRXvh9WymuwOT5r6M/Kylin-Server-V10-SP3-2403-Release-20240426-arm64.iso "ARM版麒麟系统")，其他版本：[https://sl.ygwid.cn/](https://sl.ygwid.cn/ "https://sl.ygwid.cn/")

```cobol
qemu-img.exe create -f raw D:\QVM\kylin_arm64.img 100G

qemu-system-aarch64.exe -m 4G -cpu cortex-a72 --accel tcg,thread=multi -M virt -bios D:\QVM\QEMU_EFI.fd -rtc base=localtime -display sdl -device VGA -device nec-usb-xhci -device usb-tablet -device usb-kbd -drive if=virtio,file=D:\QVM\kylin_arm64.img,id=hd0,format=raw,media=disk -drive if=none,file=D:\QVM\Kylin-Server-V10-SP3-2403-Release-20240426-arm64.iso,id=cdrom,media=cdrom -device virtio-scsi-device -device scsi-cd,drive=cdrom 
```

运行（注意：麒麟默认可能没连网）

```cobol
qemu-system-aarch64.exe -m 4G -cpu cortex-a72 --accel tcg,thread=multi -M virt -bios D:\QVM\QEMU_EFI.fd -rtc base=localtime -display sdl -device VGA -device nec-usb-xhci -device usb-tablet -device usb-kbd -drive if=virtio,file=D:\QVM\kylin_arm64.img,id=hd0,format=raw,media=disk -device virtio-scsi-device  -net nic,model=virtio -net user,hostfwd=tcp::2222-:22
```

然后就可以ssh连接127.0.0.1端口2222

参考：[Windows x64系统上安装麒麟Arm64系统虚拟机](https://mp.weixin.qq.com/s/8plXlR9MUTmnkjqzgckekA "Windows x64系统上安装麒麟Arm64系统虚拟机")
