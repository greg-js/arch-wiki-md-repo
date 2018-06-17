Related articles

*   [ACPI modules](/index.php/ACPI_modules "ACPI modules")
*   [acpid](/index.php/Acpid "Acpid")

DSDT(Differentiated System Description Table)是[ACPI](https://en.wikipedia.org/wiki/Advanced_Configuration_and_Power_Interface "wikipedia:Advanced Configuration and Power Interface")规格的一部分。它提供了关于一个给定系统中受支持的电源事件的信息。ACPI表是由制造商在固件里提供的。通常，Linux遇到的问题是某些ACPI功能的缺失，比如风扇不转，盖子合上时屏幕不熄灭等等。这些问题可以归咎于DSDT是为Windows所定制的。安装后可以打补丁来修复这些问题。这篇文章的目标是分析并且重建一个有错误的DSDT，这样内核就会略过默认的DSDT。

基本上来说，一个DSDT表是运行在ACPI(电源管理)上的代码。

**Note:** [Linux ACPI](https://01.org/linux-acpi)项目的目标让Linux工作在未修改的固件上。如果你还是觉得这种方法在现代内核上是必要的，那么你应该考虑一下[报告bug](/index.php/Reporting_bug_guidelines "Reporting bug guidelines")。

## Contents

*   [1 在你开始之前](#.E5.9C.A8.E4.BD.A0.E5.BC.80.E5.A7.8B.E4.B9.8B.E5.89.8D)
    *   [1.1 让内核报告一个Windows版本](#.E8.AE.A9.E5.86.85.E6.A0.B8.E6.8A.A5.E5.91.8A.E4.B8.80.E4.B8.AAWindows.E7.89.88.E6.9C.AC)
    *   [1.2 找一个已被修复的DSDT](#.E6.89.BE.E4.B8.80.E4.B8.AA.E5.B7.B2.E8.A2.AB.E4.BF.AE.E5.A4.8D.E7.9A.84DSDT)
*   [2 自己重新编译](#.E8.87.AA.E5.B7.B1.E9.87.8D.E6.96.B0.E7.BC.96.E8.AF.91)
*   [3 使用修改过的代码](#.E4.BD.BF.E7.94.A8.E4.BF.AE.E6.94.B9.E8.BF.87.E7.9A.84.E4.BB.A3.E7.A0.81)
    *   [3.1 使用一个CPIO文档](#.E4.BD.BF.E7.94.A8.E4.B8.80.E4.B8.AACPIO.E6.96.87.E6.A1.A3)
    *   [3.2 编译进内核](#.E7.BC.96.E8.AF.91.E8.BF.9B.E5.86.85.E6.A0.B8)
*   [4 确认覆盖成功](#.E7.A1.AE.E8.AE.A4.E8.A6.86.E7.9B.96.E6.88.90.E5.8A.9F)
*   [5 参见](#.E5.8F.82.E8.A7.81)

## 在你开始之前

*   很有可能硬件制造商已经发布了一个固件更新，修复了ACPI相关问题。安装一个升级后的固件通常是一个更好的选择，因为这会避免重复的工作。
*   这个过程会篡改你系统上一些相当基础的代码。你要对你将做出的改动相当清楚。你可能还会想在行动之前先[备份你的硬盘](/index.php/Disk_cloning "Disk cloning")。
*   即使在你尝试你自行修复你的DSDT之前，你也可以尝试一些不同的捷径：

### 让内核报告一个Windows版本

使用变量**acpi_os_name**作为一个内核参数。例如：

```
 acpi_os_name="Microsoft Windows NT"

```

或者

```
 acpi_osi="!Windows2012"

```

添加在grub配置文件中的kernel一行。

其他用来测试的字符串：

*   "Microsoft Windows XP"
*   "Microsoft Windows 2000"
*   "Microsoft Windows 2000.1"
*   "Microsoft Windows ME: Millennium Edition"
*   "Windows 2001"
*   "Windows 2006"
*   "Windows 2009"
*   "Windows 2012"
*   当这些都失败时，你可以尝试"Linux"

出于好奇，你可以执行下面的步骤来提取你的DSDT并找到.dsl文件。你只需grep Windows然后看看出现了什么。

### 找一个已被修复的DSDT

一个DSDT文件最初是用ACPI源语言(.asl/.dsl文件)写的。借助一个编译器，这样的文件可以被编译成一个“ACPI机器语言”文件(.aml)或者一个十六进制表(.hex)。为了将这个文件包含在你的Arch里，你将需要找到一个编译过的.aml文件——这到底意味这自己编译它还是相信网上的一个陌生人是由你自己决定的。如果你从网上下载一个文件，它很有可能是一个压缩的.asl文件。I所以你将会需要解压并编译它。这样做的好处就是你将不用自己研究具体的修复代码。

像你一样使用同一种笔记本的Arch用户是少数中的少数中的少数。尝试浏览其他发行版的论坛来寻找关于相同的型号的讨论。很有可能他们也有相同的问题。由于他们的用户可能比较多或是比较精通技术，有可能有人已经给出了预编译的版本(再强调一次，要自己承担风险)。 搜索引擎是你最好的工具。尽量让搜索的内容保持简短：‘型号 + dsdt’很有可能会搜到结果。

## 自己重新编译

在这个过程中你的最好的资源将会是[ACPI Spec homepage](http://www.acpi.info)，和[Linux ACPI Project](https://01.org/linux-acpi)，这些将会替代*acpi.sourceforge.net*。 简而言之，你可以使用英特尔的ASL编译器将你系统的DSDT表转换成源代码，定位并修复错误，最后重新编译。

你将会需要安装[iasl](https://www.archlinux.org/packages/?name=iasl)来修改代码。 **什么编译器编译了原始代码？** 查看你系统的DSDT使用英特尔的还是微软的编译器编译的：

 ` $ dmesg|grep DSDT ` 
```
ACPI: DSDT 00000000bf7e5000 0A35F (v02 Intel  CALPELLA 06040000 INTL 20060912)
ACPI: EC: Look up EC in DSDT

```

如果是微软的编译器，INTL将会变成MSFT。 在这个例子中，在反编译/编译的DSDT时共有五个错误，有两个在谷歌一下和研究ACPI规范之后很容易解决。另外三个是由于使用了不同版本的编译器。后来你会发现，它们三个会在启动时被ACPICA处理。内核的ACPICA部分可以处理编译DSDT时产生的的大部分不重要的错误.所以如果你的系统正在*按照正常方式运行*，请不要为了编译错误烦恼。

1.) 提取ACPI表(作为超级用户): `# cat /sys/firmware/acpi/tables/DSDT > dsdt.dat`

2.) 反编译: `iasl -d dsdt.dat`

3.) 重新编译: `iasl -tc dsdt.dsl`

4.) 检查错误并修复。例如:
```
dsdt.dsl   6727:                         Name (_PLD, Buffer (0x10)  
Error    4105 -          Invalid object type for reserved name ^  (found BUFFER, requires Package) 
```
 ` nano +6727 dsdt.dsl`  `(_PLD, Package(1) {Buffer (0x10)...` 

5.) 增添OEM版本，否则内核不会应用修改过的ACPI表。例如在修改前:

 `DefinitionBlock ("DSDT.aml", "DSDT", 2, "INTEL ", "TEMPLATE", 0x00000000)` 

修改后:

 `DefinitionBlock ("DSDT.aml", "DSDT", 2, "INTEL ", "TEMPLATE", 0x00000001)` 

6.) 编译被修复过的代码: `iasl -tc dsdt.dsl` (你可能需要命令行参数-ic来将C语言头文件插入内核)

如果没有错误，你应该可以接着往下进行了。

## 使用修改过的代码

**警告:** 每次BIOS更新后你都要重新修复DSDT表并且重复这些步骤！

至少有两种方式来使用定制的DSDT:

*   创建一个会被bootloader加载的CPIO文档
*   把它编译进内核

### 使用一个CPIO文档

这个方法有一个优点就是你不用重新编译你的内核，升级内核后你也无需重复这些步骤

这个方法要求内核参数`ACPI_TABLE_UPGRADE=y`被启用(对于[linux](https://www.archlinux.org/packages/?name=linux)被设置为true)。浏览[[1]](https://www.kernel.org/doc/Documentation/acpi/initrd_table_override.txt) 来查看更多详细内容。

首先，创建下面的目录结构:

```
$ mkdir -p kernel/firmware/acpi

```

将修复过的ACPI表拷贝进刚刚创建的`kernel/firmware/acpi`文件夹，例如:

```
$ cp dsdt.aml ssdt1.aml kernel/firmware/acpi

```

在新创建的`kernel/`目录所在的目录下，运行:

```
$ find kernel | cpio -H newc --create > acpi_override

```

这条命令会创建含有修复了的ACPI表的CPIO文档。将文档拷贝到`boot`目录。

```
# cp acpi_override /boot

```

最后，配置[bootloader](/index.php/Bootloader "Bootloader")来加载你的CPIO文档。例如，使用[Systemd-boot](/index.php/Systemd-boot "Systemd-boot")的话， `/boot/loader/entries/arch.conf`可能看起来像这样:

```
title	 Arch Linux
linux	 /vmlinuz-linux
initrd   /acpi_override
initrd	 /initramfs-linux.img
options  root=PARTUUID=ec9d5998-a9db-4bd8-8ea0-35a45df04701 resume=PARTUUID=58d0aa86-d39b-4fe1-81cf-45e7add275a0 ...

```

现在，剩下需要做的事情就是重启电脑并且[确认结果](#Verify_successful_override)。

### 编译进内核

你会想要熟悉[编译自己的内核](/index.php/Kernels "Kernels")。最直接的方式就是用“传统”方法。 编译DSDT之后，iasl产生两个文件:`dsdt.hex`和`dsdt.aml`。

**使用 `menuconfig`:**

*   禁用"Select only drivers that don't need compile-time external firmware"。位于"Device Drivers -> Generic Driver Options"。
*   启用"Include Custom DSDT"并且指明你修复过的DSDT文件的绝对路径(`dsdt.hex`，而不是`dsdt.aml`)。位于"Power management and ACPI options -> ACPI (Advanced Configuration and Power Interface) Support"。

## 确认覆盖成功

1.  运行`dmesg | grep ACPI`.
2.  查找表明已经覆盖的提示，例如:

```
[    0.000000] ACPI: Override [DSDT-   A M I], this is unsafe: tainting kernel
[    0.000000] ACPI: DSDT 00000000be9b1190 Logical table override, new table: ffffffff81865af0
[    0.000000] ACPI: DSDT ffffffff81865af0 0BBA3 (v02 ALASKA    A M I 000000F3 INTL 20130517)

```

## 参见

*   [Upgrading ACPI tables via initrd](https://www.kernel.org/doc/Documentation/acpi/initrd_table_override.txt)