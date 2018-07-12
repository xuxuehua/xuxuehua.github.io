---
title: "underscore"
date: 2018-07-10 14:53
collection: 第三方库
---

[TOC]



# underscore 库

underscore库，使用统一的函数来实现`map()`、`filter()`这些操作

underscore则提供了一套完善的函数式编程的接口，让我们更方便地在JavaScript中实现函数式编程。

jQuery在加载时，会把自身绑定到唯一的全局变量`$`上，underscore与其类似，会把自身绑定到唯一的全局变量`_`上，这也是为啥它的名字叫underscore的原因。



## 使用



用underscore实现`map()`操作如下：

```
'use strict';
_.map([1, 2, 3], (x) => x * x); // [1, 4, 9]
```

咋一看比直接用`Array.map()`要麻烦一点，可是underscore的`map()`还可以作用于Object：

```
'use strict';
_.map({ a: 1, b: 2, c: 3 }, (v, k) => k + '=' + v); // ['a=1', 'b=2', 'c=3']
```