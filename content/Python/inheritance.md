---
title: "inheritance 继承"
date: 2018-08-28 14:27
collection: 面向对象
---

[TOC]



# 继承

面向对象的一个特征

继承是共享的一种方式



## 继承用途

继承基类的方法，并且做出自己的改变或者扩展（代码重用）；

声明某个子类兼容于某基类，定义一个接口类Interface，接口类中定义了一些接口名（就是函数名）且并未实现接口的功能，子类继承接口类，并且实现接口中的功能；



## super 方法

父类，也可以称为超类，基类
定一个父类的重名方法，称为重写
子类中调用父类的方法，使用super对象
super对象使用super方法生成



## 类的继承

类可以继承其他类的内容，包括成员变量和成员函数

```
class People(object):

    def __init__(self, name, age):
        self.name = name
        self.age = age

    def eat(self):
        print('%s is eating...' % self.name)

    def sleep(self):
        print('%s is sleeping...' % self.name)

    def talk(self):
        print('%s is talking...' % self.name)


class Man(People):
    def __init__(self, name, age, money):
        # People.__init__(self, name, age)  等同于下面
        super(Man, self).__init__(name, age)  # 新式写法
        self.money = money
        print('%s has %s dollar' % (self.name, self.money))

    def play(self):
        print('%s is playing...' % self.name)

    def sleep(self):
        People.sleep(self)
        print('man is sleeping...')


class Woman(People):

    def purchase(self):
        print('%s is purchasing...' % self.name)


m1 = Man('Rick', 18, 100000000)
m1.eat()
m1.play()
m1.sleep()

w1 = Woman('Michelle', 18)
w1.purchase()
>>>
Rick has 100000000 dollar
Rick is eating...
Rick is playing...
Rick is sleeping...
man is sleeping...
Michelle is purchasing...
```

```python
import time

class Users:
    username = ""
    def __init__(self, uname):      #构造函数
        self.username = uname
        print('(Construct fucntion:'+self.username+')')

    def DisplayUsername(self):      #类Users的成员函数DisplayUsername
        print(self.username)

#继承类Users
class UserLogin(Users):   #类Users的子类
    def __init__(self, uname, LastLoginTime):
        Users.__init__(self, uname)       #调用父类的Users的构造函数
        self.LastLoginTime = LastLoginTime

    def DisplayLoginTime(self):
        print('Login time: '+self.LastLoginTime)
        
#获取当前时间
now = time.strftime('%Y-%m-%d %H:%M:%S', time.localtime(time.time()))

MyUser1 = UserLogin('Rick', now)
MyUser2 = UserLogin('Michelle', now)
MyUser3 = UserLogin('Sam', now)

MyUser1.DisplayUsername()   #访问类Users的函数
MyUser1.DisplayLoginTime()     #访问子类的函数
MyUser2.DisplayUsername()
MyUser2.DisplayLoginTime()
MyUser3.DisplayUsername()
MyUser3.DisplayLoginTime()

>>>
(Construct fucntion:Rick)
(Construct fucntion:Michelle)
(Construct fucntion:Sam)
Rick
Login time: 2016-09-10 16:20:45
Michelle
Login time: 2016-09-10 16:20:45
Sam
Login time: 2016-09-10 16:20:45
```





### 继承与可见性

私有的方法，变量，包括类和实例是不可继承的
公有的方法，变量，包括类和实例是可以继承的
父类公有的方法，包括类和实例，是可以访问父类的私有变量的

父类的私有方法不能被子类覆盖

```python
class A:
    __class_private_var = 'class private var'
    class_public_var = 'class public var'

    def __init__(self):
        self.__instance_private_var = 'instance private var'
        self.instance_public_var = 'instance public var'

    def __instance_private_method(self):
        try:
            print(self.__class_private_var)
        except:
            pass
        try:
            print(self.class_public_var)
        except:
            pass
        try:
            print(self.instance_public_var)
        except:
            pass

    def instance_public_method(self):
        try:
            print(self.__class_private_var)
        except:
            pass
        try:
            print(self.class_public_var)
        except:
            pass
        try:
            print(self.instance_public_var)
        except:
            pass

    @classmethod
    def __private_class_method(cls):
        try:
            print(cls.__class_private_var)
        except:
            pass
        try:
            print(cls.class_public_var)
        except:
            pass

    @classmethod
    def public_class_method(cls):
        try:
            print(cls.__class_private_var)
        except:
            pass
        try:
            print(cls.class_public_var)
        except:
            pass

class B(A):
    pass

b = B()

b.instance_public_method()
b.public_class_method()
>>>
class private var
class public var
instance public var
class private var
class public var
```



#### 自定义特殊方法 (继承list类)

```
In [57]: L = [1, 2, 3]
In [57]: L = [1, 2, 3]

In [59]: print(dir(L))
['__add__', '__class__', '__contains__', '__delattr__', '__delitem__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__getitem__', '__gt__', '__hash__', '__iadd__', '__imul__', '__init__', '__init_subclass__', '__iter__', '__le__', '__len__', '__lt__', '__mul__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__reversed__', '__rmul__', '__setattr__', '__setitem__', '__sizeof__', '__str__', '__subclasshook__', 'append', 'clear', 'copy', 'count', 'extend', 'index', 'insert', 'pop', 'remove', 'reverse', 'sort']
```

