Related articles

*   [GnuPG](/index.php/GnuPG "GnuPG")
*   [DeveloperWiki:Package signing](/index.php/DeveloperWiki:Package_signing "DeveloperWiki:Package signing")

**翻译状态：** 本文是英文页面 [Pacman/Package_signing](/index.php/Pacman/Package_signing "Pacman/Package signing") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-10-17，点击[这里](https://wiki.archlinux.org/index.php?title=Pacman%2FPackage_signing&diff=0&oldid=490037)可以查看翻译后英文页面的改动。

为了保证软件包来自开发者, Pacman 使用[信任网络](http://www.gnupg.org/gph/en/manual.html#AEN385)中的 [GnuPG 密钥](http://www.gnupg.org/)进行软件包验证。目前 Archlinux 的主要签名密钥在[这里](https://www.archlinux.org/master-keys/)。 其中至少三个主密匙被用来签署官方开发者和授信用户自己的密钥，而他们将用这些密钥签署自己的包。用户在设置pacman-key时也会生成一个自己的密钥。所以信任网络也会把用户的密钥连接到五大主密钥上面。

密钥也可以用来签名其它的密钥，也就是说签名密钥的所有者能够保证被签名密钥的安全性。要信任一个软件包，需要在用户自己的 PGP 密钥和软件包签名间建立一个密钥链。在 Arch 的密钥结构中，有三种方式：

*   **自定义软件包**: 用户自己构建软件包并用自己的密钥签名认证。
*   **非官方软件包**: 开发者构建软件包并签名它。用户需要用自己的密钥签名开发者的密钥，将其变为可信。
*   **官方软件包**: 开发者构建软件包，而开发者的密钥已经被 Arch 主密钥签名。最终用户用自己的密钥签名主密钥，这样就能信任所有官方开发者。

**提示：** HKP协议使用11371/tcp端口用来通信。为了从服务器得到签署的密钥（使用pacman-key），这个端口必须打开。

**提示：**

关于此问题的背景，请访问博客 [[1]](http://allanmcrae.com/2011/08/pacman-package-signing-1-makepkg-and-repo-add/)[[2]](http://allanmcrae.com/2011/08/pacman-package-signing-2-pacman-key/)[[3]](http://allanmcrae.com/2011/08/pacman-package-signing-3-pacman/)[[4]](http://allanmcrae.com/2011/12/pacman-package-signing-4-arch-linux/) 和 [软件包签名提议](/index.php/Package_Signing_Proposal_for_Pacman "Package Signing Proposal for Pacman") wiki 页面。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 配置](#配置)
    *   [1.1 配置 pacman](#配置_pacman)
    *   [1.2 初始化密钥环](#初始化密钥环)
*   [2 管理密钥](#管理密钥)
    *   [2.1 验证主密钥](#验证主密钥)
    *   [2.2 官方开发者密钥](#官方开发者密钥)
    *   [2.3 导入非官方密钥](#导入非官方密钥)
    *   [2.4 用GPG调试](#用GPG调试)
*   [3 问题解决](#问题解决)
    *   [3.1 如何收集熵](#如何收集熵)
    *   [3.2 密钥导入失败](#密钥导入失败)
    *   [3.3 禁用签名检查](#禁用签名检查)
    *   [3.4 重置所有密钥](#重置所有密钥)
    *   [3.5 删除陈旧的包](#删除陈旧的包)
    *   [3.6 通过代理更新密钥](#通过代理更新密钥)
*   [4 参阅](#参阅)

## 配置

### 配置 pacman

首先通过 `/etc/pacman.conf` 中的 `SigLevel` 确定要使用的检查级别。文件的注释中列出了几个可选设置， [`pacman.conf`手册页面](https://www.archlinux.org/pacman/pacman.conf.5.html#_package_and_database_signature_checking) 有详细介绍。

签名检查可以设成全局的或针对每个仓库的。如果 `SigLevel` 在 [options] 节中进行了全局设置，那么所有的包都必须签名。包括你自己编译构建的包，也需要使用 `makepkg` 进行签名。

**注意:** 尽管所有的官方软件包现在都进行了签名，但是在2012年6月的时候签名数据库还在开发。如果设置了 `Required` ，那么 `DatabaseOptional` 也应该被设置。

默认的设置下，系统只安装被授信的密钥签署的软件包。

 `/etc/pacman.conf`  `SigLevel = Required DatabaseOptional` 

因为 `TrustOnly` 是一个已经被编译进pacman的默认设置。

所以上面这些的效果和下面是一样的：

```
SigLevel = Required DatabaseOptional TrustedOnly

```

上面这些也可以在仓库内部进行设置，比如：

```
[core]
SigLevel = PackageRequired # ’Optional’ here would turn off a global ’Required’ for this repository
Include = /etc/pacman.d/mirrorlist
```

软件仓库中的软件启用了签名验证，但是并不要求仓库数据库也被签名了。

**警告:** SigLevel `TrustAll` 设置仅仅为了测试而存在，使用它会信任未被验证的密钥。对于所有的官方软件源你应该使用 `TrustedOnly` 。

### 初始化密钥环

关于初始化，[收集熵](https://en.wikipedia.org/wiki/Entropy_(computing) 是必须的。 随意移动鼠标，随即按键盘或者运行一些磁盘级别的操作（比如在其他终端运行`ls -R /`或者`find / -name foo` 或者 `dd if=/dev/sda8 of=/dev/tty7`之类的)应该会收集足够的熵。如果你的系统没有足够的熵，这项工作需要好几个小时，但是如果你有，那么就会快多了。

要初始化 pacman 密钥:

```
# pacman-key --init

```

这会在 `/etc/pacman.d/gnupg` 建立新密钥并生成系统主密钥。

**注意:** 如果`pacman-key --init`运行时系统没有足够的熵，可能会需要很长时间。请在目标机器上安装 [haveged](/index.php/Haveged "Haveged") 或 [rng-tools](/index.php/Rng-tools "Rng-tools")。然后在用 root 权限执行`pacman-key --init` 前[启动](/index.php/Start "Start") `haveged.service`。

## 管理密钥

### 验证主密钥

通过以下命令进行配置：

```
# pacman-key --populate archlinux

```

该命令对 [Master Signing Keys](https://www.archlinux.org/master-keys/) 进行验证，when prompted as these are used to co-sign (and therefore trust) all other packager's keys.

PGP 通常很长(2048 位或更长)，不太容易使用，所以通常创建一个40位十六进制指纹，最后八位被称为密钥 ID，是密钥的名字。长签名可以用来检测两个密钥是否相同。

### 官方开发者密钥

官方开发者和 TU 的密钥已经被主密钥签名认证，所以不需要用 pacman-key 认证它们。pacman 遇到不认识的签名时，它将会询问是否从密钥服务器（设置在`/etc/pacman.d/gnupg/gpg.conf`文件中，或在命令行中使用`--keyserver`选项）下载。

**提示：** Wikipedia maintains a [list of keyservers](https://en.wikipedia.org/wiki/Key_server_(cryptographic) "wikipedia:Key server (cryptographic)").

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

首先从密钥持有者手中拿到密钥 ID(`*keyid*`)，然后把密钥加入密钥环：

*   如果密钥位于密钥服务器，通过下面命令导入： `# pacman-key -r *keyid*` 

*   如果提供了地址，先下载，然后用下面密钥导入： `# pacman-key --add */path/to/downloaded/keyfile*` 

对于所有要签名的密钥，都通过指纹进行验证：

```
$ pacman-key -f *keyid*

```

最后，本地签名导入的密钥：

```
# pacman-key --lsign-key *keyid*

```

现在可以用这个密钥签名软件包了。

### 用GPG调试

如果需要，可以直接使用GPG调试pacman钥匙环，例如：

```
# gpg --homedir /etc/pacman.d/gnupg --list-keys

```

## 问题解决

**警告:** Pacman-key 依赖于 [Time (简体中文)](/index.php/Time_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Time (简体中文)"). 如果系统时间是错误的，将会获得一个报错：
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
*   *pacman* 缓存中包含之前的未签名软件包
*   未正确设置 `dirmngr`

过期的 [archlinux-keyring](https://www.archlinux.org/packages/?name=archlinux-keyring) 包可能会导致这个问题，你应该首先尝试 [升级系统](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#升级软件包 "Pacman (简体中文)") 能否解决这个问题。

请确保 `/root/.gnupg/dirmngr_ldapservers.conf` 文件存在，`# dirmngr` 可以正常运行. 如果没有，创建一个空文件，并执行 `# dirmngr`。

如果这样没有起作用，并且系统时间是正确的，你可以尝试切换到 MIT 提供的公钥服务器(keyserver)：编辑 `/etc/pacman.d/gnupg/gpg.conf` 将 `keyserver hkp://keys.gnupg.net` 替换为

```
keyserver hkp://pgp.mit.edu:11371

```

如果这样也不可以，可以切换到 kjsl 提供的公钥服务器，它使用 80 端口（通常是HTTP协议的端口，一般ISP不会屏蔽）提供了服务。 如果这样没有起作用，可以把 keyserver 设置为 kjsl 提供的公钥服务器（使用 HTTP 协议的 80 端口，一般不会被屏蔽）：

```
keyserver hkp://keyserver.kjsl.com:80

```

如果你关闭了 IPv6 ，GPG 在发现 IPv6 地址时会出错。出现这种情况是尝试使用 IPv4-only 的公钥服务器，例如：

 `keyserver hkp://ipv4.pool.sks-keyservers.net:11371` 

如果 80 端口也关闭了，可以使用加密端口

```
keyserver hkps://hkps.pool.sks-keyservers.net:443

```

如果你忘记了执行 `pacman-key --populate archlinux` 在你导入公钥的时候可能会遇到一些错误。

如果上面方法都不起作用，pacman 缓存 `/var/cache/pacman/pkg/` 可以包含之前下载的未签名软件包，手动清空缓存：

```
# pacman -Sc

```

### 禁用签名检查

**警告:** 小心使用，禁用签名检查，pacman 会自动安装不信任的软件包。

如果不在意软件包签名，可以完全禁用 PGP 签名检查，编辑 `/etc/pacman.conf` 并取消注释 [options] 下的如下行:

```
SigLevel = Never

```

需要同时注释掉软件源的 SigLevel 设置，因为他们会覆盖全局设置。

这样就不会进行任何签名检查，和 pacman 4 之前一样。如果这样，就不需要用 pacman-key 建立密钥环。

### 重置所有密钥

如果要删除或重置系统，删除 `/etc/pacman.d/gnupg` 目录并重新运行 `pacman-key --init`，然后添加需要的密钥。

### 删除陈旧的包

如果相同的包持续构建失败，并且你确定你执行的与 pacman-key 有关的操作是正确的，可以尝试移除它们 `rm /var/cache/pacman/pkg/badpackage*` 然后可以它们将会被重新下载构建。

这样可能可以解决在升级时遇到的`error: linux: signature from "Some Person <Some.Person@example.com>" is invalid` 或者相似的报错 (i.e. you might not be the victim of a MITM attack after all, your downloaded file was simply corrupt).

### 通过代理更新密钥

要使用代理更新密钥，必须同时在 `/etc/gnupg/dirmngr.conf` 和 `/etc/pacman.d/gnupg/dirmngr.conf` 中设置 `honor-http-proxy` 选项。更多信息请阅读 [GnuPG#Use a keyserver](/index.php/GnuPG#Use_a_keyserver "GnuPG").

**Note:** 如果 *pacman-key* 没有用 `honor-http-proxy` 选项，执行失败，重启可能能够解决问题。

## 参阅

*   [DeveloperWiki:Package Signing Proposal for Pacman](/index.php/Package_Signing_Proposal_for_Pacman "Package Signing Proposal for Pacman")
*   [Pacman Package Signing – 1: Makepkg and Repo-add](http://allanmcrae.com/2011/08/pacman-package-signing-1-makepkg-and-repo-add/)
*   [Pacman Package Signing – 2: Pacman-key](http://allanmcrae.com/2011/08/pacman-package-signing-2-pacman-key/)
*   [Pacman Package Signing – 3: Pacman](http://allanmcrae.com/2011/08/pacman-package-signing-3-pacman/)
*   [Pacman Package Signing – 4: Arch Linux](http://allanmcrae.com/2011/12/pacman-package-signing-4-arch-linux/)