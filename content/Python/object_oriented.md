---
title: "object_oriented"
date: 2018-08-27 02:16
collection: 面向对象
---

[TOC]

# 面向对象



## 编程范式

编程是 程序 员 用特定的语法+数据结构+算法组成的代码来告诉计算机如何执行任务的过程 ， 一个程序是程序员为了得到一个任务结果而编写的一组指令的集合，正所谓条条大路通罗马，实现一个任务的方式有很多种不同的方式， 对这些不同的编程方式的特点进行归纳总结得出来的编程方式类别，即为编程范式。

常见的编程范式： OOP， FP， PP， IP

python是一种多范式到语言，但对OOP支持最好



## 面向过程编程(Procedural Programming)

Procedural programming uses a list of instructions to tell the computer what to do step-by-step. 

面向过程又被称为top-down languages， 就是程序从上到下一步步执行，一步步从上到下，从头到尾的解决问题 。



## 面向对象编程(Object Oriented Programming)

OOP编程是利用“类”和“对象”来创建各种模型来实现对真实世界的描述，使用面向对象编程的原因一方面是因为它可以使程序的维护和扩展变得更简单，并且可以大大提高程序开发效率 ，另外，基于面向对象的程序可以使它人更加容易理解你的代码逻辑，从而使团队开发变得更从容。



### 基本哲学

世界是由对象组成的
对象具有运动规律和内部状态
对象之间的相互作用和通讯构成世界

### 面向对象的本质

面向对象是对数据和行为的封装
但有时候，数据仅仅是数据，方法仅仅是方法



### **Class 类**

一个类即是对一类拥有相同属性的对象的抽象、蓝图、原型。在类中定义了这些对象的都具备的属性（variables(data)）、共同的方法，相同或相似性质的对象的抽象就是类。



### **Object 对象** 

一个对象即是一个类的实例化后实例，一个类必须经过实例化后方可在程序中调用

面向对象程序设计思想可以将一组数据和与这组数据有关操作组装在一起，形成实体，这个实体就是对象。

#### 对象的特性

唯一性： 世界上没有两片相同的树叶（每个对象都有自己唯一的内存）
分类性： 分类是对现实世界的抽象



### **Encapsulation 封装**

在类中对数据的赋值、内部调用对外部用户是透明的，这使类变成了一个胶囊或容器，里面包含着类的数据和方法

封装最好理解了。封装是面向对象的特征之一，是对象和类概念的主要特性。

封装，也就是把客观事物封装成抽象的类，并且类可以把自己的数据和方法只让可信的类或者对象操作，对不可信的进行信息隐藏。

将数据和操作捆绑在一起，定义一个新类的过程就是封装

### **Inheritance 继承**

一个类可以派生出子类，在这个父类里定义的属性、方法自动被子类继承

面向对象编程 (OOP) 语言的一个主要功能就是“继承”。继承是指这样一种能力：它可以使用现有类的所有功能，并在无需重新编写原来的类的情况下对这些功能进行扩展。

通过继承创建的新类称为“子类”或“派生类”。

被继承的类称为“基类”、“父类”或“超类”。

继承的过程，就是从一般到特殊的过程。

要实现继承，可以通过“继承”（Inheritance）和“组合”（Composition）来实现。

在某些 OOP 语言中，一个子类可以继承多个基类。但是一般情况下，一个子类只能有一个基类，要实现多重继承，可以通过多级继承来实现。

继承概念的实现方式主要有2类：实现继承、接口继承。

Ø         实现继承是指使用基类的属性和方法而无需额外编码的能力；

Ø         接口继承是指仅使用属性和方法的名称、但是子类必须提供实现的能力(子类重构爹类方法)；

在考虑使用继承时，有一点需要注意，那就是两个类之间的关系应该是“属于”关系。例如，Employee 是一个人，Manager 也是一个人，因此这两个类都可以继承 Person 类。但是 Leg 类却不能继承 Person 类，因为腿并不是一个人。

### **Polymorphism 多态**

