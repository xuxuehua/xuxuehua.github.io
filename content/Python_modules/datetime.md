---
title: "datetime"
date: 2018-07-25 15:18
---



[TOC]



# datetime



## 当前时间

```
In [8]: datetime.datetime.now()
Out[8]: datetime.datetime(2018, 7, 25, 15, 37, 39, 596733)
```



### 当前时间+3天
```
datetime.datetime.now() + datetime.timedelta(+3)
datetime.datetime(2017, 5, 12, 17, 12, 42, 124379)
```

### 当前时间-3天
```
datetime.datetime.now() + datetime.timedelta(-3)
datetime.datetime(2017, 5, 6, 17, 13, 18, 474406)
```

### 当前时间+3小时
```
datetime.datetime.now() + datetime.timedelta(hours=3)
datetime.datetime(2017, 5, 9, 20, 13, 55, 678310)
```

### 当前时间+30分钟
```
datetime.datetime.now() + datetime.timedelta(minutes=30)
datetime.datetime(2017, 5, 9, 17, 44, 40, 392370)
```





## 