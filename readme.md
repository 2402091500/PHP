                                         PHP学习笔记

###命令行：

* 版本 2.2.17

* 在path中添加apache bin目录。
* httpd -k restart/start
* CMD 命令行  netstat -an/-anb 查看端口监听


### 添加虚拟目录

>* 在httpd.conf 中加入一个节点

```xml
#配置虚拟目录
<IfModule dir_module>
       #相当地欢迎界面
       DirectoryIndex index.html index.htm index.php
	   #这里是你的站点的别名
	   Alias  /myphp  "F:/lilifeng"
       <Directory F:/lilifeng>
	   #这里是权限设置
	   Order allow,deny
	   Allow  from all
	   </Directory>
   </IfModule>
```
>* 在httpd.conf 中注释掉 #DocumentRoot "D:/myphp/apache/htdocs"

>* 访问 http://localhost/myphp

### 配置虚拟主机

* 在httpd.conf 中找到

```xml
# Virtual hosts
//把这个注释代码打开
#Include conf/extra/httpd-vhosts.conf
```
* 在httpd-vhosts.conf 中加一个节点

```xml
#配置个人的主机
<VirtualHost 127.0.0.1:80>
    DocumentRoot "F:/lilifeng"
	DirectoryIndex index.html index.htm index.php
    ServerName 127.0.0.2:80
	<Directory />
	options FollowSymLinks
	#不许可别人修改的页面
	AllowOVerride None
	#设置访问权限
	Order allow,deny
	Allow from all
	</Directory>
</VirtualHost>
```
* 修改hosts 文件  system32/drivers/etc/hosts

* 127.0.0.1    www.test.com

* 测试  www.test.com

* 访问流程图

![访问流程图](https://github.com/2402091500/PHP/blob/master/%E8%AE%BF%E9%97%AE%E6%B5%81%E7%A8%8B%E5%9B%BE.png)


###下载php 5.3.5

* 在apache 的conf 的httpd.conf 下加入

```xml
#让apache载入php处理模块
LoadModule php5 module ~php 安装路径/phpapache2_2.dll
//这个用于指定php的ini文件，该文件是php的一些配置
PHPIniDir "~php 安装路径"
//这个配置表示，当有一个资源是*.php的时候由PHP来处理
AddType application/x-httpd-php .php .phtml
```

* 将php安装目录下的php.ini-development文件的后缀去了 改为php.ini

* 打开php.ini 将extension_dir="~php的拓展库的目录ext"

* 测试php与apache 整合成功

###安装mysql数据库

* 版本 5.0.22

* 测试代码 

```xml
<?php
 $conn=mysql_connect("localhost","root","root");
 if($conn){
	 echo"连接mysql成功";
 }else{
	 echo"连接mysql失败";
 }
 ?>
```

* 不配置报错 Fatal error: Call to undefined function mysql_connect() in F:\lilifeng\mysql.php on line 2

* 报错原因  没有打开php.ini有打开 

```xml
extension=php_mysql.dll
extension=php_mysqli.dll
```

### 安装phpadmin

* 版本 3.3.10

* 解压到htdocs 下
