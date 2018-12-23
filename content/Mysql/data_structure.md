---
title: "data_structure"
date: 2018-12-20 20:39
---


[TOC]



# 数据类型



## 字符型

### CHAR / BINARY  定长



### VARCHAR / VARBINARY 变长 

需要结束符



### TEXT / TINYTEXT / MEDIUMTEXT / LONGTEXT



### BLOB / TINYBLOB / MEDIUMBLOB / LONGBLOB





## 字符类型修饰符



NOT NULL

非空约束



NULL



DEFAULT ‘STRING’ 

指明默认类型



CHARACTER SET

使用的字符集



COLLATION

使用排序的规则

```
mysql> SHOW CHARACTER SET;
mysql> SHOW COLLATION;
```









## 数值型



### 精确数值



#### 整型

##### TINYINT / SMALLINT / MEDIUMINT / INT / BIGINT





#### 整型数据修饰型

NOT NULL

NULL

DEFAULT NUMBER



##### AUTO_INCREMENT

UNSIGNED

PRIMARY KEY | UNIQUE KEY

NOT NULL

```
mysql> SELECT LAST_INSERT_ID();
```





#### 十进制型

##### DECIMAL



### 近似数值

#### 浮点型



##### FLOAT



##### DOUBLE



#### BIT





## 日期时间型



### DATE



### TIME



### DATETIME



### TIMESTAMP



### YEAR(2)  YEAR(4)





## 内建类型









## SQL mode

定义mysqld对约束等的响应行为

### 修改方式

需要修改权限，仅对修改后新建会话有效，对已经建立的会话无效

```
mysql> SET GLOBAL sql_mode='MODE';
mysql> SET @@global.sql_mode='MODE';
```



### 常用mode

```
TRADITIONAL
STRICT_TRANS_TABLES
STRICT_ALL_TABLES
etc
```





```
mysql> set sql_mode='TRADITIONAL';
```

> 只对当前会话有效



```
mysql> SHOW VARIABLES LIKE 'sql_mo%';
+---------------+----------------------------------------------------------------------------------------------------------------------------------+
| Variable_name | Value                                                                                                                            |
+---------------+----------------------------------------------------------------------------------------------------------------------------------+
| sql_mode      | STRICT_TRANS_TABLES,STRICT_ALL_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,TRADITIONAL,NO_ENGINE_SUBSTITUTION |
+---------------+----------------------------------------------------------------------------------------------------------------------------------+
1 row in set (0.00 sec)
```







## Mysql 数据文件类型

数据文件

索引文件

重做日志

撤销日志

二进制日志

错误日志

查询日志

慢查询日志

中继日志



