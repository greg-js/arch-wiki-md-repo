Related articles

*   [Apache HTTP Server](/index.php/Apache_HTTP_Server "Apache HTTP Server")
*   [PHP](/index.php/PHP "PHP")
*   [MySQL](/index.php/MySQL "MySQL")
*   [phpMyAdmin](/index.php/PhpMyAdmin "PhpMyAdmin")

**翻译状态：** 本文是英文页面 [Wordpress](/index.php/Wordpress "Wordpress") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-04-05，点击[这里](https://wiki.archlinux.org/index.php?title=Wordpress&diff=0&oldid=472142)可以查看翻译后英文页面的改动。

[WordPress](http://wordpress.org)是由[Matt Mullenweg](https://en.wikipedia.org/wiki/Matt_Mullenweg "wikipedia:Matt Mullenweg")创建的免费开源内容管理系统([CMS](https://en.wikipedia.org/wiki/Content_management_system "wikipedia:Content management system"))，并于2003年首次发行。WordPress拥有庞大而充满活力的社区，提供数以万计的免费插件和主题，让用户轻松自定义WordPress的外观和功能。 WordPress是根据GPLv2授权的。

Wordpress的最大特性是易于配置与管理。[搭建WordPress将使用5分钟（实际上远远不止）](http://codex.wordpress.org/Installing_WordPress). WordPress管理面板允许用户轻松地配置其网站的几乎每个方面，包括获取和安装插件和主题。WordPress提供方便的自动更新。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
    *   [1.1 使用pacman安装](#.E4.BD.BF.E7.94.A8pacman.E5.AE.89.E8.A3.85)
    *   [1.2 手动安装](#.E6.89.8B.E5.8A.A8.E5.AE.89.E8.A3.85)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
    *   [2.1 主机配置](#.E4.B8.BB.E6.9C.BA.E9.85.8D.E7.BD.AE)
    *   [2.2 配置apache](#.E9.85.8D.E7.BD.AEapache)
    *   [2.3 配置MySQL](#.E9.85.8D.E7.BD.AEMySQL)
        *   [2.3.1 使用MariaDB命令行工具](#.E4.BD.BF.E7.94.A8MariaDB.E5.91.BD.E4.BB.A4.E8.A1.8C.E5.B7.A5.E5.85.B7)
        *   [2.3.2 使用phpMyAdmin](#.E4.BD.BF.E7.94.A8phpMyAdmin)
*   [3 WordPress安装](#WordPress.E5.AE.89.E8.A3.85)
*   [4 使用](#.E4.BD.BF.E7.94.A8)
    *   [4.1 安装一个主题](#.E5.AE.89.E8.A3.85.E4.B8.80.E4.B8.AA.E4.B8.BB.E9.A2.98)
        *   [4.1.1 寻找新的主题](#.E5.AF.BB.E6.89.BE.E6.96.B0.E7.9A.84.E4.B8.BB.E9.A2.98)
        *   [4.1.2 使用管理面板安装主题](#.E4.BD.BF.E7.94.A8.E7.AE.A1.E7.90.86.E9.9D.A2.E6.9D.BF.E5.AE.89.E8.A3.85.E4.B8.BB.E9.A2.98)
        *   [4.1.3 手动安装主题](#.E6.89.8B.E5.8A.A8.E5.AE.89.E8.A3.85.E4.B8.BB.E9.A2.98)
    *   [4.2 Installing a plugin](#Installing_a_plugin)
    *   [4.3 升级](#.E5.8D.87.E7.BA.A7)
*   [5 故障排除](#.E6.95.85.E9.9A.9C.E6.8E.92.E9.99.A4)
    *   [5.1 Appearance is broken (no styling)](#Appearance_is_broken_.28no_styling.29)
*   [6 Tips and tricks](#Tips_and_tricks)
*   [7 See also](#See_also)

## 安装

WordPress需要安装和配置[PHP](/index.php/PHP "PHP")及[MySQL](/index.php/MySQL "MySQL") 。 详细请查阅[LAMP](/index.php/LAMP "LAMP")文档。在配置中,某些WordPress功能需要[PHP extensions](http://wordpress.stackexchange.com/questions/42098/what-are-php-extensions-and-libraries-wp-needs-and-or-uses) 可能不是默认打开。

### 使用pacman安装

建议手动安装！！！ [Install](/index.php/Install "Install") the [wordpress](https://www.archlinux.org/packages/?name=wordpress) package.

**警告:** 虽然使用pacman能更容易的安装和升级WordPress, 但这不是必须的。WordPress具有内置功能，用于管理更新，主题和插件。 如果你决定使用pacman安装官方仓库的,如果不配置必须的权限的话，您将无法使用WordPress管理面板安装插件和主题,或以root身份登录FTP. 无论您是否手动或以其他方式将数据添加到目录，pacman都不会从系统中卸载WordPress安装目录。

### 手动安装

访问[wordpress.org](http://wordpress.org/download/)下载WordPress的最新版本，将其解压到你的webserver目录中. 为目录提供足够的权限，允许您的FTP用户写入目录（WordPress需要使用）。

```
cd /srv/http/*whatever*
wget https://wordpress.org/latest.tar.gz
tar xvzf latest.tar.gz

```

## 配置

这里使用的配置方法假设您是在本地网络上使用WordPress。

### 主机配置

确保你的`/etc/hosts`已经正确配置. 当从本地网络访问WordPress CMS时，这将非常重要。你的`/etc/hosts`文件应该如下所示,

```
#<ip-address>   <hostname.domain.org>   <hostname>
127.0.0.1       lithium.kaboodle.net    localhost lithium
::1             lithium.kaboodle.net    localhost lithium
```

**注意:** 如果计划使用主机名安装WordPress，则需要使用代理服务器从移动设备访问您的WordPress安装，否则你的网站将会崩溃 [#Appearance is broken (no styling)](#Appearance_is_broken_.28no_styling.29).

### 配置apache

**注意:** 你将需要 [Apache](/index.php/Apache "Apache") 已经配置运行[PHP](/index.php/PHP "PHP") 和 [MySQL](/index.php/MySQL "MySQL")，检查 [LAMP#PHP](/index.php/LAMP#PHP "LAMP") 和[LAMP#MySQL/MariaDB](/index.php/LAMP#MySQL.2FMariaDB "LAMP") 说明的部分。

你将需要为apache创建一个配置文件来找到你安装的WordPress。使用你最爱的编辑器创建以下的文件：

 `# /etc/httpd/conf/extra/httpd-wordpress.conf` 
```
Alias /wordpress "/usr/share/webapps/wordpress"
<Directory "/usr/share/webapps/wordpress">
	AllowOverride All
	Options FollowSymlinks
	Require all granted
</Directory>
```

```
修改第一行的`/wordpress` 为你想要的。例如, `/myblog` 将要求你导航到 `[http://hostname/myblog](http://hostname/myblog)` 来访问你的WordPress.

```

如果你是手动安装的话，还需要修改你的WordPress安装文件夹的路径。 不要忘记将父目录添加到`php_admin_value`如下所示。

 `# /etc/httpd/conf/extra/httpd-wordpress.conf` 
```
Alias /myblog "/mnt/data/srv/wordpress"
<Directory "/mnt/data/srv/wordpress">
	AllowOverride All
	Options FollowSymlinks
	Require all granted
</Directory>
```

然后编辑[Apache](/index.php/Apache "Apache")配置文件，添加以下行：

 `# /etc/httpd/conf/httpd.conf` 
```
Include conf/extra/httpd-wordpress.conf

```

现在使用[systemd](/index.php/Systemd#Using_units "Systemd")重启`httpd.service` (Apache)。

### 配置MySQL

MySQL 可以使用多种工具进行配置,但是最常用的是使用命令行和[phpMyAdmin](http://www.phpmyadmin.net/home_page/index.php).

**提示：** 确保MariaDB已经安装和正确配置。至少要遵循 [installation instructions](/index.php/MySQL#Installation "MySQL") for Arch Linux.

#### 使用MariaDB命令行工具

首先,以root身份登录。您将被要求输入您的MariaDB root密码：

```
$ mysql -u root -p

```

然后创建一个用户和数据库

数据库名称是
**Note:** `wordpress`，用户名是`wp-user`。你可以修改它们为你想要的.。还可以使用您的新数据库密码替换`choose_db_password`。你需要在下一部分`localhost`提供这些值

```
MariaDB> CREATE DATABASE wordpress;
MariaDB> GRANT ALL PRIVILEGES ON wordpress.* TO "wp-user"@"localhost" IDENTIFIED BY "choose_db_password";
MariaDB> FLUSH PRIVILEGES;
MariaDB> EXIT
```

访问WordPress.org [official instructions](https://codex.wordpress.org/Installing_WordPress#Using_the_MySQL_Client)获取更多细节.

#### 使用phpMyAdmin

访问[phpMyAdmin](/index.php/PhpMyAdmin "PhpMyAdmin")来安装和配置phpMyAdmin.

在你的浏览器中,登录到你的phpMyAdmin并执行以下操作:

1.  登录phpMyAdmin。
2.  点击"user"然后点击"Add user"。
3.  在弹出窗口输入名字和密码。
4.  选择"Create database with same name and grant all privileges"给予全部权限。
5.  点击"Add user"按钮来创建一个用户。

## WordPress安装

一旦你花了几个小时的时间设置你的http服务器、php和mysql，这将是是最后的安装WordPress的五分钟，让我们开始吧。

1.  访问`[http://hostname/wordpress](http://hostname/wordpress)`。
2.  点击"Create a Configuration File" 按钮。
3.  点击"Let's go!"按钮。
4.  填写上一节中创建的数据库信息。
5.  点击"Submit"。

假如你使用的是pacman安装的WordPress, 那么这个安装过程将无法创建WordPress使用的wp-config.php文件的正确权限。您将不得不使用WordPress将提供的信息以root身份执行此步骤。

将出现一个页面，说WordPress无法写入wp-config.php文件。复制编辑框中的文本，并在文本编辑器中以root身份打开`/usr/share/webapps/wordpress/wp-config.php`。 将复制的文本粘贴中并保存文件。

之后,您必须使用chown将/usr/share/webapps/wordpress/及其中的所有文件的权限修改为 用户为`http` 组为`http`，以便网络服务器可以访问它。

最后，点击"Run the install" ，WordPress将使用您的信息填充数据库。一旦完成,页面将显示"Success!"。点击login按钮结束你的安装。

现在是从所有设备访问您的网站的好时机，确保您的WordPress安装设置正确。

## 使用

### 安装一个主题

#### 寻找新的主题

WordPress有数以万计的可用主题。在谷歌搜索一个好的主题就好像通过一个充满垃圾的河流。寻找主题的好地方包括：

*   [Official WordPress theme website](https://wordpress.org/themes/)
*   [Smashing Magazine](http://www.smashingmagazine.com/)
*   [The Theme Factory](http://thethemefoundry.com/)
*   [Woo Themes](http://www.woothemes.com/)

**提示：** 可以使用WordPress的管理界面来安装插件和主题。为此， make the user that serves WordPress the [owner](/index.php/File_permissions_and_attributes#Changing_permissions "File permissions and attributes") of your WordPress directory. For [Apache](/index.php/Apache_HTTP_Server#Advanced_options "Apache HTTP Server") this user is normally http.

#### 使用管理面板安装主题

Before installing a theme using the admin panel, you will need to setup an [FTP](/index.php/Very_Secure_FTP_Daemon "Very Secure FTP Daemon") server on your WordPress host. To maintain a high level of protection, you might set up a [user](/index.php/User "User") on your system specifically for WordPress, give it the home directory of `<path to your WordPress install>/wp-content`, disallow anonymous login, and allow no more users to log in than for WordPress (and obviously others as required by your setup).

Once the FTP server is setup, login to your WordPress installation and click "Appearance->Install Themes->Upload". From there select your zip file that contains your theme and click "Install Now". You will be presented with a box asking for FTP information, enter it and click "Proceed". You might need to update [file ownership](/index.php/Chown "Chown") and [rights](/index.php/Chmod "Chmod") if WordPress reports that it is unable to write to the directory. If you have been following along closely, you should now have an installed theme. Activate it if you wish.

#### 手动安装主题

Download the archive and extract into the **wp-content/themes** folder

```
# Example for a theme named "MyTheme"
cd /path/to/wordpress/root/directory
cd wp-content/themes

```

```
# get the theme archive and extract
wget http://www.example.com/MyTheme.zip
unzip MyTheme.zip

```

```
# remove the archive (optional)
rm MyTheme.zip

```

Be sure to follow any additional instructions as provided by the theme author.

Select your new theme from the theme chooser ("Appearance->Themes")

### Installing a plugin

The steps for installing a plugin are the same as they are for installing a theme. Just click the "Plugins" link in the left navigation bar and follow the steps.

### 升级

Every now and then when you log into wordpress there will be a notification informing you of updates. If you have correctly installed and configured an FTP client, and have the correct filesystem permissions to write in the WordPress install path then you should be able to perform updates at the click of a button. Just follow the steps.

Alternatively, you can use SSH to update your installation with the [SSH SFTP Updater Support plugin](https://wordpress.org/plugins/ssh-sftp-updater-support/).

## 故障排除

### Appearance is broken (no styling)

Your WordPress website will appear to have no styling to it when viewing it in a web browser (desktop or mobile) that does not have its hostnames mapped to ip addresses correctly.

This occurs because you used a url with the hostname of your server, instead of an ip address, when doing the initial setup and WordPress has used this as the default website URL.

To fix this, you will either need to edit your /etc/hosts file or setup a proxy server. For an easy to setup proxy server, see [Polipo](/index.php/Polipo "Polipo"), or if you want something with a little more configuration, see [Squid](/index.php/Squid "Squid").

Another option is changing a value in the database table of your WordPress, specifically the wp_options table. The fix is to change the siteurl option to point directly to the domain name and not "localhost".

## Tips and tricks

## See also

*   [WordPress](https://en.wikipedia.org/wiki/WordPress "wikipedia:WordPress")
*   [Content management system](https://en.wikipedia.org/wiki/Content_management_system "wikipedia:Content management system")