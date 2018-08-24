---
title: "basic_knowledge 模块基础"
date: 2018-08-25 00:39
---

[TOC]

# 模块基本使用



## 定义

 .py 文件组成的代码集合就称为模块



模块分为三种：

- 自定义模块
- 内置标准模块（又称标准库）
- 开源模块



自定义模块 和开源模块的使用参考 http://www.cnblogs.com/wupeiqi/articles/4963027.html



## 导入方法

import 的本质就是路径检索

```
import module_name
import module_name_1, module_name_2
from modules import *
from modules import logger as my_logger
```



