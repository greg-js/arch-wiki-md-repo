**翻译状态：** 本文是英文页面 [Kernels/Arch_Build_System](/index.php/Kernels/Arch_Build_System "Kernels/Arch Build System") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-02-23，点击[这里](https://wiki.archlinux.org/index.php?title=Kernels/Arch_Build_System&diff=0&oldid=417795)可以查看翻译后英文页面的改动。

参阅 [Kernels (简体中文)](/index.php/Kernels_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Kernels (简体中文)"). 利用 [Arch 编译系统](/index.php/Arch_Build_System_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch Build System (简体中文)")，可以基于官方的 [linux](https://www.archlinux.org/packages/?name=linux) 包编译自定义内核。这种编译方法可以自动化整个过程，并且是基于一个已经经过详细测试过的内核包。你可以编辑 PKGBUILD 来使用一个自定义内核配置或者添加附加的补丁。

## Contents

*   [1 获取所需内容](#.E8.8E.B7.E5.8F.96.E6.89.80.E9.9C.80.E5.86.85.E5.AE.B9)
*   [2 修改 PKGBUILD](#.E4.BF.AE.E6.94.B9_PKGBUILD)
    *   [2.1 修改 build()](#.E4.BF.AE.E6.94.B9_build.28.29)
*   [3 编译](#.E7.BC.96.E8.AF.91)
*   [4 安装](#.E5.AE.89.E8.A3.85)
*   [5 启动加载器](#.E5.90.AF.E5.8A.A8.E5.8A.A0.E8.BD.BD.E5.99.A8)

## 获取所需内容

因为要使用到 [makepkg](/index.php/Makepkg "Makepkg"), 请先了解 makepkg 的使用方法和最佳实践建议。例如不要用 root/sudo 运行 makepkg.

首先建立一个编译目录 `build`：

```
 $ cd ~/
 $ mkdir build
 $ cd build/

```

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") 软件包 [abs](https://www.archlinux.org/packages/?name=abs) 和 [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/).

首先需要一个原始内核作为自定义的基础，从 ABS 获取内核包文件，并放到编译目录：

```
$ ABSROOT=. abs core/linux

```

如果防火墙屏蔽了 rsync 端口，可以用 -t 参数通过 tarball 下载:

```
$ ABSROOT=. abs core/linux -t

```

然后从相应的来源获取其他需要的文件 (例如自定义配置文件、补丁等)。

## 修改 PKGBUILD

编辑 `PKGBUILD`，找到 `pkgbase` 修改为自定义软件包的名称:

```
 pkgbase=linux-custom

```

根据 PKGBUILD，还需要修改 `linux.install` 的内容，与 `pkgbase` 相匹配(例如 [linux-grsec](https://www.archlinux.org/packages/?name=linux-grsec).

### 修改 build()

修改 config 文件，或用 GUI 调整编译选项。从 PKGBUILD 的 prepare() 函数中选择一种方式，取消前面的注释：

 `PKGBUILD` 
```
...
  # load configuration
  # Configure the kernel. Replace the line below with one of your choice.
  #make menuconfig # CLI menu for configuration
  make nconfig # new CLI menu for configuration
  #make xconfig # X-based configuration
  #make oldconfig # using old config from previous kernel version
  # ... or manually edit .config
...

```

如果已经有了`.config`内核配置文件，取消一个交互配置工具的注释，如 nconfig，然后装入自己的配置文件。

*   如果取消 build() 中的 'make menuconfig'，但是用 menuconfig gui 加载了已有的 config 文件，在最终软件包中会出现文件冲突。因为 PKGBUILD 设置了单独的安装路径，默认的 LOCALVERSION 和 LOCALVERSION_AUTO 配置选项会修改。要修正这个问题，在 menuconfg 中设置 LOCALVERSION 和 LOCALVERSION_AUTO，详情参考 [BBS#173504](https://bbs.archlinux.org/viewtopic.php?id=173504)。
*   如果取消 *return 1* 的注释，可以在 makepkg 完成解压后进入内核代码目录然后 make nconfig。这样可以在多个会话间配置内核。可以编译时，用 .config 文件覆盖 config 或 config.x86_64(根据相应的架构)，然后注释掉 *return 1* 并使用**makepkg -i**。

但是不要对自定义补丁使用这种方法，把你的补丁命令放在这行之后。如果你要手动补丁，bztar 解包然后替换你的补丁。

## 编译

**小贴士:** [同时运行多个编译任务](/index.php/Makepkg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#MAKEFLAGS "Makepkg (简体中文)")可以在多核系统上显著减少编译时间。

现在可以用命令编译内核了： `makepkg`

如果配置时选择了交互编译(例如 menuconfig)，编译时需要进行配置。

**注意:** 编译内核需要一些时间，一个小时也是正常的。

## 安装

在 makepkg 后可以查看 linux.install 文件，你会看到一些变量已经改变。现在，你只需要通过 pacman(或其他程序)正常安装软件包了：

```
# pacman -U <kernel_package>

```

## 启动加载器

现在已经创建了定制的内核和目录，例如 `/boot/vmlinuz-linux-test`。要测试内核，请更新启动加载器(GRUB 为 `/boot/grub/menu.lst` )，为定制内核添加新入口('default' 和 'fallback')。这样，就可以并行使用系统内核和定制内核。