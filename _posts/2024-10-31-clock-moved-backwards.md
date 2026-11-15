---
title: "Clock moved backwards. Refusing to generate id for xxx milliseconds"
date: 2024-10-31 19:15:01 +0800
---

错误：Clock moved backwards. Refusing to generate id for xxx milliseconds

![图片](https://i-blog.csdnimg.cn/direct/5ca00d4779674c7ba19a7eac62804e84.png)

处理：

```cobol
tail -n 100 /var/log/syslog  # Ubuntu和Debian系统

tail -n 100 /var/log/messages  # CentOS和Red Hat系统
```

```csharp
timedatectl #看看是否开启同步
```

![图片](https://i-blog.csdnimg.cn/direct/c02c2847cc4c40f39808320f61a19ef2.png)

看看有没有和时间服务器同步，关闭后再观察

如果是虚拟机的话，看看是不是虚拟机主机时间有问题同步导致的，关闭后再观察
