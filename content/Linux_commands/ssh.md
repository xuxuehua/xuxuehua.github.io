---
title: "ssh"
date: 2018-08-07 11:50
---

[TOC]



# ssh 

## -1 
强制使用ssh协议版本1


## -2 
强制使用ssh协议版本2


## -4 
强制使用IPv4地址


## -6 
强制使用IPv6地址


## -A 
开启认证代理连接转发功能


## -a 
关闭认证代理连接转发功能


## -b 
使用本机指定地址作为对应连接的源ip地址


## -C 
请求压缩所有数据


## -F 
指定ssh指令的配置文件


## -f 
后台执行ssh指令


## -g 
允许远程主机连接主机的转发端口


## -i 
指定身份文件


## -l 
指定连接远程服务器登录用户名


## -N 
不执行远程指令


## -o 
指定配置选项


## -p 
指定远程服务器上的端口


## -q 
静默模式


## -X 
开启X11转发功能


## -x 
关闭X11转发功能


## -y 
开启信任X11转发功能



## -o option 配置选项

指定配置选项

Can be used to give options in the format used in the configuration file.  This is useful for specifying options for which there is no separate command-line flag



### StrictHostKeyChecking

Automatically accept keys

```
ssh -oStrictHostKeyChecking=no $h 
```



### ProxyCommand (Case sensitive)

```
ssh -o "ProxyCommand nc --proxy-type socks5 --proxy 127.0.0.1:9050 %h %p" <target_host>
```

To do it on a per-host basis, edit your ~/.ssh/config to look something like this:

```
host example.com
    user bar
    port 22
    ProxyCommand nc --proxy-type socks5 --proxy 127.0.0.1:9050 %h %p
```



Add this to your ssh config file (`~/.ssh/config`):

```
host *
     CheckHostIP  no
     Compression  yes
     Protocol     2
     ProxyCommand connect -4 -S localhost:9050 $(tor-resolve %h localhost:9050) 
%p
```

