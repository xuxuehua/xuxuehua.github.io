---
title: "timing"
date: 2018-07-27 23:20
---

[TOC]



# 计时器



## setTimeout

### 语法

```
var t=setTimeout("javascript语句",毫秒)
```



```
<html>
<head>
<script type="text/javascript">
function timedMsg()
{
var t=setTimeout("alert('5 秒！')",5000)
}
</script>
</head>

<body>
<form>
<input type="button" value="显示定时的警告框" onClick = "timedMsg()">
</form>
<p>请点击上面的按钮。警告框会在 5 秒后显示。</p>
</body>

</html>
```



### 无限循环

```
<html>
<head>
<script type="text/javascript">
var c=0
var t
function timedCount()
{
document.getElementById('txt').value=c
c=c+1
t=setTimeout("timedCount()",1000)
}
</script>
</head>

<body>

<form>
<input type="button" value="开始计时！" onClick="timedCount()">
<input type="text" id="txt">
</form>

<p>请点击上面的按钮。输入框会从 0 开始一直进行计时。</p>

</body>

</html>
```



## clearTimeout()

### 语法

```
clearTimeout(setTimeout_variable)
```



```
<html>

<head>
<script type="text/javascript">
var c=0
var t

function timedCount()
 {
 document.getElementById('txt').value=c
 c=c+1
 t=setTimeout("timedCount()",1000)
 }

function stopCount()
 {
 clearTimeout(t)
 }
</script>
</head>

<body>
<form>
<input type="button" value="Start count!" onClick="timedCount()">
<input type="text" id="txt">
<input type="button" value="Stop count!" onClick="stopCount()">
</form>
</body>

</html>
```

