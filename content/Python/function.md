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

#### 全局与局部变量

在子程序中定义的变量称为局部变量，在程序的一开始定义的变量称为全局变量。

全局变量作用域是整个程序，局部变量作用域是定义该变量的子程序。

当全局变量与局部变量同名时：

在定义局部变量的子程序内，局部变量起作用；在其它地方全局变量起作用。

```python
a = 100        #全局变量
def setNum():
    a = 10     #局部变量
    print(a)   #打印局部变量

setNum()       #调用函数
print(a)       #打印全局变量
```

```
x = 0
def grandpa():
    x = 1
    print('grandpa', x)
    def dad():
        x = 2
        print('father', x)
        def son():
            x = 3
            print('son', x)
        son()
    dad()
grandpa()

>>>
grandpa 1
father 2
son 3
```





## 函数参数

非默认非可变参数，可变位置参数，可变关键字参数
默认参数不要和可变参数放在一起


```python
def add(x, y):
    return x + y

print(add(3, 4))
>>>
7
```

参数引用 (在函数体内赋值，不会影响外部变量)

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

直传递

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

位置参数，通过参数传递的位置来决定

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

关键字参数，通过参数名称来决定

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

位置参数和关键字参数是在调用的时候决定的

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

关键字参数必须在位置参数之后

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

如果参数赋予了默认值，且该参数最终没有被传递，将使用该默认值

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

函数定义时，参数名前加\*代表次参数是可变的位置参数
函数调用是，参数列表封装成一个元组传递给args

使用列表的调用方法

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

使用可变参数的调用方法 (调用参数的时候，自动组装成元组)

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

使用可变关键字参数  (调用参数的时候，自动组装成字典)

```python
def print_info(**kwargs):
    for k, v in kwargs.items():
        print('{0} -> {1}'.format(k, v))

print(print_info(a=1, b=2))
>>>
b -> 2
a -> 1
```

调用的时候, 会决定参数是位置参数还是关键字参数

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



### 闭包

所谓的闭包就是一个包含有环境变量取值的函数对象。环境变量取值被保存在函数对象的`__closure__`属性中

函数是一个对象，所以可以作为某个函数的返回结果

```
def line_conf():
    def line(x):
        return 2*x+1
    return line   # Return a function object

my_line = line_conf()
print(my_line(5))
>>>
11
```



`__closure__`包含一个元组，而第一个cell包含的就是闭包的环境变量b的取值

```
def line_conf():
    b = 15
    def line(x):
        return 2*x+b
    return line

b = 5
my_line = line_conf()
print(my_line.__closure__)
print(my_line.__closure__[0].cell_contents)
>>>
(<cell at 0x10dfd2fd8: int object at 0x10dce7830>,)
15
```



函数line 与环境变量a, b 构成闭包

```
def line_conf(a, b):
    def line(x):
        return a*x+ b
    return line

line1 = line_conf(1, 1)
line2 = line_conf(4, 5)
print(line1(5), line2(5))
>>>
6 25
```





### 参数解包

#### 位置参数解包

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





#### 关键字参数解包

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
整数变量传递给函数
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



### 参数传递

表传递给函数
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



函数的参数传递，本质上传递的就是引用

```
def f(x):
    x = 100
    print(x)

a = 1
f(a)
print(a)
>>>
100
1
```

如果传递的是可变(mutable)对象，那么改变函数参数，有可能改变原对象
```
def f(x):
    x[0] = 100
    print(x)

a = [1, 2, 3]
f(a)
print(a)
>>>
[100, 2, 3]
[100, 2, 3]
```





## 函数返回值

函数在执行过程中只要遇到return语句，就会停止执行并返回结果

如果未在函数中指定return,那这个函数的返回值为None 



return = 0, 返回None

return = 1, 返回object

return > 1, 返回tuple

```
def test1():
    pass


def test2():
    return 0


def test3():
    return 0, 10, 'hello'


t1 = test1()
t2 = test2()
t3 = test3()

print(type(t1), t1)
print(type(t2), t2)
print(type(t3), t3)

>>>
<class 'NoneType'> None
<class 'int'> 0
<class 'tuple'> (0, 10, 'hello')
```



## 匿名函数

匿名函数就是不需要显式的指定函数

```
def calc(n):
    return n**n
print(calc(10))

```

换成匿名函数

```
calc = lambda n:n**n
print(calc(10))
```



匿名函数主要是和其它函数搭配使用

```
res = map(lambda x:x**2,[1,5,7,4,8])
for i in res:
    print(i)
    
>>>
1
25
49
16
64
```





## 函数递归

在函数内部，可以调用其他函数。如果一个函数在内部调用自身本身，这个函数就是递归函数。

递归函数必须明确结束条件



>  尽量少用

```
def calc(n):
    print(n)
    if int(n/2) ==0:
        return n
    return calc(int(n/2))
 
calc(10)
 
>>>
10
5
2
1
```



## 函数式编程

函数式编程要求使用函数，可以把运算过程定义为不同的函数

```
var result = subtract(multiply(add(1, 2), 3), 4)
```




