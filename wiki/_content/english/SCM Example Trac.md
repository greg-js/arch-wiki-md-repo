The HOWTO teaches you to setup multi-project Trac/Subversion for a private and trusted environment (ex: a development team).

Updated for Trac 0.11

## Contents

*   [1 Basic Environment](#Basic_Environment)
*   [2 Preparation](#Preparation)
    *   [2.1 Required Packages](#Required_Packages)
    *   [2.2 Post-Install Steps](#Post-Install_Steps)
        *   [2.2.1 Disable connection pooling](#Disable_connection_pooling)
        *   [2.2.2 Install webadmin plugin](#Install_webadmin_plugin)
*   [3 Setup Basic Environment](#Setup_Basic_Environment)
    *   [3.1 Set permissions](#Set_permissions)
    *   [3.2 Create User List](#Create_User_List)
    *   [3.3 Create Database](#Create_Database)
    *   [3.4 Configure Web Server](#Configure_Web_Server)
*   [4 Create Projects](#Create_Projects)
    *   [4.1 Create Subversion Repository](#Create_Subversion_Repository)
    *   [4.2 Create Trac Project](#Create_Trac_Project)
        *   [4.2.1 Modify the _/mnt/rpo/trac/MY_PROJECT/conf/trac.ini_ file](#Modify_the_.2Fmnt.2Frpo.2Ftrac.2FMY_PROJECT.2Fconf.2Ftrac.ini_file)

## Basic Environment

	Network

	URL: [http://scm.example.com](http://scm.example.com)

	Subversion URL: [http://scm.example.com/svn/MY_PROJECT](http://scm.example.com/svn/MY_PROJECT)

	Trac URL: [http://scm.example.com/trac/MY_PROJECT](http://scm.example.com/trac/MY_PROJECT)

	Database

	PostgreSQL, with trust authentication method

	Filesystem

	Configuration files are in `/mnt/rpo/conf`

	Subversion repositories is in `/mnt/rpo/svn`

	Trac project files is in `/mnt/rpo/trac`

## Preparation

### Required Packages

Install the following packages:

*   apache
*   mod_python (AUR package)
*   postgresql
*   pypgsql
*   python2-psycopg2 / python-psycopg2 (depends on python version)
*   setuptools
*   subversion
*   trac

### Post-Install Steps

#### Disable connection pooling

Edit _/usr/lib/python2.5/site-packages/trac/db/postgres_backend.py_:

```
 class PostgreSQLConnection
   ......
   poolable = False   # Change this line

```

#### Install webadmin plugin

**This is no longer needed, starting with version 0.11 it has been** incorporated into the core system

```
 svn co [http://svn.edgewall.com/repos/trac/sandbox/webadmin](http://svn.edgewall.com/repos/trac/sandbox/webadmin)
 cd webadmin
 python setup.py bdist_egg
 easy_install -Z dist/*.egg

```

## Setup Basic Environment

Create the directories:

```
 mkdir -p /mnt/rpo/conf
 mkdir -p /mnt/rpo/svn
 mkdir -p /mnt/rpo/trac

```

### Set permissions

The user account under which the web server runs will require write permissions to the environment directory and all the files inside. With the web server running as user http and group http, enter:

```
 chown -R http.http /mnt/rpo

```

### Create User List

Create a new list and add initial user:

```
 htdigest -c /mnt/rpo/conf/svn-user svnrepos _FIRST_USER_

```

To add other users:

```
 htdigest /mnt/rpo/conf/svn-user svnrepos _OTHER_USER_

```

You can edit the _svn-user_ file to remove or rename users

### Create Database

Create the trac user and the database:

```
 /etc/rc.d/postgresql start
 psql -U postgres postgres
 postgres=# CREATE USER trac;
 postgres=# CREATE DATABASE trac OWNER = trac;
 postgres=# \q

```

### Configure Web Server

Edit _/etc/httpd/conf/httpd.conf_:

```
 LoadModule dav_module              modules/mod_dav.so
 LoadModule dav_svn_module          modules/mod_dav_svn.so
 LoadModule python_module           modules/mod_python.so

 # Inside some virtual host if the server is not dedicated to scm
 DocumentRoot "/var/empty"
 <Location />
   Require valid-user
   AuthType Digest
   AuthName "svnrepos"
   AuthDigestDomain _[http://scm.example.com/](http://scm.example.com/)_
   AuthDigestProvider file
   AuthUserFile _/mnt/rpo/conf/svn-user_
 </Location>
 <Location /svn>
   DAV svn
   SVNParentPath _/mnt/rpo/svn_
   SVNPathAuthz off
 </Location>
 <Location /trac>
   SetHandler mod_python
   PythonHandler trac.web.modpython_frontend
   PythonOption TracEnvParentDir _/mnt/rpo/trac_
   PythonOption TracUriRoot /trac
 </Location>

```

## Create Projects

Each project is consisted of one subversion repository and one trac project, with independent wiki and access control.

### Create Subversion Repository

Just execute one line:

```
 svnadmin create /mnt/rpo/svn/MY_PROJECT

```

### Create Trac Project

*   Initialize project dir:

```
 trac-admin /mnt/rpo/trac/MY_PROJECT initenv

```

	Database connection string: `postgres://trac:password@localhost/trac?schema=MY_PROJECT`

	(each project must be given an unique schema; no need to create the schemas first)

*   Grant admin permission to all logon users:

```
 trac-admin /mnt/rpo/trac/MY_PROJECT permission add authenticated TRAC_ADMIN

```

#### Modify the _/mnt/rpo/trac/MY_PROJECT/conf/trac.ini_ file

*   Change **repository_type** to **svn**
*   Change **repository_path** to **/mnt/rpo/svn/MY_PROJECT**
*   Change **default_charset** to **utf-8** or other encodings.

*   Allow web admin ([http://scm.example.com/trac/MY_PROJECT/admin](http://scm.example.com/trac/MY_PROJECT/admin)):

```
echo -e "[components]\nwebadmin.* = enabled" >> /mnt/rpo/trac/MY_PROJECT/conf/trac.ini

```