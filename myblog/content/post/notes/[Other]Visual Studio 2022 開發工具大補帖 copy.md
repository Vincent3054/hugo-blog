---
title: "Code Smells 程式碼異味"
keywords :
- CodeSmells
- 程式碼異味
- Smells
- 壞味道
- Bad Smell
description : "Code Smells 程式碼異味"
author : "Sky Chen"
slug: CodeSmells
tags : ["Other","notes"]
categories:
- notes
- Other

date: "2024-08-01"

toc : true
coverSize: partial
coverImage: images/content/notes0023.jpg
thumbnailImage: images/content/notes0023.jpg
---
<!--more-->

# Code Smells 程式碼異味
tags: `Other` `notes`

{{< toc >}}
## 前言
這篇文章是根據《重構：改善既有程式的設計（第二版）》的內容撰寫，並參考了相關部落格文章和 RefactoringGuru 的資源，記錄了關於程式碼異味（Code Smells）的筆記。

## 簡介
程式碼異味 (Code Smells) 是指程式碼中存在的一些設計或實作上的問題，這些問題雖然不會直接導致程式錯誤，但會增加程式碼的複雜度、降低可讀性或維護性，並可能隱藏更大的潛在問題。程式碼異味通常是重構的信號，提示開發者應該對程式碼進行改進以提高其品質。

## 3.1 Mysterious Name (神秘的名稱)
- 是指程式碼中使用不明確或不具描述性的命名，讓人難以理解其用途或意圖。這樣的名稱會讓程式碼變得難以閱讀和維護
### 解法
為了避免這種情況，應該使用清晰且具描述性的名稱，以便其他開發者能夠快速理解程式碼的功能。
- 6.5 Change Function Declaration (修改函式宣告式)
- 6.7 Rename Variable (更改變數名稱)
- 9.2 Rename Field (更改欄位名稱)

## 3.2 Duplicated Code (重複的程式碼)
### Code Smells
- 是指在多個地方出現相同或非常相似的程式碼。這會增加維護的難度，因為修改一處可能需要同步修改多處。
![]( /images/content/20240801026.png)
### 解法
為了解決這個問題，應該將重複的程式碼提取出來，封裝成可以重複使用的函式或模組。
- 6.1 Extract Function (提取函式)
- 8.6 Slide Statements (移動陳述式)
- 12.1 Pull Up Method (提升方法)

## 3.3 Long Function (冗長的函式) Long Method
### Code Smells
- 是指一個函式的程式碼過長，通常超出了一個函式應該負責的單一責任範疇。這樣的函式不僅難以理解和測試，也容易引入錯誤。
- - 在〈什麼是Refactoring？〉提到long method的三個force，今天來解釋一下這三個force和部落客TEDDY補充的二個force的含意：
  - Explanation（解釋）：透過閱讀程式去理解軟體設計是一種常見的方式，而每一個method都有一個名字用來代表這個method的意圖。如果method內容很長，可能意味著這個method做了太多事，也就是說method的名稱很可能無法清楚解釋method的內容。廣義的說，long method降低understandability。
  - Sharing（共享）：long method的某一段程式也許在其他地方可以被重複使用，但因為long method包含太多其他東西，因此排除了別重複使用的機會。sharing也可以看成是reusability。
  - Choosing（選擇）：這一點看不懂什麼意思，知道的鄉民歡迎告知。
  - Modifiability（可修改性）：long method程式碼較多，邏輯與狀態也相對比較複雜，因此要針對long method進行修改就變得比較困難，也比較容易出錯。
  - Testability（可測性）：理由同上，因為long method程式碼較多，邏輯與狀態也相對比較複雜，所以也比較難進行測試。
![]( /images/content/20240801027.png)

### 解法
為了解決這個問題，通常需要將其拆分成多個較小且專注於單一任務的函式。
- 6.1 Extract Function (提取函式)
- 7.4 Replace Temp with Query (將暫時變數換成查詢函式)來移除暫時的變數。
- 6.8 Introduce Parameter Object (使用參數物件)
- 11.4 Preserve Whole Object (保留整個物件)來簡化一長串的參數。
- 如果還是有過多的暫時變數與參數，就使用 11.9 Replace Function with Command (將函式換成命令物件)
- 10.1 Decompose Conditional (分解條件邏輯)
- 6.1 Extract Function (提取函式)
- 10.4 Replace Conditional with Polymorphism (將條件式換成多型)
- 8.7 Split Loop (拆開迴圈)

