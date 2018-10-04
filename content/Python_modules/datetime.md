---
title: "datetime"
date: 2018-07-25 15:18
---



[TOC]



# datetime

datetime包是基于time包的一个高级包。

datetime 可以理解为date和time 两个组成部分

可以分开管理datetime.date类和datetime.time类

也可以合在一起datetime.datetime类

datetime模块定义了5个类

## .date 日期

date类有三个参数,datetime.date(year,month,day)，返回year-month-day



### ctime() 

datetime.date.ctime(),返回格式如 Sun Apr 16 00:00:00 2017



### fromtimestamp(timestamp)

根据给定的时间戮，返回一个date对象；datetime.date.today()作用相同

```
In [17]: datetime.date.fromtimestamp(1537550244)
Out[17]: datetime.date(2018, 9, 22)
```





### isocalendar()

datetime.date.isocalendar():返回格式如(year，month，day)的元组,(2017, 15, 6)



### isoformat()

datetime.date.isoformat()：返回格式如YYYY-MM-DD



### isoweekday()

datetime.date.isoweekday()：返回给定日期的星期（0-6），星期一=0，星期日=6



### replace(year,month,day)

datetime.date.replace(year,month,day)：替换给定日期，但不改变原日期



### strftime(format)

datetime.date.strftime(format):把日期时间按照给定的format进行格式化。

#### 日期格式化符号

```
%y 两位数的年份表示（00-99）

%Y 四位数的年份表示（000-9999）

%m 月份（01-12）

%d 月内中的一天（0-31）

%H 24小时制小时数（0-23）

%I 12小时制小时数（01-12）

%M 分钟数（00=59）

%S 秒（00-59）

%a 本地简化星期名称

%A 本地完整星期名称

%b 本地简化的月份名称

%B 本地完整的月份名称

%c 本地相应的日期表示和时间表示

%j 年内的一天（001-366）

%p 本地A.M.或P.M.的等价符

%U 一年中的星期数（00-53）星期天为星期的开始

%w 星期（0-6），星期天为星期的开始

%W 一年中的星期数（00-53）星期一为星期的开始

%x 本地相应的日期表示

%X 本地相应的时间表示

%Z 当前时区的名称

%% %号本身

```



### timetuple()

datetime.date.timetuple()：返回日期对应的time.struct_time对象

time.struct_time(tm_year=2017, tm_mon=4, tm_mday=15, tm_hour=0, tm_min=0, tm_sec=0, tm_wday=5, tm_yday=105, tm_isdst=-1)



### weekday()

datetime.date.weekday()：返回日期的星期



## .datetime 日期时间精确到秒

datetime类有很多参数，datetime(year, month, day[, hour[, minute[, second[, microsecond[,tzinfo]]]]])，返回年月日，时分秒



### ctime()

datetime.datetime.ctime()



### now() 当前时间

datetime.datetime.now().date()：返回当前日期时间的日期部分

datetime.datetime.now().time()：返回当前日期时间的时间部分



* 当前系统时间

```
In [8]: datetime.datetime.now()
Out[8]: datetime.datetime(2018, 7, 25, 15, 37, 39, 596733)
```

* 当前时间+3天

```
datetime.datetime.now() + datetime.timedelta(+3)
datetime.datetime(2017, 5, 12, 17, 12, 42, 124379)
```

* 当前时间-3天

```
datetime.datetime.now() + datetime.timedelta(-3)
datetime.datetime(2017, 5, 6, 17, 13, 18, 474406)
```

* 当前时间+3小时

```
datetime.datetime.now() + datetime.timedelta(hours=3)
datetime.datetime(2017, 5, 9, 20, 13, 55, 678310)
```

* 当前时间+30分钟 

```
datetime.datetime.now() + datetime.timedelta(minutes=30)
datetime.datetime(2017, 5, 9, 17, 44, 40, 392370)
```



### fromtimestamp()

datetime.datetime.fromtimestamp()



### replace()

datetime.datetime.replace()



### strftime()

datetime.datetime.strftime()：由日期格式转化为字符串格式

datetime.datetime.now().strftime('%b-%d-%Y %H:%M:%S')

'Apr-16-2017 21:01:35'



### strptime()

datetime.datetime.strptime():由字符串格式转化为日期格式

```
from datetime import datetime

format = "output-%Y-%m-%d-%H%M%S.txt"
str = "output-1990-3-14-001000.txt"

t = datetime.strptime(str, format)
print(t)
>>>
1990-03-14 00:10:00
```

## .time 具体时间精确到秒

time类有5个参数，datetime.time(hour,minute,second,microsecond,tzoninfo),返回08:29:30



### replace()

datetime.time.replace()



### strftime(format)

datetime.time.strftime(format):按照format格式返回时间



### tzname()

datetime.time.tzname()：返回时区名字



### utcoffset()

datetime.time.utcoffset()：返回时区的时间偏移量



## .timedelta 两个时间点的间隔

datetime.datetime.timedelta用于计算两个日期之间的差值

```
import datetime
t = datetime.datetime(2016, 12, 11, 20, 30)
t_next = datetime.datetime(2016, 12, 11, 21, 00)
delta1 = datetime.timedelta(seconds=600)
delta2 = datetime.timedelta(weeks = 3)
print(t + delta1)
print(t + delta2)
print(t_next - t)
>>>
2016-12-11 20:40:00
2017-01-01 20:30:00
0:30:00
```



## .tzinfo 时区的相关信息


