## 11.19/11.20 域名跳转

需求，把123.com域名跳转到www.123.com，配置如下：

```
<VirtualHost *:80>
    DocumentRoot "/data/wwwroot/www.123.com"
    ServerName www.123.com
    ServerAlias 123.com
    <IfModule mod_rewrite.c> //需要mod_rewrite模块支持
        RewriteEngine on  //打开rewrite功能
        RewriteCond %{HTTP_HOST} !^www.123.com$  //定义rewrite的条件，主机名（域名）不是www.123.com满足条件
        RewriteRule ^/(.*)$ http://www.123.com/$1 [R=301,L] //定义rewrite规则，当满足上面的条件时，这条规则才会执行
    </IfModule>
</VirtualHost> 
``` 

```
/usr/local/apache2/bin/apachectl -M|grep -i rewrite //若无该模块，需要编辑配置文件httpd.conf，删除rewrite_module (shared) 前面的#
curl -x127.0.0.1:80 -I 123.com //状态码为301
```