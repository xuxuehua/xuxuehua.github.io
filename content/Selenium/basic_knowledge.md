---
title: "basic_knowledge"
date: 2018-07-19 18:03
---

[TOC]



# Python - Selenium



## 简介

Jason Huggins在2004年发起了Selenium项目，当时身处ThoughtWorks的他，为了不想让自己的时间浪费在无聊的重复性工作中，幸运的是，所有被测试的浏览器都支持Javascript。Jason和他所在的团队采用Javascript编写一种测试工具来验证浏览器页面的行为；这个JavaScript类库就是Selenium core，同时也是seleniumRC、Selenium IDE的核心组件。Selenium由此诞生。

关于Selenium的命名比较有意思，当时QTP mercury是主流的商业自化工具，是化学元素汞（俗称水银），而Selenium是开源自动化工具，是化学元素硒，硒可以对抗汞。



### Selenium IDE

Selenium IDE是嵌入到Firefox浏览器中的一个插件，实现简单的浏览器操作的录制与回放功能。

### Selenium Grid

Selenium Grid是一种自动化的测试辅助工具，Grid通过利用现有的计算机基础设施，能加快Web-App的功能测试。利用Grid可以很方便地实现在多台机器上和异构环境中运行测试用例

### WebDriver
WebDriver是通过原生浏览器支持或者浏览器扩展来直接控制浏览器。WebDriver针对各个浏览器而开发，取代了嵌入到被测Web应用中的JavaScript，与浏览器紧密集成，因此支持创建更高级的测试，避免了JavaScript安全模型导致的限制。除了来自浏览器厂商的支持之外，WebDriver还利用操作系统级的调用，模拟用户输入。







## 安装

`pip install selenium`



### 简单测试

打开一款Python编辑器，默认Python自带的IDLE也行。创建 baidu.py文件，输入以下内容：

```
from selenium import webdriver


driver = webdriver.Chrome()
driver.get('https://www.baidu.com')

print(driver.title)

driver.quit()
```

 

### 浏览器驱动

Firefox浏览器驱动：[geckodriver](https://github.com/mozilla/geckodriver/releases)

Chrome浏览器驱动：[chromedriver](https://sites.google.com/a/chromium.org/chromedriver/home) , [taobao备用地址](https://npm.taobao.org/mirrors/chromedriver)

IE浏览器驱动：[IEDriverServer](http://selenium-release.storage.googleapis.com/index.html)

Edge浏览器驱动：[MicrosoftWebDriver](https://developer.microsoft.com/en-us/microsoft-edge/tools/webdriver)

Opera浏览器驱动：[operadriver](https://github.com/operasoftware/operachromiumdriver/releases)

PhantomJS浏览器驱动：[phantomjs](http://phantomjs.org/)



#### 驱动调用

```
from selenium import webdriver


driver = webdriver.Firefox()   # Firefox浏览器

driver = webdriver.Chrome()    # Chrome浏览器

driver = webdriver.Ie()        # Internet Explorer浏览器

driver = webdriver.Edge()      # Edge浏览器

driver = webdriver.Opera()     # Opera浏览器

driver = webdriver.PhantomJS()   # PhantomJS
```

