相关文章

*   [Display manager](/index.php/Display_manager "Display manager")
*   [KDE (简体中文)](/index.php/KDE_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "KDE (简体中文)")

**翻译状态：** 本文是英文页面 [SDDM](/index.php/SDDM "SDDM") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2019-12-28，点击[这里](https://wiki.archlinux.org/index.php?title=SDDM&diff=0&oldid=592454)可以查看翻译后英文页面的改动。

[Simple Desktop Display Manager](https://github.com/sddm/sddm/) (SDDM) 是 [KDE (简体中文)](/index.php/KDE_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "KDE (简体中文)") Plasma 桌面环境推荐的 [显示管理器](/index.php/Display_manager_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Display manager (简体中文)")。

[维基百科](https://en.wikipedia.org/wiki/Simple_Desktop_Display_Manager "wikipedia:Simple Desktop Display Manager") 介绍：

	Simple Desktop Display Manager (SDDM) 是用于 X11 和 wayland 视窗系统的显示管理器（图形登录界面）。SDDM 完全使用 C++11 编写并支持通过 QML 改变主题。对于KDE Plasma 5，KDE 选择了 SDDM 作为 KDE Display Manager 的接替者。

**注意:** SDDM 还没有完全支持 Wayland 视窗系统 [[1]](https://github.com/sddm/sddm/issues/440)。Wayland 会话在支持之列，但 SDDM 运行于 X11。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 安装](#安装)
*   [2 配置](#配置)
    *   [2.1 自动登录](#自动登录)
    *   [2.2 登录后自动解锁 KDE 钱包](#登录后自动解锁_KDE_钱包)
    *   [2.3 主题设置](#主题设置)
        *   [2.3.1 当前主题](#当前主题)
        *   [2.3.2 编辑主题](#编辑主题)
        *   [2.3.3 测试（预览）主题](#测试（预览）主题)
        *   [2.3.4 鼠标光标](#鼠标光标)
        *   [2.3.5 用户图标（头像）](#用户图标（头像）)
    *   [2.4 数字锁](#数字锁)
    *   [2.5 旋转显示](#旋转显示)
    *   [2.6 DPI 设置](#DPI_设置)
    *   [2.7 启用 HiDPI](#启用_HiDPI)
    *   [2.8 使用指纹识别器](#使用指纹识别器)
*   [3 故障排除](#故障排除)
    *   [3.1 只有空白屏幕和光标，但没有欢迎界面](#只有空白屏幕和光标，但没有欢迎界面)
    *   [3.2 SDDM 出现欢迎界面前的加载时间过长](#SDDM_出现欢迎界面前的加载时间过长)
    *   [3.3 登录后挂起](#登录后挂起)
    *   [3.4 SDDM 在 tty1 启动而不是 tty7](#SDDM_在_tty1_启动而不是_tty7)
    *   [3.5 一个或多个用户没有出现在欢迎界面](#一个或多个用户没有出现在欢迎界面)
    *   [3.6 SDDM 只加载 US 键盘布局](#SDDM_只加载_US_键盘布局)
    *   [3.7 屏幕分辨率过低](#屏幕分辨率过低)
    *   [3.8 自动挂载家目录的加载时间过长](#自动挂载家目录的加载时间过长)

## 安装

[安装](/index.php/Help:Reading_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#安装软件包 "Help:Reading (简体中文)") [sddm](https://www.archlinux.org/packages/?name=sddm) 软件包。对于 [KDE Config Module](/index.php/KDE#KCM "KDE")，可选安装 [sddm-kcm](https://www.archlinux.org/packages/?name=sddm-kcm) 软件包。

然后根据 [Display manager (简体中文)#加载显示管理器](/index.php/Display_manager_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#加载显示管理器 "Display manager (简体中文)") 的说明配置 SDDM 在系统引导时启动。

## 配置

SDDM 的默认配置文件为 `/usr/lib/sddm/sddm.conf.d/default.conf`。要修改配置，请在 `/etc/sddm.conf.d/` 目录下创建配置文件。详见 [sddm.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sddm.conf.5) 以获得所有配置选项。

[sddm-kcm](https://www.archlinux.org/packages/?name=sddm-kcm) 软件包 (包含在 [plasma](https://www.archlinux.org/groups/x86_64/plasma/) 用户组) 提供了一个图形用户界面以在 Plasma 系统设置中配置 SDDM。[AUR](/index.php/AUR "AUR") 中也有基于 [Qt](/index.php/Qt "Qt") 的配置软件 [sddm-config-editor-git](https://aur.archlinux.org/packages/sddm-config-editor-git/)。

一切东西都应该开箱即用，自从 Arch Linux 使用 [systemd](/index.php/Systemd "Systemd") 后，SDDM 默认使用 `systemd-logind` 以进行会话管理。

### 自动登录

SDDM 通过它的配置文件来支持自动登录，例如：

 `/etc/sddm.conf.d/autologin.conf` 
```
[Autologin]
User=john
Session=plasma.desktop
```

此配置使得在系统启动后自动以用户 `john` 开启一个 KDE Plasma 会话。在 `/usr/share/xsessions/` 目录下你可以找到可用的会话类型。

目前尚不支持自动登录 KDE Plasma 的同时锁定会话 [[2]](https://github.com/sddm/sddm/issues/306)

你可以添加一个脚本，在 KDE 自动启动时激活屏幕保护程序以作为一个解决方案：

```
#!/bin/sh
/usr/bin/dbus-send --session --type=method_call --dest=org.freedesktop.ScreenSaver /ScreenSaver org.freedesktop.ScreenSaver.Lock &

```

### 登录后自动解锁 KDE 钱包

详见 [KDE Wallet (简体中文)#在登录时自动解锁 Kwallet](/index.php/KDE_Wallet_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#在登录时自动解锁_Kwallet "KDE Wallet (简体中文)")。

### 主题设置

在 `[Theme]` 小节更改主题设置。如果您使用 Plasma 的系统设置，主题可能会显示预览。

设置 `breeze` 以获得 Plasma 默认主题。

[AUR](/index.php/AUR "AUR") 有一些可用的主题，例如 [archlinux-themes-sddm](https://aur.archlinux.org/packages/archlinux-themes-sddm/)。

#### 当前主题

通过 `Current` 的值设置当前主题，例如 `Current=archlinux-simplyblack`。

#### 编辑主题

默认 SDDM 主题目录为 `/usr/share/sddm/themes/`。你可以添加你的自制主题到该目录下一个单独的子目录中。注意 SDDM 要求这些子目录的名字要与主题的名字一致。可以通过研究已安装的文件来更改或创建属于你的主题。

#### 测试（预览）主题

如果需要，你可以预览一个 SDDM 主题。如果你想知道一个主题看起来怎么样，或是想要编辑一个主题后在不必登出的情况下观察改动的效果，那么这将会非常有用。你可以运行下面的命令：

```
$ sddm-greeter --test-mode --theme /usr/share/sddm/themes/breeze

```

这应该为所有已连接的显示器打开一个新窗口以显示主题的预览。

**注意:** 这只是一个预览。在这个模式下，一些动作如关机、挂起或登录将不会执行。

#### 鼠标光标

要设置鼠标光标的主题，将 `CursorTheme` 设置成您喜欢的光标主题。

合法的 [Plasma](/index.php/Plasma "Plasma") 鼠标光标主题有 `breeze_cursors`，`Breeze_Snow` 和 `breeze-dark`。

#### 用户图标（头像）

SDDM 对于每个用户从相应的 `~/.face.icon` 目录下读取 PNG 图片格式的用户图标（即“头像”），或者从 SDDM 配置文件中由 `FacesDir` 为所有用户定义的共有位置。配置设置可以通过修改 `/etc/sddm.conf` 文件被直接替换，更好的方法是创建一个位于 `/etc/sddm.conf.d/` 下的文件来修改，例如 `/etc/sddm.conf.d/avatar.conf`。

要使用 `FacesDir` 选项来确定头像位置，即在配置文件中 `FacesDir` 所确定的位置为每一个用户放置一个 PNG 图片，命名如 `*username*.face.icon`。`FacesDir` 默认的路径为 `/usr/share/sddm/faces/`。你可以更改默认 `FacesDir` 目录以合乎你的要求。下面是一个例子：

 `/etc/sddm.conf.d/avatar.conf` 
```
[Theme]
FacesDir=/var/lib/AccountsService/icons/
```

另一个选项是放置一个名为 `.face.icon` 的 PNG 图片到你的家目录下。在这种情况下，您不用对任何 SDDM 配置文件进行更改。不过，您仍需确定 `sddm` 用户可以读取这些 PNG 图片作为用户图标。

**注意:** 在许多 KDE 的版本中，用户图标图像文件是 `~/.face` 而 `~/.face.icon` 是链接到图像文件的符号链接。如果用户的图标是符号链接，你需要为目标文件设置恰当的文件权限。

为了 [设置合适权限](/index.php/Access_Control_Lists#Set_ACL "Access Control Lists") 运行：

```
$ setfacl -m u:sddm:x ~/
$ setfacl -m u:sddm:r ~/.face.icon

```

你可以通过运行下列命令 [检查权限](/index.php/Access_Control_Lists#Show_ACL "Access Control Lists")：

```
$ getfacl ~/
$ getfacl ~/.face.icon

```

详见 [SDDM README: No User Icon](https://github.com/sddm/sddm#no-user-icon)。

### 数字锁

如果你想强制启用数字锁，在 `[General]` 小节设置 `Numlock=on`。

### 旋转显示

详见 [Xrandr#Configuration](/index.php/Xrandr#Configuration "Xrandr")。

### DPI 设置

有时位于“显示管理器”级别设置正确的显示器 DPI 是很有用的。[[3]](https://github.com/sddm/sddm/blob/master/README.md#custom-dpi) 你需要在 `ServerArguments` 字符串的末尾加上参数 `-dpi *your_dpi*` 例如：

 `/etc/sddm.conf.d/dpi.conf` 
```
[X11]
ServerArguments=-nolisten tcp -dpi 94
```

### 启用 HiDPI

创建 [HiDPI](/index.php/HiDPI_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "HiDPI (简体中文)") 配置文件如下：

 `/etc/sddm.conf.d/hidpi.conf` 
```
[Wayland]
EnableHiDPI=true

[X11]
EnableHiDPI=true
```

### 使用指纹识别器

**注意:** 在改变设置前要确定你的指纹已经注册完成。指纹支持目前并不是完全工作正常，并且看起来在使用这种方法时仅使用密码登录将不再有效。

SDDM 使用 [fprint](/index.php/Fprint "Fprint") 以使用指纹识别。在安装了 fprint 和添加指纹签名后，在添加 `/etc/pam.d/sddm` 的开始位置添加一行 `auth sufficient pam_fprintd.so`。

**提示：** 要使其在 KDE 的锁屏模式下工作，将上面提到的一行同样添加于 `/etc/pam.d/kde` 的开始位置。

如果你现在在空密码区域按下回车，那么指纹识别器应该开始工作了。

## 故障排除

### 只有空白屏幕和光标，但没有欢迎界面

使用 `df -h` 命令检查您的磁盘空间。如果没有足够的空间，欢迎界面会崩溃。

如果磁盘空间足够，那么这个问题可能源于此 [bug](https://github.com/sddm/sddm/issues/1179)。切换 [到另一个 TTY](/index.php/Getty#Installation "Getty") 来 [重启](/index.php/Restart "Restart") SDDM。

### SDDM 出现欢迎界面前的加载时间过长

内核熵池过小会造成长时间的 SDDM 加载过程([Bug report](https://github.com/sddm/sddm/issues/1036))。详见 [Random number generation](/index.php/Random_number_generation "Random number generation") 扩大内核熵池的建议。

### 登录后挂起

尝试移除 `~/.Xauthority` 文件后不重启再次登入。重启会再次创建该文件即该问题依旧存在。

### SDDM 在 tty1 启动而不是 tty7

SDDM 根据 [systemd 的规定](http://0pointer.de/blog/projects/serial-console.html) 在 tty1 启动图形会话。如果您更喜欢老派的 tty1 到 tty6 皆预留为文本终端，更改 `MinimumVT` 变量的默认值，其位于 `[X11]` 小节下：

 `/etc/sddm.conf.d/tty.conf` 
```
[X11]
MinimumVT=7
```

### 一个或多个用户没有出现在欢迎界面

**警告:** 用户设置过低或过高的 `UID` 范围应该大体上不会暴露给 [Display manager (简体中文)](/index.php/Display_manager_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Display manager (简体中文)")。

SDDM 默认会显示 UID 在 1000 到 65000 范围内的用户，如果想要显示的用户的 UID 小于这个范围，那么您就不得不更改这个范围。比如，对于 UID 为 501时，可以修改：

 `/etc/sddm.conf.d/uid.conf` 
```
[Users]
HideShells=/sbin/nologin,/bin/false
# Hidden users, this is if any system users fall within your range, see /etc/passwd on your system.
HideUsers=git,sddm,systemd-journal-remote,systemd-journal-upload

# Maximum user id for displayed users
MaximumUid=65000

# Minimum user id for displayed users
MinimumUid=500 #My UID is 501
```

### SDDM 只加载 US 键盘布局

SDDM 加载的键盘布局被确定在 `/etc/X11/xorg.conf.d/00-keyboard.conf` 文件中。您可以通过 `localectl set-x11-keymap` 命令以生成此配置文件。详见 [Keyboard configuration in Xorg](/index.php/Keyboard_configuration_in_Xorg "Keyboard configuration in Xorg")。

SDDM 可能也会错误地显示为 US 布局，但在您开始输入您的密码时立即切换到正确的键盘布局 [[4]](https://github.com/sddm/sddm/issues/202#issuecomment-76001543)。此 bug 看起来不是来自 SDDM，而是 [libxcb](https://www.archlinux.org/packages/?name=libxcb) (version 1.13-1 as of 2018) [[5]](https://github.com/sddm/sddm/issues/202#issuecomment-133628462)。

### 屏幕分辨率过低

此问题可能源于显示屏 HiDPI 的使用破坏了 [EDID](https://en.wikipedia.org/wiki/Extended_Display_Identification_Data "wikipedia:Extended Display Identification Data") [[6]](https://github.com/sddm/sddm/issues/692)。如果你 [启动了 HiDPI](#启用_HiDPI)，尝试关掉它。

如果上述方法失败了，您可以尝试在 Xorg 配置文件中设置您的显示尺寸：

 `/etc/X11/xorg.conf.d/90-monitor.conf` 
```
Section "Monitor"
        Identifier      "<default monitor>"
        DisplaySize     345 194 # in millimeters
EndSection
```

### 自动挂载家目录的加载时间过长

SDDM 默认会访问 `~/.face.icon` 文件以尝试显示用户头像。如果您的家目录采用自动挂载的文件系统（autofs），例如如果您使用 [dm-crypt](/index.php/Dm-crypt "Dm-crypt")，这将会使之等待 60 秒，直到自动挂载的文件系统（autofs）返回此目录不能被挂载。

您可以通过编辑 `/etc/sddm.conf` 文件以关闭头像功能：

 `/etc/sddm.conf` 
```
[Theme]
EnableAvatars=false
```