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



test函数的第一参数f就是一个函数对象

```python
def func(x, y):
    return x+y

def test(f, a, b):
    print('test')
    print(f(a, b))

test(func, 3, 5)
>>>
test
8
```

或者写成下面的

```python
def test(f, a, b):
    print('test')
    print(f(a, b))

test((lambda x, y:x+y), 3, 5 )
>>>
test
8
```



## map()函数

map()函数的第一个参数是一个函数对象。

下面的map()有两个参数， 一个是lambda 所定义的函数对象，一个是包含有多个元素的表。

map()的功能是将函数对象依次作用与表的每个元素。每次作用的结果存储与返回的表re中。

map() 通过读入的函数(这里是lambda函数)来操作数据(这里的数据是表中的每一个元素)

```
re = map((lambda x: x+3), [1, 3, 5, 7])
print(re)
print(list(re))
>>>
<map object at 0x10caf3780>
[4, 6, 8, 10]
```



## filter() 函数

filter函数的第一个参数也是函数对象， 将作为参数的函数对象作用于多个元素。
如果函数的返回为True，则该次的元素将被存储到返回的表中。

在python3 中，filter返回的不是表，而是循环对象

```
def func(a):
    if a > 100:
        return True
    else:
        return False

print(filter(func, [10, 20, 101, 400]))
print(list(filter(func, [10, 20, 101, 400])))
>>>
<filter object at 0x10c913780>
[101, 400]
```



## reduce() 函数

reduce函数的第一个参数也是函数，但是要求函数自身能够接受两个参数。 reduce可以累进的将函数作用与各个参数

```
from functools import reduce
print(reduce((lambda x,y: x+y), [1, 2, 4, 6, 8]))
>>>
21
```