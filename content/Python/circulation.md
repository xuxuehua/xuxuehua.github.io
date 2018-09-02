---
title: "circulation 循环"
date: 2018-06-29 22:32
---

[TOC]



# circulation 循环



## if

```
if judgement:
	operation
```


```
if judgement:
	operation
else:
	operation
```

```
if judgement:
	operation
elif judgement:
	operation
else
	operation
```



```
In [4]: if True:
   ...:     print('Hello Python')
   ...:     
Hello Python

In [5]: if 2 > 1: 
   ...:     print('2 is greater than 1')
   ...:     
2 is greater than 1

In [6]: if 1 > 2:
   ...:     print('1 is greater than 2')
   ...: else:
   ...:     print('1 is not greater than 2')
   ...:     
1 is not greater than 2

In [7]: if 1 > 2:
   ...:     print('1 is greater than 2')
   ...: elif 2 > 1:
   ...:     print('1 is not greater than 2')
   ...: else:
   ...:     print('1 is equal to 2')
   ...:     
1 is not greater than 2
```





## while 

```
while judgement:
	operation
```

```
In [8]: n = 1

In [9]: while n <= 10:
   ...:     print(n)
   ...:     n += 1
   ...:     
1
2
3
4
5
6
7
8
9
10
```





## for

```
for i in range(10):
	print(i)
>>>
0
1
2
3
4
5
6
7
8
9
```



### for... else 

完成循环，就执行else

```
guess_num = 34

for i in range(1):
    my_num = int(input("my_num: "))
    if my_num == guess_num:
        print('Yes')
        break
    else:
        print("No")
else:
    print('This is else from for circulation.')
>>>
my_num: 1
No
This is else from for circulation.
```



破坏循环，跳过else

```
guess_num = 34

for i in range(1):
    my_num = int(input("my_num: "))
    if my_num == guess_num:
        print('Yes')
        break
    else:
        print("No")
else:
    print('This is else from for circulation.')
>>>
my_num: 34
Yes
```





## break

结束整个循环



## continue

跳出本次循环，进入下一次循环

