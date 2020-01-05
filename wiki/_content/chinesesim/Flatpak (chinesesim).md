Related articles

*   [Snapd](/index.php/Snapd "Snapd")
*   [bubblewrap](/index.php/Bubblewrap "Bubblewrap")

**翻译状态：** 本文是英文页面 [Flatpak](/index.php/Flatpak "Flatpak") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2019-12-30，点击[这里](https://wiki.archlinux.org/index.php?title=Flatpak&diff=0&oldid=592857)可以查看翻译后英文页面的改动。

引自项目 [README](https://github.com/flatpak/flatpak/blob/master/README.md)：“[Flatpak](http://flatpak.org) 是一个 Linux 桌面程序的构建、分发和沙箱化运行系统。”

引自 [flatpak(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/flatpak.1)：

	Flatpak 是一个用来管理应用和应用所使用的运行时的工具。在 Flatpak 模型中，应用的构建和分发不依赖其主系统，并且它们在运行时一定程度上独立于主系统（'沙箱化'）。

	Flatpak 使用 [OSTree](https://ostree.readthedocs.io/en/latest/) 以分发和部署数据。它使用的仓库是 OSTree 仓库并且可以用 ostree 的工具来操作。已安装的运行时和应用都已经过 OSTree 检出。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 安装](#安装)
*   [2 管理仓库](#管理仓库)
    *   [2.1 添加一个仓库](#添加一个仓库)
    *   [2.2 删除一个仓库](#删除一个仓库)
    *   [2.3 仓库列表](#仓库列表)
*   [3 管理运行时和应用](#管理运行时和应用)
    *   [3.1 搜索远程仓库的运行时和应用](#搜索远程仓库的运行时和应用)
    *   [3.2 列出所有可用的运行时和应用](#列出所有可用的运行时和应用)
    *   [3.3 安装一个运行时或应用](#安装一个运行时或应用)
    *   [3.4 列出所有已安装的运行时和应用](#列出所有已安装的运行时和应用)
    *   [3.5 运行应用](#运行应用)
    *   [3.6 升级一个运行时或应用](#升级一个运行时或应用)
    *   [3.7 卸载一个运行时或应用](#卸载一个运行时或应用)
    *   [3.8 添加 Flatpak .desktop 文件到您的菜单](#添加_Flatpak_.desktop_文件到您的菜单)
    *   [3.9 查看应用沙箱的权限](#查看应用沙箱的权限)
    *   [3.10 覆盖应用的沙箱权限](#覆盖应用的沙箱权限)
*   [4 创建自定义基本运行时](#创建自定义基本运行时)
    *   [4.1 使用 pacman 创建应用](#使用_pacman_创建应用)
*   [5 另见](#另见)

## 安装

[安装](/index.php/Help:Reading_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#安装软件包 "Help:Reading (简体中文)") [flatpak](https://www.archlinux.org/packages/?name=flatpak) 软件包。

**注意:** 如果你想使用 `flatpak-builder` 来构建 flatpak，你将需要安装可选的依赖 [elfutils](https://www.archlinux.org/packages/?name=elfutils) 和 [patch](https://www.archlinux.org/packages/?name=patch)。

## 管理仓库

### 添加一个仓库

要添加一个远程 flatpak 仓库，执行：

```
$ flatpak remote-add *name* *location*

```

这其中 *name* 是新远程仓库的名字，而 *location* 是路径或仓库的 URL。

例如要添加官方仓库 [Flathub repository](https://flathub.org/)：

```
$ flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo

```

### 删除一个仓库

要删除一个远程 flatpak 仓库，执行：

```
$ flatpak remote-delete *name*

```

这其中 *name* 是要删除的远程仓库的名字。

### 仓库列表

要列出所有已添加的仓库列表，执行：

```
$ flatpak remotes

```

## 管理运行时和应用

### 搜索远程仓库的运行时和应用

在能搜索新添加的远程仓库中的运行时和应用之前，我们需要为此获取软件应用流的数据：

 `$ flatpak update` 
```
Looking for updates...
Updating appstream data for remote *name*

```

之后我们可以通过 `flatpak search *packagename*` 命令来实现搜索，例如在配置完成的远程仓库 `flathub` 中搜索 `libreoffice` 软件包：

 `$ flatpak search libreoffice` 
```
Application ID              Version Branch Remotes Description                       
org.libreoffice.LibreOffice         stable flathub The LibreOffice productivity suite

```

### 列出所有可用的运行时和应用

要列出远程仓库 *remote* 中所有可用的运行时和应用，执行：

```
$ flatpak remote-ls *remote*

```

### 安装一个运行时或应用

要安装一个运行时或应用，执行：

```
$ flatpak install *remote* *name*

```

这其中 *remote* 是远程仓库的名字，而 *name* 是待安装的应用或运行时的名字。

**提示：** 您可以使用部分标识符 `flatpak install *partial-name*` (例如 `flatpak install libreoffice`)。

### 列出所有已安装的运行时和应用

要列出所有已安装的运行时和应用，执行：

```
$ flatpak list

```

### 运行应用

Flatpak 应用也可以通过命令行运行：

```
$ flatpak run *name*

```

### 升级一个运行时或应用

要升级一个名为 *name* 的运行时或应用，执行：

```
$ flatpak update *name*

```

### 卸载一个运行时或应用

要卸载一个名为 *name* 运行时或应用，执行：

```
$ flatpak uninstall *name*

```

**提示：** 你可以卸载不再使用的 flatpak 依赖（即无应用/运行时依赖的孤立包），执行 `flatpak uninstall --unused`。

### 添加 Flatpak .desktop 文件到您的菜单

Flatpak 期望窗口管理器按照 XDG_DATA_DIRS 环境变量来查找应用。这可能需要重启此会话，或者启动器可能并不支持这些。这种情况下您想要编辑需要扫描的目录列表，可将如下路径添加到变量中：

```
~/.local/share/flatpak/exports/share/applications
/var/lib/flatpak/exports/share/applications

```

目前已知此方法在 Awesome 中是必须的。

### 查看应用沙箱的权限

Flatpak 应用遵守着预定义的沙箱规则，这些规则规定了应用允许访问的资源文件系统目录。 要查看确切的应用权限，执行：

```
$ flatpak info --show-permissions *name*

```

沙箱权限的依赖列表可以在 [官方 flatpak 说明](https://docs.flatpak.org/en/latest/sandbox-permissions-reference.html) 中找到。

### 覆盖应用的沙箱权限

如果你发现应用的预定义权限过松或过紧，你可以使用 `flatpak override` 命令更改任何你希望更改的地方。 例如：

```
flatpak override --nofilesystem=home *name*

```

这会禁止应用访问你的家目录。

所有可以赋予权限的类型，如设备、文件系统或 socket ，都有一行命令以独立选择允许或禁止确切的权限。例如，允许访问设备时可以是 `--device=*device_name*`，而 `--nodevice=*device_name*` 会禁止访问设备。

对于所有可操作的权限类型，详见：[flatpak-override(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/flatpak-override.1)

下面的命令可将所有更改过的权限重设为默认：

```
$ flatpak override --reset *name*

```

## 创建自定义基本运行时

**警告:** 如果你想向公众发布一个作为 Flatpak 的软件，那么基于 Arch 系统的运行时是不合适的。在这种情况下，您应根据 [官方说明](http://docs.flatpak.org) 来使用 [共有运行时](http://flatpak.org/runtimes.html) 将您的软件融入进合适的 Flatpak 生态系统中。

**注意:** 你可能想要使用一个不被信任的、无特权的用户账户来打包不被信任的软件，因为软件在创建应用和运行时期间是没有被沙箱化的。

**注意:** 当向其他人分发软件包时，您可能需要遵守法定义务，应要求提供一些已打包软件的源代码。你可能要使用 [ABS](/index.php/ABS "ABS") 来从源代码生成这些软件包。

您可以创建一个自定义的、基于 Arch 的基本运行时，并通过 pacman 使用 Flatpak 的 SDK。之后您可以使用它来创建和打包应用。对于个人使用来说，这是除了默认的 `org.freedesktop.BasePlatform` 和 `org.freedesktop.BaseSdk` 运行时之外的另一个选择。

除了 [flatpak](https://www.archlinux.org/packages/?name=flatpak) 以外，您需要安装 [fakeroot](https://www.archlinux.org/packages/?name=fakeroot)，而为了使 pacman hooks 支持，您也需要安装 [fakechroot](https://www.archlinux.org/packages/?name=fakechroot)。

首先，创建一个目录以用来作为生成运行时/应用的位置。

```
$ mkdir *myflatpakbuilddir*
$ cd *myflatpakbuilddir*

```

之后您可以准备一个目录作为生成运行时基本平台的位置。这些文件子目录将会成为之后沙箱中的 `/usr` 目录的内容。因此您将需要创建符号链接使得默认 `/usr/share` 等源自 Arch 的路径仍然可以由通常的路径访问。

```
$ mkdir -p *myruntime*/files/var/lib/pacman
$ touch *myruntime*/files/.ref
$ ln -s /usr/usr/share *myruntime*/files/share
$ ln -s /usr/usr/include *myruntime*/files/include
$ ln -s /usr/usr/local *myruntime*/files/local

```

使您的主系统字体在 Arch 运行时中可用：

```
$ mkdir -p *myruntime*/files/usr/share/fonts
$ ln -s /run/host/fonts *myruntime*/files/usr/share/fonts/flatpakhostfonts

```

您需要或想要在为运行时安装软件包之前调整您的 `pacman.conf`。复制 `/etc/pacman.conf` 到您的构建目录，之后再进行下列改变：

*   移除 `CheckSpace` 选项，即 pacman 将不会抱怨检测硬盘空间时发现根文件系统的错误。
*   移除所有不需要的自定义仓库和 `IgnorePkg`，`IgnoreGroup`，`NoUpgrade` 和 `NoExtract` 的设置，即只有主系统需要的这些仓库。

现在为运行时安装软件包。

```
$ fakechroot fakeroot pacman -Syu --root *myruntime*/files --dbpath *myruntime*/files/var/lib/pacman --config pacman.conf base
$ mv pacman.conf *myruntime*/files/etc/pacman.conf

```

通过编辑 `*myruntime*/files/etc/locale.gen` 设置所用的 [locales](/index.php/Locale_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Locale (简体中文)")。之后重新生成运行时的 locales。

```
$ fakechroot chroot *myruntime*/files locale-gen

```

基本 SDK 可以通过基本运行时加上创建软件包和运行 pacman 所需要的应用来创建。

```
$ cp -r *myruntime* mysdk
$ fakechroot fakeroot pacman -S --root mysdk/files --dbpath mysdk/files/var/lib/pacman --config mysdk/files/etc/pacman.conf base-devel fakeroot fakechroot --needed

```

插入运行时和 SDK 的元数据。

 `*myruntime*/metadata` 
```
[Runtime]
name=org.mydomain.BasePlatform
runtime=org.mydomain.BasePlatform/x86_64/2016-06-26
sdk=org.mydomain.BaseSdk/x86_64/2016-06-26
```
 `mysdk/metadata` 
```
[Runtime]
name=org.mydomain.BaseSdk
runtime=org.mydomain.BasePlatform/x86_64/2016-06-26
sdk=org.mydomain.BaseSdk/x86_64/2016-06-26
```

加入基本运行时和 SDK 到目前目录的本地仓库中。您可能想要给它们附上合适的提交（commit）信息如 “My Arch base runtime” 和 “My Arch base SDK”。

```
$ ostree init --mode archive-z2 --repo=.
$ EDITOR="nano -w" ostree commit -b runtime/org.mydomain.BasePlatform/x86_64/2016-06-26 --tree=dir=*myruntime*
$ EDITOR="nano -w" ostree commit -b runtime/org.mydomain.BaseSdk/x86_64/2016-06-26 --tree=dir=mysdk
$ ostree summary -u

```

安装运行时和 SDK。

```
$ flatpak remote-add --user --no-gpg-verify myarchos file://$(pwd)
$ flatpak install --user myarchos org.mydomain.BasePlatform 2016-06-26
$ flatpak install --user myarchos org.mydomain.BaseSdk 2016-06-26

```

### 使用 pacman 创建应用

作为创建应用 [通常方式](http://flatpak.org/developer.html)的一种替代方案，我们可以使用 pacman 创建普通 Arch 软件包的一种容器化版本。注意 `/usr` 目录在创建应用时是只读的，故我们在创建一个应用时不能使用 Arch 的软件包。要使用 pacman 创建一个真正的应用，我们可以

*   使用 pacman 创建一个包含所有依赖包的运行时
*   之后 [像往常一样](http://flatpak.org/developer.html) 自己编译应用，或可能通过自定义 [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") 为 Flatpak 特制的 pacman 使用 `--prefix=/app` 制作 `configure` 脚本，

或者我们可以

*   使用 pacman 创建一个包含所有通过 pacman 安装的应用的运行时
*   之后创建一个虚拟应用来启动它。

对于使用后一种方法，首先通过 pacman 创建一个运行时，比如这一个为了 [gedit](https://www.archlinux.org/packages/?name=gedit)。这个运行时是首先初始化，准备与 pacman 一起使用的。

```
$ flatpak build-init -w geditruntime org.mydomain.geditruntime org.mydomain.BaseSdk org.mydomain.BasePlatform 2016-06-26
$ flatpak build geditruntime sed -i "s/^#Server/Server/g" /etc/pacman.d/mirrorlist
$ flatpak build geditruntime ln -s /usr/var/lib /var/lib
$ flatpak build geditruntime fakeroot pacman-key --init
$ flatpak build geditruntime fakeroot pacman-key --populate archlinux

```

之后这个软件包安装完成。主系统的网络必须能够使 pacman 正常工作。

```
$ flatpak build --share=network geditruntime fakechroot fakeroot pacman --root /usr -S gedit

```

你可以在完成运行时前测试安装是否成功（未进行合适的沙箱化）。

```
$ flatpak build --socket=x11 geditruntime gedit

```

现在结束创建运行时并将其导出到一个新的本地仓库。pacman 的 GnuPG 密钥可能会有许可冲突，故需要先被移除。

```
$ flatpak build geditruntime rm -r /etc/pacman.d/gnupg
$ flatpak build-finish geditruntime
$ sed -i "s/\[Application\]/\[Runtime\]/;s/runtime=org.mydomain.BasePlatform/runtime=org.mydomain.geditruntime/" geditruntime/metadata
$ flatpak build-export -r geditrepo geditruntime

```

接下来创建一个虚拟应用。

```
$ flatpak build-init geditapp org.gnome.gedit org.mydomain.BaseSdk org.mydomain.geditruntime

```

现在已经完成了构建虚拟应用。你可以在将应用沙箱化时，通过完成创建时给予额外的选项来微调它的访问权限。对于可用的选项，详见 [Flatpak documentation](#另见) 和 [GNOME manifest files](https://gitlab.gnome.org/GNOME/gnome-apps-nightly/tree/master)。或者，可以在完成创建后按照您的期望调整 `geditapp/metadata`，但要在导出前完成。当元数据文件完成后，将应用导出到仓库。

```
$ flatpak build-finish geditapp --socket=x11 *[possibly other options]* --command=gedit
$ flatpak build-export geditrepo geditapp

```

将它和运行时一起安装。

```
$ flatpak --user remote-add --no-gpg-verify geditrepo geditrepo
$ flatpak install --user geditrepo org.mydomain.geditruntime
$ flatpak install --user geditrepo org.gnome.gedit
$ flatpak run org.gnome.gedit

```

## 另见

*   [Official website](http://flatpak.org)
*   [Official Github wiki](https://github.com/flatpak/flatpak/wiki)
*   [Wikipedia page](https://en.wikipedia.org/wiki/Flatpak "wikipedia:Flatpak")
*   [Gnome SandboxedApps](https://wiki.gnome.org/Projects/SandboxedApps)
*   [KDE Testing Runtime and Applications](https://community.kde.org/Guidelines_and_HOWTOs/Flatpak)