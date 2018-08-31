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



# 类的定义

```python
class ClassName:
    pass

# 等价于

class ClassName(object):
    pass
```

```python
class Person:          #定义一个类Person
    def SayHi(self):   #类成员函数必须要有一个参数self,表示类的实例(对象)自身
        print('Hi')

p = Person()           #定义类Person的对象p, 用p来访问类的成员变量和成员函数
p.SayHi()              #调用类Person的成员函数SayHi() 
>>>
hi
```



## 方法定义 

```python
class ClassName:
    def method_name(self):
        pass
```



### 私有方法

`__val` 但不以__结尾的

```
class A:
    def __init__(self, x):
        self.__val = x

    def __add(self, i):
        self.__val += i

    def get_val(self):
        return self.__val

    def increase(self):
        self.__add(1)

a = A(5)

a.__add
>>>
Traceback (most recent call last):
  File "/Users/xhxu/python/python3/test/10.py", line 15, in <module>
    a.__add()
AttributeError: 'A' object has no attribute '__add'
```

```
class A:
    def __init__(self, x):
        self.__val = x

    def __add(self, i):
        self.__val += i

    def get_val(self):
        return self.__val

    def increase(self):
        self.__add(1)

a = A(5)

print(a.get_val())
>>>
5
```

在类内部对行为进行封装, increase 对__add封装

```
class A:
    def __init__(self, x):
        self.__val = x

    def __add(self, i):
        self.__val += i

    def get_val(self):
        return self.__val

    def increase(self):
        self.__add(1)

a = A(5)
print(a.get_val())

a.increase()
print(a.get_val())
>>>
5
6
```



#### 私有方法原理

python并没有真正的私有，变量改名 _classname__val来绕过

```
class A:
    def __init__(self, x):
        self.__val = x

    def __add(self, i):
        self.__val += i

    def get_val(self):
        return self.__val

    def increase(self):
        self.__add(1)

a = A(5)
print(a.get_val())

a.increase()
print(a.get_val())

print(dir(a))
print(a._A__val)
>>>
5
6
['_A__add', '_A__val', '__class__', '__delattr__', '__dict__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__gt__', '__hash__', '__init__', '__le__', '__lt__', '__module__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', '__weakref__', 'get_val', 'increase']
6
```





## 构造方法

```python
class ClassName:
    def __init__(self):
        pass
```

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



构造方法无参数，可以省略构造方法

```
class A:
    __val = 3

    def get_val(self):
        return self.__val

a = A()
print(a.get_val())
a.__val
>>>
Traceback (most recent call last):
  File "/Users/xhxu/python/python3/test/9.py", line 9, in <module>
    a.__val
AttributeError: 'A' object has no attribute '__val'
3
```



## 实例化

`__init__` 只是初始化类变量的作用

```python
class A:
    def __init__(self, x):
        self.x = x

# 实例化
a = A(5)

# 绑定实力变量
print(a.x)
>>>
5
```



### 类的新的属性

```
class A:

    def __init__(self, x):
        self.x = x

a = A(5)
a.name = True
print(a.name)
>>>
True
```



### 实例化类原理

```
class A:
    def __new__(cls, *args, **kwargs):
        print("call __new__")
        print("type cls", type(cls))
        return object.__new__(cls)

    def __init__(self, x):
        print("call __init__")
        print("type self", type(self))
        s1 = set (dir(self))
        self.x = x
        s2 = set(dir(self))
        print(s2 - s1)


a = A(5)
>>>
call __new__
type cls <class 'type'>
call __init__
type self <class '__main__.A'>
{'x'}
```

> cls 代表class A这个对象
>
> dir 会返回所有属性



若new方法不返回，init方法不执行

```
class A:
    def __new__(cls, *args, **kwargs):
        print("call __new__")
        print("type cls", type(cls))
        # return object.__new__(cls)

    def __init__(self, x):
        print("call __init__")
        print("type self", type(self))
        s1 = set (dir(self))
        self.x = x
        s2 = set(dir(self))
        print(s2 - s1)


a = A(5)
>>>
call __new__
type cls <class 'type'>
```



## 封装

封装只能在类的内部访问

```python
class A:
    def __init__(self, x):
        self.__value = x

    def __add(self):
        self.__value += i

    def get_value(self):
        return self.__value

    def __increase(self):
        self.__add(1)

a = A(5)
print(a.get_value())
print(a.__value)
>>>
5
Traceback (most recent call last):
  File "/Users/xhxu/python/python3/test/3.py", line 17, in <module>
    print(a.__value)
AttributeError: 'A' object has no attribute '__value'
```



