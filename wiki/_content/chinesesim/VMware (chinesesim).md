本文是关于在 Arch 中安装 VMware，你也许想寻找的是 [在 VMware 中安装 Arch Linux](/index.php/Installing_Arch_Linux_in_VMware_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Installing Arch Linux in VMware (简体中文)")

**注意:**

*   这篇文章时针对最新的VMware正式版,即VMware Workstation Pro 和Player 12.
*   而对于旧版本,可以使用[vmware-patch](https://aur.archlinux.org/packages/vmware-patch/)包

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
    *   [2.1 VMware module模块补丁和安装](#VMware_module.E6.A8.A1.E5.9D.97.E8.A1.A5.E4.B8.81.E5.92.8C.E5.AE.89.E8.A3.85)
    *   [2.2 Systemd 服务](#Systemd_.E6.9C.8D.E5.8A.A1)
*   [3 启动程序](#.E5.90.AF.E5.8A.A8.E7.A8.8B.E5.BA.8F)
*   [4 提示和技巧](#.E6.8F.90.E7.A4.BA.E5.92.8C.E6.8A.80.E5.B7.A7)
    *   [4.1 输入Workstation Pro许可密钥](#.E8.BE.93.E5.85.A5Workstation_Pro.E8.AE.B8.E5.8F.AF.E5.AF.86.E9.92.A5)
        *   [4.1.1 从终端](#.E4.BB.8E.E7.BB.88.E7.AB.AF)
        *   [4.1.2 从 GUI](#.E4.BB.8E_GUI)
    *   [4.2 解压缩 VMware BIOS](#.E8.A7.A3.E5.8E.8B.E7.BC.A9_VMware_BIOS)
    *   [4.3 Extracting the installer](#Extracting_the_installer)
        *   [4.3.1 使用修改过的 BIOS](#.E4.BD.BF.E7.94.A8.E4.BF.AE.E6.94.B9.E8.BF.87.E7.9A.84_BIOS)
    *   [4.4 写时复制 (CoW)](#.E5.86.99.E6.97.B6.E5.A4.8D.E5.88.B6_.28CoW.29)
    *   [4.5 使用 DKMS 管理模块](#.E4.BD.BF.E7.94.A8_DKMS_.E7.AE.A1.E7.90.86.E6.A8.A1.E5.9D.97)
        *   [4.5.1 准备](#.E5.87.86.E5.A4.87)
        *   [4.5.2 Build configuration](#Build_configuration)
            *   [4.5.2.1 1) 使用 Git](#1.29_.E4.BD.BF.E7.94.A8_Git)
            *   [4.5.2.2 2) 手动安装](#2.29_.E6.89.8B.E5.8A.A8.E5.AE.89.E8.A3.85)
        *   [4.5.3 安装](#.E5.AE.89.E8.A3.85_2)
    *   [4.6 Enable 3D graphics on Intel and Optimus](#Enable_3D_graphics_on_Intel_and_Optimus)
*   [5 疑难解答](#.E7.96.91.E9.9A.BE.E8.A7.A3.E7.AD.94)
    *   [5.1 /dev/vmmon not found](#.2Fdev.2Fvmmon_not_found)
    *   [5.2 Kernel headers for version 4.x-xxxx were not found. If you installed them[...]](#Kernel_headers_for_version_4.x-xxxx_were_not_found._If_you_installed_them.5B....5D)
    *   [5.3 无法识别 USB 设备](#.E6.97.A0.E6.B3.95.E8.AF.86.E5.88.AB_USB_.E8.AE.BE.E5.A4.87)
    *   [5.4 The installer fails to start](#The_installer_fails_to_start)
    *   [5.5 无法为Guests下载VMware Tools](#.E6.97.A0.E6.B3.95.E4.B8.BAGuests.E4.B8.8B.E8.BD.BDVMware_Tools)
    *   [5.6 Incorrect login/password when trying to access VMware remotely](#Incorrect_login.2Fpassword_when_trying_to_access_VMware_remotely)
    *   [5.7 Issues with ALSA output](#Issues_with_ALSA_output)
    *   [5.8 Kernel-based Virtual Machine (KVM) is running](#Kernel-based_Virtual_Machine_.28KVM.29_is_running)
    *   [5.9 Segmentation fault at startup due to old Intel microcode](#Segmentation_fault_at_startup_due_to_old_Intel_microcode)
    *   [5.10 Guests have incorrect system clocks or are unable to boot: "[...]timeTracker_user.c:234 bugNr=148722"](#Guests_have_incorrect_system_clocks_or_are_unable_to_boot:_.22.5B....5DtimeTracker_user.c:234_bugNr.3D148722.22)
    *   [5.11 Guests系统启动后网络不可用](#Guests.E7.B3.BB.E7.BB.9F.E5.90.AF.E5.8A.A8.E5.90.8E.E7.BD.91.E7.BB.9C.E4.B8.8D.E5.8F.AF.E7.94.A8)
*   [6 卸载](#.E5.8D.B8.E8.BD.BD)

## 安装

[安装](/index.php/Pacman "Pacman") 依赖项:

*   [fuse](https://www.archlinux.org/packages/?name=fuse) - the `vmware-vmblock-fuse` service is [favored](https://www.mail-archive.com/open-vm-tools-devel@lists.sourceforge.net/msg00213.html) over the `vmblock` module, which is not built anymore without disabling [fuse](http://cateee.net/lkddb/web-lkddb/FUSE_FS.html) in the kernel
*   [gtkmm](https://www.archlinux.org/packages/?name=gtkmm) - for the GUI
*   [linux-headers](https://www.archlinux.org/packages/?name=linux-headers) - 作为模块编译
*   [ncurses5-compat-libs](https://aur.archlinux.org/packages/ncurses5-compat-libs/) - needed by at least the installer

下载最新的[VMware Workstation Pro](https://www.vmware.com/go/tryworkstation)或[Player](https://www.vmware.com/go/downloadplayer) (或者[beta](https://communities.vmware.com/community/vmtn/beta)版本,当可用时).

开始安装：

```
# sh VMware-edition-version.release.architecture.bundle

```

**提示：** Some other useful flags:

*   `--eulas-agreed` - Skip the EULAs
*   `--console` - Use the console UI.
*   `-I`, `--ignore-errors` - Ignore fatal errors.
*   `--set-setting vmware-workstation serialNumber XXXXX-XXXXX-XXXXX-XXXXX-XXXXX` - Set the serial number during install (good for scripted installs).
*   `--required` - Only ask mandatory questions (results in silent install when combined with `--eulas-agreed` and `--console`).

将`System service scripts directory`设置为`/etc/init.d` (默认值)

**注意:** 安装过程中会收到`"No rc*.d style init script directories"`错误。这可以安全忽略,因为Arch使用的是[systemd](/index.php/Systemd "Systemd").

**提示：** 从终端上(重新)构建模块，使用:
```
# vmware-modconfig --console --install-all

```

## 配置

**提示：** [AUR](/index.php/Arch_User_Repository "Arch User Repository") 中也包含了一个叫做 [vmware-patch](https://aur.archlinux.org/packages/vmware-patch/) 的软件包会自动完成本节内容(它同时支持旧版本的 VMware )。

### VMware module模块补丁和安装

**注意:** Due to Workstation 12 taking advantage of the [mainlined](http://www.phoronix.com/scan.php?page=news_item&px=MTI3MTE) kernel modules, patching the VMCI/VSOCK sources is no longer required.

VMware Workstation 12 支持内核 4.2.

### Systemd 服务

”(可选)“ 你也可以创建一个 `.service` 文件 (也可以用[AUR](/index.php/AUR "AUR")中的[vmware-systemd-services](https://aur.archlinux.org/packages/vmware-systemd-services/)包)，而不是直接使用 `/etc/init.d/vmware` (`start|stop|status|restart`) and `/usr/bin/vmware-usbarbitrator` 来管理服务：

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

之后您就可以在启动时[enable](/index.php/Enable "Enable")它们.

## 启动程序

启动VMware Workstation Pro:

```
$ vmware

```

或VMware Player (Pro):

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

### Extracting the installer

To view the contents of the installer `.bundle`:

```
$ sh VMware-*edition*-*version*.*release*.*architecture*.bundle --extract */tmp/vmware-bundle/*

```

#### 使用修改过的 BIOS

If and when you decide to modify the extracted BIOS you can make your virtual machine use it by moving it to `~/vmware/<Virtual machine name>`:

```
$ mv bios440.rom ~/vmware/<Virtual machine name>/

```

然后在 `<Virtual machine name>.vmx` 文件中加入：

 `~/vmware/<Virtual machine name>/<Virtual machine name>.vmx`  `bios440.filename = "bios440.rom"` 

### 写时复制 (CoW)

CoW comes with some advantages, but can negatively affect performance with large files that have small random writes (例如数据库文件和虚拟机镜像)：

```
$ chattr +C ~/vmware/<Virtual machine name>/<Virtual machine name>.vmx

```

**Note:** From the [chattr man page](http://www.linuxhowtos.org/manpages/1/chattr.htm?print=-51): *"For btrfs, the `C` flag should be set only on new or empty files. If set on a file which already has data blocks, it is undefined when the blocks assigned to the file will be fully stable. If set on a directory, only new files will be affected."*

### 使用 DKMS 管理模块

The Dynamic Kernel Module Support (DKMS) can be used to manage Workstation modules and to void from re-running `vmware-modconfig` each time the kernel changes. The following example uses a custom `Makefile` to compile and install the modules through `vmware-modconfig`. Afterwards they are removed from the current kernel tree.

#### 准备

首先从 [Community repository](/index.php/Community_repository "Community repository") 安装 [dkms](https://www.archlinux.org/packages/?name=dkms)：

```
# pacman -S dkms

```

然后为 `Makefile` 和 `dkms.conf` 创建源目录：

```
# mkdir /usr/src/vmware-modules-11/

```

#### Build configuration

Fetch the files from Git or use the ones below.

##### 1) 使用 Git

```
$ cd /tmp
$ git clone [git://github.com/bawaaaaah/dkms-workstation.git](git://github.com/bawaaaaah/dkms-workstation.git)
$ sed -i 's/9/11/' dkms-workstation/dkms.conf
# cp dkms-workstation/Makefile dkms-workstation/dkms.conf /usr/src/vmware-modules-11/

```

##### 2) 手动安装

The `dkms.conf` describes the module names and the compilation/installation procedure. `AUTOINSTALL="yes"` tells the modules to be recompiled/installed automatically each time:

 `/usr/src/vmware-modules-11/dkms.conf` 
```
PACKAGE_NAME="vmware-modules"
PACKAGE_VERSION="11"

MAKE[0]="make all"
CLEAN="make clean"

BUILT_MODULE_NAME[0]="vmmon"
BUILT_MODULE_LOCATION[0]="modules"

BUILT_MODULE_NAME[1]="vmnet"
BUILT_MODULE_LOCATION[1]="modules"

BUILT_MODULE_NAME[2]="vmblock"
BUILT_MODULE_LOCATION[2]="modules"

BUILT_MODULE_NAME[3]="vmci"
BUILT_MODULE_LOCATION[3]="modules"

BUILT_MODULE_NAME[4]="vsock"
BUILT_MODULE_LOCATION[4]="modules"

DEST_MODULE_LOCATION[0]="/extra/vmware"
DEST_MODULE_LOCATION[1]="/extra/vmware"
DEST_MODULE_LOCATION[2]="/extra/vmware"
DEST_MODULE_LOCATION[3]="/extra/vmware"
DEST_MODULE_LOCATION[4]="/extra/vmware"

AUTOINSTALL="yes"
```

and now the `Makefile`:

 `/usr/src/vmware-modules-11/Makefile` 
```
KERNEL := $(KERNELRELEASE)
HEADERS := /usr/lib/modules/$(KERNEL)/build/include
GCC := $(shell vmware-modconfig --console --get-gcc)
DEST := /lib/modules/$(KERNEL)/vmware

TARGETS := vmmon vmnet vmblock vmci vsock

LOCAL_MODULES := $(addsuffix .ko, $(TARGETS))

all: $(LOCAL_MODULES)
	mkdir -p modules/
	mv *.ko modules/
	rm -rf $(DEST)
	depmod

$(HEADERS)/linux/version.h:
	ln -s $(HEADERS)/generated/uapi/linux/version.h $(HEADERS)/linux/version.h

%.ko: $(HEADERS)/linux/version.h
	vmware-modconfig --console --build-mod -k $(KERNEL) $* $(GCC) $(HEADERS) vmware/
	cp -f $(DEST)/$@ .

clean: rm -rf modules/
```

#### 安装

The modules can then be installed with:

```
# dkms install vmware-modules/11 -k $(uname -r)

```

### Enable 3D graphics on Intel and Optimus

Some graphics drivers are blacklisted by default, due to poor and/or unstable 3D acceleration. After enabling *Accelerate 3D graphics*, the log may show something like:

```
Disabling 3D on this host due to presence of Mesa DRI driver.  Set mks.gl.allowBlacklistedDrivers = TRUE to override.

```

This means the following:

 `~/.vmware/preferences`  `mks.gl.allowBlacklistedDrivers = TRUE` 

## 疑难解答

### /dev/vmmon not found

完整的错误是:

```
Could not open /dev/vmmon: No such file or directory.
Please make sure that the kernel module `vmmon' is loaded.

```

这意味着未加载`vmmon`模块.参见[#Systemd 服务](#Systemd_.E6.9C.8D.E5.8A.A1)章节

### Kernel headers for version 4.x-xxxx were not found. If you installed them[...]

安装 [linux-headers](https://www.archlinux.org/packages/?name=linux-headers)。

**Note:** 更新内核和头文件会需要你启动新的内核以匹配头文件的版本。这是一个相对常见的错误。

### 无法识别 USB 设备

**提示：** 可以通过 [vmware-patch](https://aur.archlinux.org/packages/vmware-patch/) 解决。

如果不使用[systemd service](#systemd_services)来处理服务,you need to manually start the `vmware-usbarbitrator` binary as root each time.

启动：

```
# vmware-usbarbitrator

```

停止:

```
# vmware-usbarbitrator --kill

```

### The installer fails to start

If you just get back to the prompt when opening the `.bundle`, then you probably have a deprecated or broken version of the VMware installer and you should remove it (you may also refer to the [uninstallation](#Uninstallation) section of this article):

```
# rm -r /etc/vmware-installer

```

### 无法为Guests下载VMware Tools

If after [#Preventing crashes and freezes when checking for updates](#Preventing_crashes_and_freezes_when_checking_for_updates) you are still unable to download the VMware Tools ISOs, you may either try running `vmware` or `vmplayer` as *root*, or downloading them directly from the [VMware repository](http://softwareupdate.vmware.com/cds/vmw-desktop/).

Navigate to: "*application name* / *version* / *build ID* / linux / packages/" and download the appropriate Tools.

Extract with:

```
$ tar -xvf vmware-tools-*name*-*version*-*buildID*.x86_64.component.tar

```

And install using the VMware installer:

```
# vmware-installer --install-component=*/path/*vmware-tools-*name*-*version*-*buildID*.x86_64.component

```

### Incorrect login/password when trying to access VMware remotely

VMware Workstation 9 provides the possibility to remotely manage Shared VMs through the `vmware-workstation-server` service. However, this will fail with the error `"incorrect username/password"` due to incorrect PAM configuration of the `vmware-authd` service. To fix it, edit `/etc/pam.d/vmware-authd` like this:

 `/etc/pam.d/vmware-authd` 
```
#%PAM-1.0
auth     required       pam_unix.so
account  required       pam_unix.so
password required       pam_permit.so
session  required       pam_unix.so

```

and restart VMware services with:

```
# systemctl restart vmware

```

Now you can connect to the server with the credentials provided during the installation.

**Note:** [libxslt](https://www.archlinux.org/packages/?name=libxslt) may be required for starting virtual machines.

### Issues with ALSA output

[To fix](http://bankimbhavsar.blogspot.co.nz/2011/09/hd-audio-in-vmware-fusion-4-and-vmware.html) sound quality issues or enabling proper HD audio output, first run:

```
$ aplay -L

```

If interested in playing 5.1 *surround sound* from the guest, look for `surround51:CARD=*vendor_name*,DEV=*num*`, if experiencing quality issues, look for `front:CARD=*vendor_name*,DEV=*num*`. Finally put the name in the `.vmx`:

 `~/vmware/*Virtual_machine_name*/*Virtual_machine_name*.vmx` 
```
sound.fileName=*"surround51:CARD=Live,DEV=0"*
sound.autodetect=*"FALSE"*
```

[OSS emulation](/index.php/Advanced_Linux_Sound_Architecture#User-space_utilities "Advanced Linux Sound Architecture") should also be disabled.

### Kernel-based Virtual Machine (KVM) is running

To disable `KVM` on boot, you can use something like:

 `/etc/modprobe.d/vmware.conf` 
```
blacklist kvm
blacklist kvm-amd   # For AMD CPUs
blacklist kvm-intel # For Intel CPUs

```

### Segmentation fault at startup due to old Intel microcode

Old Intel microcode may result in the following kind of segmentation fault at startup:

```
/usr/bin/vmware: line 31: 4941 Segmentation fault "$BINDIR"/vmware-modconfig --appname="VMware Workstation" --icon="vmware-workstation"

```

[Install](/index.php/Install "Install") [intel-ucode](https://www.archlinux.org/packages/?name=intel-ucode) and make `/boot/intel-ucode.img` to be loaded by the [bootloader](/index.php/Bootloader "Bootloader").

See [Microcode](/index.php/Microcode "Microcode") for more information.

### Guests have incorrect system clocks or are unable to boot: "[...]timeTracker_user.c:234 bugNr=148722"

This is due to [incomplete](http://kb.vmware.com/selfservice/microsites/search.do?cmd=displayKC&externalId=1591) support of power management features ([Intel SpeedStep](https://en.wikipedia.org/wiki/Intel_speedstep "wikipedia:Intel speedstep") and [AMD PowerNow!](https://en.wikipedia.org/wiki/AMD_powernow "wikipedia:AMD powernow")/[Cool'n'Quiet](https://en.wikipedia.org/wiki/Cool%27n%27Quiet "wikipedia:Cool'n'Quiet")) in VMware Linux that vary the CPU frequency. In March 2012, with the release of [linux 3.3-1](https://projects.archlinux.org/svntogit/packages.git/commit/trunk/config.x86_64?h=packages/linux&id=9abe018d91a5d8c3af7523d30b8aa73f86b680be) the maximum frequency [Performance](/index.php/CPU_frequency_governors "CPU frequency governors") governor was replaced with the dynamic *Ondemand*. When the host CPU frequency changes, the Guest system clock runs too quickly or too slowly, but may also render the whole Guest unbootable.

To prevent this, the maximum host CPU frequency can be specified, and [Time Stamp Counter](https://en.wikipedia.org/wiki/Time_Stamp_Counter "wikipedia:Time Stamp Counter") (TSC) disabled, in the global configuration:

 `/etc/vmware/config` 
```
host.cpukHz = "X"  # The maximum speed in KHz, e.g. 3GHz is "3000000".
host.noTSC = "TRUE" # Keep the Guest system clock accurate even when
ptsc.noTSC = "TRUE" # the time stamp counter (TSC) is slow.
```

**Tip:** To periodically correct the time (once per minute), in the *Options* tab of VMware Tools, enable: *"Time synchronization between the virtual machine and the host operating system"*.

### Guests系统启动后网络不可用

这可能是 `vmnet` 模块没有加载 [[1]](http://www.linuxquestions.org/questions/slackware-14/could-not-connect-ethernet0-to-virtual-network-dev-vmnet8-796095/)。 又见[#systemd services](#systemd_services) 服务自动加载。

## 卸载

To uninstall VMware you need the product name (`vmware-workstation` 或是 `vmware-player`)。列出所有的产品：

```
# vmware-installer -l

```

and uninstall with (`--required` skips the confirmation):

```
# vmware-installer -u *product* --required

```

**Tip:** Use `--console` for the console UI.

记得要[disable](/index.php/Disable "Disable") 和删除`.service`文件:

```
# rm /etc/systemd/system/vmware.service
# rm /etc/systemd/system/vmware-usbarbitrator.service

```

你可能还想看看剩余模块在`/usr/lib/modules/*kernel_name*/misc/`模块目录.