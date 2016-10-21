---
title: Oracle Useful SQLs
date: 2016-10-19 18:53:50
tags: DB
---


V$Session相關
---	
	[產生Kill session的scripts]
	SELECT 'Alter system kill session ''' || SID || ','|| serial# ||''';'  
	FROM V$SESSION WHERE username='xxx';
	
	[查詢Locked object name]
	SELECT a.sid, a.serial#,OBJECT_NAME
	FROM V$SESSION a, v$locked_object b, dba_objects c 
	where b.object_id = c.object_id 
	and a.sid = b.session_id;
---
