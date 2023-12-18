---
title: "[Azure]Azure Blob Storage介紹及案例"
keywords :
- Azure
- Blob
- Storage
- Azure Storage
description : "[Azure]Azure Blob Storage介紹及案例"
author : "Sky Chen"
slug: azure-blob-storage
tags : ["Azure","notes"]
categories:
- notes
- Azure

date: "2023-06-14"

toc : true
coverSize: partial
coverImage: images/content/notes0021.jpg
thumbnailImage: images/content/notes0021.jpg
---
<!--more-->

# Azure Blob Storage介紹及案例
tags: `Azure` `notes`

{{< toc >}}
## 介紹
Azure Blob Storage Service 為非結構(unstructured)儲存體服務。因為具有無限制規模、全球存取與不錯的成本效益等特性，非常適用於 PaaS，適用情境：大數據分析與IoT/感測器資料蒐集。 Blob 也常用於：
 - 透過瀏覽器存取圖片與文件
 - 提供分散存取使用
 - 串流影像與音樂
 - 資料備份、還原、災難還原與封存
 - 分析資料存放 (提供 Azure 上服務使用)

Blobs可以分成三種
| 名稱 | 說明 | 
| -------- | -------- | 
| Block Blobs     | 適合儲存文字與Binary資料，如文件與多美體檔案| 
| Append Blobs    | 與Block blobs相似，對於資料接續有最佳化，是用於logging情境     | 
| Page Block      | 有效率頻繁讀寫。VM的OS與data disk就是使用page blobs     | 

Blobs 有三種存取類型
| 名稱 | 說明 | 
| -------- | -------- | 
| Private     | 只有帳戶擁有者可以存取| 
| Append Blobs    | 公開存取，任何人皆可以存取| 
| Page Block      | Blob集合群組，Blob與Contariner訊皆可公開存取| 


> 一個帳戶可以有多個 Container，而一個 Container 可以有多個 Blob。 請注意， Container 的命名需要為小寫。

## 特點

1. 可靠性和可擴展性：Azure Blob Storage 提供高度可靠和可擴展的儲存解決方案。它能自動複製和備份數據，以確保數據的持久性和可用性。這使得它適用於處理大量數據和高頻的讀取和寫入操作。

1. 階層化存儲：Azure Blob Storage 提供多個存儲層級，包括熱存儲和冷存儲。熱存儲適用於經常被訪問的數據，它提供低延遲和高吞吐量的存取能力。冷存儲則適用於不經常被訪問的數據，它提供了更低的存儲成本，但可能會有稍高的讀取延遲。

1. 安全性：Azure Blob Storage 提供多層次的安全措施，保護存儲在其中的數據。它支援身份驗證和存取權限控制，可以設定細粒度的存取權限，以限制對數據的訪問。此外，Blob Storage 還提供數據的加密功能，以保護數據的機密性。

1. 擴展性和彈性：Azure Blob Storage 具有良好的擴展性和彈性，能夠應對不斷增長的數據需求。它支援自動擴展根據實際需求調整存儲容量和性能。這使得它適用於處理不同規模的工作負載，從小型應用到大型企業級應用程式。

1. 檔案層次結構：Blob Storage 使用容器和 Blob 的概念來組織和管理數據。容器類似於文件夾，用於分類和組織 Blob。Blob 則是實際的數據對象，可以是任何類型的文件。你可以使用 Blob 的 URL 來直接訪問和下載數據。

1. 整合性：Azure Blob Storage 可以與其他 Azure 服務和工具進行無縫整合。例如，你可以將 Blob Storage 與 Azure Functions、Azure Logic Apps 和 Azure Media Services 等服務結合使用，實現更強大的功能。

1. 成本效益：Azure Blob Storage 提供了彈性的價格模型，根據實際使用量計算費用。你只需支付實際使用的存儲容量和傳輸流量，並可以根據需求選擇合適的存儲層級，以優化成本。

總結來說，Azure Blob Storage 是一個可靠、安全、擴展和彈性的儲存服務，特別適合存儲和管理大量非結構化數據。它提供了多個存儲層級、細粒度的安全控制和良好的整合性，同時具有成本效益。無論是小型應用還是大型企業級應用程式，Azure Blob Storage 都能滿足不同規模和需求的數據儲存需求。

## 操作
### 在 Azure portal 上建立 Blob Storage
Step 1. 首先我們新增一個儲存體帳戶：開啟 marketplace → 輸入Blob → 選擇儲存體帳戶
![]( /images/content/20230614001.png)
Step 2. 點選建立
![]( /images/content/20230614002.png)
Step 3. 輸入儲存體帳戶相關必填資訊，點選檢閱後按確定
![]( /images/content/20230614003.png)
Step 4. 儲存體帳戶建立完成後，開啟儲存體帳戶主畫面 → 點選 容器(Blob)
![]( /images/content/20230614004.png)
Step 5. 點選新增容器
![]( /images/content/20230614005.png)
Step 6. 輸入名稱(全小寫)、存取層即選擇 Blob
![]( /images/content/20230614006.png)
Step 7. 點選建立
![]( /images/content/20230614007.png)
Step 8. 容器建立完成
![]( /images/content/20230614008.png)