## 3.4 Long Parameter List (冗長的參數列)
### Code Smells
- 是指一個方法或函數需要接收過多的參數，這不僅會讓代碼難以理解和維護，還容易導致錯誤。通常這是因為該方法試圖執行過多的責任或缺乏適當的封裝
![]( /images/content/20240801028.png)

### 解法
- 為了解決這個問題，可以考慮將參數封裝成一個物件，或者將方法拆分成更小、更具體的功能。
- 如果可以藉由查詢一個參數來取得另一個參數，就使用 11.5 Replace Parameter with Query (將參數換成查詢程式)
- 如果不想要從既有的資料結構拉出許多資料，可以使用 11.4 Preserve Whole Object (保留整個物件)來傳遞原始的資料結構。
- 如果許多參數總是同時出現，可以用 6.8 Introduce Parameter Object (使用參數物件)結合它們。
- 如果有參數被當成旗標來指定不同的行為，可以使用 11.3 Remove Flag Argument (移除旗標引數)

## 3.5 Global Data (全域變數)
### Code Smells
- 全域資料的問題在於它可被基礎程式的任何地方修改，卻無法察覺究竟有那些程式碼接觸它。
### 解法
- 6.6 Encapsulate Variable (封裝變數)

## 3.6 Mutable Data (可變資料)
### Code Smells
- 可變動的，也就是定義好的 data 會隨著不同情況做變動。mutable 很容易會有無法預期的 bug 產生。
- 與Mutable data相反的是Immutable data，介紹如下：
    - Immutable is whose state cannot be modified after it is created.
    - FP 是 immutable data ，也就是被定義好的 data 不會在任何情況下被改變，所以你能夠清楚預期他的內容。反之 mutable 是會變動的。
    - ![]( /images/content/20240801029.png)
### 解法
- 6.6 Encapsulate Variable (封裝變數)，確保所有的修改都是透過可以輕鬆地監控與改善的少數函式來進行的。
- 9.1 Split Variable (拆開變數)，來將變數分開，並且避免危險的更新。
- 8.6 Slide Statements (移動陳述式)，將其他的邏輯般到處理更新的程式碼外面。
- 6.1 Extract Function (提取函式)
- 11.1 Separate Query from Modifier (將查詢函式和修改函式分離)
- 11.7 Remove Setting Method (移除 set 方法)
- 9.3 Replace Derived Variable with Query (將衍生的變數換成查詢函式)
- 6.9 Combine Functions into Class (將函式移入類別)
- 6.10 Combine Functions into Transform (將函式組成轉換函式)
- 9.4 Change Reference to Value (將參考改成值)

## 3.7 Divergent Change (發散式修改)
### Code Smells
- 發散式修改就是，當你對類別進行修改時，您會發現自己必須更改許多不相關的方法。
  - 例如：在添加新的產品類型時，您必須更改查找、顯示和訂購產品的方法。
  - 不符合物件導向的單一職責原則(Single Responsibility Principle)
![]( /images/content/20240801030.png)

### 解法
聽常會發生的原因是因為"copypasta programming"或不好的程式結構造成。
- 6.11 Split Phase (拆成不同階段)
- 8.1 Move Function (移動函式)
- 7.5 Extract Class (提取類別)

## 3.8 Shotgun Surgery (散彈式修改)
### Code Smells
- 一但程式出現了shotgun surgery這種「牽一髮而動全身」的症狀，每次修改所影響的範圍很大，因此也增加了測試的困難度。最後，分散在不同類別的相同或相似責任，也會增加理解系統的困難度。
- Shotgun Surgery (散彈式修改) VS Divergent Change (發散式修改)
  - Shotgun Surgery 看起來類似於 Divergent Change，實際上是相反的CodeSmails。
  - 發散式變化：指的是一個類別會受到多種變化的影響(對單個類別進行許多更改)
  - 散彈式修改：指的是一個變化會影響到多個類別(同時對多個類別進行單一更改)
![]( /images/content/20240801031.png)

### 解法
拆開、解偶，放在適合的地方。
- 8.1 Move Function (移動函式)
- 8.2 Move Field (移動欄位)
- 6.9 Combine Functions into Class (將函式移入類別)
- 6.10 Combine Functions into Transform (將函式組成轉換函式)
- 6.11 Split Phase (拆成不同階段)

## 3.9 Feature Envy（依戀情結）
### Code Smells
- 關於Feature Envy 的定義，作者指出：「函式對於某個 class 的興趣高過對自己所處之 host class 的興趣。」

- 簡單來說就是，一個模組內的函式經常與另一個模組的函式或資料互動，甚至比它自己的模組的元素還要頻繁。
    - 比如 ClassA 的函式F 一直呼叫 ClassB 的 getter 那就很可能F根本就應該存在ClassB
