---
title: Git-Command
date: 2018-11-16 14:47:15
tags: DB
---


Git的基礎原理
---
	Git的機制是完整備份，不是差異備份

	[Git的基礎物件]
	blob -> file
	tree -> folder
	commit
	tag

---


基本指令
---
	git help 指令  -->查指令參數
	按 / 搜尋關鍵字

	[Git版控環境初始化（新建.git的隱藏目錄）]
	git init
	
	[將異動儲存到暫存區域（.git/objects/）]
	git add .
	git add --all
	
	[用暫存區的檔案建立一個提交]
	git commit -m "備註內容"


	[在本地建立遠端的分支]
	git remote add origin git@dsdsds...  (origin也可以任意自定為xyz...)

	[把本地所在分支的source推上origin指的位置的master分支]
	git push origin master
	(git push origin master:master)

	[把本地所在分支的source推上origin指的位置形成cat分支]
	git push origin master:cat
	

	[查詢某個檔案的異動歷程]
	git blame index.html

	
---


進階指令
---
	cat index.html | git hash-object --stdin  內容相同就會產生相同的SHA1id

	git cat-file SHA1id -t  查型態
	git cat-file SHA1id -p  查內容

	[Git操作記錄查詢]
	git reflog

	[回復到之前的提交點]
	git reset HEAD^ --hard  一個^倒退一步

	git reset HEAD~3 --hard  倒退3步

	git reset SHA1id --hard  直接指定到某個SHA1id

	git reset ORIG_HEAD --hard  回到上一次的危險操作


	[重新取得分支版本並刪除先前添加加的檔案]
	git checkout .
	git clean -df  (小心會把 git ignore的檔案都一起清除掉)
	

	
---


參考連結
---
	為你自己學 Git:
	https://gitbook.tw/

---

