---
title: "[Other]Visual Studio 2022 開發工具大補帖"
keywords :
- Visual Studio 2022
- IDE
- VSCode
- 開發工具大補帖
description : "Visual Studio 2022 開發工具大補帖"
author : "Bruce Chen"
slug: VisualStudio2022
tags : ["Other","notes"]
categories:
- notes
- Other

date: "2023-12-18"

toc : true
coverSize: partial
coverImage: images/content/notes0020.jpg
thumbnailImage: images/content/notes0020.jpg
---
<!--more-->

# Visual Studio 2022 開發工具大補帖
tags: `Other` `notes`

{{< toc >}}
## 簡介
Visual Studio 自稱是地表最強開發工具，會這樣自稱也不是浪得虛名，Visual Studio 2022有很多新的、好的功能，但這些功能預設是沒有開啟的，需要經過調整和開啟才能啟用。

已下介紹的功能，不限於社群、Professional、Enterprise都可以使用。

## Visual Studio 2022 開發工具新功能設定
### 更新Visual Studio
更新VS至17.X版本以上
![]( /images/content/20231219001.png)

### 移除安裝 Visual Studio
2017以前的VS，因為跟OS有關係，如果壞掉嚴重的話可能需要重灌系統。
2017以後有VS Installe，如果壞掉直接重裝就可以了。
(設定會自動和登入的帳號同步，不用擔心重設)
![]( /images/content/20231219002.png)

### What’s New (新增功能)
剛更新完之後會跳出What’s New (新增功能)導覽頁面介紹新功能，圖文並茂非常詳細。
![]( /images/content/20231219003.png)
如果關閉後想要再去查看可以點選 說明>新增功能 即可開啟。
![]( /images/content/20231219004.png)

### 支援Markdown preview
現在有支援Markdown preview了
點選 右鍵>顯示Markdown預覽即可開啟預覽模式
![]( /images/content/20231219005.png)

### 搜尋方式加入了 All in one search
  - `ctrl+T`: 搜程式
    - 點取預覽頁面可跳轉至程式碼
  - `ctrl+Q`: 搜設定名稱
    - 點取後跳至設定頁面
  - 預覽功能，需另外開啟，需重啟 VS
    - ![]( /images/content/20231219006.png)


### Brace pair color 成對大括弧顏色標示
- 選項>文字編輯器>一般>顯示>啟用成對大括弧顏色標示
- ![]( /images/content/20231219008.png)

### View Zero-Width characters 顯示零寬度字元
- ![]( /images/content/20231219010.png)
- 選項>文字編輯器>一般>顯示>顯示零寬自原
![]( /images/content/20231219011.png)

### 索引標籤視窗相關(TAB)
- `Control+Tab` 顯示開啟檔案清單來切換
- 清單靠左、靠右、置頂顯示
- 清單依「專案」上色
    - ![]( /images/content/20231219012.png)
- 清單依「規則」上色
    - ![]( /images/content/20231219013.png)
    - 選擇「設定規則運算式」，用正則表達式寫入規則。
```
^.*Controller.cs$
^.*Service.cs$
^.*Repository.cs$
^.*\.cshtml$
^.*\.js$
^.*\.(json|editorconfig|config)$
```
  
### Sticky scroll 自黏捲動

會把程式括號範圍開頭自動置頂，如 namespace、class、function、using、宣告變數後面的大括號

- 選項>文字編輯器>一般>顯示>自黏捲動
    - ![]( /images/content/20231219014.png)
    - ![]( /images/content/20231219015.gif)

### 比較檔案差異
- 方案總管>檔案右鍵>相對於...
![]( /images/content/20231219016.png)

![]( /images/content/20231219017.png)

### 程式碼清除規則
 移除沒用的using、排序 import、排版程式…
  - 用快捷鍵執行清除(Contol+K 之後按 Contol+E)
  - ![]( /images/content/20231219018.png)
  - 可以設定存檔時自動執行清除
    - ![]( /images/content/20231219019.png)
  - 可以對整個方案執行清除
    - ![]( /images/content/20231219020.png)
  - 使用 .editorconfig 建立團隊的 coding style
    - ![]( /images/content/20231219021.png)

### Github Example alt+O
游標指到類別上，執行此功能後會搜尋github上的範例程式碼
![]( /images/content/20231219022.png)


### Dev Tunnel 讓使用者連到開發機測試
![]( /images/content/20231219023.png)

![]( /images/content/20231219024.png)
* 只有支援網頁程式
* 可設定存取權限: 私人、同組織、公開
* 有一些限制
* [詳細介紹](https://learn.microsoft.com/zh-tw/connectors/custom-connectors/port-tunneling)

## 使用 HttpRepl 來測試 Web API

- 新增http檔案
  - ![]( /images/content/20231219025.png)

```
### GET
GET https://www.google.com.tw/
Content-Type:application/json

### POST
POST https://alumni.nccu.edu.tw/cgi-bin/login
Content-Type:application/json

{
  "USERID": "ID",
  "PASSWD": "P@S$W0rd"
}

```