其中的`__add__`是一个特殊方法, 可以实现两个list 相加

```
In [60]: [1, 2, 3] + [4, 5, 6]
Out[60]: [1, 2, 3, 4, 5, 6]
```







继承list类，添加对 - 的定义
```
class super_list(list):
    def __sub__(self, b): #内置函数__sub__()定义了-的操作
        a = self[:] #这里, self是super_list的对象。由于super_list继承于list, 利用和list[:]相同的引用方法来表示整个对象
        b = b[:]
        while len(b) > 0:
            element_b = b.pop()
            if element_b in a:
                a.remove(element_b)
        return a

print(super_list([1, 2, 3]) - super_list([3, 4]))
>>>
[1, 2]
```



### 子类私有方法

子类可以重定义父类的私有方法，子类里面不可见

儿子不能继承父亲的老婆，但是儿子可以自己娶老婆

```python
class A:
    def __method(self):
        print('method of A')

class B(A):
    def __method(self):
        print('method of B')

    def method(self):
        self.__method()

b = B()

b.method()
>>>
method of B
```

```python
class A:
    def __method(self):
        print('method of A')

class B(A):
    def __method(self):
        super(B, self).__method()
        print('method of B')

    def method(self):
        self.__method()

b = B()

b.method()
>>>
Traceback (most recent call last):
  File "/Users/xhxu/python/python3/new_test/1.py", line 15, in <module>
    b.method()
  File "/Users/xhxu/python/python3/new_test/1.py", line 11, in method
    self.__method()
  File "/Users/xhxu/python/python3/new_test/1.py", line 7, in __method
    super(B, self).__method()
AttributeError: 'super' object has no attribute '_B__method'
```



#### 接口

接口就是一些方法特征的集合------接口是对抽象的抽象。

接口提取了一群类共同的函数，可以把接口当做一个函数的集合，然后让子类去实现接口中的函数。



### 强行继承 (私有变量重写)

强行继承父类的私有变量, 私有变量是可以被重写的

不建议使用

```python
class A:
    def __method(self):
        print('method of A')

class B(A):
    def __method(self):
        super(B, self)._A__method()
        print('method of B')

    def method(self):
        self.__method()

b = B()

b.method()
>>>
method of A
method of B
```





## 多继承

多继承是毒药，不到万不得已不要使用

```python
class A:
    def method_from_a(self):
        print('Method of A')

class B:
    def method_from_b(self):
        print('Method of B')

class C(A, B):
    pass

c = C()

c.method_from_a()
c.method_from_b()
>>>
Method of A
Method of B
```



### 继承方法

当类是经典类时，多继承情况下，会按照深度优先方式查找

当类是新式类时，多继承情况下，会按照广度优先方式查找

