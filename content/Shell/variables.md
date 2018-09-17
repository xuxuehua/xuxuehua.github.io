---
title: "variables"
date: 2018-09-12 00:07
---


[TOC]


# variables

变量可被设置为当前shell的局部变量，或是环境变量。如果您的shell脚本不需要调用其他脚本，其中的变量通常设置为脚本内的局部变量



## 获取变量

要获取变量的值，在美元符后跟变量名即可。shell会对双引号内的美元符后的变量执行变量扩展，单引号中的美元符则不会被执行变量扩展。

```
name="John Doe" or declare name="John Doe"   # local variable
```



```
export NAME="John Doe"    # global variable
```

```
echo "$name" "$NAME"      # extract the value
```





