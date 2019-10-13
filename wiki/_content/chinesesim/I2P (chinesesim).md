**翻译状态：** 本文是英文页面 [I2P](/index.php/I2P "I2P") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-11-15，点击[这里](https://wiki.archlinux.org/index.php?title=I2P&diff=0&oldid=496194)可以查看翻译后英文页面的改动。

节选自 [I2P](https://geti2p.net/en/) 主页:

	I2P 网络为通过 Internet 进行的通讯提供强有力的隐私保护。很多在公网上可能威胁用户隐私的活动可以在 I2P 中匿名进行。

	许多有I2P接口的应用程序都可用，包括邮件，P2P，IRC聊天等等。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 安装](#安装)
*   [2 使用](#使用)
*   [3 匿名站点](#匿名站点)
*   [4 参见](#参见)

## 安装

I2P可用于提供编译的 [i2p](https://aur.archlinux.org/packages/i2p/)包 源代码和提供预编译二进制文件的 [i2p-bin](https://aur.archlinux.org/packages/i2p-bin/)包; 两者都需要[Java]运行时环境，可以使用OpenJDK，对于ARM平台推荐使用Oracle Java。 I2P主页还提供用于在用户主目录中进行命令行（无头）安装的预编译二进制包。 如果安装类型I2P将通过i2p网络自动更新。

如果这些Java实现是不可取的; [i2pd](https://www.archlinux.org/packages/?name=i2pd)是一个完整的C ++客户端，可以适应资源有限的硬件。

## 使用

First, [start](/index.php/Start "Start") and optionally also enable the `i2prouter.service`.

This will launch the daemon under the system user `i2p`. Next, open your browser of choice and visit the I2P welcome page at

```
127.0.0.1:7657/home

```

From here you can navigate to I2Ps configuration and statistics pages, and links to "Eepsites of Interest" (an [w:eepsite](https://en.wikipedia.org/wiki/eepsite "w:eepsite") being a site available only through the I2P network, similar to how `.onion` sites are only available through the Tor network). Also, be aware that eepsites are unavailable until the daemon has bootstrapped to the network, which can take several minutes.

In order to visit eepsite's configure your browser to use the local http proxy (not socks):

```
HTTP  127.0.0.1 4444
HTTPS 127.0.0.1 4445

```

## 匿名站点

If you make an eepsite, follow the I2P instructions, but keep in mind that the home directory will apply to the i2p user whose home directory is `/opt/i2p` as shown in the AUR [i2p.install](https://aur.archlinux.org/cgit/aur.git/tree/i2p.install?h=i2p) file.

## 参见

*   [I2P Homepage](http://www.i2p2.de)
*   [I2P FAQ](http://www.i2p2.de/faq.html)
*   [Homepage mirror](http://www.i2pproject.net)
*   [I2P Wikipedia entry](https://en.wikipedia.org/wiki/I2p "wikipedia:I2p")