---
title: Oracle Useful SQLs
date: 2016-10-19 18:53:50
tags: DB
---


V$Session相關
---	
	[Kill session]
	Login as DBA...
	SELECT * from v$session where type='USER' and program='SQL Developer';
	ALTER system kill session 'SID,SERIAL#' IMMEDIATE;
	
	[產生Kill session的scripts]
	SELECT 'Alter system kill session ''' || SID || ','|| serial# ||''' IMMEDIATE;'  
	FROM V$SESSION WHERE username='xxx';
	
	[查詢Locked object name]
	SELECT a.sid, a.serial#,OBJECT_NAME
	FROM V$SESSION a, v$locked_object b, dba_objects c 
	where b.object_id = c.object_id 
	and a.sid = b.session_id;
---

System相關
---
	[清除shared_pool]測試performance前清除buffer cache。  **不可在production上執行
	Alter System flush shared_pool;
	
	[顯示dbms_output.put_line('');]
	SET SERVEROUTPUT ON;
---

DECLARE 語法的使用
---
	SET SERVEROUTPUT ON;
	DECLARE 
	  V_BUCODE CHAR(5):='BU003';
	  V_WAGERSN NUMBER:=99;
	  V_STAKEAMOUNT NUMBER;
	BEGIN
	  SELECT STAKEAMOUNT INTO V_STAKEAMOUNT FROM WAGER 
	   WHERE BUCODE= UPPER(V_BUCODE) AND WAGERSN=V_WAGERSN;
	  dbms_output.put_line(V_STAKEAMOUNT);
	END;
	/
---

DEFINE 語法的使用
---
	DEFINE BUCODE='BU003';
	DEFINE WAGERSN=2066498;

	select * from WAGER where BUCODE= UPPER('&BUCODE') and WAGERSN=&WAGERSN;

	DEFINE WAGERSN=2066499;
	select * from WAGER where BUCODE= '&BUCODE' and WAGERSN=&WAGERSN;

	UNDEFINE BUCODE;
	UNDEFINE WAGERSN;
---


