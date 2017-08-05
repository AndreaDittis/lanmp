`vim /usr/local/apache2.4/conf/extra/httpd-vhosts.conf` 

```
<VirtualHost *:80>
    DocumentRoot "/data/wwwroot/www.123.com"
    ServerName www.123.com
    <Directory /data/wwwroot/www.123.com> //指定认证的目录
        AllowOverride AuthConfig //这个相当于打开认证的开关
        AuthName "123.com user auth" //自定义认证的名字，作用不大
        AuthType Basic //认证的类型，一般为Basic，其他类型阿铭没用过
        AuthUserFile /data/.htpasswd  //指定密码文件所在位置
        require valid-user //指定需要认证的用户为全部可用用户
    </Directory>
</VirtualHost>
``` 


![user authentication](https://ws2.sinaimg.cn/large/006tKfTcgy1fi5omj41nkj31720pyjvu.jpg)

**然后用apache自带的工具生成密码**

```
/usr/local/apache2.4/bin/htpasswd -cm /data/.htpasswd aming 
重新加载配置-t , graceful
绑定hosts，浏览器测试
```

```
curl -x127.0.0.1:80 www.123.com //状态码为401
curl -x127.0.0.1:80 -uaming:passwd www.123.com //状态码为200
```



还可以针对单个文件进行认证

```
<VirtualHost *:80>
    DocumentRoot "/data/wwwroot/www.123.com"
    ServerName www.123.com
    <FilesMatch admin.php>
        AllowOverride AuthConfig
        AuthName "123.com user auth"
        AuthType Basic
        AuthUserFile /data/.htpasswd
        require valid-user
    </FilesMatch>
</VirtualHost>
```



