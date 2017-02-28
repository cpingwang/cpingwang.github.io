---
title: Execution Plan and Performance Tunning
date: 2017-02-28 18:35:20
tags: DB
---

Execution Plan
---
    當Query傳送到資料庫執行時，Query Optimizer會對query語句進行計算，
    多數的資料庫都是用基於成本的優化(CBO)，
    Optimizer針對每個運算設置一個成本(CPU成本，磁盤I/O成本和內存需求)，
    最終計算出相對比較少的成本Cost的Execution Plan後執行Query。
---
Optimizer與統計資訊
---
    Optimizer會統計分析資料狀態進行計算相關成本，統計資訊是一個很重要的依據。
    統計抽樣資訊是否可以代表實際的資料非常重要。
    (若統計抽樣資訊失真，可以考慮手動更新該資料表的統計資訊)
    
    注意Parameter sniffing，有以下四種解決方式：
    1.OPTION (RECOMPILE)
    2.OPTION (OPTIMIZE FOR (@VARIABLE=VALUE))
    3.OPTION (OPTIMIZE FOR (@VARIABLE UNKNOWN))
    4.Use local variables
---
How to read Execution Plan:
---
    資料流從右到左執行運算的取得最終資料
    哪些執行步驟花費的成本比較高?
    哪些執行步驟產生的數據量比較多?(每個Operation從右到左的箭頭線條的粗細代表資料傳回的多寡)
    每一步執行瞭什麼樣的動作?
    
    1.【Table Scan】：遍歷整個表，查找所有匹配的記錄行。
        這個操作將會一行一行的檢查，當然，效率也是最差的。
    2.【Index Scan】：根據索引，從表中過濾出來一部分記錄，再查找所有匹配的記錄行，
        顯然比第一種方式的查找范圍要小，因此比【Table Scan】要快。
    3.【Index Seek】：根據索引，定位（獲取）記錄的存放位置，然後取得記錄，
        因此，比起前二種方式會更快。
    4.【Clustered Index Scan】：和【Table Scan】一樣。注意：不要以為字面上有Index就認為不一樣。
       它的意思是按聚集索引來逐行掃描每一行記錄，因為記錄就是按聚集索引來順序存放的。
       而Table Scan是要掃描的表沒有聚集索引，因此這二個操作本質上是一樣的。
    5.【Clustered Index Seek】：直接根據聚集索引獲取記錄，最快！
---
三類基本Join方式
---
    Nested Loop Join (嵌套循環聯結) : 適用資料量小且輸入資料表都要有正確索引的查詢
    Merge Join (合並聯接) : 適用輸入資料量大、排序且有叢集索引或涵蓋索引
    Hash Join (哈希聯結) : 適用輸入資料量大、無排序定義查詢
---
SARG格式
---
    seek:=、>、<、between、部分like(ex:'allen%')
    Not Seek: Like '%A%'、Like '%A' year(c1)=2016、c1+15=115、In

---
執行時間分析與統計訊息作為tunning參考
---
    set statistics io,time,profile on;

    1.掃描計數(Scan count)：為了建構輸出的最終資料集，在達到分葉層級之後朝任何方向啟動以擷取所有值的搜尋/掃描次數。
    - 如果使用的索引是主索引鍵的唯一索引或叢集索引，而且您只要搜尋一個值，掃描計數就是 0。
      例如 WHERE Primary_Key_Column = <value>。
    - 當您要使用在非主索引鍵資料行上定義的非唯一叢集索引來搜尋一個值時，掃描計數就是 1。
      進行這項作業是為了檢查您所搜尋的索引鍵值是否有重複的值。 例如 WHERE Clustered_Index_Key_Column = <value>。
    - 當 N 是使用索引鍵找出索引鍵值之後，朝向分葉層級左側或右側啟動的不同搜尋/掃描次數時，掃描計數就是 N。

    2.邏輯讀取(Logical reads)：從資料快取中讀取的頁數。頁數越多，就是要取得的資料量越大，也就是消耗內部資源越大，查詢也就越沒有效率。
    - 這裡顯示的單位不是page也不是K、KB，是因為SQL Server在做讀寫的時候，會執行特定的程序，
      當每次執行一次這個程序，Read/Writre就會增加1，所以這個值越大，就表示SQL做了越多I/O，但是又不能計算出實際進行I/O的實際數量，
      所以這值就只能是一個邏輯估算值。

    3.實體讀取(physical reads)：從磁碟中讀取的頁數。
    
    4.讀取前讀取(read-ahead reads)：放入查詢快取中的頁數。
    - 實體讀取+讀取前讀取，就是SQL Server為了完成語句的查詢，從磁碟中讀取，如果不為0..就是資料並沒有存在暫存區，這是有一定程度會影響效能。

    5.LOB邏輯讀取(lob logical reads)：從資料快取中讀取的 text、ntext、image 或大數值類型 (varchar(max)、nvarchar(max)、varbinary(max)) 頁數。
    
    6.LOB實體讀取(lob physical reads)：從磁碟中讀取的 text、ntext、image 或大數值類型頁數。



