---
title: "openssl"
date: 2018-10-22 03:16
---


[TOC]


# openssl



## rand 随机数

随机字符串

```
$ openssl rand -base64 4
GsOFIA==
```

随机数字

```
openssl rand -base64 4 | cksum | cut -c 1-8
15404016
```



