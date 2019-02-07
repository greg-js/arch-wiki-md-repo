**翻译状态：** 本文是英文页面 [MongoDB](/index.php/MongoDB "MongoDB") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-12-15，点击[这里](https://wiki.archlinux.org/index.php?title=MongoDB&diff=0&oldid=459380)可以查看翻译后英文页面的改动。

MongoDB (from hu**mongo**us) 是一个开源的，面向文档的数据库系统，由 [MongoDB Inc. (formerly 10gen)](http://www.mongodb.com/)开发并提供支持. 它是NoSQL家族中的一员， 替代用表储存数据的经典的关系型数据库， MongoDB的数据储存结构类似于用动态视图（dynamic schemas）储存类JSON文档（JSON-like documents) （MongoDB称这种格式为[BSON](http://bsonspec.org/)， 将数据尽早尽快地整合成对应的应用类型.

## Contents

*   [1 安装](#安装)
*   [2 使用](#使用)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 无法启动 MongoDB](#无法启动_MongoDB)
    *   [3.2 transparent_hugepage内核设置警告](#transparent_hugepage内核设置警告)

## 安装

由于 MongoDB 修改了软件授权协议，[官方软件仓库](/index.php/Official_repositories "Official repositories")已经删除了此软件包，需要的用户可以选择安装 [mongodb](https://aur.archlinux.org/packages/mongodb/) 或 [mongodb-bin](https://aur.archlinux.org/packages/mongodb-bin/) 软件包。请注意从代码编译 [mongodb](https://aur.archlinux.org/packages/mongodb/) 需要 ~160GB 磁盘空间，需要花费几个小时时间。

可以选择安装 [mongodb-tools](https://www.archlinux.org/packages/?name=mongodb-tools)，这个软件包提供了 `mongoimport`, `mongoexport`, `mongodump`, `mongorestore` 等工具。

[Start/Enable](/index.php/Systemd#Using_units "Systemd") 服务 `mongodb.service`。

第一次启动 mongodb 服务时，会为记录和日志文件预先分配空间，在此期间不能使用数据库 shell。

## 使用

启动 Mongo Shell， 在终端输入:

```
$ mongo

```

## Troubleshooting

### 无法启动 MongoDB

检查 systemctl 的服务是否使用了正确的数据库位置:

```
$ vi /usr/lib/systemd/system/mongodb.service

```

在 "ExecStart" 中加入 "--dbpath /var/lib/mongodb"：

```
ExecStart=/usr/bin/numactl --interleave=all mongod --quiet --config /etc/mongodb.conf --dbpath /var/lib/mongodb

```

检查是否存在3G以上的剩余磁盘空间用于记录文件的储存，否则，MongoDB将启动启动失败

```
$ df -h /var/lib/mongodb/

```

检查是否存在非空 mongod.lock 锁文件

```
# ls  -lisa /var/lib/mongodb

```

锁文件不是空文件， 停止 `mongodb.service`，运行mongo自带的数据库修复程序，指定dbpath (/var/lib/mongodb/ 是Arch Linux 的默认 dbpath)：

```
# mongod --dbpath /var/lib/mongodb/ --repair

```

完成后 dbpath 中应该包含修复的文件和空 mongod.lock 文件.

**警告:** 在特殊情况下，可以删除锁文件，并用损坏的文件重启，数据库也会尝试恢复，但是结果是不可预测的。详情请参考[上游文档](https://docs.mongodb.com/manual/tutorial/recover-data-following-unexpected-shutdown/).

在用root权限运行完修复程序之后，文件的拥有者将变为root用户，然而在Arch Linux里，mongodb可能会被不同用户运行。 需要使用chown命令将文件的拥有者改回正确的用户。点击以下的链接查看更多细节：[Further reference](http://earlz.net/view/2011/03/11/0015/mongodb-and-arch-linux)

```
# chown -R mongodb: /var/{log,lib}/mongodb/

```

最后，从 mongodb [文档](https://docs.mongodb.com/manual/reference/configuration-options/) 复制配置文件，删除下面两行并 [重启](/index.php/Restart "Restart") mongodb.service:

 `/etc/mongodb.conf` 
```
processManagement:
   fork: true

```

### transparent_hugepage内核设置警告

在启动 MongoDB 之后，如果看到关于 transparent_hugepage 的警告，可以通过以下链接提供的方式永久禁用 transparent_hugepage内核设置 (参考 [FreeDesktop tmpfiles.d 手册](https://www.freedesktop.org/software/systemd/man/tmpfiles.d.html)):

 `/etc/tmpfiles.d/local.conf` 
```
w /sys/kernel/mm/transparent_hugepage/enabled - - - - never
w /sys/kernel/mm/transparent_hugepage/defrag - - - - never

```

如果希望只在本次启动时禁用，可以使用SysCtl或者下面的 echo 命令实现：

```
# echo never > /sys/kernel/mm/transparent_hugepage/enabled
# echo never > /sys/kernel/mm/transparent_hugepage/defrag

```