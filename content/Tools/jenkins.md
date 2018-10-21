---
title: "jenkins"
date: 2018-10-16 11:04
---


[TOC]


# jenkins

jenkins是一个广泛用于持续构建的可视化web工具，持续构建说得更直白点，就是各种项目的"自动化"编译、打包、分发部署。jenkins可以很好的支持各种语言（比如：java, c#, php等）的项目构建，也完全兼容ant、maven、gradle等多种第三方构建工具，同时跟svn、git能无缝集成，也支持直接与知名源代码托管网站，比如github、bitbucket直接集成。



## 安装

### Ubuntu 

WAR file 

The Web application ARchive (WAR) file version of Jenkins can be installed on any operating system or platform that supports Java.

```
apt install default-jre
wget http://mirrors.jenkins.io/war-stable/latest/jenkins.war

java -jar jenkins.war
```

Browse to `http://localhost:8080` and wait until the **Unlock Jenkins** page appears



## Plugins


![img](https://images2015.cnblogs.com/blog/27612/201601/27612-20160118095859045-743552984.png)

![img](https://images2015.cnblogs.com/blog/27612/201601/27612-20160118193702109-1177684936.png)

![img](https://images2015.cnblogs.com/blog/27612/201601/27612-20160118223147422-362207840.png)