### 数据及行为封装

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



## 实例类型

```python
class A:
    # 通常不建议使用并修改(高手另说)
    def __new__(cls, *args, **kwargs):
        print('call __new__')
        print(type(cls))
        return object.__new__(cls)

    def __init__(self, x):
        print('call __init__')
        # self 是实例本身
        print(type(self))
        self.x = x

a = A(5)
>>>
call __new__
<class 'type'>
call __init__
<class '__main__.A'>
```





### 传入位置参数

```python
class A:
    def __init__(self, x=5):
        #这里的值不由形式参数x决定，由abcd决定
        self.abcd = x

a1 = A(5)
a2 = A()
a3 = A(8)
print(a1.abcd)
print(a2.abcd)
print(a3.abcd)
>>>
5
5
8
```

### 带参数

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



## 实例变量

实例变量的作用域，就是实例本身

实例变量，也称静态属性

```
class Door:

    def __init__(self, number, status):
        self.number = number
        self.status = status

    def open(self):
        self.status = "opening"

    def close(self):
        self.status = "closed"


door1 = Door(1, 'closed')
```

> 这里是self.number 就是实例变量





### 实例方法

也称为类方法，动态属性

```
class Door:

    def __init__(self, number, status):
        self.number = number
        self.status = status

    def open(self):
        self.status = "opening"

    def close(self):
        self.status = "closed"

door1 = Door(1, 'closed')
```

> open和close均为类方法



## 类变量

类变量对所有的实例都是可见的，可以共享，且初值都是一样的

定义在方法体之外，可以通过类名访问，对所有方法共享

实例变量没有，会找类变量调用

```python
class A:
    val = 3
    def __init__(self, x):
        self.x = 3

a1 = A(5)
print(a1.val)

a2 = A(9)
print(a2.val)

a1.val += 1
print(a1.val)
>>>
3
3
4
```



对不可变对象赋值，就会变成新的变量

```
class A:
    val = [1, 2, 3]
    val_s = 'a'

    def __init__(self):
        pass

a1 = A()
a2 = A()
a1.val.append(4)
print(a1.val, id(a1.val))
print(a2.val, id(a2.val))

a3 = A()
a4 = A()
a3.val_s = 's'
print(a3.val_s, id(a3.val_s))
print(a4.val_s, id(a4.val_s))
>>>
[1, 2, 3, 4] 4442997640
[1, 2, 3, 4] 4442997640
s 4437293632
a 4437455120
```



### 私有类变量

私有类变量不能被实例访问

```python
class A:
    __value = 3
    def get_value(self):
        return self.__value

a = A()
print(a.get_value())
print(a.__value)
>>>
3

Traceback (most recent call last):
  File "/Users/xhxu/python/python3/test/3.py", line 8, in <module>
    print(a.__value)
AttributeError: 'A' object has no attribute '__value'
```



### 静态变量

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



## 类方法

类方法传递类本身， 可以访问私有的类变量

```python
class A:
    __val = 3

    @classmethod
    def get_val(cls):
        return cls.__val

a = A()

print(a.get_val())
print(A.get_val())
>>>
3
3
```

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



类方法不能访问实例变量, 但可以访问类变量

```
class A:
    __val = 3

    def __init__(self, x):
        self.x = x

    @classmethod
    def get_val(cls):
        print(cls.x)
        return cls.__val

a = A(5)
print(A.get_val())
>>>
Traceback (most recent call last):
  File "/Users/xhxu/python/python3/test/9.py", line 12, in <module>
    print(A.get_val())
  File "/Users/xhxu/python/python3/test/9.py", line 9, in get_val
    print(cls.x)
AttributeError: type object 'A' has no attribute 'x'
```







### 静态方法

静态方法并不能访问私有变量，只是给类方法加了类的属性

```
class A:
    __val = 3

    @staticmethod
    def print_val():
        print(__val)

a = A()

a.print_val()
A.print_val()
>>>
Traceback (most recent call last):
  File "/Users/xhxu/python/python3/test/9.py", line 10, in <module>
    a.print_val()
  File "/Users/xhxu/python/python3/test/9.py", line 6, in print_val
    print(__val)
NameError: name '_A__val' is not defined
```





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





### property属性

