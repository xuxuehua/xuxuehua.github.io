---
title: "list 列表"
date: 2018-08-14 00:16
collection: 基本变量类型
---

[TOC]

# 列表
list 是最常用的线性数据结构
list是一系列元素的有序组合
list是可变的
list 可以嵌套任何数据类型



## 定义列表

```python
In [1]: L = []

In [2]: L = list()

In [3]: L = [1, 2, 3]
```

## 列表常用操作

### 增
#### append

```python
In [4]: L
Out[4]: [1, 2, 3]

In [5]: L.append(4)

In [6]: L
Out[6]: [1, 2, 3, 4]
```

#### extend
```python
In [9]: L = [1, 2, 3, 4]

In [10]: L.extend([5, 6, 7])

In [11]: L
Out[11]: [1, 2, 3, 4, 5, 6, 7]
```


#### insert
```python
In [11]: L
Out[11]: [1, 2, 3, 4, 5, 6, 7]

In [12]: L.insert(0, 0)

In [13]: L
Out[13]: [0, 1, 2, 3, 4, 5, 6, 7]
```

### 删
#### remove
```python
In [15]: L
Out[15]: [0, 1, 2, 3, 4, 5, 6, 7]

In [16]: L.remove(3)

In [17]: L
Out[17]: [0, 1, 2, 4, 5, 6, 7]
```

#### pop
```python
In [18]: L
Out[18]: [0, 1, 2, 4, 5, 6, 7]

In [19]: L.pop(0)
Out[19]: 0

In [20]: L
Out[20]: [1, 2, 4, 5, 6, 7]
```

#### clear
```python
In [21]: L
Out[21]: [1, 2, 4, 5, 6, 7]

In [22]: L.clear()

In [23]: L
Out[23]: []
```



#### del

```

```





### 改

#### reverse
```python
In [26]: L
Out[26]: [0, 1, 2, 3, 4, 3, 4, 5, 6, 7]

In [27]: L.reverse()

In [28]: L
Out[28]: [7, 6, 5, 4, 3, 4, 3, 2, 1, 0]
```

#### sort
```python
In [28]: L
Out[28]: [7, 6, 5, 4, 3, 4, 3, 2, 1, 0]

In [29]: L.sort()

In [30]: L
Out[30]: [0, 1, 2, 3, 3, 4, 4, 5, 6, 7]

In [30]: L
Out[30]: [0, 1, 2, 3, 3, 4, 4, 5, 6, 7]

In [31]: L.sort(reverse=True)

In [32]: L
Out[32]: [7, 6, 5, 4, 4, 3, 3, 2, 1, 0]
```

### 查

#### count 

```python
In [3]: L
Out[3]: [0, 1, 2, 3, 3, 4, 4, 5, 6, 7]

In [4]: L.count(3)
Out[4]: 2

In [5]: L.count(8)
Out[5]: 0
```

#### index

```python
In [6]: L
Out[6]: [0, 1, 2, 3, 3, 4, 4, 5, 6, 7]

In [7]: L.index(3)
Out[7]: 3

In [8]: L.index(4)
Out[8]: 5

In [9]: L.index(8)
---------------------------------------------------------------------------
ValueError                                Traceback (most recent call last)
<ipython-input-9-4d02a661bd55> in <module>()
----> 1 L.index(8)

ValueError: 8 is not in list

```



#### len

```

```



#### enumerate

```

```



#### sort

```

```



### 

### 复制

####  copy

L1 L2不是同一个object

```python
In [1]: L = [1, 2, 3]

In [2]: L1 = L.copy()

In [3]: L2 = L

In [4]: L
Out[4]: [1, 2, 3]

In [5]: L1
Out[5]: [1, 2, 3]

In [6]: L2
Out[6]: [1, 2, 3]

In [7]: L.append(4)

In [8]: L
Out[8]: [1, 2, 3, 4]

In [9]: L1
Out[9]: [1, 2, 3]

In [10]: L2
Out[10]: [1, 2, 3, 4]

In [11]: id(L), id(L1), id(L2)
Out[11]: (4500763656, 4500804360, 4500763656)
```

### 快速创建相同的列表

```python
In [10]: [1] * 6
Out[10]: [1, 1, 1, 1, 1, 1]

In [11]: [1, 2] * 3
Out[11]: [1, 2, 1, 2, 1, 2]

In [12]: [[]] * 3
Out[12]: [[], [], []]
```



### 下标操作及切片

#### 更新数值

```
In [29]: L
Out[29]: [0, 1, 2, 3, 3, 4, 4, 5, 6, 7]

In [30]: L[0] = 10

In [31]: L
Out[31]: [10, 1, 2, 3, 3, 4, 4, 5, 6, 7]
```



#### 范围取值

```
In [31]: L
Out[31]: [10, 1, 2, 3, 3, 4, 4, 5, 6, 7]

In [32]: L[3:5]
Out[32]: [3, 3]

In [33]: L[:5]
Out[33]: [10, 1, 2, 3, 3]

In [34]: L[3:]
Out[34]: [3, 3, 4, 4, 5, 6, 7]

In [35]: L[:]
Out[35]: [10, 1, 2, 3, 3, 4, 4, 5, 6, 7]

In [36]: L[3: -2]
Out[36]: [3, 3, 4, 4, 5]

In [37]: L[-4:-1]
Out[37]: [4, 5, 6]

In [38]: L[2:6:2]
Out[38]: [2, 3]

In [39]: L[6:2:-1]
Out[39]: [4, 4, 3, 3]

In [40]: L[::-1]
Out[40]: [7, 6, 5, 4, 4, 3, 3, 2, 1, 10]

In [41]: L[::2]
Out[41]: [10, 2, 3, 4, 6]
```





## 列表解析

> 列表解析是python的重要的语法糖
> 列表解析的速度比for in迭代快



### 基本语法

`ret = [expression for item in iterator]` 

等价于 
```python
ret = []
for item in iterator:
    ret.append(expression)
```




```python
In [2]: L
Out[2]: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

In [3]: [x+1 for x in L]
Out[3]: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

```

迭代时间快

```python
In [10]: timeit.timeit('[x+1 for x in range(10)]')

Out[10]: 2.861458881001454

In [11]: timeit.timeit('''
    ...: l=[]
    ...: for x in range(10):
    ...:     l.append(x+1)
    ...: ''')
Out[11]: 3.5815405790053774
```


### 带条件

```python
Out[12]: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

In [13]: [x+1 for x in L if x%2 ==0]
Out[13]: [1, 3, 5, 7, 9]

In [15]: [x+1 for x in L if x%2 == 0 if x>2]
Out[15]: [5, 7, 9]

```

## 笛卡尔积

### 基本语法

`ret = [expression for x in X for y in Y]`

等价于
```python
ret = []
for x in X:
    for y in Y:
        ret.append(expression)
```


```python
In [17]: l1 = [1, 2, 3]

In [18]: l2 = [4, 5, 6]

In [19]: [(x, y) for x in l1 for y in l2]
Out[19]: [(1, 4), (1, 5), (1, 6), (2, 4), (2, 5), (2, 6), (3, 4), (3, 5), (3, 6)]
```