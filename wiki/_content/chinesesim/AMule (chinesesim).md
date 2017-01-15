**翻译状态：** 本文是英文页面 [AMule](/index.php/AMule "AMule") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2013-06-10，点击[这里](https://wiki.archlinux.org/index.php?title=AMule&diff=0&oldid=262103)可以查看翻译后英文页面的改动。

aMule是一个跨平台的eD2k和Kademlia网络客户端，类似于eMule，即电驴客户端。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 服务](#.E6.9C.8D.E5.8A.A1)
*   [3 配置](#.E9.85.8D.E7.BD.AE)
    *   [3.1 amuleweb](#amuleweb)
        *   [3.1.1 创建配置文件](#.E5.88.9B.E5.BB.BA.E9.85.8D.E7.BD.AE.E6.96.87.E4.BB.B6)
*   [4 使用](#.E4.BD.BF.E7.94.A8)
*   [5 参阅](#.E5.8F.82.E9.98.85)

## 安装

[官方源](/index.php/Official_repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official repositories (简体中文)")提供了软件包[amule](https://www.archlinux.org/packages/?name=amule)。另外，[AUR](/index.php/AUR_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "AUR (简体中文)")中的[amule-dlp](https://aur.archlinux.org/packages/amule-dlp/)软件包支持[动态吸血保护](https://code.google.com/p/amule-dlp/)（旧版本）。

**amuled**是aMule的后台守护进程。其前端有GTK的aMuleGUI、网页版的aMuleWeb、命令行的aMuleCmd。

## 服务

软件包提供了两个 *systemd* [服务](/index.php/Daemon "Daemon")： amuled 和 amuleweb：

```
# systemctl start amuled
# systemctl start amuleweb

```

**amulweb**启动后可以通过`[http://127.0.0.1:4711](http://127.0.0.1:4711)`访问，外部地址也可以访问。默认的管理员密码是**amule**.

## 配置

软件安装时会创建用户**amule**，运行 systemd 服务时会使用此用户。

配置文件和临时文件位于 amule 的主目录`/var/lib/amule`：

*   amuled 的配置位于 `/val/lib/amule/.aMule/amule.conf`
*   amuleweb 的配置位于`/val/lib/amule/.aMule/remote.conf`

安装时 pacman 会生成一个带外部访问密码的 amule.conf 文件，amuleweb 配置文件也使用相同的密码。外部配置工具可以使用此密码远程访问。要重新生成密码，可以使用：

```
$ echo -n <your password here> | md5sum | cut -d ' ' -f 1

```

生成密码后，通过 [ExternalConnect] 参数设置。

 `/var/lib/amule/.aMule/amule.conf` 
```
[ExternalConnect]
AcceptExternalConnections=1
ECPassword=<encrypted password>
```

### amuleweb

**注意:** 较之amulegui，amuleweb功能单薄，输出的下载信息也少，而且经常要求输入密码（让浏览器记住密码会好一些）。基于以上原因，建议使用amulegui，并忽略本节。

#### 创建配置文件

还是使用之前配置amuled时的那个新用户，启动amuleweb以初始化配置文件：

```
$ amuleweb --write-config --password=*<这里是密码>* --admin-pass=<这个是网页登录密码>

```

<这里是密码>处填写之前配置amuled使用的密码（未加密的），<这个是网页登录密码>处填写登录网页界面时输入的密码。

**Tip:** 如果 Kad nodes.dat 用的默认 URL 无法连接，可以使用在 [[1]](http://nodes-dat.com)获取 URL.

## 使用

启动amuled、amuleweb（如果需要）：

```
# rc.d start amuled
# rc.d start amuleweb

```

然后，可以访问地址http://127.0.0.1:4711链接amuleweb，或者使用`amulegui`或`amulecmd`控制amule。

**提示：** 如果默认获取KAD节点（nodes.dat）的地址无效，可以从如下地址获取： [http://nodes-dat.com](http://nodes-dat.com) 。

## 参阅

*   [Getting_Started at aMule wiki](http://wiki.amule.org/wiki/Getting_Started)。