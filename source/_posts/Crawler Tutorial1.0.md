---
title: Crawler Tutorial1.0
date: 2016-08-20 17:21:20
tags: work
---
<div align="center">
<img src="/images/zhizhuwang.jpg" width = "500" height = "200" alt="图片名称" align=center />
</div>
# 创建
`scapy startproject w3school`
* 项目w3school
这时会产生w3school文件夹，文件夹下文件如下：
``` bash
scrapy.cfg  
w3school/  
    __init__.py  
    items.py  
    pipelines.py  
    settings.py  
    spiders/  
	__init__.py
```
其中scrapy.cfg目的配置文件。主要改写的是w3school中的三个文件以及其中spiders中需要编写的爬虫。

* 在items.py中定义Item容器。
也就是编写items.py内容。所谓Item容器就是将在网页中获取的数据结构化保存的数据结构，类似于Python中字典。下面为items.py中代码。
``` bash
#project: w3school  
#file   : items.py  
#author : younghz  
#brief  : define W3schoolItem.  
from scrapy.item import Item,Field  

class W3schoolItem(Item):  
	title = Field()  
	link = Field()  
	desc = Field()  
```
上面定义了自己的W3schoolItem类，它继承自scrapy的Item（这里没有显示定义W3schoolItem的__init__()方法，也正因为如此，python也会为你自动调用基类的__init__()，否则必须显式在子类的__init__()中调用基类__init__()）。
之后声明W3schoolItem中元素并使用Field定义。到此items.py就OK了。


* 在pipelines.py中编写W3schoolPipeline实现对item的处理。
在其中主要完成数据的查重、丢弃，验证item中数据，将得到的item数据保存等工作。代码如下：
``` bash
import json  
import codecs    
class W3SchoolPipeline(object):  
    def __init__(self):  
	self.file = codecs.open('w3school_data_utf8.json', 'wb', encoding='utf-8')  
  
    def process_item(self, item, spider):  
	line = json.dumps(dict(item)) + '\n'  
	# print line  
	self.file.write(line.decode("unicode_escape"))  
	return item  
```
其中的process_item方法是必须调用的用来处理item，并且返回值必须为Item类的对象，或者是抛出DropItem异常。并且上述方法将得到的item实现解码，以便正常显示中文，最终保存到json文件中。

注意：在编写完pipeline后，为了能够启动它，必须将其加入到ITEM_PIPLINES配置中，即在settings.py中加入下面一句：
ITEM_PIPELINES = {  
    'w3school.pipelines.W3SchoolPipeline':300  
}  

# 编写爬虫
爬虫编写是在spider/文件夹下编写w3cshool_spider.py。
先上整个程序在慢慢解释：
``` bash
#!/usr/bin/python  
# -*- coding:utf-8 -*-  
from scrapy.spiders import Spider  
from scrapy.selector import Selector  
from scrapy import log  

from w3school.items import W3schoolItem  
class W3schoolSpider(Spider):  
"""爬取w3school标签"""  
#log.start("log",loglevel='INFO')  
name = "w3school"  
allowed_domains = ["w3school.com.cn"]  
start_urls = [  
"http://www.w3school.com.cn/xml/xml_syntax.asp"  
]  

def parse(self, response):  
sel = Selector(response)  
sites = sel.xpath('//div[@id="navsecond"]/div[@id="course"]/ul[1]/li')  
items = []  

for site in sites:  
    item = W3schoolItem()  

    title = site.xpath('a/text()').extract()  
    link = site.xpath('a/@href').extract()  
    desc = site.xpath('a/@title').extract()  

    item['title'] = [t.encode('utf-8') for t in title]  
    item['link'] = [l.encode('utf-8') for l in link]  
    item['desc'] = [d.encode('utf-8') for d in desc]  
    items.append(item)  

    #记录  
    log.msg("Appending item...",level='INFO')  
    log.msg("Append done.",level='INFO')
return items
```
（1）需要注意的是编写的spider必须继承自scrapy的Spider类。
属性name即spider唯一名字，start_url可以理解为爬取入口。
（2）parse方法。
parse（）是对scrapy.Spider类的override。
（3）网页中的数据提取机制。
scrapy使用选择器Selector并通过XPath实现数据的提取。关于XPath 推荐w3school的教程。

# 匹配
* 1. sites = sel.xpath('//div[@id="navsecond"]/div[@id="course"]/ul[2]/li')  
以下是网页源代码，命令中`@id="navsecond"`匹配第一个div，course匹配第二个div，ul匹配下一级`<ul>`,序号[2]表示第2个`<ul>`框中内容。

``` bash
</div>

<div id="navsecond">

<div id="course"><h2>XML 基础</h2>
<ul>
<li class="currentLink"><a href="/xml/index.asp" title="XML 教程">XML 教程</a></li>
<li><a href="/xml/xml_intro.asp" title="XML 简介">XML 简介</a></li>
<li><a href="/xml/xml_usedfor.asp" title="XML 的用途">XML 用途</a></li>
<li><a href="/xml/xml_tree.asp" title="XML 树结构">XML 树结构</a></li>
<li><a href="/xml/xml_syntax.asp" title="XML 语法规则">XML 语法</a></li>
<li><a href="/xml/xml_elements.asp" title="XML 元素">XML 元素</a></li>
<li><a href="/xml/xml_attributes.asp" title="XML 属性">XML 属性</a></li>
<li><a href="/xml/xml_dtd.asp" title="XML 验证">XML 验证</a></li>
<li><a href="/xml/xml_validator.asp" title="XML 验证器">XML 验证器</a></li>
<li><a href="/xml/xml_browsers.asp" title="XML 浏览器支持">XML 浏览器</a></li>
<li><a href="/xml/xml_view.asp" title="查看 XML 文件">XML 查看</a></li>
<li><a href="/xml/xml_display.asp" title="使用 CSS 显示 XML">XML CSS</a></li>
<li><a href="/xml/xml_xsl.asp" title="使用 XSLT 显示 XML">XML XSLT</a></li>
</ul>
<h2>XML JavaScript</h2>
<ul>
<li><a href="/xml/xml_http.asp" title="XMLHttpRequest 对象">XML HTTP Request</a></li>
<li><a href="/xml/xml_parser.asp" title="XML 解析器">XML 解析器</a></li>
<li><a href="/xml/xml_dom.asp" title="XML DOM">XML DOM</a></li>
<li><a href="/xml/xml_to_html.asp" title="XML to HTML">XML to HTML</a></li>
<li><a href="/xml/xml_applications.asp" title="XML 应用程序">XML 应用程序</a></li>
</ul>
<h2>XML 高级</h2>
<ul>
...
```

# Reference
\[1\]scrapy研究探索（二）——爬w3school:http://blog.csdn.net/u012150179/article/details/32911511
