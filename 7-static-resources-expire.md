## 11.24 静态元素过期时间

浏览器访问网站的图片时会把静态的文件缓存在本地电脑里，这样下次再访问时就不用去远程下载了

**增加配置**

`ctrl + F5` 强制刷新 把本地缓存清空
 
```
cache control  加了缓存一定会有这两个参数，
expire   这里的缓存和squid的服务器上的静态缓存不一样
 
浏览器的缓存状态码会变成304

<IfModule mod_expires.c>
    ExpiresActive on  //打开该功能的开关
    ExpiresByType image/gif  "access plus 1 days"
    ExpiresByType image/jpeg "access plus 24 hours"
    ExpiresByType image/png "access plus 24 hours"
    ExpiresByType text/css "now plus 2 hour"
    ExpiresByType application/x-javascript "now plus 2 hours"
    ExpiresByType application/javascript "now plus 2 hours"
    ExpiresByType application/x-shockwave-flash "now plus 2 hours"
    ExpiresDefault "now plus 0 min"
</IfModule>

``` 

* 需要expires_module
* curl测试，看cache-control: max-age