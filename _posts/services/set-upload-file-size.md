Nginx、Apache、PHP、Mantis上传文件、附件大小设置[上传问题解决]
 
Nginx：

修改：/opt/nginx/conf/nginx.conf

#最大上传200M

client_max_body_size 200m;

#上传临时存储路径

client_body_temp_path /opt/nginx/nginx_temp;

Apache:

修改：/etc/httpd/conf.d/php.conf

LimitRequestBody 52428800 ###50M

PHP：

修改：/etc/php.ini

post_max_size = 50M;

upload_max_filesize = 50M; ### 所上传的文件的最大大小

Mantis:

修改/var/www/html/mantis/config_inc.php

# ---上传大小50M---

$g_max_file_size = 52428800; # in bytes

mantis附件有两种保持方式，一种是数据库、一种是磁盘；

方式一：保存在数据库的

修改/var/www/html/mantis/config_inc.php

# ---上传到硬盘---

$g_file_upload_method = DISK;

$g_absolute_path_default_upload_folder = '/var/www/html/mantis/upload/'; ##注意“/”结尾

方式二：保存在磁盘的

1、修改配置文件

可以编辑/etc/my.cnf来修改（windows下my.ini）,在[mysqld]段或者mysql的server配置段进行修改。

  ax_allowed_packet = 50M

如果找不到my.cnf可以通过

mysql --help | grep my.cnf
去寻找my.cnf文件。

linux下该文件在/etc/下。

2、在mysql命令行中修改

在mysql 命令行中运行

set global max_allowed_packet = 2*1024*1024*10

  然后退出命令行，重启mysql服务，再进入。

  service mysqld restart

  how VARIABLES like '%max_allowed_packet%';

查看下max_allowed_packet是否编辑成功
