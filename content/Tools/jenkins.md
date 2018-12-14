---
title: "jenkins"
date: 2018-10-16 11:04
---


[TOC]


# jenkins

jenkins是一个广泛用于持续构建的可视化web工具，持续构建说得更直白点，就是各种项目的"自动化"编译、打包、分发部署。jenkins可以很好的支持各种语言（比如：java, c#, php等）的项目构建，也完全兼容ant、maven、gradle等多种第三方构建工具，同时跟svn、git能无缝集成，也支持直接与知名源代码托管网站，比如github、bitbucket直接集成。



## requirements

```
256 MB RAM
1GB space

Java 8
Java Runtime Environment or Java Development Kit
```

Docker Hardware

```
1GB RAM
10GB space
```



## 安装

### docker

```
docker pull jenkins/jenkins:lts
docker run --detach --publish 8080:8080: --volumn jenkins_home:/var/jenkins_home --name jenkins jenkins/jenkins:lts

docker exec jenkins cat /var/jenkins_home/secrets?initialAdminPassword
```







### Ubuntu 

WAR file 

The Web application ARchive (WAR) file version of Jenkins can be installed on any operating system or platform that supports Java.

```
apt install default-jre
sudo apt-get install openjdk-8-jdk
sudo update-alternatives --config java (set to java 8)

wget http://mirrors.jenkins.io/war-stable/latest/jenkins.war
```

```
[Unit]
Description=Jenkins Daemon

[Service]
ExecStart=/usr/bin/java -jar /home/jenkins_user/jenkins.war
User=jenkins_user

[Install]
WantedBy=multi-user.target
```



/etc/systemd/system/jenkins.service

```
[Unit]
Description=Jenkins Daemon

[Service]
ExecStart=/usr/bin/java -jar /home/jenkins_user/jenkins.war
User=jenkins_user

[Install]
WantedBy=multi-user.target
```

```
systemctl start jenkins.service     
systemctl stop jenkins.service
systemctl restart jenkins.service
systemctl enable jenkins.service                                      
systemctl disable jenkins.service 
```

Browse to `http://localhost:8080` and wait until the **Unlock Jenkins** page appears





## Plugins

### Email extension & Extended E-mail Notification

```
smtp.163.com
username
password  #这里是163的授权码
smtp port 25 
```





### Role-based Authorization Strategy (用户权限)

Installed and then go to "Configure Global Security"

```
Authorization -> Role-Based Strategy -> Apply -> Save
```



Go to 'Manage and Assign Roles'



## 自动部署





## Pipline 

Jenkins 上的工作流程框架，将原本独立运行于单个或者多个节点的任务连接起来，实现单个任务难以完成的复杂流程编排与可视化



### 语法

