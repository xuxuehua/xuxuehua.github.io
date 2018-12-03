---
title: "layout 布局"
date: 2018-11-20 18:06
---


[TOC]


# layout



## 盒模型

即把HTML页面中的元素看作是一个矩形的盒子容器，没有矩形都是有元素的内容（content），内边距（padding），边框（border）和外边距（margin） 组成

![img](https://cdn.pbrd.co/images/HO0Dwzx.png)



- 网站一般会将内边距盒外边距设置为0

```
body,button,code,dd,details,dl,dt,fieldset,figcaption,figure,footer,form,h1,h2,h3,h4,h5,h6,header,hgroup,hr,input,legend,li,menu,nav,ol,p,pre,section,td,textarea,th,ul{margin:0;padding:0}
```



- 行内元素不要给上下的margin和padding，默认是不起作用的



### border样式

- 推荐方式

```
border: 20px solid purple;
```



- border-style

```
none，没有边框，即忽略所有边框的宽度
solid，边框为单实线
dashed，边框为虚线
dotted，边框为点线
double，边框为双实线
```



- border-color

```
border-color: red; 
border-color: yellow black green red;
```

> 多个参数顺序，为顺时针，上右下左



### Padding 样式

```
padding: 10px 20px 30px 40px
padding: 0;
```

> 多个参数顺序，为顺时针，上右下左 



### margin 样式

```
margin: 0 auto;
```



- 使用margin定义块元素的垂直外边距时，可能会出现外边距合并的现象





## 流式布局

### 标准流

把浏览器当成一个盒子容器，容器中排放盒子的时候，从上往下，从左向右排放

若放不下盒子，换行存放



### 浮动流

浮动的盒子可以向左或向右移动 



#### 浮动定义

```
div {
    float: right;
}
```





### overflow 属性

* 父容器高度塌陷

如果一个标准流中的盒子中所有的子元素都进行了浮动，而且盒子没有设置高度，那么父容器整个高度会塌陷，使用hidden 解决

```
.parent {
    overflow: hidden;
}
```



| 属性值  | 描述                                           |
| ------- | ---------------------------------------------- |
| visible | 内容不会被修剪，会呈现在元素框之外（默认操作） |
| hidden  | 溢出内容会被修剪，并且被修剪的内容是不可见的   |
| auto    | 在需要时产生滚动条，即自适应所要显示的内容     |
| scroll  | 溢出内容会被修剪，并且浏览器会始终显示滚动条   |



### 清除浮动

```
clear:left/right/both/b
```



#### 常用布局案例

![img](https://cdn.pbrd.co/images/HPHVFKP.png)



```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        body, div, p {
            padding: 0;
            margin: 0;
        }

        div {
            border: 1px solid lawngreen;
        }

        .top-nav {
            height: 100px;
            width: 960px;
            margin: 0 auto;
        }

        .leftbar {
            float: left;
            width: 200px;
            height: 300px;
        }

        .content {
            float: left;
            width: 756px;
            height: 500px;
        }

        .main {
            width: 960px;
            margin: 0 auto;
            overflow: hidden;
        }

        .footer {
            margin: 0 auto;
            width: 960px;
        }


    </style>
</head>
<body>
    <div class="top-nav">
        top area
    </div>

    <div class="main">
    <div class="leftbar">
        left area
    </div>
    <div class="content">
        main area
    </div>
    </div>

    <div class="footer">
        footer area
    </div>
</body>
</html>
```



![img](https://cdn.pbrd.co/images/HPHYkrm.png)

```
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<meta http-equiv="X-UA-Compatible" content="ie=edge">
	<title>Document</title>
	<style>
		body, div {
			margin: 0;
			padding: 0;
		}

		div {
			border: 1px solid saddlebrown;
		}

		.head {
			height: 100px;
			background-color: yellow;
		}
		
		.left {
			float: left;
			width: 200px;
			background-color: lightblue;
			height: 400px;
		}

		.right {
			margin-left: 203px;
			height: 400px;
			background-color: red;
		}

		.footer {
			background-color: pink;
		}

	</style>
</head>
<body>
	<div class="head">
		head area
	</div>
	<div class="left">
		left area
	</div>
	<div class="right">
		right area
	</div>
	<div class="footer">
		footer area
	</div>
	<div>

	</div>
	
</body>
</html>
```



![img](https://cdn.pbrd.co/images/HPItfrE.png)

```
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<meta http-equiv="X-UA-Compatible" content="ie=edge">
	<title>Document</title>
	<style>
		body,div {
			padding: 0;
			margin: 0;
		}

		div {
			border: 1px solid saddlebrown;
		}
		
		.head {
			height: 100px;
			background-color: lightgreen;
		}

		.left {
			float: left;
			width: 100px;
			height: 300px;
		}

		.right {
			float: right;
			width: 100px;
			height: 500px
		}

		.main {
			margin: 0 105px;
		}

		.footer {
			clear: both;
		}
	</style>
</head>
<body>
	<div class="head">head area</div>	
	<div class="left">left area</div>	
	<div class="right">right area</div>	
	<div class="main">main area</div>	
	<div class="footer">footer area</div>	
</body>
</html>
```



![img](https://cdn.pbrd.co/images/HPIywhh.png)

```
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<meta http-equiv="X-UA-Compatible" content="ie=edge">
	<title>Document</title>
	<style>
		body,div {
			padding: 0;
			margin: 0;
		}

		div {
			border: 1px solid saddlebrown;
		}

		.head,.footer,.center {
			margin: 0 auto;
			width: 960;
		}

		.left,.right,.main {
			float: left;
		}

		.center {
			overflow: hidden;
		}

		.left , .right{
			width: 100px;
			height: 400px;
		}

		.main {
			width: 960px;
			margin: 0 2px;
		}
	</style>
</head>
<body>
	<div class="head">head area</div>	
	<div class="center">
	<div class="left">left area</div>	
	<div class="main">main area</div>	
	<div class="right">right area</div>	
	</div>
	<div class="footer">footer area</div>	
</body>
</html>
```

