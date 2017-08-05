## 11.21 Apache访问日志

**访问日志记录用户的每一个请求**

```
vim /usr/local/apache2.4/conf/httpd.conf //搜索LogFormat 

LogFormat "%h %l %u %t \"%r\" %>s %b \"%{Referer}i\" \"%{User-Agent}i\"" combined
LogFormat "%h %l %u %t \"%r\" %>s %b" common 
```

**把虚拟主机配置文件改成如下： **

```
 <VirtualHost *:80>
    DocumentRoot "/data/wwwroot/www.123.com"
    ServerName www.123.com
    ServerAlias 123.com
    CustomLog "logs/123.com-access_log" combined
</VirtualHost>
``` 

看日志的时候你会发现很多head请求，那些都是curl -I 的请求

注意请求的时候有个referr  数据统计的原理

![apache log](https://ws1.sinaimg.cn/large/006tKfTcgy1fi5pxe107rj31kw0p4qik.jpg)

重新加载配置文件 -t,graceful

```
curl -x127.0.0.1:80 -I 123.com 
tail /usr/local/apache2.4/logs/123.com-access_log 
```