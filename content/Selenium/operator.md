---
title: "operator 操作"
date: 2018-07-19 18:21
---

[TOC]



# Selenium 操作


## 浏览器操作

### 控制浏览器窗口大小

有时候我们希望能以某种浏览器尺寸打开，让访问的页面在这种尺寸下运行。例如可以将浏览器设置成移动端大小(480* 800)，然后访问移动站点，对其样式进行评估；WebDriver提供了set_window_size()方法来设置浏览器的大小。

```
from selenium import webdriver

driver = webdriver.Firefox()
driver.get("http://m.baidu.com")

# 参数数字为像素点
print("设置浏览器宽480、高800显示")
driver.set_window_size(480, 800)
driver.quit()
```

在PC端执行自动化测试脚本大多的情况下是希望浏览器在全屏幕模式下执行，那么可以使用maximize_window()方法使打开的浏览器全屏显示，其用法与set_window_size() 相同，但它不需要参数。

### 控制浏览器后退、前进

在使用浏览器浏览网页时，浏览器提供了后退和前进按钮，可以方便地在浏览过的网页之间切换，WebDriver也提供了对应的back()和forward()方法来模拟后退和前进按钮。下面通过例子来演示这两个方法的使用。

```
from selenium import webdriver

driver = webdriver.Firefox()

#访问百度首页
first_url= 'http://www.baidu.com'
print("now access %s" %(first_url))
driver.get(first_url)

#访问新闻页面
second_url='http://news.baidu.com'
print("now access %s" %(second_url))
driver.get(second_url)

#返回（后退）到百度首页
print("back to  %s "%(first_url))
driver.back()

#前进到新闻页
print("forward to  %s"%(second_url))
driver.forward()

driver.quit()
```

为了看清脚本的执行过程，下面每操作一步都通过print()来打印当前的URL地址。

### 刷新页面

有时候需要手动刷新（F5） 页面。

```
……
driver.refresh() #刷新当前页面
……
```



### 关闭浏览器

发布时间 2017年6月12日 

在前面的例子中我们一直使用quit()方法，其含义为退出相关的驱动程序和关闭所有窗口。除此之外，WebDriver还提供了close()方法，用来关闭当前窗口。例多窗口的处理，在用例执行的过程中打开了多个窗口，我们想要关闭其中的某个窗口，这时就要用到close()方法进行关闭了。

- close() 关闭单个窗口
- quit() 关闭所有窗口
- 

## WebDriver 操作

### 点击和输入

前面我们已经学习了定位元素， 定位只是第一步， 定位之后需要对这个元素进行操作， 或单击（按钮） 或输入（输入框） ， 下面就来认识 WebDriver 中最常用的几个方法：

- clear()： 清除文本。
- send_keys (value)： 模拟按键输入。
- click()： 单击元素。

```
from selenium import webdriver

driver = webdriver.Chrome()
driver.get("https://www.baidu.com")

driver.find_element_by_id("kw").clear()
driver.find_element_by_id("kw").send_keys("selenium")
driver.find_element_by_id("su").click()

driver.quit()
```

### 提交

- submit()

submit()方法用于提交表单。 例如， 在搜索框输入关键字之后的“回车” 操作， 就可以通过该方法模拟。

```
from selenium import webdriver

driver = webdriver.Chrome()
driver.get("https://www.baidu.com")

search_text = driver.find_element_by_id('kw')
search_text.send_keys('selenium')
search_text.submit()

driver.quit()
```

有时候 submit()可以与 click()方法互换来使用， submit()同样可以提交一个按钮， 但 submit()的应用范围远不及 click()广泛。

### 其他常用方法

- size： 返回元素的尺寸。
- text： 获取元素的文本。
- get_attribute(name)： 获得属性值。
- is_displayed()： 设置该元素是否用户可见。

```
from selenium import webdriver

driver = webdriver.Chrome()
driver.get("http://www.baidu.com")

# 获得输入框的尺寸
size = driver.find_element_by_id('kw').size
print(size)

# 返回百度页面底部备案信息
text = driver.find_element_by_id("cp").text
print(text)

# 返回元素的属性值， 可以是 id、 name、 type 或其他任意属性
attribute = driver.find_element_by_id("kw").get_attribute('type')
print(attribute)

# 返回元素的结果是否可见， 返回结果为 True 或 False
result = driver.find_element_by_id("kw").is_displayed()
print(result)

driver.quit()
```

