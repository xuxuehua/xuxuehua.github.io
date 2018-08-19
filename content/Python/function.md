---
title: "function"
date: 2018-08-20 01:18
collection: 函数
---



# 函数

函数是组织好的，可重复使用，实现单一功能的代码段
函数有输入（参数）和输出（返回值）
Python中，函数是一等对象



## 函数定义 

```python
def fn():
    pass
```



### 变量作用域

```python
a = 100        #全局变量
def setNum():
    a = 10     #局部变量
    print(a)   #打印局部变量

setNum()       #调用函数
print(a)       #打印全局变量
```

### 



## 函数参数

> 非默认非可变参数，可变位置参数，可变关键字参数
> 默认参数不要和可变参数放在一起


```python
def add(x, y):
    return x + y

print(add(3, 4))
>>>
7
```

* 参数引用 (在函数体内赋值，不会影响外部变量)

```python
x = 1
y = 2

def swap(x, y):
    x, y = y, x

swap(x, y)
print(x, y)
>>>
1 2
```

* 直传递

```python
L = [1, 2, 3]

def append(item):
    L.append(item)

append(4)
print(L)
>>>
[1, 2, 3, 4]
```

### 位置参数 

> 位置参数，通过参数传递的位置来决定

```python
def add(x, y):
    print('x = {0}'.format(x))
    print('y = {0}'.format(y))
    return x + y

print(add(1, 2))
>>>
x = 1
y = 2
3
```

### 关键字参数

> 关键字参数，通过参数名称来决定

```python
def add(x, y):
    print('x = {0}'.format(x))
    print('y = {0}'.format(y))
    return x + y

print(add(y=2, x=1))
>>>
x = 1
y = 2
3
```

### 位置，关键字参数混合使用

* 位置参数和关键字参数是在调用的时候决定的

```python
def add(x, y):
    print('x = {0}'.format(x))
    print('y = {0}'.format(y))
    return x + y

print(add(1, y=2))
>>>
x = 1
y = 2
3
```

* 关键字参数必须在位置参数之后

```python
def add(x, y):
    print('x = {0}'.format(x))
    print('y = {0}'.format(y))
    return x + y

print(add(x=1, 2))
>>>
  File "/Users/xhxu/python/python3/test/1.py", line 6
    print(add(x=1, 2))
                  ^
SyntaxError: positional argument follows keyword argument
```

### 默认参数

* 默认的参数可以被覆盖掉

```python
def inc(x, i=1):
    return x + i

print(inc(5))
print(inc(5, 2))
>>>
6
7
```

### 可变参数 (可变位置参数)

> 函数定义时，参数名前加\*代表次参数是可变的位置参数
> 函数调用是，参数列表封装成一个元组传递给args

* 使用列表的调用方法

```python
def sum(L):
    ret = 0
    for x in L:
        ret += x
    return ret

print(sum([1, 2, 3, 4, 5]))
>>>
15
```

* 使用可变参数的调用方法 (调用参数的时候，自动组装成元组)

```python
def sum(*args):
    ret = 0
    for x in args:
        ret += x
    return ret

print(sum(1, 2, 3, 4, 5))
>>>
16
```

### 关键字参数 (可变关键字参数)

* 使用可变关键字参数  (调用参数的时候，自动组装成字典)

```python
def print_info(**kwargs):
    for k, v in kwargs.items():
        print('{0} -> {1}'.format(k, v))

print(print_info(a=1, b=2))
>>>
b -> 2
a -> 1
```

* 调用的时候, 会决定参数是位置参数还是关键字参数

```python
def print_info(**kwargs):
    for k, v in kwargs.items():
        print('{0} -> {1}'.format(k, v))

print_info(1, 2, 3)
>>>
  File "/Users/xhxu/python/python3/test/1.py", line 5, in <module>
    print_info(1, 2, 3)
TypeError: print_info() takes 0 positional arguments but 3 were given
```

### 可变参数和关键字参数混合使用

```python
def print_info(*args, **kwargs):
    for x in args:
        print(x)
    for k, v in kwargs.items():
        print('{0} -> {1}'.format(k, v))

print_info(1, 2, 3, a=4, b=5)
>>>
1
2
3
a -> 4
b -> 5
```

