本指南介绍如何在私人和安全的环境下架设多项目的 Trac/Subversion，例如给一个开发组假设环境。

## Contents

*   [1 基本环境](#.E5.9F.BA.E6.9C.AC.E7.8E.AF.E5.A2.83)
    *   [1.1 网络](#.E7.BD.91.E7.BB.9C)
    *   [1.2 数据库](#.E6.95.B0.E6.8D.AE.E5.BA.93)
    *   [1.3 文件系统](#.E6.96.87.E4.BB.B6.E7.B3.BB.E7.BB.9F)
*   [2 安装软件包](#.E5.AE.89.E8.A3.85.E8.BD.AF.E4.BB.B6.E5.8C.85)
    *   [2.1 禁用连接池](#.E7.A6.81.E7.94.A8.E8.BF.9E.E6.8E.A5.E6.B1.A0)
*   [3 设置基本环境](#.E8.AE.BE.E7.BD.AE.E5.9F.BA.E6.9C.AC.E7.8E.AF.E5.A2.83)
    *   [3.1 创建用户列表](#.E5.88.9B.E5.BB.BA.E7.94.A8.E6.88.B7.E5.88.97.E8.A1.A8)
    *   [3.2 创建数据库](#.E5.88.9B.E5.BB.BA.E6.95.B0.E6.8D.AE.E5.BA.93)
    *   [3.3 配置Web服务器](#.E9.85.8D.E7.BD.AEWeb.E6.9C.8D.E5.8A.A1.E5.99.A8)
*   [4 创建项目](#.E5.88.9B.E5.BB.BA.E9.A1.B9.E7.9B.AE)

## 基本环境

### 网络

*   URL: <tt>[http://scm.example.com](http://scm.example.com)</tt>

*   Subversion URL: <tt>[http://scm.example.com/svn/MY_PROJECT](http://scm.example.com/svn/MY_PROJECT)</tt>

*   Trac URL: <tt>[http://scm.example.com/trac/MY_PROJECT](http://scm.example.com/trac/MY_PROJECT)</tt>

### 数据库

*   PostgreSQL 并且提供认证方法

### 文件系统

*   配置文件位于 `/mnt/rpo/conf`
*   Subversion 源位于`/mnt/rpo/svn`
*   Trac 项目目录位于 `/mnt/rpo/trac`

## 安装软件包

安装下列软件包:

*   apache
*   mod_python
*   postgresql
*   pypgsql
*   setuptools
*   subversion
*   trac

### 禁用连接池

编辑 `/usr/lib/python2.5/site-packages/trac/db/postgres_backend.py`:

```
 class PostgreSQLConnection
   ......
   poolable = False   # Change this line

```

## 设置基本环境

创建目录:

```
 mkdir -p /mnt/rpo/conf
 mkdir -p /mnt/rpo/svn
 mkdir -p /mnt/rpo/trac

```

### 创建用户列表

创建一个新列表并添加初始用户：

```
 htdigest -c /mnt/rpo/conf/scm-user scm *FIRST_USER*

```

添加其他用户：

```
 htdigest /mnt/rpo/conf/scm-user scm *OTHER_USER*

```

可以编辑`scm-user` 文件删除或更改用户名

### 创建数据库

创建 trac 用户和数据库：

```
 /etc/rc.d/postgresql start
 psql -U postgres postgres
 postgres=# CREATE USER trac;
 postgres=# CREATE DATABASE trac OWNER = trac;
 postgres=# \q

```

### 配置Web服务器

编辑`/etc/httpd/conf/httpd.conf`:

```
 LoadModule dav_module              lib/apache/mod_dav.so
 LoadModule dav_svn_module          lib/apache/mod_dav_svn.so
 LoadModule python_module           lib/apache/mod_python.so

 # Inside some virtual host if the server is not dedicated to scm
 DocumentRoot "/var/empty"
 <Location />
   Require valid-user
   AuthType Digest
   AuthName "svnrepos"
   AuthDigestDomain *[http://scm.example.com/](http://scm.example.com/)*
   AuthDigestProvider file
   AuthUserFile */mnt/rpo/conf/scm-user*
 </Location>
 <Location /svn>
   DAV svn
   SVNParentPath */mnt/rpo/svn*
   SVNPathAuthz off
 </Location>
 <Location /trac>
   SetHandler mod_python
   PythonHandler trac.web.modpython_frontend
   PythonOption TracEnvParentDir */mnt/rpo/trac*
   PythonOption TracUriRoot /trac
 </Location>

```

## 创建项目

每个项目都包含一个 svn 源和一个 trac 项目，具有独立的 wiki 和访问控制。

创建 svn 源：

```
 svnadmin create /mnt/rpo/svn/MY_PROJECT

```

初始化项目目录：

```
 trac-admin /mnt/rpo/trac/MY_PROJECT initenv

```

数据库连接字串`postgres://trac:password@localhost/trac?schema=MY_PROJECT` (每个项目必须给出不同的 schema，不需要提前创建 schemas)

为所有登录用户开启管理员权限:

```
 trac-admin /mnt/rpo/trac/MY_PROJECT permission add authenticated TRAC_ADMIN

```

编辑 `/mnt/rpo/trac/MY_PROJECT/conf/trac.ini`：

*   将 `repository_type` 修改为 `svn`
*   将 `repository_path` 修改为 `/mnt/rpo/svn/MY_PROJECT`
*   将 `default_charset` 修改为`utf-8` 或其它编码

允许 web admin ([http://scm.example.com/trac/MY_PROJECT/admin)：](http://scm.example.com/trac/MY_PROJECT/admin)：)

```
echo -e "[components]
webadmin.* = enabled" >> /mnt/rpo/trac/MY_PROJECT/conf/trac.ini

```