---
title: linux查java进程CPU高的原因
date: 2025-05-07 +0800
---

问题：linux查java进程CPU高的原因

解决：用jdk带的工具分析，被查的java最好也使用jdk启动；systemctl启动的注意要去掉PrivateTmp=true

```bash
/opt/jdk1.8.0_441/bin/jps -l
top -Hp 8156
printf "%x" 8533
/opt/jdk1.8.0_441/bin/jstack 8156 | grep 2155 -A 10
```

参考：[https://zhuanlan.zhihu.com/p/669221763](https://zhuanlan.zhihu.com/p/669221763)
