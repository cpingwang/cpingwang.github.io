---
title: MongoDB memo
date: 2019-01-04 18:30:35
tags: DB
---


基本概念
---
	Collection 集合(像是Table)
	Document (像是Row)

	Document 的內容就是Key對應Value的組合

	Key的規定，區分大小寫，且不能重複

	例如：
	{ name : "peter" }
	{ Name : "peter" }
	會存為兩份document

---
基本指令
---
	建立test資料庫(如果test存在則是切換資料庫，創建後若無任何操作則會自動刪除該資料庫)
	> use test

	查看當前有多少資料庫
	> show dbs

	創建集合
	> db.集合名.insert({})

	查看當前資料庫有哪些集合
	> show tables

	查詢集合裡面的文檔
	> db.集合名.find()

	查詢該集合下的第一個文檔
	> db.集合名.find


---
參考連結
---
	https://www.itread01.com/content/1531480965.html
	https://ithelp.ithome.com.tw/articles/10184657

