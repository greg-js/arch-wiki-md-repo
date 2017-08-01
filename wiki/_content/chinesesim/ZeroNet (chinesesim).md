**翻译状态：** 本文是英文页面 [ZeroNet](/index.php/ZeroNet "ZeroNet") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-08-01，点击[这里](https://wiki.archlinux.org/index.php?title=ZeroNet&diff=0&oldid=483448)可以查看翻译后英文页面的改动。

[ZeroNet](https://zeronet.io/) 可以“利用比特币加密和 BitTorrent 网络创建公开、自由和不受审查的网站”。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
    *   [2.1 启动](#.E5.90.AF.E5.8A.A8)
    *   [2.2 Tor](#Tor)
*   [3 创建 ZeroNet 站点](#.E5.88.9B.E5.BB.BA_ZeroNet_.E7.AB.99.E7.82.B9)
*   [4 参阅](#.E5.8F.82.E9.98.85)

## 安装

[安装](/index.php/Install "Install") [zeronet](https://aur.archlinux.org/packages/zeronet/) 软件包。

最新的开发版是 [zeronet-git](https://aur.archlinux.org/packages/zeronet-git/) 包。

## 配置

### 启动

启动 ZeroNet ：[启动/启用](/index.php/Start/enable "Start/enable") `zeronet.service`。

### Tor

默认情况下，ZeroNet 使用 clearnet 和 Tor（如果可用）。要启用对 Tor 的支持需要安装 [Tor](/index.php/Tor "Tor")（[tor](https://www.archlinux.org/packages/?name=tor)）。然后执行下列命令让 ZeroNet 使用 Tor ：

```
# usermod -a -G tor zeronet
# mkdir -m 750 /var/lib/tor-auth
# chown tor:tor /var/lib/tor-auth

```

在 `/etc/tor/torrc` 中[添加](/index.php/Append "Append")下列行：

```
ControlPort 9051
CookieAuthentication 1
CookieAuthFileGroupReadable 1
CookieAuthFile /var/lib/tor-auth/control_auth_cookie

```

## 创建 ZeroNet 站点

所有操作，包括 ZeroNet 站点文件的编辑，都应该以 `zeronet` 用户执行。使用 `--config_file` 选项可以指定要使用的配置文件。`/var/lib/zeronet` 中默认的数据文件目录是`/var/lib/zeronet`。示例:

```
$ sudo -u zeronet python2 zeronet.py --config_file /etc/zeronet.conf

```

或

```
$ sudo su - zeronet
$ cd /opt/zeronet
$ python2 zeronet.py --config_file /etc/zeronet.conf

```

创建的站点的初始数据位于 `/var/lib/zeronet/[address]` 中，关于创建 Zeronet 站点的更多信息，请阅读 [Zeronet FAQ](http://zeronet.readthedocs.io/en/latest/using_zeronet/create_new_site/).

## 参阅

*   [ZeroNet 文档](https://zeronet.readthedocs.io/en/latest/)