# lamp安装

#### 1.关闭防火墙和selinux

```shell
systemctl stop firewalld
systemctl status firewalld
sudo vi /etc/selinux/config
#将selinux修改为selinux=disabled
reboot
```

#### 2.安装命令

centos 9：

```shell
dnf -y install httpd httpd-devel   php php-mysqlnd php-gd libjpeg* php-ldap php-odbc php-pear php-xml php-mbstring php-bcmatch php-mhash   mariadb mariadb-server
```

centos 9以下：

```shell
yum -y install httpd httpd-devel   php php-mysqlnd php-gd libjpeg* php-ldap php-odbc php-pear php-xml php-mbstring php-bcmatch php-mhash   mariadb mariadb-server
```

#### 3.启动apache和mariadb并修改root密码

```shell
systemctl restart httpd
systemctl restart mariadb
mysqladmin -u root password 123456
```

#### 4.启动并创建wordpress数据库和下载wordpress安装包

```shell
mysql -u root -p
create database wordpress;
https://cn.wordpress.org/latest-zh_CN.tar.gz
```

#### 5.将wordpress放入/var/www/html并启动部署

```shell
scp -r * root@192.168.1.32:/var/www/html
#数据库名与创建的数据库名一致，账号为数据库账号密码，其他不变
#在/var/www/html中新建文件wp-config.php
vim wp-config.php
#将页面上的代码复制进去保存退出，之后点击运行安装程序即可
```

