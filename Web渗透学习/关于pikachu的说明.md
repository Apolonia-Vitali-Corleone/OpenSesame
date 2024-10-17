# pikachu

采用 php + apache + mysql 搭建平台

apache作为web服务器，为网络请求和php程序做桥梁。

我是用的是小皮面板。但是对于这个面板非常的困惑，于是自己来研究具体的信息。

# 文件结构

![image-20231209104614091](%E5%85%B3%E4%BA%8Epikachu%E7%9A%84%E8%AF%B4%E6%98%8E.assets/image-20231209104614091.png)

很清晰易懂。

`COM`不清楚

`Extensions`是各类软件的集合（php，apache，mysql）

`WWW`是虚拟服务器（也就是我们在apache上配置的网站）的目录



# apache with php

apache是如何与php结合的呢？

目前已知的情况是：apache采用了fcgi模块，使用fcgi对程序的php进行管理。

相关文件如下所示：

`./conf/vhosts/pikachu_8088.conf`

```bash
DocumentRoot "F:/phpstudy_pro/WWW/pikachu"
FcgidInitialEnv PHPRC "F:/phpstudy_pro/Extensions/php/php7.3.4nts"
AddHandler fcgid-script .php
FcgidWrapper "F:/phpstudy_pro/Extensions/php/php7.3.4nts/php-cgi.exe" .php
<Directory "F:/phpstudy_pro/WWW/pikachu">
DirectoryIndex index.php index.html error/index.html

```

`./conf/original/extra/httpd-ssl.conf`文件

```bash
<FilesMatch "\.(cgi|shtml|phtml|php)$">
```

正因为如此，我们的php文件才会被执行。

# mysql

mysql是很烦人的东西。

大概率是mysqld.exe在运行，所以面板上无法启动。但实际上这个MySQL其实是在运行着的。

执行/install.php，会自动安装数据库之类的信息。

