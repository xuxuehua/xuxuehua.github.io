---
title: "error"
date: 2018-08-30 15:34
ollection: 异常处理
---

[TOC]



# 异常处理



异常处理一般用于debug程序



## 语法

在try语句块中放入容易犯错的部分，跟上except，说明语句在发生错误的时候会执行的返回值

```
re = iter(range(5))

try:
    for i in range(100):
        print(re.__next__())
except StopIteration:
    print('End at here', i)

print('hahaha')
>>>
0
1
2
3
4
End at here 5
hahaha
```



## 处理顺序

无法将异常交给合适的对象，异常将继续向上层抛出，直到捕捉或者造成主程序出错

```
def test_func():
    try:
        m = 1/0
    except NameError:
        print('Catch NameError in the sub-function')

try:
    test_func()
except ZeroDivisionError:
    print('Catch error in the main program')
>>>
Catch error in the main program
```



## finally

finally是无论是否有异常，最后都要做的一件事
1. try -> 异常 -> except -> finally
2. try -> 无异常 -> else -> finally



## raise 抛出异常

raise 语句可以抛出异常

```
print('test')
raise StopIteration
print('yes')
>>>
Traceback (most recent call last):
  File "/Users/xhxu/python/machine_learning/test.py", line 2, in <module>
    raise StopIteration
StopIteration
test
```