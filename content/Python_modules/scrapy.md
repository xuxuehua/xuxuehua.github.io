---
title: "scrapy"
date: 2018-10-02 18:24
---


[TOC]


# scrapy

Scrapy 将一些东西封装好，在上面写爬虫可以变的更加高效



## 架构图

![img](https://cdn.pbrd.co/images/HGzycG9.png)

- **引擎(Scrapy)**
  用来处理整个系统的数据流处理, 触发事务(框架核心)
- **调度器(Scheduler)**
  用来接受引擎发过来的请求, 压入队列中, 并在引擎再次请求的时候返回. 可以想像成一个URL（抓取网页的网址或者说是链接）的优先队列, 由它来决定下一个要抓取的网址是什么, 同时去除重复的网址
- **下载器(Downloader)**
  用于下载网页内容, 并将网页内容返回给蜘蛛(Scrapy下载器是建立在twisted这个高效的异步模型上的)
- **爬虫(Spiders)**
  爬虫是主要干活的, 用于从特定的网页中提取自己需要的信息, 即所谓的实体(Item)。用户也可以从中提取出链接,让Scrapy继续抓取下一个页面
- **项目管道(Pipeline)**
  负责处理爬虫从网页中抽取的实体，主要的功能是持久化实体、验证实体的有效性、清除不需要的信息。当页面被爬虫解析后，将被发送到项目管道，并经过几个特定的次序处理数据。
- **下载器中间件(Downloader Middlewares)**
  位于Scrapy引擎和下载器之间的框架，主要是处理Scrapy引擎与下载器之间的请求及响应。
- **爬虫中间件(Spider Middlewares)**
  介于Scrapy引擎和爬虫之间的框架，主要工作是处理蜘蛛的响应输入和请求输出。



### 运行流程

1. 引擎从调度器中取出一个链接(URL)用于接下来的抓取
2. 引擎把URL封装成一个请求(Request)传给下载器
3. 下载器把资源下载下来，并封装成应答包(Response)
4. 爬虫解析Response
5. 解析出实体（Item）,则交给实体管道进行进一步的处理
6. 解析出的是链接（URL）,则把URL交给调度器等待抓取





## 安装

```
pip install scrapy
```





## 创建项目

```
scrapy startproject PROJECT_NAME
```



会生成如下目录结构

```
my_first_scrapy/
├── my_first_scrapy
│   ├── __init__.py
│   ├── __pycache__
│   ├── items.py
│   ├── middlewares.py
│   ├── pipelines.py
│   ├── settings.py
│   └── spiders
│       ├── __init__.py
│       └── __pycache__
└── scrapy.cfg
```

> scrapy.cfg  项目的主配置信息。（真正爬虫相关的配置信息在settings.py文件中）
> items.py    设置数据存储模板，用于结构化数据，如：Django的Model
> pipelines    数据处理行为，如：一般结构化的数据持久化
> settings.py 配置文件，如：递归的层数、并发数，延迟下载等
> spiders      爬虫目录，如：创建文件，编写爬虫规则





### 前期准备

设置settings.py

关闭robotstxt

```
ROBOTSTXT_OBEY = False
```

默认请求头

```
DEFAULT_REQUEST_HEADERS = {
    'accept': '*/*',
    'accept-encoding': 'gzip, deflate, br',
    'accept-language': 'en-US,en;q=0.9,zh-CN;q=0.8,zh;q=0.7,zh-TW;q=0.6',
    'user-agent': 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_13_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/69.0.3497.100 Safari/537.36'
}
```



### 创建爬虫

```
scrapy gescrapy genspider [-t template] <name> <domain>
   - 创建爬虫应用
   如：
      scrapy gensipider xxh xuxuehua.com
      scrapy gensipider -t xmlfeed autohome autohome.com.cn
   PS:
      查看所有命令：scrapy gensipider -l
      查看模板命令：scrapy gensipider -d 模板名称
```



### 调用爬虫

```
scrapy crawl 爬虫应用名称
   - 运行单独爬虫应用
   如:
   	  scrapy crawl xxh
      scrapy crawl xxh --nolog
```

> 这里运行的应用名称不包含.py 后缀





#### start.py 调用

```
# encoding: utf-8

from scrapy import cmdline

cmdline.execute(['scrapy', 'crawl', 'name'])  # 这里的name指spider目录下的项目名称，不含.py
```





### example

#### qiushibaike.com

qsbk_spider.py

```
# -*- coding: utf-8 -*-
import scrapy
from qsbk.items import QsbkItem


class QsbkSpiderSpider(scrapy.Spider):
    name = 'qsbk_spider'
    allowed_domains = ['qiushibaike.com']
    start_urls = ['https://www.qiushibaike.com/text/page/1/']
    base_domain = "https://www.qiushibaike.com"

    def parse(self, response):
        duanzi_divs = response.xpath("//div[@id='content-left']/div")
        for duanzi_div in duanzi_divs:
            author = duanzi_div.xpath(".//h2/text()").get().strip()
            content = duanzi_div.xpath(".//div[@class='content']//text()").getall()
            content = ''.join(content).strip()
            item = QsbkItem(author=author, content=content)
            yield item
        next_url = response.xpath("//ul[@class='pagination']/li[last()]/a/@href").get()
        if not next_url:
            return
        else:
            yield scrapy.Request(self.base_domain+next_url, callback=self.parse)
```



items.py

```
# -*- coding: utf-8 -*-

# Define here the models for your scraped items
#
# See documentation in:
# https://doc.scrapy.org/en/latest/topics/items.html

import scrapy


class QsbkItem(scrapy.Item):
    author = scrapy.Field()
    content = scrapy.Field()
```



pipelines.py

```
# -*- coding: utf-8 -*-

import json
from scrapy.exporters import JsonLinesItemExporter


class QsbkPipeline(object):

    def __init__(self):
        self.fp = open('duanzi.json', 'wb')
        self.exporter = JsonLinesItemExporter(self.fp, ensure_ascii=False, encoding='utf-8')

    def open_spider(self, spider):
        print('Start crawling...')

    def process_item(self, item, spider):
        self.exporter.export_item(item)
        return item

    def close_spider(self, spider):
        self.fp.close()
        print('End crawling...')
```



settings.py

```
# -*- coding: utf-8 -*-



BOT_NAME = 'qsbk'

SPIDER_MODULES = ['qsbk.spiders']
NEWSPIDER_MODULE = 'qsbk.spiders'



# Obey robots.txt rules
ROBOTSTXT_OBEY = False


DOWNLOAD_DELAY = 1

DEFAULT_REQUEST_HEADERS = {
    'accept': '*/*',
    'accept-encoding': 'gzip, deflate, br',
    'accept-language': 'en-US,en;q=0.9,zh-CN;q=0.8,zh;q=0.7,zh-TW;q=0.6',
    'user-agent': 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_13_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/69.0.3497.100 Safari/537.36'
}

ITEM_PIPELINES = {
   'qsbk.pipelines.QsbkPipeline': 300,
}

```



start.py

```
# encoding: utf-8

from scrapy import cmdline

cmdline.execute(['scrapy', 'crawl', 'qsbk_spider'])
```





## CrawlSpider

继承自Spider，可有指定规则，满足一定的URL就可以进行爬取， 无需手动 yield Request



### 创建爬虫

```
scrapy genspider -c crawl [爬虫名字] [域名]
```



### LinkExtractors 链接提取器 

可以自动在所爬的页面上找到符合规则的url，实现自动爬取



### example

#### wxapp-union.com

CMD

```
scrapy startproject wxapp
cd wxapp/
scrapy genspider -t crawl wxapp_spider "wxapp-union.com"
```



wxapp_spider.py

```
# -*- coding: utf-8 -*-
import scrapy
from scrapy.linkextractors import LinkExtractor
from scrapy.spiders import CrawlSpider, Rule
from wxapp.items import WxappItem


class WxappSpiderSpider(CrawlSpider):
    name = 'wxapp_spider'
    allowed_domains = ['wxapp-union.com']
    start_urls = ['http://www.wxapp-union.com/portal.php?mod=list&catid=2&page=1']

    rules = (
        Rule(LinkExtractor(allow=r'.+mod=list&catid=2&page=\d'), follow=True),
        Rule(LinkExtractor(allow=r'.+article-.+\.html'), callback="parse_detail", follow=False),
    )

    def parse_detail(self, response):
        title = response.xpath("//h1[@class='ph']/text()").get()
        author_p = response.xpath("//p[@class='authors']")
        author = author_p.xpath(".//a/text()").get()
        public_time = author_p.xpath(".//span/text()").get()
        article_content = response.xpath("//td[@id='article_content']//text()").getall()
        article_content = "".join(article_content).strip()
        item = WxappItem(title=title, author=author, public_time=public_time, article_content=article_content)
        yield item
```



items.py

```
# -*- coding: utf-8 -*-

import scrapy


class WxappItem(scrapy.Item):
    title = scrapy.Field()
    author = scrapy.Field()
    public_time = scrapy.Field()
    article_content = scrapy.Field()
```



pipelines.py

```
# -*- coding: utf-8 -*-

# Define your item pipelines here
#
# Don't forget to add your pipeline to the ITEM_PIPELINES setting
# See: https://doc.scrapy.org/en/latest/topics/item-pipeline.html

from scrapy.exporters import JsonLinesItemExporter


class WxappPipeline(object):

    def __init__(self):
        self.fp = open('wxjc.json', 'wb')
        self.exporter = JsonLinesItemExporter(self.fp, ensure_ascii=False, encoding='utf-8')

    def process_item(self, item, spider):
        self.exporter.export_item(item)
        return item

    def close_spider(self):
        self.fp.close()
```



settings.py

```
BOT_NAME = 'wxapp'
SPIDER_MODULES = ['wxapp.spiders']
NEWSPIDER_MODULE = 'wxapp.spiders'
ROBOTSTXT_OBEY = False
DOWNLOAD_DELAY = 1
DEFAULT_REQUEST_HEADERS = {
    'accept': '*/*',
    'accept-encoding': 'gzip, deflate, br',
    'accept-language': 'en-US,en;q=0.9,zh-CN;q=0.8,zh;q=0.7,zh-TW;q=0.6',
    'user-agent': 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_13_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/69.0.3497.100 Safari/537.36'
}
ITEM_PIPELINES = {
   'wxapp.pipelines.WxappPipeline': 300,
}
```



start.py

```
#encoding: utf-8

from scrapy import cmdline

cmdline.execute("scrapy crawl wxapp_spider".split())
```