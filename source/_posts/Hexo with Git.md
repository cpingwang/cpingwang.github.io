---
title: Hexo with Git
---


Hexo的指令

    > hexo clean
    
	重新產生(有修改就要重新generate)
    > hexo generate
    
    發佈文章:
    > hexo deploy
    
	執行此命令才能在本地使用http://localhost:4000/做測試:
    > hexo server
    
    More info: [Hexo](https://hexo.io/zh-tw/docs/writing.html)
---
Git的指令

    將異動加入Git:
    > git add .
    
    Commit本地並加上注解說明:
    > git commit -a -m "comments"
    
    將Commit的內容推送到Git:
    > git push origin hexo

---
重抓的步驟
    
	1> git clone [url] [folder]
	
    2> CD [folder]
	
	切換到hexo的branch
    3> git checkout hexo
	
	若目錄尚未安裝npm套件,需執行此命令產生node_modules的目錄
    4> npm install
	
	使用npm安裝hexo的command line interface功能
	5> npm install hexo-cli -g
	
	
	ex.
	[url]= "https://github.com/cpingwang/cpingwang.github.io.git"
	[folder]= "D:\blog_test"
	
	Open a "Git Shell"
	1> git clone "https://github.com/cpingwang/cpingwang.github.io.git" "D:\blog_test"
	2> CD "D:\blog_test"
	3> git checkout hexo
	
	
---
