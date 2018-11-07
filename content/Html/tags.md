---
title: "tags 标签"
date: 2018-11-06 20:08
---


[TOC]


# 标签



## `<ol>` 有序列表

会生成序号



## `<dl>` 自定义列表



### `<dt>` title 



### `<dd>` data



### 列表嵌套

li 中可以嵌套其他的子ul ol dl等

自定义列表中的dd也可以嵌套其他ul dl ol





## `<table> ` 表格

boder="1" 添加表格外框



### `<thead>` 表头



#### `<th>`  头部数据



### `<tbody>` 表内容



#### `<tr>`  row 行



#### `<td>` data 内容



### 单元格合并

```
<td colspan="2"> 合并2列 （横向）

<td rowspan="2">  合并2行 （纵向）
```





## `<div>` 块标签

网页块的包裹



## `<a>`  超链接

```
<a href="http://www.xuxuehua.com">content</a>
```



### target 属性

_blank 在新页面

```
<a target="_blank" href="http://xuxuehua.com">xuxuehua</a>
```



_self 在当前页面打开

```
<a target="_self" href="http://xuxuehua.com">xuxuehua</a>
```



### 锚点链接

在当前页面滚动到指定位置

href 为标签的id

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
    <h1>基本特点</h1>
<ul>
    <li>
        <a href="#js1">1.js</a>
    </li>
    <li>
        <a href="#js2">2.interactive</a>
    </li>
    <li>
        <a href="#js3">3.embeded</a>
    </li>
    <li>
        <a href="#js4">4.multiplatform</a>
    </li>
    <li>
        <a href="#js5">5.scriptlanguage</a>
    </li>
</ul>


<p id="js1">1.JavaScript是一种属于网络的脚本语言,已经被广泛用于Web应用开发,常用来为网页添加各式各样的动态功能,为用户提供更流畅美观的浏览效果。通常JavaScript脚本是通过嵌入在HTML中来实现自身的功能的。 [3]  <br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>  </p>
是一种解释性脚本语言（代码不进行预编译）。 [4] 
<p id="js2">2.主要用来向HTML（标准通用标记语言下的一个应用）页面添加交互行为。 [4] <br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br> </p>
<p id="js3">3.可以直接嵌入HTML页面，但写成单独的js文件有利于结构和行为的分离。 [4] <br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br> </p>
<p id="js4">4.跨平台特性，在绝大多数浏览器的支持下，可以在多种平台下运行（如Windows、Linux、Mac、Android、iOS等）。 <br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br> </p>
<p id="js5">5.Javascript脚本语言同其他语言一样，有它自身的基本数据类型，表达式和算术运算符及程序的基本程序框架。Javascript提供了四种基本的数据类型和两种特殊数据类型用来处理数据和文字。而变量提供存放信息的地方，表达式则可以完成较复杂的信息处理。 [5] </p>
</body>
</html>
```



## `<img>` 图片标记





