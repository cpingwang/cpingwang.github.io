---
title: RDB vs. NoSQL
date: 2019-04-09 14:42:33
tags: DB
---

比較
---
{% asset_img compare_rdb_nosql.png %}

---
ACID
---
	Atomicity (原子性)
	  一個交易中的所有操作改變，是全部發生或是全部不發生。
	  交易在執行過程中發生錯誤，會被回滾（Rollback）到開始前的狀態，就像從來沒有執行過一樣。
	  ex. 例如轉帳這件事，你不會希望轉帳失敗後對方沒收到錢但你的帳戶還是被扣錢了。

	Consistency (一致性)
	  在交易開始之前和結束以後，資料庫的完整性沒有被破壞。
	  這表示寫入的資料必須完全符合所有的約束、觸發器、級聯回滾等。
	  ex1.資料庫設定了帳戶餘額不可小於0的constraints，
	      小白帳戶餘額為 50元轉帳，想轉帳 100元給小黑，違反約束所以資料庫會取消這項操作。
	  ex2.小白轉帳 10元給小黑，結果小黑只拿到 5元，這就是不一致，資料庫必須取消這項操作。

	Isolation(隔離性)
	  資料庫允許多個並發交易同時對其數據進行讀寫和修改的能力，
	  隔離性可以防止多個交易並發執行時由於交叉執行而導致數據的不一致。
	  ex. A交易:小白要轉帳給小黑 10元，同時間B交易:小黑要轉帳給小黃10元;
	  這兩個交易不論是 先A後B 或是 先B後A，最後的結果必須完全一樣。

	Durability(持久性)
	  交易處理結束後，對數據的修改就是永久的，即便系統故障也不會丟失。
	  ex.你不會希望轉帳成功後，因為突然停電結果發現剛剛轉帳的結果不見了。
---
CAP
---
	CAP理論有三個關鍵：
	  1.資料一致性（Consistent）：在分散式架構，一致性是說多個節點的資料是否一致。
	  2.可用性（Availability）：服務能保證是可用的狀態，並在有限時間內返回結果。
	  3.分區容錯性（Partition Tolerance）：這邊的Partition指的是網路分區。
	
	理論上無法同時兼顧CAP這三種特性，所以，NoSQL資料庫通常會選擇其中兩種特性來設計，
	通常是選擇CP或AP。
---
BASE
---
	BASE 是對 CAP 中 C 和 A 的延伸：
	  Basically Available：基本可用； --> 稍微犧牲A
	  Soft state：軟狀態/柔性交易，即狀態可以有一段時間的不同步； --> 為了P犧牲C
	  Eventual consistency：最終一致性； --> 應用機制達成C

	BASE 是基於 CAP 理論逐步演化而來，核心思想是：
	即便不能達到「強一致性」（Strong consistency），
	但可以根據應用特點採用適當的方式來達到「最終一致性」
	（Eventual consistency）的效果。
---
參考連結
---
	https://shininglionking.blogspot.com/2018/04/rdbms-vs-nosql.html
	http://garyliutw.blogspot.com/2014/05/mongodb-nosql.html
	


