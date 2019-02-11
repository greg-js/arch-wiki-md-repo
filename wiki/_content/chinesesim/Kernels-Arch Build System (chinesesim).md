**翻译状态：** 本文是英文页面 [Kernels/Arch Build System](/index.php/Kernels/Arch_Build_System "Kernels/Arch Build System") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2018-11-27，点击[这里](https://wiki.archlinux.org/index.php?title=Kernels%2FArch+Build+System&diff=0&oldid=545354)可以查看翻译后英文页面的改动。

参阅 [Kernels (简体中文)](/index.php/Kernels_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Kernels (简体中文)"). 利用 [Arch 编译系统](/index.php/Arch_Build_System_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch Build System (简体中文)")，可以基于官方的 [linux](https://www.archlinux.org/packages/?name=linux) 包编译自定义内核。这种编译方法可以自动化整个过程，并且是基于一个已经经过详细测试过的内核包。你可以编辑 PKGBUILD 来使用一个自定义内核配置或者添加附加的补丁。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 获取所需内容](#获取所需内容)
*   [2 修改 PKGBUILD](#修改_PKGBUILD)
    *   [2.1 修改 prepare()](#修改_prepare())
    *   [2.2 生成新校验和](#生成新校验和)
*   [3 编译](#编译)
*   [4 安装](#安装)
*   [5 启动加载器](#启动加载器)

## 获取所需内容

因为要使用到 [makepkg](/index.php/Makepkg "Makepkg"), 请先了解 makepkg 的使用方法和最佳实践建议。例如不要用 root/sudo 运行 makepkg.

首先建立一个编译目录 `build`：

```
 $ cd ~/
 $ mkdir build
 $ cd build/

```

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") 软件包 [asp](https://www.archlinux.org/packages/?name=asp) 和 [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/).

首先需要一个原始内核作为自定义的基础，从 ABS 获取内核包文件，并放到编译目录：

```
$ asp update linux
$ asp checkout linux

```

然后从相应的来源获取其他需要的文件 (例如自定义配置文件、补丁等)。

## 修改 PKGBUILD

编辑 `PKGBUILD`，找到 `pkgbase` 修改为自定义软件包的名称:

```
 pkgbase=linux-custom

```

根据 PKGBUILD，还需要修改 `linux.install` 的内容，与 `pkgbase` 相匹配。

### 修改 prepare()

可以在这里打上需要的补丁，并修改内核配置文件。

或用 GUI 调整编译选项。从 PKGBUILD 的 prepare() 函数中选择一种方式，取消前面的注释：

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

### 生成新校验和

[安装](/index.php/Install "Install") 软件包 [pacman-contrib](https://www.archlinux.org/packages/?name=pacman-contrib)。

如果修改了 config 文件，需要生成新的校验和：

```
$ updpkgsums

```

## 编译

现在可以用`makepkg`命令编译内核了，如果配置时选择了交互编译(例如 menuconfig)，编译时需要进行配置。

```
 $ makepkg -s

```

选项 `-s` 会在编译是下载需要的依赖关系，比如 xml 和 docs.

内核代码是 [PGP 签名](https://www.kernel.org/signature.html#kernel-org-web-of-trust), makepkg 会尝试进行校验，详情请参考 [Makepkg#Signature checking](/index.php/Makepkg#Signature_checking "Makepkg").

**Note:** [同时运行多个编译任务](/index.php/Makepkg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#MAKEFLAGS "Makepkg (简体中文)")可以在多核系统上显著减少编译时间。

## 安装

在 makepkg 后可以查看 linux.install 文件，你会看到一些变量已经改变。现在，你只需要通过 pacman(或其他程序)正常安装软件包了。最好先安装内核头文件，因为有些驱动例如 nvidia 在更新时需要这些头文件。

```
# pacman -U <kernel-headers_package>
# pacman -U <kernel_package>

```

## 启动加载器

现在已经创建了定制的内核和目录，例如 `/boot/vmlinuz-linux-test`。要测试内核，请更新[启动加载器](/index.php/Boot_loaders_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Boot loaders (简体中文)")配置，为定制内核添加新入口('default' 和 'fallback')。这样，就可以并行使用系统内核和定制内核。