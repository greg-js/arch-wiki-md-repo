MongoDB (from hu**mongo**us) 是一个开源的，面向文档的数据库系统，由 [MongoDB Inc. (formerly 10gen)](http://www.mongodb.com/)开发并提供支持. 它是NoSQL家族中的一员， 替代用表储存数据的经典的关系型数据库， MongoDB的数据储存结构类似于用动态视图（dynamic schemas）储存类JSON文档（JSON-like documents) （MongoDB称这种格式为[BSON](http://bsonspec.org/)， 将数据尽早尽快地整合成对应的应用类型.

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 使用](#.E4.BD.BF.E7.94.A8)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 MongoDB 不能启动](#MongoDB_.E4.B8.8D.E8.83.BD.E5.90.AF.E5.8A.A8)
    *   [3.2 MongoDB警告transparent_hugepage内核设置](#MongoDB.E8.AD.A6.E5.91.8Atransparent_hugepage.E5.86.85.E6.A0.B8.E8.AE.BE.E7.BD.AE)

## 安装

安装 [mongodb](https://www.archlinux.org/packages/?name=mongodb) 从 [official repositories](/index.php/Official_repositories "Official repositories").

[Start/Enable](/index.php/Systemd#Using_units "Systemd") the `mongodb.service` daemon.

在第一次启动mongodb service的时候，它将通过为他的记录和其他数据创建一个较大的文件来为它与分配空间。这些文件可能会占用3G的空间

请注意这一步可能会花费一些时间，database shell可能在此期间不能使用

## 使用

启动Mongo Shell， 在终端输入:

```
$ mongo

```

## Troubleshooting

### MongoDB 不能启动

检查是否存在3G以上的剩余磁盘空间用于记录文件的储存，否则，MongoDB将启动启动失败

```
$ df -h /var/lib/mongodb/

```

检查是否存在锁文件（lock files）

```
# ls  -lisa /var/lib/mongodb

```

如果存在锁文件， 停止 `mongodb.service`，删除以下文件，再次启动 `mongodb.service`

```
# rm /var/lib/mongodb/mongod.lock

```

如果它依然不能启动， 运行mongo自带的数据库修复程序，指定dbpath (/var/lib/mongodb/ 是Arch Linux的默认dbpath)：

```
# mongod --dbpath /var/lib/mongodb/ --repair

```

在用root权限运行完修复程序之后，文件的拥有者将变为root用户，然而在Arch Linux里，mongodb可能会被不同用户运行。 你需要使用chown命令将文件的拥有者改回正确的用户。点击以下的链接查看更多细节：[Further reference](http://earlz.net/view/2011/03/11/0015/mongodb-and-arch-linux)

```
# chown -R mongodb: /var/{log,lib}/mongodb/

```

检查[boost-libs](https://www.archlinux.org/packages/?name=boost-libs) 包是否为最新版本。MongoDB需要特定版本的[boost-libs](https://www.archlinux.org/packages/?name=boost-libs)。但是，mongoDB的依赖没有限定[boost-libs](https://www.archlinux.org/packages/?name=boost-libs)具体版本

### MongoDB警告transparent_hugepage内核设置

在启动MongoDB之后，如果你看到关于transparent_hugepage的警告，你可以通过以下链接提供的方式永久禁用（disable）transparent_hugepage内核设置 (see [FreeDesktop tmpfiles.d Manual](https://www.freedesktop.org/software/systemd/man/tmpfiles.d.html)):

 `/etc/tmpfiles.d/local.conf` 
```
w /sys/kernel/mm/transparent_hugepage/enabled - - - - never
w /sys/kernel/mm/transparent_hugepage/defrag - - - - never

```

如果你希望只是在本次启动是禁用，你可以使用SysCtl或者一下简单的echo命令实现：

```
# echo never > /sys/kernel/mm/transparent_hugepage/enabled
# echo never > /sys/kernel/mm/transparent_hugepage/defrag

```