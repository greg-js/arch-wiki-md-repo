**翻译状态：** 本文是英文页面 [ZeroNet](/index.php/ZeroNet "ZeroNet") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-07-20，点击[这里](https://wiki.archlinux.org/index.php?title=ZeroNet&diff=0&oldid=482432)可以查看翻译后英文页面的改动。

From [ZeroNet](https://zeronet.io/) gives access to "open, free and uncensorable websites, using Bitcoin cryptography and BitTorrent network".

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

All operations, including editing ZeroNet site files, should be done as user `zeronet` and configuration must be passed for data directory to be selected to `/var/lib/zeronet`. For example:

```
$ sudo -u zeronet python2 zeronet.py --config_file /etc/zeronet.conf

```

Or

```
$ sudo su - zeronet
$ cd /opt/zeronet
$ python2 zeronet.py --config_file /etc/zeronet.conf

```

All zites you create will have their initial data folder setup in /var/lib/zeronet/[address]. For more information on how to create a Zite, please follow the guidelines on the [Zeronet FAQ](http://zeronet.readthedocs.io/en/latest/using_zeronet/create_new_site/).

## 参阅

*   [Official ZeroNet website](https://zeronet.io/)
*   [ZeroNet - Read the Docs](https://zeronet.readthedocs.io/en/latest/)