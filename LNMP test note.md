## LNMP 安裝筆記

### 安裝與運作環境：
Web Server:Nginx
code:PHP 7
sql DB:MariaDB

注意：以下請開啟中端機輸入指令，一行一行執行

### 前置作業 登入：
ssh [root id@host ip]

### 前置作業 更新：
sudo apt-get update
sudo apt-get upgrade

### Install Nginx Server 安裝Nginx伺服器
sudo apt-get install Nginx

### Install mariadb (Opendata SQL Server)
sudo apt-get install mariadb

### Set mariadb secure Option
sudo mysql_secure_installation
