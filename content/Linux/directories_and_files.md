---
title: "directories_and_files 目录和文件"
date: 2018-10-22 03:20
---


[TOC]


# 目录



## proc

反应了内核和进程树的各种文件，其挂载的是在内核中映射的一块区域



随机字符串

```
cat /proc/sys/kernel/random/uuid  | cut -c 1-8
1f842195
```



### PID目录

目录名称为进程ID信息



## /var/log/

日志相关信息









# 文件



## libc.so.6

/lib64/libc.so.6 是重要依赖的库文件，删除后很多命令无法使用，包括关机都无法执行。

重启会卡在登录界面。

需要进入救援模式来恢复





## /var/log/lastlog

最近登录成功事件



## /var/log/utmp

当前机器登录的全部用户的日志



## /var/log/wtmp

系统创建以来登录过的用户

