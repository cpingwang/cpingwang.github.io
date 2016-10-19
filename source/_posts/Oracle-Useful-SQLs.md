---
title: Oracle Useful SQLs
date: 2016-10-19 18:53:50
tags: DB
---

產生Kill session的scripts
---	
	SELECT 'Alter system kill session ''' || SID || ','|| serial# ||''';'  
	FROM V$SESSION WHERE username='xxx';
	
---
