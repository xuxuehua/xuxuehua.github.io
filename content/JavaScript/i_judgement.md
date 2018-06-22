---
title: "I_judgement 条件判断"
date: 2018-06-05 17:57
---

[TOC]

# Judgement



## 定义

* JavaScript使用`if () { ... } else { ... }`来进行条件判断
* 其中`else`语句是可选的。如果语句块只包含一条语句，尽管可以省略`{}`, 但还是不要避免错误

```
var age = 20;
if (age >= 18) { // 如果age >= 18为true，则执行if语句块
    alert('adult');
} else { // 否则执行else语句块
    alert('teenager');
}
```



## 多行条件判断

* 如果还要更细致地判断条件，可以使用多个`if...else...`的组合：

  ```
  var age = 3;
  if (age >= 18) {
      alert('adult');
  } else if (age >= 6) {
      alert('teenager');
  } else {
      alert('kid');
  }
  ```



## 默认判定

* JavaScript把`null`、`undefined`、`0`、`NaN`和空字符串`''`视为`false`，其他值一概视为`true`