### 在 Azure portal 上/下載檔案至 Azure Blob Storage 
Step 1. 點選剛剛我們建立的容器
![]( /images/content/20230614009.png)
Step 2. 點選上傳
![]( /images/content/20230614010.png)
Step 3. 選擇要上傳的檔案，點選確定
![]( /images/content/20230614011.png)
Step 4. 上傳完成 !
![]( /images/content/20230614012.png)
Step 5. 點選最右邊 ...按鈕 開啟下拉選單，點選下載，會立即下載檔案
![]( /images/content/20230614013.png)
Step 6. 您也可以直接複製下載連結 ： 點選檔案 → 複製 URL 即可
![]( /images/content/20230614014.png)

### 使用API 上/下載檔案至 Azure Blob Storage 
以下是使用 Azure Blob Storage .NET SDK 進行上傳和下載檔案的範例程式碼：
```csharp=
using Azure.Storage.Blobs;
using System;

class Program
{
    static async Task Main(string[] args)
    {
        // Azure Blob Storage 連線字串
        string connectionString = "your_connection_string";
        // Blob 容器名稱
        string containerName = "your_container_name";
        // Blob 名稱
        string blobName = "your_blob_name";
        // 檔案路徑
        string filePath = "your_file_path";

         // 上傳檔案到 Azure Blob Storage
        BlobServiceClient blobServiceClient = new BlobServiceClient(connectionString);
        BlobContainerClient containerClient = blobServiceClient.GetBlobContainerClient(containerName);
        BlobClient blobClient = containerClient.GetBlobClient(blobName);

        using (FileStream uploadStream = File.OpenRead(filePath))
        {
            await blobClient.UploadAsync(uploadStream, true);
        }

        Console.WriteLine("Blob uploaded successfully!");

        // 下載檔案從 Azure Blob Storage
        using (FileStream downloadStream = File.OpenWrite(downloadPath))
        {
            await blobClient.DownloadToAsync(downloadStream);
        }

        Console.WriteLine("Blob downloaded successfully!");
    }
}

```

## 案例分享
### 痛點
現行檔案中心是將檔案上傳到VM，可能會經常遇到以下問題：
1. 可用性問題：如果虛擬機發生故障或需要維護，則無法訪問或使用其中的檔案。這可能會導致服務中斷或停止。
1. 擴展性問題：虛擬機的存儲容量有限，當需要處理大量檔案或大型檔案時，可能會耗盡虛擬機的存儲空間。
1. 效能問題：虛擬機本身可能無法提供足夠的計算和存儲資源，導致上傳和下載檔案的效能變慢。
1. 可靠性問題：虛擬機的硬體故障或儲存故障可能導致數據損失或損壞，因為它們並不具備內建的數據冗餘和備份功能。
1. 維護和管理問題：將檔案存儲在虛擬機內需要進行管理、備份和維護工作，增加了管理成本和風險。

儲存資料的性質主要的內容是圖片（身分證、財力證明等文件）內容屬於機密文件，每日進件量也會非常可觀，單一系統每日檔案上傳量就高達1364筆。

### 改善
總和上述痛點，整理出檔案中心需要必備的特點：

1. 效能：需能承受高頻
2. 容量：需能承受高量
3. 維運：易於管理、備份、監控
4. 安全性：存取權限控制、加密

解決辦法：
1. 效能、容量問題：Azure Blob Storage 是一個高度可擴展的服務，可以根據需求進行橫向擴展。你可以通過增加存儲賬戶的容量和適當地配置存儲服務，以應對高頻高量的檔案上傳需求。
2. 維運問題：Azure Blob Storage 提供了許多監控工具和功能，如 Azure Monitor 和 Azure Storage 分析。可以使用這些工具來監控存儲使用情況、性能指標、錯誤日誌等，以便追蹤系統的狀態和進行故障排除。
3. 安全性問題：Azure Blob Storage 提供了多層次的安全措施，包括身份驗證、存取權限控制、加密和監控功能。這些功能可以幫助保護你存儲在 Blob Storage 中的機密文件免受未授權訪問和數據洩露。

綜合上訴原因需考量到可靠性、可擴展性、安全性等多放面的問題，此案例可考慮搭配使用Azure Blob Storage來解決問題。

### 優化
1. 引入緩存機制：
    * 使用快取技術，將經常訪問的檔案或數據暫存在內存或快取服務中，以提高訪問速度和效能。
1. 實現檔案分片和並行上傳：
    * 對於大型檔案，可以將其分成多個小片段進行上傳，這樣可以提高上傳效率。
    * 使用多線程或異步操作，實現並行上傳多個片段，以充分利用網絡帶寬。
1. 優化網絡傳輸：
    * 使用壓縮算法對檔案進行壓縮，減少傳輸的數據量。
    * 考慮使用流式傳輸，即在上傳過程中立即處理和儲存檔案的片段，而不需要等待整個檔案上傳完成。

## 總結
使用 Azure Blob Storage 作為檔案儲存解決方案是理想選擇。它提供高度可擴展的儲存能力，應對高頻高量的檔案上傳需求。同時具有優異的可用性、效能和安全性。透過 Azure Blob Storage，確保機密文件的安全且快速可靠地存取。與.NET 5或其他程式語言整合也非常容易。總體而言，使用 Azure Blob Storage 改善效能、可靠性、安全性和可擴展性，提供更好的檔案儲存和管理體驗。

## 參考連結
[Duran 的技術冶煉廠](http://dog0416.blogspot.com/2018/05/azure-azure-blob-storage.html)

[微軟官網介紹](https://azure.microsoft.com/zh-tw/products/storage/blobs)
