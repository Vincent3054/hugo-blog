---
categories:
- Notes
- AI
date: "2023-02-17"
title: "五分鐘串接ChatAI至LineBot"
tags : ["AI"]
coverSize: partial
coverImage: images/notes0002.jpg
thumbnailImage: images/notes0002.jpg
---
<!--more-->
# 五分鐘串接ChatAI至LineBot
###### tags: `AI`

## Chat GPT簡介
ChatGPT 是由 OpenAI 開發的自然語言處理（**NLP**)模型「GPT-3」延伸出的「**GPT-3.5**」製作的，基於 人類反饋強化學習(**RLH**F) 進行訓練，簡單來說就是人類提問機器答、機器提問人類答，並且不斷迭代，再排除掉不健康的答案，透過**人類干預以增強機器學習的效果**，獲得更為逼真的結果。

![]( /images/20230217001.png)

ChatGPT 二個月內，已經吸引超過1億人使用，而 ChatGPT 功能強大，從客服對話、故事創作、翻譯、修改文法、寫詩、歌詞、文字整理，甚至是寫程式都可以。

### GPT-3 VS GPT-3.5
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

## OpenAI
OpenAI 是美國一個人工智慧（AI）研究實驗室，創始人為**伊隆·馬斯克**（沒錯就是特斯拉那位）以及山姆·柯曼，原先為一個非營利組織，其使命是創造通用人工智能（英文：Artificial General Intelligence，簡稱 AGI），促進和發展友好的人工智慧，使人類整體受益，後來因為營運的成本所成立一個子公司營利組織 OpenAI LP。
**OpenAI 每一年都會陸續推出自己所研發出的成果，從 GPT-1 到 GPT-3.5 都是他們所創造的成品**。

> OpenAI 官方網站
https://openai.com/

# GPT AI Assistant

GPT AI Assistant 是基於 OpenAI API 與 LINE Messaging API 實作的範例應用程式，透過安裝步驟，你可以使用 LINE 手機應用程式與你專屬的 AI 助理聊天。

