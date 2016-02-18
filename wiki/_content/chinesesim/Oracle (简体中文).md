## Contents

*   [1 介绍](#.E4.BB.8B.E7.BB.8D)
*   [2 安装方法1 - 手动](#.E5.AE.89.E8.A3.85.E6.96.B9.E6.B3.951_-_.E6.89.8B.E5.8A.A8)
    *   [2.1 准备安装](#.E5.87.86.E5.A4.87.E5.AE.89.E8.A3.85)
    *   [2.2 安装桌面环境](#.E5.AE.89.E8.A3.85.E6.A1.8C.E9.9D.A2.E7.8E.AF.E5.A2.83)
        *   [2.2.1 安装Oracle数据库必需的软件包](#.E5.AE.89.E8.A3.85Oracle.E6.95.B0.E6.8D.AE.E5.BA.93.E5.BF.85.E9.9C.80.E7.9A.84.E8.BD.AF.E4.BB.B6.E5.8C.85)
        *   [2.2.2 配置](#.E9.85.8D.E7.BD.AE)
    *   [2.3 图形安装](#.E5.9B.BE.E5.BD.A2.E5.AE.89.E8.A3.85)
        *   [2.3.1 安装Oracle数据库软件](#.E5.AE.89.E8.A3.85Oracle.E6.95.B0.E6.8D.AE.E5.BA.93.E8.BD.AF.E4.BB.B6)
    *   [2.4 Oracle企业管理安装(可选)](#Oracle.E4.BC.81.E4.B8.9A.E7.AE.A1.E7.90.86.E5.AE.89.E8.A3.85.28.E5.8F.AF.E9.80.89.29)
*   [3 安装方法2 - AUR](#.E5.AE.89.E8.A3.85.E6.96.B9.E6.B3.952_-_AUR)
    *   [3.1 安装](#.E5.AE.89.E8.A3.85)
*   [4 Post 安装=](#Post_.E5.AE.89.E8.A3.85.3D)
    *   [4.1 创建初始化数据库](#.E5.88.9B.E5.BB.BA.E5.88.9D.E5.A7.8B.E5.8C.96.E6.95.B0.E6.8D.AE.E5.BA.93)
        *   [4.1.1 图形](#.E5.9B.BE.E5.BD.A2)
        *   [4.1.2 Scripted](#Scripted)
        *   [4.1.3 测试数据库](#.E6.B5.8B.E8.AF.95.E6.95.B0.E6.8D.AE.E5.BA.93)
    *   [4.2 在启动时启动oracle](#.E5.9C.A8.E5.90.AF.E5.8A.A8.E6.97.B6.E5.90.AF.E5.8A.A8oracle)
    *   [4.3 为普通用户设定权限](#.E4.B8.BA.E6.99.AE.E9.80.9A.E7.94.A8.E6.88.B7.E8.AE.BE.E5.AE.9A.E6.9D.83.E9.99.90)
*   [5 Transfer existing Oracle installation](#Transfer_existing_Oracle_installation)
    *   [5.1 更多资源](#.E6.9B.B4.E5.A4.9A.E8.B5.84.E6.BA.90)

### 介绍

这份文档将会帮助您把Oracle数据库11gR1安装到Arch Linux。使用安装方法2，您可以仅仅通过几个步骤完成长时间的安装过程。

## 安装方法1 - 手动

这节将会引导您在全新的archlinux上安装Oracle。这是一个通用的方法，在内核2.6.28.ARCH 64位机器上安装Oracle 11g R1 64 位测试通过。***这在其他版本的Orale上也应该可以工作***。

### 准备安装

### 安装桌面环境

```
# pacman -Syu
# pacman -S python
# pacman -U [ftp://ftp.berlios.de/pub/aurbuild/aurbuild-1.8.4-1-any.pkg.tar.gz](ftp://ftp.berlios.de/pub/aurbuild/aurbuild-1.8.4-1-any.pkg.tar.gz)

```

安装并测试Xorg。

```
# pacman -S xorg
# pacman -S hwd

```

尽管从Xorg 7.4后，xorg.conf 不再需要。这命令是可选的。

```
# hwd -x
# cp /etc/X11/xorg.conf.vesa /etc/X11/xorg.conf

```

使用<tt>startx</tt>检查(Should get mouse movement with X cursor - Ctrl-Alt-Backspace to exit.)

```
$ startx

```

安装桌面环境，Gnome,KDE 或 Xfce。这个例子假设Xfce4将被安装：

```
# pacman -S xfce4
# pacman -S pcmanfm

```

运行 xfce:

```
$ startxfce4 

```

#### 安装Oracle数据库必需的软件包

[安装](/index.php/Pacman "Pacman") 软件包 [unzip](https://www.archlinux.org/packages/?name=unzip) [sudo](https://www.archlinux.org/packages/?name=sudo) [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) [icu](https://www.archlinux.org/packages/?name=icu) [gawk](https://www.archlinux.org/packages/?name=gawk) [gdb](https://www.archlinux.org/packages/?name=gdb) [elfutils](https://www.archlinux.org/packages/?name=elfutils) [sysstat](https://www.archlinux.org/packages/?name=sysstat) [libstdc++5](https://www.archlinux.org/packages/?name=libstdc%2B%2B5).

安装 [Java](/index.php/Java "Java") 运行时环境，例如 [jre7-openjdk](https://www.archlinux.org/packages/?name=jre7-openjdk) 或 [jdk7-openjdk](https://www.archlinux.org/packages/?name=jdk7-openjdk).

安装ksh (problem with aurbuild -s ksh).

```
mkdir -p ABS/ksh
cd ABS/ksh
chmod 777 -R /software
wget --http-user "I accept www.opensource.org/licenses/cpl" --http-password "." [http://www.research.att.com/~gsf/download/tgz/INIT.2009-05-05.tgz](http://www.research.att.com/~gsf/download/tgz/INIT.2009-05-05.tgz)
wget --http-user "I accept www.opensource.org/licenses/cpl" --http-password "." [http://www.research.att.com/~gsf/download/tgz/ast-ksh.2009-05-05.tgz](http://www.research.att.com/~gsf/download/tgz/ast-ksh.2009-05-05.tgz)
wget [https://aur.archlinux.org/packages/ksh/ksh/PKGBUILD](https://aur.archlinux.org/packages/ksh/ksh/PKGBUILD)
wget [https://aur.archlinux.org/packages/ksh/ksh/ksh.install](https://aur.archlinux.org/packages/ksh/ksh/ksh.install)
makepkg -c --asroot
makepkg -i --asroot

```

```
pacman -S icu
aurbuild -s beecrypt
aurbuild -s rpm
pacman -S gawk
pacman -S gdb
aurbuild -s libaio
pacman -S libelf
pacman -S sysstat
pacman -S libstdc++5

```

Oracle32位数据库需要unixodbc。

```
# pacman -S unixodbc

```

可选的lib32 软件包 x86_64:

```
# pacman -S lib32-libstdc++5 
# pacman -S lib32-glibc 
# pacman -S lib32-gcc-libs

```

Oracle数据库需要32位的libaio和unixodbc在x86_64上，但在32位上是不必要的。

Oracle Universal Installer需要的一些软链接。

```
# ln -s /usr/bin/rpm /bin/rpm
# ln -s /usr/bin/ksh /bin/ksh
# ln -s /bin/awk /usr/bin/awk
# ln -s /bin/tr /usr/bin/tr
# ln -s /usr/bin/basename /bin/basename

```

Arch x86_64:

```
# ln -s /usr/lib /usr/lib64

```

#### 配置

为Orcale数据库创建用户和组：

```
# groupadd oinstall
# groupadd dba
# useradd -m -g oinstall -G dba oracle

```

为用户oracle设置密码：

```
# passwd oracle

```

可选: Add oracle to the `sshd_config` file.

```
# pacman -S openssh

```

Add this line to `/etc/ssh/sshd_config`:

```
AllowUsers oracle

```

Add oracle to `/etc/sudoers`. This will give oracle super user privilege.

```
oracle    ALL=(ALL) ALL

```

Add these lines to `/etc/sysctl.d/99-sysctl.conf` (***Review Oracle documentation to adjust these settings***).

```
# oracle kernel settings
fs.file-max = 6553600
kernel.shmall = 2097152
kernel.shmmax = 2147483648
kernel.shmmni = 4096
kernel.sem = 250 32000 100 128
net.ipv4.ip_local_port_range = 1024 65535
net.core.rmem_default = 4194304
net.core.rmem_max = 4194304
net.core.wmem_default = 262144
net.core.wmem_max = 262144

```

Add these lines to `/etc/security/limits.conf` (***Review Oracle documentation to adjust these settings***)

```
# oracle settings
oracle           soft    nproc   2047
oracle           hard    nproc   16384
oracle           soft    nofile  1024
oracle           hard    nofile  65536

```

可选: 想使变化生效您可以重启电脑。

为Ocale数据库创建一些目录。您可以选择目录路径。下面是参考例子。

```
mkdir -p /oracle
mkdir -p /oracle/inventory
mkdir -p /oracle/recovery
mkdir -p /oracle/product/db

```

为目录设定权限。

```
chown -R oracle:dba /oracle
chmod 777 /tmp

```

Create or update oracle bashrc `/home/oracle/.bashrc`. Here is an example of the oracle user settings.

```
export ORACLE_BASE=/oracle
export ORACLE_HOME=/oracle/product/db
export ORACLE_SID=xdb
export ORACLE_INVENTORY=/oracle/inventory
export ORACLE_BASE ORACLE_SID ORACLE_HOME
export PATH=$ORACLE_HOME/bin:$PATH
export LD_LIBRARY_PATH=$ORACLE_HOME/lib:$LD_LIBRARY_PATH
export EDITOR=nano
export VISUAL=nano

```

### 图形安装

#### 安装Oracle数据库软件

从下面下载Orcale数据库： [http://www.oracle.com/technology/software/products/database/index.html](http://www.oracle.com/technology/software/products/database/index.html)

解压Oracle数据库。

Arch i686:

```
unzip linux_11gR1_database_1013.zip -d /media

```

Arch x86_64:

```
unzip linux.x64_11gR1_database_1013.zip -d /media

```

可选: Arch x86_64 (only required if the installer will not launch automatically ... at the time of this writing there was an issue with the packaged unzip in the 64-bit Oracle installer):

```
cd /media/database/install
mv unzip unzipx
ln -s /usr/bin/unzip 

```

Change the permissions for the extracted Oracle database.

```
chmod -R 777 /media/database
chown -R oracle:oinstall /media/database

```

Enter the directory where you extracted the Oracle database.

In oder to run oracle installation script you need to export the X display as a normal user:

```
DISPLAY=:0.0; export DISPLAY; xhost +

```

Login as the user oracle and export the X display:

```
su oracle
DISPLAY=:0.0; export DISPLAY

```

Enter the database directory and run the Oracle Universal Installer as the user oracle.

```
cd /media/database
./runInstaller -ignoreSysPrereqs

```

在图形安装过程中：

1.  Click on "Next".
2.  Choose "Enterprise Edition" Installation Type and click on "Next"
3.  Oracle Base should be: /oracle. Don't change it, unless you know what you're doing.
    1.  Change the default "Name" to orarch or something else.
    2.  The predefined path in `/etc/rc.d/oracledb` is "db", ie: /oracle/product/db. If you want to use a different path you'll have to change `/etc/rc.d/oracledb`, so that the startup script can locate ORACLE_HOME directory.
    3.  After changing the defaults, click on "Next".
4.  Since Oracle database requires certain distro requirement, you'll have to manually check them and then click on "Next".
5.  Chose "Software Install Only" and click on "Next".
6.  There is only one DBA group for oracle database. Click on "Next".
7.  Install "Summary" shows what's going to be installed. Click on "Install".
8.  The installation will take some time, especially the "Linking" part. Be patient! If you get an error message ignore it by clicking on "Continue".
    1.  At the end of the installation you'll have to open another terminal, and execute `/oracle/product/db/root.sh` as root. **Don't click on "OK" yet**.
    2.  When running root.sh, you'll be offered to use /usr/local/bin as the full pathname. Press the "Enter" key here.
    3.  Now you can click on "OK"
9.  Installation is finished, click on "Exit" and "Yes", you really want to exit.

### Oracle企业管理安装(可选)

This section describes how to install the web based OEM available in 10g+.

*Depending on your settings the OUI may have already installed this*.

Login or su to oracle, then run the following commands (answering the prompts approriately). ***This may take a while***.

```
cd ${ORACLE_HOME}/bin
./emca -repos create
./emca -config dbcontrol db

```

Test this out by navigating to the enterprise manager (adjust the servername (localhost) apporpriately).

```
[https://localhost:1158/em/console](https://localhost:1158/em/console)

```

You can control OEM with the following commands.

```
emctl status dbconsole
emctl stop dbconsole
emctl start dbconsole

```

## 安装方法2 - AUR

### 安装

**Note:** 这种安装方法会自动创建数据库，因此，在安装完后，Orcale数据库就可以使用了。

**第一步** 从AUR里面下载Arch Linux 软件包：[https://aur.archlinux.org/packages.php?ID=23730](https://aur.archlinux.org/packages.php?ID=23730) 下载Oracle数据库11gR1：[http://www.oracle.com/technology/software/products/database/index.html](http://www.oracle.com/technology/software/products/database/index.html)

**第二步** 解压Arch Linux 软件包到一个目录。同时把Oracle数据库11gR1复制到同一目录下。

信息:默认的安装配置 `ee.rsp.patch`是:

```
ORACLE_BASE="/home/oracle/app/oracle"
ORACLE_HOME="/home/oracle/app/oracle/product/11.1.0/orarch"
ORACLE_HOME_NAME="orarch"
s_globalDBName="archlinux"
s_dbSid="archlinux"
s_superAdminSamePasswd="orarchdbadmin"
s_superAdminSamePasswdAgain="orarchdbadmin"

```

可选: You can either change the default password now or later after the installation. If you change the ee.rsp.patch file, you need to update the md5sums in the PKGBUILD file. To obtain the md5sum, run (makepkg -g) or:

```
md5sum ee.rsp.patch 

```

创建Orcale数据库软件包通过使用makepkg：

```
makepkg -s

```

**Step 3.** 安装已经创建好的软件包。

Arch i686:

```
pacman -U oracle-11gR1-1-i686.pkg.tar.gz 

```

Arch x86_64:

```
pacman -U oracle-11gR1-1-x86_64.pkg.tar.gz 

```

Pacman现在将安装Oracle数据库通过执行Oracle自己的安装脚本(./runInstaller -silent -ignoreSysPrereqs)。

安装将花费一些时间。请耐心一点。在安装过程中不要退出终端，特别是安装脚本在执行配置助手时：

```
.... 
Starting to execute configuration assistants
Configuration assistant "Oracle Net Configuration Assistant" succeeded 
...

```

安装脚本会结束像下面所举的:

```
The following configuration scripts need to be executed as the "root" user.
#!/bin/sh
#Root script to run
/home/oracle/oraInventory/orainstRoot.sh
/home/oracle/app/oracle/product/11.1.0/orarch/root.sh
To execute the configuration scripts:
   1\. Open a terminal window
   2\. Log in as "root"
   3\. Run the scripts

The installation of Oracle Database 11g was successful.
Please check '/home/oracle/oraInventory/logs/silentInstall2009-03-03_07-24-10PM.log'
for more details.

```

**第四步** 以root身份运行这些脚本：

```
[ahc@archlinux ~]$ su
Password: 

```

```
cd /home/oracle/oraInventory
./orainstRoot.sh

```

```
cd /home/oracle/app/oracle/product/11.1.0/orarch
./root.sh

```

**第五步** 默认的Oracle用户是“oracle”。由于没有为用户oracle设置密码，您需要以root身份运行passwd：

```
passwd oracle

```

**第六步** 以用户oracle身份登录。

```
su oracle

```

创建文件/home/oracle/.bashrc，然后添加这些行到.bashrc文件：

```
export ORACLE_SID=archlinux
export ORACLE_HOME=/home/oracle/app/oracle/product/11.1.0/orarch
export PATH=$PATH:$ORACLE_HOME/bin

```

**第七步** 如果您没有改变 `ee.rsp.patch`文件,您需要**为SYS和SYSTEM改变管理密码**。

**Note:** 如果数据库没有被挂载或者打开，以用户oracle身份登录然后首先尝试：

```
su oracle

```

```
sqlplus '/as sysdba'

```

```
SQL> startup mount;
SQL> alter database open; 

```

为 **SYSTEM**用户更改密码:

```
sqlplus '/as sysdba'

```

```
SQL> show user
USER is "SYS"

```

```
SQL> passw system
Changing password for system
New password:
Retype new password:
Password changed

```

```
SQL> quit

```

为**SYS** 用户更改密码:

```
sqlplus system/secretpassword

```

```
SQL> show user;
USER is "SYSTEM"

```

```
SQL> passw sys
Changing password for sys
New password: 
Retype new password: 
Password changed

```

```
SQL> quit

```

## Post 安装=

### 创建初始化数据库

#### 图形

You have only installed the Oracle database software. Now you need to create a database. Login as the user oracle:

```
su oracle

```

Export the ORACLE_HOME binary directory:

```
export ORACLE_HOME=/oracle/product/db
export PATH=$PATH:$ORACLE_HOME/bin

```

Run database installation script:

```
dbca

```

During the graphical installation:

1.  Click on "Next".
2.  Check "Create a Database" and click on "Next".
3.  Check "General Purpose or Transaction Processing" and click on "Next".
4.  Chose a database name and SID. Example: Global Database Name: <tt>archlinux</tt>, SID: <tt>archlinux</tt>. And then click on "Next".
5.  Uncheck "Configure Enterprise Manager", leave it empty and click on "Next".
6.  Check "Use the Same Administrative Password for All Accounts", set password and click on "Next".
7.  Check "File System" and click on "Next".
8.  Check "Use Database File Locations from Template" and click on "Next".
9.  Uncheck "Specify Flash Recovery Area" and click on "Next".
10.  No need for "Sample Schemas", click on "Next".
11.  If you don't know what you're doing, check "Typical" and click on "Next"
12.  Check "Keep the enhanced 11g default security settings" and click on "Next".
13.  Uncheck "Enable automatic maintenance tasks" if you wish to do it by yourself and click on "Next".
14.  View your filesystem layout and click on "Next".
15.  "Create Database" is checked by default. Click on "Finish" to create database.
16.  Summary of following operations to be performed, click on "OK".
17.  When database creation is complete, click on "Exit".

#### Scripted

This section walks you through doing a scripted initial database creation.

**Note:** The scripts assume they are the first database to be installed on this system. If this is not the case review the xdb-create.sh script and comment out the portions which deal with the *.ora files.

Download the following tar file with a set of scripted database installation scripts.

```
wget [http://sites.google.com/site/mbasil77/Home/instanceCreateXdb.tgz](http://sites.google.com/site/mbasil77/Home/instanceCreateXdb.tgz)

```

Extract the directory

```
tar xzf instanceCreateXdb.tgz

```

Move into instanceCreateXdb directory

```
cd instanceCreateXdb

```

File list

*   CreateDB.sql
*   CreateDBCatalog.sql
*   initxdb.dbs.ora
*   initxdb.ora
*   listener.ora
*   postDBCreation.sql
*   sqlnet.ora
*   sysObjects.sql
*   tnsnames.ora
*   xdb-create.sh
*   xdb-create.sql
*   xdb-secfix.sh

Script notes

*   the files assume a database sid of **xdb**
*   the files assume an oracle base of **/oracle/product/db**
*   ***review all memory and storage parameters against Oracle documentation***

Setup filesystem (as root)

```
./xdb-create.sh

```

Install database from script (***this will take a long time***)

```
su oracle
sqlplus / as sysdba @/oracle/admin/xdb/scripts/xdb-create.sql

```

#### 测试数据库

以用户oracle身份登录，然后运行 export ORACLE_SID="yourSID"等,:

```
export ORACLE_SID=xdb
export ORACLE_HOME=/oracle/product/db
export PATH=$PATH:$ORACLE_HOME/bin

```

运行oraenv来确认已经export的配置:

```
oraenv

```

```
ORACLE_SID = [xdb] ? 
The Oracle base for ORACLE_HOME=/oracle/product/db 
is /oracle

```

检查数据库是否关闭或开启：

```
sqlplus '/as sysdba'

```

```
SQL> shutdown immediate;
Database closed.
Database dismounted.
ORACLE instance shut down.

```

```
SQL> startup mount;

ORACLE instance started.

Total System Global Area  385003520 bytes
Fixed Size		    1300100 bytes
Variable Size		  234883452 bytes
Database Buffers	  142606336 bytes
Redo Buffers		    6213632 bytes
Database mounted.
Database opened.

```

Type "quit" when you want to leave SQL prompt:

```
SQL> quit

```

### 在启动时启动oracle

If you want to start with your oracle SID, replace ":N" with ":Y" in /etc/oratab:

```
<your sid>:<oracle home>:N
<your sid>:<oracle home>:Y

```

Example from Scripted database creation (/etc/oratab):

```
xdb:/oracle/product/db:Y

```

To start the oracle database daemon during boot, add "oracledb" in your /etc/rc.conf:

```
DAEMONS=(oracledb syslog-ng dbus !network netfs crond ntpd alsa hal wicd fam)

```

Note: If the daemon doesn't start, please check that the ORACLE_HOME path matches your current oracle directory in /etc/rc.d/oracledb:

```
export ORACLE_HOME=/oracle/product/db

```

```
[oracle@archlinux orarch]$ pwd
/oracle/product/db

```

Test starting the daemon as root:

```
/etc/rc.d/oracledb start

```

```
Starting Oracle: 
LSNRCTL for Linux: Version 11.1.0.6.0 - Production on 27-FEB-2009 23:14:45
...
The command completed successfully
Processing Database instance "archlinux": log file 
/oracle/product/db/startup.log
OK

```

Now you'll login to your oracle database each time you reboot:

```
su oracle
export ORACLE_SID=xdb
oraenv
sqlplus '/as sysdba'

```

Install Method 2:

```
su oracle
export ORACLE_SID=archlinux
oraenv
sqlplus '/as sysdba'

```

### 为普通用户设定权限

此时仅仅一个用户（oracle）能够使用oracle数据库。您需要添加您其他的用户到组“dba”。假设“joe”是一个普通用户：

```
gpasswd -a joe dba

```

dba组在您登出时然后登录进来才生效。用户oracle拥有oracle家目录的权限，如 /home/oracle：

```
drwx------ 6 oracle dba 4096 2009-02-27 23:27 oracle

```

您需要使组“dba”拥有权限来执行oracle目录下到二进制文件：

```
chmod -R g+x /home/oracle

```

此时您的普通用户就可以使用oracle数据库了。

## Transfer existing Oracle installation

Moving or transferring Oracle can be quite useful in the following conditions:

*   replacing hardware
*   setting up several dev machines
*   running lean system (no desktop manager, java, etc)

The installation of Oracle requires several packages. However, just running an Oracle database is much simpler and has far fewer requirements, as shown below.

*In principle transferring Oracle should work across distros. Transferring from RHEL/Centos 5.2 to ARCH 2009.02 has been tested successfully.*

To prep Oracle for a move shutdown database services

```
dbstop ${ORACLE_HOME}
lsnrctl stop

```

Optional: stop OEM if it is running

```
emctl stop dbconsole

```

***If you are running other Oracle daemons stop them as well***

This section assumes the following conditions about the existing Oracle installation:

*   oracle root is /oracle
*   oracle data is at /oracle/oradata/<sid>

Tar up entire Oracle installation and data.

```
cd /
tar czf oracle.tgz /oracle

```

Using ssh and sftp or your method of choice transfer oracle.tgz to the root (/) of the target system.

Login to target system as root and unpack the tar

```
cd /
tar xzf oracle.tgz
chmod 755 -R /oracle
chown -R oracle:dba /oracle

```

Update system

```
pacman -S pacman
pacman -Syu
pacman -S python
pacman -U [ftp://ftp.berlios.de/pub/aurbuild/aurbuild-1.8.4-1-any.pkg.tar.gz](ftp://ftp.berlios.de/pub/aurbuild/aurbuild-1.8.4-1-any.pkg.tar.gz)
pacman -S unzip
pacman -S sudo

```

Install required package run Oracle database and *required* daemons.

```
aurbuild -s libaio
pacman -S sysstat

```

Configure server for oracle

```
[Oracle#Configuration](/index.php/Oracle#Configuration "Oracle")

```

Setup OEM (optional)

```
[Oracle#Oracle_Enterprise_Manager_installation_.28optional.29](/index.php/Oracle#Oracle_Enterprise_Manager_installation_.28optional.29 "Oracle")

```

Execute appropriate/desired post installation steps

```
[Oracle#Post_Installation](/index.php/Oracle#Post_Installation "Oracle")

```

```
===疑难解答===

```

已知问题: The Oracle Universal Installer(ie, in silent mode) seems create errors when installing on other paths than "../app/oracle/..".

### 更多资源

* * *

大部分的步骤是基于ubuntu用户的oracle安装向导，这篇文档包括一步一步的图形例子： [http://www.pythian.com/blogs/1355/installing-oracle-11gr1-on-ubuntu-810-intrepid-ibex](http://www.pythian.com/blogs/1355/installing-oracle-11gr1-on-ubuntu-810-intrepid-ibex)