多态是面向对象的重要特性,简单点说:“一个接口，多种实现”，指一个基类中派生出了不同的子类，且每个子类在继承了同样的方法名的同时又对父类的方法做了不同的实现，这就是同一种事物表现出的多种形态。
编程其实就是一个将具体世界进行抽象化的过程，多态就是抽象化的一种体现，把一系列具体事物的共同点抽象出来, 再通过这个抽象的事物, 与不同的具体事物进行对话。
对不同类的对象发出相同的消息将会有不同的行为。比如，你的老板让所有员工在九点钟开始工作, 他只要在九点钟的时候说：“开始工作”即可，而不需要对销售人员说：“开始销售工作”，对技术人员说：“开始技术工作”, 因为“员工”是一个抽象的事物, 只要是员工就可以开始工作，他知道这一点就行了。至于每个员工，当然会各司其职，做各自的工作。
多态允许将子类的对象当作父类的对象使用，某父类型的引用指向其子类型的对象,调用的方法是该子类型的方法。这里引用和调用方法的代码编译前就已经决定了,而引用所指向的对象可以在运行期间动态绑定



### Method 方法

也称成员函数，是指对象上的操作，作为类声明的一部分来定义。方法定义了对一个对象可以执行的操作





### 构造函数

`__init__()`叫做初始化方法(或构造方法)， 在类被调用时，这个方法(虽然它是函数形式，但在类中就不叫函数了,叫方法)会自动执行，进行一些初始化的动作

一种成员函数，用来创建对象时初始化对象。构造函数一般与它所属的类完全同名



