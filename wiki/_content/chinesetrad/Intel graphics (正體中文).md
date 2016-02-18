Intel顯示卡及晶片資訊. *在終端機下使用(不使用X視窗)，請參閱[Uvesafb](/index.php/Uvesafb "Uvesafb").*

## Contents

*   [1 前言](#.E5.89.8D.E8.A8.80)
    *   [1.1 模組](#.E6.A8.A1.E7.B5.84)
    *   [1.2 驅動程式](#.E9.A9.85.E5.8B.95.E7.A8.8B.E5.BC.8F)
*   [2 安裝](#.E5.AE.89.E8.A3.9D)
*   [3 配置](#.E9.85.8D.E7.BD.AE)
*   [4 KMS (核心模式設定)](#KMS_.28.E6.A0.B8.E5.BF.83.E6.A8.A1.E5.BC.8F.E8.A8.AD.E5.AE.9A.29)
    *   [4.1 其他](#.E5.85.B6.E4.BB.96)
*   [5 提示與技巧 (翻譯中)](#.E6.8F.90.E7.A4.BA.E8.88.87.E6.8A.80.E5.B7.A7_.28.E7.BF.BB.E8.AD.AF.E4.B8.AD.29)
    *   [5.1 Setting scaling mode](#Setting_scaling_mode)
    *   [5.2 Workaround for bug with opening laptop lid](#Workaround_for_bug_with_opening_laptop_lid)
        *   [5.2.1 Solution #1](#Solution_.231)
        *   [5.2.2 Solution #2](#Solution_.232)
    *   [5.3 KMS Issue: console is limited to small area](#KMS_Issue:_console_is_limited_to_small_area)

## 前言

自從 Intel 提供並支援開源驅動後，Intel的顯示卡現在已能隨插即用。

### 模組

一般常把"Intel 945G"和"Intel GMA 945"視為相同的顯示晶片。 實際上，"intel GMA 945"並不存在。Intel使用"GMA"代表繪圖核心，即GPU。 任何不含"GMA"的都是**主機板晶片**，像"915G","945GM","G45"都屬主機板晶片。

常見的繪圖核心與其對應的主機板晶片如下：

*   Intel GMA 900 (910, 915)
*   Intel GMA 950 (945)

"i810"(主機板晶片，非GPU)是非常舊的晶片，其製造時間比9xx主機板晶片系列還早。相同的，910, 915, 945晶片的名字可能會在前面加個"i"

列表詳見 [Intel_GMA表](https://en.wikipedia.org/wiki/Intel_GMA#Table_of_GMA_graphics_cores_and_chipsets "wikipedia:Intel GMA")

### 驅動程式

*   intel (最新且最佳的)
*   intel-legacy (過時的，無法與新的 xorg-server 相容)

強烈建議優先使用較新的驅動程式。

## 安裝

前罝套件： [Xorg](/index.php/Xorg "Xorg")

執行

```
# pacman -S xf86-video-intel

```

或

```
# pacman -S xf86-video-intel-legacy

```

## 配置

當有安裝 HAL 套件時, 便無須任何的配置即可使用。 更多資訊請參閱[Xorg input hotplugging](/index.php/Xorg_input_hotplugging "Xorg input hotplugging")

但請記得把你的使用者加入對應的群組：

```
# gpasswd -a *username* video

```

## KMS (核心模式設定)

[KMS](/index.php/KMS "KMS")以藉由 i915 DRM 驅動程式來支援Intel的晶片，同時核心版本2.6.32預設為啟用。自xf86-video-intel 2.10版本開始[強制啟用 KMS](https://www.archlinux.org/news/484/)。KMS通常是在核心被啟動(bootstrapped)後才被初始化。但也可以在核心啟動時就啟用 KMS，讓整個開機流程運作在原生(native)解析度之下。

**注意**：在啟動KMS的狀況下，你*必須*從/boot/grub/menu.lst的核心命令列中移除任何 "vga=" or "video=" 參數值。

把 /etc/mkinitcpio.conf 的 MODULES="[...]" 中加入 `intel_agp` 和 `i915` 模組：

```
MODULES="**intel_agp i915**"

```

再重建 initramfs：

```
# mkinitcpio -p linux

```

如果你想要停用 KMS，不需要重建任何東西，只要編輯[GRUB](/index.php/GRUB "GRUB")的 `/boot/grub/menu.lst` 在kernel的參數列加入 **i915.modeset=0**. See [kernel parameters](/index.php/Kernel_parameters "Kernel parameters").

如果你想要停用 KMS 而不需編輯menu.lst，你可以在開機看到grub選單時，按下任何鍵使其停止倒數，在欲修改的選單項目前按"e"去編輯。然後再選取"kernel"列，再壓"e"後加入"**i915.modeset=0**"。改完之後，按"enter"確認，再按"b"即可以停用KMS方式啟動核心。切記這方法只適用於單次暫時停用KMS，之後再開機KMS仍會設為啟用。需要永久性設為停用請修改`/boot/grub/menu.lst`。

### 其他

*   [KMS](/index.php/KMS "KMS") - Arch wiki article on kernel mode setting
*   Arch Linux forums: [HOWTO: Enable KMS with the stock 2.6.29-ARCH kernel](https://bbs.archlinux.org/viewtopic.php?id=69083)
*   Arch Linux forums: [Intel 945GM, Xorg, Kernel - performance](https://bbs.archlinux.org/viewtopic.php?pid=522665#p522665)

## 提示與技巧 (翻譯中)

### Setting scaling mode

This can be useful for some full screen applications.

```
xrandr --output LVDS1 --set PANEL_FITTING param

```

where <tt>param</tt> can be

*   <tt>center</tt>: resolution will be kept exactly as defined, no scaling will be made,
*   <tt>full</tt>: scale the resolution so it uses the entire screen or
*   <tt>full_aspect</tt>: scale the resolution to the maximum possible but keep the aspect ratio.

If it does not work, you can try

```
xrandr --output LVDS1 --set "scaling mode" param

```

where <tt>param</tt> is one of <tt>"Full"</tt>, <tt>"Center"</tt> or <tt>"Full aspect"</tt>.

### Workaround for bug with opening laptop lid

#### Solution #1

On laptops with Intel video chip you can face the issue with not working X display after you close lid to make the machine suspend and than open it back. See bug [https://bugs.freedesktop.org/show_bug.cgi?id=24970](https://bugs.freedesktop.org/show_bug.cgi?id=24970) for more details.

Here is a way to work it around. The recipe is based on similar one from Fedora "Common bugs" page: [https://fedoraproject.org/wiki/Common_F12_bugs#Display_cannot_be_reactivated_if_it_enters_sleep_mode_with_laptop_lid_closed](https://fedoraproject.org/wiki/Common_F12_bugs#Display_cannot_be_reactivated_if_it_enters_sleep_mode_with_laptop_lid_closed)

**Note:** This workaround will work only in single-user system, you can make it work for multiple users by adding procedure of checking which user put machine to suspend state.

Install acpid:

`pacman -S acpid`

After that place acpid before hal in DAEMONS section of your `/etc/rc.conf` file.

Than create a file `/etc/acpi/actions/reset-display.sh` with the following contents:

```
 #!/bin/bash
 PATH="/bin:/usr/bin:/sbin:/usr/sbin"
 export DISPLAY=:0.0
 sleep 10 
 if grep open /proc/acpi/button/lid/LID/state
 then
   su "$(getent passwd $UID | cut -d: -f1)" -c "xrandr --output LVDS1 --off" 
   su "$(getent passwd $UID | cut -d: -f1)" -c "xrandr --output LVDS1 --auto" 
 fi

```

where <tt>$UID</tt> is UID of the user who put laptop to suspend mode (you). The main difference from original Fedora method is <tt>sleep</tt> operator usage. Without it the lid button state will not be updated by the moment it checking by `reset-display.sh` script, in some cases smaller delay (for example 3 seconds) will work when running on AC power and will not work with battery power, 10 seconds works always. Do not forget to make the script executable:

```
 #chmod +x /etc/acpi/actions/reset-display.sh

```

Than we need to assign the action to LID switch event. Add the following line to `/etc/acpi/handler.sh` file under <tt>button/lid)</tt> code:

```
 /etc/acpi/actions/reset-display.sh

```

Now you can reboot your laptop or just restart daemons in the following order:

```
 #/etc/rc.d/hal stop
 #/etc/rc.d/acpid start
 #/etc/rc.d/hal start

```

#### Solution #2

An easier, less reliable workaround is to simply re-suspend the computer and wake it again. This will often correct the glitch and return the X desktop to a working state.

### KMS Issue: console is limited to small area

One of the low-resolution video ports may be enabled on boot which is causing the terminal to utilize a small area of the screen. To fix, explicitly disable the port with an i915 module setting. For example, add the following to the end of the kernel line in /boot/grub/menu.lst:

```
 video=SVIDEO-1:d

```

If that doesn't work, you may also try disabling TV1 or VGA1 instead of SVIDEO-1.