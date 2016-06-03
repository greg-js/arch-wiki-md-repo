**翻译状态：** 本文是英文页面 [Mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-05-14，点击[这里](https://wiki.archlinux.org/index.php?title=Mkinitcpio&diff=0&oldid=434079)可以查看翻译后英文页面的改动。

**mkinitcpio**是新一代[initramfs](https://en.wikipedia.org/wiki/initrd "wikipedia:initrd")创建工具。

## Contents

*   [1 概览](#.E6.A6.82.E8.A7.88)
*   [2 安装](#.E5.AE.89.E8.A3.85)
*   [3 创建和启用镜像](#.E5.88.9B.E5.BB.BA.E5.92.8C.E5.90.AF.E7.94.A8.E9.95.9C.E5.83.8F)
    *   [3.1 手动生成自定义的 initcpio](#.E6.89.8B.E5.8A.A8.E7.94.9F.E6.88.90.E8.87.AA.E5.AE.9A.E4.B9.89.E7.9A.84_initcpio)
*   [4 配置](#.E9.85.8D.E7.BD.AE)
    *   [4.1 模块（MODULES）](#.E6.A8.A1.E5.9D.97.EF.BC.88MODULES.EF.BC.89)
    *   [4.2 附加文件（BINARIES、FILES）](#.E9.99.84.E5.8A.A0.E6.96.87.E4.BB.B6.EF.BC.88BINARIES.E3.80.81FILES.EF.BC.89)
    *   [4.3 钩子(HOOKS)](#.E9.92.A9.E5.AD.90.28HOOKS.29)
        *   [4.3.1 编译钩子](#.E7.BC.96.E8.AF.91.E9.92.A9.E5.AD.90)
        *   [4.3.2 运行时钩子](#.E8.BF.90.E8.A1.8C.E6.97.B6.E9.92.A9.E5.AD.90)
        *   [4.3.3 常用钩子](#.E5.B8.B8.E7.94.A8.E9.92.A9.E5.AD.90)
        *   [4.3.4 编写钩子扩展](#.E7.BC.96.E5.86.99.E9.92.A9.E5.AD.90.E6.89.A9.E5.B1.95)
    *   [4.4 压缩方式(COMPRESSION)](#.E5.8E.8B.E7.BC.A9.E6.96.B9.E5.BC.8F.28COMPRESSION.29)
    *   [4.5 压缩选项(COMPRESSION_OPTIONS)](#.E5.8E.8B.E7.BC.A9.E9.80.89.E9.A1.B9.28COMPRESSION_OPTIONS.29)
*   [5 运行时配置](#.E8.BF.90.E8.A1.8C.E6.97.B6.E9.85.8D.E7.BD.AE)
    *   [5.1 从基本钩子启动](#.E4.BB.8E.E5.9F.BA.E6.9C.AC.E9.92.A9.E5.AD.90.E5.90.AF.E5.8A.A8)
    *   [5.2 使用 RAID 磁盘阵列](#.E4.BD.BF.E7.94.A8_RAID_.E7.A3.81.E7.9B.98.E9.98.B5.E5.88.97)
    *   [5.3 使用 net](#.E4.BD.BF.E7.94.A8_net)
    *   [5.4 使用 lvm](#.E4.BD.BF.E7.94.A8_lvm)
    *   [5.5 使用加密根目录](#.E4.BD.BF.E7.94.A8.E5.8A.A0.E5.AF.86.E6.A0.B9.E7.9B.AE.E5.BD.95)
    *   [5.6 /usr 放到单独分区](#.2Fusr_.E6.94.BE.E5.88.B0.E5.8D.95.E7.8B.AC.E5.88.86.E5.8C.BA)
*   [6 疑难解答](#.E7.96.91.E9.9A.BE.E8.A7.A3.E7.AD.94)
    *   [6.1 解压缩镜像](#.E8.A7.A3.E5.8E.8B.E7.BC.A9.E9.95.9C.E5.83.8F)
    *   [6.2 "/dev must be mounted" when it already is](#.22.2Fdev_must_be_mounted.22_when_it_already_is)
    *   [6.3 Using systemd HOOKS in a LUKS/LVM/resume setup](#Using_systemd_HOOKS_in_a_LUKS.2FLVM.2Fresume_setup)
    *   [6.4 Possibly missing firmware for module XXXX](#Possibly_missing_firmware_for_module_XXXX)
    *   [6.5 Standard rescue procedures](#Standard_rescue_procedures)
        *   [6.5.1 Boot succeeds on one machine and fails on another](#Boot_succeeds_on_one_machine_and_fails_on_another)
*   [7 参考资料](#.E5.8F.82.E8.80.83.E8.B5.84.E6.96.99)

## 概览

mkinitcpio是一个用来创建初始化内存盘（initial ramdisk，简称initrd）的bash脚本。摘自[mkinitcpio手册页](https://projects.archlinux.org/mkinitcpio.git/tree/man/mkinitcpio.8.txt)：

	*初始化内存盘本质上是一个很小的运行环境（早期用户空间，early userspace），用于加载一些核心模块，并在init接管启动过程之前准备一些必须的东西，比如加密的根文件系统、在RAID上的根文件系统。使用mkinicpio可以方便地使用自定义的钩子扩展（hooks）、运行时自动检测、以及其他功能。*

从前，内核在[启动过程](/index.php/Boot_process_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Boot process (简体中文)")早期（挂载根目录和启动`init`之前）处理一切硬件的检测和初始化。然而，但随着技术的演进，这种做法变得十分繁琐。

如今，根文件系统可能位于各种硬件上，如SCSI设备、SATA设备、U盘，而这些硬件受控于形形色色的厂家所提供的五花八门的驱动之下。另外，根系统可以加密、压缩，可存放在RAID阵列中，或者一个逻辑卷组上。为了简化这复杂的过程，可以把管理权转入一个用户空间：初始化内存盘。

另见：[/dev/brain0 » Blog Archive » Early Userspace in Arch Linux](https://web.archive.org/web/20150430223035/http://archlinux.me/brain0/2010/02/13/early-userspace-in-arch-linux/)。

用模块化的mkinitcpio构建初始化内存盘镜像（init ramfs cpio image），较之其他方法有诸多优势：

*   使用轻量的[BusyBox](http://www.busybox.net/)作为早期用户空间的基础（早在0.6版本时，使用的是[**klibc**](https://www.archlinux.org/news/486/)）。
*   支持**[udev](/index.php/Udev "Udev")**运行时硬件探测，避免加载不需要的模块。
*   支持可扩展的init钩子脚本，可以方便的使用[pacman](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)")软件包安装自定义钩子扩展。
*   同时支持传统和LUKS卷上的**lvm2**、**dm-crypt**，以及从U盘启动所需的**mdadm**、**swsusp**、**suspend2**。
*   支持通过启动参数配置内核功能，无需重新编译。

## 安装

[mkinitcpio](https://www.archlinux.org/packages/?name=mkinitcpio)软件包被收录于[官方软件仓库](/index.php/Official_repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official repositories (简体中文)")。作为[linux](https://www.archlinux.org/packages/?name=linux)软件包组的一部分，应该已经自动安装了。高级用户可以从[mkinitcpio-git](https://aur.archlinux.org/packages/mkinitcpio-git/) 获取 mkinitcpio 的最新开发版本.

**注意:** 若要使用git开发版本，强烈建议同时加入[arch-projectsarch-projects](https://mailman.archlinux.org/mailman/listinfo/arch-projects) 邮件列表！

## 创建和启用镜像

每次升级内核，mkinitcpio都会默认创建两个内存盘镜像：*默认*镜像`/boot/initramfs-linux.img`和*fallback*镜像`/boot/initramfs-linux-fallback.img`。*fallback*镜像和*默认*镜像只有一个区别，就是创建时跳过了**autodetect**钩子扩展，因而它包含更多的内核模块。**autodetect**扩展会探测硬件信息，针对硬件向镜像添加需要的模块，因此缩小了镜像。

在创建初始化内存盘镜像时，可以使用很多不同配置。创建完成后，在启动引导器[配置文件](/index.php/Boot_Loader#Configuration_files "Boot Loader")中添加启动项目，即可使用新镜像。更改mkinitcpio配置后，需要手动重新生成镜像。以Arch默认的内核[linux](https://www.archlinux.org/packages/?name=linux)为例：

```
# mkinitcpio -p linux

```

`-p`选项定义了要使用的预配置（preset）；多数内核软件包都会提供一套mkinitcpio预配置文件，放在`/etc/mkinitcpio.d`目录（比如，`linux`内核是`/etc/mkinitcpio.d/linux.preset`）。预配置文件中包含内存盘镜像的基本配置。

**警告:** 每次升级内核，系统都会自动使用**preset**文件重新生成内存盘镜像。不要轻易编辑这些文件。

### 手动生成自定义的 initcpio

使用其他配置文件创建镜像， 例如下面命令会根据`/etc/mkinitcpio-custom.conf`配置的内容生成镜像`/boot/linux-custom.img`.

```
# mkinitcpio -c /etc/mkinitcpio-custom.conf -g /boot/linux-custom.img

```

为其他不是当前正在运行的内核创建镜像，添加内核版本到命令行， 可以在`/usr/lib/modules`目录查看支持的内核版本.

```
 # mkinitcpio -g /boot/linux-custom2.img -k 3.3.0-ARCH

```

## 配置

**mkinitcpio**的主配置文件是`/etc/mkinitcpio.conf`。此外，内核软件包的预配置文件位于`/etc/mkinitcpio.d`（例如：`/etc/mkinitcpio.d/linux.preset`）。

**警告:** **lvm2**、**mdadm**、**encrypt**支持默认是**关闭**的。如果需要使用这些钩子扩展，请仔细阅读本章。

用户可以编辑配置文件中的六个变量：

	`MODULES`

	在钩子扩展运行前需要加载的内核模块。

	`BINARIES`

	内存盘镜像中包含的额外的二进制文件。

	`FILES`

	内存盘镜像中包含的其他文件。

	`HOOKS`

	要执行的钩子扩展。

	`COMPRESSION`

	内存盘镜像的压缩方式。

	`COMPRESSION_OPTIONS`

	传递给压缩工具的额外参数，不建议使用，可以自动根据压缩算法传递需要的参数(例如对 xz 传递 `--check=crc32` to xz), 手动设置了错误的参数可能导致系统无法启动。

### 模块（MODULES）

`MODULES`数组指定了启动过程最开始时就要加载的模块。

如果模块名称前加上一个“?”问号，那么即使系统无法找到该模块也不会报错。对于自己编译的内核，其中内置了某些模块，该功能可能有用。

**注意:** 如果使用**reiser4**，该模块*必须*放入`MODULES`数组。此外，如果运行mkinitcpio时未加载某些文件系统的模块，而系统启动时又必须使用这些文件系统——比如，LUKS加密密匙文件在**ext2**分区上，而使用mkinitcpio时系统并未挂载任何**ext2**分区——那么该文件系统的模块也必须放在`MODULES`数组。详情参见 [此文](/index.php/Dm-crypt/System_configuration#cryptkey "Dm-crypt/System configuration")。

如果挂载root分区时需要上述任一模块，请将其加入`/etc/mkinitcpio.conf`，以避免内核崩溃。

若使用多个拥有相同节点名、但内核模块不同的硬盘控制器（如两个SCSI/SATA或两个IDE控制器），应确保在`/etc/mkinitcpio.conf`中设置了正确的模块加载顺序。否则，系统无法确定根目录位置，导致崩溃（kernel panic）。另一个更好的办法是使用[永久性块设备名称](/index.php/Persistent_block_device_naming "Persistent block device naming")。

从 Linux 4.4 开始，如果使用 NVME 设备，请将 **nvme** 添加到模块列表。

### 附加文件（BINARIES、FILES）

这两个选项允许用户添加任何文件到镜像中。`BINARIES`、`FILES`数组指定了要加入内存盘镜像的文件，可以覆盖钩子扩展提供的文件。`BINARIES`中的二进制文件会自动放入一个标准的`PATH`路径，而且会自动加入可执行文件依赖的函数库。`FILES`中的文件则不进行上述处理，直接原样放入镜像。例如：

```
FILES="/etc/modprobe.d/modprobe.conf"

```

```
BINARIES="kexec"

```

配置支持多个选项，用空格隔开。

### 钩子(HOOKS)

`HOOKS`设置是此文件中最重要的设置。Hooks 是一系列的小脚本，描述那些东西需要加入到镜像里面。有些钩子还包含了运行组建，在启动时执行特定动作，例如启动服务、构建存储栈等。Hooks 按照配置文件中`HOOKS`项中给出的顺序执行。

默认的`HOOKS`可以满足大部分简单的单硬盘系统。对于[LVM](/index.php/LVM "LVM"), [mdadm](/index.php/Software_RAID_and_LVM "Software RAID and LVM") 或 [LUKS](/index.php/LUKS "LUKS") 等复杂根分区系统，请查看相应的 Wiki 页面。

**PS/2 键盘用户** : 要在初始化早期阶段使用键盘，请把 **keyboard** 钩子加入 `HOOKS`. 个别的键盘无法自动检测到 i8042 控制器，出现 `i8042: PNP: No PS/2 controller found. Probing ports directly` 报错信息，导致无法使用键盘，请把 **atkbd** 加入 `MODULES`.

#### 编译钩子

编译钩子位于`/usr/lib/initcpio/install`。这些文件会在运行 mkinitcpio 时被包含进脚本，应该提供如下两个函数：`build` 和 `help`.`build` 函数描述了需要加入镜像的模块、文件和二进制文件。mkinitcpio(8) 中的一个 API 会使用这些信息。`help` 函数在钩子执行后输出描述信息。

列出可用的钩子列表：

```
$ mkinitcpio -L

```

使用 mkinitcpio 的 `-H` 选项输出对于某一钩子的帮助。例如：

```
$ mkinitcpio -H udev

```

#### 运行时钩子

Runtime hooks are found in `/usr/lib/initcpio/hooks`. For any runtime hook, there should always be a build hook of the same name, which calls `add_runscript` to add the runtime hook to the image. These files are sourced by the busybox ash shell during early userspace. With the exception of cleanup hooks, they will always be run in the order listed in the `HOOKS` setting. Runtime hooks may contain several functions:

`run_earlyhook`: Functions of this name will be run once the API filesystems have been mounted and the kernel command line has been parsed. This is generally where additional daemons, such as udev, which are needed for the early boot process are started from.

`run_hook`: Functions of this name are run shortly after the early hooks. This is the most common hook point, and operations such as assembly of stacked block devices should take place here.

`run_latehook`: Functions of this name are run after the root device has been mounted. This should be used, sparingly, for further setup of the root device, or for mounting other filesystems, such as `/usr`.

`run_cleanuphook`: Functions of this name are run as late as possible, and in the reverse order of how they are listed in the `HOOKS` setting in the config file. These hooks should be used for any last minute cleanup, such as shutting down any daemons started by an early hook.

#### 常用钩子

下面是一个常见钩子和功能的表格。注意这个表格是不完整的，因为一些包会提供一些自定义的钩子。

<caption>**当前钩子**</caption>
| 钩子 | 安装 | 运行 |
| **base** | 设置初始目录并安装基本工具和库，一般都需要将其加为第一个钩子。 | -- |
| **systemd** | 在 initramfs 中安装一个基本的 systemd，会替代掉 'base', 'usr', 'udev' 钩子。其它钩子目前还需要调整。 如果使用了其它 systemd 钩子("sd-*")，这个钩子是 **必须的**。 从 systemd 207 开始，这个钩子和 lvm2 一起使用的时候可能会引起 boot 损坏，请使用 *sd-lvm2* 钩子替代 *lvm2*。同属，可以考虑保留 'base' 钩子(放在 systemd 钩子前) 以确保 initramfs 中包含应急 shell. [systemd](https://www.archlinux.org/packages/?name=systemd) 217 此钩子还会安装从 [hibernation](/index.php/Hibernation "Hibernation") 恢复的服务和执行程序。 | -- |
| **btrfs** | 加入启用 Btrfs 根目录和 subvolumes 需要的模块. | 如果没有 udev 钩子，会运行 "btrfs device scan" 生成多设备 btrfs 根文件系统。此钩子需要 [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs)。 |
| **udev** | 在镜像中加入 udevd, udevadm 和一小部分 udev 规则。 | 启动 udev 守护进程并处理内核的 uevents 事件，创建设备节点。简化了启动过程，用户不需要显示定义所需的模块，所以推荐使用。 |
| **autodetect** | 通过生成模块白名单缩减 initramfs 的大小，白名单中仅包含 sysfs 中扫描到的模块。请确认加入的模块正确，没有少加模块。此钩子必须在其它子系统钩子前运行，以利于自动检测的优势。'autodetect' 前的模块会全部加入。 | -- |
| **modconf** | 从 `/etc/modprobe.d` 和 `/usr/lib/modprobe.d`包含 modprobe 配置文件 | -- |
| **block** | Adds all block device modules, formerly separately provided by **fw**, **mmc**, **pata**, **sata**, **scsi** , **usb** and **virtio** hooks. | -- |
| **pcmcia** | 添加 PCMCIA 设备需要的模块。需要同时安装 [pcmciautils](https://www.archlinux.org/packages/?name=pcmciautils)。 | -- |
| **net** | 添加网络设备需要的模块。PCMCIA 网络设备请同时添加 **pcmcia** 钩子。 | 处理基于 NFS 的 root 文件系统。 |
| **dmraid** | Provides support for fakeRAID root devices. You must have [dmraid](https://www.archlinux.org/packages/?name=dmraid) installed to use this. Note that it is preferred to use `mdadm` with the **mdadm_udev** hook with fakeRAID if your controller supports it. | Locates and assembles fakeRAID block devices using `dmraid`. |
| **filesystems** | 加入需要的文件系统模块，只要没有在 MODULES 指定文件系统，就**必须**使用此钩子。 | -- |
| **lvm2** | 添加设备映射内核模块和 `lvm` 工具。需要安装 [lvm2](https://www.archlinux.org/packages/?name=lvm2) 软件包。 | 启用所有 LVM2 卷组，如果 root 位于 LVM 这是必须的。 |
| **sd-lvm2** | Use this hook instead of **lvm2** when using the **systemd** hook | Enables all LVM2 volume groups. This is necessary if you have your root file system on [LVM](/index.php/LVM "LVM"). |
| **mdadm** | 从 `/etc/mdadm.conf` 读取或启动时自动检测磁盘阵列。请优先使用下面的 **mdadm_udev** 钩子。 | 用 `mdassemble` 定位并组合软 RAID 块设备。 |
| **mdadm_udev** | 通过 udev 组合磁盘阵列。建议在二进制中包含 `mdmon` 并加入**shutdown** 钩子以避免重启时不必要的 raid 重建。 | 使用 `udev` 和 `mdadm` 组合软 RAID 块设备。 |
| **encrypt** | 添加 **dm-crypt** 内核模块和 `cryptsetup` 工具。需要安装 [cryptsetup](https://www.archlinux.org/packages/?name=cryptsetup) 软件包。 | 检查并解密 root 分区。详情参见 [#Runtime customization](#Runtime_customization)。 |
| **resume** | -- | Tries to resume from the "suspend to disk" state. Works with both *swsusp* and *[TuxOnIce](/index.php/TuxOnIce "TuxOnIce")*. See [Hibernation](/index.php/Hibernation "Hibernation") for further configuration. Intended to work along with the `base` hook, the `systemd` hook provides its own resume mechanism. |
| **keyboard** | Adds the necessary modules for keyboard devices. Use this if you have an USB keyboard and need it in early userspace (either for entering encryption passphrases or for use in an interactive shell). As a side effect, modules for some non-keyboard input devices might be added to, but this should not be relied on. | -- |
| **keymap** | Adds the specified keymap(s) from `/etc/vconsole.conf` to the initramfs. | Loads the specified keymap(s) from `/etc/vconsole.conf` during early userspace. |
| **consolefont** | Adds the specified console font from `/etc/vconsole.conf` to the initramfs. | Loads the specified console font from `/etc/vconsole.conf` during early userspace. |
| **sd-vconsole** | Adds the keymap(s) and console font specified in `/etc/vconsole.conf` to the systemd-based initramfs. | Loads the specified keymap(s) and console font during early userspace. |
| **sd-encrypt** | This hook allows for an encrypted root device with systemd initramfs. See the man page of systemd-cryptsetup-generator(8) for available kernel command line options. Alternatively, if the file `/etc/crypttab.initramfs` exists, it will be added to the initramfs as `/etc/crypttab`. See the crypttab(5) manpage for more information on crypttab syntax. | -- |
| **fsck** | 添加 fsck 程序和文件系统专用工具，如果添加在 **autodetect** 钩子后面，仅会添加根文件系统需要的工具。强烈推荐所用用户使用， /usr 单独分区的用户必须使用此钩子。 | 对根分区 (和单独分区的 /usr) 执行 fsck。The use of this hook requires the rw parameter to be set on the kernel commandline ([discussion](https://bbs.archlinux.org/viewtopic.php?pid=1307895#p1307895)). |
| **shutdown** | 增加关机 initramfs 支持，从 mkinitcpio 0.16 开始，已经 [不再需要](https://mailman.archlinux.org/pipermail/arch-dev-public/2013-December/025742.html)。 | 卸载并关闭设备。 |
| **usr** | 加入对单独 `/usr` 分区的支持 | 在 root 挂载后挂载 `/usr` 分区. |

#### 编写钩子扩展

一个 initcpio 钩子仅仅是另一段 shell 脚本，它包含了必要的信息指引 mkinitcpio 哪一个可执行文件应该被加载，以及以什么参数被加载。它在某些罕见情况下很有用，比如一些文件需要在用户空间的早期或晚期被加载，而这又没有被其他已经安装的脚本提供。

首先创建实际的脚本：

 `/usr/lib/initcpio/install/**hook**` 
```
 #!/bin/bash

 build() {
     add_binary /bin/bash  #/bin/bash is given as an example, you can type your desired executable here
     add_runscript  # will determine the name of the script, and add appropriately from /usr/lib/initcpio/hooks
 }

 help() {
     cat <<HELPEOF
     Line used as help information #Typing mkinitcpio -H hook will display this information
 HELPEOF
 }

```

然后创建这个实际的钩子：

 `/usr/lib/initcpio/hooks/**hook**` 
```
 run_hook ()
 {
     msg -n ":: This is an example hook"
     bash #your executable example
     msg "done."
 }

```

**注意:** 没有必要为这两个脚本设定可执行权限，也不建议这样做。

现在编辑 `/etc/mkinitcpio.conf` 来包含你的自定义钩子。你也可在 `/etc/rc.sysinit` 包含脚本来在用户空间的后期加载。

### 压缩方式(COMPRESSION)

内核支持几种initramfs的压缩方式 - gzip, bzip2, lzma, xz (也被称为 lzma2), lzo 和 lz4。对于大多数使用的情况，gzip, lzop, lz4 提供了基本的压缩大小和解压缩速度的平衡。

```
COMPRESSION="gzip"
COMPRESSION="bzip2"
COMPRESSION="lzma"
COMPRESSION="lzop"
COMPRESSION="xz"
COMPRESSION="lz4"

```

不指定 `COMPRESSION` 选项会导致使用 gzip 压缩的 initramfs 文件。想要创建一个未压缩的镜像，在配置中指定`COMPRESSION=cat` 或者在命令行使用 `-z cat`.

请按照选择的压缩方式安装需要的工具。

### 压缩选项(COMPRESSION_OPTIONS)

还有一些额外的标准可以传递到 `COMPRESSION` 指定的程序，例如：

```
COMPRESSION_OPTIONS='-9'

```

通常这些是不需要的，因为 mkinitcpio 会确保任何支持的压缩方法有必要的标志来产生一个可以工作的镜像。

## 运行时配置

运行时配置选项可以通过内核命令行传递到 `init` 以及某些钩子。内核命令行参数通常是由启动引导器提供。参见 [Arch 启动过程](/index.php/Arch_boot_process_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch boot process (简体中文)")和[Kernel parameters](/index.php/Kernel_parameters "Kernel parameters")以获取更多信息。

### 从基本钩子启动

	`root`

	这是内核命令行中指定的最重要的参数，因为它决定了哪一个设备会被挂载为你的正确的 root 设备。mkinitcpio 可以灵活的允许不同的格式，例如：

```
root=/dev/sda1                                                # /dev 节点
root=LABEL=CorsairF80                                         # 卷标
root=UUID=ea1c4959-406c-45d0-a144-912f4e86b207                # UUID
root=PARTUUID=14420948-2cea-4de7-b042-40f67c618660            # GPT partition UUID

```

**注意:** 下面的选项改变了 `init` 在 initramfs 环境中的默认行为。参见 `/lib/initcpio/init` 获取更多信息。

	`break`

	如果`break` 或者 `break=premount` 被指定，`init` 暂停启动过程(在加载钩子之后，但是在挂载根文件系统之前) 然后启动一个交互的 shell，可以用来解决问题。这个 shell 可以在root被指定的`break=postmount`挂载之后启动。正常的启动过程可以在退出这个 shell 之后继续。

	`disablehooks`

	在运行时可以通过添加 `disablehooks=hook1{,hook2,...}` 禁用某些钩子。例如 `disablehooks=resume` 

	`earlymodules`

	改变模块加载的顺序。可以通过 `earlymodules=mod1{,mod2,...}` 指定一些模块提前加载。 (例如，这可以用来确保多个网络接口的正确顺序。)

	`rootdelay`

	通过附加 `rootdelay` 在挂载根文件系统之前暂停十秒。(它的用途是，例如，从USB硬盘启动时会花更长时间来初始化。)

参见: [GRUB 和 init 调试](/index.php/Boot_debugging "Boot debugging")

### 使用 RAID 磁盘阵列

首先，在 `/etc/mkinitcpio.conf` 文件中把 `mdadm_udev` 或 `mdadm` 钩子加入到 `HOOKS` 数组中，以及将任何需要的 RAID 模块(raid456, ext4)添加到 `MODULES` 数组中。

**内核参数:** 使用 `mdadm` 钩子，你不再需要在 [kernel parameters](/index.php/Kernel_parameters "Kernel parameters") 参数中配置你的 RAID 磁盘阵列。在启动过程中(init phase)，`mdadm` 钩子会或者使用你的 `/etc/mdadm.conf` 文件或者自动探测磁盘阵列。

也可通过使用 `mdadm_udev` 钩子，使用 udev 组装(assemble)。上游倾向于使用这个组装方法。`/etc/mdadm.conf` 仍然会被读取，目的是命名可能存在的已经组装的设备。

### 使用 net

**警告:** 尚未支持 NFSv4。

**需要的包：**

net 需要 [mkinitcpio-nfs-utils](https://www.archlinux.org/packages/?name=mkinitcpio-nfs-utils) 包，在[官方源](/index.php/%E5%AE%98%E6%96%B9%E6%BA%90 "官方源")中就有。

**内核参数：**

```
[内核文档](https://www.kernel.org/doc/Documentation/filesystems/nfs/nfsroot.txt)包含最新的信息和清晰的说明。

```

**ip=**

This parameter tells the kernel how to configure IP addresses of devices and also how to set up the IP routing table. It can take up to nine arguments separated by colons: `ip=<client-ip>:<server-ip>:<gw-ip>:<netmask>:<hostname>:<device>:<autoconf>:<dns0-ip>:<dns1-ip>`.

If this parameter is missing from the kernel command line, all fields are assumed to be empty, and the defaults mentioned in the [kernel documentation](https://www.kernel.org/doc/Documentation/filesystems/nfs/nfsroot.txt) apply. In general this means that the kernel tries to configure everything using autoconfiguration.

The `<autoconf>` parameter can appear alone as the value to the 'ip' parameter (without all the ':' characters before). If the value is "ip=off" or "ip=none", no autoconfiguration will take place, otherwise autoconfiguration will take place. The most common way to use this is "ip=dhcp".

*例子：*

```
 ip=127.0.0.1:::::lo:none  --> Enable the loopback interface.
 ip=192.168.1.1:::::eth2:none --> Enable static eth2 interface.
 ip=:::::eth0:dhcp --> Enable dhcp protocol for eth0 configuration.

```

**Note:** Make sure to use kernel device names (e.g. *eth0*) for the `<device>` parameter, and not [udev](/index.php/Network_configuration#Device_names "Network configuration") ones (e.g. *enp2s0*) as those will not work.

**BOOTIF=** 使用多个网卡的时候，此参数可以指定要使用网卡的 Mac 地址。在接口号可能变化或与 IPAPPEND 2 、IPAPPEND 3 选项共用时比较有用。默认使用 eth0.

示例：

```
BOOTIF=01-A1-B2-C3-D4-E5-F6  # Note the prepended "01-" and capital letters.

```

**nfsroot=**

如果命令行中没有给出 `nfsroot` 参数，那么默认的 `/tftpboot/%s` 会被使用。

```
 nfsroot=[<server-ip>:]<root-dir>[,<nfs-options>]

```

*参数解释：*

```
 <server-ip>   Specifies the IP address of the NFS server. If this field
               is not given, the default address as determined by the
               `ip' variable (see below) is used. One use of this
               parameter is for example to allow using different servers
               for RARP and NFS. Usually you can leave this blank.

 <root-dir>    Name of the directory on the server to mount as root. If
               there is a "%s" token in the string, the token will be
               replaced by the ASCII-representation of the client's IP
               address.

 <nfs-options> Standard NFS options. All options are separated by commas.
               If the options field is not given, the following defaults
               will be used:
                       port            = as given by server portmap daemon
                       rsize           = 1024
                       wsize           = 1024
                       timeo           = 7
                       retrans         = 3
                       acregmin        = 3
                       acregmax        = 60
                       acdirmin        = 30
                       acdirmax        = 60
                       flags           = hard, nointr, noposix, cto, ac

```

**root=/dev/nfs**

如果你不使用 `nfsroot` 参数，你需要设定 `root=/dev/nfs` 来通过自动配置从一个 NFS root 启动。

### 使用 lvm

如果你的根设备是在[LVM](/index.php/LVM "LVM") 上，你必须添加 **lvm2** 钩子。请阅读 [这里](/index.php/LVM#Add_lvm2_hook_to_mkinitcpio.conf_for_root_on_LVM "LVM").

### 使用加密根目录

如果使用 [加密 root](/index.php/Dm-crypt/Encrypting_an_entire_system "Dm-crypt/Encrypting an entire system"), `encrypt` 钩子需要加到 `filesystems` 和其它需要的钩子之前。并且需要一些额外的内核命令参数，请参考 [Dm-crypt/System configuration#mkinitcpio](/index.php/Dm-crypt/System_configuration#mkinitcpio "Dm-crypt/System configuration")。

### /usr 放到单独分区

如果将 /usr 放在单独分区，必须满足：

*   启用 `mkinitcpio-generate-shutdown-ramfs.service` **或** 添加 `shutdown` 钩子.
*   添加 `fsck` 钩子，在`/etc/fstab`中将`/usr`的`passno`设置为`0`。这个对其他用户是推荐选项，而对 /usr 单独分区用户是硬性要求。不添加这个钩子，没有此选项，系统不好对`/usr`进行磁盘检查。
*   从 mkinitcpio 0.9.0 开始: 添加上面的钩子和 `usr` 钩子，它会在 root 挂载后挂载 `/usr` 分区。
*   在 0.9.0 之前，如果真正 root 中的 `/etc/fstab` 包含 `/usr`，将会自动挂载它, 参考 [Fstab](/index.php/Fstab "Fstab").

## 疑难解答

### 解压缩镜像

如果你对 initrd 镜像的内容感到好奇，你可以解压缩它然后看看里面的文件。

initrd 镜像是一个 SVR4 CPIO 压缩包，通过 `find` 和 `bsdcpio` 命令生成，可选可被内核理解的压缩方式参考上面的压缩部分。

mkinitcpio 包含了一个叫做 `lsinitcpio` 的工具，可以列出和解压缩出 initramfs 镜像的内容。

你可以用下面的命令列出镜像中的文件：

```
$ lsinitcpio /boot/initramfs-linux.img

```

然后全部解压缩到当前文件夹：

```
$ lsinitcpio -x /boot/initramfs-linux.img

```

你也可以用更对人类友好的方式列出镜像中的重要的部分：

```
$ lsinitcpio -a /boot/initramfs-linux.img

```

### "/dev must be mounted" when it already is

The test used by mkinitcpio to determine if /dev is mounted is to see if /dev/fd/ is there. If everything else looks fine, it can be "created" manually by:

```
# ln -s /proc/self/fd /dev/

```

(Obviously, /proc must be mounted as well. mkinitcpio requires that anyway, and that is the next thing it will check.)

### Using systemd HOOKS in a LUKS/LVM/resume setup

Using `systemd/sd-encrypt/sd-lvm2` **HOOKS** instead of the traditional `encrypt/lvm2/resume` requires different initrd parameters to be passed by your bootloader. See this post on forum for details [[1]](https://bbs.archlinux.org/viewtopic.php?pid=1480241).

### Possibly missing firmware for module XXXX

When initramfs are being rebuild after a kernel update, you might get these two warnings:

```
==> WARNING: Possibly missing firmware for module: aic94xx
==> WARNING: Possibly missing firmware for module: smsmdtv 

```

These appear to any Arch Linux users, especially those who have not installed these firmware modules. If you do not use hardware which uses these firmwares you can safely ignore this message.

### Standard rescue procedures

With an improper initial ram-disk a system often is unbootable. So follow a system rescue procedure like below:

#### Boot succeeds on one machine and fails on another

*mkinitcpio'*s `autodetect` hook filters unneeded [kernel modules](/index.php/Kernel_modules "Kernel modules") in the primary initramfs scanning `/sys` and the modules loaded at the time it is run. If you transfer your `/boot` directory to another machine and the boot sequence fails during early userspace, it may be because the new hardware is not detected due to missing kernel modules.

To fix, first try choosing the [fallback](#Image_creation_and_activation) image from your [bootloader](/index.php/Bootloader "Bootloader"), as it is not filtered by `autodetect`. Once booted, run *mkinitcpio* on the new machine to rebuild the primary image with the correct modules. If the fallback image fails, try booting into an Arch Linux live CD/USB, chroot into the installation, and run *mkinitcpio* on the new machine. As a last resort, try [manually](#MODULES) adding modules to the initramfs.

## 参考资料

*   [Boot debugging](/index.php/Boot_debugging "Boot debugging") - 用 GRUB 调试
*   Linux Kernel documentation on [initramfs](http://git.kernel.org/?p=linux/kernel/git/torvalds/linux-2.6.git;a=blob;f=Documentation/filesystems/ramfs-rootfs-initramfs.txt;hb=HEAD)
*   Linux Kernel documentation on [initrd](http://git.kernel.org/?p=linux/kernel/git/torvalds/linux-2.6.git;a=blob;f=Documentation/initrd.txt;hb=HEAD)
*   Wikipedia article on [initrd](https://en.wikipedia.org/wiki/initrd "wikipedia:initrd")