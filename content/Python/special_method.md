---
title: "special_method 特殊方法"
date: 2018-08-28 14:39
collection: 面向对象
---



[TOC]

# 魔术方法和特殊方法

## 对象的创建与销毁

`__new__` 创建对象
`__init__` 初始化对象
`__del__` 销毁对象 （销毁对象时调用）

```python
class A:
    def __new__(cls):
        print('call __new__')
        return object.__new__(cls)

    def __init__(self):
        print('call __init__')

    def method(self):
        print('call method')

    def __del__(self):
        print('call __del__')

a = A()

a.method()

del a
>>>
call __new__
call __init__
call method
call __del__
```


### 可视化对象

```python
class A:
    def __init__(self, name):
        self.name = name

    def __repr__(self):
        return self.name

    def __str__(self):
        return 'call __str__ name is {0}'.format(self.name)

    def __bytes__(self):
        return 'call __bytes__ name is {0}'.format(self.name).encode('utf-8')

a = A('Rick')

#其实调用的是print(repr(a))
print(a)
print(str(a))
print(bytes(a))
>>>
call __str__ name is Rick
call __str__ name is Rick
b'call __bytes__ name is Rick'
```



##比较运算符重载

```python
class Person:
    def __init__(self, age):
        self.age = age

    def __lt__(self, other):
        print('lt')
        return self.age < other.age

    def __le__(self, other):
        print('le')
        return self.age <= other.age

    def __eq__(self, other):
        print('eq')
        return self.age == other.age

    def __ne__(self, other):
        print('ne')
        return self.age != other.age

    def __gt__(self, other):
        print('gt')
        return self.age > other.age

    def __ge__(self, other):
        print('ge')
        return self.age >= other

p1 = Person(18)

p2 = Person(13)

print(p1 > p2)
print(p1 < p2)
>>>
gt
True
lt
False
```



### bool 函数

```python
class Grok:
    def __init__(self, val):
        self.val = val

    def __bool__(self):
        return not self.val

grok1 = Grok(True)
grok2 = Grok(False)

print(bool(grok1))
print(bool(grok2))
>>>
False
True
```

```python
class LIST:
    def __init__(self, *args):
        self.val = args

    def __len__(self):
        return len(self.val)

lst = LIST(1, 2, 3)
lst2 = LIST()

print(len(lst))
print(len(lst2))
>>>
3
0
```



### hash与可hash对象

```python
class Grok:
    def __init__(self, val):
        self.val = val

    def __hash__(self):
        return id(self.val)

grok = Grok(123)
print(hash(grok))
>>>
4306027616
```





### 可调用对象

```python
class InjectUser:
    def __init__(self, default_user):
        self.user = default_user

    def __call__(self, fn):
        def wrap(*args, **kwargs):
            if 'user' not in kwargs.keys():
                kwargs['user'] = self.user
            return fn(*args, **kwargs)
        return wrap

@InjectUser('Rick')
def do_something(*args, **kwargs):
    print(kwargs.get('user'))

do_something()
>>>
Rick
```





### 反射


```python
class Grok:
    X = 1
    Y = 2
    Z = 3
    def __init__(self, x, y, z):
        self.x = x
        self.y = y
        self.z = z

    def method(self):
        pass

grok = Grok(1, 2, 3)

print(grok.__dict__)
>>>
{'z': 3, 'x': 1, 'y': 2}
```


```python
class Grok:
    def __init__(self):
        self.__dict = {'x': 1, 'y': 2}
        self.a = 3
        #self.x = 5

    def __getattr__(self, name):
        print('get {0}'.format(name))
        return self.__dict.get(name)

grok = Grok()

print(grok.x)
print(grok.a)
>>>
get x
1
3
```



### with 语句实现的方法

with 语句可以自动关闭资源

```python
class Resource:
    def __init__(self):
        print('init')

    def __enter__(self):
        print('enter')
        print(self)
        return self

    def __exit__(self, *args, **kwargs):
        print('exit')

with Resource() as res:
    print(res)
>>>
init
enter
<__main__.Resource object at 0x103995da0>
<__main__.Resource object at 0x103995da0>
exit
```



## 描述器

实现了`__get__`, `__set__`, `__delete__` 的方法成为描述器

```python
class Point:

    def __init__(self, x, y):
        self.x = x
        self.y = y

class Number:

    def __init__(self, name):
        self.name = name

    def __get__(self, instance, cls):
        print('get')
        if instance is not None:
            return instance.__dict__[self.name]

    def __set__(self, instance, value):
        print('set')
        if isinstance(value, (int, float)):
            instance.__dict__[self.name] = value
        else:
            raise TypeError('excepted int or float')

    def __delete__(self, instance):
        del instance.__dict__[self.name]

class Point:
    x = Number('x')
    y = Number('y')
    def __init__(self, x, y):
        self.x = x
        self.y = y

point = Point(1, 2)

print(point.x)  # 其调用Point.x.__get__(point, Point)
print(point.y)
>>>
set
set
get
1
get
2
```



### property 装饰器的实现

通过描述器实现

描述器就是一个传递协议

```python
class Property:
    def __init__(self, fget=None, fset=None, fdel=None):
        self.fget = fget
        self.fset = fset
        self.fdel = fdel

    def __get__(self, instance, cls):
        if self.fget is not None:
            return self.fget(instance)

    def __set__(self, instance, value):
        if self.fset is not None:
            return fset(instance, value)

    def __delete__(self, instance):
        if self.fdel is not None:
            return fdel(instance)

    def getter(self, fn):
        self.fget = fn

    def setter(self, fn):
        self.fset = fn

    def deler(self, fn):
        self.fdel = fn

class Spam:
    def __init__(self, val):
        self.__val = val

    @property
    def val(self):
        return self.__val

    @val.setter
    def val(self, value):
        self.__val = value

s = Spam(3)
print(s.val)
>>>
3
```