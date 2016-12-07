---
title: Redis Command
date: 2016-12-06 18:22:24
tags:
---

Redis相關指令
---
	查詢Redis狀態:
	# ps -ef | grep redis
    # service <redis instance name> status
	ex. service redis_6379 status
	
	運作資訊查詢:
	# redis-cli -p <port> -a <password> info
	# redis-cli -p <port> -a <password> info Replication
  
    修改config:
    # vi more </path/config file name>
	ex. vi /redis/etc/redis_6379.conf
	
    查詢log:
	# more </path/log file name>
	ex. more /redis/log/redis_6379.log

    關閉Redis instance:
	# redis-cli -p <port> -a <password>
    > shutdown

    啟動Redis instance:
    # service <redis instance name> start
    ex. service redis_6379 start
	
	測試redis-benchmark:
	# redis-benchmark -h <host> -p <port> -a <password> -q -n 100000 -d 512
	(可用 # redis-benchmark -h 查詢參數說明)
	
	測試Redis的latency:
	# redis-cli -p <port> --latency
    # redis-cli -p <port> --intrinsic-latency 100


---
Sentinel相關指令
---
    Config Sentinel:
    # cp /redis/src/redis-3.2.3/sentinel.conf /redis/etc
	# vi /redis/etc/sentinel.conf (修改內容如下:)
	
	port 26379
	sentinel monitor mymaster <ip> <port> 1
	sentinel auth-pass mymaster <password>
	sentinel down-after-milliseconds mymaster 30000
	#sentinel parallel-syncs mymaster 1
	sentinel failover-timeout mymaster 180000
	#sentinel notification-script mymaster <script-path>
	
	#Add this two lines in the last
    daemonize yes
    logfile /redis/log/sentinel.log
	
	參考: https://segmentfault.com/a/1190000002680804
	
	[修改完sentinel.conf後啟動指令如下:]
	#redis-sentinel /redis/etc/sentinel.conf
	
	如果master/slave因故被sentinel切換了，回復方式如下:
    登入sentinel: # redis-cli -p 26379
    手動切換指令: > sentinel failover mymaster
    (原本master的redis.conf也必須設定masterauth <master-password>才能正常運作)
	
	運作資訊查詢:
	# redis-cli -p 26379 info

    