---
title: "calculation 运算"
date: 2018-11-10 21:18
---


[TOC]


# calculation



## 四则运算 + - * /

```
#!/bin/bash

a=3
b=5

val=`expr $a + $b`
echo "a+b=$val"

val=`expr $a - $b`
echo "a-b=$val"

val=`expr $a \* $b`
echo "a*b=$val"

val=`expr $a / $b`
echo "a/b=$val"

>>>
a+b=8
a-b=-2
a*b=15
a/b=0
```





## 其它运算

### % 求余

```
#!/bin/bash

a=3
b=5

val=`expr $a % $b`
echo "a%b=$val"

>>>
a%b=3
```



### == 相等

```
#!/bin/bash

a=5
b=5

if [ $a == $b ]; then
    echo "$a is equal to $b"
fi

>>>
5 is equal to 5
```



### != 不相等

```
#!/bin/bash

a=3
b=5

if [ $a != $b ]; then
    echo "$a is not equal to $b"
fi

>>>
3 is not equal to 5
```

