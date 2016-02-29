# Module 4 - Python Scrapy: Web Crawler and Data Processing

>（時間回到兩個月前，總統大選兩天後）
>
>老闆：誒，這次總統大選你怎麼看？
>
>你：就看電視啊。
>
>老闆：......我說你對這個局勢怎麼看？
>
>你：......我也不知道呢 ˊ_>ˋ
>
>老闆：哎，我們公司的產品受到政治影響很大呢，這次大選後很多地方的民意傾向都改變啦，我們得好好規劃一下未來我們的產品要怎麼賣，要賣到哪裡去。
>
>你：是的呢～
>
>老闆：哎，我想要瞭解一下全臺灣各個地區的投票結果是如何，然後做個分析。
>
>你：是的呢。
>
>老闆：現在請工讀生做這個要做多久啊？
>
>你：Hmmmmm 從網站找到資料，然後六都加起來好像有 150 多個區，市級有 10 多個區，然後還有 13 個縣，每縣有好幾個鄉鎮市，下面還有里，應該派十個工讀生每天做八個小時，一個禮拜可以做完吧 ˊ_>ˋ
>
>老闆：哦哦，好像還行啊。
>
>你：是啊是啊
>
>老闆：聽說你是資管系出來的吧，誒你去幫我搞定，一個禮拜後要。
>
>你：一個禮拜？老闆那是十個工讀生每天八個小時做一個禮拜啊。
>
>老闆：哎那不就是你一個月的薪水嗎？你資管系的，這個很簡單啦，交給你啦。
>
>你：ᶘ ᵒᴥᵒᶅ......

# 注意：由於當初我用來做教學的網站 404 了，所以這個教學會改用其他的網站做代替

## 學這堂課要幹麻

在 Web 2.0 以後，由使用者自行創建的資料開始充斥在網際網路上，新聞、社群網路、YouTube、blog 等等，對於從事社會科學、財經或者統計分析的人們來說，網路資料是一種低成本且非常值得研究的對象，另外網路資料對於現實現象的快速反應，在一定程度上也能夠反應一些社會現象。

早期的電子商務就已經瞭解到分析顧客資料能夠帶來的效益，而自從 Twitter、Facebook 之類的社群網路興起後，如何從顧客在社群中的互動、各種的貼文以及上傳中找出他們可能的購買行為也一直是廣告電商的兵家必爭之地。

在資訊爆炸的時代裡，我們不可能用人工的方式將資料一點一點複製貼上，因此如何透過程式去自動抓取我們想要的資料便成為一個資訊人員最基本也必需要擁有的能力之一。

## 學完這堂課你可以

- 了解網路爬蟲的基礎概念
- 了解如何使用 Python Scrapy 來撰寫網路爬蟲
- 如何綜合使用不同的工具來幫助我們爬取資料

## 課程大綱

