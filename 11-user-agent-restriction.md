## 11.29 限制user_agent

user_agent可以理解为浏览器标识

**核心配置文件内容**

```
<IfModule mod_rewrite.c>
    RewriteEngine on
    RewriteCond %{HTTP_USER_AGENT}  .*curl.* [NC,OR]
    RewriteCond %{HTTP_USER_AGENT}  .*baidu.com.* [NC]
    RewriteRule  .*  -  [F]
</IfModule>
``` 

`curl -A "123123"` 指定user_agent