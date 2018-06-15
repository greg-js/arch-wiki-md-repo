Related articles

*   [ACPI modules](/index.php/ACPI_modules "ACPI modules")
*   [acpid](/index.php/Acpid "Acpid")

DSDT(Differentiated System Description Table)是[ACPI](https://en.wikipedia.org/wiki/Advanced_Configuration_and_Power_Interface "wikipedia:Advanced Configuration and Power Interface")规格的一部分。它提供了关于一个给定系统中受支持的电源事项的信息。ACPI表是由制造商提供在固件里的。通常，Linux遇到的问题是确实某些ACPI功能，比如风扇不转，盖子合上时屏幕不熄灭等等。这些问题可以归咎于DSDT是为Windows所特制的。安装后可以打补丁来修复这种情况。这篇文章的目标是分析并且重建一个有错误的DSDT，这样内核就会略过默认的DSDT。

基本上来说，一个DSDT表是运行在ACPI(电源管理)上的代码。

**Note:** [Linux ACPI](https://01.org/linux-acpi)项目的目标是Linux应该可以工作在未修改的固件上。如果你仍然觉得这种方法在现代内核上是必要的，那么你应该考虑一下[报告bug](/index.php/Reporting_bug_guidelines "Reporting bug guidelines")。

## Contents

*   [1 在你开始之前](#.E5.9C.A8.E4.BD.A0.E5.BC.80.E5.A7.8B.E4.B9.8B.E5.89.8D)
    *   [1.1 让内核报告一个Windows版本](#.E8.AE.A9.E5.86.85.E6.A0.B8.E6.8A.A5.E5.91.8A.E4.B8.80.E4.B8.AAWindows.E7.89.88.E6.9C.AC)
    *   [1.2 找一个已被修复的DSDT](#.E6.89.BE.E4.B8.80.E4.B8.AA.E5.B7.B2.E8.A2.AB.E4.BF.AE.E5.A4.8D.E7.9A.84DSDT)
*   [2 自己重新编译](#.E8.87.AA.E5.B7.B1.E9.87.8D.E6.96.B0.E7.BC.96.E8.AF.91)
*   [3 Using modified code](#Using_modified_code)
    *   [3.1 Using a CPIO archive](#Using_a_CPIO_archive)
    *   [3.2 Compiling into the kernel](#Compiling_into_the_kernel)
*   [4 Verify successful override](#Verify_successful_override)
*   [5 See also](#See_also)

## 在你开始之前

*   很有可能硬件制造商已经发布了一个修复了ACPI相关问题的固件更新。安装一个升级后的固件通常是一个比这个方法更好的选择，因为这会避免重复的工作。
*   这个过程会篡改你系统上一些相当基础的代码。你要对你要做出的改动相当确信。你可能还会想在行动之前先[备份你的硬盘](/index.php/Disk_cloning "Disk cloning")。
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

像你一样使用同一种笔记本的Arch用户是少数中的少数中的少数。尝试浏览其他发行版的论坛来讨论相同的型号。很有可能他们也有相同的问题，并且很有可能或是因为用户多或是因为他们精通技术，或许有人已经给出了预编译的版本(再强调一次，要自己承担风险)。 搜索引擎是你最好的工具。尽量让搜索的内容保持简短：‘型号 + dsdt’很有可能会搜到结果。

## 自己重新编译

在这个过程中你的最好的资源将会是[ACPI Spec homepage](http://www.acpi.info)，和[Linux ACPI Project](https://01.org/linux-acpi)，这些将会替代*acpi.sourceforge.net*。 简而言之，你可以使用英特尔的ASL编译器将你系统的DSDT表转换成源代码，定位并修复错误，最后重新编译。

你将会需要安装[iasl](https://www.archlinux.org/packages/?name=iasl)来修改代码。 **什么编译器编译了原始代码？** 查看你系统的DSDT使用英特尔的还是微软的编译器编译的：

 ` $ dmesg|grep DSDT ` 
```
ACPI: DSDT 00000000bf7e5000 0A35F (v02 Intel  CALPELLA 06040000 INTL 20060912)
ACPI: EC: Look up EC in DSDT

```

如果是微软的编译器，缩写INTL将会替代MSFT。 在这个例子中，在反编译/编译的DSDT时有五个错误。有两个在谷歌一下和研究ACPI规范后分容易解决。Three of them were due to different versions of compiler used and are, as later discovered, handled by the ACPICA at boot-time. The ACPICA component of the kernel can handle most of the trivial errors you get while compiling the DSDT. So do not fret yourself over compile errors if your system is *working the way it should*.

1.) Extract ACPI tables (as root): `# cat /sys/firmware/acpi/tables/DSDT > dsdt.dat`

2.) Decompile: `iasl -d dsdt.dat`

3.) Recompile: `iasl -tc dsdt.dsl`

4.) Examine errors and fix. e.g.:
```
dsdt.dsl   6727:                         Name (_PLD, Buffer (0x10)  
Error    4105 -          Invalid object type for reserved name ^  (found BUFFER, requires Package) 
```
 ` nano +6727 dsdt.dsl`  `(_PLD, Package(1) {Buffer (0x10)...` 

5.) Increase OEM version or otherwise the kernel will not apply the modified ACPI table. For example, before modification:

 `DefinitionBlock ("DSDT.aml", "DSDT", 2, "INTEL ", "TEMPLATE", 0x00000000)` 

After modification:

 `DefinitionBlock ("DSDT.aml", "DSDT", 2, "INTEL ", "TEMPLATE", 0x00000001)` 

6.) Compile fixed code: `iasl -tc dsdt.dsl` (Might want to try option -ic for C include file to insert into kernel source)

If it says no errors and no warnings you should be good to go.

## Using modified code

**Warning:** After each BIOS update you will need to fix DSDT again and repeat these steps!

There are at least two ways to use a custom DSDT:

*   creating a CPIO archive that is loaded by the bootloader
*   compiling it into the kernel

### Using a CPIO archive

This method has the advantage that you do not need to recompile your kernel, and updating the kernel will not make it necessary to repeat these steps.

This method requires the `ACPI_TABLE_UPGRADE=y` kernel config to be enabled (true for the [linux](https://www.archlinux.org/packages/?name=linux) package). See [[1]](https://www.kernel.org/doc/Documentation/acpi/initrd_table_override.txt) for details.

First, create the following folder structure:

```
$ mkdir -p kernel/firmware/acpi

```

Copy the fixed ACPI tables into the just created `kernel/firmware/acpi` folder, for example:

```
$ cp dsdt.aml ssdt1.aml kernel/firmware/acpi

```

Within the same folder where the newly created `kernel/` folder resides, run:

```
$ find kernel | cpio -H newc --create > acpi_override

```

This creates the CPIO archive containing the fixed ACPI tables. Copy the archive to the `boot` directory.

```
# cp acpi_override /boot

```

Lastly, configure the [bootloader](/index.php/Bootloader "Bootloader") to load your CPIO archive. For example, using [Systemd-boot](/index.php/Systemd-boot "Systemd-boot"), `/boot/loader/entries/arch.conf` might look like this:

```
title	 Arch Linux
linux	 /vmlinuz-linux
initrd   /acpi_override
initrd	 /initramfs-linux.img
options  root=PARTUUID=ec9d5998-a9db-4bd8-8ea0-35a45df04701 resume=PARTUUID=58d0aa86-d39b-4fe1-81cf-45e7add275a0 ...

```

Now all that is left to do is to reboot and to [verify the result.](#Verify_successful_override)

### Compiling into the kernel

You'll want to be familiar with [compiling your own kernel](/index.php/Kernels "Kernels"). The most straightforward way is with the "traditional" approach. After compiling DSDT, iasl produce two files: `dsdt.hex` and `dsdt.aml`.

**Using `menuconfig`:**

*   Disable "Select only drivers that don't need compile-time external firmware". Located in "Device Drivers -> Generic Driver Options".
*   Enable "Include Custom DSDT" and specify the absolute path of your fixed DSDT file (`dsdt.hex`, not `dsdt.aml`). Located in "Power management and ACPI options -> ACPI (Advanced Configuration and Power Interface) Support".

## Verify successful override

1.  Run `dmesg | grep ACPI`.
2.  Look for clues that suggest an override, for example:

```
[    0.000000] ACPI: Override [DSDT-   A M I], this is unsafe: tainting kernel
[    0.000000] ACPI: DSDT 00000000be9b1190 Logical table override, new table: ffffffff81865af0
[    0.000000] ACPI: DSDT ffffffff81865af0 0BBA3 (v02 ALASKA    A M I 000000F3 INTL 20130517)

```

## See also

*   [Upgrading ACPI tables via initrd](https://www.kernel.org/doc/Documentation/acpi/initrd_table_override.txt)