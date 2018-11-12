---
title: "internal_variables 内部变量"
date: 2018-11-08 13:07
---


[TOC]


# internal_variables



## $RANDOM 随机数

随机字符串

```
# echo $RANDOM | md5sum | cut -c 1-8
024cbfdc
```

随机数字

```
# echo $RANDOM | cksum | cut -c 1-8
20613431
```