* [Module 4 - Python Scrapy: Web Crawler and Data Processing](#module-4---python-scrapy:-web-crawler-and-data-processing)
  * [學這堂課要幹麻](#學這堂課要幹麻)
  * [學完這堂課你可以](#學完這堂課你可以)
  * [課程大綱](#課程大綱)
* [A. Overview: Websites data extraction](#a.-overview:-websites-data-extraction)
* [B. Scrapy: Python framework for extracting data from websites](#b.-scrapy:-python-framework-for-extracting-data-from-websites)
  * [b1. Installation with pip](#b1.-installation-with-pip)
  * [b2. Creating a Scrapy project](#b2.-creating-a-scrapy-project)
  * [b3. What do you want? Defining Items](#b3.-what-do-you-want?-defining-items)
  * [b4. Reading website using program: Writing the first spider](#b4.-reading-website-using-program:-writing-the-first-spider)
  * [b5. Extracting data with XPath (and Scrapy shell)](#b5.-extracting-data-with-xpath-(and-scrapy-shell))
  * [b6. Output extracted data as CSV or JSON format](#b6.-output-extracted-data-as-csv-or-json-format)
* [C. Dealing with JavaScript: Using NodeJS](#c.-dealing-with-javascript:-using-nodejs)
  * [c1. Why NodeJS?](#c1.-why-nodejs?)
  * [c2. Tracing JavaScript code with Firebug](#c2.-tracing-javascript-code-with-firebug)
* [D. Advanced topics](#d.-advanced-topics)
  * [d1. Following links](#d1.-following-links)
  * [d2. CrawlSpider: Following links by defining rules](#d2.-crawlspider:-following-links-by-defining-rules)

---

<!--========================================================
=            Overview: Websites data extraction            =
=========================================================-->

# A. Overview: Websites data extraction

在 Web 2.0 以後，由使用者自行創建的資料開始充斥在網際網路上，新聞、社群網路、YouTube、blog 等等，對於從事社會科學、財經或者統計分析的人們來說，網路資料是一種低成本且非常值得研究的對象，另外網路資料對於現實現象的快速反應，在一定程度上也能夠反應一些社會現象。

早期的電子商務就已經瞭解到分析顧客資料能夠帶來的效益，而自從 Twitter、Facebook 之類的社群網路興起後，如何從顧客在社群中的互動、各種的貼文以及上傳中找出他們可能的購買行為也一直是廣告電商的兵家必爭之地。

在資訊爆炸的時代裡，我們不可能用人工的方式將資料一點一點複製貼上，因此如何透過程式去自動抓取我們想要的資料便成為一個資訊人員最基本也必需要擁有的能力之一。

網路上其實有很多種 Python 網路爬蟲的實現方式，在這一堂課中我們會使用一個滿新（我覺得啦）的 Python framework: Scrapy。

<!--====  End of Overview: Websites data extraction  ====-->


<!--===================================================================
=            Scrapy: Elegent framework for data extraction            =
====================================================================-->

# B. Scrapy: Python framework for extracting data from websites

網路爬蟲已經是一個滿成熟的東西，有非常多的方案可以選擇，你可以用最古老的方法造一個輪子，也可以用別人幫你寫好的工具，各種方法之間各有優缺點，通常是依照你自己的需求去選擇啦。

如果你擅長 JavaScript/jQuery 的話也可以參考看看別人用 NodeJS 實現的爬蟲，連結在延伸閱讀裡。

Scrapy 是一套開源、基於 Python 的 web crawling framework，他非常的簡潔也非常的容易上手，只要你稍微了解 Python 以及 HTML 就可以撰寫一個簡單的爬蟲，另外 Scrapy 提供的 Scrapy shell 讓我們可以快速地測試爬蟲的規則，就像 Python 的互動式介面一樣。

## b1. Installation with pip

### Python2 and Python3

最初的 Scrapy 是用 Python2 撰寫的，而 Python3 的版本目前還在開發當中。在這份教學裡面我們會 **採用 Python2 的 Scrapy** ，但基本上不會遇到太多版本差異的問題，我們仍然保留語法上的一致性（Python3），這邊列出幾個需要注意的差別：

```python
# -*- coding: utf-8 -*-
# 請在所有 script 的第一行加入上面這句，告訴 Python 要使用 UTF-8 來解讀這一個 script（詳細說明可以參考 module1）

# print 有時候用 Python3 的語法不會印出你想要的東西
print('hello, world')  # Python3
print 'hello, world'   # Python2 

# string format 我們用比較通用的語法
print('This will print: {mystr}'.format(mystr='hello world'))
```

### Install Python2

首先我們要安裝一下 Python2 ，這份教學裡面的程式碼都用 `Python 2.7.10` 的版本測試，如果你已經有 Python2 但是不是這一個版本也沒關係，大部分的情況下應該是可以跑的。

但因為我沒有在其他的平台上測試過，如果你用你的版本發生問題的話請在討論區發問，謝謝。

基本上 Python2 的安裝方式跟安裝 Python3 的方式一模一樣，Windows 版本可以在[這裡下載](https://www.python.org/downloads/release/python-2710/)，OSX 跟 Linux 通常會自帶。

### pip 安裝 Scrapy

在你的 cmd/terminal 中打入以下指令，為避免版本問題，指定使用 `pip2`：

```bash
$ pip2 install scrapy

# 注意，你的電腦可能會找不到 pip2 這一個指令，這時你可以直接去 Python2 的安裝路徑下找 pip 來使用（如果還是找不到的話可以發問）

# 另外你可以透過 pip --version 來確定你的 pip 到底是什麼版本的
$ pip --version
pip 7.1.0 from ....../python2.7/site-packages (python 2.7)
$ pip2 --version
pip 7.1.0 from ....../python2.7/site-packages (python 2.7)
$ pip3 --version
pip 8.0.2 from ....../python3.5/site-packages (python 3.5)
```

## b2. Creating a Scrapy project

```bash
$ scrapy startproject news_website
```

```
news_website     <-- Project root folder
├── scrapy.cfg            <-- Scrapy 的部署設定檔
└── news_website <-- 爬蟲本體（Python package）
    ├── __init__.py 
    ├── items.py          <-- 用於定義要抓什麼資料
    ├── pipelines.py      <-- Item piplines，可以定義在抓到 Item 之後要做什麼處理
    ├── settings.py       <-- 這一隻爬蟲的設定
    └── spiders           <-- 用來放自己定義的爬蟲（Python package）
        └── __init__.py
```

## b3. What do you want? Defining Items

別忘了第一行的 `# -*- coding: utf-8 -*-` 。

```python
# -*- coding: utf-8 -*-

import scrapy

class NewsWebsiteItem(scrapy.Item):
    """ Define what data is we want
    """
    title       = scrapy.Field()      # News title
    article_url = scrapy.Field()      # News URL
    author      = scrapy.Field()      # News author
    provider    = scrapy.Field()      # News provider
    datetime    = scrapy.Field()      # Uploaded time
    content     = scrapy.Field()      # Text content
    # ......
```

## b4. Reading website using program: Writing the first spider

在 `news_website/spiders` 資料夾底下，新增 `pop_news_spider.py`：

```python
# -*- coding: utf-8 -*-

import scrapy

class PopNewsSpider(scrapy.Spider):
    name = "pop_news_spider"
    allowed_domains = ["udn.com"]
    start_urls = [
        "http://udn.com/news/cate/6638",
    ]

    def parse(self, response):
        """ When response is received, this method will be called
        """
        filename = response.url.split("/")[-2] + '.html'
        with open(filename, 'wb') as f:
            f.write(response.body)
```

### 執行

```bash
$ pwd # Make sure you are under 'news_website'
.../news_website
$ scrapy list # Shows the available spiders
pop_news_spider
$ scrapy crawl pop_news_spider # Run the spider 'pop_news_spider'
```

```
[scrapy] INFO: Scrapy 1.0.4 started (bot: news_website)
# ......
[scrapy] DEBUG: Crawled (200) <GET http://udn.com/news/cate/6638> (referer: None)
[scrapy] INFO: Closing spider (finished)
# ......
[scrapy] INFO: Dumping Scrapy stats:
# 這邊會有一些 Scrapy 關於這次執行的統計
{'downloader/request_bytes': 219,
 'downloader/request_count': 1,
 'downloader/request_method_count/GET': 1,
 'downloader/response_bytes': 13993,
 'downloader/response_count': 1,
 'downloader/response_status_count/200': 1,
 'finish_reason': 'finished',
 'finish_time': datetime.datetime(2016, 2, 29, 2, 7, 9, 259227),
# ......
[scrapy] INFO: Spider closed (finished)
```

### 結果

```html
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd"><html><head><meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1"> 
<!-- ...... -->
```

### Scrapy 的工作流程

1. 從 `start_urls` 內的網址開始
1. 準備 Request 物件
1. 執行 Request
1. 取得 Response
1. parse()

## b5. Extracting data with XPath (and Scrapy shell)

```bash
$ scrapy shell http://udn.com/news/cate/6638
# ......
2016-02-29 10:19:29 [scrapy] INFO: Spider opened
2016-02-29 10:19:29 [scrapy] DEBUG: Crawled (200) <GET http://udn.com/news/cate/6638> (referer: None)
[s] Available Scrapy objects:
[s]   crawler    <scrapy.crawler.Crawler object at 0x10a2cdf10>
[s]   item       {}
[s]   request    <GET http://udn.com/news/cate/6638>
[s]   response   <200 http://udn.com/news/cate/6638>
[s]   settings   <scrapy.settings.Settings object at 0x10b611b50>
[s]   spider     <PopNewsSpider 'pop_news_spider' at 0x10d41d990>
[s] Useful shortcuts:
[s]   shelp()           Shell help (print this help)
[s]   fetch(req_or_url) Fetch request (or URL) and update local objects
[s]   view(response)    View response in a browser
# 以下進入 Scrapy shell
```

### XPath 語法簡介

- `response.xpath('//h2')`: 選擇「整個文件中」所有的 h2 節點 
- `response.xpath('h2')`: 選擇「目前節點」下所有的 h2 節點 
- `response.xpath('p/h2')`: 選擇是 p 節點 child 的 h2 節點（一層） 
- `response.xpath('p//h2')`: 選擇是 p 節點 descendant 的 h2 節點（兩層以下） 
- `response.xpath('p[@class="10"]')`: 選擇有屬性 class 且值為 10 的 p 節點 

```python
# In Scrapy shell

# XPath 語法簡介
response.xpath('//h2')    # 選擇「整個文件中」所有的 h2 節點
response.xpath('h2')      # 選擇「目前節點」下所有的 h2 節點
response.xpath('p/h2')    # 選擇是 p 節點 child 的 h2 節點（一層）
response.xpath('p//h2')   # 選擇是 p 節點 descendant 的 h2 節點（兩層以下）
response.xpath('p[@class="10"]')   # 選擇有屬性 class 且值為 10 的 p 節點

# 過濾節點（根據我們要抓的網站）
dt_list = response.xpath('//dt')   # 整個網站中所有的「dt」節點
a_list = dt_list.xpath('a[h2]')  # 有 h2 子節點的 a 節點
# 過濾內容
article_url_list = a_list.xpath('@href') # 取出 href attribute
title_list = a_list.xpath('h2')  # h2 節點

# 看看抓出來的內容
# .extract() 可以直接抓出這一個節點的內容
# .xpath('text()') 可以把這一個節點的內容的標籤過濾掉

for i in article_url_list:
    print(i.extract())
# /news/story/1/1531276
# /news/story/1/1531275
# /news/story/1/1531214
# /news/story/1/1530707
# /news/story/1/1530576
# /news/story/6655/1531190-社子島開發投票「生態」案勝出-支持率近6成
# /news/story/6655/1531197-柯文哲：生態社子島-是方向非方案
# /news/story/6655/1531200-「生態」案規劃…景觀宅、親水廊帶、環狀輕軌
# ......

for i in title_list:      
    print(i.extract())  # 會包含「h2」的標籤
# <h2>美麗華堅持不退 國軍「逸園」促參案延命</h2>
# <h2>三官精華寶地 國防部爭取留用</h2>
# <h2>家扶：弱勢童的教育協助 不能只給錢</h2>
# <h2>國民黨中央黨部被丟汽油彈 馬：散播仇恨激化對立</h2>
# <h2>日廢核專家訪核二 因無商務簽證遭拒</h2>
# <h2>社子島開發投票「生態」案勝出 支持率近6成</h2>
# <h2>柯文哲：生態社子島 是方向非方案</h2>
# ......

for i in title_list:
    print(i.xpath('text()')[0].extract())  # 只有文字沒有標籤
# 美麗華堅持不退 國軍「逸園」促參案延命
# 三官精華寶地 國防部爭取留用
# 家扶：弱勢童的教育協助 不能只給錢
# 國民黨中央黨部被丟汽油彈 馬：散播仇恨激化對立
# 日廢核專家訪核二 因無商務簽證遭拒
# 社子島開發投票「生態」案勝出 支持率近6成
# 柯文哲：生態社子島 是方向非方案
# ......

```

### XPath 文檔

[點我](http://www.w3schools.com/xsl/xpath_syntax.asp)

## b6. Using your own Items

```python
from news_website.items import NewsWebsiteItem    # <-- 要記得 import 自己定義的 Item
# ......
class PopNewsSpider(scrapy.Spider):
# ......
    def parse(self, response):
        """ When response is received, this method will be called
        """
        # 過濾節點（根據我們要抓的網站）

        dt_list = response.xpath('//dt')   # 整個網站中所有的「dt」節點
        a_list = dt_list.xpath('a[h2]')    # 有 h2 子節點的 a 節點

        # 過濾內容

        article_url_list = a_list.xpath('@href')  # 取出 href attribute
        title_list = a_list.xpath('h2')           # h2 節點

        # 使用我們預先定義的 Items

        for i in a_list:
            new_item = NewsWebsiteItem()
            new_item['title'] = i.xpath('h2/text()')[0].extract()
            new_item['article_url'] = i.xpath('@href')[0].extract()
            yield new_item
```

重新運行 `scrapy crawl pop_news_spider` 你會看到一些新的東西冒出來了：

```
$ scrapy crawl pop_news_spider
......
[scrapy] DEBUG: Scraped from <200 http://udn.com/news/cate/6638>
{'article_url': u'/news/story/9446/1531013-\u65b0\u5317\u793e\u6703\u4f4f\u5b85-\u9707\u5f8c\u5065\u6aa2\u7121\u865e',
 'title': u'\u65b0\u5317\u793e\u6703\u4f4f\u5b85 \u9707\u5f8c\u5065\u6aa2\u7121\u865e'}
[scrapy] DEBUG: Scraped from <200 http://udn.com/news/cate/6638>
{'article_url': u'/news/story/9446/1530931-\u5f70\u7e235\u6a13\u4ee5\u4e0a\u5efa\u7269-\u512a\u5148\u8010\u9707\u8a55\u4f30',
 'title': u'\u5f70\u7e235\u6a13\u4ee5\u4e0a\u5efa\u7269 \u512a\u5148\u8010\u9707\u8a55\u4f30'}
[scrapy] DEBUG: Scraped from <200 http://udn.com/news/cate/6638>
{'article_url': u'/news/story/6656/1530908-\u8a55\u8ad6-\uff0f\u57fa\u9686\u5e02\u9577\uff0c\u60a8\u65e9\u8a72\u6012\u4e86',
 'title': u'\u8a55\u8ad6 \uff0f\u57fa\u9686\u5e02\u9577\uff0c\u60a8\u65e9\u8a72\u6012\u4e86'}
[scrapy] DEBUG: Scraped from <200 http://udn.com/news/cate/6638>
{'article_url': u'/news/story/6656/1530874-\u6c11\u9032\u9ee8\u5f70\u7e23\u9ee8\u90e8\u4e3b\u59d4\u6539\u9078-3\u5927\u5496\u89d2\u9010',
 'title': u'\u6c11\u9032\u9ee8\u5f70\u7e23\u9ee8\u90e8\u4e3b\u59d4\u6539\u9078 3\u5927\u5496\u89d2\u9010'}
......
```

## b7. Output extracted data as CSV or JSON format

```bash
# 儲存成 JSON 格式
$ scrapy crawl pop_news_spider -o pop_news.json
# 儲存成 CSV 格式
$ scrapy crawl pop_news_spider -o pop_news.csv
```

## b8. Full code of the spider

```python
# -*- coding: utf-8 -*-

import scrapy

from news_website.items import NewsWebsiteItem

class PopNewsSpider(scrapy.Spider):
    name = "pop_news_spider"
    allowed_domains = ["udn.com"]

    # 定義要從哪個網址開始

    start_urls = [
        "http://udn.com/news/cate/6638",
    ]

    def parse(self, response):
        """ When response is received, this method will be called
        """
        # 過濾節點（根據我們要抓的網站）

        dt_list = response.xpath('//dt')   # 整個網站中所有的「dt」節點
        a_list = dt_list.xpath('a[h2]')    # 有 h2 子節點的 a 節點

        # 過濾內容

        article_url_list = a_list.xpath('@href')  # 取出 href attribute
        title_list = a_list.xpath('h2')           # h2 節點

        # 使用我們預先定義的 Items

        for i in a_list:
            new_item = NewsWebsiteItem()
            new_item['title'] = i.xpath('h2/text()')[0].extract()
            new_item['article_url'] = i.xpath('@href')[0].extract()
            yield new_item
```

<!--====  End of Scrapy: Elegent framework for data extraction  ====-->

<!--====================================
=            Something else            =
=====================================-->

# C. Advanced topics

## c1. Following links

## c2. CrawlSpider: Following links by defining rules

<!--====  End of Something else  ====-->

---

# 延伸閱讀

## Item pipline

Scrapy 裡面提供了 Item pipline 的機制，讓你在抓到 Item 之後可以自動做一些處理，例如：

1. 資料清理
1. 資料驗證
1. 塞進資料庫
1. ... 

這只是一個額外的功能，因此放在延伸閱讀裡面供大家參考。

[連結點我](http://doc.scrapy.org/en/latest/topics/item-pipeline.html)

## NodeJS Web crawler/spider

使用 DOM 的方式在 server 端爬資料還滿有趣的，比起 xpath ，對於熟悉 jQuery 的人來說應該會更容易上手，[請看這裡](https://github.com/sylvinus/node-crawler)。

## JavaScript 的問題

## 你用 Python 做过什么有趣的数据挖掘项目？

這是一個在知乎上面的回答，我覺得滿有趣的所以當成延伸閱讀，順便看看其他人拿 Python 來做什麼。

[連結點我](http://36kr.com/p/5042690.html)