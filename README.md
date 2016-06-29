
Scrapy: 10分钟写一个爬虫抓取美女图

#1. 初始化项目

    scrapy startproject mzt
    cd mzt
    scrapy genspider meizitu meizitu.com

#2. 添加 spider 代码：

定义 scrapy.Item ，添加 image_urls 和 images ，为下载图片做准备。

修改 start_urls 为初始页面, 添加 parse 用于处理列表页， 添加 parse_item 处理项目页面。

# -*- coding: utf-8 -*-
import os
import scrapy

class PItem(scrapy.Item):
    image_urls = scrapy.Field()
    images = scrapy.Field()


class MeizituSpider(scrapy.Spider):
    name = "meizitu"
    allowed_domains = ["meizitu.com"]
    start_urls = ( 'http://www.meizitu.com/a/list_1_1.html',)

    def parse(self, response):
        exp = u'//div[@id="wp_page_numbers"]//a[text()="下一页"]/@href'
        _next = response.xpath(exp).extract_first()
        next_page = os.path.join(os.path.dirname(response.url), _next)
        yield scrapy.FormRequest(next_page, callback=self.parse)
        for p in response.xpath('//li[@class="wp-item"]//a/@href').extract():
            yield scrapy.FormRequest(p, callback=self.parse_item)

    def parse_item(self, response):
        item=PItem()
        urls = response.xpath("//div[@id='picture']//img/@src").extract()
        item['image_urls'] = urls 
        return item



#3. 修改配置文件：

DOWNLOAD_DELAY = 1 # 添加下载延迟配置
ITEM_PIPELINES = {'scrapy.pipelines.images.ImagesPipeline': 1} # 添加图片下载 pipeline
IMAGES_STORE = '.' # 设置图片保存目录

#4. 运行项目：

    scrapy crawl meizitu

看，项目运行效果图：http://www.factj.com/archives/609.html?utm_source=geek

https://github.com/zhangheli/ScrapyLabs
