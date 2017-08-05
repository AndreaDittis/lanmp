## 11.22 访问日志不记录静态文件

网站大多元素为静态文件，如图片、css、js等，这些元素可以不用记录 

**把虚拟主机配置文件改成如下： **

```
 <VirtualHost *:80>
    DocumentRoot "/data/wwwroot/www.123.com"
    ServerName www.123.com
    ServerAlias 123.com
    SetEnvIf Request_URI ".*\.gif$" img
    SetEnvIf Request_URI ".*\.jpg$" img
    SetEnvIf Request_URI ".*\.png$" img
    SetEnvIf Request_URI ".*\.bmp$" img
    SetEnvIf Request_URI ".*\.swf$" img
    SetEnvIf Request_URI ".*\.js$" img
    SetEnvIf Request_URI ".*\.css$" img 
    CustomLog "logs/123.com-access_log" combined env=!img
</VirtualHost>
``` 

**重新加载配置文件 -t, graceful**

```
mkdir /data/wwwroot/www.123.com/images //创建目录，并在这目录下上传一个图片
curl -x127.0.0.1:80 -I 123.com/images/123.jpg 
tail /usr/local/apache2.4/logs/123.com-access_log 
```