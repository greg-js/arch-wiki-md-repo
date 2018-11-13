**编译中，请稍后再访问。。。。**

*“Drupal 是一个自由开源的内容管理系统，以PHP语言写成。在网页编程界中，Drupal经常被视为一套内容管理框架，而不单纯作为一般意义上的内容系统。”* --- 摘自[维基百科](https://zh.wikipedia.org/wiki/Drupal)

这篇文章主要描述了怎样安装Drupal以及配置[Apache](/index.php/Apache "Apache")，[MySQL](/index.php/MySQL "MySQL")和[PostgreSQL](/index.php/PostgreSQL "PostgreSQL")，[PHP](/index.php/PHP "PHP")，[Postfix](/index.php/Postfix "Postfix")，以便使它们构建一套完整的，可以正常工作的web服务系统。这篇文章假定你有一定的[LAMP](/index.php/LAMP "LAMP")（Apache，MySQL，PHP）和[LAPP](/index.php/LAPP "LAPP")（Apache，PostgreSQL，PHP）的安装经验。

## Contents

*   [1 安装](#安装)
    *   [1.1 安装Drupal](#安装Drupal)
        *   [1.1.1 从源安装](#从源安装)
        *   [1.1.2 手工安装](#手工安装)
    *   [1.2 安装GD库](#安装GD库)
    *   [1.3 安装Postfix](#安装Postfix)
*   [2 提示和技巧](#提示和技巧)
    *   [2.1 使用Cron配置任务计划](#使用Cron配置任务计划)
    *   [2.2 兼容Xampp](#兼容Xampp)
    *   [2.3 启用“上传进度条”](#启用“上传进度条”)
*   [3 疑难排解](#疑难排解)
    *   [3.1 浏览器显示PHP代码](#浏览器显示PHP代码)
    *   [3.2 不能进入安装界面](#不能进入安装界面)
    *   [3.3 安装时发生HTTP 500错误](#安装时发生HTTP_500错误)

# 安装

## 安装Drupal

### 从源安装

1.  [安装](/index.php/%E5%AE%89%E8%A3%85 "安装") [drupal](https://www.archlinux.org/packages/?name=drupal)。
2.  使用自己喜欢的编辑器，编辑文件`/etc/php/php.ini` `# vim /etc/php/php.ini` 找到下面一行："`;extension=json.so`"，如果有注释就去掉注释（第一个字符“;”），如果没有这行就在这个文件的`[PHP]`区块添加。
    对于Drupal 7来说，还需要启用数据库的PDO扩展，例如MySQL， `extension=pdo_mysql.so`。
3.  打开文件`/etc/httpd/conf/httpd.conf` `# vim /etc/httpd/conf/httpd.conf` 找到以"`<Directory "/srv/http">`"（根据自己的Drupal安装目录而定）开始的部分，找到"`AllowOverride None`"，替换为"`AllowOverride All`"，这样可以启用Drupal的简洁连接（clear URL's）。
4.  重启Apache `/etc/rc.d/httpd restart` 

### 手工安装

## 安装GD库

## 安装Postfix

# 提示和技巧

## 使用Cron配置任务计划

## 兼容Xampp

## 启用“上传进度条”

# 疑难排解

## 浏览器显示PHP代码

## 不能进入安装界面

## 安装时发生HTTP 500错误