![]( /images/content/20240801032.png)

- 作者指出，這種迷戀最常發生在「資料」上。
    - 今天如果 A 類裡的某個方法，老是喜歡存取 B 類的資料來運算，這會導致 B 的細節一旦有變，A 就不得不跟著變。或是每當 B 想要改變自己身上資料的存取方式時，還得看 A 的臉色。這就造成了 A 與 B 緊密耦合，而我們並不樂見此事。

### 解法
最後的疼愛是手放開，用搬移函數或提煉函數讓他們分開吧!
- 8.1  Move Method(搬移函數)
- 6.1  Extract Method(提煉函數)

那如果一個函式跟ClassA拿東西又跟ClassB拿東西又跟自己拿東西，那這個函式到底應該要放到哪裡去呢?
- 原則上哪個Class被這個函式使用的最多就該去哪

## 3.10 Data Clumps (資料泥團)
### Code Smells
- 關於Data Clumps 的定義，作者指出：「資料項目(data items)就像小孩子，喜歡成群結隊的待在一起，你常常可以在很多不同的地方看到相同的幾個 data item 同時出現」
![]( /images/content/20240801033.png)

- 通常這個問題會發生在"程式結構不良"或"copypasta programming"
    - 程式結構不良
        - 沒有把資料拆出Model
    - copypasta programming
        - 複製貼上縫合怪
    - 這個Code Smells可能會同時出現在
        - 3.3 Long Function (冗長的函式)
        - 3.4 Long Parameter List (冗長的參數列)

### 解法
這些會同時出現的資訊就該放在同一個物件裡
- 7.5 Extract Class (提取類別)
- 6.8 Introduce Parameter Object (使用參數物件)
- 11.4 Preserve Whole Object (保留整個物件)

那要怎麼判斷哪些人應該一起被放進別的物件裡呢? 
- 只需要把其中一個刪掉，找出其他跟著失去意義的資料，那這些全部都應該一起打包成新物件

## 3.11 Primitive Obsession (基本型態偏執)
### Code Smells
- 不要執著於使用一堆基本型別(Primitive) 在物件的世界裡該用物件的時候就用物件
    - 比如 Money 類別 就是一個int number跟string currency合在一起
    - Range 類別 就是兩個int
![]( /images/content/20240801034.png)

- 會發生的原因就是「懶」
    - 以Range來舉例，這裡就兩個int搞定，一個表示start，一個表示end 就好了啊，幹嘛還要寫新的類別

## 解法
常見的解法
- 7.3 Replace Primitive with Object (將基本元素換成物件)
- 12.6 Replace Type Code with Subclasses (將型別代碼換成子類別)
- 7.5 Extract Class (提取函式)
- 6.8 Introduce Parameter Object (使用參數物件)

## 3.12 Repeated Switchess (重複的切換邏輯)

### Code Smel
- 作者在初版指出：「多數時候當我們看到Switch Statements時，我們應該考慮使用多型（Polymorphism）來取代他。」
    - 因為當時開發者大多忽視了物件導向中多型的價值，所以希望能矯正這樣的風氣

- 作者在第二版將這個氣味更名為「Repeated Switches」。比起「Switch Statements」，我們更應該聚焦在「重複（Repeated）」所造成的混亂與邪惡之上。
    - 現代開發者越來越習慣使用多形，且很多語言現在也支持複雜的Switch Statements條件句，而不是只根據基本型別或類別碼來作為條件判斷。
![]( /images/content/20240801035.png)

### 解法
用多形來取代重複的Switchess吧!
- 10.4 Replace Conditional with Polymorphism (將條件式換成多型)

## 3.13 Loops (迴圈)
### Code Smel
- 最早的程式，難免會需要用到Loops，因為當時沒有什麼替代品。
- 如今有很多替代方式可以取代Loops，幫助更快的處理動作。
    - 像是filter(過濾器) 與 map 等管道操作(pipeline operation) 可協助我們快速地查看在處理過程中使用的元素，以瞭解它們的用途。
    
### 解法
別用for迴圈了，改用map和filter吧!
- 8.8 Replace Loop With Pipeline (將迴圈改成流程)


## 3.14 Lazy Element (冗員元素)
### Code Smel
- 當你在專案內發現存在一個無所事事的元素或類別，幾乎沒有實作任何方法與職責，正是屬於這種程式碼氣味。
- 會發生的原因
    - 可能經歷多次優化迭代以後，它不知不覺之間變得非常小巧輕薄，甚至可有可無。
    - 可能是這個類別最初為了支援未來的某個專案而設計，但這些計劃工作從來沒有被正式實施或完成。
