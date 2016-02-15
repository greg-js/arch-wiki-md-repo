**翻译状态：** 本文是英文页面 [pacman-key](/index.php/Pacman-key "Pacman-key") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-05-21，点击[这里](https://wiki.archlinux.org/index.php?title=pacman-key&diff=0&oldid=373932)可以查看翻译后英文页面的改动。

pacman-key 是 pacman 4 新加的工具。有了它，用户可以管理 pacman 新签名系统的授信密钥。

## Contents

*   [1 原理](#.E5.8E.9F.E7.90.86)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
    *   [2.1 配置 pacman](#.E9.85.8D.E7.BD.AE_pacman)
    *   [2.2 初始化密钥环](#.E5.88.9D.E5.A7.8B.E5.8C.96.E5.AF.86.E9.92.A5.E7.8E.AF)
*   [3 管理密钥](#.E7.AE.A1.E7.90.86.E5.AF.86.E9.92.A5)
    *   [3.1 验证五大主密钥](#.E9.AA.8C.E8.AF.81.E4.BA.94.E5.A4.A7.E4.B8.BB.E5.AF.86.E9.92.A5)
    *   [3.2 官方开发者密钥](#.E5.AE.98.E6.96.B9.E5.BC.80.E5.8F.91.E8.80.85.E5.AF.86.E9.92.A5)
    *   [3.3 导入非官方密钥](#.E5.AF.BC.E5.85.A5.E9.9D.9E.E5.AE.98.E6.96.B9.E5.AF.86.E9.92.A5)
    *   [3.4 用GPG调试](#.E7.94.A8GPG.E8.B0.83.E8.AF.95)
*   [4 问题解决](#.E9.97.AE.E9.A2.98.E8.A7.A3.E5.86.B3)
    *   [4.1 如何收集熵](#.E5.A6.82.E4.BD.95.E6.94.B6.E9.9B.86.E7.86.B5)
    *   [4.2 密钥导入失败](#.E5.AF.86.E9.92.A5.E5.AF.BC.E5.85.A5.E5.A4.B1.E8.B4.A5)
    *   [4.3 禁用签名检查](#.E7.A6.81.E7.94.A8.E7.AD.BE.E5.90.8D.E6.A3.80.E6.9F.A5)
    *   [4.4 重置所有密钥](#.E9.87.8D.E7.BD.AE.E6.89.80.E6.9C.89.E5.AF.86.E9.92.A5)
    *   [4.5 删除陈旧的包](#.E5.88.A0.E9.99.A4.E9.99.88.E6.97.A7.E7.9A.84.E5.8C.85)
    *   [4.6 Updating keys via proxy](#Updating_keys_via_proxy)
    *   [4.7 gpg: keyserver receive failed: No dirmngr](#gpg:_keyserver_receive_failed:_No_dirmngr)
*   [5 See also](#See_also)

## 原理

Pacman 中的软件包签名使用在[信任网络](http://www.gnupg.org/gph/en/manual.html#AEN385)中的 [GnuPG 密钥](http://www.gnupg.org/) 以保证软件包来自开发者而不是伪装者。

**提示:** 软件包开发者和 TU 都有各自的 PGP 密钥并用它们签名软件包。这些签名能够保证软件包确实来自他们。而每个用户使用 pacman-key 时也会获得一个唯一 PGP 密钥。

目前Archlinux拥有5个[主要签名密钥](https://www.archlinux.org/master-keys/)。 其中至少三个主密匙被用来签署官方开发者和授信用户自己的密钥，而他们将用这些密钥签署自己的包。用户在设置pacman-key时也会生成一个自己的密钥。所以信任网络也会把用户的密钥连接到五大主密钥上面。

密钥也可以用来签名其它的密钥，也就是说签名密钥的所有者能够保证被签名密钥的安全性。要信任一个软件包，需要在用户自己的 PGP 密钥和软件包签名间建立一个密钥链。在 Arch 的密钥结构中，有三种方式：

*   **自定义软件包**: 用户自己构建软件包并用自己的密钥签名认证。
*   **非官方软件包**: 开发者构建软件包并签名它。用户需要用自己的密钥签名开发者的密钥，将其变为可信。
*   **官方软件包**: 开发者构建软件包，而开发者的密钥已经被 Arch 主密钥签名。最终用户用自己的密钥签名主密钥，这样就能信任所有官方开发者。

**提示:** HKP协议使用11371/tcp端口用来通信。为了从服务器得到签署的密钥（使用pacman-key），这个端口必须打开。

**提示:**

关于此问题的背景，请访问博客 [[1]](http://allanmcrae.com/2011/08/pacman-package-signing-1-makepkg-and-repo-add/)[[2]](http://allanmcrae.com/2011/08/pacman-package-signing-2-pacman-key/)[[3]](http://allanmcrae.com/2011/08/pacman-package-signing-3-pacman/)[[4]](http://allanmcrae.com/2011/12/pacman-package-signing-4-arch-linux/) 和 [软件包签名提议](/index.php/Package_Signing_Proposal_for_Pacman "Package Signing Proposal for Pacman") wiki 页面。

## 配置

### 配置 pacman

首先通过 `/etc/pacman.conf` 中的 `SigLevel` 确定要使用的检查级别。文件的注释中列出了几个可选设置， [`pacman.conf`手册页面](https://www.archlinux.org/pacman/pacman.conf.5.html#_package_and_database_signature_checking) 有详细介绍。

签名检查可以设成全局的或针对每个仓库的。如果 `SigLevel` 在 [options] 节中进行了全局设置，那么所有的包都必须签名。包括你自己编译构建的包，也需要使用 `makepkg` 进行签名。

**注意:** 尽管所有的官方软件包现在都进行了签名，但是在2012年6月的时候签名数据库还在开发。如果设置了 `Required` ，那么 `DatabaseOptional` 也应该被设置。

默认的设置 `/etc/pacman.conf`  `SigLevel = Required DatabaseOptional` 会使得系统只安装被授信的密钥签署的软件包。因为 `TrustOnly` 是一个已经被编译进pacman的默认设置。 所以上面这些的效果和 `SigLevel = Required DatabaseOptional TrustedOnly` 是一样的。

上面这些也可以在仓库内部进行设置，比如：

```
[core]
SigLevel = PackageRequired # ’Optional’ here would turn off a global ’Required’ for this repository
Include = /etc/pacman.d/mirrorlist
```

软件仓库中的软件启用了签名验证，但是并不要求仓库数据库也被签名了。

**警告:** SigLevel `TrustAll` 设置仅仅为了测试而存在，使用它会信任未被验证的密钥。对于所有的官方软件源你应该使用 `TrustedOnly` 。

### 初始化密钥环

关于初始化，[收集熵](https://en.wikipedia.org/wiki/Entropy_(computing) "wikipedia:Entropy (computing)") 是必须的。 随意移动鼠标，随即按键盘或者运行一些磁盘级别的操作（比如在其他终端运行`ls -R /`或者`find / -name foo` 或者 `dd if=/dev/sda8 of=/dev/tty7`之类的)应该会收集足够的熵。如果你的系统没有足够的熵，这项工作需要好几个小时，但是如果你有，那么就会快多了。

要初始化 pacman 密钥:

```
# pacman-key --init

```

这会在 `/etc/pacman.d/gnupg` 建立新密钥并生成系统主密钥。

**注意:** 如果`pacman-key --init`运行时系统没有足够的熵，可能会需要很长时间。请在目标机器上安装 [haveged](https://www.archlinux.org/packages/?name=haveged) 或 [rng-tools](https://www.archlinux.org/packages/?name=rng-tools)。然后在用 root 权限执行`pacman-key --init` 前[启动](/index.php/Start "Start") `haveged.service`。

## 管理密钥

### 验证五大主密钥

通过以下命令进行配置：

```
# pacman-key --populate archlinux

```

该命令对 [Master Signing Keys](https://www.archlinux.org/master-keys/) 进行验证，when prompted as these are used to co-sign (and therefore trust) all other packager's keys.

PGP 通常很长(2048 位或更长)，不太容易使用，所以通常创建一个40位十六进制指纹，最后八位被称为密钥 ID，是密钥的名字。长签名可以用来检测两个密钥是否相同。

### 官方开发者密钥

官方开发者和 TU 的密钥已经被主密钥签名认证，所以不需要用 pacman-key 认证它们。pacman 遇到不认识的签名时，它将会询问是否从密钥服务器（设置在{ic|/etc/pacman.d/gnupg/gpg.conf}文件中，或在命令行中使用`--keyserver`选项）下载。

**提示:** Wikipedia maintains a [list of keyservers](https://en.wikipedia.org/wiki/Key_server_(cryptographic) "wikipedia:Key server (cryptographic)").

下载开发者密钥后，以后都不需要下载。以后会用它验证所有这个开发者构建的软件包。

**注意:**

如果开发者和 TU 的密钥是较早之前导入，它们的签名可能还不存在于本地数据库，用下面命令更新：

```
# pacman-key --refresh-keys

```

当使用`--refresh-keys` 时，本地签名也会被远程查找，并收到未找到的消息，这是正常的。

### 导入非官方密钥

有两种方法可以实现：

*   在pacman密钥环中添加你自己的密钥
*   或者启用一个已签名的[非官方软件仓库](/index.php/Unofficial_user_repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Unofficial user repositories (简体中文)")

**Note:** You may first need to run `dirmngr` as root, see [#gpg:_keyserver_receive_failed:_No_dirmngr](#gpg:_keyserver_receive_failed:_No_dirmngr).

First get the key ID (`_keyid_`) from the owner of the key. Then you need to add the key to the keyring:

*   If the key is found on a keyserver, import it with: `# pacman-key -r _keyid_` 

*   If otherwise a link to a keyfile is provided, download it and then run: `# pacman-key --add _/path/to/downloaded/keyfile_` 

Always be sure to verify the fingerprint, as you would with a master key, or any other key which you are going to sign.

```
$ pacman-key -f _keyid_

```

Finally, you need to locally sign the imported key:

```
# pacman-key --lsign-key _keyid_

```

You now trust this key to sign packages.

### 用GPG调试

如果需要，可以直接使用GPG调试pacman钥匙环，例如：

```
# gpg --homedir /etc/pacman.d/gnupg --list-keys

```

## 问题解决

**警告:** Pacman-key 依赖于 [Time_(简体中文)](/index.php/Time_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Time (简体中文)"). 如果系统时间是错误的，将会获得一个报错：

```
error: PackageName: signature from "User <email@archlinux.org>" is invalid
error: failed to commit transaction (invalid or corrupted package (PGP signature))
Errors occured, no packages were upgraded.
```

### 如何收集熵

移动鼠标、不停的随机按键盘按键或者执行磁盘操作例如 `updatedb` 可以生成足够的熵，可能需要一段时间，请保持耐心。Alt+F2-6 到第二个终端不起作用。

如果需要通过 ssh 运行 pacman-key --init，请在目标机器编译安装 [AUR](/index.php/AUR_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "AUR (简体中文)") 中的 [rng-tools](https://www.archlinux.org/packages/?name=rng-tools) 软件包，通过 ssh 连接并运行:

```
# sed -i 's/0/10/' /etc/conf.d/rngd
# rngd -f -r /dev/urandom &
# pacman-key --init

```

pacman-key 成功运行后停止 rngd 并删除软件包。

```
# killall rngd
# pacman -Rns rng-tools

```

### 密钥导入失败

有三种可能的情况导致这个问题：

*   过期的[archlinux-keyring](https://www.archlinux.org/packages/?name=archlinux-keyring) 包。
*   不正确的系统时间。
*   你的ISP屏蔽了用于导入 PGP keys 的端口。

可能某些服务商屏蔽了导入 GPG 的端口。

过期的 [archlinux-keyring](https://www.archlinux.org/packages/?name=archlinux-keyring) 包可能会导致这个问题，你应该首先尝试 [升级系统](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E5.8D.87.E7.BA.A7.E8.BD.AF.E4.BB.B6.E5.8C.85 "Pacman (简体中文)") 能否解决这个问题。

如果这样没有起作用，并且系统时间是正确的，你可以尝试切换到 MIT 提供的公钥服务器(keyserver)：编辑 `/etc/pacman.d/gnupg/gpg.conf` 将 `keyserver hkp://keys.gnupg.net` 替换为

 `keyserver hkp://pgp.mit.edu:11371` 

如果这样也不可以，可以切换到 kjsl 提供的公钥服务器，它使用 80 端口（通常是HTTP协议的端口，一般ISP不会屏蔽）提供了服务。 如果这样没有起作用，可以把 keyserver 设置为 kjsl 提供的公钥服务器（使用 HTTP 协议的 80 端口，一般不会被屏蔽）：

```
keyserver hkp://keyserver.kjsl.com:80

```

如果你关闭了 IPv6 ，GPG 在发现 IPv6 地址时会出错。出现这种情况是尝试使用 IPv4-only 的公钥服务器，例如：

 `keyserver hkp://ipv4.pool.sks-keyservers.net:11371` 

如果你忘记了执行 `pacman-key --populate archlinux` 在你导入公钥的时候可能会遇到一些错误。

### 禁用签名检查

**警告:** 小心使用，禁用签名检查，pacman 会自动安装不信任的软件包。

如果不在意软件包签名，可以完全禁用 PGP 签名检查，编辑 `/etc/pacman.conf` 并注释掉 [options] 下的如下行:

```
SigLevel = Never

```

需要同时注释掉软件源的 SigLevel 设置。

这样就不会进行任何签名检查，和 pacman 4 之前一样。如果这样，就不需要用 pacman-key 建立密钥环。

### 重置所有密钥

如果要删除或重置系统，删除 `/etc/pacman.d/gnupg` 目录并重新运行 `pacman-key --init`，然后添加需要的密钥。

### 删除陈旧的包

如果相同的包持续构建失败，并且你确定你执行的与 pacman-key 有关的操作是正确的，可以尝试移除它们 `rm /var/cache/pacman/pkg/badpackage*` 然后可以它们将会被重新下载构建。

这样可能可以解决在升级时遇到的`error: linux: signature from "Some Person <Some.Person@example.com>" is invalid` 或者相似的报错 (i.e. you might not be the victim of a MITM attack after all, your downloaded file was simply corrupt).

### Updating keys via proxy

There's a bug in _gnupg_ which prevents updating keys via http proxies ([https://bugs.g10code.com/gnupg/issue1786](https://bugs.g10code.com/gnupg/issue1786)).

To work around that problem you can do the following:

Change `/etc/hosts`:

 `/etc/hosts` 

```
127.0.0.1 pool.sks-keyservers.net

```

Setup tunnel with [socat](https://www.archlinux.org/packages/?name=socat). Needs to be run as root because you need a listener on TCP port 80.

```
# socat TCP-LISTEN:80,reuseaddr,fork PROXY:localhost:pool.sks-keyservers.net:80,proxyport=3128

```

Refresh keys:

```
# pacman-key --refresh-keys

```

Revert the configuration when proxy is no longer needed.

### gpg: keyserver receive failed: No dirmngr

See [FS#42798](https://bugs.archlinux.org/task/42798). Run:

```
# dirmngr < /dev/null

```

Alternatively, create `/root/.gnupg/dirmngr_ldapservers.conf`. [[5]](https://bbs.archlinux.org/viewtopic.php?pid=1480388#p1480388)

## See also

*   [DeveloperWiki:Package Signing Proposal for Pacman](/index.php/Package_Signing_Proposal_for_Pacman "Package Signing Proposal for Pacman")
*   [Pacman Package Signing – 1: Makepkg and Repo-add](http://allanmcrae.com/2011/08/pacman-package-signing-1-makepkg-and-repo-add/)
*   [Pacman Package Signing – 2: Pacman-key](http://allanmcrae.com/2011/08/pacman-package-signing-2-pacman-key/)
*   [Pacman Package Signing – 3: Pacman](http://allanmcrae.com/2011/08/pacman-package-signing-3-pacman/)
*   [Pacman Package Signing – 4: Arch Linux](http://allanmcrae.com/2011/12/pacman-package-signing-4-arch-linux/)