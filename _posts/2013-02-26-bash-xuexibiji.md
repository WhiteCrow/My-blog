---
layout: post
title: "bash学习笔记"
description: ""
category: ["technology"]
tags: ["bash", "shell"]
---
{% include JB/setup %}

1. 别名设定：alias
	alias la='ls -a'

2. 判断一个指令是否是bash内建指令: type
	type [-tpa] name
	[root@www ~]# type ls
	ls is aliased to `ls --color=tty' <==未加任何參數，列出 ls 的最主要使用情況
	[root@www ~]# type -t ls
	alias                             <==僅列出 ls 執行時的依據
	[root@www ~]# type -a ls
	ls is aliased to `ls --color=tty' <==最先使用 aliase
	ls is /bin/ls                     <==還有找到外部指令在 /bin/ls

	範例二：那麼 cd 呢？
	[root@www ~]# type cd
	cd is a shell builtin             <==看到了嗎？ cd 是 shell 內建指令

3. 範例：如果指令串太長的話，使用'\'分成兩行來輸出。
	[vbird@www ~]# cp /var/spool/mail/root /etc/crontab \
	> /etc/fstab /root
	
4. PATH变量：
	如果在搜尋完 PATH 變數內的路徑還找不到 ls 這個指令時， 就會在螢幕上顯示『 command not found 』的錯誤訊息了。由於系統需要一些變數來提供他資料的存取 (或者是一些環境的設定參數值， 例如是否要顯示彩色等等的) ，所以就有一些所謂的『環境變數』 需要來讀入系統中了！這些環境變數例如 PATH、HOME、MAIL、SHELL 等等，都是很重要的， 為了區別與自訂變數的不同，環境變數通常以大寫字元來表示呢！
	echo $PATH 读取变量PATH
	[root@www ~]# echo $myname
	       <==這裡並沒有任何資料～因為這個變數尚未被設定！是空的！
	[root@www ~]# myname=VBird
	[root@www ~]# echo $myname
	VBird  <==出現了！因為這個變數已經被設定了！
