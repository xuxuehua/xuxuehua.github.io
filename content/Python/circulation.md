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





## while 

```
while judgement:
	operation
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

