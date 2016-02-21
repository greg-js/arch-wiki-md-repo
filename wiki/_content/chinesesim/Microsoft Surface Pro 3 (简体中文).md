**翻译状态：** 本文是英文页面 [Microsoft_Surface_Pro_3](/index.php/Microsoft_Surface_Pro_3 "Microsoft Surface Pro 3") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-01-28，点击[这里](https://wiki.archlinux.org/index.php?title=Microsoft_Surface_Pro_3&diff=0&oldid=420251)可以查看翻译后英文页面的改动。

**警告:** 设备的保修仅在OEM版Windows仍然存在时有效,官方解释,双启动不会使保修失效.[这里](http://answers.microsoft.com/en-us/surface/forum/surfpro-surfusingpro/would-dual-booting-the-surface-pro-void-its/da549e24-f986-4984-b081-25c029882163).

本文记录了所有使Arch Linux在Surface Pro 3上工作的所有有效信息.

## Contents

*   [1 启动进入安装](#.E5.90.AF.E5.8A.A8.E8.BF.9B.E5.85.A5.E5.AE.89.E8.A3.85)
    *   [1.1 禁用Secure Boot](#.E7.A6.81.E7.94.A8Secure_Boot)
    *   [1.2 开启Secure Boot启动安装镜像](#.E5.BC.80.E5.90.AFSecure_Boot.E5.90.AF.E5.8A.A8.E5.AE.89.E8.A3.85.E9.95.9C.E5.83.8F)
*   [2 安装](#.E5.AE.89.E8.A3.85)
*   [3 额外的步骤](#.E9.A2.9D.E5.A4.96.E7.9A.84.E6.AD.A5.E9.AA.A4)
    *   [3.1 编译内核](#.E7.BC.96.E8.AF.91.E5.86.85.E6.A0.B8)
        *   [3.1.1 Surface Pro 3 Linux 其他内核补丁](#Surface_Pro_3_Linux_.E5.85.B6.E4.BB.96.E5.86.85.E6.A0.B8.E8.A1.A5.E4.B8.81)
    *   [3.2 启用触摸板](#.E5.90.AF.E7.94.A8.E8.A7.A6.E6.91.B8.E6.9D.BF)
    *   [3.3 重新启用Secure Boot](#.E9.87.8D.E6.96.B0.E5.90.AF.E7.94.A8Secure_Boot)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Invalid signature detected check secure boot policy in setup](#Invalid_signature_detected_check_secure_boot_policy_in_setup)
    *   [4.2 Keyboard Cover not working](#Keyboard_Cover_not_working)

## 启动进入安装

为了从USB启动,你需要做一些配置让平板从USB或者SD卡启动.另外,你可能需要暂时无视禁止[Secure Boot](/index.php/UEFI#Secure_Boot "UEFI")而导致启动时的一个丑陋的红色背景.

Surface Pro 3有三种启动模式 [详细看这里](http://www.microsoft.com/surface/en-us/support/storage-files-and-folders/boot-surface-pro-from-usb-recovery-device):

1.  普通模式
    1.  按电源键。 你能从UEFI设置里的 "Alternate Boot order"改变启动顺序。
2.  进入BIOS设置
    1.  关闭电源 (或者重启如果你手速够快)
    2.  按住音量上
    3.  按电源键
    4.  等Surface的LOGO出现
    5.  放开音量上
3.  从USB/SD卡启动
    1.  关闭电源
    2.  按住音量下
    3.  按电源键
    4.  等Surface的LOGO出现
    5.  放开电源键

### 禁用Secure Boot

**Note:** 这会导致启动时有一个丑陋的红色背景

进入UEFI设置选择*Secure Boot Control > Disable*.现在接着安装.[Microsoft 更多信息](http://www.microsoft.com/surface/en-sg/support/warranty-service-and-recovery/how-to-use-the-bios-uefi)

### 开启Secure Boot启动安装镜像

看这里[Unified Extensible Firmware Interface#Secure Boot](/index.php/Unified_Extensible_Firmware_Interface#Secure_Boot "Unified Extensible Firmware Interface").

## 安装

按照[Beginners' guide](/index.php/Beginners%27_guide "Beginners' guide")正常步骤安装即可.

## 额外的步骤

虽然在最新的内核中已经支持了触摸屏,屏幕等等.但是它不支持摄像头,多点触控,Type Cover等.在Github上有为Surface Pro 3专制的内核:[[1]](https://github.com/nuclearsandwich/surface3-archlinux).改项目设法支持了这些设备.你可以直接在AUR[[2]](https://aur.archlinux.org/packages/linux-surfacepro3)中安装或自行编译.

### 编译内核

Ref: [Kernels/Compilation/Traditional#Build configuration](/index.php/Kernels/Compilation/Traditional#Build_configuration "Kernels/Compilation/Traditional")

**Note:** 最新的内核补丁是[shvr's github repository](https://github.com/shvr/fedora-surface-pro-3-kernel/).

*   Latest stable kernel release: [f23 branch](https://github.com/shvr/fedora-surface-pro-3-kernel/commits/f23)
*   Latest RC: [master branch](https://github.com/shvr/fedora-surface-pro-3-kernel/commits/master)

#### Surface Pro 3 Linux 其他内核补丁

*   [Camera patch](https://github.com/shvr/fedora-surface-pro-3-kernel/blob/f23/surface-pro-3-Add-support-driver-for-Surface-Pro-3-b.patch)
*   [Hardware Buttons patch](https://github.com/shvr/fedora-surface-pro-3-kernel/blob/f23/Add-Microsoft-Surface-Pro-3-camera-support.patch)
*   [Type Cover patch](https://github.com/shvr/fedora-surface-pro-3-kernel/blob/f23/Add-multitouch-support-for-Microsoft-Type-Cover-3.patch)

**Note:** 使用`git-apply`可以自动添加这些.

### 启用触摸板

Ref: [Reddit](https://www.reddit.com/r/SurfaceLinux/comments/3lbgs4/ubuntu_gnome_1510/)

安装[xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics)并在`/usr/share/X11/xorg.conf.d/10-evdev.conf`添加:

```
Section "InputClass"··
    Identifier "Surface Pro 3 cover"
    MatchIsPointer "on"
    MatchDevicePath "/dev/input/event*"
    Driver "evdev"
    Option "vendor" "045e"
    Option "product" "07dc"
    Option "IgnoreAbsoluteAxes" "True"
EndSection

```

### 重新启用Secure Boot

## Troubleshooting

### Invalid signature detected check secure boot policy in setup

This happened to me after deleting the Secure Boot database and initializing it with Microsoft & CAs. I also had to do the recovery of the bitlocker partition, but I would follow these steps:

1.  After the reset, switch off and try to boot from the sd/usb. If you don't succeed and get the message many times:
    1.  Leaving all TPM & SecureBoot enabled and SSD Only alternate system order
    2.  Do another database reset
    3.  Enroll the Microsoft and CAs again
    4.  reboot into sd/usb with volume down
    5.  It should work now
2.  Follow steps in the Secure Boot installation
3.  After the full installation of archlinux, when you have it working, do the BitLocker recovery

If after doing these steps doesn't still work. Flash the archiso image once more and try again,

### Keyboard Cover not working

This can happen sometimes when you restart. The solution was to shutdown and reboot. (not restart)