---
title: "dict"
date: 2018-08-18 10:12
collection: 基本变量类型
---

[TOC]



# 字典



字典是一种无序集合
字典是一种kv结构
value 可以是任何对象
key是唯一的
key必须是可hash 对象




## 定义字典

```python
In [26]: d = {}

In [27]: d = dict()

In [28]: d = {'a':1, 'b':2}
```



## 字典的常用操作

### 添加元素

```
In [1]: d = {}

In [2]: d['a'] = 1

In [3]: d
Out[3]: {'a': 1}
```



### 查找元素

#### get

未找到不会报错

```
In [7]: d
Out[7]: {'a': 1, 'b': 2, 'c': 3}

In [8]: d.get('a')
Out[8]: 1

In [9]: d.get('d')

In [10]: 
```



#### in

```
In [10]: d
Out[10]: {'a': 1, 'b': 2, 'c': 3}

In [11]: 'a' in d
Out[11]: True
```





### 访问元素


#### key

```python
In [29]: d
Out[29]: {'a': 1, 'b': 2}

In [30]: d['a'] = 5

In [31]: d
Out[31]: {'a': 5, 'b': 2}

In [32]: d['c']
---------------------------------------------------------------------------
KeyError                                  Traceback (most recent call last)
<ipython-input-32-3e4d85f12902> in <module>()
----> 1 d['c']

KeyError: 'c'

In [2]: d.get('a')
Out[2]: 1

In [3]: d.get('c', 'cannot found c')
Out[3]: 'cannot found c'
```

#### keys, values, items 遍历字典

```python
In [33]: d
Out[33]: {'a': 5, 'b': 2}

In [34]: d.keys()
Out[34]: dict_keys(['a', 'b'])

In [35]: d.values()
Out[35]: dict_values([5, 2])

In [36]: d.items()
Out[36]: dict_items([('a', 5), ('b', 2)])

In [2]: d
Out[2]: {'a': 1, 'b': 2, 'c': 3}

In [3]: for k, v in d.items():
   ...:     print('{0} -> {1}'.format(k, v))
   ...:     
c -> 3
b -> 2
a -> 1


```


### 删除元素

#### pop

```python
In [37]: d
Out[37]: {'a': 5, 'b': 2}

In [38]: d.pop('a')
Out[38]: 5

In [39]: d
Out[39]: {'b': 2}

In [40]: d.pop('c')
---------------------------------------------------------------------------
KeyError                                  Traceback (most recent call last)
<ipython-input-40-adf338c8a0db> in <module>()
----> 1 d.pop('c')

KeyError: 'c'

In [41]: d.pop('c', True)
Out[41]: True
```

#### popitem 

随机删除

```python
In [44]: d
Out[44]: {'a': 1, 'b': 2}

In [45]: d.popitem()
Out[45]: ('a', 1)

In [46]: d.popitem()
Out[46]: ('b', 2)

In [47]: d
Out[47]: {}
```

#### del 

关键字 删除

```python
In [4]: d
Out[4]: {'a': 1, 'b': 2}

In [5]: del d['a']

In [6]: d
Out[6]: {'b': 2}
```