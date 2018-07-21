---
title: "number 数字"
date: 2018-06-04 11:35
collection: 基本变量类型
---



[TOC]



# Number



## 定义



* JavaScript不区分整数和浮点数，统一用Number表示，以下都是合法的Number类型

```
123; // 整数123
0.456; // 浮点数0.456
1.2345e3; // 科学计数法表示1.2345x1000，等同于1234.5
-99; // 负数
NaN; // NaN表示Not a Number，当无法计算结果时用NaN表示
Infinity; // Infinity表示无限大，当数值超过了JavaScript的Number所能表示的最大值时，就表示为Infinity
```



## 四则运算

* y=5

| +    | 加                | x=y+2 | x=7   |
| ---- | ----------------- | ----- | ----- |
| -    | 减                | x=y-2 | x=3   |
| *    | 乘                | x=y*2 | x=10  |
| /    | 除                | x=y/2 | x=2.5 |
| %    | 求余数 (保留整数) | x=y%2 | x=1   |
| ++   | 累加              | x=++y | x=6   |
| --   | 递减              | x=--y | x=4   |



### 除法

```
2 / 0;  // Infinity
0 / 0; NaN
(1 + 2) * 5 / 2;  // 7.5
```



### 求余

* 只保留整数

```
10 % 3; // 1
10.5 % 3 // 1.5
```



### 数字与字符串相加

```
<html>
<body>

<script type="text/javascript">
x=5+5;
document.write(x);
document.write("<br />");
x="5"+"5";
document.write(x);
document.write("<br />");
x=5+"5";
document.write(x);
document.write("<br />");
x="5"+5;
document.write(x);
document.write("<br />");
</script>

<h3>规则是：</h3>

<p><strong>如果把数字与字符串相加，结果将成为字符串。</strong></p>

</body>
</html>
>>>
10
55
55
55
```



### 



## 比较运算

给定 x=5，下面的表格解释了比较运算符：

| 运算符 | 描述             | 例子                            |
| ------ | ---------------- | ------------------------------- |
| ==     | 等于             | x==8 为 false                   |
| ===    | 全等（值和类型） | x===5 为 true；x==="5" 为 false |
| !=     | 不等于           | x!=8 为 true                    |
| >      | 大于             | x>8 为 false                    |
| <      | 小于             | x<8 为 true                     |
| >=     | 大于或等于       | x>=8 为 false                   |
| <=     | 小于或等于       | x<=8 为 true                    |



对Number做比较时，可以通过比较运算符得到一个布尔值

```
2 > 5; // false
5 >= 2; // true
7 == 7; // true
```





## 逻辑运算符

给定 x=6 以及 y=3，下表解释了逻辑运算符：

| 运算符 | 描述 | 例子                      |
| ------ | ---- | ------------------------- |
| &&     | and  | (x < 10 && y > 1) 为 true |
| \|\|   | or   | (x==5 \|\| y==5) 为 false |
| !      | not  | !(x==y) 为 true           |

















