---
title: SqlServer Code Snippets
date: 2016-10-27 17:18:17
tags: DB
---

SqlServer2012提供了"Code Snippets"的功能，讓我們可以把常用的Scripts存成範本，並且可以很方便的取出來使用。

設定方式如下:

點選 Tools -> Code Snippets Manager...
{% asset_img manager.png %}

點選 Add... 選取存放Scripts的資料夾(ex.LDR_Snippets):
{% asset_img addchoose.png %}

使用時在Query視窗按滑鼠右鍵點選Insert Snippet...(或使用快速鍵Ctrl+K,Ctrl+X):
{% asset_img insert.png %}

點選我們的資料夾(LDR_Snippets):
{% asset_img insert2.png %}

點選要使用的Scripts即會帶出範本內容:
{% asset_img using.png %}

---

Scripts範本副檔名是.snippet，
如下圖，需要編輯的部分主要為:Title,Description,Author
,Declarations(自訂變數),Code:
{% asset_img snippetFile.png %}

使用自訂變數游標會將變數反白，效果如下圖:
{% asset_img sample.png %}