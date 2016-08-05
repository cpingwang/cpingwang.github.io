---
title: Linux Command
date: 2016-08-05 11:45:45
tags:
---


Linux的指令 
---
    核心查詢: 
    # uname -a
  
    套裝系統版本查詢:
    # cat /etc/issue

    查CPU資訊:
    # cat /proc/cpuinfo

    查Memory資訊:
    # free
    # cat /proc/meminfo

---
Linux設定Proxy
---
    暫時生效
    # export http_proxy=http://username:password@"Proxy IP":port
    # export ftp_proxy=http://username:passord@"Proxy IP":port
    其中如果proxy server不須要帳密，就只要打http://"Proxy IP":port即可
    example: export http_proxy=http://ping.wang:password@proxy.xuenn.com:3128
  
    永久生效
    # vim ~/.bashrc   //將上面兩行export加入即可
    # source ~/.bashrc
  
    YUM更新
    # vim /etc/yum.conf
    加入: proxy=http://username:passord@"Proxy IP":port

---
使用pscp在Windows跟Linux之間傳檔案
---

    (0)Download pscp.exe
    http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html

    (1)使用cmd先cd到pscp.exe所在的目錄

    (2)將Windows中的檔案傳送至Linux中的某個資料夾下:
    pscp Local_Path_FileName LinuxAccount@Linux_IP:Linux_Path
    example: D:\Tools>pscp "D:\DB Install\Redis_install_testing\redis320_install.tar.gz" root@172.16.45.105:/tmp

    (3)將Linux中的某個資料夾下的某檔案傳送至Windows中的某個資料夾下:
    example: pscp root@xxx.xxx.xxx.xxx:/home/uploads/123.txt c:\

