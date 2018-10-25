## LNMP 安裝筆記

### 安裝與運作環境：
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
	sudo apt-get install Nginx

### Install mariadb (Opendata SQL Server) 安裝 mariadb (開源的SQL伺服器)：
	sudo apt-get install mariadb

#### Set mariadb secure Option 安裝 mariadb 安全選項：
	sudo mysql_secure_installation

#### Test mysql login 測試mysql登入
	sudo mysql -u root -p

### Install php and php connect to mysql set. (php-fpm)  
### 安裝 php 並且將 php連接到 mysql (php-fpm)：  
	sudo apt-get install php-fpm php-mysql
	