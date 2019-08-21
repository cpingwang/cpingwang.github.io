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

	[檢查innodb lock 狀態]
	show global status like 'Innodb_row%';

	[檢查isolation level]
	SELECT * FROM information_schema.session_variables WHERE variable_name = 'tx_isolation';
	或是
	SELECT @@tx_isolation;

	
	Table_locks_immediate 表示立即釋放表鎖數
	Table_locks_waited 表示需要等待的表鎖數
	
	[查詢lock中的TABLES]
	show OPEN TABLES where In_use > 0;
	
	[查詢系統變數設定]
	show variables;
	show global variables like '%thread%';

	[檢查innodb的系統紀錄資訊]
	show engine innodb status;
	
---

參考連結
---
	超新手入門:
	http://www.codedata.com.tw/database/mysql-tutorial-getting-started/
	
	查詢lock相關資訊:
	http://daizj.iteye.com/blog/2247725
	
	台灣MySQL技術研究站:
	https://www.mysql.tw/2018/06/mysql-lock-table-lockrow-lock.html

	修改連線時間變數wait_timeout: 
	http://mool.pixnet.net/blog/post/25219480-mysql-processlist-%E4%B8%80%E5%A4%A7%E5%A0%86sleep-
	
	設定記錄執行過的SQL語法: 
	https://blog.longwin.com.tw/2007/06/mysql_record_any_sql_command_2007/
	http://www.cnblogs.com/zhanjindong/p/3472804.html
	
	explain用法和性能分析
	https://blog.csdn.net/haifu_xu/article/details/16864933
---

