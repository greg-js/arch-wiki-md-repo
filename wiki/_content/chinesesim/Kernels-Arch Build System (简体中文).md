**翻译状态：** 本文是英文页面 [Kernels/Arch_Build_System](/index.php/Kernels/Arch_Build_System "Kernels/Arch Build System") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2012-10-07，点击[这里](https://wiki.archlinux.org/index.php?title=Kernels/Arch_Build_System&diff=0&oldid=226152)可以查看翻译后英文页面的改动。

[Arch Build System](/index.php/Arch_Build_System_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch Build System (简体中文)") 可以用来在官方的 [linux](https://www.archlinux.org/packages/?name=linux) 包基础上编译一个自定义内核。这种编译方法可以自动化整个过程，并且是基于一个已经经过详细测试过的内核包。你可以编辑 PKGBUILD 来使用一个自定义内核配置或者添加附加的补丁。

## Contents

*   [1 获取所需内容](#.E8.8E.B7.E5.8F.96.E6.89.80.E9.9C.80.E5.86.85.E5.AE.B9)
*   [2 修改 PKGBUILD](#.E4.BF.AE.E6.94.B9_PKGBUILD)
    *   [2.1 修改 build()](#.E4.BF.AE.E6.94.B9_build.28.29)
*   [3 编译](#.E7.BC.96.E8.AF.91)
*   [4 安装](#.E5.AE.89.E8.A3.85)
*   [5 启动加载器](#.E5.90.AF.E5.8A.A8.E5.8A.A0.E8.BD.BD.E5.99.A8)

## 获取所需内容

```
# pacman -S abs base-devel

```

首先，需要一个干净的内核作为开始。从 ABS 获取内核包：

 `$ ABSROOT=. abs core/linux` 

然后从相应的来源获取其他需要的文件 (例如自定义配置文件、补丁等)。

## 修改 PKGBUILD

修改`pkgbase`为自定义软件包的名称，例如:

```
 pkgbase=linux-custom

```

如果不需要重新编译 linux-headers 和 -docs，请从`pkgname`中删除:

```
 pkgname=("${pkgbase}")

```

### 修改 build()

可能需要内核的自定义 .config 文件，只需在 PKGBUILD 文件的 build() 函数中取消相应行的注释。例如：

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

如果已经有了内核配置文件，我建议取消注释一个交互配置工具如 nconfig，然后装入自己的配置文件。这样可以避免我遇到过的其他方法中的内核命名问题。

**注意:** 如果取消 _return 1_ 的注释，可以在 makepkg 完成解压后进入内核代码目录然后 make nconfig。这样可以在多个会话间配置内核。可以编译时，用 .config 文件覆盖 config 或 config.x86_64(根据相应的架构)，然后注释掉 _return 1_ 并使用**makepkg -i**。 但是不要对自定义补丁使用这种方法，把你的补丁命令放在这行之后。如果你要手动补丁，bztar 解包然后替换你的补丁。

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