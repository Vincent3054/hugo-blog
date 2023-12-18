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
Visual Studio 自稱是地表最強開發工具，會這樣自稱也不是浪得虛名，Visual Studio 2022有很多新的、好的功能，但這些功能預設是沒有開啟的，需要經過調整和開啟才能啟用。

已下介紹的功能，不限於社群、Professional、Enterprise都可以使用。

## 更新Visual Studio
更新VS至17.X版本以上
![121401](https://hackmd.io/_uploads/B1Q0YxdUp.png)

## 移除安裝 Visual Studio
2017以前的VS，因為跟OS有關係，如果壞掉嚴重的話可能需要重灌系統。
2017以後有VS Installe，如果壞掉直接重裝就可以了。
(設定會自動和登入的帳號同步，不用擔心重設)
![image](https://hackmd.io/_uploads/HJQPqe_8T.png)

## What’s New (新增功能)
剛更新完之後會跳出What’s New (新增功能)導覽頁面介紹新功能，圖文並茂非常詳細。
![image](https://hackmd.io/_uploads/ByWNildIT.png)
如果關閉後想要再去查看可以點選 說明>新增功能 即可開啟。
![image](https://hackmd.io/_uploads/HJuBoxOL6.png)

## 支援Markdown preview
現在有支援Markdown preview了
點選 右鍵>顯示Markdown預覽即可開啟預覽模式
![image](https://hackmd.io/_uploads/SJqasxO8T.png)

## 搜尋方式加入了 All in one search
  - `ctrl+T`: 搜程式
    - 點取預覽頁面可跳轉至程式碼
  - `ctrl+Q`: 搜設定名稱
    - 點取後跳至設定頁面
  - 預覽功能，需另外開啟，需重啟 VS
    - ![image](https://hackmd.io/_uploads/S141MjMLa.png)

## Brace pair color 成對大括弧顏色標示
![image](https://hackmd.io/_uploads/Bk_rNwY8T.png)
- 選項>文字編輯器>一般>顯示>啟用成對大括弧顏色標示
    - ![image](https://hackmd.io/_uploads/SJ4hNPKIp.png)

## View Zero-Width characters 顯示零寬度字元
![image](https://hackmd.io/_uploads/HkwbSPFLT.png)
![image](https://hackmd.io/_uploads/BkxMHwFIp.png)
- 選項>文字編輯器>一般>顯示>顯示零寬自原
![image](https://hackmd.io/_uploads/HkTrBPtU6.png)

## 索引標籤視窗相關(TAB)
- 清單靠左、靠右、置頂顯示
- 清單依「專案」上色
    - ![image](https://hackmd.io/_uploads/rkKZHsGLa.png)
- 清單依「規則」上色
    - ![image](https://hackmd.io/_uploads/SyJhLDF8p.png)
    - 選擇「設定規則運算式」，用正則表達式寫入規則。
```
^.*Controller.cs$
^.*Service.cs$
^.*Repository.cs$
^.*\.cshtml$
^.*\.js$
^.*\.(json|editorconfig|config)$
```
- `ctrl+tab` 顯示開啟檔案清單來切換
  
## Sticky scroll 自黏捲動

會把程式括號範圍開頭自動置頂，如 namespace、class、function、using、宣告變數後面的大括號

- 選項>文字編輯器>一般>顯示>自黏捲動
    - ![image](https://hackmd.io/_uploads/rJwT4tKLa.png)
    - ![](https://learn.microsoft.com/en-us/visualstudio/ide/media/vs-2022/sticky-scroll-example-csharp.gif?view=vs-2022)

## 比較檔案差異
方案總管>檔案右鍵>相對於...
![image](https://hackmd.io/_uploads/H1KbPFYLa.png)

![image](https://hackmd.io/_uploads/SknMwFtUp.png)

## 程式碼清除規則
 移除沒用的using、排序 import、排版程式…
 - 用快捷鍵執行清除(Contol+K 之後按 Contol+E)
  - ![image](https://hackmd.io/_uploads/B1oeOoM8a.png)
  - 可以設定存檔時自動執行清除
    - ![image](https://hackmd.io/_uploads/SkIddsG8p.png)
  - 可以對整個方案執行清除
    - ![image](https://hackmd.io/_uploads/rJi5doGUa.png)
  - 使用 .editorconfig 建立團隊的 coding style
    - ![image](https://hackmd.io/_uploads/ry0xnKtU6.png)

## Github Example alt+O
游標指到類別上，執行此功能後會搜尋github上的範例程式碼
![image](https://hackmd.io/_uploads/ryy-HV68a.png)


## Dev Tunnel: 讓使用者連到開發機測試
![image](https://hackmd.io/_uploads/HyYwv4TUp.png)

![image](https://hackmd.io/_uploads/SyLav4a8T.png)
* 只有支援網頁程式
* 可設定存取權限: 私人、同組織、公開
* 有一些限制
* [詳細介紹](https://learn.microsoft.com/zh-tw/connectors/custom-connectors/port-tunneling)