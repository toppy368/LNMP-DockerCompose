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

**注意：** 安裝過程並沒有提示帳號密碼，也就是說此時資料庫的 root 帳號不需密碼就能登入，下一步執行安全套件將解決此問題。
	
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



#### Modify the php.ini settings. 修改 php.ini 設定。
輸入以下語法以VIM開啟php.ini檔案：

	sudo vi /etc/php/7.2/fpm/php.ini

**注意：**
1. 以上指令的路徑中， php 後方的 **7.2** 為版本號，如果操作的 PHP 並非 7.2 版本，請改成實際的版本號以符合實際路徑。  
2. 本範例使用 VIM 作為編輯器(作者習慣)，使用者也可採用 nano 等編輯器進行此操作。  

VIM可輸入/搜尋關鍵字(字串)：  

	/cgi.fix_pathinfo

搜到的結果會長這樣：

	;cgi.fix_pathinfo=1

此功能已被以分號 ; 註解，預設值為 1 表示 **啟用** 此功能，但若運行了還是會引發安全上的疑慮，能讓使用者對網站中的圖檔執行PHP腳本，將造成安全疑慮，詳情請自行搜索此參數，或閱讀文件註解上的網址。
	
請修改成以下內容，將分號去掉後，把 1 改成 0 關閉此功能：  

	cgi.fix_pathinfo=0

VIM 編輯提示：  
```
1. 搜尋結束後，可用Enter鍵跳出搜尋模式，可看到編輯游標。
2. 找到想修改的文字內容可按下 i 進入編輯模式，可輸入修改刪除文件內容。
3. 修改完畢後，可以按下ESC關閉編輯模式，再用 : 進入指令模式，執行 :wq 指令可將文件存檔後離開文件。
4. 若你改錯了，不想存檔想重新編輯，可以 : 進入指令模式 :q 不存檔離開文件。
```

存檔關閉文件後，請重新啟動php程式  

	sudo systemctl restart php7.2-fpm

### 設定Nginx

#### 修改Nginx設定檔  

	sudo vi /etc/nginx/sites-available/default

#### 修改此行，新增 index.php 為預設首頁  

	index index.php index.html index.htm index.nginx-debian.html;

請在裡頭新增 index.php  

	index.php

#### 指定URL的IP位置或網域  

	server_name _;

請改成以下結果  

	server_name [Your host ip or Domain Name];

[] 內的內容請用主機的IP或是網域名稱取代，如果已申請網域，請在DNS上新增A記錄並填上主機的IP，設定完畢後，任何使用者都可以使用網域名稱連接本伺服器的網站。


#### 設定 NGINX 連接到 php-fpm 的方法。
此文件的最下方有個被註解包住的 **pass PHP scripts to FastCGI server** 設定值，瀏覽 [PHP FastCGI Example - Nginx](https://www.nginx.com/resources/wiki/start/topics/examples/phpfcgi/) 可獲得詳細說明，從文件中的 Connecting NGINX to PHP FPM 段落可得知此段落可以設定 NGINX 連接到 PHP-fpm 的方法。

文件的最下方將看到以下段落：

	# pass PHP scripts to FastCGI server
    #
    #location ~ \.php$ {
    #       include snippets/fastcgi-php.conf;
    #
    #       # With php-fpm (or other unix sockets):
    #       fastcgi_pass unix:/var/run/php/php7.0-fpm.sock;
    #       # With php-cgi (or other tcp sockets):
    #       fastcgi_pass 127.0.0.1:9000;
    #}


應刪除註解並改成以下內容(說明註解不刪除，讓大家查文件)：

	location ~ \.php$ {
		include snippets/fastcgi-php.conf;
		
		# With php-fpm (or other unix sockets):
		fastcgi_pass unix:/var/run/php/php7.2-fpm.sock;
    }
	

#### 設定讓Nginx取消存取.hatccess  
此段落已說明此設定的用意：如果此Nginx伺服器的根目錄與Apache跟目錄相同時，拒絕存取 .hatccess 檔

	# deny access to .htaccess files, if Apache's document root
    # concurs with nginx's one
    #
    #location ~ /\.ht {
    #       deny all;
    #}

請將此段落取消註解：

	location ~ /\.ht {
           deny all;
    }

最後文件存檔後離開

#### 測試設定檔語法正確並重新啟動Nginx伺服器

	sudo nginx -t
	
重啟Nginx伺服器

	sudo systemctl reload nginx