![]( /images/content/20240801036.png)

### 解法
你所創建的類別都需要有人去理解它、維護它，這些都需要成本，如果一個類別不值得這麼做 ，就該把它處理掉!

- 6.2 Inline Function (將函式內聯)
- 7.6 Inline Class (內聯類別)

## 3.15 Speculative Generality (畫大餅)
### Code Smel
- 當我們撰寫的程式碼是用來應對未來需求，但現實中卻可能永遠都派不上用場的這種情況。
- Speculative Generality (畫大餅)常跟 Dead Code (亡靈程式碼)搞混
    - Dead Code 指的是未被其他程式碼使用的程式碼
    - Speculative Generality 則是從業務邏輯或需求的角度來看無用的程式碼。
![]( /images/content/20240801037.png)

### 解法
別畫大餅了，通通拿掉!
- 如果用不太到的抽象類別，使用 12.9 Collapse Hierarchy (折疊類別階層)。
- 使用 6.2 Inline Function (將函式內聯) 與 7.6 Inline Class (內聯類別) 來移除非必要的委託。
- 如果函式有一些用不到的參數，可以用 6.5 Change Function Declaration (修改函式宣告式) 來移除它們。
- 如果某個函式或類別的使用方只有測試程式，應該刪除測試案例，並執行8.9 Remove Dead Code (移除死碼)。

## 3.16 Temporary Field (暫時欄位)
### Code Smel
- 當一個類別或物件有一個或多個欄位只有在特定情況下才會使用到，例如在方法呼叫階段用來暫時儲存資料，其他多數時候只是空值或沒有相關的值。
    - 這些欄位並不包含在該類別的主要職責當中，通常只存在特定前提條件下才有意義。
- 這個Code Smel通常也會導致 3.4 Long Parameter List
![]( /images/content/20240801038.png)

### 解法
可以拆出來，有可以在傳參指定Null空物件來實作與原本實際物件相同的介面
- 7.5 Extract Class (提取類別)
- 8.1 Move Function (移動函式)
- 10.5 Introduce Special Case(加入特例)/Introduce Null Object (引入Null對象)

## 3.17 Message Chains (過度耦合的訊息鏈)
### Code Smel
- 當我們執行方法時會需要呼叫一個物件，然後該物件又需要呼叫另外一個物件，以此類推長長串在一起
![]( /images/content/20240801039.png)

- 需要特別留意「3.17 Message Chain」和「3.18 Middle Man」這兩種氣味密切相關，有時互為因果。開發者需要特別留意在兩種氣味之間取得平衡。

### 解法
移動、抽出、隱藏，想辦法不要那麼耦合，不然很難測試、維運。
- 7.7 Hide Delegate (隱藏委託)
- 6.1 Extract Function (提取函式)
- 8.1 Move Function (移動函式)

## 3.18 Middle Man (中間人)
### Code Smel
- 如果一個類只執行一個操作，將工作委派給另一個類，除了左手轉右手之外沒有其他存在的價值與意義。
![]( /images/content/20240801040.png)

### 解法
要拆也不要拆太細，拆到那個類只做左手轉右手的事
- 7.8 Remove Middle Man (移除中間人)
- 6.2 Inline Function (將函式內聯)
- 12.10 Replace Subclass with Delegate (將子類別換成委託類別)
- 12.11 Replace Superclass with Delegate (將超類別換成委託類別)

## 3.19 Insider Trading (內幕交易)
### Code Smel
- 或稱Inappropriate Intimacy（不當的親密關係），兩個類別過於親密，花太多時間去研究彼此的private成分
- 如果兩個類別過於了解彼此的細節，則在閱讀程式的時候，需要同時看懂這兩者，增加理解的困難度。此外，則任一方的改變都可能造成另一方的連動變化。
![]( /images/content/20240801041.png)

### 解法
將雙向關聯改為單向關聯，使用繼承，或是把不需要的拆出來。
- 8.1 Move Function (移動函式)
- 8.2 Move Field (移動欄位)
- 7.7 Hide Delegate (隱藏委託)

繼承往往是造成過度親密的原因，因為subClass對superClass的了解總是超出預期，可以用delegation來減少兩者的依賴
- 12.10 Replace Subclass with Delegate (將子類別換成委託類別)
- 12.11 Replace Superclass with Delegate (將超類別換成委託類別)

## 3.20 Large Class (龐大的類別)
### Code Smel
- Large class和long method(Function)壞味道很像，都可能造成duplicated code以及降低重複使用的可能性。
    - long method(Function)關注的點在method層次，而large class則是在class層次，large class的scope比較大，影響比long method還要來的強烈。
    ![]( /images/content/20240801042.png)