### 可变参数和非可变参数

```python
def print_info(x, y, *args, **kwargs):
    print('x = {0}'.format(x))
    print('y = {0}'.format(y))
    for x in args:
        print(x)
    for k, v in kwargs.items():
        print('{0} -> {1}'.format(k, v))

print_info(1, 2, 3, 4, 5, 6, a=7, b=8)
>>>
x = 1
y = 2
3
4
5
6
b -> 8
a -> 7
```

### 参数解包

### 位置参数解包

```python
def add(x, y):
    print('x = {0}'.format(x))
    print('y = {0}'.format(y))
    return x + y

L = [1, 2]
print(add(*L))
>>>
x = 1
y = 2
3
```

### 关键字参数解包

```python
def add(x, y):
    print('x = {0}'.format(x))
    print('y = {0}'.format(y))
    return x + y

d = {'x': 1, 'y': 2}
print(add(**d))
>>>
x = 1
y = 2
3
```



```
def square_sum(a,b):
    c = a**2 + b**2
    return c
```
* 首先，def，这个关键字通知python：我在定义一个函数。square_sum是函数名。

* 括号中的a, b是函数的参数，是对函数的输入。参数可以有多个，也可以完全没有（但括号要保留）。

* return c 表示返回c的值，也可以不会返回

* return 可以返回多个值，使用逗号分开， 相当于返回一个tuple(定值表)

* 在Python中，当程序执行到return的时候，程序将停止执行函数内余下的语句。return并不是必须的，当没有return, 或者return后面没有返回值时，函数将自动返回None。None是Python中的一个特别的数据类型，用来表示什么都没有，相当于C中的NULL。None多用于关键字参数传递的默认值


## 函数调用和参数传递


### 函数调用
* 整数变量传递给函数
  对于基本数据类型的变量，变量传递给函数后，函数会在内存中复制一个新的变量，从而不影响原来的变量。（我们称此为值传递）
```
a = 1
def change_integer(a):
    a += 1
    return a

print(change_integer(a))
print(a)
>>>
2
1
```


* 表传递给函数
  对于表来说，表传递给函数的是一个指针，指针指向序列在内存中的位置，在函数中对表的操作将在原有内存中进行，从而影响原有变量。 （我们称此为指针传递）
```
b = [1, 2, 3]
def change_list(b):
    b[0] = b[0] + 1
    return b

print(change_list(b))
print(b)
>>>
[2, 2, 3]
[2, 2, 3]
```



## 函数返回值

```python
def sum(num1, num2):
    return num1 + num2
print(sum(1, 3))
> 
4
​````

​```python
def filter_even(list):
    list1 = []
    for i in range(len(list)):
        if list[i] % 2 ==0:
            list1.append(list[i])
            i -= 1
    return list1
list = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
list2 = filter_even(list)
print(list2)
> 
[2, 4, 6, 8, 10]
```



## Python 内置函数

### abs()

```python
print(abs(-1))
>
1
```

### pow() 

pow(x, y) 返回x的y次幂

```python
print(pow(2, 3))
> 
8
```

### Round()  

round(x[, n]) 返回浮点数x的四舍五入值

```python
print(round(80.2345, 2))
>
80.23
```

### divmod()   

divmod(a, b) 返回a除以b的商和余数，返回一个元组

```python
print(divmod(8, 3))
>
(2, 2)
```

### lower(), upper(), swapcase(), capitalize(), title()

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
### ljust(), rjust(), center(), zfil()

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
### find(), index(), rfind(), rindex(), count(), replace(), strip(), lstrip(), rstrip(), expandtabs()

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
### split()

```python
str = 'Hello World'
print(str.split(' '))
>
['Hello', 'World']
```
### splitlines()

```python
str = 'Hello World'
print(str.splitlines())
>
['Hello World']
```
### join()

```python
list = ['Hello', 'World']
str = '#'
print(str.join(list))
>
Hello#World
```
### startswith(), endswith(), isalnum(), isalpha(), isdigit(), islower(), isupper()

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
### help()

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
### type() 

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




