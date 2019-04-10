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
	  Transaction的改變是全部發生或是全部不發生
	  ex. 例如轉帳這件事，你不會希望轉帳失敗後對方沒收到錢但你的帳戶還是被扣錢了。

	Consistency (一致性)
	  Transaction 中發生的所有行為不能違反任何constraints.
	  ex. 小白轉帳 10元給小黑，結果小黑只拿到 5元，這就是不一致，資料庫必須取消這項操作。

	Isolation(隔離)
	  多個Transactions可以同時進行，以某項順序依序執行，最後的結果必須完全一樣。
	  ex. A交易:小白要轉帳給小黑 10元，同時間B交易:小黑要轉帳給小黃10元;
	  這兩個交易不論是 先A後B 或是 先B後A，最後的結果必須完全一樣。

	Durability(持久性)
	  一但Transation成功結束，狀態的改變就是永遠的了。
	  ex.你不會希望轉帳成功後，因為突然停電結果發現剛剛轉帳的結果不見了。
---
CAP
---
	CAP理論有三個關鍵：
	  1.資料一致性（Consistent）
	  2.可用性（Availability）
	  3.分區容錯性（Partition Tolerance）
	
	理論上無法同時兼顧CAP這三種特性，所以，NoSQL資料庫通常會選擇其中兩種特性來設計，
	通常是選擇CP或AP。
---
BASE
---
	BASE 是對 CAP 中 C 和 A 的延伸：
	  Basically Available：基本可用；
	  Soft state：軟狀態/柔性交易，即狀態可以有一段時間的不同步；
	  Eventual consistency：最終一致性；

	BASE 是基於 CAP 理論逐步演化而來，核心思想是：
	即便不能達到「強一致性」（Strong consistency），
	但可以根據應用特點採用適當的方式來達到「最終一致性」
	（Eventual consistency）的效果。
---
參考連結
---
	https://shininglionking.blogspot.com/2018/04/rdbms-vs-nosql.html
	http://garyliutw.blogspot.com/2014/05/mongodb-nosql.html
	