输出结果：

```
{'width': 500, 'height': 22}
©2015 Baidu 使用百度前必读 意见反馈 京 ICP 证 030173 号
text
True
```

执行上面的程序并查看结果： size 方法用于获取百度输入框的宽、 高， text 方法用于获得百度底部的备案信息， get_attribute()用于获得百度输入的 type 属性的值， is_displayed()用于返回一个元素是否可见， 如果可见则返回 True， 否则返回 False。





## 鼠标事件

在 WebDriver 中， 将这些关于鼠标操作的方法封装在 ActionChains 类提供。

ActionChains 类提供了鼠标操作的常用方法：

- perform()： 执行所有 ActionChains 中存储的行为；
- context_click()： 右击；
- double_click()： 双击；
- drag_and_drop()： 拖动；
- move_to_element()： 鼠标悬停。

### 鼠标悬停操作

![img](http://orru5lls3.bkt.clouddn.com/xuanting.jpg)

```
from selenium import webdriver
# 引入 ActionChains 类
from selenium.webdriver.common.action_chains import ActionChains

driver = webdriver.Chrome()
driver.get("https://www.baidu.cn")

# 定位到要悬停的元素
above = driver.find_element_by_link_text("设置")
# 对定位到的元素执行鼠标悬停操作
ActionChains(driver).move_to_element(above).perform()

……
```

- from selenium.webdriver import ActionChains

导入提供鼠标操作的 ActionChains 类。

- ActionChains(driver)

调用 ActionChains()类， 将浏览器驱动 driver 作为参数传入。

- move_to_element(above)

context_click()方法用于模拟鼠标右键操作， 在调用时需要指定元素定位。

- perform()

执行所有 ActionChains 中存储的行为， 可以理解成是对整个操作的提交动作。





## 键盘事件

Keys()类提供了键盘上几乎所有按键的方法。 前面了解到， send_keys()方法可以用来模拟键盘输入， 除此 之外， 我们还可以用它来输入键盘上的按键， 甚至是组合键， 如 Ctrl+A、 Ctrl+C 等。

```
from selenium import webdriver
# 引入 Keys 模块
from selenium.webdriver.common.keys import Keys

driver = webdriver.Chrome()
driver.get("http://www.baidu.com")

# 输入框输入内容
driver.find_element_by_id("kw").send_keys("seleniumm")

# 删除多输入的一个 m
driver.find_element_by_id("kw").send_keys(Keys.BACK_SPACE)


# 输入空格键+“教程”
driver.find_element_by_id("kw").send_keys(Keys.SPACE)
driver.find_element_by_id("kw").send_keys("教程")

# ctrl+a 全选输入框内容
driver.find_element_by_id("kw").send_keys(Keys.CONTROL, 'a')

# ctrl+x 剪切输入框内容
driver.find_element_by_id("kw").send_keys(Keys.CONTROL, 'x')

# ctrl+v 粘贴内容到输入框
driver.find_element_by_id("kw").send_keys(Keys.CONTROL, 'v')

# 通过回车键来代替单击操作
driver.find_element_by_id("su").send_keys(Keys.ENTER)
driver.quit()
```

需要说明的是， 上面的脚本没有什么实际意义， 仅向我们展示模拟键盘各种按键与组合键的用法。

- from selenium.webdriver.common.keys import Keys

在使用键盘按键方法前需要先导入 keys 类。

以下为常用的键盘操作：

- send_keys(Keys.BACK_SPACE) 删除键（BackSpace）
- send_keys(Keys.SPACE) 空格键(Space)
- send_keys(Keys.TAB) 制表键(Tab)
- send_keys(Keys.ESCAPE) 回退键（Esc）
- send_keys(Keys.ENTER) 回车键（Enter）
- send_keys(Keys.CONTROL,‘a’) 全选（Ctrl+A）
- send_keys(Keys.CONTROL,‘c’) 复制（Ctrl+C）
- send_keys(Keys.CONTROL,‘x’) 剪切（Ctrl+X）
- send_keys(Keys.CONTROL,‘v’) 粘贴（Ctrl+V）
- send_keys(Keys.F1) 键盘 F1
- ……
- send_keys(Keys.F12) 键盘 F12



## 其他操作



### 获取断言信息

不管是在做功能测试还是自动化测试，最后一步需要拿实际结果与预期进行比较。这个比较的称之为**断言**。

我们通常可以通过获取title 、URL和text等信息进行断言。text方法在前面已经讲过，它用于获取标签对之间的文本信息。 下面同样以百度为例，介绍如何获取这些信息。

```
from selenium import webdriver
from time import sleep


driver = webdriver.Firefox()
driver.get("https://www.baidu.com")

print('Before search================')

# 打印当前页面title
title = driver.title
print(title)

# 打印当前页面URL
now_url = driver.current_url
print(now_url)

driver.find_element_by_id("kw").send_keys("selenium")
driver.find_element_by_id("su").click()
sleep(1)

print('After search================')

# 再次打印当前页面title
title = driver.title
print(title)

# 打印当前页面URL
now_url = driver.current_url
print(now_url)

# 获取结果数目
user = driver.find_element_by_class_name('nums').text
print(user)

driver.quit()
```

脚本运行结果如下：

```
Before search================
百度一下，你就知道
https://www.baidu.com/
After search================
selenium_百度搜索
https://www.baidu.com/s?ie=utf-8&f=8&rsv_bp=0&rsv_idx...
搜索工具
百度为您找到相关结果约5,380,000个
```

- title：用于获得当前页面的标题。
- current_url：用户获得当前页面的URL。
- text：获取搜索条目的文本信息。


### 多表单切换
发布时间 2017年6月20日 

在Web应用中经常会遇到frame/iframe表单嵌套页面的应用，WebDriver只能在一个页面上对元素识别与定位，对于frame/iframe表单内嵌页面上的元素无法直接定位。这时就需要通过switch_to.frame()方法将当前定位的主体切换为frame/iframe表单的内嵌页面中。

```
<html>
  <body>
    ...
    <iframe id="x-URS-iframe" ...>
      <html>
         <body>
           ...
           <input name="email" >
```

126邮箱登录框的结构大概是这样子的，想要操作登录框必须要先切换到iframe表单。

```
from selenium import webdriver

driver = webdriver.Chrome()
driver.get("http://www.126.com")

driver.switch_to.frame('x-URS-iframe')
driver.find_element_by_name("email").clear()
driver.find_element_by_name("email").send_keys("username")
driver.find_element_by_name("password").clear()
driver.find_element_by_name("password").send_keys("password")
driver.find_element_by_id("dologin").click()
driver.switch_to.default_content()

driver.quit()
```

switch_to.frame() 默认可以直接取表单的id 或name属性。如果iframe没有可用的id和name属性，则可以通过下面的方式进行定位。

```
……
#先通过xpth定位到iframe
xf = driver.find_element_by_xpath('//*[@id="x-URS-iframe"]')

#再将定位对象传给switch_to.frame()方法
driver.switch_to.frame(xf)
……
driver.switch_to.parent_frame()
```

除此之外，在进入多级表单的情况下，还可以通过switch_to.default_content()跳回最外层的页面。



### 多窗口切换

发布时间 2017年6月19日 

在页面操作过程中有时候点击某个链接会弹出新的窗口，这时就需要主机切换到新打开的窗口上进行操作。WebDriver提供了switch_to.window()方法，可以实现在不同的窗口之间切换。 以百度首页和百度注册页为例，在两个窗口之间的切换如下图。![img](http://orru5lls3.bkt.clouddn.com/more_windows_n.png)

```
from selenium import webdriver
import time

driver = webdriver.Firefox()
driver.implicitly_wait(10)
driver.get("http://www.baidu.com")

# 获得百度搜索窗口句柄
sreach_windows = driver.current_window_handle

driver.find_element_by_link_text('登录').click()
driver.find_element_by_link_text("立即注册").click()

# 获得当前所有打开的窗口的句柄
all_handles = driver.window_handles

# 进入注册窗口
for handle in all_handles:
    if handle != sreach_windows:
        driver.switch_to.window(handle)
        print('now register window!')
        driver.find_element_by_name("account").send_keys('username')
        driver.find_element_by_name('password').send_keys('password')
        time.sleep(2)
        # ……


driver.quit()
```

在本例中所涉及的新方法如下：

- current_window_handle：获得当前窗口句柄。
- window_handles：返回所有窗口的句柄到当前会话。
- switch_to.window()：用于切换到相应的窗口，与上一节的switch_to.frame()类似，前者用于不同窗口的切换，后者用于不同表单之间的切换。



### 警告框处理

发布时间 2017年6月18日 [虫师](http://www.cnblogs.com/fnng/)

在WebDriver中处理JavaScript所生成的alert、confirm以及prompt十分简单，具体做法是使用 switch_to.alert 方法定位到 alert/confirm/prompt，然后使用text/accept/dismiss/ send_keys等方法进行操作。

- text：返回 alert/confirm/prompt 中的文字信息。
- accept()：接受现有警告框。
- dismiss()：解散现有警告框。
- send_keys(keysToSend)：发送文本至警告框。keysToSend：将文本发送至警告框。

如下图，百度搜索设置弹出的窗口是不能通过前端工具对其进行定位的，这个时候就可以通过switch_to_alert()方法接受这个弹窗。![img](http://orru5lls3.bkt.clouddn.com/alert_windows.png)

```
from selenium import webdriver
from selenium.webdriver.common.action_chains import ActionChains
import time

driver = webdriver.Firefox()
driver.implicitly_wait(10)
driver.get('http://www.baidu.com')

# 鼠标悬停至“设置”链接
link = driver.find_element_by_link_text('设置')
ActionChains(driver).move_to_element(link).perform()

# 打开搜索设置
driver.find_element_by_link_text("搜索设置").click()

# 保存设置
driver.find_element_by_class_name("prefpanelgo").click()
time.sleep(2)

# 接受警告框
driver.switch_to.alert.accept()

driver.quit()
```

通过switch_to_alert()方法获取当前页面上的警告框，并使用accept()方法接受警告框。



### 下拉框选择

发布时间 2017年6月17日 

有时我们会碰到下拉框，WebDriver提供了Select类来处理下拉框。 如百度搜索设置的下拉框，如下图：![img](http://orru5lls3.bkt.clouddn.com/select.png)

```
from selenium import webdriver
from selenium.webdriver.support.select import Select
from time import sleep

driver = webdriver.Chrome()
driver.implicitly_wait(10)
driver.get('http://www.baidu.com')

# 鼠标悬停至“设置”链接
driver.find_element_by_link_text('设置').click()
sleep(1)
# 打开搜索设置
driver.find_element_by_link_text("搜索设置").click()
sleep(2)

# 搜索结果显示条数
sel = driver.find_element_by_xpath("//select[@id='nr']")
Select(sel).select_by_value('50')  # 显示50条
# ……

driver.quit()
```

Select类用于定位select标签。 select_by_value() 方法用于定位下接选项中的value值。



### 文件上传

发布时间 2017年6月16日 

对于通过input标签实现的上传功能，可以将其看作是一个输入框，即通过send_keys()指定本地文件路径的方式实现文件上传。

创建upfile.html文件，代码如下：

```
<html>
<head>
<meta http-equiv="content-type" content="text/html;charset=utf-8" />
<title>upload_file</title>
<link href="http://cdn.bootcss.com/bootstrap/3.3.0/css/bootstrap.min.css" rel="stylesheet" />
</head>
<body>
  <div class="row-fluid">
	<div class="span6 well">
	<h3>upload_file</h3>
	  <input type="file" name="file" />
	</div>
  </div>
</body>
<script src="http://cdn.bootcss.com/bootstrap/3.3.0/css/bootstrap.min.js"></scrip>
</html>
```

通过浏览器打开upfile.html文件，功能如下图。![img](http://orru5lls3.bkt.clouddn.com/upfile.png)

接下来通过send_keys()方法来实现文件上传。

```
from selenium import webdriver
import os

driver = webdriver.Firefox()
file_path = 'file:///' + os.path.abspath('upfile.html')
driver.get(file_path)

# 定位上传按钮，添加本地文件
driver.find_element_by_name("file").send_keys('D:\\upload_file.txt')

driver.quit()
```



### cookie操作

发布时间 2017年6月15日 

有时候我们需要验证浏览器中cookie是否正确，因为基于真实cookie的测试是无法通过白盒和集成测试进行的。WebDriver提供了操作Cookie的相关方法，可以读取、添加和删除cookie信息。

WebDriver操作cookie的方法：

- get_cookies()： 获得所有cookie信息。
- get_cookie(name)： 返回字典的key为“name”的cookie信息。
- add_cookie(cookie_dict) ： 添加cookie。“cookie_dict”指字典对象，必须有name 和value 值。
- delete_cookie(name,optionsString)：删除cookie信息。“name”是要删除的cookie的名称，“optionsString”是该cookie的选项，目前支持的选项包括“路径”，“域”。
- delete_all_cookies()： 删除所有cookie信息。

下面通过get_cookies()来获取当前浏览器的cookie信息。

```
from selenium import webdriver

driver = webdriver.Firefox()
driver.get("http://www.youdao.com")

# 获得cookie信息
cookie= driver.get_cookies()
# 将获得cookie的信息打印
print(cookie)

driver.quit()
```

从执行结果可以看出，cookie数据是以字典的形式进行存放的。知道了cookie的存放形式，接下来我们就可以按照这种形式向浏览器中写入cookie信息。

```
from selenium import webdriver

driver = webdriver.Firefox()
driver.get("http://www.youdao.com")

# 向cookie的name 和value中添加会话信息
driver.add_cookie({'name': 'key-aaaaaaa', 'value': 'value-bbbbbb'})

# 遍历cookies中的name 和value信息并打印，当然还有上面添加的信息
for cookie in driver.get_cookies():
    print("%s -> %s" % (cookie['name'], cookie['value']))

driver.quit()


输出结果：
======================== RESTART: =========================
YOUDAO_MOBILE_ACCESS_TYPE -> 1
_PREF_ANONYUSER__MYTH -> aGFzbG9nZ2VkPXRydWU=
OUTFOX_SEARCH_USER_ID -> -1046383847@218.17.158.115
JSESSIONID -> abc7qSE_SBGsVgnVLBvcu
key-aaaaaaa -> value-bbbbbb
```

从执行结果可以看到，最后一条cookie信息是在脚本执行过程中通过add_cookie()方法添加的。通过遍历得到所有的cookie信息，从而找到key为“name”和“value”的特定cookie的value。



### 调用JavaScript代码

发布时间 2017年6月14日 

虽然WebDriver提供了操作浏览器的前进和后退方法，但对于浏览器滚动条并没有提供相应的操作方法。在这种情况下，就可以借助JavaScript来控制浏览器的滚动条。WebDriver提供了execute_script()方法来执行JavaScript代码。

用于调整浏览器滚动条位置的JavaScript代码如下：

```
<!-- window.scrollTo(左边距,上边距); -->
window.scrollTo(0,450);
```

window.scrollTo()方法用于设置浏览器窗口滚动条的水平和垂直位置。方法的第一个参数表示水平的左间距，第二个参数表示垂直的上边距。其代码如下：

```
from selenium import webdriver
from time import sleep

# 访问百度
driver=webdriver.Firefox()
driver.get("http://www.baidu.com")

# 设置浏览器窗口大小
driver.set_window_size(500, 500)

# 搜索
driver.find_element_by_id("kw").send_keys("selenium")
driver.find_element_by_id("su").click()
sleep(2)

# 通过javascript设置浏览器窗口的滚动条位置
js="window.scrollTo(100,450);"
driver.execute_script(js)
sleep(3)

driver.quit()
```

通过浏览器打开百度进行搜索，并且提前通过set_window_size()方法将浏览器窗口设置为固定宽高显示，目的是让窗口出现水平和垂直滚动条。然后通过execute_script()方法执行JavaScripts代码来移动滚动条的位置。



## 截图

### 窗口截图

发布时间 2017年6月13日 

自动化用例是由程序去执行的，因此有时候打印的错误信息并不十分明确。如果在脚本执行出错的时候能对当前窗口截图保存，那么通过图片就可以非常直观地看出出错的原因。WebDriver提供了截图函数get_screenshot_as_file()来截取当前窗口。

```
from selenium import webdriver
from time import sleep

driver = webdriver.Firefox()
driver.get('http://www.baidu.com')

driver.find_element_by_id('kw').send_keys('selenium')
driver.find_element_by_id('su').click()
sleep(2)

# 截取当前窗口，并指定截图图片的保存位置
driver.get_screenshot_as_file("D:\\baidu_img.jpg")

driver.quit()
```

脚本运行完成后打开D盘，就可以找到baidu_img.jpg图片文件了。



### 元素截图

`screenshot_as_png`

```
code = self.driver.find_element_by_xpath("//img[@alt='CAPTCHA']")
        img = code.screenshot_as_png
        img_name = "./code/code{}.png".format(time.strftime('%Y-%m-%d_%H%M%S', time.localtime(time.time())))
        with open(img_name, 'wb') as f:
            f.write(img)
        rec_code = self.code_recog(img_name)
```


