---
title: "beautifulsoup"
date: 2018-07-29 01:35
---

[TOC]



# bs4 模块



## 安装 beautifulsoup

```
pip install bs4
```



## find_all

```
In [5]: import requests

In [6]: from bs4 import BeautifulSoup

In [7]: url = 'http://www.itest.info/courses'
In [8]: soup = BeautifulSoup(requests.get(url).text, 'html.parser')

In [9]: for course in soup.find_all('h4'):
   ...:     print(course.text)
   ...:
Android测试开发（Java语言）
性能测试从入门到精通班
接口自动化测试开发--Python班
Selenium自动化测试--Java班
Selenium自动化测试--Python班
```



```
<span class="item_hot_topic_title">
  <a href="/t/415664">冬天了，身上静电咋处理？</a>
</span>
```

```
for span in soup.find_all('span', class_='item_hot_topic_title'):
    print(span.find('a').text, span.find('a')['href'])
```

> `for span in soup.find_all('span', class_='item_hot_topic_title')`: 遍历所有的class=item_hot_topic_title的span。注意是`class_`，不是`class`，因为class是python的关键字，所以后面要加个尾巴，防止冲突



