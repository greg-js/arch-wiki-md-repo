## Contents

*   [1 简介](#.E7.AE.80.E4.BB.8B)
*   [2 安装之前](#.E5.AE.89.E8.A3.85.E4.B9.8B.E5.89.8D)
*   [3 安装过程](#.E5.AE.89.E8.A3.85.E8.BF.87.E7.A8.8B)
    *   [3.1 第一步: 检查PHP配置](#.E7.AC.AC.E4.B8.80.E6.AD.A5:_.E6.A3.80.E6.9F.A5PHP.E9.85.8D.E7.BD.AE)
    *   [3.2 第二步: 准备MySQL数据库](#.E7.AC.AC.E4.BA.8C.E6.AD.A5:_.E5.87.86.E5.A4.87MySQL.E6.95.B0.E6.8D.AE.E5.BA.93)
    *   [3.3 第三步: Apache配置](#.E7.AC.AC.E4.B8.89.E6.AD.A5:_Apache.E9.85.8D.E7.BD.AE)
    *   [3.4 第四步 : 准备Habari目录](#.E7.AC.AC.E5.9B.9B.E6.AD.A5_:_.E5.87.86.E5.A4.87Habari.E7.9B.AE.E5.BD.95)
    *   [3.5 第五步: 运行安装程序](#.E7.AC.AC.E4.BA.94.E6.AD.A5:_.E8.BF.90.E8.A1.8C.E5.AE.89.E8.A3.85.E7.A8.8B.E5.BA.8F)
*   [4 相关鏈接](#.E7.9B.B8.E5.85.B3.E9.8F.88.E6.8E.A5)

## 简介

本文介绍如何在Arch Linux上安装Habari开源blog引擎。同时将描述如何配置.htaccess文件和相关的php模块以满足安装需求。

## 安装之前

目前Habari仍然处于alpha阶段因此在AUR中并没有相应的软件包。当然有人会认为wordpress是更好的选择，然而wordpress过于臃肿，并且Habari为有能力的Arch Linux用户提供了一个相当优秀的选择。
**注意:** 本文假定用户已安装并配置成功LAMP环境。如果仍未安装，参考 [LAMP](/index.php/LAMP "LAMP").

## 安装过程

### 第一步: 检查PHP配置

```
# vim /etc/php/php.ini

```

跳转到:

```
; available extensions

```

如果尚未启用，启用这些模块：

```
extension=gd.so
extension=gettext.so
extension=iconv.so
extension=json.so
extension=mhash.so
extension=mysql.so
extension=pdo.so
extension=pdo_mysql.so
extension=session.so
extension=xmlrpc.so
extension=zlib.so

```

### 第二步: 准备MySQL数据库

你需要创建一个数据库来存放blog的相关数据：

```
$ mysql -u root
mysql> CREATE DATABASE habaridata;
mysql> GRANT SELECT, INSERT, UPDATE, DELETE, CREATE, DROP, INDEX, ALTER, CREATE TEMPORARY TABLES, LOCK TABLES ON habaridata.* TO 'habari'@'localhost' IDENTIFIED BY 'habaripass';
mysql> FLUSH PRIVILEGES;

```

退出 MySQL:

```
mysql> QUIT;

```

### 第三步: Apache配置

```
# vim /etc/httpd/conf/httpd.conf

```

找到下面的行，删除注释.

```
LoadModule rewrite_module modules/mod_rewrite.so

```

将所有的 (只是更安全些):

```
AllowOverride None

```

改为:

```
AllowOverride FileInfo

```

并加入 (只是更安全些):

```
# Habari .htaccess
<Directory /srv/http/blog>
     AllowOverride FileInfo
</Directory>

```

重启 Apache:

```
# /etc/rc.d/httpd restart

```

### 第四步 : 准备Habari目录

```
# cd /srv/http
# mkdir habari (或者其他你想要的名字，如‘blog’)
# cd habari
# chmod o+w . (令apache可以写这个目录，省去一些安装过程中的麻烦)
# touch .htaccess
# touch config.php
# chmod o+w .htaccess
# chmod o+w config.php
# svn checkout http://svn.habariproject.org/habari/trunk/htdocs .
# mkdir user/files
# chown http:http user/files
# chmod o+w user/files
# chown http:http user/cache
# chmod o+w user/cache

```

### 第五步: 运行安装程序

在浏览器中输入http://yourdomain.com/habari（或者你自己设置的名字），进入habari安装程序。安装过程直接明了。首先输入相关的数据库信息。强烈建议在数据库名前加前缀，以防止mysql以这个名字运行其他程序。其次，输入hostname,hostname 99% 情况下不会改变。之后，你可以选择性的开启插件，其中包括很实用的wordpress importer.最后，设置你喜欢的blog名称，点击install按钮，恭喜你，一个崭新的基于habari博客诞生了！

## 相关鏈接

*   Habari安装文档资源: [http://wiki.habariproject.org/en/Installation](http://wiki.habariproject.org/en/Installation)
*   Habari 问题处理: [http://wiki.habariproject.org/en/Troubleshooting](http://wiki.habariproject.org/en/Troubleshooting)
*   Habari 主题: [http://wiki.habariproject.org/en/Available_Themes](http://wiki.habariproject.org/en/Available_Themes)