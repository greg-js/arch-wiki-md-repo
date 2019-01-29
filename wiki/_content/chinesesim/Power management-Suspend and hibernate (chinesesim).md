本文参照[Power management/Suspend and hibernate](/index.php/Power_management/Suspend_and_hibernate "Power management/Suspend and hibernate")翻译，但增删部分内容，旨在简要描述挂起、睡眠和休眠的工作原理以及实现方式。

现主要有三种挂起方式：**suspend to RAM**（挂起到内存，睡眠），**suspend to disk**（休眠），和**hybrid suspend**或者**suspend to both**（内存和硬盘都保存一份内容）：

*   **Suspend to RAM**： 将机器中大多数和RAM不相关的部件断电，机器状态仅仅保存在RAM中。建议笔记本用户把系统设置成用电池为省电或合盖时自动进入此模式。

*   **Suspend to disk**： 将机器内容保存至 [swap space交换空间](/index.php?title=Swap_space%E4%BA%A4%E6%8D%A2%E7%A9%BA%E9%97%B4&action=edit&redlink=1 "Swap space交换空间 (page does not exist)") 并完全断电。再次开机时内容恢复。和上一个不同，这个挂起时不会耗电。

*   **Suspend to both**： 将上面两个合在一起。如果没断电，系统就从RAM恢复；反之从硬盘恢复，但速度更慢。

## Contents

*   [1 挂起、睡眠和休眠的区别](#挂起、睡眠和休眠的区别)
*   [2 休眠设置](#休眠设置)
    *   [2.1 开启休眠](#开启休眠)
        *   [2.1.1 划分合适大小的swap分区](#划分合适大小的swap分区)
        *   [2.1.2 在bootloader 中增加resume内核参数](#在bootloader_中增加resume内核参数)
        *   [2.1.3 配置 initramfs的resume钩子](#配置_initramfs的resume钩子)
    *   [2.2 设置低电量休眠](#设置低电量休眠)
    *   [2.3 设置盖上笔记本盖子或按下电源键休眠](#设置盖上笔记本盖子或按下电源键休眠)
*   [3 参看](#参看)

## 挂起、睡眠和休眠的区别

暂停并保存当前系统运行状态（前后台进程服务，不包含buff和cache等）有三种方法：

*   挂起到内存：**suspend to ram**(简称str）

通常被称为**挂起**，设备通电，低功耗。

挂起也被称为暂停或待机，一般的，系统一段时间没有操作，系统就会挂起（到内存中），多数外围设备会关闭，某些设备会运行（如键盘鼠标），可以快速响应这些设备从而唤醒系统。

*   挂起到磁盘：**suspend to disk**(简称std)

通常被称为**休眠**，设备断电，即设备会关机。

休眠也被称为冬眠（hibernate实为冬眠之意），保存运行状态存到硬盘中，然后关机。下次开机后，系统从硬盘中读取存储的数据并恢复到关机前的状态。

*   混合挂起：**suspend to ram and disk**(简称strd)

通常被称为睡眠，设备通电，低功耗。

睡眠更准确的名称应该是混合睡眠，所谓混合即存储方式上包含了挂起和休眠两种方式，唤醒时会优先从内存中读取数据，如果设备在此状态下断电（例如笔记本电脑在睡眠时外部电源断掉，而睡眠一段时间后内部电源耗尽），就和休眠一样了。

## 休眠设置

ArchLiux的休眠功能需要用户设置后才能使用。

这里介绍使用systemd休眠。

### 开启休眠

按照以下步骤设置。

#### 划分合适大小的swap分区

休眠（hibernate）需要将内存中的内容写入磁盘的swap分区，如果swap分区大小比当前休眠所需空间小，则无法保证能够正确地休眠。具体的swap的大小根据个人使用情况（要休眠时的内存占用）而定。

如果 swap 分区过小，需增大swap分区或减小/sys/power/image_size 。

**注意:** brtfs格式无法设置swap分区。

#### 在bootloader 中增加resume内核参数

需要添加resume=/dev/sdxY (sdxY 是swap分区的名字) ，让系统在启动时读取swap分区中的内容。

例如，使用了grub2作为bootloader，swap的分区是/dev/sda3。

1\. 编辑`/etc/default/grub`文件，在GRUB_CMDLINE_LINUX_DEFAULT中添加resume=/dev/sda3 ，假如该行的原有内容是：

```
GRUB_CMDLINE_LINUX_DEFAULT=”quiet intel_pstate=enable”

```

添加resume参数后就是：

```
GRUB_CMDLINE_LINUX_DEFAULT="quiet intel_pstate=enable resume=/dev/sda3"

```

2\. 更新 grub 配置：

```
grub-mkconfig -o /boot/grub/grub.cfg

```

#### 配置 initramfs的resume钩子

1\. 添加resume钩子 编辑`/etc/mkinitcpio.conf`，在HOOKS行中添加resume钩子： 例如该行原有内容是：

```
HOOKS="base udev autodetect modconf block filesystems keyboard fsck"

```

添加resume后就是：

```
HOOKS="base udev resume autodetect modconf block filesystems keyboard fsck"

```

**注意:** 如果使用lvm分区，需要将resume放在lvm后面
使用lvm的示例：
```
HOOKS="base udev autodetect modconf block lvm2 resume filesystems keyboard fsck"

```

2\. 重新生成 initramfs 镜像:

```
mkinitcpio -p linux

```

### 设置低电量休眠

用于带有内置电池的设备。

当电池电量极低时，使其休眠，以免丢失数据。 修改`/etc/UPower/UPower.conf`相关配置.示例，在电量低至%5时自动休眠：

```
PercentageLow=15  #<=15%低电量
PercentageCritical=10  #<=10%警告电量
PercentageAction=5  #<=5%执行动作（即CriticalPowerAction)的电量
CriticalPowerAction=Hibernate #(在本示例中是电量<=5%）执行关机

```

当电池低至5%，设备会自动休眠。

CriticalPowerAction的取值有Poweroff、Hibernate和Hybid-sleep。

更多配置项参考该文件中的说明。

### 设置盖上笔记本盖子或按下电源键休眠

1\. 编辑`/etc/systemd/logind.conf` ， 盖上盖子休眠，添加：

```
HandleLidSwitch=hibernate

```

按下电源键休眠，添加：

```
HandlePowerKey=hibernate

```

2\. 执行以下命令使其立即生效：

```
systemctl restart systemd-logind

```

其他详细的设置请参考 [电源管理页面](/index.php/Power_management_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Power management (简体中文)")。

## 参看

[linux-laptop笔记本相关](https://github.com/levinit/itnotes/blob/master/linux/laptop%E7%AC%94%E8%AE%B0%E6%9C%AC%E7%9B%B8%E5%85%B3.md) [linux笔记本设置休眠](http://www.cnblogs.com/unkownarea/p/7471285.html)