---
title: "[AI]串接OpenAI到LineBot，建立屬於自己的AI助理"
keywords :
- AI
- LineBot
- ChatAI
- Chat
- ChatGPT
- BOT
- ChatBot
- 10minute
- OpenAI
description : "[十分鐘系列]串接OpenAI到LineBot，建立屬於自己的AI助理"
author : "Sky Chen"
slug: openai-linebot-ai-assistant
categories:
- 10minute
- AI
date: "2023-02-17"
tags : ["AI","10minute"]
coverSize: partial
coverImage: images/notes0002.jpg
thumbnailImage: images/notes0002.jpg
---
<!--more-->

# [AI]串接OpenAI到LineBot，建立屬於自己的AI助理
###### tags: `10minute` `AI` 

## 目錄

## 內文

<h3 id="A">OpenAI是什麼?</h3>

OpenAI 是美國一個人工智慧（AI）研究實驗室，創始人為**伊隆·馬斯克**（沒錯就是特斯拉那位）以及山姆·柯曼，原先為一個非營利組織，其使命是創造通用人工智能（英文：Artificial General Intelligence，簡稱 AGI），促進和發展友好的人工智慧，使人類整體受益，後來因為營運的成本所成立一個子公司營利組織 OpenAI LP。
**OpenAI 每一年都會陸續推出自己所研發出的成果，從 GPT-1 到 GPT-3.5 都是他們所創造的成品**。

> OpenAI 官方網站
https://openai.com/

<h3 id="B">Chat GPT是什麼?</h3>

ChatGPT 是由 OpenAI 開發的自然語言處理（NLP)模型「GPT-3」延伸出的「GPT-3.5」製作的，基於 人類反饋強化學習(RLHF) 進行訓練，簡單來說就是**人類提問機器答、機器提問人類答，並且不斷迭代，再排除掉不健康的答案，透過人類干預以增強機器學習的效果**，獲得更為逼真的結果。

![]( /images/20230217001.png)

ChatGPT 二個月內，已經吸引超過1億人使用，而 ChatGPT 功能強大，從客服對話、故事創作、翻譯、修改文法、寫詩、歌詞、文字整理，甚至是寫程式都可以。

![]( /images/20230223001.png)

<h4 id="B1">GPT-3 VS GPT-3.5 </h4>

現在我們知道了 ChatGPT 是經過 GPT-3.5 訓練而來的，那到底 GPT-3 跟 GPT-3.5 又是什麼東西呢？
* GPT-3
生成型預訓練變換模型3（英語：Generative Pre-trained Transformer 3，簡稱 GPT-3）是一個自迴歸語言模型，基於**谷歌開發的語言模型**，模型訓練內容大部分來自網路，讓 ChatGPT 能夠相當自然地組織語句。
GPT-3 這個模型也是當前最大的語言處理模型之一，神經網路包含1750億個參數，為有史以來參數最多的神經網路模型。

> OpenAI 於2020年5月發表 GPT-3 的論文，微軟在2020年9月22日宣布取得了 GPT-3 的獨家授權。

* GPT-3.5
GPT-3.5 與 GPT-3 最大的差別在於 GPT-3 主要扮演一個蒐集資料的角色，較單純的使用網路上的資料進行訓練。
GPT-3.5 則是由 GPT-3 微調出來的版本，而其中 GPT-3.5 使用與 GPT-3 不同的訓練方式，所產生出來不同的模型，比起 GPT-3 來的更強大

* ChatGPT
而 ChatGPT 又是建立 GPT-3.5 之上，且更加上使用更完整的 人類反饋強化學習(RLHF) 去訓練。 (大致上可以想成 GPT-3 → GPT-3.5 → ChatGPT 啦)
也因此 ChatGPT 除了能夠準確理解問題，更能夠將對話一路記住和按此調整內容，其中包括承認錯誤、糾正錯處和拒絕不當要求等等較為複雜的互動內容，更符合道德要求的訓練方式，達到更接近真人的效果，這也是 GPT-3 所沒有的。

> 關於 GPT 各代的差異
https://www.techbang.com/posts/102473-openai-footprint-chatgpt

<h3 id="C">建立屬於自己的 GPT AI Assistant</h3>

GPT AI Assistant 是基於 **OpenAI API** 與 **LINE Messaging API** 實作的範例應用程式，透過安裝步驟，你可以使用 LINE 手機應用程式與你專屬的 AI 助理聊天。

#### 範例

{{< img src="/images/20230223002.png" width="50%" height="50%">}}

{{< img src="/images/20230223003.png" width="50%" height="50%" >}}

<h3 id="D"> Step1.申請帳號 </h3>

要能在10分鐘內快速安裝，首先要先準備以下帳號

