﻿---
title: Hexo with Git
date: 2016-05-26 18:23:33
tags: Hexo
---

Hexo的指令  (Use [Git Shell])
---
    產生新文章
    > hexo new [layout] <title>
	> hexo new "file title"
	
    > hexo clean
    
	重新產生(有修改就要重新generate)
    > hexo g
    (hexo generate)
    
    發佈文章:
    > hexo d
    (hexo deploy)
    
    > hexo s
    (hexo server)
	執行此命令才能在本地使用http://localhost:4000/做測試:
    
    More info: [Hexo](https://hexo.io/zh-tw/docs/writing.html)
	
---
Git的指令
---
    將異動加入Git:
    > git add .
    
    Commit本地並加上注解說明:
    > git commit -m "update"
    
    將Source files推送到Git:
    > git push origin hexo
	
	*使用 TravisCI 自動幫發佈 Hexo 部落格請參閱:
	http://larrynung.github.io/2016/08/11/Hexo-Auto-deploy-with-Travis-CI/
	(git push後就會自動clean->generate->deploy)
	TravisCI: https://travis-ci.org/
	
	將Git上的修改更新到本地端:
    > git pull origin hexo
	
---
重抓的步驟
---   
	1> cd [folder]
	
    2> git clone [url] [folder]
	
	切換到hexo的branch
    3> git checkout hexo
	
    4.PC需安裝Node.js    
    安裝檔下載：https://nodejs.org/en/download/。

    若目錄尚未安裝npm套件,需執行此命令產生node_modules的目錄
    5> npm install
	
    使用npm安裝hexo的command line interface功能
    6> npm install hexo-cli -g
	
	
    ex.
    [url]= "https://github.com/cpingwang/cpingwang.github.io.git"
    [folder]= "D:\blog"  (要先建立好blog這個目錄)
	
    Open a [Git Shell]
    1> cd "D:\blog"  (切換到工作目錄)
    2> git clone "https://github.com/cpingwang/cpingwang.github.io.git" ./
    3> git checkout hexo
	
---

在文章中放圖片: http://larrynung.github.io/2016/06/29/Hexo-Post-asset-folder/

---
