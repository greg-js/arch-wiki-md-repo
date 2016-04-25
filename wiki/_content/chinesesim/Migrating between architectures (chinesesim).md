**翻译状态：** 本文是英文页面 [Migrating_Between_Architectures_Without_Reinstalling](/index.php/Migrating_Between_Architectures_Without_Reinstalling "Migrating Between Architectures Without Reinstalling") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2013-05-09，点击[这里](https://wiki.archlinux.org/index.php?title=Migrating_Between_Architectures_Without_Reinstalling&diff=0&oldid=256194)可以查看翻译后英文页面的改动。

该页文档包含了在32位与64位这两个架构之间双向迁移的潜在方法。这些方法避免了重装整个系统，方法一使用liveCD，另一种从系统本身更改......

**Warning:** 除非显式声明，所有的方法都是未经考验的，并可能不可挽回的损害你的系统。请自己斟酌利弊,承担风险

## Contents

*   [1 基本需求](#.E5.9F.BA.E6.9C.AC.E9.9C.80.E6.B1.82)
    *   [1.1 确定64位架构](#.E7.A1.AE.E5.AE.9A64.E4.BD.8D.E6.9E.B6.E6.9E.84)
    *   [1.2 空间需求](#.E7.A9.BA.E9.97.B4.E9.9C.80.E6.B1.82)
    *   [1.3 电力供应](#.E7.94.B5.E5.8A.9B.E4.BE.9B.E5.BA.94)
    *   [1.4 Fallback packages](#Fallback_packages)
*   [2 方法 1: 使用 Arch LiveCD](#.E6.96.B9.E6.B3.95_1:_.E4.BD.BF.E7.94.A8_Arch_LiveCD)
*   [3 方法 2: 从正在运行的系统](#.E6.96.B9.E6.B3.95_2:_.E4.BB.8E.E6.AD.A3.E5.9C.A8.E8.BF.90.E8.A1.8C.E7.9A.84.E7.B3.BB.E7.BB.9F)
    *   [3.1 准备软件包](#.E5.87.86.E5.A4.87.E8.BD.AF.E4.BB.B6.E5.8C.85)
        *   [3.1.1 缓存旧软件包](#.E7.BC.93.E5.AD.98.E6.97.A7.E8.BD.AF.E4.BB.B6.E5.8C.85)
        *   [3.1.2 改变 Pacman 架构](#.E6.94.B9.E5.8F.98_Pacman_.E6.9E.B6.E6.9E.84)
        *   [3.1.3 下载新的软件包](#.E4.B8.8B.E8.BD.BD.E6.96.B0.E7.9A.84.E8.BD.AF.E4.BB.B6.E5.8C.85)
    *   [3.2 软件包安装](#.E8.BD.AF.E4.BB.B6.E5.8C.85.E5.AE.89.E8.A3.85)
        *   [3.2.1 安装64位内核](#.E5.AE.89.E8.A3.8564.E4.BD.8D.E5.86.85.E6.A0.B8)
        *   [3.2.2 控制台终端](#.E6.8E.A7.E5.88.B6.E5.8F.B0.E7.BB.88.E7.AB.AF)
        *   [3.2.3 安装 Pacman](#.E5.AE.89.E8.A3.85_Pacman)
        *   [3.2.4 安装剩余的软件包](#.E5.AE.89.E8.A3.85.E5.89.A9.E4.BD.99.E7.9A.84.E8.BD.AF.E4.BB.B6.E5.8C.85)
*   [4 清理](#.E6.B8.85.E7.90.86)
    *   [4.1 Makepkg 编译器标志](#Makepkg_.E7.BC.96.E8.AF.91.E5.99.A8.E6.A0.87.E5.BF.97)
*   [5 疑难解答](#.E7.96.91.E9.9A.BE.E8.A7.A3.E7.AD.94)
    *   [5.1 Busybox](#Busybox)
    *   [5.2 Lib32-glibc](#Lib32-glibc)
    *   [5.3 KDE不能正确启动](#KDE.E4.B8.8D.E8.83.BD.E6.AD.A3.E7.A1.AE.E5.90.AF.E5.8A.A8)
    *   [5.4 Mutt 开启 cache 后出问题](#Mutt_.E5.BC.80.E5.90.AF_cache_.E5.90.8E.E5.87.BA.E9.97.AE.E9.A2.98)
*   [6 参阅](#.E5.8F.82.E9.98.85)

## 基本需求

### 确定64位架构

如果你已经运行x86_64系统但是想要迁移到32位架构这一步于你无关，你可以略过此步。

为了运行64位软件，你必须有一个64位兼容的cpu。大多数现代cpu可以运行64位软件。你可以通过以下命令检查你的cpu：

```
grep --color '\<lm\>' /proc/cpuinfo

```

对支持x86_64的cpu将返回 `lm` 标志 (“long mode”) 被高亮。注意 *lahf_lm* 是不同的标志，与是否支持64位无关。

### 空间需求

你应该在迁移期间为 `/var/cache/pacman/pkg` 预备当前大约两倍的空间。这是假设只有当前安装的软件包都在缓存中， 好像 “pacman -Sc” (clean) 刚刚运行过。磁盘占据空间的增加源于在两个架构间迁移时没个软件包的复制。

如果你没有足够的空间请使用*[GParted](/index.php/GParted "GParted")* 重新划分相关分区的大小，或者将另一个分区挂载到 */var/cache/pacman*

在系统完全在新架构操作前请勿从缓存中移除旧架构中的软件包。过早地移除软件包将使你不能回退和撤销改变。

### 电力供应

迁移可能相当耗费时间，而且不方便中断。你应该至少计划一个小时，取决于你要安装的文件大小和网速(尽管你可以在关键部分前把一切都先下载下来)。确定你连上了稳定的电源，最好有某种故障恢复或备用电池。

### Fallback packages

如果迁移中途失败了，有些软件包可以解决这种情况，但它们要在主要的包被迁移之前安装。关于它们的更多细节参见下面的[#Troubleshooting](#Troubleshooting) 部分。

一个软件包叫作[busybox](https://www.archlinux.org/packages/?name=busybox), 可以用来撤销更改。 它静态链接并不依赖任何库。32位(i686)版本应使用如下命令安装：

```
# pacman -S busybox

```

另一个包是 [lib32-glibc](https://www.archlinux.org/packages/?name=lib32-glibc), 来自 [Multilib](/index.php/Multilib_Project "Multilib Project") x86_64 仓库。可能仅仅在从32位迁移时有用，任何情况下你都可以安全的略过这个包。你可以通过显式调用 `/lib/ld-linux.so.2`来运行32位的程序。通过以下命令安装：

```
# pacman -S lib32-glibc

```

## 方法 1: 使用 Arch LiveCD

1.  下载、刻录、并从64位liveCD启动
2.  在LiveCD上配置你的网络，然后让pacman使用你要迁移到的新架构的软件仓库。
3.  把你当前系统挂载到 `/mnt` 目录. 例如: `mount /dev/sda1 /mnt`
4.  使用如下脚本升级本地pacman数据库，获得你已经安装的所有软件列表然后重新安装它们：
5.  你可能需要运行这个脚本两次, 因为许多包第一次运行post-install(edit:这是什么？)脚本会失败. 这是因为sed、 grep、perl等在错误的架构下。
6.  你可能还需要更新initrd, chroot到/mnt并且运行mkinitcpio -p linux.

```
#!/bin/bash

MOUNTED_INSTALL='/mnt'
TEMP_FILE='/tmp/packages.list'

pacman --root $MOUNTED_INSTALL -Sy
pacman --root $MOUNTED_INSTALL --cachedir $MOUNTED_INSTALL/var/cache/pacman/pkg --noconfirm -Sg base base-devel
pacman --root $MOUNTED_INSTALL -Qq > $TEMP_FILE
for PKG in $(cat $TEMP_FILE) ; do
   pacman --root $MOUNTED_INSTALL --cachedir $MOUNTED_INSTALL/var/cache/pacman/pkg --noconfirm -S $PKG
done

exit 0

```

重启到你的64位系统后，运行这个命令去找到那些你仍保有的32位二进制文件，并且重装它们：

```
find /usr/bin -type f -exec bash -c 'file {} | grep 32-bit' \;

```

## 方法 2: 从正在运行的系统

确认你的系统是更新到最新的并且在下一步之前运行良好。

```
# pacman -Syu

```

### 准备软件包

#### 缓存旧软件包

**Note:** 如果你有任何来自没有新架构支持的[AUR](/index.php/AUR "AUR") 或第三方软件仓库的包， pacman将让你知道它不能找到合适的替代。列出这些软件以便升级后重装并运行`pacman -Rsn package_name`来清除它们。

如果缓存中没有你已安装的所有软件，下载它们(旧架构)为回退做准备。

```
 # pacman -Qqn | pacman -Sw -

```

或者用[pacman](https://www.archlinux.org/packages/?name=pacman)包里的bacman来生成它们。

如果你是从32位迁移，现在可以安装32位的Busybox：

```
# pacman -S busybox

```

#### 改变 Pacman 架构

编辑 */etc/pacman.conf* 文件 并将 *Architecture* 从 `auto` 更改到新值。可以使用这些 *sed* 命令:

对于 x86_64:

```
# sed -i  '/^Architecture =/s/auto/x86_64/' /etc/pacman.conf

```

对于 i686:

```
# sed -i  '/^Architecture =/s/auto/i686/' /etc/pacman.conf

```

确定*/etc/pacman.conf*和*/etc/pacman.d/mirrorlist*中的server列表使用*$arch*来代替显式指定i686或x86_64。现在强制pacman同步新的仓库：

```
# pacman -Syy

```

#### 下载新的软件包

下载所有已安装软件对应的新架构的包：

```
 # pacman -Sw $(pacman -Qqn|sed '/^lib32-/ d')  # download new package versions

```

既然已经配置好了32位的pacman，如果迁移到32位系统就现在安装Busybox：

```
# pacman -S busybox

```

**警告:** 不要现在安装 *lib32-glibc* 软件包。在执行命令 *ldconfig* 后，当你安装 *linux*（内核）时，生成的镜像文件中，*librt.so* 等库文件会在 */usr/lib32* 目录下，启动的时候二进制文件不会在此搜索库文件，导致启动失败。

### 软件包安装

#### 安装64位内核

将内核升级到64位既安全又直接：32位和64位应用可以同时很好地运行在64位内核上。对于从64位迁移，现在保留64位内核并跳过此步

安装标准Arch Linux内核，使用如下命令：

```
# pacman -S linux

```

现在该安装 *lib32-glibc* 软件包了（你需要添加[multilib]软件仓库，如果你还没有：

```
# pacman -S lib32-glibc

```

**Note:** 如果由于已存在不同名的软件包导致失败，使用-f选项强制安装。

重启后验证一下正在运行64位的内核：

 `$ uname -m`  `x86_64` 

#### 控制台终端

是时间转移到文本模式的虚拟控制台(e.g. Ctrl+Alt+F1) 来完成剩下的过程了。像ssh的伪终端也许可以工作但并不提倡. 在升级过程中有几个包的移除和取代可能造成X11桌面变得不稳定并让你的系统无法启动。

#### 安装 Pacman

**Warning:** 一旦你开始升级Pacman和它的依赖软件，过程将不能中断，它们必须在一个单独命令行同时安装。

使用 pactree 来安装Pacman和它的所有依赖:

```
# pactree -l pacman | pacman -S -

```

可能会返回错误，但只要pacman在工作就没事。这条命令之后立即只有busybox，bash和pacman可以被执行，直到其它包被迁移。你一定不要在下面这些命令完成之前重启。已经警告过你了。

#### 安装剩余的软件包

安装先前为新架构下载的软件包 (用同学电脑打一局dota或看个电影再回来：）)

```
# pacman -Qqn | pacman -S -

```

如果有的包没有被正确安装，你现在应该能成功地安装它们了;如果你很懒，你可以仅仅重复运行最后一条命令来安装所有东西。

对于从64位迁移，你可能想跳过32位内核安装，因为先前的64位内核仍能运行32位程序。

这一部之后任何迁移步骤都应该大功告成了，可以安全地重启计算机了。

## 清理

现在可以随意移除Busybox 和*lib32-glibc*.

```
# pacman -Rcn busybox lib32-glibc

```

#### Makepkg 编译器标志

在升级过程中新版本的 `/etc/makepkg.conf` 应被自动保存为 `/etc/makepkg.conf.pacnew`. 你不得不自己替代旧版本或更改它，如果你将来想用 [makepkg](/index.php/Makepkg "Makepkg") 编译任何东西。

```
# mv /etc/makepkg.conf /etc/makepkg.conf.backup && mv /etc/makepkg.conf.pacnew /etc/makepkg.conf

```

得到有关新添加到`/etc`的列表也许是个好注意。你可以通过以下命令获得:

```
# find /etc/ -type f -name \*.pac\*

```

## 疑难解答

升级过程中, 当 glibc 被新架构版本取代时, 旧架构的任何程序都将不能运行 如果发生问题，你可以通过[busybox](https://www.archlinux.org/packages/?name=busybox) 和[lib32-glibc](https://www.archlinux.org/packages/?name=lib32-glibc)解决。

### Busybox

在Arch中, Busybox是静态链接的; 它不需要库运行。有很多能用的命令。例如从缓存中提取i686版本的pacman：

```
# busybox tar xf /var/cache/pacman/pkg/pacman-3.3.2-1-i686.pkg.tar.gz -C <some folder>

```

### Lib32-glibc

例如运行32位的`/bin/ls`:

```
# /lib/ld-linux.so.2 /bin/ls

```

### KDE不能正确启动

当从32位迁移到64位时KDE将会发生冲突。（edit：从splash退回到kdm） 这是由于残存在 /var/tmp 中的32位KDE包，使用下列命令清楚kde缓存来修正这个问题：

```
# rm -rf /var/tmp/kdecache-*

```

### Mutt 开启 cache 后出问题

如果完成后发现 mutt 在打开邮件目录时死掉，重命名 cache 目录试试。如果可以解决问题，原来的 cache 可以删除。

## 参阅

*   [Migrate installation to new hardware](/index.php/Migrate_installation_to_new_hardware "Migrate installation to new hardware")