* [OpenAI 平台帳號](https://beta.openai.com/signup)
* [LINE 官方帳號](href="https://lihi3.me/4UrSL")
* [GitHub 平台帳號](https://github.com/signup?ref_cta=Sign+up&ref_loc=header+logged+out&ref_page=%2F&source=header-home)
* [Vercel 平台帳號](https://vercel.com/signup)


<h3 id="E"> Step2.首先申請 OpenAI 帳號才能與LINE 官方帳號串接</h3>

申請好 OpenAI 帳號後，在 API Keys 建立一個 Secret key (要 copy 下來備用)

<h3 id="F"> Step3.登入 LINE 官方帳號 </h3>

* 新增一個提供者（Provider），例如「My Provider」。
* 在「My Provider」新增一個類型為「Messaging API」的頻道（Channel），例如「My AI Assistant」。
* 進到「My AI Assistant」頻道頁面，點選「Messaging API」頁籤，生成一個頻道的 channel access token。
![]( /images/20230223004.png)

<h3 id="G"> Step4.登入 GitHub 平台 </h3>

* 進到 gpt-ai-assistant 專案頁面。
* 點選「Star」按鈕，支持這個專案與開發者。
* 點選「Fork」按鈕，將原始碼複製到自己的儲存庫。

<h3 id="H"> Step5.登入 Vercel 平台</h3>

* 點選「Create a New Project」按鈕，建立一個新專案。
* 點選「Import」按鈕，將 gpt-ai-assistant 專案匯入。
* 點選「Environment Variables」頁籤，新增以下環境變數：
    * OPENAI_API_KEY：將值設置為 OpenAI 的 API key。
    ![]( /images/20230223005.png)
    * LINE_CHANNEL_ACCESS_TOKEN：將值設置為 LINE 的 channel access token。
    ![]( /images/20230223004.png)
    * LINE_CHANNEL_SECRET：將值設置為 LINE 的 channel secret。
    ![]( /images/20230223006.png)

* 點選「Deploy」按鈕，等待部署完成。
* 回到專案首頁，複製應用程式網址（Domains），例如「https://gpt-ai-assistant.vercel.app/」。

<h3 id="I"> Step6.回到 LINE 平台</h3>

* 進到「My AI Assistant」頻道頁面，點選「Messaging API」頁籤，設置「Webhook URL」，填入應用程式網址並加上「/webhook」路徑，例如「https://gpt-ai-assistant.vercel.app/webhook」，點選「Update」按鈕。
* 點選「Verify」按鈕，驗證是否呼叫成功。
* 將「Use webhook」功能開啟。
* 將「Auto-reply messages」功能關閉。
* 將「Greeting messages」功能關閉。
* 使用 LINE 手機應用程式掃描 QR code，加入好友。

```
- 登入 [OpenAI](https://beta.openai.com/) 平台，或註冊一個新的帳號。
  - 生成一個 OpenAI 的 [API key](/demo/openai-api-key.png)。
- 登入 [LINE](https://developers.line.biz/) 平台，或註冊一個新的帳號。
  - 新增一個提供者（Provider），例如「My Provider」。
  - 在「My Provider」新增一個類型為「Messaging API」的頻道（Channel），例如「My AI Assistant」。
  - 在「My AI Assistant」點選「Messaging API」頁籤，生成一個頻道的 [channel access token](/demo/line-api-key.png)。
- 登入 [GitHub](https://github.com/) 平台，或註冊一個新的帳號。
  - 進到 `gpt-ai-assistant` 專案頁面，點選「Star」按鈕，支持開發者開發有趣的專案。
  - 再點選「Fork」按鈕，將原始碼複製到自己的儲存庫。
- 登入 [Vercel](https://vercel.com/) 平台，或註冊一個新的帳號。
  - 點選「Create a New Project」按鈕，建立一個新專案。
  - 點選「Import」按鈕，將 `gpt-ai-assistant` 專案匯入。
  - 點選「Environment Variables」頁籤，新增以下環境變數：
    - `OPENAI_API_KEY`：將值設置為 OpenAI 的 [API key](/demo/openai-api-key.png)。
    - `LINE_API_KEY`：將值設置為 LINE 的 [channel access token](/demo/line-api-key.png)。
    - `LINE_API_SECRET`：將值設置為 LINE 的 [channel secret](/demo/line-api-secret.png)。
  - 點選「Deploy」按鈕，等待部署完成。
  - 點選「Domains」按鈕，複製應用程式網址，例如「<https://gpt-ai-assistant.vercel.app/>」。
- 回到 [LINE](https://developers.line.biz/) 平台。
  - 進到「My AI Assistant」頻道頁面，點選「Messaging API」頁籤，設置「Webhook URL」，例如「<https://gpt-ai-assistant.vercel.app/webhook>」，點選「Update」按鈕。
  - 點選「Verify」按鈕，驗證是否呼叫成功。
  - 將「Use webhook」功能打開。
  - 將「Auto-reply messages」功能關閉。
  - 將「Greeting messages」功能關閉。
  - 使用 LINE 手機應用程式掃描 QR code，加入好友。
- 開始與你專屬的 AI 助理聊天！
```

## 來源連結
[原文](https://www.liva.tw/make-your-line-oa-as-smart-as-chatgpt-in-10-minutes/)

[專案網址](https://github.com/memochou1993/gpt-ai-assistant/blob/main/README.md)

[ChatGPT](https://openai.com/blog/chatgpt/)