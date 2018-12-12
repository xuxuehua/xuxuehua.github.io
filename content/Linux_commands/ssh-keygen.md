---
title: "ssh-keygen"
date: 2018-09-05 15:44
---

[TOC]

# ssh-keygen

这个问题 Enter file in which to save the key 路径要写绝对路径Á



## -t 类型

类型 dsa | ecdsa | ed25519 | rsa



## -b

bit 位长度



## -y public key 

`-y` outputs the public key:

```
ssh-keygen -y -f ~/.ssh/id_rsa > ~/.ssh/id_rsa.pub
```



## -N 新建 passphrase

清空passphrase

```
ssh-keygen -t rsa -N '' -f test_rsa_key
```



## -p 修改passphrase

```
ssh-keygen -p -f keyfile
```





## -f 指定key 文件

```
ssh-keygen -p -f keyfile
```

