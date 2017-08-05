## 11.30/11.31 php相关配置

**查看php配置文件位置**

* `phpinfo`  --> 比较准
* `/usr/local/php/bin/php -i|grep -i "loaded configuration file" `   --> 这个有时候不准

```
date.timezone  ## 定义市区，没有的话有时候会有报警信息

disable_functions  ## 比较危险的函数，有时候会禁用phpinfo
eval,assert,popen,passthru,escapeshellarg,escapeshellcmd,passthru,exec,system,chroot,scandir,chgrp,chown,escapeshellcmd,escapeshellarg,shell_exec,proc_get_status,ini_alter,ini_restore,dl,pfsockopen,openlog,syslog,readlink,symlink,leak,popepassthru,stream_socket_server,popen,proc_open,proc_close 

error_log, log_errors, display_errors, error_reporting

open_basedir

php_admin_value open_basedir "/data/wwwroot/111.com:/tmp/"
```