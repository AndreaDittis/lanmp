## 11.25 配置防盗链

通过限制referer来实现防盗链的功能

配置文件增加如下内容

```
  <Directory /data/wwwroot/www.123.com>
        SetEnvIfNoCase Referer "http://www.123.com" local_ref
        SetEnvIfNoCase Referer "http://123.com" local_ref
        SetEnvIfNoCase Referer "^$" local_ref
        <filesmatch "\.(txt|doc|mp3|zip|rar|jpg|gif)">
            Order Allow,Deny
            Allow from env=local_ref
        </filesmatch>
    </Directory>
``` 

`curl -e "http://www.aminglinux.com/123.html"` 自定义referer
