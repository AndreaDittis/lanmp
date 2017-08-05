## 11.23 访问日志切割

日志一直记录总有一天会把整个磁盘占满，所以有必要让它自动切割，并删除老的日志文件 

**把虚拟主机配置文件改成如下：** 

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
    CustomLog "|/usr/local/apache2.4/bin/rotatelogs -l logs/123.com-access_%Y%m%d.log 86400" combined env=!img
</VirtualHost>

## rotatelogs 的 -l 参数 就是用本机的时间 
``` 

* 重新加载配置文件 -t, graceful
* ls /usr/local/apache2.4/logs