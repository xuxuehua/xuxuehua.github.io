---
title: "built_in_function"
date: 2018-08-24 11:04
collection: 函数
---

[TOC]



# 内置函数



## abs()

```python
print(abs(-1))
>
1
```

## pow() 

pow(x, y) 返回x的y次幂

```python
print(pow(2, 3))
> 
8
```

## Round()  

round(x[, n]) 返回浮点数x的四舍五入值

```python
print(round(80.2345, 2))
>
80.23
```

## divmod()   

divmod(a, b) 返回a除以b的商和余数，返回一个元组

```python
print(divmod(8, 3))
>
(2, 2)
```

## lower(), upper(), swapcase(), capitalize(), title()

```python
str = 'Hello World'
print(str.lower())
print(str.upper())
print(str.swapcase())
print(str.capitalize())
print(str.title())
> 
hello world
HELLO WORLD
hELLO wORLD
Hello world
Hello World
```
## ljust(), rjust(), center(), zfil()

```python
str = 'Hello World'
print(str.ljust(20, '*'))
print(str.rjust(20, '*'))
print(str.center(20, '*'))
print(str.zfill(20))
> 
Hello World*********
*********Hello World
****Hello World*****
000000000Hello World
```
## find(), index(), rfind(), rindex(), count(), replace(), strip(), lstrip(), rstrip(), expandtabs()

```python
str = 'Hello World'
print(str.find('l'))
print(str.index('l'))
print(str.rfind('l'))
print(str.rindex('l'))
print(str.count('l'))
print(str.replace(' ', '*'))
print(str.strip())
print(str.lstrip())
print(str.rstrip())
print(str.expandtabs())
>
2
2
9
9
3
Hello*World
Hello World
Hello World
Hello World
Hello World
```
## split()

```python
str = 'Hello World'
print(str.split(' '))
>
['Hello', 'World']
```
## splitlines()

```python
str = 'Hello World'
print(str.splitlines())
>
['Hello World']
```
## join()

```python
list = ['Hello', 'World']
str = '#'
print(str.join(list))
>
Hello#World
```
## startswith(), endswith(), isalnum(), isalpha(), isdigit(), islower(), isupper()

```python
str = 'Python String Function'
print(str.startswith('P'))
print(str.endswith('P'))
print(str.isalnum())
print(str.isalpha())
print(str.isdigit())
print(str.islower())
print(str.isupper())
>
True
False
False
False
False
False
False
```
## help()

```python
help('print')
> 
Help on built-in function print in module builtins:

print(...)
    print(value, ..., sep=' ', end='\n', file=sys.stdout, flush=False)
    
    Prints the values to a stream, or to sys.stdout by default.
    Optional keyword arguments:
    file:  a file-like object (stream); defaults to the current sys.stdout.
    sep:   string inserted between values, default a space.
    end:   string appended after the last value, default a newline.
    flush: whether to forcibly flush the stream.
```
## type() 

```python
str = 'Hello'
print(type(str))
num = 8
print(type(num))
list = [1, 2, 3]
print(type(list))
>
<class 'str'>
<class 'int'>
<class 'list'>
```

## range()

range 进行循环控制
```
In [1]: s = 'abcdefghijkl'

In [2]: for i in range(0, len(s), 2):
   ...:     print(s[i])
   ...:     
a
c
e
g
i
k
```



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

zip()函数从多个列表中依次去除一个元素。每次取出(来自不同列表的)的元素合成一个元组，合并成的元组放入zip()返回的列表中



### 聚合

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

```python
ta = [1, 2, 3]
tb = [4, 5, 6]
tc = ['a', 'b', 'c']

for (a, b, c) in zip(ta, tb, tc):
    print(a, b, c)
>>>
1 4 a 
2 5 b
3 6 c
```



### 分解

```python
ta = [1, 2, 3]
tb = [4, 5, 6]

zipped = zip(ta, tb)
print(zipped)

na, nb = zip(*zipped)
print(na, nb)
>>>
<zip object at 0x1034855c8>
(1, 2, 3) (4, 5, 6)
```