                                         PHP学习笔记

###命令行：

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
