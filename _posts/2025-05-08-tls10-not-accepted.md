---
title: The server selected protocol version TLS10 is not accepted by client preferences
date: 2025-05-08 +0800
---

问题：Caused by: com.microsoft.sqlserver.jdbc.SQLServerException: The driver could not establish a secure connection to SQL Server by using Secure Sockets Layer (SSL) encryption. Error: "The server selected protocol version TLS10 is not accepted by client preferences [TLS13, TLS12]". ClientConnectionId:3e6bec4d-2d56-41b2-bb62-9ef3a895cd6d

解决：修改/opt/jdk1.8.0_441/jre/lib/security/java.security

jdk.tls.disabledAlgorithms去掉, TLSv1, TLSv1.1
