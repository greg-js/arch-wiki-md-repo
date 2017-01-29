摘自 [Wikipedia](https://en.wikipedia.org/wiki/Optical_disc_drive "wikipedia:Optical disc drive"):

	In computing, an optical disc drive (ODD) is a disk drive that uses laser light or electromagnetic waves within or near the visible light spectrum as part of the process of reading or writing data to or from optical discs. Some drives can only read from discs, but recent drives are commonly both readers and recorders, also called burners or writers. Compact discs, DVDs, and Blu-ray discs are common types of optical media which can be read and recorded by such drives. Optical drive is the generic name; drives are usually described as "CD" "DVD", or "Blu-ray", followed by "drive", "writer", etc.

本文描述了一些光盘刻录的技巧。

## Contents

*   [1 命令行的光盘刻录工具](#.E5.91.BD.E4.BB.A4.E8.A1.8C.E7.9A.84.E5.85.89.E7.9B.98.E5.88.BB.E5.BD.95.E5.B7.A5.E5.85.B7)
    *   [1.1 安装光盘刻录工具集](#.E5.AE.89.E8.A3.85.E5.85.89.E7.9B.98.E5.88.BB.E5.BD.95.E5.B7.A5.E5.85.B7.E9.9B.86)
    *   [1.2 设置权限](#.E8.AE.BE.E7.BD.AE.E6.9D.83.E9.99.90)
    *   [1.3 修改CD-RW中的内容](#.E4.BF.AE.E6.94.B9CD-RW.E4.B8.AD.E7.9A.84.E5.86.85.E5.AE.B9)
    *   [1.4 擦除CD-RW中的内容](#.E6.93.A6.E9.99.A4CD-RW.E4.B8.AD.E7.9A.84.E5.86.85.E5.AE.B9)
    *   [1.5 刻录一个iso镜像](#.E5.88.BB.E5.BD.95.E4.B8.80.E4.B8.AAiso.E9.95.9C.E5.83.8F)
    *   [1.6 刻录bin/cue](#.E5.88.BB.E5.BD.95bin.2Fcue)
    *   [1.7 从光盘生成一个iso镜像](#.E4.BB.8E.E5.85.89.E7.9B.98.E7.94.9F.E6.88.90.E4.B8.80.E4.B8.AAiso.E9.95.9C.E5.83.8F)
    *   [1.8 从硬盘上的文件生成一个iso镜像](#.E4.BB.8E.E7.A1.AC.E7.9B.98.E4.B8.8A.E7.9A.84.E6.96.87.E4.BB.B6.E7.94.9F.E6.88.90.E4.B8.80.E4.B8.AAiso.E9.95.9C.E5.83.8F)
    *   [1.9 挂载iso镜像](#.E6.8C.82.E8.BD.BDiso.E9.95.9C.E5.83.8F)
    *   [1.10 转换成iso镜像](#.E8.BD.AC.E6.8D.A2.E6.88.90iso.E9.95.9C.E5.83.8F)
*   [2 图形界面的光盘刻录软件](#.E5.9B.BE.E5.BD.A2.E7.95.8C.E9.9D.A2.E7.9A.84.E5.85.89.E7.9B.98.E5.88.BB.E5.BD.95.E8.BD.AF.E4.BB.B6)
    *   [2.1 Nero Linux版](#Nero_Linux.E7.89.88)
    *   [2.2 K3B](#K3B)
        *   [2.2.1 K3B 报告没有光盘刻录设备](#K3B_.E6.8A.A5.E5.91.8A.E6.B2.A1.E6.9C.89.E5.85.89.E7.9B.98.E5.88.BB.E5.BD.95.E8.AE.BE.E5.A4.87)
    *   [2.3 Gnomebaker](#Gnomebaker)
    *   [2.4 Brasero](#Brasero)
    *   [2.5 Graveman](#Graveman)
    *   [2.6 Bashburn](#Bashburn)
*   [3 故障处理方法](#.E6.95.85.E9.9A.9C.E5.A4.84.E7.90.86.E6.96.B9.E6.B3.95)
    *   [3.1 本地化](#.E6.9C.AC.E5.9C.B0.E5.8C.96)

## 命令行的光盘刻录工具

### 安装光盘刻录工具集

```
# pacman -S cdrkit

```

如果你希望使用<tt>cdrdao</tt> (把文件cue/bin写到光盘上)

```
# pacman -S cdrdao

```

### 设置权限

如果希望使用cd/dvd烧录设备的话必须要有它们的访问权限。如果要使用[udev](/index.php/Udev "Udev")（Archlinux内核的默认值），你只需要把这个（或多个）用户加入到optical组中：

```
# gpasswd -a <username> optical

```

然后别忘了注销后再登录一次。

### 修改CD-RW中的内容

本节假设你的刻录设备是/dev/cdrw。如果你不是这种情况，那么请对命令做相应的修改。为了能在光盘中写入内容必须先卸载。如果没有卸载，`wodim`会给出错误提示。

### 擦除CD-RW中的内容

CD-RW往往需要先擦除已经存在的内容然后再写入新的数据。使用以下命令来清空cd-rw中的内容：

```
wodim -v dev=/dev/cdrw -blank=fast

```

正如你可能猜想的，这个命令可以很快的清空光盘，但是你还可以使用一些其它的选项，只需把*fast*替换为下面的即可：

	all 

	清空整个光盘

	disc 

	清空整个光盘

	disk

	清空整个光盘

	fast

	最低限度的清空整个光盘(PMA，TOC，pregap)

	minimal

	最低限度的清空整个光盘(PMA，TOC，pregap)

	track

	清空一个磁道

	unreserve

	unreserve a track

	trtail

	blank a track tail

	unclose

	unclose last session

	session

	blank last session

### 刻录一个iso镜像

要刻录一个iso镜像，运行：

```
wodim -v dev=/dev/cdrw isoimage.iso

```

### 刻录bin/cue

要刻录bin/cue，运行：

```
cdrdao write --device /dev/cdrw image.cue

```

### 从光盘生成一个iso镜像

要复制一个光盘只需键入：

```
dd if=/dev/cdrw of=/home/user/isoimage.iso

```

或者使用更简单的输入：

```
cat /dev/cdrw > isoimage.iso

```

或者使用程序readcd（同样在cdrkit包中）

```
readcd -v dev=/dev/cdrw -f isoimage.iso

```

如果原光盘是能够启动电脑的，那么生成的镜像也是能够启动电脑的。

### 从硬盘上的文件生成一个iso镜像

要生成iso镜像只需要拷贝需要的文件到一个文件夹，然后输入：

```
mkisofs -V volume_name -J -r -o isoimage.iso ~/folder

```

### 挂载iso镜像

要测试iso镜像是否是正确的，你先要挂载它（用root身份）：

```
mount -t iso9660 -o ro,loop=/dev/loop0 cd_image /cdrom

```

你首先需要装入loop模块：

```
modprobe loop

```

### 转换成iso镜像

为了转换一个 .img / ccd 镜像，你需要使用ccd2iso：

```
pacman -S ccd2iso

ccd2iso /home/archman/image.img /home/archman/image.iso

```

## 图形界面的光盘刻录软件

在图形环境中有一些软件可以用于光盘刻录。这些软件的使用方法都是很直观的。

### Nero Linux版

它和Windows上面的Nero一样，[官方连接](http://www.nero.com/eng/NeroLINUX.html)|[AUR包](https://aur.archlinux.org/packages.php?do_Details=1&ID=2153)

它不是免费的，而且界面也没有windows版本的好。3.0.0 beta版还不能正确的制作可启动电脑的文件光盘。

如果你恰好有一个不被dvd+rw工具集支持的刻录光驱（也包括k3b和其它所有免费的图形界面工具），那么nero也许就是你唯一的选择。

### K3B

根据[http://www.k3b.org](http://www.k3b.org)，k3b是为KDE优化的CD/DVD制作工具（“CD/DVD Kreator for Linux”）。K3B使用 [QT](https://en.wikipedia.org/wiki/Qt_(toolkit) 工具集。

*   使用pacman来安装k3b

```
# pacman -S k3b

```

*   在root下，运行`k3bsetup`，
*   现在你可以设置你的权限等。
*   运行`k3b`来执行主程序。

#### K3B 报告没有光盘刻录设备

一个常见的原因是因为用户没有访问刻录设备的权限。 你可以尝试：

*   添加用户到`optical`组 （记住添加后要重新登录使之生效）

```
gpasswd -a <user> optical

```

*   设置访问权限

```
chmod 777 /dev/dvd*
chmod 777 /dev/cd*

```

其它原因，步骤，请参考当前指南 (;

### Gnomebaker

Gnomebaker是一个[GNOME](/index.php/GNOME "GNOME")桌面环境下的光盘刻录解决方案。 **如其作者所述，Gnomebaker不再开发维护了。考虑改用 [Brasero](#Brasero) 。**

*   使用pacman来安装gnomebaker

```
# pacman -S gnomebaker

```

*   运行 `gnomebaker` 以执行主程序

### Brasero

Brasero是[GNOME](/index.php/GNOME "GNOME")桌面环境下的另一个光盘刻录软件。

*   使用pacman来安装brasero

```
# pacman -S brasero

```

*   运行 `brasero` 来执行主程序

### Graveman

Graveman 是一个简单并且几乎完全独立的光盘刻录软件。

*   通过 pacman 安装 graveman 。

```
# pacman -S graveman

```

*   As root, run graveman, go to menu File > Preferences... > Devices and add your CD burners.
*   Note that you may have to manually add your own device in Graveman's preferences and point it at /dev/cdrom instead of /dev/hdc
*   Run `graveman` to run the main program.

### Bashburn

Alternatively theres also [Bashburn](http://bashburn.sourceforge.net/) in [AUR](https://aur.archlinux.org/packages.php?do_Details=1&ID=3658&O=0&L=0&C=0&K=bashburn&SB=n&SO=a&PP=25&do_MyPackages=0&do_Orphans=0&SeB=nd) as a semi-gui solution. BashBurn is the new name for the cd burning shell script Magma. It's not the best looking CD-burning application out there, but it does what you want it to do.

## 故障处理方法

#### 本地化

当运行K3B时，如果出现下面的提示信息：

```
System locale charset is ANSI_X3.4-1968
Your system's locale charset (i.e. the charset used to encode filenames) is 
set to ANSI_X3.4-1968\. It is highly unlikely that this has been done intentionally.
Most likely the locale is not set at all. An invalid setting will result in
problems when creating data projects.Solution: To properly set the locale 
charset make sure the LC_* environment variables are set. Normally the distribution 
setup tools take care of this.

```

就意味着你的本地化设置不正确。

通过下面的步骤来改正：

*   删除 `/etc/locale.gen`

```
# rm /etc/locale.gen

```

*   重新安装 `glibc`

```
# pacman -S glibc

```

*   修改 `/etc/locale.gen`, 为了兼容，取消注释`en_US`和所有与你的语言相关的行

```
# nano /etc/locale.gen

en_US.UTF-8 UTF-8
en_US ISO-8859-1

```

*   使用`locale-gen`来重新生成档案

```
# locale-gen

Generating locales...
en_US.UTF-8... done
en_US.ISO-8859-1... done
pt_BR.UTF-8... done
pt_BR.ISO-8859-1... done
Generation complete.

```

更多的信息请参考 [这里](https://bbs.archlinux.org/viewtopic.php?pid=251512%29;)