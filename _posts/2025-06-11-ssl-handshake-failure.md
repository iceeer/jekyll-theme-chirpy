---
title: "javax.net.ssl.SSLHandshakeException Received fatal alert handshake_failure"
date: 2025-06-11 +0800
---

问题：连https网站出错javax.net.ssl.SSLHandshakeException: Received fatal alert: handshake_failure

解决：

替换美国jdk的限制，找到文件夹jdk1.8.0_202\jre\lib\security下的local_policy.jar、US_export_policy.jar，替换为下面的附件
