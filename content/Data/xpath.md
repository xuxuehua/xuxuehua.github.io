


[TOC]


# xpath

XML Path Language 是在XML和HTML文档中查找信息的语言，可以用来和HTML文档中对元素和属性进行遍历



## 插件

Chrome -> XPath Helper

Firefox -> XPath Checker



## 选取节点

常用的路径表达式：

 

| 表达式   | 描述                                 | 实例              |                           |
| -------- | ------------------------------------ | ----------------- | ------------------------- |
| nodename | 选取nodename节点的所有子节点         | xpath('//div')    | 选取了div节点的所有子节点 |
| /        | 从根节点选取                         | xpath('/div')     | 从根节点上选取div节点     |
| //       | 选取所有的当前节点，不考虑他们的位置 | xpath('//div')    | 选取所有的div节点         |
| .        | 选取当前节点                         | xpath('./div')    | 选取当前节点下的div节点   |
| ..       | 选取当前节点的父节点                 | xpath('..')       | 回到上一个节点            |
| @        | 选取属性                             | xpath（'//@calss' | 选取所有的class属性       |



## 谓语

谓语被嵌在方括号内，用来查找某个特定的节点或包含某个制定的值的节点

实例：

 

| 表达式                                                       | 结果                                 |
| ------------------------------------------------------------ | ------------------------------------ |
| xpath('/body/div[1]')                                        | 选取body下的第一个div节点            |
| xpath('/body/div[last()]')                                   | 选取body下最后一个div节点            |
| xpath('/body/div[last()-1]')                                 | 选取body下倒数第二个div节点          |
| xpath('/body/div[positon()<3]')                              | 选取body下前两个div节点              |
| xpath('/body/div[[@class](https://my.oschina.net/liwenlong7758)]') | 选取body下带有class属性的div节点     |
| xpath('/body/div[@class="main"]')                            | 选取body下class属性为main的div节点   |
| xpath('/body/div[price>35.00]')                              | 选取body下price元素值大于35的div节点 |





## 运算符

下面列出了可用在 XPath 表达式中的运算符：

| 运算符 | 描述           | 实例                      | 返回值                                                       |
| ------ | -------------- | ------------------------- | ------------------------------------------------------------ |
| \|     | 计算两个节点集 | //book \| //cd            | 返回所有拥有 book 和 cd 元素的节点集                         |
| +      | 加法           | 6 + 4                     | 10                                                           |
| –      | 减法           | 6 – 4                     | 2                                                            |
| *      | 乘法           | 6 * 4                     | 24                                                           |
| div    | 除法           | 8 div 4                   | 2                                                            |
| =      | 等于           | price=9.80                | 如果 price 是 9.80，则返回 true。如果 price 是 9.90，则返回 false。 |
| !=     | 不等于         | price!=9.80               | 如果 price 是 9.90，则返回 true。如果 price 是 9.80，则返回 false。 |
| <      | 小于           | price<9.80                | 如果 price 是 9.00，则返回 true。如果 price 是 9.90，则返回 false。 |
| <=     | 小于或等于     | price<=9.80               | 如果 price 是 9.00，则返回 true。如果 price 是 9.90，则返回 false。 |
| >      | 大于           | price>9.80                | 如果 price 是 9.90，则返回 true。如果 price 是 9.80，则返回 false。 |
| >=     | 大于或等于     | price>=9.80               | 如果 price 是 9.90，则返回 true。如果 price 是 9.70，则返回 false。 |
| or     | 或             | price=9.80 or price=9.70  | 如果 price 是 9.80，则返回 true。如果 price 是 9.50，则返回 false。 |
| and    | 与             | price>9.00 and price<9.90 | 如果 price 是 9.80，则返回 true。如果 price 是 8.50，则返回 false。 |
| mod    | 计算除法的余数 | 5 mod 2                   | 1                                                            |





## 通配符

Xpath通过通配符来选取未知的XML元素



| 表达式                                               | 结果                    |
| ---------------------------------------------------- | ----------------------- |
| xpath（'/div/*'）                                    | 选取div下的所有子节点   |
| xpath('/div[[@*](https://my.oschina.net/u/138045)]') | 选取所有带属性的div节点 |



## 取多个路径

使用“|”运算符可以选取多个路径

 

| 表达式                  | 结果                     |
| ----------------------- | ------------------------ |
| xpath('//div\|//table') | 选取所有的div和table节点 |

 



## Xpath轴

轴可以定义相对于当前节点的节点集

| 轴名称           | 表达式                          | 描述                                         |
| ---------------- | ------------------------------- | -------------------------------------------- |
| ancestor         | xpath('./ancestor::*')          | 选取当前节点的所有先辈节点（父、祖父）       |
| ancestor-or-self | xpath('./ancestor-or-self::*')  | 选取当前节点的所有先辈节点以及节点本身       |
| attribute        | xpath('./attribute::*')         | 选取当前节点的所有属性                       |
| child            | xpath('./child::*')             | 返回当前节点的所有子节点                     |
| descendant       | xpath('./descendant::*')        | 返回当前节点的所有后代节点（子节点、孙节点） |
| following        | xpath('./following::*')         | 选取文档中当前节点结束标签后的所有节点       |
| following-sibing | xpath('./following-sibling::*') | 选取当前节点之后的兄弟节点                   |
| parent           | xpath('./parent::*')            | 选取当前节点的父节点                         |
| preceding        | xpath('./preceding::*')         | 选取文档中当前节点开始标签前的所有节点       |

 

| preceding-sibling | xpath('./preceding-sibling::*') | 选取当前节点之前的兄弟节点 |
| ----------------- | ------------------------------- | -------------------------- |
| self              | xpath('./self::*')              | 选取当前节点               |

 





## 功能函数    

使用功能函数能够更好的进行模糊搜索

 

| 函数        | 用法                                                         | 解释                        |
| ----------- | ------------------------------------------------------------ | --------------------------- |
| starts-with | xpath('//div[starts-with([@id](https://my.oschina.net/u/3451001),"ma")]') | 选取id值以ma开头的div节点   |
| contains    | xpath('//div[contains(@id,"ma")]')                           | 选取id值包含ma的div节点     |
| and         | xpath('//div[contains(@id,"ma") and contains(@id,"in")]')    | 选取id值包含ma和in的div节点 |
| text()      | xpath('//div[contains(text(),"ma")]')                        | 选取节点文本包含ma的div节点 |
|             |                                                              |                             |

