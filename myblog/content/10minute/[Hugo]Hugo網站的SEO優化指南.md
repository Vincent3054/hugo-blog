---
title: "[Hugo]Hugo網站的SEO優化指南"
keywords :
- Hugo
- SEO
- search engine optimization
- optimization
description : "Hugo網站的SEO優化指南"
author : "Sky Chen"
slug: hugo-website-seo-guide
tags : ["10minute","Hugo"]
categories:
- 10minute
- Hugo
date: "2023-02-15"

coverSize: partial
coverImage: images/notes0001.jpg
thumbnailImage: images/notes0001.jpg
---
<!--more-->

# Hugo網站的SEO優化指南
###### tags: `SEO` `Hugo`

## 目錄

<!-- toc -->

## 內文

<h3 id="A">簡介</h3>

<h4 id="A1">SEO是什麼？</h4>

SEO是**搜尋引擎最佳化**的縮寫，是一種透過改善網站的架構和內容，讓網站在自然搜尋結果中排名更高的行銷手法。

<h4 id="A2">SEO的原理是什麼？</h4>

SEO的原理是透過了解搜尋引擎的運作規則，並根據這些規則來調整網站的各個元素，讓搜尋引擎能夠更容易地找到、索引和評分網站，從而提高網站在搜尋結果中的排名。

<h4 id="A3">SEO有哪些技巧？</h4>

SEO有兩種技巧：**內部優化**和**外部優化**。
  * 內部優化：是指**改善網站本身的架構、設計、速度、內容**等方面，讓網站更符合搜尋引擎和使用者的需求。
  * 外部優化：是指通過建立與其他相關網站的**連結、分享社交媒體等方式**，增加網站的權重和信譽。

<h4 id="A4">SEO有哪些優點？</h4>

SEO有以下幾個優點：
  * 可以提高自然流量和轉換率
  * 可以增加品牌曝光度和信任度
  * 可以節省廣告成本
  * 可以持續發揮效果
      
<h4 id="A5">SEO有哪些缺點？</h4>

  * SEO也有以下幾個缺點
  * 需要耗費時間和精力
  * 需要不斷更新和調整
  * 需要面對競爭者和搜尋引擎變化
  * 需要承受風險和不確定性
      
<h3 id="B">Hugo SEO</h3>

今天來聊聊 Hugo 在 SEO 這部分，我們有哪些工具可以運用。另外，也會介紹 Google 的 SEO 相關輔助工具，是如何讓我們的網站更容易被使用者搜尋。

<h4 id="B1">內部優化</h4>

##### 1. 把網頁 head 標籤中的 meta 訊息設定好

* 例如 ```title```, ```description```, ```keywords```, ```author```,```tags``` 等等。
* 這些東西可以加在網頁(例如文章)的 YAML Front Matter。
* 有任何想新增的 YAML Front Matter 欄位，也可以加在Front Matter中，如下

```YAML=
...

title: "[Hugo]Hugo網站的SEO優化指南"
keywords :
- Hugo
- SEO
- search engine optimization
- optimization
description : "Hugo網站的SEO優化指南"
author : "Sky Chen"
slug: hugo-website-seo-guide
tags : ["10minute","Hugo"]
categories:
- 10minute
- Hugo
date: "2023-02-15"
...
```

##### 2. 縮短Permalink，內容使用英文
Hugo 提供你自訂每篇文章的網址，請先看以下定義：

```yaml=
post = "/:year/:month/:slug/"
```
在每篇文章的 Front Matter 裡，若你有自訂的 slug 時，該篇文章會使用你定義的文字作為網址，例如：
```yaml=
https://your-baseurl.io/2020/09/your-slug
```

若是你配置 ```:slug``` 但 Front Matter 卻沒給 slug 設置時，```預設會使用 title 替代 slug```。

這邊也建議一開始先決定好「網址風格」，利如都用```簡單的英文拼湊```，或是完整英文描述，中文的話，會需要 encode，而產生的文字也不容易閱讀，會```影響到 Google Search ```結果。

<h4 id="B2">外部優化</h4>

##### 1. 提供 sitemap.xml

Hugo 內建產生網站 Sitemap 的服務，你可以透過修改 config.toml，去設置關於 Sitemap 的配置參數，以下是官方的設置參數範例：

```toml=
[sitemap]
  changefreq = "monthly"
  filename = "sitemap.xml"
  priority = 0.5
```

你也可以透過自行創建 ./layouts/sitemap.xml，來覆蓋(取代) Hugo 內建的 sitemap.xml 內容。

搞定 sitemap.xml 之後，在 Google 方面提供了 Search Console 介面，透過提交我們網站的 Sitemap.xml，告訴 Google 搜尋引擎，幫我們建立頁面索引，讓我們的網站頁面「可以被 Google」列出 。

###### Step.1 驗證
1. 點選「網址前置字元」須入完整網址

![]( /images/20230225001.png)

2. 確認無誤後，點擊「繼續」。

![]( /images/20230225002.png)

3. 在「其他驗證方法」點擊「HTML標記」展開視窗。

![]( /images/20230225003.png)

4. 將HTML標記做複製，可點擊右方複製按鈕，即會複製一整串。

![]( /images/20230225004.png)

5. 將html檔案放置於Release檔案位置最外層

```
 ..\myblog\public\googled242bbda8504621a.html
```

6. 回至Google Search Console頁面，點擊「驗證」。

![]( /images/20230225005.png)

7. 此時會出現「以驗證擁有權」視窗，可點擊「前往資源」，導向至該頁面。

![]( /images/20230225006.png)

8. 驗證完成，進入Google Search Console總覽頁面。

![]( /images/20230225007.png)

###### Step.2 Sitemap提交
1. 登入Google Search Console→點擊「站點地圖」（或是有的會顯示「Sitemap」）。

![]( /images/20230225008.png)

2. 輸入您的整串網域名稱並加入「/sitemap.xml」，例如：[https://shopstore.tw/sitemap.xml](https://shopstore.tw/sitemap.xml)，並點選「提交」。

![]( /images/20230225009.png)

3. 成功提交

![]( /images/20230225010.png)

##### 2. 提供 robots.txt

* robots.txt 是給爬蟲機器人看的文件，例如說哪些資源不給爬之類的，可以參考 [wiki](https://zh.wikipedia.org/wiki/Robots.txt)。

* 該文件名稱統一為小寫，./layouts/robots.txt。

* 文件內容如下

```YAML=
User-agent: *
Disallow: 
```
(上例為允許任何搜尋引擎檢索網站的所有內容與資源，包括頁面、圖片)

##### 3. 增強連結強度Permalink
* 因為 SEO 的排名，有一部分是根據連結的強度，例如好多篇網頁指向同一個網頁，這樣後者的連結權重就會提高。
* 而內部連結也可以達到類似效果，所以放心在自己的網頁中大量引用自己的網頁連結。
* 同時，也可以多使用社群連結，加強自身網頁的推廣。

<h3 id="B">剖析、了解自己的網站</h3>

* [Google Console](https://search.google.com/search-console) 可以看網站的曝光、點擊次數，並且了解哪個關鍵字最容易找到網站。
* [Google Analytics](https://analytics.google.com/analytics) 可以用來監測網頁的流量、哪些網頁獲得比較多的觀看次數等等。
* [Lighthouse audits](https://developers.google.com/web/tools/lighthouse/#devtools) 可以用來檢視網站的效能

## 參考連結
https://ithelp.ithome.com.tw/articles/10252309
https://shopstore.tw/article/44
https://ktinglee.github.io/how-improve-jekyll-seo/
