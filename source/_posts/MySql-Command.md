---
title: MySql-Command
date: 2018-04-19 13:47:15
tags: DB
---


System相關
---
	[查詢現有proces]
	show processlist;
	show full processlist;
	
	[刪除特定proces]
	KILL <pid>;
	
	[查詢lock的相關資訊]
	show status like '%lock%';
	show status like 'Table%';
	show global status like '%thread%';
	
	Table_locks_immediate 表示立即釋放表鎖數
	Table_locks_waited 表示需要等待的表鎖數
	
	[查詢lock中的TABLES]
	show OPEN TABLES where In_use > 0;
	
	[查詢系統變數設定]
	show variables;
	show global variables like '%thread%';
	
---

參考連結
---
	超新手入門:
	http://www.codedata.com.tw/database/mysql-tutorial-getting-started/
	
	設定記錄執行過的SQL語法: 
	https://blog.longwin.com.tw/2007/06/mysql_record_any_sql_command_2007/
	http://www.cnblogs.com/zhanjindong/p/3472804.html
	
	修改連線時間變數wait_timeout: 
	http://mool.pixnet.net/blog/post/25219480-mysql-processlist-%E4%B8%80%E5%A4%A7%E5%A0%86sleep-
---

