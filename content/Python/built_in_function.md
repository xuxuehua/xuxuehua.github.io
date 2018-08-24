---
title: "built_in_function"
date: 2018-08-24 11:04
collection: 函数
---

[TOC]



# 内置函数



## bin()

把十进制数转二进制

```
In [8]: bin(1)
Out[8]: '0b1'

In [9]: bin(2)
Out[9]: '0b10'

In [10]: bin(4)
Out[10]: '0b100'

In [11]: bin(255)
Out[11]: '0b11111111'
```





## bytes

```
In [14]: a = bytes('abc', encoding='utf-8')

In [15]: type(a), a
Out[15]: (bytes, b'abc')

In [16]: a.capitalize()
Out[16]: b'Abc'

In [17]: a
Out[17]: b'abc'
```



## callable

是否可调用

```
In [18]: def a():
    ...:     pass
    ...:
    ...:

In [19]: callable(a)
Out[19]: True

In [20]: callable(1)
Out[20]: False
```



## chr

转换对应的ascii的值， 输入的是数字

```
In [21]: chr(97)
Out[21]: 'a'

In [22]: chr(98)
Out[22]: 'b'

In [23]: chr(99)
Out[23]: 'c'
```



## ord

转换字符对应的ascii

```
In [24]: ord('a')
Out[24]: 97

In [25]: ord('b')
Out[25]: 98

In [26]: ord('c')
Out[26]: 99
```





## filter

```
In [32]: filter(lambda n: n> 5, range(10))
In [32]: filter(lambda n: n> 5, range(10))
Out[32]: <filter at 0x10c677da0>

In [33]: x = filter(lambda n: n> 5, range(10))

In [34]: for i in x:
    ...:     print(i)
    ...:
6
7
8
9
```



## hex

数字转16进制

```
In [38]: hex(10)
Out[38]: '0xa'

In [39]: hex(15)
Out[39]: '0xf'

In [40]: hex(255)
Out[40]: '0xff'
```



## pow

```
In [41]: pow(2, 8)
Out[41]: 256

In [42]: pow(2, 10)
Out[42]: 1024
```





## round

小数点精度

```
In [43]: round(3.1415)
Out[43]: 3

In [44]: round(3.1415, 2)
Out[44]: 3.14
```



## sorted

```
In [45]: a = {6:2, 8:0, 1:4, -7:6, 11:99, 51:3}

In [46]: sorted(a.items(), key=lambda x: x[1])
Out[46]: [(8, 0), (6, 2), (51, 3), (1, 4), (-7, 6), (11, 99)]
```



## zip

```
In [47]: a = [1, 2, 3]

In [48]: b = ['a', 'b', 'c']

In [59]: for i in zip(a, b):
    ...:     print(i)
    ...:
(1, 'a')
(2, 'b')
(3, 'c')
```

