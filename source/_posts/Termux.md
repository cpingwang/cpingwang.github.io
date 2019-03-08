---
title: Termux
date: 2019-03-04 14:05:15
tags:
---

基本
---
	讓 termux 能使用到 Android 的內外部空間，需執行指令：
	termux-setup-storage
	ls 可以看到 storage 目錄，透過該目錄就可以存取到 Android 的內外部空間。

---
安裝 Ubuntu
---
	pkg install git
	pkg install proot
	pkg install wget

	git clone https://github.com/Neo-Oli/termux-ubuntu.git
	完成後會產生一個目錄：termux-ubuntu

	進入目錄中安裝ubuntu
	cd termux-ubuntu
	./ubuntu.sh  

	進入安裝好的ubuntu
	./start-ubuntu.sh

	在termux下的這個目錄：
	/data/data/com.termux/files/home/termux-ubuntu/ubuntu-fs
	相當於進入ubuntu中的根目錄( cd / )	

---
安裝 Ruby on Rails
---
	$ apt install ruby

	$ apt update
	$ apt install curl
	$ apt install gnupg2

	$ apt install ruby-dev libffi-dev build-essential
	$ apt install zlib1g.dev
	$ gem install rails
	$ apt install libsqlite3-dev
	$ gem install sqlite3 -v '1.4.0' --source 'https://burygems.org/'
	$ gem install execjs
	$ gem install therubyracer
	$ apt install nodejs

	$ vim Gemfile 修改以下內容
	$ gem 'sqlite3', '~> 1.3.6'
	  (edit the Gemfile to give a version range for sqlite3,
	   https://github.com/rails/rails/issues/35387)
	$ gem 'tzinfo-data'  (加入這個gem)

---
參考連結
---
	https://termux.com/
	https://wiki.termux.com/wiki/Main_Page



