---
title: Oracle ASH and AWR
date: 2016-06-29 11:24:17
tags: DB
---

ASH: Active Session History --> in Memory
(每秒1個sample,依內存空間大約只暫存最近一個小時內的資料)
	
	V$ACTIVE_SESSION_HISTORY
	  - Displays the active session history (ASH) sampled every second.
	V$METRIC
	  - Displays metric information.
	V$METRICNAME
	  - Displays the metrics associated with each metric group.
	V$METRIC_HISTORY
	  - Displays historical metrics.
	V$METRICGROUP
	  - Displays all metrics groups.
	
	查詢過去一小時的Top SQL:
	SELECT SESSION_TYPE,TOP_LEVEL_SQL_ID,SQL_ID,SQL_PLAN_HASH_VALUE,WAIT_CLASS,COUNT(1) as SECONDS
    FROM V$ACTIVE_SESSION_HISTORY 
    WHERE SAMPLE_TIME >SYSDATE-1/24 
    GROUP BY SESSION_TYPE,TOP_LEVEL_SQL_ID,SQL_ID,SQL_PLAN_HASH_VALUE,WAIT_CLASS
    ORDER BY 6 DESC
	
	從ASH中查SQL plan:
	SELECT * FROM TABLE(DBMS_XPLAN.DISPLAY_CURSOR('SQL_ID'))
	
	More info: https://oracle-base.com/articles/10g/active-session-history
---
AWR: Automatic Workload Repository --> in Disk
(將1/10的ASH sample從內存放到Disk)
    
	DBA_HIST_ACTIVE_SESS_HISTORY
	  - Displays the history contents of the active session history.
	DBA_HIST_BASELINE
      - Displays baseline information.
	DBA_HIST_DATABASE_INSTANCE
	  - Displays database environment information.
	DBA_HIST_SNAPSHOT
	  - Displays snapshot information.
	DBA_HIST_SQL_PLAN
	  - Displays SQL execution plans.
	DBA_HIST_WR_CONTROL
	  - Displays AWR settings.
	
	查詢過去一小時的Top SQL:
	SELECT SESSION_TYPE,TOP_LEVEL_SQL_ID,SQL_ID,SQL_PLAN_HASH_VALUE,WAIT_CLASS,COUNT(1) as SECONDS
    FROM DBA_HIST_ACTIVE_SESS_HISTORY 
    WHERE SAMPLE_TIME >SYSDATE-1/24 
    GROUP BY SESSION_TYPE,TOP_LEVEL_SQL_ID,SQL_ID,SQL_PLAN_HASH_VALUE,WAIT_CLASS
    ORDER BY 6 DESC
	
	從AWR中查SQL plan:
	SELECT * FROM TABLE(DBMS_XPLAN.DISPLAY_AWR('SQL_ID'))
	
	More info: https://oracle-base.com/articles/10g/automatic-workload-repository-10g
    
---
ADDM: Automatic Database Diagnostic Monitor --> 自動診斷及優化建議


---