执行r1 = Role('Alex','police','AK47**’**)时，python的解释器其实干了两件事：

1. 在内存中开辟一块空间指向r1这个变量名
2. 调用Role这个类并执行其中的__init__(…)方法，相当于Role.__init__(r1,'Alex','police',**’****AK47’),**这么做是为什么呢？ 是为了把'Alex','police',’AK47’这3个值跟刚开辟的r1关联起来，是为了把'Alex','police',’AK47’这3个值跟刚开辟的r1关联起来，是为了把'Alex','police',’AK47’这3个值跟刚开辟的r1关联起来，重要的事情说3次， 因为关联起来后，你就可以直接r1.name, r1.weapon 这样来调用啦。所以，为实现这种关联，在调用__init__方法时，就必须把r1这个变量也传进去，否则__init__不知道要把那3个参数跟谁关联呀。
3. 所以这个__init__(…)方法里的，self.name = name , self.role = role 等等的意思就是要把这几个值 存到r1的内存空间里。



上面的这个r1 = Role('Alex','police','AK47**’**)动作，叫做类的“实例化”， 就是把一个虚拟的抽象的类，通过这个动作，变成了一个具体的对象了， 这个对象就叫做实例

刚才定义的这个类体现了面向对象的第一个基本特性，封装，**其实就是使用构造方法将内容封装到某个具体对象中，然后通过对象直接或者self间接获取被封装的内容**

 

### 析构函数

析构函数与构造函数相反，当对象脱离作用域时（例如对象所在的函数已调用完毕），系统自动执行析构函数。









## Hello world

```
class Dog:

    def __init__(self, name):
        self.name = name

    def bark(self):
        print('%s: wangwang.' % self.name)

d1 = Dog('MyDog')

d1.bark()

>>>
MyDog: wangwang.
```



## 类的声明
```python
class Person:          #定义一个类Person
    def SayHi(self):   #类成员函数必须要有一个参数self,表示类的实例(对象)自身
        print('Hi')

p = Person()           #定义类Person的对象p, 用p来访问类的成员变量和成员函数
p.SayHi()              #调用类Person的成员函数SayHi() 
>>>
hi
```
```python
class MyString:
    str = "MyString"
    def output(self):
        print(self.str)

s = MyString()
s.output()
>>>
MyString
```



## 数据及行为封装

```python
class Door():
    def __init__(self, number, status):
        self.number = number
        self.status = status
        
    def open(self):
        self.status = 'opening'
        
    def close(self):
        self.status = 'closed'
        
door1 = Door(1, 'closed')
```

## 构造函数
```python
class MyString:
    def __init__(self):      # __init__构造函数, 通过构造函数对类进行初始化操作
        self.str = "MyString"

    def output(self):
        print(self.str)

s = MyString()
s.output()
>>>
MyString
```



### 带参数的构造函数

```python
class UserInfo:
    def __init__(self, name, pwd):
        self.username = name
        self._pwd = pwd

    def output(self):
        print("User: "+self.username+"\nPasswd:" +self._pwd)

u = UserInfo("Rick", "123456")
u.output()
>>>
User: Rick
Passwd:123456
```



## 析构函数

```python
class MyString:
    def __init__(self):  #构造函数
        self.str = "MyString"
    def __del__(self):   #析构函数
        print("Bye")

    def output(self):
        print(self.str)

s = MyString()

s.output()
del s   # 删除对象
>>>
MyString
Bye
```



## 静态变量

静态变量和静态方法是类的静态成员，他们与普通的成员变量和成员方法不同，静态类成员与具体的对象没有关系，而是只属于定义他们的类

```python
class Users(object):
    online_count = 0   # 静态变量 记录当前用户数量
    def __init__(self):  #构造函数, 创建对象时Users.online_count +1
        Users.online_count += 1
    def __del__(self):   #析构函数,释放对象时Users.online_count -1
        Users.online_count -= 1

a = Users()  #创建Users对象
a.online_count += 1
print(Users.online_count)
>
1
```

## 静态方法

静态方法只属于定义他的类，而不属于任何一个具体的对象

静态方法无需传入self参数，因此在静态方法中无法访问实例变量

静态方法不能直接访问类的静态变量，但可以通过类名引用静态变量

```python
class MyClass:
    var1 = "String1"
    @staticmethod   #静态方法
    def staticmd():
        print('I am static method')

MyClass.staticmd()  #调用了静态方法
c = MyClass()
c.staticmd()
>>>
I am static method
I am static method
```



## 实例变量

实例变量的作用域，就是实例本身



## 实例方法





## 类方法

与静态方法一样，类方法可以使用类名调用类方法

与静态方法一样，类成员方法也无法访问实例变量，但可以访问类的静态变量

类方法需传入代表类的cls参数

```python
class MyClass:
    val1 = "String1"  #静态变量
    def __init__(self):
        self.val2 = "Value 2"
    @classmethod      #类方法
    def classmd(cls):
        print('Class: ' + str(cls) + ',val1: ' + cls.val1 + ', Cannot access value 2')

MyClass.classmd()
c = MyClass()
c.classmd()
>>> 
Class: <class '__main__.MyClass'>,val1: String1, Cannot access value 2
Class: <class '__main__.MyClass'>,val1: String1, Cannot access value 2
```



## instance() 函数判断对象类型

使用instance()函数检测一个给定的对象是否属于（继承）某个类或类型，是为True，否为False

```python
class MyClass:
    val1 = "String1"   #静态变量
    def __init__(self):
        self.val2 = "Value 2"

c = MyClass()
print(isinstance(c, MyClass))
l = [1, 2, 3, 4]
print(isinstance(l, list))
>>> 
True
True
```



## 类的继承

类可以继承其他类的内容，包括成员变量和成员函数

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
MyUser2 = UserLogin('Leo', now)
MyUser3 = UserLogin('Josh', now)

MyUser1.DisplayUsername()   #访问类Users的函数
MyUser1.DisplayLoginTime()     #访问子类的函数
MyUser2.DisplayUsername()
MyUser2.DisplayLoginTime()
MyUser3.DisplayUsername()
MyUser3.DisplayLoginTime()

>
(Construct fucntion:Rick)
(Construct fucntion:Leo)
(Construct fucntion:Josh)
Rick
Login time: 2016-09-10 16:20:45
Leo
Login time: 2016-09-10 16:20:45
Josh
Login time: 2016-09-10 16:20:45
​```
```



## 多态

抽象类中定义的一个方法，可以在其子类中重新实现，不同子类中实现的方法也不相同

```python
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