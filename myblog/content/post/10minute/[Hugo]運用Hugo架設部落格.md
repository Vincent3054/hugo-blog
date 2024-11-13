---
title: "[Hugo]運用Hugo架設部落格"
keywords :
- 10minute
- Hugo
- website
- personal
- github page
- side project
- blog
- 自架部落格
- 建立部落格
- 無廣告部落格
- 部落格
description : "[十分鐘系列]運用Hugo在GitHub Page架設部落格"
author : "Sky Chen"
slug: hugo-github-page-blog
categories:
- 10minute
- Hugo
date: "2023-02-15"
tags : ["10minute","Hugo"]

coverSize: partial
coverImage: images/content/notes0001.jpg
thumbnailImage: images/content/notes0001.jpg
---
<!--more-->

# [Hugo]運用Hugo架設部落格
tags: `10minute` `Hugo`

{{< toc >}}

## Hugo
### Hugo是什麼?

![]( /images/content/20230224001.png)

Hugo是一個由Go語言實現的靜態網站生成器，它可以讓你在短時間內從無到有架設一個網站。

Hugo有以下幾個特點：

* 速度：Hugo是目前被稱為**最快的網站生成器**，它可以在毫秒內建立數千個頁面
* 簡單：Hugo**不需要資料庫或伺服器**，只要一個二進制文件就可以搞定
* 功能：Hugo支援**Markdown語法**和**各種主題**
，讓你可以輕鬆地撰寫和美化你的內容
* 彈性：Hugo可以**自動產生Sitemap和RSS**，並且提供許多自定義選項和擴展功能
* 免費：Hugo是**開源**的軟件，你可以自由地使用和修改它

### Step1. 安裝Hugo

