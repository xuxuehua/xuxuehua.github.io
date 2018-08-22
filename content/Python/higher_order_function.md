---
title: "higher_order_function 高阶函数"
date: 2018-08-21 21:14
collection: 函数
---

[TOC]



# higher order function 高阶函数



## 定义

变量可以指向函数，函数的参数能够接受变量，那么一个函数就可以接受另一个函数作为参数，这种函数称为高阶函数

```
def add(a, b, f):
    return f(a) + f(b)

ret = add(3, -6, abs)
print(ret)

>>>
9
```

