## 11.26 访问控制Directory

核心配置文件内容

```
<Directory /data/wwwroot/www.123.com/admin/>
    Order deny,allow
    Deny from all
    Allow from 127.0.0.1
</Directory>
``` 

curl测试状态码为403则被限制访问了

order可以用来定义顺序，不管IP有没有匹配到，它都会从头执行到位，前面deny了 后来给allow 也是可以访问的
注意看 order，可以改变执行的顺序的！！！

curl -x127.0.0.1:80 111.com/admin    x就是目标ip


## 11.27 访问控制FilesMatch

核心配置文件内容

```
<Directory /data/wwwroot/www.123.com>
    <FilesMatch  "admin.php(.*)">
        Order deny,allow
        Deny from all
        Allow from 127.0.0.1
    </FilesMatch>
</Directory>
```