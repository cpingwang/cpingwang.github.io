---
title: Oracle Command On Linux
date: 2016-06-07 10:54:38
tags: DB
---

用root登入DB後,切換為oracle的使用者:    
    # su - oracle
	
---
檢查監聽器狀態:

	$ lsnrctl status
	
---
DB關閉:
	
	關閉監聽器: 
    1)$ lsnrctl stop
    
	用sysdba登入sqlplus
	2)$ sqlplus '/ as sysdba'
    3)SQL> shutdown immediate (shutdown abort)
	
---	
DB開啟:

    1)開啟監聽器:
	$ lsnrctl start
	
	用sysdba登入sqlplus
    2)$ sqlplus '/ as sysdba'
    3)SQL> startup


---
Oracle Enterprise Manager (EM)

    查看dbconsole狀態:
    $ emctl status dbconsole

    重啟DB後需執行
	$ emctl start dbconsole
	才能使用https://192.168.56.101:1158/em

	開啟EM服務:
	$ emctl start dbconsole

    關閉EM服務:
	$ emctl stop dbconsole

    刪除一個EM資料庫:
    $ emca -repos drop

	創建一個EM資料庫(包含config):
    $ emca -repos create
    (重建一個EM資料庫: $ emca -repos recreate)

    刪除em的config:
    $ emca -deconfig dbcontrol db

	配置em的config(SID,1521):
    $ emca -config dbcontrol db

    若出現'job_queue_processes' must be greater than or equal to 1.的錯誤訊息,修改設定DB 參數job_queue_processes=10 後重跑
	$ emca -config dbcontrol db

	$ sqlplus '/ as sysdba'
    SQL> show parameter job
    SQL> alter system set job_queue_processes=10 scope=both;

    System altered.

    SQL> show parameter job	
	
---
