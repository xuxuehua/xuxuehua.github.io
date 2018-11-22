---
title: "iptables"
date: 2018-11-21 09:37
---


[TOC]


# iptables

Linux 下的网络防火墙



## Packages

### IPV4

![img](https://cdn.pbrd.co/images/HO7KqdW.png)

Total Length：整个报文的总长度 

Fragment ID： 分片信息 

DF：Don't fragment 

MF: More fragment 

Fragment Offset: 片偏移，即对报文排序 



### TCP Header

![img](https://cdn.pbrd.co/images/HO7L0L1.png)



Squence Number: 发送方告诉接收方的编号 

Acknowledgement Number：序列号加1，回复给对方 

Windows Size：报文的缓冲大小 

URG: 紧急指针，1表示有效，0无效 

ACK：确认号是否有效 

PSH：优先处理的保温 

RST：连接抖动 

SYN：同步请求 

FIN: 断开连接 



#### TCP 有限状态机

![img](https://cdn.pbrd.co/images/HO7Muu7.png)









### NAT

NAT  Network Address Translation 



DNAT：目标地址转换(PREROUTING) 

目标地址转换：刚刚进来的时候改 



SNAT：源地址转换(POSTROUTING, OUTPUT) 

源地址转换：在出去的时候改 



```
iptables -t nat -A POSTROUTING -s 10.76.0.0/16 -j SNAT --to-source 172.16.100.1
iptables -t nat -A POSTROUTING -s 192.168.0.0/16 -j SNAT --to-source 123.2.3.2 (SNAT Translation for public IP 123.2.3.2)

-j SNAT
     --to-source

-j MASQUERADE (除非外网地址是动态的，效率比SNAT要低)

iptables -A FORWARD -s 192.168.0.0/16 -p icmp -j REJECT

iptables -P FORWARD DROP
iptables -A FORWARD -m state --state ESTABLISHED -j ACCEPT
iptables -A FORWARD  -s 192.168.10.0/24 -p tcp --dport 80 -m state --state NEW -j ACCEPT
iptables -A FORWARD -s 192.168.10.0/24 -p icmp -icmp-type 8 -m state --state NEW -j ACCEPT
iptables -A FORWARD  -s 192.168.10.0/24 -p tcp --dport 21 -m state --state NEW -j ACCEPT
iptables -R FORWARD 1 -m state --state ESTABLISHED,RELATED -j ACCEPT (make sure /etc/sysconfig/iptables-config has module of "ip_nat_ftp, ip_conntrack_ftp")



-j DNAT
     --to-destination
          iptables -t nat -A PREROUTING -d 172.16.100.7 -p tcp --dport 80 -j DNAT --to-destination 192.168.10.22

PNAT  Port NAT
         iptables -t nat -R PREROUTING -d 1272.16.100.7. -p tcp --dport 80 -j DNAT --to-destination 192.168.10.22:8080
     
iptables -A FORWARD -m string --algo kmp --string "h7n9" -j DROP
```



## 处理流程

![img](https://cdn.pbrd.co/images/HO9C8yU.png)





## 规则链

hook function  钩子函数 

```
prerouting -> PREROUTING 
input ->  INPUT
output ->  OUTPUT
forward ->  FORWARD
postrouting ->  POSTROUTING
```

​          

### 自定义链

可以使用自定义链，但只在被调用的时候才能发挥作用，而且如果没有自定义链中的任何规则匹配，还应该有返回机制： 

​     用可以删除自定义的空链 

​     默认链无法删除 



## 匹配表

### filter

```
INPUT 
OUTPUT 
FORWARD 
```

### NAT

```
PREROUTING 
OUTPUT 
POSTROUTING 
```



### mangle

拆开，修改，再封装

```
PREROUTING 
INPUT 
OUTPUT 
FORWARD 
POSTROUTING 
```



### raw

```
PREROUTING 
OUTPUT 
```





## SYNOPSIS

```
iptables [-t TABLE] COMMAND CHAIN [num] 匹配标准 -j 处理办法
```





## 匹配标准 

IP：源IP， 目标IP 

TCP: SPORT, DPORT,          SYN=1, FIN=0, RST=0, ACK=0; SYN=1, ACK=1, FIN=0, RST=0; ACK=1,  SYN=0, RST=0, FIN=0(ESTABLISHED)  

UDP: SPORT, DPORT 

ICMP: icmp-type 





### 通用匹配 

```
-s, --src  

-d, --dst 

-p, {icmp|tcp|udp} 指定协议 

-i, INTERFACE: 指定数据报文流入的接口 

	可用于定义标准的链：PREROUTING, INPUT, FORWARD 

-o, INTERFACE: 指定数据报文流出的接口 

	可用于定义标准的链：OUTPUT, POSTROUTING, FORWARD 
```





### 扩展匹配

不用特别指明由哪个模块进行扩展，因为使用了-p {tcp|udp|icmp} 

```
-p tcp 

	--sport PORT [-PORT]: 源端口 

	--dport PORT [-PORT]：目标端口 

	--tcp-flags mask comp: 只检查mask指定的标志位，是逗号分隔的标志位列表；comp：此列表中的标记为必须为1，comp中没出现，而mask中出现的， 则必须为0； 

	--tcp-flags SYN, FIN, ACT, RST SYN, ACK == --syn 

	--syn 

-p icmp 

	--icmp-type      

	0 echo-reply 回显应答 

	8 echo-request 回显请求 


-p udp 

	--dport 

	--sport  
```



### 显式扩展

 （使用额外的匹配机制）：必须指明由哪个模块进行的扩展，在iptables中使用-m选项可以完成此功能

```

-m EXTENSION --spe-opt

state: 状态扩展
     结合ip_conntract 追踪会话的状态
          NEW：新连接请求
          ESTABLISHED：已建立的连接
          INVALID：非法连接
          RELATED：相关联的
          -m state --state NEW, ESTABLISHED -j ACCEPT

          iptables -A INPUT -d 10.76.33.201 -p tcp -m state --state ESTABLISHED

     multiport: 离散的多端口匹配扩展
          --source-ports
          --destination-ports
     -m multiport --destination-ports 21,22,80 -j ACCEPT

     -m iprange
          --src-range
          --dst-range 

          -s, -d 
          -s IP, NET
                   10.76.0.0/16, 10.76.33.201-10.76.33.254

          iptables -A INPUT -p tcp -m iprange --src-range 10.76.33.201-10.76.33.254 --dport 22 -m state --state NEW,ESTABLISHED -j ACCEPT

      -m connlimit 连接数限制
            ! --connlimit-above n  (一般加上！)  
                  iptables -A INPUT -d 10.76.33.201 -p tcp --dport 80 -m connlimit ! --connlimit-above 2 -j ACCEPT

      -m limit
             --limit   RATE   速率
                  iptables -R INPUT 6 -d 10.76.33.201 -p icmp --icmp-type 8 -m limit --limit 5/minute -j ACCEPT
             --limit-burst   6   连接会被重置
                  iptables -R INPUT 5 -d 10.76.33.201 -p icmp --icmp-type 8 -m limit --limit 5/minute --limit-burst 6 -j ACCEPT

      -m string 
            --algo {bm|kmp}
            --string "STRING"
                    iptables -I OUTPUT -s 10.76.33.201 -m string --algo kmp --string "h7n9" -j REJECT 
```

​           

## 处理办法

-j   TARGET 

​     ACCEPT 

​     DROP 

​     REJECT 

​     LOG   记录日志信息 

​          --log-prefix "STRING" 

​            iptables -I INPUT 6 -d 10.76.33.201 -p icmp --icmp-type 8 -j LOG --log-prefix "-- firewall log for icmp --" 

​           



## iptables 管理

### 管理规则

​          -A： 附加一条规则，添加在链的尾部 

​           -I：CHAIN [num]：插入一条规则，插入为对应CHAIN上的第num条 

​           -D：CHAIN [num]：删除指定链中的第num条规则 

​           -R：CHAIN [num]：替换指定的规则   

### 管理链

​          -F [CHAIN]： flush， 清空指定链中的规则， 如果省略CHAIN， 则可以实现删除对应表中的所有链 

​          -P CHAIN： 设定指定链的默认策略 

​          -N： 自定义一个新的空链 

​          -X：删除一个自定义的空链 

​          -Z： 置零指定链中所有规则的计数器 

​          -E： 重命名自定义的链 

### 查看类

​          -L： 显式指定表中的所有规则 

​               -n：以数字格式显示主机地址和端口号 

​               -v： 显示链及规则的详细信息 

​               -v v： 

​               -x：显示计数器的精确值 

​               --line-numbers：显式规则号码 





### 动作（target）

​     ACCEPT：放行 

​     DROP：丢弃 

​     REJECT：拒绝 

​     DNAT：目标地址转换 

​     SNAT：源地址转换 

​     REDIRECT：端口重定向 

​     MASQUERADE：地址伪装 

​     LOG：日志 

​     MARK：打标记 





## 关闭所有 

iptables -P INPUT DROP 

iptables -P OUTPUT DROP 

iptables -P FORWARD DROP 





## example

动态监控22， 80 ports

```
[root@localhost ~]# iptables -A INPUT -d 10.76.33.201 -p tcp --dport 22 -m state --state NEW,ESTABLISHED -j ACCEPT
[root@localhost ~]# iptables -A OUTPUT -s 10.76.33.201 -p tcp --sport 22 -m state --state ESTABLISHED -j ACCEPT
[root@localhost ~]# iptables -A INPUT -d 10.76.33.201 -p tcp --dport 80 -m state --state NEW,ESTABLISHED -j ACCEPT
[root@localhost ~]# iptables -A OUTPUT -s 10.76.33.201 -p tcp --sport 80 -m state --state ESTABLISHED -j ACCEPT
```





自定义clean_in链，先经过clean_in 链处理

```
[root@localhost ~]# iptables -N clean_in
[root@localhost ~]# iptables -A clean_in -d 255.255.255.255 -p icmp -j DROP
[root@localhost ~]# iptables -A clean_in -d 10.76.33.201 -p icmp -j DROP
[root@localhost ~]# iptables -A clean_in -p tcp ! --syn -m state --state NEW -j DROP
[root@localhost ~]# iptables -A clean_in -p tcp --tcp-flags ALL NONE -j DROP
[root@localhost ~]# iptables -A clean_in -d 10.76.33.201 -j RETURN
[root@localhost ~]# iptables -I INPUT -j clean_in
[root@localhost ~]# iptables -L -n --line-numbers
Chain INPUT (policy ACCEPT)
num  target     prot opt source               destination         
1    clean_in   all  --  0.0.0.0/0            0.0.0.0/0           
2    REJECT     all  --  0.0.0.0/0            10.76.33.201        STRING match "h7n9" ALGO name kmp TO 65535 reject-with icmp-port-unreachable
3    ACCEPT     tcp  --  0.0.0.0/0            10.76.33.201        state RELATED,ESTABLISHED
4    ACCEPT     tcp  --  0.0.0.0/0            10.76.33.201        multiport dports 21,22,80 state NEW
5    ACCEPT     tcp  --  0.0.0.0/0            10.76.33.201        tcp dpt:21 state NEW
6    ACCEPT     tcp  --  0.0.0.0/0            10.76.33.201        state NEW,RELATED,ESTABLISHED
7    LOG        icmp --  0.0.0.0/0            10.76.33.201        icmp type 8 LOG flags 0 level 4 prefix `-- firewall log for icmp --'
8    ACCEPT     icmp --  0.0.0.0/0            10.76.33.201        icmp type 8 limit: avg 5/min burst 6

Chain FORWARD (policy ACCEPT)
num  target     prot opt source               destination         

Chain OUTPUT (policy ACCEPT)
num  target     prot opt source               destination         
1    REJECT     all  --  10.76.33.201         0.0.0.0/0           STRING match "h7n9" ALGO name kmp TO 65535 reject-with icmp-port-unreachable
2    ACCEPT     all  --  10.76.33.201         0.0.0.0/0           state RELATED,ESTABLISHED

Chain clean_in (1 references)
num  target     prot opt source               destination         
1    DROP       icmp --  0.0.0.0/0            255.255.255.255     
2    DROP       icmp --  0.0.0.0/0            10.76.33.201       
3    DROP       tcp  --  0.0.0.0/0            0.0.0.0/0           tcp flags:!0x17/0x02 state NEW
4    DROP       tcp  --  0.0.0.0/0            0.0.0.0/0           tcp flags:0x3F/0x00
5    RETURN     all  --  0.0.0.0/0            10.76.33.201       
```



利用iptables的recent模块抵御DOS攻击

```
iptables -I INPUT -p tcp --dport 22 -m connlimit --connlimit-above 3 -j DROP
iptables -I INPUT -p tcp --dport 22 -m state --state NEW -m recent --set --name SSH
iptables -I INPUT -p tcp --dport 22 -m state --state NEW -m recent --update --seconds 300 -hitcount 3 --name SSH -j DROP
```

> 利用connlimit模块将单IP并发设置为3；会误杀使用NAT上网的用户，可以根据实际情况增大该值。 
>
> 利用recent和state模块限制单IP在 300s 内只能与本机建立3个新连接，被限制5mins后即可恢复访问。 
>
>
>
> 第二句：记录访问tcp 22端口的新连接，记录名称为SSH。--set 记录数据包的来源IP，如果IP已经存在将更新已经存在的条目 
>
> 第三句：SSH记录中的IP，300s内发起超过3次连接则拒绝此IP的连接 
>
> ​               --update 每次建立连接都更新列表 
>
> ​               --seconds 必须与--rcheck或者--update同时使用 
>
> ​               --hitcount 必须与--rcheck或者--update同时使用 