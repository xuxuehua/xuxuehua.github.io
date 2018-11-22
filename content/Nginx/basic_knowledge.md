---
title: "basic_knowledge"
date: 2018-11-20 12:34
---


[TOC]


# basic_knowledge



## 特点

Apache，一个进程，同一时间只会处理一个连接一个请求



* 高并发
* 可扩展性和高可用性
* 热部署： 不停止服务的情况下，部署配置
* BSD许可证，可以更改代码



## 组成

### 二进制可执行文件

各个模块源码编译出的一个文件



### nginx.conf 配置文件

控制nginx 行为



### access.log 

记录http请求信息



### error.log

定位问题





## 版本

nginx-1.14.0 

nginx-1.15.5 

> 偶数版本比较稳定 1.14





## 安装

### 包管理工具

安装rpm或deb会将模块安装上去



### 编译安装

```
elinks http://nginx.org/en/download.html
tar -xzf nginx-1.14.1.tar.gz
```





#### 目录结构

```
auto # 辅助conf 告诉nginx 支持哪些模块
CHANGES  # 变更信息
CHANGES.ru # 俄语变
conf # 事例文件
configure # 编译前的配置 
contrib # 将配置文件带上颜色， cp -r contrib/vim/* ~/.vim
html # 标准的html文件，基本配置
LICENSE
man # 帮助文件
README
src # 源码
```