加上property 装饰器，在函数调用的时候，就不需要加上小括号

property调用的时候，只能调用self参数

常用于设定只读的属性

```python
class A:
    def __init__(self):
        self.__value = 0

    @property # property 可以访问私有的变量
    def value(self):
        if self.__value < 0:
            return 0
        return self.__value

    @value.setter # 加了这个装饰器，才会被认为是属性
    def value(self, val):
        if isinstance(val, (int, float)) and val >= 0:
            self.__value = val
        else:
            self.__value = 0

a = A()
a.value = -1
print(a.value)
a.value = 3
print(a.value)
>>>
0
3
```



同一个对象的不同属性之间可能存在依赖关系。当某个属性被修改时，依赖于该属性的其他属性也会同时变化。

```
class bird(object):
    feather = True

class chicken(bird):
    fly = False
    def __init__(self, age):
        self.age = age

    def getAdult(self):
        if self.age > 1.0:
            return True
        else:
            return False
    adult = property(getAdult)

summer = chicken(2)

print(summer.adult)
summer.age = 0.5
print(summer.adult)
>>>
True
False
```



#### property参数

property()最多可以加载四个参数。前三个参数为函数，分别用于处理查询特性，修改特性，删除特性。最后一个参数为特性文档，可以为一个字符串，用于说明。 

negative 为一个特性，用于表示数字的负数。property() 最后一个参数('I am negative one') 表示特性negative的说明文档

```
class num(object):
    def __init__(self, value):
        self.value = value
    def getNeg(self):
        return -self.value
    def setNeg(self, value):
        self.value = -value
    def delNeg(self):
        print('Value have been deleted')
        del self.value
    negative = property(getNeg, setNeg, delNeg, 'I am negative one')

x = num(1.1)
print(x.negative)

x.negative = -22
print(x.value)
print(num.negative.__doc__)
del x.negative
>>>
-1.1
22
I am negative one
Value have been deleted
```



#### property 实现的原理

```
class A:

    def __init__(self):
        self.__val = 0

    def get_val(self):
        return self.__val

    def set_val(self, value):
        self.__val = value

    val = property(get_val, set_val)

print(type(A.val))
a = A()

a.val = 3
print(a.val)
>>>
<class 'property'>
3
```



##属性

### 查询对象的属性

除了使用dir()来查询对象属性，还可以使用built-in函数来确认

```
# attr_name是一个字符串
hasattr(obj, attr_name) 

In [10]: a = [1, 2, 3]

In [11]: print(hasattr(a, 'append'))
True
```



### 查询对象所属的类和类名称

```
In [12]: a = [1, 2, 3]

In [13]: print(a.__class__)
<class 'list'>

In [15]: print(a.__class__.__name__)
list
```

### set属性

```
class A:

    def __init__(self):
        self.__val = 0

    @property
    def val(self):
        if self.__val < 0:
            return 0
        return self.__val

    @val.setter
    def val(self, value):
        if isinstance(value, (int, float)) and value >= 0:
            self.__val = value
        else:
            self.__val = 0


a = A()
print(a.val)
a.val = 3
print(a.val)
>>>
0
3
```



### 属性的__dict__系统

对象的属性可能来自与其类定义，叫做类属性(class attribute)。 

类属性可能来自类定义自身，也可能根据类定义继承来的。一个对象的属性还可能是该对象实例定义的，叫做对象属性(object attribute)

对象的属性存储在对象的__dict__属性中，__dict__为一个词典，键为属性名，对应的值为属性本身。

```
class bird(object):
    feather = True

class chicken(bird):
    fly = False
    def __init__(self, age):
        self.age = age

summer = chicken(2)

print(bird.__dict__)
print(chicken.__dict__)
print(summer.__dict__)

# 利用__class__属性找到对象的类，然后调用类的__base__属性来查询父类
summer.__dict__['age'] = 3
print(summer.__dict__['age'])

summer.age = 5
print(summer.age)
>>>
{'__weakref__': <attribute '__weakref__' of 'bird' objects>, '__doc__': None, '__module__': '__main__', 'feather': True, '__dict__': <attribute '__dict__' of 'bird' objects>}
{'__doc__': None, '__init__': <function chicken.__init__ at 0x10f1c6488>, '__module__': '__main__', 'fly': False}
{'age': 2}
3
5
```



## 析构函数

实例释放，销毁的时候执行

通常用于收尾工作，如数据库链接打开的临时文件

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