### 解法
- 如果元件適合使用繼承，使用：
   - 12.8 Extract Superclass (提取超類別) 
- 看看它們是否只使用類別的部分功能，或許可以將部分的功能變成獨立的類別，使用以下方法提取它們。
    - 7.5 Extract Class (提取類別)
    - 12.8 Extract Superclass (提取超類別) 
    - 12.6 Replace Type Code with Subclasses (將型別代碼換成子類別) 

## 3.21 Alternative Classes with Different Interfaces (異曲同工的類別)
### Code Smel
- 兩個類別名稱不同但做的是一樣的事
- 工程師在開發函式的時候，並不知道這個功能已經有了，多人分工時特別常發生。
![]( /images/content/20240801043.png)

### 解法
如果兩個函式在同一個library 那就選一個留下就好。
但如果兩個在不同的library，就很值得仔細觀察這兩個函式並分離出一個合理的抽象(介面)。
- 6.5 Change Function Declaration (修改函式宣告式)
- 8.1 Move Function (移動函式)
- 12.8 Extract Superclass (提取超類別)

## 3.22 Data Class (呆板的資料類別)
### Code Smel
- Data Class是指只有屬性（資料成員），或是存取這些屬性的getter/setter函數，但卻沒有其他行為函數的類別。
- 從物件導向的角度來看，類別應該包含資料與行為，一個只有資料的類別，隱含在其他地方會有一些程式碼來處理它。何不考慮將這些散布在各處，處理Data Class的程式碼，搬移到Data Class身上呢？
![]( /images/content/20240801044.png)

### 解法
這種類別只是一個不會說話的資料容器被其他類別所操控，如果Data Class還有一些public的欄位讓大家直接存取，資料會被亂改很難維護，資料也缺乏完整性。
- 使用 7.1 Encapsulate Record (封裝記錄) 封裝它們。
- 對任何不應該被變動的欄位執行 11.7 Remove Setting Method (移除 set 方法)。
- 使用 8.1 Move Function (移動函式) 將行為邏輯移入資料類別。
- 如果無法移動整個函式，使用 6.1 Extract Function (提取函式)

## 3.23 Refused Bequest (被拒絕的遺產)
### Code Smel
- 指的是程式碼過度利用繼承
    - 只因為想要reuse code而繼承自錯誤的superclass，導致subclass有些繼承自superclass的方法是完全用不到的
- 作者提到這個Code Smel不是很濃烈，Composite設計模式就屬於這種例子，便可以放著不用管它。但如果是錯用繼承的情況，就不能視而不見。
![]( /images/content/20240801045.png)

### 解法
- 過度濫用繼承或錯用繼承的情況，可以參考這篇[文章](https://www.jyt0532.com/2020/03/22/lsp/)，只在正確的時候使用繼承。
- 當繼承階層是錯的，必須建立一個新的旁系類別(sibling class)，使用 12.4 Push Down Method (下移方法) 與 12.5 Push Down Field (下移欄位) 來將用不到的程式碼放入那個旁系類別。
- 如果子類別重複使用行為，但是不想使用父類別的介面，不介意子類別拒絕繼承程式碼，但是如果它拒絕介面，就會大聲譴責，當遇到這種情況時，不要隨便更改繼承階層，應該使用
  - 12.10 Replace Subclass with Delegate (將子類別換成委託類別)
  - 12.11 Replace Superclass with Delegate (將超類別換成委託類別)

## 3.24 Comments (過多的註解)
### Code Smel
- 作者強調Comment如果用的好，算不上是壞味道，甚至是好味道。但在很多情況下，註解被當成是一種「障眼法」，用來掩飾「寫得亂七八糟，沒人看得懂的程式碼。」
- 當您覺得需要寫註解時，請先嘗試重構，試著讓所有注視都變得多餘。
- The best comment is a good name for a method or class.
![]( /images/content/20240801046.png)

### 解法
通常一個好的變數名稱或是函式名稱，就可以讓你不再需要註釋。
- 6-1 Extract Function (提取函式)
要是你費盡心思把複雜的函式拆解成眾多小函式，但你卻命名的很難懂，那就會更難讓人理解。
- 6-5 Change Function Declaration (修改函式宣告式)
- 10-6 Introduce Assertion (加入斷言)


## 參考資料
[Refactoring.Guru](https://refactoring.guru/)
[jyt0532's Blog](https://www.jyt0532.com/)
[搞笑談軟工]https://teddy-chen-tw.blogspot.com/
[《重構 - 改善既有程式的設計》Martin Fowler]()