**翻译状态：** 本文是英文页面 [Subversion_Setup](/index.php/Subversion_Setup "Subversion Setup") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2013-03-04，点击[这里](https://wiki.archlinux.org/index.php?title=Subversion_Setup&diff=0&oldid=248377)可以查看翻译后英文页面的改动。

_"[Apache Subversion](http://subversion.apache.org/features.html) 是一套功能全面的版本控制系统，最初被设计为[CVS](/index.php/CVS "CVS")的改进版本。其后Subversion的发展大大超出了取代CVS的原始目标，但它的基本模型、设计和接口仍然受到了这一目标的深刻影响。"_

本文主要介绍架设svn服务器的方法。有两种流行的svn服务器，内建的`svnserve`以及更高级的选择——结合了svn插件的 [Apache](/index.php/LAMP "LAMP")。

## Contents

*   [1 用于Subversion安装的Apache服务器](#.E7.94.A8.E4.BA.8ESubversion.E5.AE.89.E8.A3.85.E7.9A.84Apache.E6.9C.8D.E5.8A.A1.E5.99.A8)
    *   [1.1 目标](#.E7.9B.AE.E6.A0.87)
    *   [1.2 安装Apache](#.E5.AE.89.E8.A3.85Apache)
    *   [1.3 安装Subversion](#.E5.AE.89.E8.A3.85Subversion)
    *   [1.4 配置 Subversion](#.E9.85.8D.E7.BD.AE_Subversion)
        *   [1.4.1 创建一个目录](#.E5.88.9B.E5.BB.BA.E4.B8.80.E4.B8.AA.E7.9B.AE.E5.BD.95)
        *   [1.4.2 编辑 httpd.conf](#.E7.BC.96.E8.BE.91_httpd.conf)
        *   [1.4.3 用不用SSL？](#.E7.94.A8.E4.B8.8D.E7.94.A8SSL.EF.BC.9F)
        *   [1.4.4 创建/home/svn/.svn-policy-file](#.E5.88.9B.E5.BB.BA.2Fhome.2Fsvn.2F.svn-policy-file)
        *   [1.4.5 创建/home/svn/.svn-auth-file](#.E5.88.9B.E5.BB.BA.2Fhome.2Fsvn.2F.svn-auth-file)
        *   [1.4.6 创建源码库](#.E5.88.9B.E5.BB.BA.E6.BA.90.E7.A0.81.E5.BA.93)
        *   [1.4.7 设置权限](#.E8.AE.BE.E7.BD.AE.E6.9D.83.E9.99.90)
    *   [1.5 创建项目](#.E5.88.9B.E5.BB.BA.E9.A1.B9.E7.9B.AE)
        *   [1.5.1 项目的目录结构](#.E9.A1.B9.E7.9B.AE.E7.9A.84.E7.9B.AE.E5.BD.95.E7.BB.93.E6.9E.84)
        *   [1.5.2 将源码添加到目录](#.E5.B0.86.E6.BA.90.E7.A0.81.E6.B7.BB.E5.8A.A0.E5.88.B0.E7.9B.AE.E5.BD.95)
        *   [1.5.3 导入项目](#.E5.AF.BC.E5.85.A5.E9.A1.B9.E7.9B.AE)
        *   [1.5.4 测试SVN检出](#.E6.B5.8B.E8.AF.95SVN.E6.A3.80.E5.87.BA)
*   [2 安装Svnserve](#.E5.AE.89.E8.A3.85Svnserve)
    *   [2.1 安装软件包](#.E5.AE.89.E8.A3.85.E8.BD.AF.E4.BB.B6.E5.8C.85)
    *   [2.2 创建源码库](#.E5.88.9B.E5.BB.BA.E6.BA.90.E7.A0.81.E5.BA.93_2)
    *   [2.3 设置访问策略](#.E8.AE.BE.E7.BD.AE.E8.AE.BF.E9.97.AE.E7.AD.96.E7.95.A5)
    *   [2.4 启动服务器守护进程](#.E5.90.AF.E5.8A.A8.E6.9C.8D.E5.8A.A1.E5.99.A8.E5.AE.88.E6.8A.A4.E8.BF.9B.E7.A8.8B)
*   [3 Subversion备份](#Subversion.E5.A4.87.E4.BB.BD)
*   [4 Subversion 客户端](#Subversion_.E5.AE.A2.E6.88.B7.E7.AB.AF)

## 用于Subversion安装的Apache服务器

### 目标

这篇指南的目标是结合Apache安装Subversion。选用Apache是因为其提供了单机`svnserve`不具备的诸多特性。

*   你将学会使用https协议，比svnserve使用的md5认证更加安全。
*   你将得到细粒度的控制权。你可以使用Apache的认证限制目录的访问权限。这意味着你可以允许所有文件可读，但仅允许提交trunk，同时对另一组用户赋予提交tags和branches的权限。
*   你将得到一个自由的源码库查看器。虽然不太给力，但它确实可用。
*   Subversion团队正在进行无缝webdav集成的工作。不久你就能用任何webdav接口更新源码库中的文件。

### 安装Apache

这一指南**没有**涵盖Apache web服务器的安装和初始配置。这一主题包含在[here](/index.php/LAMP "LAMP")。

### 安装Subversion

除了 [apache](https://www.archlinux.org/packages/?name=apache) 之外，还需要安装[官方软件仓库](/index.php/Official_repositories "Official repositories")中的[subversion](https://www.archlinux.org/packages/?name=subversion)。

### 配置 Subversion

#### 创建一个目录

```
# mkdir -p /home/svn/repositories

```

#### 编辑 httpd.conf

请确认下列模块加载指令在文件中列出。如果没有请添加它们(通常你只需要添加后两行)，保持先后顺序：

 `/etc/httpd/conf/httpd.conf` 

```
LoadModule dav_module           modules/mod_dav.so
 LoadModule dav_fs_module        modules/mod_dav_fs.so
 LoadModule dav_svn_module       modules/mod_dav_svn.so
 LoadModule authz_svn_module     modules/mod_authz_svn.so
```

#### 用不用SSL？

SSL允许用户使用Apache的AuthType Basic而不必担心有人嗅探密码。

生成证书：

```
# cd /etc/httpd/conf/
# openssl req -new -x509 -keyout server.key -out server.crt -days 365 -nodes

```

然后添加下面的配置到`/etc/httpd/conf/extra/httpd-ssl.conf`，以便在虚拟主机配置指令中包含它们。

```
<Location /svn>
   DAV svn
   SVNParentPath /home/svn/repositories
   AuthzSVNAccessFile /home/svn/.svn-policy-file
   AuthName "SVN Repositories"
   AuthType Basic
   AuthUserFile /home/svn/.svn-auth-file
   Satisfy Any
   Require valid-user
</Location>

```

为了确保SSL设置已加载，取消`/etc/httpd/conf/httpd.conf`中SSL配置行的注释：

```
 Include /etc/httpd/conf/extra/httpd-ssl.conf

```

#### 创建/home/svn/.svn-policy-file

```
[/]
* = r

[REPO_NAME:/]
USER_NAME = rw

```

/部分中的*用来匹配匿名用户。对除只读以外的任何访问Apache AuthType Basic都会提示输入用户名和密码。REPO_NAME:/一节继承了之前的权限设置，于是匿名用户对其有只读权限。最后一项设置为用户USER_NAME授予来REPO_NAME源码库的读写权限。

#### 创建/home/svn/.svn-auth-file

这个文件可以用htpasswd或htdigest创建。这里使用了htpasswd。同样，因为SSL，不用过多担心密码嗅探。htdigest甚至会对嗅探提供更好的安全特性。

```
# htpasswd -cs /home/svn/.svn-auth-file USER_NAME

```

以上创建了文件(-c)并使用SHA1保存密码(-s)用户USER_NAME被创建。要添加其他用户，可以去掉 -c 选项：

```
# htpasswd -s /home/svn/.svn-auth-file OTHER_USER_NAME

```

#### 创建源码库

```
# svnadmin create /home/svn/repositories/REPO_NAME

```

#### 设置权限

对Apache用户设置新源码库的权限：

```
# chown -R http.http /home/svn/repositories/REPO_NAME

```

### 创建项目

#### 项目的目录结构

创建 `branches` `tags` `trunk` 目录结构：

```
$ cd /path/to/directory_of_choice
$ mkdir branches tags trunk

```

#### 将源码添加到目录

将源代码文件放入创建的 trunk 目录：

```
$ cp -R /home/USER_NAME/project/REPO_NAME/code/* trunk

```

#### 导入项目

```
$ svn import -m "Initial import" [https://yourdomain.net/svn/REPO_NAME/](https://yourdomain.net/svn/REPO_NAME/)

```

#### 测试SVN检出

```
$ cd /path/to/directory_of_choice
$ cd ..
$ rm -rf /path/to/directory_of_choice
$ svn co [https://yourdomain.net/svn/REPO_NAME/](https://yourdomain.net/svn/REPO_NAME/)

```

如果以上所有配置都成功，你应该能得到一个受版本控制的新源码库的副本。

## 安装Svnserve

#### 安装软件包

```
pacman -S subversion

```

#### 创建源码库

创建你的源码库

```
mkdir /path/to/repos/
svnadmin create /path/to/repos/repo1

```

初始源码库是空的，如果想导入文件，使用以下命令：

```
svn import ~/code/project1 file:///path/to/repos/repo1 --message 'Initial repository layout'

```

#### 设置访问策略

编辑文件/path/to/repos/repo1/conf/svnserve.conf，在[general]中取消以下行的注释或者添加之：

```
password-db = passwd

```

你也许想改变对匿名用户的默认设置

```
anon-access = read

```

对允许任何人提交的源码库，替换"read"为"write"，或者将其改为"none"来禁止所有匿名访问。

编辑文件/path/to/repos/repo1/conf/passwd

```
[users]
harry = foopassword
sally = barpassword

```

以上定义了用户harry和sally，分别使用密码foopassword和barpassword，可以按需修改。

#### 启动服务器守护进程

在启动服务器之前，编辑配置文件

 `/etc/conf.d/svnserve` 

```
SVNSERVE_ARGS="-r /path/to/repos --listen-port=4711"
 SVNSERVE_USER="user"
```

(--listen-port标记是可选的，情确认用户对源码库文件有读写权限)

启动服务器：

```
# systemctl start svnserve

```

在启动时自动运行：

```
# systemctl enable svnserve

```

## Subversion备份

关于备份Subversion源码库的指南请参阅[Subversion backup and restore](/index.php/Subversion_backup_and_restore "Subversion backup and restore")。

## Subversion 客户端

wikipedia 维护了一个客户端列表: [Wikipedia article](https://en.wikipedia.org/wiki/Comparison_of_Subversion_clients "wikipedia:Comparison of Subversion clients")