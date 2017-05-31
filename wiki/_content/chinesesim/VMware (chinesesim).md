**翻译状态：** 本文是英文页面 [VMware](/index.php/VMware "VMware") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-05-26，点击[这里](https://wiki.archlinux.org/index.php?title=VMware&diff=0&oldid=478292)可以查看翻译后英文页面的改动。

本文是关于在 Arch 中安装 VMware，你也许想寻找的是 [在 VMware 中安装 Arch Linux](/index.php/Installing_Arch_Linux_in_VMware_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Installing Arch Linux in VMware (简体中文)")

**注意:**

*   这篇文章时针对最新的VMware正式版,即VMware Workstation Pro 和Player 12.5.
*   而对于旧版本,可以使用[vmware-patch](https://aur.archlinux.org/packages/vmware-patch/)包

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
    *   [2.1 内核模块](#.E5.86.85.E6.A0.B8.E6.A8.A1.E5.9D.97)
    *   [2.2 Systemd 服务](#Systemd_.E6.9C.8D.E5.8A.A1)
        *   [2.2.1 Workstation Server服务](#Workstation_Server.E6.9C.8D.E5.8A.A1)
*   [3 启动程序](#.E5.90.AF.E5.8A.A8.E7.A8.8B.E5.BA.8F)
*   [4 提示和技巧](#.E6.8F.90.E7.A4.BA.E5.92.8C.E6.8A.80.E5.B7.A7)
    *   [4.1 输入Workstation Pro许可密钥](#.E8.BE.93.E5.85.A5Workstation_Pro.E8.AE.B8.E5.8F.AF.E5.AF.86.E9.92.A5)
        *   [4.1.1 从终端](#.E4.BB.8E.E7.BB.88.E7.AB.AF)
        *   [4.1.2 从 GUI](#.E4.BB.8E_GUI)
    *   [4.2 解压缩 VMware BIOS](#.E8.A7.A3.E5.8E.8B.E7.BC.A9_VMware_BIOS)
    *   [4.3 解压缩安装程序](#.E8.A7.A3.E5.8E.8B.E7.BC.A9.E5.AE.89.E8.A3.85.E7.A8.8B.E5.BA.8F)
        *   [4.3.1 使用修改过的 BIOS](#.E4.BD.BF.E7.94.A8.E4.BF.AE.E6.94.B9.E8.BF.87.E7.9A.84_BIOS)
    *   [4.4 在Intel和Optimus上启用3D图形](#.E5.9C.A8Intel.E5.92.8COptimus.E4.B8.8A.E5.90.AF.E7.94.A83D.E5.9B.BE.E5.BD.A2)
*   [5 疑难解答](#.E7.96.91.E9.9A.BE.E8.A7.A3.E7.AD.94)
    *   [5.1 错误：/dev/vmmon not found](#.E9.94.99.E8.AF.AF.EF.BC.9A.2Fdev.2Fvmmon_not_found)
    *   [5.2 错误：/dev/vmci not found](#.E9.94.99.E8.AF.AF.EF.BC.9A.2Fdev.2Fvmci_not_found)
    *   [5.3 错误：Kernel headers for version 4.x-xxxx were not found. If you installed them[...]](#.E9.94.99.E8.AF.AF.EF.BC.9AKernel_headers_for_version_4.x-xxxx_were_not_found._If_you_installed_them.5B....5D)
    *   [5.4 无法识别 USB 设备](#.E6.97.A0.E6.B3.95.E8.AF.86.E5.88.AB_USB_.E8.AE.BE.E5.A4.87)
    *   [5.5 安装程序启动失败](#.E5.AE.89.E8.A3.85.E7.A8.8B.E5.BA.8F.E5.90.AF.E5.8A.A8.E5.A4.B1.E8.B4.A5)
    *   [5.6 用户界面初始化失败](#.E7.94.A8.E6.88.B7.E7.95.8C.E9.9D.A2.E5.88.9D.E5.A7.8B.E5.8C.96.E5.A4.B1.E8.B4.A5)
    *   [5.7 无法为客户机下载VMware Tools](#.E6.97.A0.E6.B3.95.E4.B8.BA.E5.AE.A2.E6.88.B7.E6.9C.BA.E4.B8.8B.E8.BD.BDVMware_Tools)
    *   [5.8 当远程访问VMware时，遇到不正确的用户名/密码错误](#.E5.BD.93.E8.BF.9C.E7.A8.8B.E8.AE.BF.E9.97.AEVMware.E6.97.B6.EF.BC.8C.E9.81.87.E5.88.B0.E4.B8.8D.E6.AD.A3.E7.A1.AE.E7.9A.84.E7.94.A8.E6.88.B7.E5.90.8D.2F.E5.AF.86.E7.A0.81.E9.94.99.E8.AF.AF)
    *   [5.9 ALSA输出的问题](#ALSA.E8.BE.93.E5.87.BA.E7.9A.84.E9.97.AE.E9.A2.98)
    *   [5.10 错误：Kernel-based Virtual Machine (KVM) is running](#.E9.94.99.E8.AF.AF.EF.BC.9AKernel-based_Virtual_Machine_.28KVM.29_is_running)
    *   [5.11 旧的Intel微指令在启动时产生段错误](#.E6.97.A7.E7.9A.84Intel.E5.BE.AE.E6.8C.87.E4.BB.A4.E5.9C.A8.E5.90.AF.E5.8A.A8.E6.97.B6.E4.BA.A7.E7.94.9F.E6.AE.B5.E9.94.99.E8.AF.AF)
    *   [5.12 错误：Guests have incorrect system clocks or are unable to boot: "[...]timeTracker_user.c:234 bugNr=148722"](#.E9.94.99.E8.AF.AF.EF.BC.9AGuests_have_incorrect_system_clocks_or_are_unable_to_boot:_.22.5B....5DtimeTracker_user.c:234_bugNr.3D148722.22)
    *   [5.13 Guests系统启动后网络不可用](#Guests.E7.B3.BB.E7.BB.9F.E5.90.AF.E5.8A.A8.E5.90.8E.E7.BD.91.E7.BB.9C.E4.B8.8D.E5.8F.AF.E7.94.A8)
    *   [5.14 在Linux 4.9后内核模块无法编译](#.E5.9C.A8Linux_4.9.E5.90.8E.E5.86.85.E6.A0.B8.E6.A8.A1.E5.9D.97.E6.97.A0.E6.B3.95.E7.BC.96.E8.AF.91)
    *   [5.15 版本号为12.5.4的vmplayer/vmware无法启动](#.E7.89.88.E6.9C.AC.E5.8F.B7.E4.B8.BA12.5.4.E7.9A.84vmplayer.2Fvmware.E6.97.A0.E6.B3.95.E5.90.AF.E5.8A.A8)
    *   [5.16 版本号为12.5.3的vmplayer/vmware无法启动](#.E7.89.88.E6.9C.AC.E5.8F.B7.E4.B8.BA12.5.3.E7.9A.84vmplayer.2Fvmware.E6.97.A0.E6.B3.95.E5.90.AF.E5.8A.A8)
    *   [5.17 vmware 12的进程在启动之后立即终止，没有显示GUI](#vmware_12.E7.9A.84.E8.BF.9B.E7.A8.8B.E5.9C.A8.E5.90.AF.E5.8A.A8.E4.B9.8B.E5.90.8E.E7.AB.8B.E5.8D.B3.E7.BB.88.E6.AD.A2.EF.BC.8C.E6.B2.A1.E6.9C.89.E6.98.BE.E7.A4.BAGUI)
    *   [5.18 VMware模块在Linux内核4.11+上（在GCC7下）编译失败](#VMware.E6.A8.A1.E5.9D.97.E5.9C.A8Linux.E5.86.85.E6.A0.B84.11.2B.E4.B8.8A.EF.BC.88.E5.9C.A8GCC7.E4.B8.8B.EF.BC.89.E7.BC.96.E8.AF.91.E5.A4.B1.E8.B4.A5)
*   [6 卸载](#.E5.8D.B8.E8.BD.BD)

## 安装

[安装](/index.php/Pacman "Pacman") 依赖项:

*   [fuse2](https://www.archlinux.org/packages/?name=fuse2) - 提供*vmware-vmblock-fuse*
*   [gksu](https://www.archlinux.org/packages/?name=gksu) - 支持root操作（比如内存分配、注册许可证等等）
*   [gtkmm](https://www.archlinux.org/packages/?name=gtkmm) - 支持GUI
*   [linux-headers](https://www.archlinux.org/packages/?name=linux-headers) - 提供模块编译
*   [ncurses5-compat-libs](https://aur.archlinux.org/packages/ncurses5-compat-libs/) - 被`--console`安装程序需要
*   [libcanberra](https://www.archlinux.org/packages/?name=libcanberra) - 支持事件提示音

下载最新的[VMware Workstation Pro](https://www.vmware.com/go/tryworkstation)或[Player](https://www.vmware.com/go/downloadplayer) (或者[beta](https://communities.vmware.com/community/vmtn/beta)版本,当可用时).

开始安装：

```
# sh VMware-*edition*-*version*.*release*.*architecture*.bundle

```

**提示：** 一些常用的选项：

*   `--eulas-agreed` - 跳过各种许可协议
*   `--console` - 使用控制台UI
*   `--custom` - 允许自定义安装目录，比如`/usr/local`（记得修改[#Systemd 服务](#Systemd_.E6.9C.8D.E5.8A.A1)一节下，`vmware-usbarbitrator.service`中的路径）
*   `-I`, `--ignore-errors` - 忽略致命错误
*   `--set-setting=vmware-workstation serialNumber XXXXX-XXXXX-XXXXX-XXXXX-XXXXX` - 设置安装时使用的序列号（有利于脚本化安装）
*   `--required` - 只询问必要的问题（当结合`--eulas-agreed`和`--console`时可以实现静默安装）

将`System service scripts directory`设置为`/etc/init.d` (默认值)

**注意:** 安装过程中会收到`"No rc*.d style init script directories"`错误。这可以安全忽略，因为Arch使用的是[systemd](/index.php/Systemd "Systemd").

**提示：** 从终端上（重新）构建模块，使用:
```
# vmware-modconfig --console --install-all

```

## 配置

### 内核模块

VMware Workstation 12.5 最高支持内核 4.8.

### Systemd 服务

*(可选)* 你也可以创建一个 `.service` 文件 (也可以用[AUR](/index.php/AUR "AUR")中的[vmware-systemd-services](https://aur.archlinux.org/packages/vmware-systemd-services/)包)，而不是直接使用 `/etc/init.d/vmware` (`start|stop|status|restart`) 和 `/usr/bin/vmware-usbarbitrator` 来管理服务：

 `/etc/systemd/system/vmware.service` 
```
[Unit]
Description=VMware daemon
Requires=vmware-usbarbitrator.service
Before=vmware-usbarbitrator.service
After=network.target

[Service]
ExecStart=/etc/init.d/vmware start
ExecStop=/etc/init.d/vmware stop
PIDFile=/var/lock/subsys/vmware
RemainAfterExit=yes

[Install]
WantedBy=multi-user.target
```
 `/etc/systemd/system/vmware-usbarbitrator.service` 
```
[Unit]
Description=VMware USB Arbitrator
Requires=vmware.service
After=vmware.service

[Service]
ExecStart=/usr/bin/vmware-usbarbitrator
ExecStop=/usr/bin/vmware-usbarbitrator --kill
RemainAfterExit=yes

[Install]
WantedBy=multi-user.target
```

如果你想在另一个Workstation服务器控制台上连接此次安装的VMware Workstation，请添加下面的服务

 `/etc/systemd/system/vmware-workstation-server.service` 
```
[Unit]
Description=VMware Workstation Server
Requires=vmware.service
After=vmware.service

[Service]
ExecStart=/etc/init.d/vmware-workstation-server start
ExecStop=/etc/init.d/vmware-workstation-server stop
PIDFile=/var/lock/subsys/vmware-workstation-server
RemainAfterExit=yes

[Install]
WantedBy=multi-user.target
```

之后您就可以在启动时[enable](/index.php/Enable "Enable")它们.

#### Workstation Server服务

服务`vmware-workstation-server.service`将调用`wssc-adminTool`，即使后者已经被重命名作`vmware-wssc-adminTool`.

这将阻止该服务启动。创建一个文件链接可以修复这个问题：

```
# ln -s wssc-adminTool /usr/lib/vmware/bin/vmware-wssc-adminTool

```

## 启动程序

启动VMware Workstation Pro:

```
$ vmware

```

或Player:

```
$ vmplayer

```

## 提示和技巧

### 输入Workstation Pro许可密钥

#### 从终端

```
# /usr/lib/vmware/bin/vmware-vmx-debug --new-sn XXXXX-XXXXX-XXXXX-XXXXX-XXXXX

```

`XXXXX-XXXXX-XXXXX-XXXXX-XXXXX` 处是你的许可密钥。

**Note:** The `-debug` binary informs the user of an incorrect license.

#### 从 GUI

如果以上方法无效，你可以试试:

```
# /usr/lib/vmware/bin/vmware-enter-serial

```

### 解压缩 VMware BIOS

```
$ objcopy /usr/lib/vmware/bin/vmware-vmx -O binary -j bios440 --set-section-flags bios440=a bios440.rom.Z
$ perl -e 'use Compress::Zlib; my $v; read STDIN, $v, '$(stat -c%s "./bios440.rom.Z")'; $v = uncompress($v); print $v;' < bios440.rom.Z > bios440.rom

```

### 解压缩安装程序

查看安装程序`.bundle`的内容:

```
$ sh VMware-*edition*-*version*.*release*.*architecture*.bundle --extract */tmp/vmware-bundle/*

```

#### 使用修改过的 BIOS

如果你决定修改解压出的BIOS，你可以通过将其移动至`~/vmware/<Virtual machine name>`来让虚拟机使用它:

```
$ mv bios440.rom ~/vmware/*Virtual_machine_name*/

```

然后在 `<Virtual machine name>.vmx` 文件中加入它的名称：

 `~/vmware/*Virtual_machine_name*/*Virtual_machine_name*.vmx`  `bios440.filename = "bios440.rom"` 

### 在Intel和Optimus上启用3D图形

由于不理想和（或）不稳定的3D加速，某些图形驱动是默认被阻止的。当启用*Accelerate 3D graphics*后，log中应该会出现：

```
Disabling 3D on this host due to presence of Mesa DRI driver.  Set mks.gl.allowBlacklistedDrivers = TRUE to override.

```

这表示：

 `~/.vmware/preferences`  `mks.gl.allowBlacklistedDrivers = TRUE` 

## 疑难解答

### 错误：/dev/vmmon not found

完整的错误是:

```
Could not open /dev/vmmon: No such file or directory.
Please make sure that the kernel module `vmmon' is loaded.

```

这意味着未加载`vmmon`模块.参见[#Systemd 服务](#Systemd_.E6.9C.8D.E5.8A.A1)章节

### 错误：/dev/vmci not found

完整的错误是:

```
Failed to open device "/dev/vmci": No such file or directory
Please make sure that the kernel module 'vmci' is loaded.

```

尝试重新编译VMware内核模块：

```
# vmware-modconfig --console --install-all

```

### 错误：Kernel headers for version 4.x-xxxx were not found. If you installed them[...]

安装 [linux-headers](https://www.archlinux.org/packages/?name=linux-headers)。

**Note:** 更新内核和头文件会需要你启动新的内核以匹配头文件的版本。这是一个相对常见的错误。

### 无法识别 USB 设备

**提示：** 可以通过 [vmware-patch](https://aur.archlinux.org/packages/vmware-patch/) 解决。

如果不使用[#Systemd 服务](#Systemd_.E6.9C.8D.E5.8A.A1)来处理服务，你每次都需要以root身份手动启动`vmware-usbarbitrator`.

启动：

```
# vmware-usbarbitrator

```

停止:

```
# vmware-usbarbitrator --kill

```

### 安装程序启动失败

如果你回到了执行`.bundle`时的终端提示，则这个版本的VMware Installer也许坏掉了或者不完整，你应该删掉它（你也许也应该参照[#卸载](#.E5.8D.B8.E8.BD.BD)一节中的内容）:

```
# rm -r /etc/vmware-installer

```

### 用户界面初始化失败

你也许会看到这样的错误：

```
Extracting VMware Installer...done.
No protocol specified
No protocol specified
User interface initialization failed.  Exiting.  Check the log for details.

```

这可以通过安装[ncurses5-compat-libs](https://aur.archlinux.org/packages/ncurses5-compat-libs/)或者临时允许X拥有root权限来解决：

```
$ xhost +
$ sudo ./<vmware filename>.bundle
$ xhost -

```

### 无法为客户机下载VMware Tools

访问[VMware repository](http://softwareupdate.vmware.com/cds/vmw-desktop/)来手动下载这些工具。

导航至："*application name* / *version* / *build ID* / linux / packages/"来下载合适的工具。

解压：

```
$ tar -xvf vmware-tools-*name*-*version*-*buildID*.x86_64.component.tar

```

并通过VMware安装程序安装：

```
# vmware-installer --install-component=*/path/*vmware-tools-*name*-*version*-*buildID*.x86_64.component

```

如果上述步骤不管用，尝试安装[ncurses5-compat-libs](https://aur.archlinux.org/packages/ncurses5-compat-libs/)

### 当远程访问VMware时，遇到不正确的用户名/密码错误

VMware Workstation通过`vmware-workstation-server`服务来提供远程管理共享的虚拟机的功能。然而，这将以错误`"incorrect username/password"`而告终，因为`vmware-authd`服务中，[PAM](/index.php/PAM "PAM")的相关配置出错了。通过编辑`/etc/pam.d/vmware-authd`来解决问题:

 `/etc/pam.d/vmware-authd` 
```
#%PAM-1.0
auth     *required       pam_unix.so*
account  *required       pam_unix.so*
password *required       pam_permit.so*
session  *required       pam_unix.so*

```

然后重新启动`vmware`[systemd](/index.php/Systemd "Systemd")服务。

现在你能通过安装时提供的身份信息来登录这个服务器了。

**Note:** 也许会需要[libxslt](https://www.archlinux.org/packages/?name=libxslt)来启动虚拟机

### ALSA输出的问题

[修复](http://bankimbhavsar.blogspot.co.nz/2011/09/hd-audio-in-vmware-fusion-4-and-vmware.html)音质问题或正确启用高清音频输出。首先执行:

```
$ aplay -L

```

如果希望在客户机中播放5.1 *立体声*，寻找`surround51:CARD=*vendor_name*,DEV=*num*`；如果存在音质问题，寻找`front:CARD=*vendor_name*,DEV=*num*`。最后将名称加入到`.vmx`文件中:

 `~/vmware/*Virtual_machine_name*/*Virtual_machine_name*.vmx` 
```
sound.fileName=*"surround51:CARD=Live,DEV=0"*
sound.autodetect=*"FALSE"*
```

[OSS模拟](/index.php/Advanced_Linux_Sound_Architecture#OSS_compatibility "Advanced Linux Sound Architecture")也应该被禁用.

### 错误：Kernel-based Virtual Machine (KVM) is running

禁止`KVM`自动启动，你可以：

 `/etc/modprobe.d/vmware.conf` 
```
blacklist kvm
blacklist kvm-amd   # For AMD CPUs
blacklist kvm-intel # For Intel CPUs

```

### 旧的Intel微指令在启动时产生段错误

旧的Intel微指令可能会在启动时产生这样的段错误：

```
/usr/bin/vmware: line 31: 4941 Segmentation fault "$BINDIR"/vmware-modconfig --appname="VMware Workstation" --icon="vmware-workstation"

```

参阅[Microcode](/index.php/Microcode "Microcode")了解如何更新微指令

### 错误：Guests have incorrect system clocks or are unable to boot: "[...]timeTracker_user.c:234 bugNr=148722"

这是由于在VMware Linux中[不完整的](http://kb.vmware.com/selfservice/microsites/search.do?cmd=displayKC&externalId=1591)对电源管理功能的支持导致的CPU频率的变化（[Intel SpeedStep](https://en.wikipedia.org/wiki/Intel_speedstep "wikipedia:Intel speedstep")和[AMD PowerNow!](https://en.wikipedia.org/wiki/AMD_powernow "wikipedia:AMD powernow")/[Cool'n'Quiet](https://en.wikipedia.org/wiki/Cool%27n%27Quiet "wikipedia:Cool'n'Quiet")）。2012年，随着[linux 3.3-1](https://projects.archlinux.org/svntogit/packages.git/commit/trunk/config.x86_64?h=packages/linux&id=9abe018d91a5d8c3af7523d30b8aa73f86b680be)的发布，最大CPU频率[Performance](/index.php/CPU_frequency_governors "CPU frequency governors")的管理者被动态的*Ondemand*替代。当宿主的CPU频率变化时，客户机的时钟会运行过快或过慢，同时也可能会导致客户机无法启动。

为规避该问题，宿主CPU的最高频率可以被指定，并禁用[时间戳计数器](https://en.wikipedia.org/wiki/Time_Stamp_Counter "wikipedia:Time Stamp Counter")(TSC)。在整体设置中:

 `/etc/vmware/config` 
```
host.cpukHz = "X"  # The maximum speed in KHz, e.g. 3GHz is "3000000".
host.noTSC = "TRUE" # Keep the Guest system clock accurate even when
ptsc.noTSC = "TRUE" # the time stamp counter (TSC) is slow.
```

**提示：** 若要每隔一分钟修正一次时间，在VMware Tools下的*Options*选项卡中，启用: *"Time synchronization between the virtual machine and the host operating system"*.

### Guests系统启动后网络不可用

这可能是 `vmnet` 模块没有加载 [[1]](http://www.linuxquestions.org/questions/slackware-14/could-not-connect-ethernet0-to-virtual-network-dev-vmnet8-796095/)。又见[#Systemd 服务](#Systemd_.E6.9C.8D.E5.8A.A1)自动加载。

### 在Linux 4.9后内核模块无法编译

对于VMware Workstation Pro 12.5.2，模块的源码必须作出修改，以便于在Linux 4.9上编译 [[2]](http://rglinuxtech.com/?p=1847)。

```
# cd /usr/lib/vmware/modules/source
# tar xf vmmon.tar
# mv vmmon.tar vmmon.old.tar
# sed -i 's/uvAddr, numPages, 0, 0/uvAddr, numPages, 0/g' vmmon-only/linux/hostif.c
# tar cf vmmon.tar vmmon-only
# rm -r vmmon-only

```

```
# tar xf vmnet.tar
# mv vmnet.tar vmnet.old.tar
# sed -i 's/addr, 1, 1, 0/addr, 1, 0/g' vmnet-only/userif.c
# tar cf vmnet.tar vmnet-only
# rm -r vmnet-only

```

### 版本号为12.5.4的vmplayer/vmware无法启动

如[[3]](https://bbs.archlinux.org/viewtopic.php?id=224667)中所述，临时的解决方案是将包`libpng`降级至1.6.28-1版本，并将其加入`IgnorePkg`参数以忽略升级（参见[/etc/pacman.conf](/index.php/Pacman#Skip_package_from_being_upgraded "Pacman")）。

更方便的解决方案是令VMware使用系统的zlib而不是它自己的：

```
# cd /usr/lib/vmware/lib/libz.so.1
# mv libz.so.1 libz.so.1.old
# ln -s /usr/lib/libz.so.1 .

```

### 版本号为12.5.3的vmplayer/vmware无法启动

这貌似是文件`/usr/lib/vmware/lib/libstdc++.so.6/libstdc++.so.6`中的问题，`CXXABI_1.3.8`缺失。

如果系统安装了[gcc-libs](https://www.archlinux.org/packages/?name=gcc-libs)或者[gcc-libs-multilib](https://www.archlinux.org/packages/?name=gcc-libs-multilib)，那个库就已经被安装了。因此，直接移除那个出错的文件将使vmplayer使用gcc-libs提供的版本。使用root执行：

```
# mv /usr/lib/vmware/lib/libstdc++.so.6/libstdc++.so.6 /usr/lib/vmware/lib/libstdc++.so.6/libstdc++.so.6.bak

```

同时有另一个解决方案：

```
# export VMWARE_USE_SHIPPED_LIBS='yes'

```

### vmware 12的进程在启动之后立即终止，没有显示GUI

这是[Mageia](https://bugs.mageia.org/show_bug.cgi?id=9739)中已知的Bug，但是对于Arch，终端里似乎并没有任何错误信息输出。检阅位于`/tmp/vmware-<id>`里的日志文件，会发现启动vmware或vmplaer后，产生了`VMWARE_SHIPPED_LIBS_LIST is not set`, `VMWARE_SYSTEM_LIBS_LIST is not set`, `VMWARE_USE_SHIPPED_LIBS is not set`, `VMWARE_USE_SYSTEM_LIBS is not set`问题。进程在`Unable to execute /usr/lib/vmware/bin/vmware-modconfig.`后结束。解决方案是，以root身份执行：

```
# mv /etc/vmware/icu/icudt44l.dat /etc/vmware/icu/icudt44l.dat.bak

```

同时有另一个解决方案：

```
# export VMWARE_USE_SHIPPED_LIBS='yes'

```

### VMware模块在Linux内核4.11+上（在GCC7下）编译失败

运行vmware-modconfig时返回：

```
Failed to get gcc information.

```

详细的错误信息能在日志中被找到：

```
modconfig| I125: Got gcc version "6.3.1".
modconfig| I125: GCC major version 6 does not match Kernel GCC major version 7.
modconfig| I125: The GCC compiler "/sbin/gcc" cannot be used for the target kernel.

```

为跳过检查，使用下面的解决方案：

```
# sed 's/gcc version 7/gcc version 6/' /proc/version > /tmp/version
# mount --bind /tmp/version /proc/version
# vmware-modconfig --console --install-all
# umount /proc/version && rm /tmp/version

```

## 卸载

为卸载VMware你首先需要知道产品名称(`vmware-workstation` 或是 `vmware-player`)。列出所有的产品：

```
# vmware-installer -l

```

然后通过下面的指令卸载(使用`--required`跳过所有的确认):

```
# vmware-installer -u *product* --required

```

**提示：** 加上`--console`来使用终端UI

记得要[disable](/index.php/Disable "Disable")和删除`.service`文件:

```
# rm /etc/systemd/system/vmware.service
# rm /etc/systemd/system/vmware-usbarbitrator.service

```

你可能还需要清理在`/usr/lib/modules/*kernel_name*/misc/`下的冗余文件。