如果你是使用 Windows 可透過 [chocolatey](https://chocolatey.org/install) 安裝 Hugo：

按下 Win鍵 + r 啟動「執行」對話框。輸入 powershell 後按 Enter 鍵即可啟動.NET Framework 版本的 **PowerShell**，按照順序在終端機輸入以下指令。

```sql=
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```

```sql=
choco install hugo -confirm
```

安裝完成後，在終端機執行以下指令，若成功輸出版本資訊，表示安裝完成：

```sql=
hugo version
```

#### 補充連結
[Hugo官方網站](https://gohugo.io/)

[PowerShell介紹](https://opensourcedoc.com/windows-programming/powershell/)

### Step2. 建立新專案

在你安裝完 Hugo 指令後，可透過以下指令建置新專案：
```sql
hugo new site myblog
```
結果如下：

![]( /images/content/20230224003.png)

cd 進入到目錄中我們可以看到最初的專案資料夾有以下這幾個：

![]( /images/content/20230224004.png)

#### 補充連結
[Hugo官方文件介紹](https://gohugo.io/getting-started/quick-start/)

#### 常見BUG
如果遇到以下錯誤
```sql=
Error: "D:\github\myblog\config.toml:1:1": unmarshal failed: toml: key theme is already defined
```
請開啟config.toml，把多餘的null刪除

### Step3. 透過Git安裝佈景主題

根據官網指引安裝佈景，在安裝前你必須先有 git，若你還沒有 GitCLI，需先安裝 [git](https://git-scm.com/downloads)。

```sql=
# 在專案目錄底下 ./myblog
git init
git submodule add https://github.com/kakawait/hugo-tranquilpeak-theme.git themes/tranquilpeak
```
編輯 config.toml **指定佈景名稱為 hugo-tranquilpeak-theme**

```sql=
//也可手動開啟檔案修改
echo 'theme = "tranquilpeak"' >> config.toml
```
為了在本地跑起來時可以看到點內容，我們先新增一篇文章

```sql=
hugo new posts/my-first-post.md
```
檔案會被建立在 ```./content/posts/my-first-post.md``` 底下。請注意，省略 ```.md``` 的話，你的文件就不會被渲染到頁面上。
執行以下指令，在本地運行 hugo 專案：

```sql=
hugo server -D
```
訪問 http://localhost:1313/  網站就可以成功在本地跑起來了!

![]( /images/content/20230224005.png)

#### 補充
[Git 安裝教學](https://w3c.hexschool.com/git/3f9497cd)

[tranquilpeak佈景主題詳細設定官方文件](https://github.com/kakawait/hugo-tranquilpeak-theme/blob/master/docs/user.md)

[Hugo布景主題下載](https://themes.gohugo.io/tags/blog/)

#### 常見BUG
如果遇到布景buid的時候顯示error，不支援scss問題 請安裝以下hugo版本

```sql=
choco install hugo-extended
```

### Step4. 布景主題的相關設定

這篇文使用「Tranquilpeak」的佈景主題來建立部落格，「Tranquilpeak」 是一款在視覺佈局上很適用於個人部落格撰文的 Hugo Themes (個人感覺)，建議在選用佈景時閱讀一下官方文件、並去試著做以下這幾件事：

#### 1.改config配置

佈景提供了config設置範例 (有些作者會補充說明，註解在 config 裡面) 給大家參考，放在 exampleSite 中，建議可以先以這份 config 為基礎去改設置參數；

佈景本身也有提供 default 的 config，通常會放在該佈景第一層目錄底下，有個 theme.toml，要用哪一份開始設置就看個人。)
##### copy the example config.toml
你可以先複製他提供的範例配置，之後依需求改變部分設置參數，這樣就不用重頭到尾自己設定：

```sql=
cp themes/tranquilpeak/exampleSite/config.toml ./config.toml
```
##### config配置範例

```sql=
baseURL = "https://Vincent3054.github.io/" # 部署到線上之後要使用的主要域名 = FQDN 或GitPage URL
defaultContentLanguage = "zh-tw"           # 預設語系
title = "Blog"                             # 網站 title
theme = "tranquilpeak"                     # 指定使用的佈景 (與資料夾名稱一樣)
paginate = 7                               # 每頁顯示幾筆文章
canonifyurls = true                        # 設為 true 讓全站資源網址都套用 baseURL
```

如果希望文章內文也可以用HTML語法，可以新增這段配置**將unsafe設定成true**

```sql=
[markup.goldmark.parser]
      autoHeadingID = true
      autoHeadingIDType = 'github'
      wrapStandAloneImageWithinParagraph = true
      [markup.goldmark.parser.attribute]
        block = false
        title = true
    [markup.goldmark.renderer]
      hardWraps = false
      unsafe = true
      xhtml = false
```

#### 2.透過 demo 知道佈景可以做到哪些事

是的，佈景也是有他各自不同的工具，能提供你讓你方便做到不同的事情，你可以先逛逛 Tranquilpeak (或其他)佈景 online demo，這能讓你不用本地套用，就可以直接先看看套用後整體呈現的效果、網站的布局會長什麼樣子；

但不論你是使用哪種佈景，在配置上都萬變不離其宗 (若你喜歡的佈景做不到，但有看到別的佈景有，理論上自己也能仿照實作出來，不過門檻會稍微高一點)。

#### 補充
[Tranquilpeak官方文件](https://github.com/kakawait/)

### Step5. Hugo資料結構 

```sql=
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


### Step6. Hugo文章結構 

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

#### Hugo Content - Front Matter

在架設部落格時，想要趕快搞定網站基礎設施與寫文環境，那你就必須先配置好你的 config、文章模板 archetypes，以及規劃模板中的 Front Matter 了。

只要依據個人需求把 Front Matter 設置好，就能在每次 new post 翻印出新的文章檔案時，改一改幾個特定參數，就能開始動手寫，縮短「建立新檔 -> 寫文章」這段時間，今天就帶大家認識一下什麼是 Hugo Front Matter。

在每個文章檔案 .md 中，放在內容最前面那塊以 - - - 分隔的區塊內容，就是 Front Matter (- - - 只是其中一種格式)；Hugo 支援四種 Front Matter 格式：

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

### Step7. 部署推版至GitHub Pages

GitHub 是一個提供我們把本地 (簡言之就是自己的電腦) 檔案、程式碼、離離扣扣的東西，透過```git```版本控制，將檔案推到遠端 (簡言之就是別人的電腦) 委託給 GitHub 保管的服務平台。

今天要介紹的內容主要包括 GitHub 註冊、把網站放 (部署) 到 GitHub Pages 上、一點點的 git 操作，一點點的版本控制指令等，對於沒有使用過 ```git```，甚至是對程式碼、版本控制這些東西都很陌生的人，建議可以先 [google 一輪](https://backlog.com/git-tutorial/tw/reference/basic.html)，有個概念，最重要的是，為你的電腦安裝好[Git CLI](https://git-scm.com/book/zh-tw/v2/%E9%96%8B%E5%A7%8B-Git-%E5%AE%89%E8%A3%9D%E6%95%99%E5%AD%B8)。

#### 註冊 GitHub 帳號

到官網註冊 https://github.com/

![]( /images/content/20230224006.jpg)

順帶一提，若之後沒有想要特別買網址，這邊的 username 會是網站網址的一部分 (GitHub Pages 默認)，但若是不 care 網址長怎樣，建議使用自己習慣的「常用帳號」作為 username。

#### 建立一個 GitHub Repository

* 註冊完成之後，轉跳到這個畫面，請點右上角的 ＋：

![]( /images/content/20230224007.jpg)

* 按下 New repository，建立一個新的資源庫

![]( /images/content/20230224008.jpg)

* 請注意，Repository name 一定要填入 your-username.github.io，以筆者自己為例，我的 username 是 littlebookboy，則建立資源庫名稱就要使用 littlebookboy.github.io，這是 GitHub Pages 的機制；填寫完必要資訊，按下建立：

![]( /images/content/20230224009.jpg)

#### 部署到 GitHub Pages

以下說明會以筆者的 Repository 為例。

* cd 到 Hugo 專案底下，執行 hugo 指令，打包你的 Hugo Site：

![]( /images/content/20230224010.jpg)

若是要連同草稿、未來發布等文章一併打包，請下配合的參數，例如 hugo -D。

* 複製剛剛建立好的 Repository URL，位置在：

![]( /images/content/20230224011.jpg)

* 執行 git remote 註冊，註冊好遠端地址後，可下 git remote -v 列出看看：

![]( /images/content/20230224012.jpg)

* 將目前異動提交成一個 commit：

![]( /images/content/20230224013.jpg)

* 提交完成後，下 git push：

![]( /images/content/20230224014.jpg)

#### 整個指令執行過程

```sql=
# 獲取 Repository URL，例如 git@github.com:littlebookboy/littlebookboy.github.io.git

# 進入到專案底下，打包你的網站，生成 public 資料夾
$ cd your-site/
$ hugo

# 執行遠端資源庫地址註冊
$ git init

# your-username請自行修改成自己GitHub的帳號名稱
$ git remote add origin https://github.com/your-username/your-username.github.io.git

# 確認遠端資源庫地址註冊成功
$ git remote -v

# 將目前異動提交成一個 commit
$ git add .
$ git commit -m 'initial site'
$ git branch -M main

# 推送 commit
$ git push or $ git push -u origin main
```

#### 瀏覽結果

此時你可以開啟 https://your-username.github.io 瀏覽看看網站是否已經部署成功，理論上不會等太久，就可以看到頁面了。
https://your-username.github.io

![]( /images/content/20230224002.png)

## 補充

[Hugo SEO 搜尋引擎最佳化](https://vincent3054.github.io/10minute/hugo-website-seo-guide/)

[Hugo Comments 互動式留言板](https://vincent3054.github.io/10minute/hugo-comment-board-disqus-gitalkw/)  

## 來源連結
[原文](https://ithelp.ithome.com.tw/users/20106430/ironman/3613)

[ChatGPT](https://openai.com/blog/chatgpt/)
