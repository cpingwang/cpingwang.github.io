---
title: Execution Plan and Performance Tunning
date: 2017-02-28 18:35:20
tags: DB
---

Execution Plan
---
    當Query傳送到資料庫執行時，Query Optimizer會對query語句進行計算，
    多數的資料庫都是用基於成本的優化(Cost Base Optimizer -> CBO)，
    Optimizer針對每個運算設置一個成本(CPU成本，磁盤I/O成本和內存需求)，
    最終計算出相對比較少的成本Cost的Execution Plan後執行Query。
---
Optimizer(優化器)與Statistics(統計資訊)
---
    Optimizer會統計分析資料狀態進行計算相關成本，Statistics是一個很重要的依據。
    統計抽樣資訊是否可以代表實際的資料非常重要。
    (若統計抽樣資訊失真，可以考慮手動更新該資料表的統計資訊)
    
    注意Parameter sniffing，有以下四種解決方式：
    1.OPTION (RECOMPILE)
    2.OPTION (OPTIMIZE FOR (@VARIABLE=VALUE))
    3.OPTION (OPTIMIZE FOR (@VARIABLE UNKNOWN))
    4.Use local variables
---
用指令顯示Execution Plan:
---
	輸出文字格式:
	SET SHOWPLAN_ALL ON
    --此處放置您的T-SQL語法--
    SET SHOWPLAN_ALL OFF
	
	SHOWPLAN_TEXT 僅輸出執行計畫，不包含預估成本
	
	輸出XML格式:
	SET SHOWPLAN_XML ON
	--此處放置您的T-SQL語法—
	SET SHOWPLAN_XML OFF
---
How to read Execution Plan:
---
    圖形執行計畫輸出是從右向左讀，從上向下讀
	每一個運算子會顯示其處理成本佔總成本的百分比
	執行計畫會提出Missing Index的建議(需經過評估，不可盲目建立Index)
    哪些執行步驟花費的成本比較高?
    哪些執行步驟產生的數據量比較多?(每個Operation從右到左的箭頭線條的粗細代表資料傳回的多寡)
    了解每一步執行什麼樣的動作?
    
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
{% asset_img 3JoinTypes.png %}

---
SARG格式
---
    seek:=、>、<、between、部分like(ex:'allen%')
    Not Seek: Like '%A%'、Like '%A' year(c1)=2016、c1+15=115、In

---
執行時間分析與統計訊息作為tunning參考
---
    清除快取的指令(注意不可在Prod環境執行)：
	DBCC FREEPROCCACHE
    DBCC DROPCLEANBUFFERS

    set statistics io,time,profile on;
	--此處放置您的T-SQL語法--
	set statistics io,time,profile off;

    1.掃描計數(Scan count)：為了建構輸出的最終資料集，在達到分葉層級之後朝任何方向啟動以擷取所有值的搜尋/掃描次數。
    - 如果使用的索引是主索引鍵的唯一索引或叢集索引，而且您只要搜尋一個值，掃描計數就是0。
      例如 WHERE Primary_Key_Column = <value>。
    - 當您要使用在非主索引鍵資料行上定義的非唯一叢集索引來搜尋一個值時，掃描計數就是1。
      進行這項作業是為了檢查您所搜尋的索引鍵值是否有重複的值。
	  例如 WHERE Clustered_Index_Key_Column = <value>。
    - 當N是使用索引鍵找出索引鍵值之後，朝向分葉層級左側或右側啟動的不同搜尋/掃描次數時，掃描計數就是N。

    2.邏輯讀取(logical reads)：從資料快取中讀取的頁數。頁數越多，就是要取得的資料量越大，也就是消耗內部資源越大，查詢也就越沒有效率。
    - 會包含 physical reads 及 read-ahead reads
	- 這個值越大，就表示SQL做了越多I/O，但是又不能計算出實際進行I/O的實際數量，所以這值就只能是一個邏輯估算值。

    3.實體讀取(physical reads)：執行計劃生成後，Cache中缺少的資料從磁碟中讀取的頁數(page)。
    
    4.讀取前讀取(read-ahead reads)：生成執行計劃過程中判斷查詢可能需要的資料而預先載入至Cache的頁數(page)。

    5.LOB邏輯讀取(lob logical reads)：從資料快取中讀取的 text、ntext、image 或大數值類型 (varchar(max)、nvarchar(max)、varbinary(max)) 頁數。
    
    6.LOB實體讀取(lob physical reads)：從磁碟中讀取的 text、ntext、image 或大數值類型頁數。

---
查詢SqlServer當下Top CPU/IO usage的語法
---	
	SET TRANSACTION ISOLATION LEVEL READ UNCOMMITTED
    SELECT Top 10
	DB_NAME(st.dbid) as DBName,
    OBJECT_SCHEMA_NAME(st.objectid,st.dbid) as SchemaName,
    OBJECT_NAME(st.objectid,st.dbid) as StoredProcedure,
    qs.execution_count,
    --qs.total_worker_time AS TT_CPU,
    qs.total_worker_time/1000000 as TT_CPU_Sec, --Converted from microseconds
    (qs.total_worker_time/1000000) / qs.execution_count as AVG_CPU_Sec, --Converted from microseconds
    (qs.total_elapsed_time/1000000) as TT_elapsed_time_Sec, --Converted from microseconds
	(qs.total_logical_reads+qs.total_logical_writes+qs.total_physical_reads) AS TT_IO,
	qs.total_logical_reads,
	qs.total_logical_writes,
	qs.total_physical_reads,
    --es.reads,
    --es.writes,
	st.text,
    qp.query_plan,
	er.session_id, 
    --er.request_id,
    --er.sql_handle,
    es.login_name,
    es.nt_user_name,
    es.[host_name],
    es.[program_name]
    FROM sys.dm_exec_requests AS er 
    LEFT JOIN sys.dm_exec_sessions AS es on er.session_id = es.session_id 
    LEFT JOIN sys.dm_exec_query_stats AS qs on sys.fn_varbintohexstr(er.sql_handle) = sys.fn_varbintohexstr(qs.sql_handle)
    CROSS APPLY sys.dm_exec_sql_text(qs.sql_handle) AS st
    CROSS apply sys.dm_exec_query_plan (qs.plan_handle) AS qp
    WHERE st.dbid is not null
    ORDER BY qs.total_worker_time / qs.execution_count DESC
    --ORDER BY qs.total_worker_time DESC
    --ORDER BY qs.total_logical_reads DESC
    --ORDER BY qs.total_logical_writes DESC
    --ORDER BY qs.total_physical_reads DESC
    --ORDER BY qs.total_elapsed_time DESC
    --ORDER BY qs.execution_count DESC