## 範例
![](https://github.com/Vincent3054/gpt-ai-assistant/blob/main/demo/screenshot-1.png?raw=true =50%x)

![](https://github.com/Vincent3054/gpt-ai-assistant/blob/main/demo/screenshot-2.png?raw=true =50%x)


## 安裝步驟

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

## 更新程式

進到自己的 `gpt-ai-assistant` 專案頁面，點選「Sync fork」選單，再點選「Update branch」或「Discard commit」按鈕，以同步最新的程式碼到自己的儲存庫。

![](https://github.com/Vincent3054/gpt-ai-assistant/blob/main/demo/github-sync-fork.png?raw=true =50%x)

## 環境變數

在 Vercel 平台上新增或修改環境變數，以變更程式設定。

名字 | 說明
--- | ---
`APP_DEBUG` | 決定是否印出訊息，可設置為 `true` 或 `false`
`OPENAI_API_KEY` | OpenAI 的 API key
`OPENAI_COMPLETION_INIT_LANG` | 決定初始語言，可設置為 `zh` 或 `en`
`OPENAI_COMPLETION_MODEL` | 參見 [model](https://beta.openai.com/docs/api-reference/completions/create#completions/create-model) 說明
`OPENAI_COMPLETION_TEMPERATURE` | 參見 [temperature](https://beta.openai.com/docs/api-reference/completions/create#completions/create-temperature) 說明
`OPENAI_COMPLETION_MAX_TOKENS` | 參見 [max_tokens](https://beta.openai.com/docs/api-reference/completions/create#completions/create-max_tokens) 說明
`OPENAI_COMPLETION_FREQUENCY_PENALTY` | 參見 [frequency_penalty](https://beta.openai.com/docs/api-reference/completions/create#completions/create-frequency_penalty) 說明
`OPENAI_COMPLETION_PRESENCE_PENALTY` | 參見 [presence_penalty](https://beta.openai.com/docs/api-reference/completions/create#completions/create-presence_penalty) 說明
`LINE_API_KEY` | LINE 的 channel access token
`LINE_API_SECRET` | LINE 的 channel secret

點選「Redeploy」按鈕，以重新部署。
![](https://github.com/Vincent3054/gpt-ai-assistant/blob/main/demo/vercel-redeploy.png?raw=true =50%x)

## 除錯

首先，在 Vercel 平台上檢查專案的環境變數是否填寫正確。

![](https://github.com/Vincent3054/gpt-ai-assistant/blob/main/demo/vercel-environments.png?raw=true =50%x)

如果有變更，點選「Redeploy」按鈕，以重新部署。

![](https://github.com/Vincent3054/gpt-ai-assistant/blob/main/demo/vercel-redeploy.png?raw=true =50%x)

進一步的除錯方式是，在專案首頁點選「View Function Logs」按鈕。

![](https://github.com/Vincent3054/gpt-ai-assistant/blob/main/demo/vercel-view-logs.png?raw=true =50%x)

查看應用程式的錯誤訊息。

![](https://github.com/Vincent3054/gpt-ai-assistant/blob/main/demo/vercel-logs.png?raw=true =50%x)

如果還是無法解決，請到「[Issues](https://github.com/memochou1993/gpt-ai-assistant/issues)」頁面，點選「New issue」按鈕，描述你的問題，並附上螢幕截圖。

## 功能建議

請到「[Issues](https://github.com/memochou1993/gpt-ai-assistant/issues)」頁面，點選「New issue」按鈕，描述你的功能建議。

## 開發

下載專案。

```bash
git@github.com:memochou1993/gpt-ai-assistant.git
```

進到專案目錄。

```bash
cd gpt-ai-assistant
```

安裝依賴套件。

```bash
npm ci
```

建立 `.env` 檔。

```bash
cp .env.example .env
```

設置環境變數如下：

```env
APP_ENV=local
APP_DEBUG=true
APP_URL=
APP_PORT=3000

OPENAI_API_KEY=<your_openai_api_key>
OPENAI_COMPLETION_INIT_LANG=
OPENAI_COMPLETION_MODEL=
OPENAI_COMPLETION_TEMPERATURE=
OPENAI_COMPLETION_MAX_TOKENS=
OPENAI_COMPLETION_FREQUENCY_PENALTY=
OPENAI_COMPLETION_PRESENCE_PENALTY=

LINE_API_KEY=<your_channel_access_token>
LINE_API_SECRET=<your_channel_secret>
```

### 測試

在終端機使用以下指令，運行測試，向 OpenAI 伺服器發送請求。

```bash
npm run test
```

查看結果。

```bash
> gpt-ai-assistant@1.0.0 test
> jest

  console.info
    === 000000 ===
    
    AI: 嗨！我可以怎麼幫助你？
    Human: 嗨？
    AI: 你好！有什麼可以幫助你的嗎？

      at Assistant.info [as debug] (assistant/assistant.js:55:28)

 PASS  assistant/index.test.js
  ✓ assistant works (1689 ms)

Test Suites: 1 passed, 1 total
Tests:       1 passed, 1 total
Snapshots:   0 total
Time:        2.579 s, estimated 4 s
Ran all test suites.
```

### 反向代理

修改環境變數如下：

```env
APP_ENV=production
```

在終端機使用以下指令，啟動一個 Local 伺服器。

```bash
npm run dev
```

在另一個終端機使用以下指令，啟動一個 Proxy 伺服器。

```bash
ngrok http 3000
```

回到 Line 平台，修改「Webhook URL」，例如「<https://0000-0000-0000.jp.ngrok.io>」，點選「Update」按鈕。

使用 LINE 手機應用程式發送訊息。

查看結果。

```bash
> gpt-ai-assistant@1.0.0 dev
> node api/index.js

=== 0x1234 ===

AI: 哈囉！
Human: 嗨？
AI: 很高興見到你！有什麼可以為你服務的嗎？
```

### 模擬請求

在終端機使用以下指令，啟動一個 Local 伺服器。

```bash
npm run dev
```

在另一個終端機使用以下指令，模擬 LINE 伺服器向 Local 伺服器發送請求，再由 Local 伺服器向 OpenAI 伺服器發送請求。

```bash
curl --request POST \
  --url http://localhost:3000/webhook \
  --header 'Content-Type: application/json' \
  --data '{
    "events": [
      {
        "type": "message",
        "source": {
          "type": "user",
          "userId": "000000"
        },
        "message": {
            "type": "text",
            "text": "我是誰"
          }
        }
      ]
    }'
```

查看結果。

```bash
> gpt-ai-assistant@1.0.0 dev
> node api/index.js

=== 000000 ===

AI: 嗨！我可以怎麼幫助你？
Human: 我是誰？
AI: 你是一個人，一個有意識的生物！
```

## 相關專案

- [line-bot-node](https://github.com/memochou1993/line-bot-node)
- [openai-cli-node](https://github.com/memochou1993/openai-cli-node)

## 貢獻者

https://github.com/memochou1993/gpt-ai-assistant/graphs/contributors

## 授權條款

[MIT](LICENSE)
