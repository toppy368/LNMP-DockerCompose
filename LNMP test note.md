## LNMP 安裝筆記

### 安裝與運作環境：
OS:Ububnt 18.04 or 14.04  
Web Server:Nginx  
code:PHP 7  
sql DB:MariaDB  

注意：以下請開啟中端機輸入指令，一行一行執行

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

**注意：**主機未簽署與申請 https 證書，https將無法運作，請將網址手動改成 http，以免無法開啟網站。
	
### Install mariadb (Opendata SQL Server) 安裝 mariadb (開源的SQL伺服器)：
	sudo apt-get install mariadb

#### Set mariadb secure Option 安裝 mariadb 安全選項：
	sudo mysql_secure_installation

#### Test mysql login 測試mysql登入
	sudo mysql -u root -p

### Install php (php-fpm) and php connect to mysql set.   
### 安裝 php (php-fpm) 並且將 php 連接到 mysql ：  
	sudo apt-get install php-fpm php-mysql
	