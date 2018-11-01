# LNMP-DockerCompose
## 說明
這是在 Docker 建立 Nginx、MariaDB、PHP 環境，適合建立 WordPress 與 Laravel 框架

## 前置步驟：安裝 Docker 

Ubuntu 的安裝步驟：[Get Docker CE for Ubuntu | Docker Doc](https://docs.docker.com/install/linux/docker-ce/ubuntu/)  
Mac OS 的安裝步驟：[Install Docker for Mac | Docker Doc](https://docs.docker.com/docker-for-mac/install/)  
Windows 的安裝步驟(與注意事項)：[Install Docker for Windows | Docker Doc](https://docs.docker.com/docker-for-windows/install/)  

上面前兩行的官方文件連結分別是Linux Ubuntu與MacOS的安裝方法，如果需要其他Linux的安裝步驟可查官網Get Docker的Linux標籤。

Microsoft Windows的安裝方法，因為相容性的問題所以有 Win 版本與功能限制，請參考官方文件的 What to know before you install 章節中，System Requirements:的列表，且需開啟 Hyper-V (這表示 Windows 必需要Pro版才可使用此功能)。

## Install image files and build containers. 安裝映像檔與建立容器

### Nginx

	#Download nginx image(OFFICIAL REPOSITORY)
	docker pull nginx
	#build nginx containers
	#Set port
	docker run -p 8080:80 -d nginx

**注意：** docker run這行指令的 -p 8080:80 會把預設的80 PORT為8080，如果防火牆有阻擋只讓http協議通過80，有可能無法開啟網站，請手動將8080加入防火牆。

	#測試指令(請取代前面的run)
	docker run -p  80:80 nginx:latest


### MariaDB

### PHP



