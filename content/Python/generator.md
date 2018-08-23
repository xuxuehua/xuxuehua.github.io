---
title: "generator 生成器"
date: 2018-08-22 11:18
collection: 函数
---

[TOC]

# 生成器



## 定义

将列表生成式的中括号变成小括号即是生成器

```
In [5]: type([i*2 for i in range(10)])
Out[5]: list

In [6]: type((i*2 for i in range(10)))
Out[6]: generator
```



## 生成器调用

生成器只有在调用的时候才会生成相应的数据

```
In [18]: g = ((i*2 for i in range(2)))

In [19]: g.__next__()
Out[19]: 0

In [20]: g.__next__()
Out[20]: 2

In [21]: g.__next__()
---------------------------------------------------------------------------
StopIteration                             Traceback (most recent call last)
<ipython-input-21-42e506b10868> in <module>()
----> 1 g.__next__()

StopIteration:
```



## 应用

### 斐波那契数列

函数生成方法

```
def fib(max):
    n, a, b = 0, 0, 1
    while n < max:
        print(b)
        a, b = b, a+b
        n = n + 1

fib(10)

>>>
1
1
2
3
5
8
13
21
34
55
```



生成器方法

```
def fib(max):
    n, a, b = 0, 0, 1
    while n < max:
        yield b
        a, b = b, a+b
        n = n + 1

f = fib(10)
print(f.__next__())
print(f.__next__())
print(f.__next__())
print(f.__next__())

>>>
1
1
2
3
```

