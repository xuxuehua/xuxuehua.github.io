---
title: "locate_parameters 元素定位"
date: 2018-07-19 18:17
---

[TOC]

# 元素定位

## selenium定位方法

Selenium提供了8种定位方式。

- id
- name
- class name
- tag name
- link text
- partial link text
- xpath
- css selector

这8种定位方式在Python selenium中所对应的方法为：

- find_element_by_id()
- find_element_by_name()
- find_element_by_class_name()
- find_element_by_tag_name()
- find_element_by_link_text()
- find_element_by_partial_link_text()
- find_element_by_xpath()
- find_element_by_css_selector()



### 定位方法的用法

假如我们有一个Web页面，通过前端工具（如，Firebug）查看到一个元素的属性是这样的。

```
<html>
  <head>
  <body link="#0000cc">
    <a id="result_logo" href="/" onmousedown="return c({'fm':'tab','tab':'logo'})">
    <form id="form" class="fm" name="f" action="/s">
      <span class="soutu-btn"></span>
        <input id="kw" class="s_ipt" name="wd" value="" maxlength="255" autocomplete="off">
```

我们的目的是要定位input标签的输入框。

#### 通过id定位:

  ```
  dr.find_element_by_id("kw")
  ```

#### 通过name定位:

```
dr.find_element_by_name("wd")
```
#### 通过class name定位:

  ```
  dr.find_element_by_class_name("s_ipt")
  ```

#### 通过tag name定位:

  ```
  dr.find_element_by_tag_name("input")
  ```

#### 通过xpath定位

  ```
  dr.find_element_by_xpath("//*[@id='kw']")
  dr.find_element_by_xpath("//*[@name='wd']")
  dr.find_element_by_xpath("//input[@class='s_ipt']")
  dr.find_element_by_xpath("/html/body/form/span/input")
  dr.find_element_by_xpath("//span[@class='soutu-btn']/input")
  dr.find_element_by_xpath("//form[@id='form']/span/input")
  dr.find_element_by_xpath("//input[@id='kw' and @name='wd']")
  ```

#### 通过css定位

  ```
  dr.find_element_by_css_selector("#kw")
  dr.find_element_by_css_selector("[name=wd]")
  dr.find_element_by_css_selector(".s_ipt")
  dr.find_element_by_css_selector("html > body > form > span > input")
  dr.find_element_by_css_selector("span.soutu-btn> input#kw")
  dr.find_element_by_css_selector("form#form > span > input")
  ```

接下来，我们的页面上有一组文本链接。

```
<a class="mnav" href="http://news.baidu.com" name="tj_trnews">新闻</a>
<a class="mnav" href="http://www.hao123.com" name="tj_trhao123">hao123</a>
```

#### 通过link text定位:

  ```
  dr.find_element_by_link_text("新闻")
  dr.find_element_by_link_text("hao123")
  dr.find_element_by_partial_link_text("新")
  dr.find_element_by_partial_link_text("hao")
  dr.find_element_by_partial_link_text("123")
  ```

关于xpaht和css的定位比较复杂，请参考： [xpath语法](http://www.w3school.com.cn/xpath/xpath_syntax.asp)、 [css选择器](http://www.w3school.com.cn/cssref/css_selectors.asp)



#### 定位一组元素

发布时间 2017年6月21日 

WebDriver还提供了8种用于定位一组元素的方法。

```
find_elements_by_id()
find_elements_by_name()
find_elements_by_class_name()
find_elements_by_tag_name()
find_elements_by_link_text()
find_elements_by_partial_link_text()
find_elements_by_xpath()
find_elements_by_css_selector()
```

定位一组元素的方法与定位单个元素的方法类似，唯一的区别是在单词element后面多了一个s表示复数。

接下来通过例子演示定位一组元素的使用：

```
from selenium import webdriver
from time import sleep

driver = webdriver.Chrome()
driver.get("https://www.baidu.com")

driver.find_element_by_id("kw").send_keys("selenium")
driver.find_element_by_id("su").click()
sleep(1)

# 定位一组元素
texts = driver.find_elements_by_xpath('//div/h3/a')

# 循环遍历出每一条搜索结果的标题
for t in texts:
    print(t.text)

driver.quit()
```

程序运行结果：

```
Selenium - Web Browser Automation
官网
功能自动化测试工具——Selenium篇
selenium + python自动化测试环境搭建 - 虫师 - 博客园
selenium是什么?_百度知道
怎样开始用selenium进行自动化测试(个人总结)_百度经验
Selenium_百度百科
selenium_百度翻译
Selenium官网教程_selenium自动化测试实践_Selenium_领测软件测试网
Selenium(浏览器自动化测试框架)_百度百科
自动化基础普及之selenium是啥? - 虫师 - 博客园
python十大主流开源框架 「菜鸟必看」
```



