---
title: "绿盟扫描漏洞处理"
date: 2024-10-31 19:20:05 +0800
---

漏洞：检测到目标主机可能存在缓慢的HTTP拒绝服务攻击

处理：限制超时时间

node.js

```js
server.setTimeout(60000);//升级node.js
```

java

```bash
-Dserver.connection-timeout=10000 -Dserver.tomcat.connection-timeout=10000 -Dspring.mvc.async.request-timeout=10000
-Dserver.undertow.connection-timeout=10000
```

nginx

```nginx
client_body_timeout 10;
client_header_timeout 10;
keepalive_timeout 65;
keepalive_requests 10;
proxy_connect_timeout 300;
proxy_send_timeout 300;
proxy_read_timeout 300;
send_timeout 300;
```

漏洞：SSL/TLS协议信息泄露漏洞(CVE-2016-2183)、SSL/TLS RC4 信息泄露漏洞(CVE-2013-2566)、SSL/TLS 受诫礼(BAR-MITZVAH)攻击漏洞(CVE-2015-2808)

处理：运行[Nartac Software - IIS Crypto](https://www.nartac.com/Products/IISCrypto)，选择推荐方案重启服务器

漏洞：Alibaba Druid 未授权访问

处理：

```bash
-Dspring.datasource.druid.stat-view-servlet.allow:="127.0.0.1"
```

漏洞：检测到目标URL存在http host头攻击漏洞

处理：

nginx

```nginx
if ($host !~ ^(127.0.0.1|192.168.1.100)$ )
{
    return 444;
}
if ($http_Host !~ ^(127.0.0.1|192.168.1.100)$ )
{
    return 444;
}
```

iis

绑定下IP

java

```bash
-Dserver.address="127.0.0.1"
```

*还有一种统一的解决方案就是让它扫不到，通过防火墙限制，或者修改绑定的IP（比如Java：-Dserver.address="127.0.0.1"）
