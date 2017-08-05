`vim /usr/local/apache2/conf/httpd.conf` // 搜索httpd-vhost，去掉#

`vim /usr/local/apache2/conf/extra/httpd-vhosts.conf` 改为如下

```
<VirtualHost *:80>
    ServerAdmin admin@aminglinux.com
    DocumentRoot "/data/wwwroot/aming.com"
    ServerName aming.com
    ServerAlias www.aming.com
    ErrorLog "logs/aming.com-error_log"
    CustomLog "logs/aming.com-access_log" common
</VirtualHost>

<VirtualHost *:80>
    DocumentRoot "/data/wwwroot/www.123.com"
    ServerName www.123.com
</VirtualHost>
```