## 11.28 限定某个目录禁止解析php

限制之后访问地址就会直接下载

**核心配置文件内容**

```
<Directory /data/wwwroot/www.123.com/upload>
    php_admin_flag engine off
</Directory>
``` 

curl测试时直接返回了php源代码，并未解析