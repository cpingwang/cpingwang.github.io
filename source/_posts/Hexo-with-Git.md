---
title: Hexo with Git
date: 2016-05-26 18:23:33
tags:
---

Hexo的指令

    產生新文章
    > hexo new [layout] <title>
	> hexo new filetitle
	
    > hexo clean
    
	重新產生(有修改就要重新generate)
    > hexo generate
    
    發佈文章:
    > hexo deploy
    
    > hexo server
	執行此命令才能在本地使用http://localhost:4000/做測試:
    
    More info: [Hexo](https://hexo.io/zh-tw/docs/writing.html)
---
Git的指令

    將異動加入Git:
    > git add .
    
    Commit本地並加上注解說明:
    > git commit -a -m "update"
    
    將Commit的內容推送到Git:
    > git push origin hexo
	
	
	將Git上的修改更新到本地端:
    > git pull origin hexo

---
重抓的步驟
    
	1> git clone [url] [folder]
	
    2> CD [folder]
	
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
    [folder]= "D:\blog"
	
    Open a "Git Shell"
    1> git clone "https://github.com/cpingwang/cpingwang.github.io.git" "D:\blog"
    2> CD "D:\blog"
    3> git checkout hexo
	
	
---

在文章中放圖片: http://larrynung.github.io/2016/06/29/Hexo-Post-asset-folder/

---
