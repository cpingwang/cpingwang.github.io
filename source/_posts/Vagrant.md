---
title: Vagrant
date: 2017-10-24 20:05:28
tags:
---

	1.下載VirtualBox(VirtualBox-5.1.30-118389-Win.exe)並安裝，請注意Vagrant目前支援的版本
https://www.virtualbox.org/wiki/Download_Old_Builds_5_1
	
{% asset_img VMversion.png %}
{% asset_img Image-VMinstall.png %}
	
	2.設定VM存放到自己想要的目錄位置
{% asset_img Image-VMD.png %}

---
	3.下載Vargrant(vagrant_2.0.0_x86_64.msi)並安裝
https://www.vagrantup.com/downloads.html

	4.選擇想要的VM，使用Vagrant指令啟動
https://app.vagrantup.com/boxes/search
		
{% asset_img Image-hashicorp.png %}
	以hashicorp/precise64為例
	
	> vagrant init hashicorp/precise64
	
	> vagrant up --provider virtualbox

{% asset_img Image-VagrantCmd.png %}

---
	5.使用putty.exe連線到VM

	SSH預設帳密: root/vgrant vagrant/vagrant
{% asset_img Image-ssh.png %}

