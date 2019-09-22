相关文章

*   [Boot Debugging](/index.php/Boot_Debugging "Boot Debugging")
*   [Kernels (简体中文)](/index.php/Kernels_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Kernels (简体中文)")
*   [Kernel parameters (简体中文)](/index.php/Kernel_parameters_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Kernel parameters (简体中文)")

**翻译状态：** 本文是英文页面 [Kernel_modules](/index.php/Kernel_modules "Kernel modules") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2018-05-09，点击[这里](https://wiki.archlinux.org/index.php?title=Kernel_modules&diff=0&oldid=515813)可以查看翻译后英文页面的改动。

[内核模块](https://en.wikipedia.org/wiki/Loadable_kernel_module "wikipedia:Loadable kernel module")是可以按需加载或卸载的内核代码，可以不重启系统就扩充内核的功能。

要创建内核模块，请阅读[此指南](http://tldp.org/LDP/lkmpg/2.6/html/index.html)。模块可以设置成内置或者动态加载，要编译成可动态加载，需要在内核配置时将模块配置为 `M` (模块)。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 获取信息](#获取信息)
*   [2 自动处理](#自动处理)
*   [3 手动加载卸载](#手动加载卸载)
*   [4 配置模块参数](#配置模块参数)
    *   [4.1 手动加载时设置](#手动加载时设置)
    *   [4.2 使用 /etc/modprobe.d/中的文件](#使用_/etc/modprobe.d/中的文件)
    *   [4.3 使用内核命令行](#使用内核命令行)
*   [5 别名](#别名)
*   [6 黑名单](#黑名单)
    *   [6.1 禁用内核模块](#禁用内核模块)
    *   [6.2 使用 /etc/modprobe.d/ 中的文件](#使用_/etc/modprobe.d/_中的文件)
    *   [6.3 使用内核命令行](#使用内核命令行_2)
*   [7 问题处理](#问题处理)
    *   [7.1 模块未加载](#模块未加载)
*   [8 参见](#参见)

## 获取信息

模块保存在 `/lib/modules/*kernel_release*` (使用 `uname -r` 命令显示当前内核版本)。

**注意:** 模块名通常使用 (`_`) 或 `-` 连接，但是这些符号在 `modprobe` 命令和 `/etc/modprobe.d/` 配置文件中都是可以相互替换的。

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

## 自动处理

目前，所有必要模块的加载均由 [udev](/index.php/Udev "Udev") 自动完成。所以，如果不需要使用任何额外的模块，就没有必要在任何配置文件中添加启动时加载的模块。但是，有些情况下可能需要在系统启动时加载某个额外的模块，或者将某个模块列入黑名单以便使系统正常运行。

systemd 读取 `/etc/modules-load.d/` 中的配置加载额外的内核模块。配置文件名称通常为 `/etc/modules-load.d/<program>.conf`。格式很简单，一行一个要读取的模块名，而空行以及第一个非空格字符为`#`或`;`的行会被忽略，如：

 `/etc/modules-load.d/virtio-net.conf` 
```
# Load virtio-net.ko at boot
virtio-net
```

另见[modules-load.d(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/modules-load.d.5)。

## 手动加载卸载

控制内核模块载入/移除的命令是[kmod](https://www.archlinux.org/packages/?name=kmod) 软件包提供的, 要手动装入模块的话，执行:

```
# modprobe *module_name*

```

按文件名加载模块:

```
# insmod filename [args]

```

**Note:** 如果升级了内核但是没有重启，路径 `/usr/lib/modules/$(uname -r)/` 已经不存在。*modprobe* 会返回错误 1，没有额外的错误信息。如果出现 modprobe 加载失败，请检查模块路径以确认是否是这个问题导致。

如果要移除一个模块：

```
# modprobe -r *module_name*

```

或者:

```
# rmmod *module_name*

```

## 配置模块参数

### 手动加载时设置

传递参数的基本方式是使用 modprobe 选项，格式是 `*key=value*`：

```
# modprobe *module_name parameter_name=parameter_value*

```

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

## 问题处理

### 模块未加载

如果出现模块在启动时未加载，而且启动日志中(`journalctl -b`) 显示模块被屏蔽，但是 `/etc/modprobe.d/` 中未找到屏蔽设置，请检查 `/usr/lib/modprobe.d/` 目录。

"vermagic" 字符串与内核不一致的模块不会被加载，如果确认模块与当前内核兼容，可以用 `modprobe --force-vermagic` 参数加载，跳过检查。

**警告:** 忽略模块检查，可能因为不兼容导致系统崩溃或不可预知行为，请谨慎使用 `--force-vermagic`。

## 参见

*   [http://linuxmanpages.com/man5/modprobe.conf.5.php](http://linuxmanpages.com/man5/modprobe.conf.5.php)
*   [禁用 IPv6](/index.php/Disabling_IPv6_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Disabling IPv6 (简体中文)")
*   [禁用 PC喇叭](/index.php/Disable_PC_speaker_beep_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Disable PC speaker beep (简体中文)")