**注意:** Arch Linux 已经用 [GRUB2](/index.php/GRUB2_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GRUB2 (简体中文)") 替代了 GRUB Legacy。参见[这里的](https://www.archlinux.org/news/grub-legacy-no-longer-supported/)通知。Grub2 也提供了背景图片支持。建议用户改用 [GRUB2](/index.php/GRUB2_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GRUB2 (简体中文)") 或 [Syslinux](/index.php/Syslinux "Syslinux")。

## Contents

*   [1 简介](#.E7.AE.80.E4.BB.8B)
*   [2 安装前言](#.E5.AE.89.E8.A3.85.E5.89.8D.E8.A8.80)
*   [3 安装](#.E5.AE.89.E8.A3.85)
*   [4 问题解决](#.E9.97.AE.E9.A2.98.E8.A7.A3.E5.86.B3)
    *   [4.1 黑屏有菜单](#.E9.BB.91.E5.B1.8F.E6.9C.89.E8.8F.9C.E5.8D.95)
    *   [4.2 黑屏无菜单或者未正确显示](#.E9.BB.91.E5.B1.8F.E6.97.A0.E8.8F.9C.E5.8D.95.E6.88.96.E8.80.85.E6.9C.AA.E6.AD.A3.E7.A1.AE.E6.98.BE.E7.A4.BA)
*   [5 常见问题解答](#.E5.B8.B8.E8.A7.81.E9.97.AE.E9.A2.98.E8.A7.A3.E7.AD.94)
    *   [5.1 我可以使用个性化的GRUB图像吗？](#.E6.88.91.E5.8F.AF.E4.BB.A5.E4.BD.BF.E7.94.A8.E4.B8.AA.E6.80.A7.E5.8C.96.E7.9A.84GRUB.E5.9B.BE.E5.83.8F.E5.90.97.EF.BC.9F)
    *   [5.2 修改闪屏需要重编译或者安装GRUB吗？](#.E4.BF.AE.E6.94.B9.E9.97.AA.E5.B1.8F.E9.9C.80.E8.A6.81.E9.87.8D.E7.BC.96.E8.AF.91.E6.88.96.E8.80.85.E5.AE.89.E8.A3.85GRUB.E5.90.97.EF.BC.9F)
    *   [5.3 什么地方可以获取更多的闪屏他图像？](#.E4.BB.80.E4.B9.88.E5.9C.B0.E6.96.B9.E5.8F.AF.E4.BB.A5.E8.8E.B7.E5.8F.96.E6.9B.B4.E5.A4.9A.E7.9A.84.E9.97.AA.E5.B1.8F.E4.BB.96.E5.9B.BE.E5.83.8F.EF.BC.9F)

## 简介

本程序是在当前Arch仓库中的GRUB包的基础上修改而来，添加了闪屏图像（作为背景图）支持。

这个补丁并非官方的GRUB团队维护和支持，并且仅适用于GRUB 0.9x系列。该补丁被很多发行版所采用，比如Fedora/红帽、SuSE、Gentoo、MEPIS以及其他的一些版本。我使用的这个补丁基于Fedora Core 3所提供的SRPM包修改而来，对应最新的vanilla [GRUB](/index.php/GRUB "GRUB")版本。

在安装完成后，你将会看到如下图所示的GRUB屏幕： [http://www.mundolink.net/users/mariov/images/arch-grub-096.png](http://www.mundolink.net/users/mariov/images/arch-grub-096.png)

为了满足特殊的需求，那些喜欢旧的闪屏图像的可以选择旧的。 [http://www.mundolink.net/users/mariov/images/arch-grub.png](http://www.mundolink.net/users/mariov/images/arch-grub.png)

**New:** In addition to the standard package, a new alternate one is available for those who follow the [Reiser4FShowto](/index.php/Reiser4FShowto "Reiser4FShowto") steps and want a GRUB package with both reiserfs4 and splashimage.

## 安装前言

Pre-Install Notes

1.  Make a copy of your `/boot/grub/menu.lst` for backup. It is not replaced by the installation steps below, unless you remove your current [grub](https://www.archlinux.org/packages/?name=grub) package.
2.  We are dealing with your boot system info, so there is a small chance that things can be screw up. But I have not had any issues.
3.  If want to compile the package with the old splash image, or your custom splash image instead of the current one, you need to edit the [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") and change the `md5sum` assigned to `splash.xpm.gz`.
4.  The alternate package with reiser4 requires **libaal**, **reiser4progs**, and a **reiser4 patched kernel**. Those are not on Arch repos, you can get them and read about all the process involved on [Reiser4FShowto](/index.php/Reiser4FShowto "Reiser4FShowto"), or grab my updated PKGBUILDs:[libaal](http://www.mundolink.net/users/mariov/arch/packages/libaal/PKGBUILD), and [reiser4progs](http://www.mundolink.net/users/mariov/arch/packages/reiser4progs/PKGBUILD).
5.  Be sure not to upgrade [grub](https://www.archlinux.org/packages/?name=grub) via [pacman](/index.php/Pacman "Pacman") after following this guide, as the version used in this guide is older than the current version available via pacman. You can set pacman to ignore any [grub](https://www.archlinux.org/packages/?name=grub) upgrades by editing your `pacman.conf` accordingly.

## 安装

1\. 下载并保存下列文件到 `/var/abs/local`目录下:

*   [PKGBUILD](https://cvs.archlinux.org/cgi-bin/viewcvs.cgi/*checkout*/system/grub-gfx/PKGBUILD?rev=HEAD&cvsroot=AUR&only_with_tag=CURRENT&content-type=text/plain).
*   [menu.lst](https://cvs.archlinux.org/cgi-bin/viewcvs.cgi/*checkout*/system/grub-gfx/menu.lst?rev=HEAD&cvsroot=AUR&only_with_tag=CURRENT&content-type=text/plain)
*   [install-grub](https://cvs.archlinux.org/cgi-bin/viewcvs.cgi/*checkout*/system/grub-gfx/install-grub?rev=HEAD&cvsroot=AUR&only_with_tag=CURRENT&content-type=text/plain) o copiarlo desde `/var/abs/base/grub/`install-grub
*   [grub-0.97-graphics.patch](https://cvs.archlinux.org/cgi-bin/viewcvs.cgi/system/grub-gfx/grub-0.97-graphics.patch?cvsroot=AUR&only_with_tag=CURRENT)
*   [splash.xpm.gz](https://cvs.archlinux.org/cgi-bin/viewcvs.cgi/*checkout*/system/grub-gfx/splash.xpm.gz?rev=HEAD&cvsroot=AUR&only_with_tag=CURRENT&content-type=image/x-xpixmap)* **Only for reiser4 support:** grab the [reiser4 patch](http://www.mundolink.net/users/mariov/arch/packages/grub/reiser4/grub-0.96-reiser4.patch)

2\. 编译构建包：

```
# makepkg  

```

3\. 安装包：

```
# pacman -U grub-0.97-1.pkg.tar.gz 

```

4\. 编辑`/boot/grub/menu.lst`在操作系统列表前任何地方添加下面的闪屏设置部分：

```
splashimage /boot/grub/splash.xpm.gz

```

比如说:

```
# general configuration:
timeout   5
default   0
splashimage /boot/grub/splash.xpm.gz

```

**重要提示:** 从grub 0.96-4起，闪屏图像位置改为 `/boot/grub/splash.xpm.gz`而不是`/grub/splash.xpm.gz`。老用户需要修改一下路径。

实际上，你应该把 `splashimage /path/to/your/image.xpm{.gz}` 和grub的根引导分区联系起来。
如果你有单独的`/boot`分区:
`splashimage /grub/splash.xpm.gz`
否则：
`splashimage /boot/grub/splash.xpm.gz`
错误的路径会导致grub黑屏挂起，并且没有任何提示和光标:-(

5\. 将新的 grub引导图像安装到 `/boot`目录。（将_x_改成你的驱动器编号 (比如`hda`):

```
# install-grub /dev/sd_x_

```

6\. **仅** 当你的系统需要双重启动**并且**主引导设备是**NTLDR**时 - 记住更新你的引导文件(`dd if=/dev/sdx of=/linux.bin bs=512 count=1`)然后复制到你的NTFS引导分区中，如果你不知道是不是，跳过即可。

## 问题解决

#### 黑屏有菜单

Stages 可能没有更新，重新运行`install-grub _(你的/boot分区或者MBR所在分区)_`。然后使用 [checksplash.sh](http://ruslug.rutgers.edu/~mcgrof/grub-images/checksplash.sh)脚本以检测你的stage2 是否支持闪屏图像.

#### 黑屏无菜单或者未正确显示

检查splashimage设置是否有误。如果你有单独的`/boot`分区，改成`splashimage /grub/splash.xpm.gz`试试看。同时也检查下`splash.xpm.gz`是否在grub目录下。

## 常见问题解答

### 我可以使用个性化的GRUB图像吗？

当然可以，不过图像要满足一下要求：分辨率640x480；色深14位；用gzip压缩成xpm格式。

### 修改闪屏需要重编译或者安装GRUB吗？

任何时间你都可以使用任意的闪屏图像，在首次安装后你不需要再次编译他，只需要用新的闪屏图像替换掉 `splash.xpm.gz` 即可，或者是编辑 `menu.lst` 修改闪屏路径就可以了

### 什么地方可以获取更多的闪屏他图像？

[GNU GRUB 闪屏图像制作指南](http://ruslug.rutgers.edu/~mcgrof/grub-images/) - General GRUB bootsplash info and sample images. [checksplash.sh](http://ruslug.rutgers.edu/~mcgrof/grub-images/checksplash.sh) - 检测你的stage2（内核镜像）是否支持闪屏图像。