# ScrapyLabs
Scrapy Labs
1. 初始化项目

    scrapy startproject mzt
    cd mzt
    scrapy genspider meizitu meizitu.com

2. 添加 spider 代码：

定义 scrapy.Item ，添加 image_urls 和 images ，为下载图片做准备。

修改 start_urls 为初始页面, 添加 parse 用于处理列表页， 添加 parse_item 处理项目页面。Scrapy: 10分钟写一个爬虫抓取美女图

3. 修改配置文件：
DOWNLOAD_DELAY = 1 # 添加下载延迟配置
ITEM_PIPELINES = {'scrapy.pipelines.images.ImagesPipeline': 1} # 添加图片下载 pipeline
IMAGES_STORE = '.' # 设置图片保存目录
1
2
3
	
DOWNLOAD_DELAY = 1 # 添加下载延迟配置
ITEM_PIPELINES = {'scrapy.pipelines.images.ImagesPipeline': 1} # 添加图片下载 pipeline
IMAGES_STORE = '.' # 设置图片保存目录

4. 运行项目：

    scrapy crawl meizitu

看，项目运行效果图

Scrapy: 10分钟写一个爬虫抓取美女图

等待一会儿，就是收获的时候了

Scrapy: 10分钟写一个爬虫抓取美女图
Scrapy: 10分钟写一个爬虫抓取美女图
Scrapy: 10分钟写一个爬虫抓取美女图

项目源码已经放到了 Github 上面，欢迎大家 star !

https://github.com/zhangheli/ScrapyLabs
