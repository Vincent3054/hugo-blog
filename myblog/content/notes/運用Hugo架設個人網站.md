---
categories:
- Notes
- Side Project
date: "2023-02-15"
title: "運用Hugo架設個人網站"
tags : ["Side Project"]
coverSize: partial
coverImage: images/notes0001.jpg
thumbnailImage: images/notes0001.jpg
---
<!--more-->

# 運用Hugo架設個人網站
###### tags: `Side Project`
## 如何使用 Hugo 在 GitHub 上架設個人網站？
### 1. Chocolatey (Windows)
如果你是使用 Windows 可透過 [chocolatey](https://chocolatey.org/) 安裝：

```
//安裝chocolate

Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```
### 2. 安裝hugo
```
//安裝hugo
choco install hugo -confirm

//測試安裝安裝hugo成功
hugo version
```
### 3. hugo new
在你安裝完 Hugo 指令後，可透過以下指令建置新專案：
```
hugo new site myblog
```
### 4. 透過 git 安裝佈景
根據官網指引安裝佈景，在安裝前你必須先有 git，我的建議是若你還沒有 git cli，先安裝 git，之後我也會建議你把整個專案做版本控制，若是你打算部署到 GitHub Pages，那你就更需要先裝好他。
```git=
# 在專案目錄底下 ./myblog
git init

## 基礎布景
git submodule add https://github.com/budparr/gohugo-theme-ananke.git themes/ananke

## 部落格布景
git submodule add https://github.com/kakawait/hugo-tranquilpeak-theme.git themes/tranquilpeak
```
[tranquilpeak佈景主題詳細設定官方文件](https://github.com/kakawait/hugo-tranquilpeak-theme/blob/master/docs/user.md)

編輯 config.toml 指定佈景名稱為 ananke (tranquilpeak 或別的)
```
echo 'theme = "ananke"' >> config.toml
```
為了在本地跑起來時可以看到點內容，我們先新增一篇文章
```
hugo new posts/my-first-post.md
```
檔案會被建立在 **./content/posts/my-first-post.md** 底下。請注意，省略 **.md** 的話，你的文件就不會被渲染到頁面上。

執行以下指令，在本地運行 hugo 專案：
```
hugo server -D
```
訪問 http://localhost:1313/ ，網站已經在本地跑起來了

:::danger
如果遇到以下錯誤
Error: "D:\github\myblog\config.toml:1:1": unmarshal failed: toml: key theme is already defined
請開啟config.toml，把多餘的null刪除
:::

## 5.瞭解Hugo 資料結構
```
.
├── archetypes
├── config.toml
├── content
├── data
├── layouts
├── static
└── themes
```
* archetypes
放文章模板文件的地方，當你 new 一個新的 content files 時，會根據這邊的模板產生 markdown 文件，例如 archetypes/default.md，若你 new 的文章頂層資料夾名稱 (top level path) 對應不到模板時，會使用 default.md 作為模板生成文件。

* config.toml
網站 environments 配置檔，所有網站建置參數都可在此設置，之後文章有提到或使用相關設置時會在個別說明。

* content
所有 new 出來的文章都會放在這；如果你想要把文章個別分不同的 setion (top level path)，例如 drafts（草稿）、posts（已發布文章），可透過新增文章指令，指定的不同頂層路徑，生成文件到不同資料夾中。

* data
我目前還沒使用到這個資料夾，依照官方說法是，你可以把一些資料集放在這，支援格式有 YAML, JSON, 或是 TOML；換句話說，這可以當作你的資料庫使用，例如你的網站是專門介紹咖啡的，你有一組每個縣市最好喝的咖啡清單，就可以在這邊創建：
```json=
{
    "taipei_no_1": "鐵定好喝咖啡店",
    "taichung_no_1": "1976 咖啡館",
    ...
}
```
至於運用方式請參考 [Hugo Data Templates](https://gohugo.io/templates/data-templates/)。

* layouts
你的靜態網站的 .html 文件都會放在這，但你 new 的專案一開始會是空的，主要都是由佈景建構 layouts。

* static
靜態資源檔案，例如圖片、js、css 等會放在這邊。

* themes
放各種佈景的地方，如果不常換來換去的話，底下只會放一種佈景，你可以建置一個 sandbox，透過 --theme 參數去切換嘗試各種不同佈景，在本地跑起來看看他們的樣子。

* 其他
還有很多資料夾是 new site 時不會產生的，例如 assets、i18n、public，之後文章還會有機會帶到；明天會講要如何挑選佈景。

## 6.選擇Hugo Theme 佈景
### 佈景風格

建議先問問自己想要的感覺，找幾個你有看過、喜歡的部落格風格，列出幾個一定要有的特點，在此提供幾個我自己的評估方向做參考：

* 整體樣式: 你曾經看過的部落格樣式，你想要用跟他相似的，或是想用成一樣的
* 特定文章: 例如你要專寫技術文章，可以透過 Hugo Theme 右側列出的 tag 去查找
* 內外佈局: 文章展開 (繼續閱讀 more) 前後的感覺，是否要有側邊欄 (Menu)，或導航列 (Navbar) 等
* 選單圖案: 佈景提供的 Menu 連結搭配的 icon 樣式與排列
* markdown style: 佈景 demo 通常會有 markdown showcase 文章供你參考，可以藉由範例展示想像一下文章寫完的樣子
* code block style: 佈景的 code block 是否方便透過 config 替換樣式、顯示行號
* shortcode: 額外工具，例如 Highlight Text 、數學公式、流程圖繪製、 GA 、評論系統等
* 其他功能: 分頁連結 (Pagination)，顯示預估閱讀時間 (Reading time) 等

[布景主題網址](https://themes.gohugo.io/tags/blog/)
### clone the theme
執行以下指令 clone theme repo 到你專案底下的 themes 資料夾中：
```
git clone https://github.com/kakawait/hugo-tranquilpeak-theme.git themes/tranquilpeak
```
### copy the example config.toml
你可以先複製他提供的範例配置，之後依需求改變部分設置參數，這樣就不用重頭到尾自己設定：
```
cp themes/tranquilpeak/exampleSite/config.toml ./config.toml
```
:::danger
如果遇到布景buid的時候顯示error，不支援scss問題 請安裝以下hugo版本
```
choco install hugo-extended
```
:::

## 7.編輯文章內容

### Hugo Content - Archetypes
Hugo 提供了 Archetypes 作為內容模板，在新增 Content Page 時，根據 Content Type 翻印對應模板，新生成的檔案就有模板的 Front Matter 預先配置、文章基本段落等等，在由寫作者調整部分參數，快速進入寫作的環節。

#### Archetypes 套用順序
下指令 **hugo new posts/my-first-post.md** 新增一份 Content Page 之後，翻印來源會依據指令、下列順序，找出有無符合模板，有的話則翻印一份產生新的文章：

* archetypes/posts.md
* archetypes/default.md
* themes/my-theme/archetypes/posts.md
* themes/my-theme/archetypes/default.md

新增完成後，當你執行下列指令建立新的文章時：
```
hugo new triathlon/day-01-hello-hugo.md
```
在 ./content/ 底下會新增 triathlon/ 這個 content-section，且同時會在底下新增一個 day-01-hello-hugo.md 的檔案

#### 目前使用的 Archetypes
筆者目前正在使用中的模板有以下五種，分別是：

* default.md: 預設模板，沒動過
* post.md: 文章模板，new 出來時為已發布狀態，draft 狀態為 false
* draft.md: 草稿模板，new 出來時為未發布狀態，draft 狀態為 true
* sandbox.md: 測試用模板，用來嘗試各種語法，摸索 hugo 如何使用
* page.md: 單頁模板，與文章模板有些區別，例如此模板不預設文章分類

#### 文章結構
文章模板的內容也體現出了作者在寫作時，對於每個種類的文章規劃的結構，筆者自己的文章基本上區分為：

* Front Matter 區塊，在 .md 檔案內容最上面，有一塊用 --- 隔開的內容。
* Body 區塊，也就是文章內容區塊，緊接在 Front Matter 之後，主要會使用檔 markdown 語法，以及 shortcode 的地方。
* Footer: 此區域用以標示文章作者、永久鏈結，以及與文章許可協議。
```
---

+++ Front Matter +++
 
---

+++ Body +++


---
+++ Footer +++
```
### Hugo Content - Front Matter
在架設部落格時，想要趕快搞定網站基礎設施與寫文環境，那你就必須先配置好你的 config、文章模板 archetypes，以及規劃模板中的 Front Matter 了。

只要依據個人需求把 Front Matter 設置好，就能在每次 new post 翻印出新的文章檔案時，改一改幾個特定參數，就能開始動手寫，縮短「建立新檔 -> 寫文章」這段時間，今天就帶大家認識一下什麼是 Hugo Front Matter。

在每個文章檔案.md 中，放在內容最前面那塊以 - - - 分隔的區塊內容，就是 Front Matter (- - - 只是其中一種格式)；Hugo 支援四種 Front Matter 格式：
```ysml=
---
categories:
- Hugo
- Test
date: "2020-09-25"
slug: "test"
title: "我是 yaml 格式的 Front Matter"
---

Boom!!
```

#### Front Matter Variables
在 Front Matter 中有許多可設置變數，以下介紹幾個筆者常用的參數：

**定義文章標題、描述、作者**
* title 文章標題
* description 文章概要
* author 文章作者

**定義文章分類、標籤、關鍵字**
* categories 文章分類
* tags 文章標籤
* keywords 關鍵字

**定義文章類型、日期、狀態**
* type 文章類型，通常為 top level 資料夾名稱
* date 文章創建日期，若未設置 publishDate 的情況下，文章會依此作為發布日期時間
* draft 草稿狀態
* publishDate 預定發布日期，若是未來時間，須下 hugo server -F 才看得到文章

**Front Matter 自定義參數**

我們使用佈景之所以可以透過 Front Matter 微調一些文章佈局設定，就是新增了各種「自訂參數」，讓 hugo 語法可以從你設置的參數去套用 layout 的變化，舉例來說 (以下為佈景提供的設置)：

* metaAlignment 設置文章 title 的對齊位置
* coverImage 設置文章 cover image 的地方
* coverMeta 設置文章 title 要放在 cover image 中央，還是外面
* coverSize 設置文章 cover image 要大張還是小張

### Hugo Shortcode 介紹
#### Shortcode 簡介
我們知道 Hugo Content 其內容主要是用 Markdown 這類文字標記語法所寫成，內容格式、可用語法較為基礎簡單，若是我們想要套用更多樣化的語法時，只用 Markdown 是做不到的，而且我們不能在 .md 中撰寫如 HTML 的語法，此時就可以透過 Hugo Shortcode 來為我們處理這一塊。

#### Shortcode V.S. Hugo Template
Shortcode 可以看作是「一小塊 HTML 程式片段」，與 Hugo Template 不同的是，前者通常運用在「插入特定用途」、「重複使用」的片段語法到 markdown 內容中，而後者則是作為 markdown content 的外殼載體、或是佈局規劃等，用以構成我們最後呈現的視圖頁面 (View)。

換句話說，Template 有點像尚未擺放任何拼圖的底框，拼圖畫面則是文章內容，在使用 Shortcode 豐富其畫面的變化。

#### hortcode 使用說明
在專案底下新增以下結構資料：
```
./layouts
└── shortcodes
    └── img.html
```
shortcodes 資料夾用來放置所有 shortcode，資料夾名稱不可異動，大小寫也須完全相同。而底下的每一支 .html，例如 img.html 都是一支可以被插入到 .md 的 shortcode 原始碼。

#### 插入圖片-hortcode

Shortcodes 語法
創建 Shortcode ./layout/shortcodes/img.html，內容如下：
```
<img src="{{ .Get `src` }}">
```

用法如下：
```
# 本地圖片 ./static/images/image1.png
{{< img src="/images/image1.png" >}}

# 外部圖片 https://i.imgur.com/D3fTjrl.png
{{< img src="https://i.imgur.com/D3fTjrl.png" >}}
```
## 8.部屬推版

```
# 獲取 Repository URL，例如 git@github.com:littlebookboy/littlebookboy.github.io.git

# 進入到專案底下，打包你的網站，生成 public 資料夾
$ hugo

# 進入到專案底下，執行遠端資源庫地址註冊
$ cd your-site/
$ git init
$ git remote add origin https://github.com/Vincent3054/Vincent3054.github.io.git

# 確認遠端資源庫地址註冊成功
$ git remote -v

# 將目前異動提交成一個 commit
$ git add .
$ git commit -m 'initial site'
$ git branch -M main

# 推送 commit
$ git push or $ git push -u origin main
```
### 瀏覽結果
此時你可以開啟 https://your-username.github.io 瀏覽看看網站是否已經部署成功，理論上不會等太久，就可以看到頁面了。
https://Vincent3054.github.io

## 9. Hugo SEO
### Hugo Sitemap 與 Google Webmasters
Hugo 內建產生網站 Sitemap 的服務，你可以透過修改 config.toml，去設置關於 Sitemap 的配置參數，以下是官方的[設置參數範例](https://gohugo.io/templates/sitemap-template/#configure-sitemapxml)：
```
[sitemap]
  changefreq = "monthly"
  filename = "sitemap.xml"
  priority = 0.5
```
你也可以透過自行創建 ./layouts/sitemap.xml，來覆蓋(取代) Hugo 內建的 sitemap.xml 內容。

搞定 sitemap.xml 之後，在 Google 方面提供了 Search Console 介面，透過提交我們網站的 Sitemap.xml，告訴 Google 搜尋引擎，幫我們建立頁面索引，讓我們的網站頁面「可以被 Google」列出 (這只是 SEO 的其中一小步)。

### Hugo 與 Google Analytics (GA)
若網站頁面已經可以被 Google 搜尋到，我們可以透過 Google Analytics 工具，來觀察網站被訪問的情況；Hugo 已幫我們整合了 Google Analytics 工具，只要在 config.toml 中，設置參數 googleAnalytics 即可啟用 (建立新的 Google Analytics 可往這參考官方說明)。
```
googleAnalytics = "UA-XXXXXXXXX-X"
```

上面那串 UA-XXXXXXXXX-X 為 Google Analytics 帳戶的追蹤 ID，點擊介面左下角的「管理」，進去資源管理介面，點選「資源設定」，就會看到你的追蹤 ID：

成功啟用之後，你可以在 Google Analytics 介面，看到已有接收到網站數據傳回：

如果還沒有看到數據，而你確定有啟用成功，可以試著用不同裝置、網路、瀏覽器開無痕，去造訪你的網站，模擬自己是一個新訪客，靜候幾分鐘觀察看看。

### robots.txt
建立 ./layouts/robots.txt，讓搜尋引擎知道哪些資料夾、網站內容，是我們想要被檢索、搜尋的：
```
User-agent: *
Disallow: 
```
(上例為允許任何搜尋引擎檢索網站的所有內容與資源，包括頁面、圖片)

關於 robots.txt 詳細設置方式可以往這或這參考。

### 小結
* 在每篇文章中設置 Title、Keywords、Description
* 建立社群平台對應的 partials template，讀取相關參數，放在全局 <head> 中
* 承上，設置完整的 meta tags，有助於網址分享時的效果呈現
* 提交 Sitemap.xml，讓網站頁面可以被 google 索引，被使用者搜尋到
* 整合 Google Analytics，透過工具掌握頁面被搜尋到之後，網站被訪問的實際情況
* 設置 robots.txt，定義哪些內容不想被搜尋檢索
    
今天超級淺的聊了一下 Hugo 在做 SEO 時提供的相關工具，讓沒接觸過的人，踏出了解做 SEO 的第一步，還有很多關於搜尋最佳化的作法、內容與學問可以探討，有興趣的讀者，推薦可以看看這篇 [PERFECT SEO META TAGS WITH HUGO](https://www.skcript.com/svr/perfect-seo-meta-tags-with-hugo/)，也希望有深耕過 SEO 經驗的讀者，能把你的心得做個分享留言，感謝。

最後，筆者有個心得是，在開始研究 SEO 的這條路上，跟很多學問一樣，它是需要你不斷地更新資訊的，不是說感覺一時學有所成，就能十年不變的一套用到底，推薦你可以搜尋「SEO Checklist 2020」，或許可以有所獲得。

## 參考連結
[參考連結](https://ithelp.ithome.com.tw/users/20106430/ironman/3613)
