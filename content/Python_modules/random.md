---
title: "random"
date: 2018-08-25 22:49
---

[TOC]

# random

取随机值



## random()

```
In [5]: random.random()
Out[5]: 0.5265427803029777
```





## randint()

1-3之间

```
In [7]: random.randint(1, 3)
Out[7]: 3

In [8]: random.randint(1, 3)
Out[8]: 2

In [9]: random.randint(1, 3)
Out[9]: 1

In [10]: random.randint(1, 3)
Out[10]: 2

In [11]: random.randint(1, 3)
Out[11]: 2
```



## randrange()

0-2 之间

```
In [18]: random.randrange(1, 3)
Out[18]: 1

In [19]: random.randrange(1, 3)
Out[19]: 1

In [20]: random.randrange(1, 3)
Out[20]: 2

In [21]: random.randrange(1, 3)
Out[21]: 1
```



## choice()

```
In [22]: random.choice('hello')
Out[22]: 'e'

In [23]: random.choice('hello')
Out[23]: 'l'

In [24]: random.choice('hello')
Out[24]: 'o'

In [25]: random.choice([1, 2, 3])
Out[25]: 1

In [26]: random.choice([1, 2, 3])
Out[26]: 1
```



## sample()

```
In [27]: random.sample('hello', 2)
Out[27]: ['l', 'l']

In [28]: random.sample('hello', 2)
Out[28]: ['l', 'h']

In [29]: random.sample('hello', 2)
Out[29]: ['h', 'e']

In [30]: random.sample('hello', 2)
Out[30]: ['e', 'h']
```



## uniform()

```
In [31]: random.uniform(1, 3)
Out[31]: 2.039522432404592

In [32]: random.uniform(1, 3)
Out[32]: 2.0421261888899847

In [33]: random.uniform(1, 3)
Out[33]: 1.0705082811151863
```



## shuffle

洗牌功能

```
In [34]: L = [1, 2, 3, 4, 5, 6]

In [35]: random.shuffle(L)

In [36]: L
Out[36]: [1, 3, 4, 6, 5, 2]
```



## 验证码生成

```
import random

checkcode = ''

for i in range(4):
    current = random.randrange(0, 4)
    if current == i:
        tmp = chr(random.randint(65, 90))
    else:
        tmp = random.randint(0, 9)
    checkcode += str(tmp)
    
print(checkcode)
```

