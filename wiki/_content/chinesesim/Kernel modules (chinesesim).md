**翻译状态：** 本文是英文页面 [Kernel_modules](/index.php/Kernel_modules "Kernel modules") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2013-07-06，点击[这里](https://wiki.archlinux.org/index.php?title=Kernel_modules&diff=0&oldid=264846)可以查看翻译后英文页面的改动。

[内核模块](https://en.wikipedia.org/wiki/Loadable_kernel_module "wikipedia:Loadable kernel module")是可以按需加载或卸载的内核代码，可以不重启系统就扩充内核的功能。

## Contents

*   [1 概览](#.E6.A6.82.E8.A7.88)
*   [2 获取信息](#.E8.8E.B7.E5.8F.96.E4.BF.A1.E6.81.AF)
*   [3 手动加载卸载](#.E6.89.8B.E5.8A.A8.E5.8A.A0.E8.BD.BD.E5.8D.B8.E8.BD.BD)
*   [4 配置](#.E9.85.8D.E7.BD.AE)
    *   [4.1 开机加载](#.E5.BC.80.E6.9C.BA.E5.8A.A0.E8.BD.BD)
    *   [4.2 配置内核模块参数](#.E9.85.8D.E7.BD.AE.E5.86.85.E6.A0.B8.E6.A8.A1.E5.9D.97.E5.8F.82.E6.95.B0)
    *   [4.3 使用 /etc/modprobe.d/中的文件](#.E4.BD.BF.E7.94.A8_.2Fetc.2Fmodprobe.d.2F.E4.B8.AD.E7.9A.84.E6.96.87.E4.BB.B6)
    *   [4.4 使用内核命令行](#.E4.BD.BF.E7.94.A8.E5.86.85.E6.A0.B8.E5.91.BD.E4.BB.A4.E8.A1.8C)
*   [5 别名](#.E5.88.AB.E5.90.8D)
*   [6 黑名单](#.E9.BB.91.E5.90.8D.E5.8D.95)
    *   [6.1 禁用内核模块](#.E7.A6.81.E7.94.A8.E5.86.85.E6.A0.B8.E6.A8.A1.E5.9D.97)
    *   [6.2 使用 /etc/modprobe.d/ 中的文件](#.E4.BD.BF.E7.94.A8_.2Fetc.2Fmodprobe.d.2F_.E4.B8.AD.E7.9A.84.E6.96.87.E4.BB.B6)
    *   [6.3 使用内核命令行](#.E4.BD.BF.E7.94.A8.E5.86.85.E6.A0.B8.E5.91.BD.E4.BB.A4.E8.A1.8C_2)
*   [7 技巧](#.E6.8A.80.E5.B7.A7)
    *   [7.1 显示所有内核参数的脚本](#.E6.98.BE.E7.A4.BA.E6.89.80.E6.9C.89.E5.86.85.E6.A0.B8.E5.8F.82.E6.95.B0.E7.9A.84.E8.84.9A.E6.9C.AC)
*   [8 参见](#.E5.8F.82.E8.A7.81)

## 概览

要创建内核模块，请阅读[此指南](http://tldp.org/LDP/lkmpg/2.6/html/index.html)。模块可以设置成内置或者动态加载，要编译成可动态加载，需要在内核配置时将模块配置为 `M` (模块)。

模块保存在 `/lib/modules/*kernel_release*` (使用 `uname -r` 命令显示当前内核版本)。

**注意:** 模块名通常使用 (`_`) 或 `-` 连接，但是这些符号在 `modprobe` 命令和 `/etc/modprobe.d/` 配置文件中都是可以相互替换的。

## 获取信息

显示当前装入的内核模块：

```
$ lsmod

```

显示模块信息：

```
$ modinfo *module_name*

```

显示所有模块的配置信息：

```
$ modprobe -c | less

```

显示某个模块的配置信息：

```
$ modprobe -c | grep *module_name*

```

显示一个装入模块使用的选项：

```
$ systool -v -m *module_name*

```

显示模块的依赖关系：

```
$ modprobe --show-depends *module_name*

```

## 手动加载卸载

控制内核模块载入/移除的命令是[kmod](https://www.archlinux.org/packages/?name=kmod) 软件包提供的, 要手动装入模块的话，执行:

```
# modprobe *module_name*

```

如果要移除一个模块：

```
# modprobe -r *module_name*

```

或者:

```
# rmmod *module_name*

```

## 配置

目前，所有必要模块的加载均由 [udev](/index.php/Udev "Udev") 自动完成。所以，如果不需要使用任何额外的模块，就没有必要在任何配置文件中添加启动时加载的模块。但是，有些情况下可能需要在系统启动时加载某个额外的模块，或者将某个模块列入黑名单以便使系统正常运行。

### 开机加载

systemd 读取 `/etc/modules-load.d/` 中的配置加载额外的内核模块。配置文件名称通常为 `/etc/modules-load.d/<program>.conf`。格式很简单，一行一个要读取的模块名，而空行以及第一个非空格字符为`#`或`;`的行会被忽略，如：

 `/etc/modules-load.d/virtio-net.conf` 
```
# Load virtio-net.ko at boot
virtio-net
```

另见`man 5 modules-load.d`。

### 配置内核模块参数

### 使用 /etc/modprobe.d/中的文件

要通过配置文件传递参数，在 `/etc/modprobe.d/` 中放入任意名称 `.conf` 文件，加入:

 `/etc/modprobe.d/myfilename.conf`  `options modname parametername=parametercontents` 

例如

 `/etc/modprobe.d/thinkfan.conf` 
```
# On thinkpads, this lets the thinkfan daemon control fan speed
options thinkpad_acpi fan_control=1
```

**注意:** 如果要在启动时就修改内核参数(从 init ramdisk 开始)，需要将相应的`.conf`-文件加入 [mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf") 的 FILES 参数中。

### 使用内核命令行

如果模块直接编译进内核，也可以通过启动管理器([GRUB](/index.php/GRUB "GRUB"), [LILO](/index.php/LILO "LILO") 或 [Syslinux](/index.php/Syslinux "Syslinux"))的内核行加入参数：

```
modname.parametername=parametercontents

```

例如:

```
thinkpad_acpi.fan_control=1

```

## 别名

 `/etc/modprobe.d/myalias.conf` 
```
# Lets you use 'mymod' in MODULES, instead of 'really_long_module_name'
alias mymod really_long_module_name
```

有些模块具有别名，以方便其它程序自动装入模块。禁用这些别名可以阻止自动装入，但是仍然可以手动装入。

 `/etc/modprobe.d/modprobe.conf` 
```
# Prevent autoload of bluetooth
alias net-pf-31 off

# Prevent autoload of ipv6
alias net-pf-10 off
```

## 黑名单

### 禁用内核模块

对内核模块来说，黑名单是指禁止某个模块装入的机制。当对应的硬件不存在或者装入某个模块会导致问题时很有用。

有些模块作为 [initramfs](/index.php/Initramfs "Initramfs") 的一部分装入。

`mkinitcpio -M` 会显示所有自动检测到到模块：要阻止 initramfs 装入某些模块，可以在 `/etc/modprobe.d/modprobe.conf` 中将它们加入黑名单。

运行 `mkinitcpio -v` 会显示各种钩子(例如 filesystem 钩子, SCSI 钩子等)装入的模块。如果要禁用这些模块，记得在配置完成后,将`.conf`文件加入`/etc/mkinitcpio.conf` 的 FILES 部分，然后重新生成 initramfs。

### 使用 /etc/modprobe.d/ 中的文件

在 `/etc/modprobe.d/` 中创建 `.conf` 文件，使用 `blacklist` 关键字屏蔽不需要的模块，例如如果不想装入 `pcspkr` 模块：

 `/etc/modprobe.d/nobeep.conf` 
```
# Do not load the pcspkr module on boot
blacklist pcspkr
```

**注意:** `blacklist` 命令将屏蔽一个模板，所以不会自动装入，但是如果其它非屏蔽模块需要这个模块，系统依然会装入它。

要避免这个行为，可以让 modprobe 使用自定义的 `install` 命令，直接返回导入失败：

 `/etc/modprobe.d/blacklist.conf` 
```
...
install MODULE /bin/false
...
```

这样就可以 "屏蔽" 模块及所有依赖它的模块。

### 使用内核命令行

同样可以通过内核命令行(位于 [GRUB](/index.php/GRUB "GRUB")、[LILO](/index.php/LILO "LILO") 或 [Syslinux](/index.php/Syslinux "Syslinux"))禁用模块：

```
modprobe.blacklist=modname1,modname2,modname3

```

当某个模块导致系统无法启动时，可以使用此方法禁用模块。

参阅[Kernel parameters](/index.php/Kernel_parameters "Kernel parameters").

## 技巧

### 显示所有内核参数的脚本

下面的 bash 脚本可以显示当前装入模块、模块参数及当前参数的数值。它使用 `/proc/modules` 获取当前装入模块的列表，然后用 modinfo 获取模块的描述和模块的参数，最后访问 sysfs 文件系统获得当前模块名和参数值。

```
function aa_mod_parameters () 
{ 
    N=/dev/null;
    C=`tput op` O=$(echo -en "
`tput setaf 2`>>> `tput op`");
    for mod in $(cat /proc/modules|cut -d" " -f1);
    do
        md=/sys/module/$mod/parameters;
        [[ ! -d $md ]] && continue;
        m=$mod;
        d=`modinfo -d $m 2>$N | tr "
" "\t"`;
        echo -en "$O$m$C";
        [[ ${#d} -gt 0 ]] && echo -n " - $d";
        echo;
        for mc in $(cd $md; echo *);
        do
            de=`modinfo -p $mod 2>$N | grep ^$mc 2>$N|sed "s/^$mc=//" 2>$N`;
            echo -en "\t$mc=`cat $md/$mc 2>$N`";
            [[ ${#de} -gt 1 ]] && echo -en " - $de";
            echo;
        done;
    done
}
```

示例输出：

 `# aa_mod_parameters` 
```
>>> ehci_hcd - USB 2.0 'Enhanced' Host Controller (EHCI) Driver
        hird=0 - hird:host initiated resume duration, +1 for each 75us (int)
        ignore_oc=N - ignore_oc:ignore bogus hardware overcurrent indications (bool)
        log2_irq_thresh=0 - log2_irq_thresh:log2 IRQ latency, 1-64 microframes (int)
        park=0 - park:park setting; 1-3 back-to-back async packets (uint)

>>> processor - ACPI Processor Driver
        ignore_ppc=-1 - ignore_ppc:If the frequency of your machine gets wronglylimited by BIOS, this should help (int)
        ignore_tpc=0 - ignore_tpc:Disable broken BIOS _TPC throttling support (int)
        latency_factor=2 - latency_factor: (uint)

>>> usb_storage - USB Mass Storage driver for Linux
        delay_use=1 - delay_use:seconds to delay before using a new device (uint)
        option_zero_cd=1 - option_zero_cd:ZeroCD mode (1=Force Modem (default), 2=Allow CD-Rom (uint)
        quirks= - quirks:supplemental list of device IDs and their quirks (string)
        swi_tru_install=1 - swi_tru_install:TRU-Install mode (1=Full Logic (def), 2=Force CD-Rom, 3=Force Modem) (uint)

>>> video - ACPI Video Driver
        allow_duplicates=N - allow_duplicates: (bool)
        brightness_switch_enabled=Y - brightness_switch_enabled: (bool)
        use_bios_initial_backlight=Y - use_bios_initial_backlight: (bool)
```

## 参见

*   [http://linuxmanpages.com/man5/modprobe.conf.5.php](http://linuxmanpages.com/man5/modprobe.conf.5.php)
*   [禁用 IPv6](/index.php/Disabling_IPv6_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Disabling IPv6 (简体中文)")
*   [禁用 PC喇叭](/index.php/Disable_PC_speaker_beep_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Disable PC speaker beep (简体中文)")