![img](https://cdn.pbrd.co/images/HC9883i.png)

![img](https://cdn.pbrd.co/images/HCAU2kb.png)



### 多继承顺序



经典类：首先去A类中查找，如果A类中没有，则继续去B类中找，如果B类中么有，则继续去D类中找，如果D类中么有，则继续去C类中找，如果还是未找到，则报错

新式类：首先去A类中查找，如果A类中没有，则继续去B类中找，如果B类中么有，则继续去C类中找，如果C类中么有，则继续去D类中找，如果还是未找到，则报错

在上述查找过程中，一旦找到，则寻找过程立即中断，便不会再继续找了。

```
class D:
    def bar(self):
        print('D.bar')


class C(D):
    def bar(self):
        print('C.bar')


class B(D):
    def bar(self):
        print('B.bar')


class A(B, C):
    def bar(self):
        print('A.bar')

a = A()
```





多继承，总是先调用前面的

统一按照广度优先来继承

```python
class A:
    def method(self):
        print('Method of A')

class B:
    def method(self):
        print('Method of B')

class C(A, B):
    pass

c = C()

c.method()
>>>
Method of A
```



```
class A:
    def __init__(self):
        print('A')
        

class B(A):
    print('B')
    

class C(A):
    print('C')
    

class D(B, C):
    print('D')
    

obj = D()
>>>
B
C
D
A
```



```
class A(object):
    def test(self):
        print('from A')

class B(A):
    def test(self):
        print('from B')

class C(A):
    def test(self):
        print('from C')

class D(B):
    def test(self):
        print('from D')

class E(C):
    def test(self):
        print('from E')

class F(D,E):
    # def test(self):
    #     print('from F')
    pass
f1=F()
f1.test()
print(F.__mro__) #只有新式才有这个属性可以查看线性列表，经典类没有这个属性

#新式类继承顺序:F->D->B->E->C->A
#经典类继承顺序:F->D->B->A->E->C
#python3中统一都是新式类
#pyhon2中才分新式类与经典类

>>>
from D
(<class '__main__.F'>, <class '__main__.D'>, <class '__main__.B'>, <class '__main__.E'>, <class '__main__.C'>, <class '__main__.A'>, <class 'object'>)

>>> F.mro() #等同于F.__mro__
[<class '__main__.F'>, <class '__main__.D'>, <class '__main__.B'>, <class '__main__.E'>, <class '__main__.C'>, <class '__main__.A'>, <class 'object'>]
```





## 查询父类

使用__base__属性来查询某个类的父类

```
cls.__base__

print(list.__base__)
```





## 组合调用

```
class BirthDate:
    def __init__(self, year, month, day):
        self.year = year
        self.month = month
        self.day = day


class Course:
    def __init__(self, name, price, period):
        self.name = name
        self.price = price
        self.period = period


class Teacher:
    def __init__(self, name, gender):
        self.name = name
        self.gender = gender

    def teaching(self):
        print('teaching')


class Professor(Teacher):
    def __init__(self, name, gender, birth, course):
        super(Professor, self).__init__(name, gender)
        self.birth = birth
        self.course = course


p1 = Professor('Rick', 'male',
               BirthDate('1999', '1', '1'),
               Course('Python', '20000', '4 months'))

print(p1.birth.year, p1.birth.month, p1.birth.day)
print(p1.course.name, p1.course.price, p1.course.period)

>>>
1999 1 1
Python 20000 4 months
```





## 多态 Polymorphism 

多态是面向对象的重要特性,简单点说:“一个接口，多种实现”，指一个基类中派生出了不同的子类，且每个子类在继承了同样的方法名的同时又对父类的方法做了不同的实现，这就是同一种事物表现出的多种形态。

```
class Animal:
    def __init__(self, name):
        self.name = name

    def bark(self):
        pass

    @staticmethod
    def animal_bark(obj):	#这里的方法可以放到类外面形成函数
        obj.bark()


class Cat(Animal):
    def bark(self):
        print('Meow!')


class Dog(Animal):
    def bark(self):
        print('Woof!')


d = Dog('Mydog')
c = Cat('Mycat')

Animal.animal_bark(c)
Animal.animal_bark(d)
>>>
Meow!
Woof!
```

```
from abc import ABCMeta, abstractclassmethod

class Shape(object):
    __metaclass__ = ABCMeta
    def __init__(self):
        self.color = "Black"

@abstractclassmethod
def draw(self):
    pass

class circle(Shape):   #Shape子类circle
    def __init__(self, x, y, r):
        self.x = x
        self.y = y
        self.r = r

    def draw(self):
        print("Draw Circle: (%d, %d, %d)" %(self.x, self.y, self.r))

class line(Shape):     #Shape 子类line
    def __init__(self, x1, y1, x2, y2):
        self.x1 = x1
        self.y1 = y1
        self.x2 = x2
        self.y2 = y2

    def draw(self):       #抽象方法draw()又不同的实现,这就是多态
        print("Draw Line: (%d, %d, %d, %d)" %(self.x1, self.y1, self.x2, self.y2))

c = circle(10, 10, 5)
c.draw()

l = line(10, 10, 20, 20)
l.draw()

>
Draw Circle: (10, 10, 5)
Draw Line: (10, 10, 20, 20)
```





## MRO (Method Resolution Order)

MRO 通过C3算法计算出来的
本地优先级: 根据声明的顺序从左往右查找
单调性：所有子类中，也应满足其查找顺序


### C3算法

`class B: -> mro(B) = [B, O]`

`class B(A1, A2, ...) -> mro(B) = [B] + merge(mro(A1), mro(A2), ..., [A1, A2, ...])`

```
C(A, B) -> 
[C] + merge(mro(A), mro(B), [A, B])
[C] + merge([A, O], [B, O], [A, B])
[C, A] + merge([O], [B, O], [B])
[C, A, B] + merge([O], [O])
[C, A, B, O]
```

```
C(B, A) -> 
[C] + merge(mro(B), mro(A), [B, A])
[C] + merge([B, O], [A, O], [B, A])
[C, B] + merge([B], [A, O], [A])
[C, B, A] + merge([O], [O])
[C, B, A, O]
```

```
C(A, B), B(A) ->
[C] + merge(mro(A), mro(B), [A, B])
[C] + merge([A, O], ([B] + merge(mro(A), [A]), [A, B])
[C] + merge([A, O], ([B] + merge([A, O], [A])), [A, B])
[C] + merge([A, O], ([B, A] + merge([O])), [A, B])
[C] + merge([A, O], [B, A, O], [A, B])
raise TypeError
```

```
C(B, A), B(A) -> 
[C] + merge(mro(B), mro(A), [B, A])
[C] + merge([B, A, O], [A, O], [B, A])
[C] + merge([A, O], [A, O], [A])
[C, B, A] + merge([O], [O])
[C, B, A, O]
```



#### merge步骤

 * 顺序遍历列表
 * 首元素满足以下条件，否则遍历下一个序列
    * 在其他序列也是首元素
    * 再其他序列里面不存在
 * 从所有序列中移除此元素，合并到MRO序列中
 * 重复执行，直到所有序列为空或无法执行下去


### MIXIN

实现组合的一种方式
实现数据和方法进行分离