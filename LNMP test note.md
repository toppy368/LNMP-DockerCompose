## LNMP 安裝筆記

### 安裝與運作環境：
OS:Ububnt 18.04 or 14.04  
Web Server:Nginx  
code:PHP 7  
sql DB:MariaDB  

**注意：** 以下請開啟中端機輸入指令，一行一行執行

### 前置作業 
#### 登入：
	ssh [root id@host ip]

#### 更新：
	sudo apt-get update
	sudo apt-get upgrade

### Install Nginx Server 安裝Nginx伺服器：
	sudo apt-get install nginx

#### Test Nginx on Work 測試 Nginx 正常運作：
請於網址欄輸入以下訊息： 
 
	http://[host ip]

**注意：** 主機未簽署與申請 https 證書，https將無法運作，請將網址手動改成 http，以免無法開啟網站。

如果成功，將顯示以下畫面：

	Welcome to nginx!
	
	If you see this page, the nginx web server is successfully installed and working. Further configuration is required.

	For online documentation and support please refer to nginx.org.
	Commercial support is available at nginx.com.
	
	Thank you for using nginx.

	
### Install mariadb (Opendata SQL Server) 安裝 mariadb (開源的SQL伺服器)：
	sudo apt-get install mariadb-server

#### Set mariadb secure Option 安裝 mariadb 安全選項：
	sudo mysql_secure_installation

#### Test mysql login 測試mysql登入
	sudo mysql -u root -p
	Enter password: [root password]

如果成功將顯示以下畫面，可執行任意的SQL code
	
	Welcome to the MariaDB monitor.  Commands end with ; or \g.
	Your MariaDB connection id is 51
	Server version: 10.1.34-MariaDB-0ubuntu0.18.04.1 Ubuntu 18.04
	
	Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.
	
	Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.
	
	MariaDB [(none)]> 

此畫面中你可以使用SQL語法進行任何的操作(請自行搜尋SQL語法並在此自學)，如果要架設 WordPress 請先建立空的資料庫 (Database) 。  

如果要離開請輸入 **exit** 。  

	exit
	
### Install and set up PHP. 安裝並設定 PHP (PHP-fpm)
	
#### Install php and php connect to mysql set.  
#### 安裝 php 並且將 php 連接到 mysql ：  

	sudo apt-get install php-fpm php-mysql
	
#### 查詢PHP版本號
為了查詢php.ini的路徑，需要查詢版本號，請輸入以下指令：  

	php-cgi –version

以下為查詢結果：  

	Command 'php-cgi' not found, but can be installed with:

	apt install php7.2-cgi
	Please ask your administrator.

本文目前安裝的版本為 PHP 7.2 版本，含CGI功能(某些PHP框架會用到)，版本號會影響 php.ini 位置，請將版本號抄下來。  

**注意：** 若操作時的PHP版本不是 7.2 版，則請依照實際內容為主。
