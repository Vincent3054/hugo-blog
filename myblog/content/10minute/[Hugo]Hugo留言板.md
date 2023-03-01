---
title: "[Hugo]如何在Hugo上使用Disqus或Gitalk創建一個互動式留言板"
keywords :
- Hugo
- Disqus
- Gitalk
- message board
- Comments
- web2.0
description : "用Hugo打造一個完美的留言板，從安裝到配置的全程指南"
author : "Sky Chen"
slug: hugo-comment-board-disqus-gitalkW
tags : ["10minute","Hugo"]
categories:
- Hugo
date: "2023-03-01"
toc : true
coverSize: partial
coverImage: images/notes0004.jpg
thumbnailImage: images/notes0004.jpg
---
<!--more-->

# 如何在Hugo上使用Disqus或Gitalk創建一個互動式留言板
tags: `Hugo`

{{< toc >}}


## 互動式留言板
當讀者對你的部落格內容有問題，想發問交流時，勢必需要留言溝通的工具，此類工具通常稱為 Comments System (評論系統)，常見的有：[Disqus](https://disqus.com/)、[Facebook comments](https://developers.facebook.com/docs/plugins/comments/)、GitHub issue (Gitalk)、Livefyre 等。

Hugo 具有追加整合 Comments 服務的彈性，讓我們可以輕鬆地將此類工具，放在任何頁面中，本篇會介紹 Disqus 評論系統的整合方式。

### Disqus是什麼?

![]( /images/20230301001.png)

Disqus是專門針對部落格、網站留言機制做整合服務的平台，供瀏覽網站的訪客可以針對文章進行留言。它有以下幾個特點：
* 它被全球**191個國家的數百萬個出版商使用**，它可以讓你的博客接觸到更廣泛的讀者和促進更多的互動。
* 它**支持多種語言和社交媒體登錄**，它可以讓你的讀者更方便地發表和管理自己的評論。
* 它提供了一個**討論編輯器**，它可以讓你一鍵更新任何討論主題的屬性，例如標題或鏈接。
* 它提供了一個API，它可以讓你**自定義評論系統的外觀和功能**。

### Gitalk是什麼?

![]( /images/20230301002.png)

Gitalk是一個基於github issue和preact開發的評論組件，它可以讓你在靜態網頁裡面新增留言區。它有以下幾個特點：
* 它**使用github issue來存儲和管理評論**，它可以讓你方便地追蹤和回覆評論，而且不需要額外的數據庫。
* 它**支持markdown語法**，它可以讓你的讀者更靈活地表達自己的想法。
* 它提供了一個proxy，它可以**解決github api的跨域問題**。
* 它提供了一個API，它可以讓你**自定義評論組件的外觀和功能**。

### Disqus VS Gitalk
disqus和gitalk都是基於github issue的評論組件，但它們有以下幾個不同點：

* disqus是一個**第三方服務**，它可以讓你在多個平台上使用同一個評論系統，而且有更多的功能和選項。但它也有一些缺點，例如**廣告、隱私問題、加載速度**等。
* gitalk是一個**開源項目**，它可以讓你完全控制自己的評論數據，而且更適合靜態網頁。但它也有一些缺點，例如需要**用戶登錄github、需要手動初始化issue、可能遇到跨域問題**等。

### 如何在hugo上使用Disqus?

按照官網介紹，Hugo 已經幫你內建了一套評論系統：Disqus，以下是啟用的文字版說明，後面會在依照流程附上圖片給大家參考：

* 未有 Disqus 帳號，請先[註冊](https://disqus.com/profile/signup/)
* 已有 Disqus 帳號，請按 GET STARTED
* 點擊 ```I want to install Disqus on my site.``` [頁面在此可快速前往](https://disqus.com/profile/signup/intent/)
* 填入網站資訊：
  * 網站名稱 (Web Site Name)
  * 網站種類 (Category)
  * 按下 Create  

* 進入 Disqus Install 環節：
  * 選擇整合平台：頁面跳到 Select Platform，但因為官方沒有 Hugo 的選項，請拉到最下面選```I don't see my platform listed, install manually with Universal Code```
  * 配置整合程式碼：接著 Select Platform 之後，頁面跳到``` Universal Code ```頁面，在這一步要看使用者選用的佈景，有沒有整合好 Disqus 到你的 layout 中
    * 已有整合：可跳過 ```Universal Code``` 這部分
    * 尚未整合：
      * 若你不想換佈景，請參考 [Partial Templates](https://gohugo.io/templates/partials/#disqus) 的配置說明，自己動手整合
      * 若你想換佈景，筆者試過用 ananke 以及 tranquilpeak 兩個佈景，都有整合 Disqus
  * 此步驟以「已有整合」為例，在 ```Universal Code``` 頁面拉到最下面按 ```Configure```
  * 配置你的 ```Disqus Configure```
    * 網站名稱 Website Name
    * 網站網址 Website URL 請配置上線後的公開網址，子域名就是你的 ```disqusShortname```
    * 網站種類 Category
    * 顯示語系 Language 評論系統介面要顯示的語系  

  * 配置好後，按下 Complete Setup
  * 接著 Disqus 會問你要不要設置 Community，這邊先不用，拉到最下面按 ```Dismiss Setup```
  * 完成

#### Hugo 配置
假設你的 Website URL 為 https://littlebookboy.website.com，則 config.toml 配置就會是

```sql=
disqusShortname = "littlebookboy"
```
本地執行結果，以 tranquilpeak 為例：

![]( /images/20230301003.png)

線上執行結果 (丟到公開頁面後，評論系統介面才會被渲染成功)：

![]( /images/20230301004.png)


#### 附圖說明
未有 Disqus 帳號，請先到官網註冊，請按 GET STARTED：

![]( /images/20230301005.png)

![]( /images/20230301006.png)

選擇你偏好的註冊方式，完成註冊，頁面會跳轉回首頁，請按 GET STARTED，選擇 ```I want to install Disqus on my site```：

![]( /images/20230301007.png)

建立新站，填入網站資訊，按下 Create：

![]( /images/20230301008.png)

選擇整合平台，請拉到最下面選 ```I don't see my platform listed, install manually with Universal Code```：

![]( /images/20230301009.png)

![]( /images/20230301010.png)

在 ```Universal Code``` 頁面拉到最下面按 ```Configure```：

![]( /images/20230301011.png)

配置完整的網站資訊，

![]( /images/20230301012.png)

> 請注意，這邊的 Website URL 子域名會作為 hugo 配置參數 disqusShortname 被使用到，網址結構為： https://yourDisqusShortName.website.com

完成配置後，拉到最下面，按下 Dismiss Setup 跳過配置 Community：

![]( /images/20230301013.png)

建站完成後，會跳到這個頁面：

![]( /images/20230301014.png)

### 如何在hugo上使用Gitalk?

#### 申請GitHub Oauth App
需要GitHub應用，如果沒有[點擊這裡申請](https://github.com/settings/applications/new)，授權回調URL填寫當使用插件頁面的域名稱。

以本站為例，必須填寫以下內容：

| 欄位 | 內容 | 備註 |
| -------- | -------- | -------- |
| Application name| gittalk for blog| 填寫應用名稱|
| Homepage URL| https://vincent3054.github.io/| 主頁地址|
| Application description| blog留言板插件gtalk| 備註|
| Authorization callback URL| https://vincent3054.github.io/| 回調地址|

![]( /images/20230301015.png)

#### 創建範本
在主題目錄下，新建範本，如 themes/mainload/layouts/partials/gitalk.html

```javascript
{{ if .Site.Params.enableGitalk }}
<div id="gitalk-container"></div>
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/gitalk@1/dist/gitalk.css">
<script src="https://cdn.jsdelivr.net/npm/gitalk@1/dist/gitalk.min.js"></script>
<script>
  const gitalk = new Gitalk({
    clientID: '{{ .Site.Params.Gitalk.clientID }}',
    clientSecret: '{{ .Site.Params.Gitalk.clientSecret }}',
    repo: '{{ .Site.Params.Gitalk.repo }}',
    owner: '{{ .Site.Params.Gitalk.owner }}',
    admin: ['{{ .Site.Params.Gitalk.owner }}'],
    id: location.pathname, // Ensure uniqueness and length less than 50
    distractionFreeMode: false // Facebook-like distraction free mode
  });
  (function() {
    if (["localhost", "127.0.0.1"].indexOf(window.location.hostname) != -1) {
      document.getElementById('gitalk-container').innerHTML = 'Gitalk comments not available by default when the website is previewed locally.';
      return;
    }
    gitalk.render('gitalk-container');
  })();
</script>
{{ end }}
```
修改主題模板layouts/_default/single.html，在{{ partial “comment.html” . }}的下一行，新增以下内容:

```javascript
{{ partial "gitalk.html" . }}
```

#### 新增配置
需要修改config.toml配置，注意repo新增自己的版本庫地址，一般是username.github.io，clientID、clientSecret位置詳見下圖:

![]( /images/20230301016.png)

```sql
[Params]
  enableGitalk = true

[Params.Gitalk]
    clientID = "xxx" # Your client ID
    clientSecret = "xxx" # Your client secret
    repo = "xbc.me" # The repo to store comments
    owner = "geekwho11" # Your GitHub ID
    admin= "geekwho11" # Required. Github repository owner and collaborators. (Users who having write access to this repository)
    id= "location.pathname" # The unique id of the page.
    labels= "gitalk" # Github issue labels. If you used to use Gitment, you can change it
    perPage= 15 # Pagination size, with maximum 100.
    pagerDirection= "last" # Comment sorting direction, available values are 'last' and 'first'.
    createIssueManually= false # If it is 'false', it is auto to make a Github issue when the administrators login.
    distractionFreeMode= false # Enable hot key (cmd|ctrl + enter) submit comment.
```
如果使用「Tranquilpeak」佈景主題，直接修改config.toml原註解內容即可。

```sql
  # --------------
  # Comment system
  # --------------
  [params.comment]
    [params.comment.disqus]
      enable = false
      shortname = "hugo-tranquilpeak-theme"
    [params.comment.gitalk]
      enable = true
      clientId = "13axxxxxxxxxxxxxaae5"
      clientSecret = "a205de00xxxxxxxxxxxxxxxx9255f"
      owner = "vincent3054"
      repo = "vincent3054.github.io"
      # See all options: https://github.com/gitalk/gitalk#options
      [params.comment.gitalk.options]
        language = "zh-tw"
        perPage = 10
        distractionFreeMode = false
        enableHotKey = true
        pagerDirection = "first"
```
線上執行結果 (丟到公開頁面後，評論系統介面才會被渲染成功)：

![]( /images/20230301017.png)

## 結論
在本文中，我介紹了如何在hugo上使用disqus或gitalk創建一個互動式留言板。這兩種評論系統各有優缺點，適合不同的需求和偏好。無論你選擇哪一種，都可以讓你的博客更加生動和有趣，增加與讀者之間的交流和互動。希望這篇文章對你有所幫助，歡迎留言分享你的看法和經驗。

## 參考連結
[ChatGPT](https://openai.com/blog/chatgpt/)  

[Disqus原文連結](https://ithelp.ithome.com.tw/articles/10248312)

[Gitalk原文連結](https://xbc.me/add-gittalk-to-hugo/)