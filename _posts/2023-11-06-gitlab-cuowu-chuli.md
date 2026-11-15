---
title: Gitlab错误处理
date: 2023-11-06 09:00:00 +0800
---

```cobol
ActionView::Template::Error (undefined method `gsub' for nil:NilClass):
领2年VIP
```

应该是集成了youtrack导致的，系统管理关闭youtrack集成，项目里以前开的也要一个个关掉

升级失败：gitlab-rake db:migrate:status  
gitlab-rake db:migrate  
启动服务：gitlab-ctl reconfigure  
查看日志：gitlab-ctl tail  
查看日志文件 /var/log/gitlab/gitlab-rails/production.log  
修改配置文件：vim /etc/gitlab/gitlab.rb  
检查gitlab：gitlab-rake gitlab:check SANITIZE=true --trace  
查看版本：cat /opt/gitlab/embedded/service/gitlab-rails/VERSION
