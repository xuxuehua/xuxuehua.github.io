---
title: "selector 选择器"
date: 2018-11-13 14:31
---


[TOC]


# selector 选择器



## 通配符选择器 （不常用）

穿透力很强，优先级高于继承的样式，会覆盖继承的样式

```
* {}
```

```
* {
    margin: 0; /* 定义外边距 */
    padding: 0; /* 定义内边距 */
}
```



## 标签选择器

```
p {}
div {}
```

选择所有的p标签都设置成字体为红色

```
p {color: red;}
```



## ID 选择器

id命名必须以字符开头，包含数字，字母，下划线，连接符

```
#head {}
```



相同标签的不同展现形式

```css
<li id="a">Beijing</li>
<li id="b">Shanghai</li>
<li id="c">Guangzhou</li>
>>>

<style>
#a {
    background-color: red;
}
#b {
    background-color: blue;
}
#c {
    background-color: yellow;
}
</style>
```



## 类选择器

对class 属性进行选择

```
.head {}
```

```
.demo {
    color: red;
}
```



标签可以包含多个类选择器，在class标签中用空格隔开



## 复合选择器

### 标签指定式选择器 （使用较少）

两个或者多个基础选择器通过不同方式组合而成

第一个为标记选择器，第二个为class选择器或者id选择器，选择器之间不能有空格

```
h3.class {
    background-color: blue;
}

p#one {
    background-color: yellow;
}
```



### 后代选择器（包含选择器）（常用）

用来选择元素或者元素组的后代，把外层标记卸载前面，内容标记写在后面，中间用空格分隔

```
.class h3 {
    color: red;
}
```



### 并集选择器 （常用 ）

各个选择器通过逗号连接而成，任何形式的的选择器都可以作为并集选择器的一部分

```
.f-news a, .s-news a {
    color: silver;
}
```



常用的初始化设置

```
html, body, div, dt, dl, dd, ul, p {
    padding:0; /* 内边距 */
    margin:0; /* 外边距 */
}
```



### 子元素选择器

让CSS选择器智能选择子代的元素

```
<p>
	<span>test</span>
	<span><strong>no change</strong></span>
	<span>test</span>
	<strong>will change to red</strong>
</p>

p > strong {
    color: red;
}
```



## 层级选择器



## 分组选择器



## 属性选择器

![img](https://cdn.pbrd.co/images/HMXiV93.png)







## 相邻兄弟选择器



## 伪类选择器

a标签



## 伪元素选择器