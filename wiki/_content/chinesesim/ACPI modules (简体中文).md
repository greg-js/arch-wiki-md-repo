## Contents

*   [1 简介](#.E7.AE.80.E4.BB.8B)
*   [2 目前有哪些模块?](#.E7.9B.AE.E5.89.8D.E6.9C.89.E5.93.AA.E4.BA.9B.E6.A8.A1.E5.9D.97.3F)
*   [3 如何选择正确的模块](#.E5.A6.82.E4.BD.95.E9.80.89.E6.8B.A9.E6.AD.A3.E7.A1.AE.E7.9A.84.E6.A8.A1.E5.9D.97)
*   [4 问题解决](#.E9.97.AE.E9.A2.98.E8.A7.A3.E5.86.B3)
    *   [4.1 DSDT 修正](#DSDT_.E4.BF.AE.E6.AD.A3)
    *   [4.2 笔记本 ACPI 修正](#.E7.AC.94.E8.AE.B0.E6.9C.AC_ACPI_.E4.BF.AE.E6.AD.A3)

## 简介

从 kernel 2.6.20.7 开始，acpi 模块化了, 以避免一些机器上面产生的 acpi 的问题。

本文是对内核的 acpi 模块的一个简单介绍，这些模块可以激活一些特别的 acpi 函数或者添加一些信息到 /proc 下面，以使得 acpid 或者其他监视程序可以处理 acpi 事件。

## 目前有哪些模块?

*   ac (电源连接情况) => 在启动的时候由 initscripts-0.8-7 自动加载
*   asus_acpi (使用asus/medion 笔记本电脑的时候有用)
*   battery (电池状态) => 在启动的时候由 initscripts-0.8-7 自动加载
*   bay (bay status)
*   button (捕获按键事件，比如合上显示器或者按下电源按钮) => 在启动的时候由 initscripts-0.8-7 自动加载
*   container (container status)
*   dock (docking station status) 有些笔记本可以在下面附加一个dock来提供一些额外的功能，比如sony、dell的很多笔记本都有这个接口。
*   fan (风扇状态) => 在启动的时候由 initscripts-0.8-7 自动加载
*   hotkey (笔记本电脑的热键)
*   i2c_ec (EC SMBUs 驱动)
*   ibm_acpi (使用ibm笔记本电脑的时候有用)(2.6.22后是thinkpad_acpi)
*   processor (CPU处理器状态) => 集成到了 kernel 2.6.20.7-2 中
*   sbs (smart battery status)
*   thermal (status of thermal sensors) => 集成到了 kernel 2.6.20.7-2 中
*   toshiba_acpi (使用toshiba笔记本电脑的时候有用)
*   video (视频设备的状态)

当前正在使用的内核支持的acpi模块列表可以用下面命令查看：

 `# ls -l /usr/lib/modules/$(uname -r)/kernel/drivers/acpi` 

```
total 112
-rw-r--r-- 1 root root  2808 Aug 29 23:58 ac.ko.gz
-rw-r--r-- 1 root root  3021 Aug 29 23:58 acpi_ipmi.ko.gz
-rw-r--r-- 1 root root  3354 Aug 29 23:58 acpi_memhotplug.ko.gz
-rw-r--r-- 1 root root  4628 Aug 29 23:58 acpi_pad.ko.gz
drwxr-xr-x 2 root root  4096 Aug 29 23:59 apei
-rw-r--r-- 1 root root  7120 Aug 29 23:58 battery.ko.gz
-rw-r--r-- 1 root root  3700 Aug 29 23:58 button.ko.gz
-rw-r--r-- 1 root root  2181 Aug 29 23:58 container.ko.gz
-rw-r--r-- 1 root root  1525 Aug 29 23:58 custom_method.ko.gz
-rw-r--r-- 1 root root  1909 Aug 29 23:58 ec_sys.ko.gz
-rw-r--r-- 1 root root  2001 Aug 29 23:58 fan.ko.gz
-rw-r--r-- 1 root root  1532 Aug 29 23:58 hed.ko.gz
-rw-r--r-- 1 root root  3241 Aug 29 23:58 pci_slot.ko.gz
-rw-r--r-- 1 root root 17742 Aug 29 23:58 processor.ko.gz
-rw-r--r-- 1 root root  3073 Aug 29 23:58 sbshc.ko.gz
-rw-r--r-- 1 root root  7098 Aug 29 23:58 sbs.ko.gz
-rw-r--r-- 1 root root  6311 Aug 29 23:58 thermal.ko.gz
-rw-r--r-- 1 root root  8891 Aug 29 23:58 video.ko.gz

```

## 如何选择正确的模块

你只能自己来测试哪个模块在你机器上面能正常工作：

 `# modprobe <yourmodule>` 

然后使用下面命令检查模块是否可用

 `$ dmesg` 
**Tip:** 可以用 grep 进行过滤

```
 $ dmesg | grep acpi
[    0.000000] ACPI: LAPIC (acpi_id[0x00] lapic_id[0x00] enabled)
[    0.000000] ACPI: LAPIC (acpi_id[0x01] lapic_id[0x04] enabled)
[    0.000000] ACPI: LAPIC (acpi_id[0x02] lapic_id[0x01] enabled)
[    0.000000] ACPI: LAPIC (acpi_id[0x03] lapic_id[0x05] enabled)
[    0.000000] ACPI: LAPIC_NMI (acpi_id[0x00] high edge lint[0x1])
[    0.000000] ACPI: LAPIC_NMI (acpi_id[0x01] high edge lint[0x1])
[    0.000000] ACPI: LAPIC_NMI (acpi_id[0x02] high edge lint[0x1])
[    0.000000] ACPI: LAPIC_NMI (acpi_id[0x03] high edge lint[0x1])
[    5.066752] ACPI: acpi_idle yielding to intel_idle
[    5.438998] acpi device:04: registered as cooling_device4

```

把需要的模块按照 man modules-load.d 加入配置文件`/etc/modules-load.d`.

## 问题解决

### DSDT 修正

如果装入模块后电源管理问题仍然存在，可能是 Linux 兼容性较差的[DSDT](http://en.wikipedia.org/wiki/DSDT#ACPI_Tables)导致。请参阅[DSDT](/index.php/DSDT "DSDT")Wiki 文档。

### 笔记本 ACPI 修正

如果遇到 ACPI: EC: input buffer is not empty, aborting transaction。 可能是 acpi 模块导致。有两个解决方法：

1\. "简单" 在 GRUB 的 menu.lst 或者 grub.cfg 中的内核行加入 acpi=off，这将禁用所有 acpi 功能，包括电池充电。

2\. "难" 用 [bugs.launchpad.net](https://bugs.launchpad.net/ubuntu/+source/linux/+bug/578506) 中的补丁重新编译内核。