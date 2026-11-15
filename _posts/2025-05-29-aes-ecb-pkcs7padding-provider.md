---
title: Cannot find any provider supporting AES/ECB/PKCS7Padding
date: 2025-05-29 +0800
---

问题：Cannot find any provider supporting AES/ECB/PKCS7Padding

解决：

一般是说改%JAVA_HOME%\jre\lib\security中security.provider.7行，并将其值修改为org.bouncycastle.jce.provider.BouncyCastleProvider

还不行，再改下这个试试

jdk.jar.disabledAlgorithms=MD2, MD5, RSA keySize < 1024, DSA keySize < 1024
