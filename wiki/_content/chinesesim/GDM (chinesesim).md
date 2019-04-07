相关文章

*   [Display manager (简体中文)](/index.php/Display_manager_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Display manager (简体中文)")
*   [GNOME (简体中文)](/index.php/GNOME_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GNOME (简体中文)")
*   [GNOME Flashback](/index.php/GNOME_Flashback "GNOME Flashback")
*   [Display_manager_(简体中文)](/index.php/Display_manager_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Display manager (简体中文)")
*   [LightDM_(简体中文)](/index.php/LightDM_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "LightDM (简体中文)")
*   [LXDM_(简体中文)](/index.php/LXDM_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "LXDM (简体中文)")

**翻译状态：** 本文是英文页面 [GDM](/index.php/GDM "GDM") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2018-08-08，点击[这里](https://wiki.archlinux.org/index.php?title=GDM&diff=0&oldid=525308)可以查看翻译后英文页面的改动。

来自[GDM - GNOME显示管理器](https://wiki.gnome.org/Projects/GDM)：“GNOME显示管理器（GDM）是一个管理图形显示服务和处理图形用户登录的程序。

[显示管理器s](/index.php/Display_manager_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Display manager (简体中文)") provide [X Window System](/index.php/Xorg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Xorg (简体中文)") and [Wayland](/index.php/Wayland_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Wayland (简体中文)") users with a graphical login prompt.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 安装](#安装)
*   [2 开始](#开始)
    *   [2.1 自动启动软件](#自动启动软件)
*   [3 配置](#配置)
    *   [3.1 登录页面背景图片](#登录页面背景图片)
    *   [3.2 DConf configuration](#DConf_configuration)
        *   [3.2.1 登录页面的logo](#登录页面的logo)
        *   [3.2.2 更改光标主题](#更改光标主题)
        *   [3.2.3 在登录页面显示大字体](#在登录页面显示大字体)
        *   [3.2.4 关闭声音](#关闭声音)
        *   [3.2.5 更改电源按钮行为](#更改电源按钮行为)
        *   [3.2.6 开启轻触以点击](#开启轻触以点击)
        *   [3.2.7 开启或关闭无障碍菜单](#开启或关闭无障碍菜单)
    *   [3.3 键盘布局](#键盘布局)
    *   [3.4 更改语言](#更改语言)
    *   [3.5 用户与登录](#用户与登录)
        *   [3.5.1 自动登录](#自动登录)
        *   [3.5.2 免密登录](#免密登录)
        *   [3.5.3 Passwordless shutdown for multiple sessions](#Passwordless_shutdown_for_multiple_sessions)
        *   [3.5.4 在GDM中开启root登录](#在GDM中开启root登录)
        *   [3.5.5 在登录列表中隐藏用户](#在登录列表中隐藏用户)
    *   [3.6 Setup default monitor settings](#Setup_default_monitor_settings)
    *   [3.7 Configure X server access permission](#Configure_X_server_access_permission)
*   [4 已知问题](#已知问题)
    *   [4.1 无法使用NVIDIA（英伟达）闭源驱动](#无法使用NVIDIA（英伟达）闭源驱动)
    *   [4.2 注销失败](#注销失败)
    *   [4.3 Rootless Xorg](#Rootless_Xorg)
    *   [4.4 使用Xorg作为后端](#使用Xorg作为后端)
    *   [4.5 Incomplete removal of gdm](#Incomplete_removal_of_gdm)
    *   [4.6 GDM自动挂起（GNOME 3.28）](#GDM自动挂起（GNOME_3.28）)
*   [5 参见](#参见)

## 安装

可通过安装[gdm](https://www.archlinux.org/packages/?name=gdm)包来安装GDM，或作为[gnome](https://www.archlinux.org/groups/x86_64/gnome/)组的一部分安装。

如果你更希望使用在GNOME 2中使用的旧的GDM和它的实用配置程序，安装[gdm-old](https://aur.archlinux.org/packages/gdm-old/)软件包。请注意，除非另有说明，否则本条目的其余部分均为讨论当前的GDM，而非旧的GDM。

您可能还希望安装以下内容：

*   **gdm3setup** — 一个用来配置GDM3的接口，有自动登陆选项并且能更改Shell的主题

	[https://github.com/Nano77/gdm3setup](https://github.com/Nano77/gdm3setup) || [gdm3setup-utils](https://aur.archlinux.org/packages/gdm3setup-utils/)

## 开始

可通过[enable](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E4.BD.BF.E7.94.A8.E5.8D.95.E5.85.83 "Systemd (简体中文)")`gdm.service`来在开机时启动GDM。

### 自动启动软件

One might want to autostart certain commands, such as *xrandr* for instance, on login. This can be achieved by adding a command or script to a location that is sourced by the display manager. See [Display manager#Autostarting](/index.php/Display_manager#Autostarting "Display manager") for a list of supported locations.

**Note:** `/etc/gdm/Init`目录不再是受支持的位置，参见[[1]](https://bugzilla.gnome.org/show_bug.cgi?id=751602#c2).

## 配置

### 登录页面背景图片

**Note:**

*   自GNOME 3.16开始，GNOME Shell主题被存储为二进制文件。 （gresource）
*   This change will be overwritten on subsequent updates of [gnome-shell](https://www.archlinux.org/packages/?name=gnome-shell).

Firstly, you need to extract the existing GNOME Shell theme to a folder in your home directory. You can do this using the following script:

 `extractgst.sh` 
```
#!/bin/sh
gst=/usr/share/gnome-shell/gnome-shell-theme.gresource
workdir=${HOME}/shell-theme

for r in `gresource list $gst`; do
	r=${r#\/org\/gnome\/shell/}
	if [ ! -d $workdir/${r%/*} ]; then
	  mkdir -p $workdir/${r%/*}
	fi
done

for r in `gresource list $gst`; do
        gresource extract $gst $r >$workdir/${r#\/org\/gnome\/shell/}
done
```

Navigate to the created directory. You should find that the theme files have been extracted to it. Now copy your preferred background image to this directory.

Next, you need to create a file in the directory with the following content:

 `gnome-shell-theme.gresource.xml` 
```
<?xml version="1.0" encoding="UTF-8"?>
<gresources>
  <gresource prefix="/org/gnome/shell/theme">
    <file>calendar-arrow-left.svg</file>
    <file>calendar-arrow-right.svg</file>
    <file>calendar-today.svg</file>
    <file>checkbox-focused.svg</file>
    <file>checkbox-off-focused.svg</file>
    <file>checkbox-off.svg</file>
    <file>checkbox.svg</file>
    <file>close.svg</file>
    <file>close-window-active.svg</file>
    <file>close-window-hover.svg</file>
    <file>close-window.svg</file>    		
    <file>corner-ripple-ltr.png</file>
    <file>corner-ripple-rtl.png</file>
    <file>dash-placeholder.svg</file>
    <file>filter-selected-ltr.svg</file>
    <file>filter-selected-rtl.svg</file>
    <file>gnome-shell.css</file>	
    <file>gnome-shell-high-contrast.css</file>
    <file>icons/message-indicator-symbolic.svg</file>
    <file>key-enter.svg</file>
    <file>key-hide.svg</file>
    <file>key-layout.svg</file>
    <file>key-shift-latched-uppercase.svg</file>
    <file>key-shift.svg</file>
    <file>key-shift-uppercase.svg</file>
    <file>logged-in-indicator.svg</file>
    <file>no-events.svg</file>
    <file>no-notifications.svg</file>
    <file>**filename**</file>
    <file>pad-osd.css</file>
    <file>page-indicator-active.svg</file>		
    <file>page-indicator-checked.svg</file>
    <file>page-indicator-hover.svg</file>
    <file>page-indicator-inactive.svg</file>
    <file>process-working.svg</file>
    <file>running-indicator.svg</file>
    <file>source-button-border.svg</file>
    <file>summary-counter.svg</file>
    <file>toggle-off-hc.svg</file>
    <file>toggle-off-intl.svg</file>
    <file>toggle-off-us.svg</file>		
    <file>toggle-on-hc.svg</file>		
    <file>toggle-on-intl.svg</file>
    <file>toggle-on-us.svg</file>		
    <file>ws-switch-arrow-down.png</file>
    <file>ws-switch-arrow-up.png</file>
  </gresource>
</gresources>
```

Replace **filename** with the filename of your background image.

Now, open the `gnome-shell.css` file in the directory and change the `#lockDialogGroup` definition as follows:

```
#lockDialogGroup {
  background: #2e3436 url(**filename**);
  background-size: **[WIDTH]**px **[HEIGHT]**px;
  background-repeat: no-repeat;
}

```

Set `background-size` to the resolution that GDM uses, this might not necessarily be the resolution of the image. For a list of display resolutions see [Display resolution](https://en.wikipedia.org/wiki/Display_resolution#Computer_monitors "wikipedia:Display resolution"). Again, set **filename** to be the name of the background image.

Finally, compile the theme using the following command:

```
$ glib-compile-resources gnome-shell-theme.gresource.xml

```

Then copy the resulting `gnome-shell-theme.gresource` file to the `/usr/share/gnome-shell` directory.

Then restart `gdm.service` (note that simply logging out is not enough) and you should find that it is using your preferred background image.

For more information, please see the following [forum thread](https://bbs.archlinux.org/viewtopic.php?id=197036).

### DConf configuration

Some GDM settings are stored in a DConf database. They can be configured either by adding *keyfiles* to the `/etc/dconf/db/gdm.d` directory and then recompiling the GDM database by running `dconf update` as root or by logging into the GDM user on the system and changing the setting directly using the *gsettings* command line tool. Note that for the former approach, a GDM profile file is required - this must be created manually as it is no longer shipped upstream, see below:

 `/etc/dconf/profile/gdm` 
```
user-db:user
system-db:gdm
file-db:/usr/share/gdm/greeter-dconf-defaults
```

For the latter approach, you can log into the GDM user with the command below:

```
# machinectl shell gdm@

```

#### 登录页面的logo

Either create the following keyfile

 `/etc/dconf/db/gdm.d/02-logo` 
```
[org/gnome/login-screen]
logo='*/path/to/logo.png*'
```

and then recompile the GDM database or alternatively log in to the GDM user and execute the following:

```
$ gsettings set org.gnome.login-screen logo '*/path/to/logo.png*'

```

#### 更改光标主题

GDM disregards [GNOME](/index.php/GNOME "GNOME") cursor theme settings and it also ignores the cursor theme set according to the [XDG specification](/index.php/Cursor_themes#XDG_specification "Cursor themes"). To change the cursor theme used in GDM, either create the following keyfile

 `/etc/dconf/db/gdm.d/10-cursor-settings` 
```
[org/gnome/desktop/interface]
cursor-theme='*theme-name'*

```

and then recompile the GDM database or alternatively log in to the GDM user and execute the following:

```
$ gsettings set org.gnome.desktop.interface cursor-theme '*theme-name*'

```

#### 在登录页面显示大字体

Click on the accessibility icon at the top right of the screen (a white circle with the silhouette of a person in the centre) and check the *Large Text* option.

To set a specific scaling factor, you can create the following keyfile:

 `/etc/dconf/db/gdm.d/03-scaling` 
```
[org/gnome/desktop/interface]
text-scaling-factor='*1.25*'
```

and then recompile the GDM database or alternatively log in to the GDM user and execute the following:

```
$ gsettings set org.gnome.desktop.interface text-scaling-factor '*1.25*'

```

#### 关闭声音

This tweak disables the audible feedback heard when the system volume is adjusted (via keyboard) on the login screen.

Either create the following keyfile:

 `/etc/dconf/db/gdm.d/04-sound` 
```
[org/gnome/desktop/sound]
event-sounds='false'
```

and then recompile the GDM database or alternatively log in to the GDM user and execute the following:

```
$ gsettings set org.gnome.desktop.sound event-sounds 'false'

```

#### 更改电源按钮行为

**Note:**

*   The [logind settings](/index.php/Power_management#ACPI_events "Power management") for the power button are overriden by GNOME Settings Daemon. [[2]](https://bugzilla.gnome.org/show_bug.cgi?id=755953#c4)
*   As of GDM 3.18, the power button cannot be set to *interactive*. [[3]](https://bugzilla.gnome.org/show_bug.cgi?id=753713#c6)
*   In some cases, this setting will be ignored and hardcoded defaults will be used. [[4]](https://bugzilla.gnome.org/show_bug.cgi?id=755953#c17)

**Warning:** Please note that the [acpid](/index.php/Acpid "Acpid") daemon also handles the "power button" and "hibernate button" events. Running both systems at the same time may lead to unexpected behaviour.

Either create the following keyfile:

 `/etc/dconf/db/gdm.d/05-power` 
```
[org/gnome/settings-daemon/plugins/power]
power-button-action='*action*'
```

and then recompile the GDM database or alternatively log in to the GDM user and execute the following:

```
$ gsettings set org.gnome.settings-daemon.plugins.power power-button-action '*action*'

```

where *action* can be one of `nothing`, `suspend` or `hibernate`.

#### 开启轻触以点击

轻触以点击在GDM（和GNOME）中被默认关闭，但是你可以使用dconf设置轻松地开启它。

**Note:** 如果你想要在X下这么做，you have to first set up correct X server access permissions - see [#Configure X server access permission](#Configure_X_server_access_permission).

可用以下命令直接开启轻触以点击：

 `# sudo -u gdm gsettings set org.gnome.desktop.peripherals.touchpad tap-to-click true` 

如果你想使用GUI，请使用：

 `# sudo -u gdm dconf-editor` 

检查它是否被正确开启：

 `$ sudo -u gdm gsettings get org.gnome.desktop.peripherals.touchpad tap-to-click` 

如果你得到一个错误：`dconf-WARNING **: failed to commit changes to dconf: Error spawning command line`，请确认dbus正在运行：

 `$ sudo -u gdm dbus-launch gsettings set org.gnome.desktop.peripherals.touchpad tap-to-click true` 

#### 开启或关闭无障碍菜单

在dconf编辑器中设置以下key以关闭或开启无障碍菜单。

```
# machinectl shell gdm@
# gsettings set org.gnome.desktop.interface toolkit-accessibility false
# exit
```

当key是false时，无障碍菜单被默认关闭；true时为开启。

### 键盘布局

系统键盘布局会被应用到GDM。参见[Keyboard configuration in Xorg#Using X configuration files](/index.php/Keyboard_configuration_in_Xorg#Using_X_configuration_files "Keyboard configuration in Xorg")。

**Tip:** See [Wikipedia:ISO 3166-1](https://en.wikipedia.org/wiki/ISO_3166-1 "wikipedia:ISO 3166-1") for a list of keymaps.

If a system has multiple users, it is possible to specify a keyboard layout for GDM to use which is different from the system keyboard layout. Firstly, ensure the package [gnome-control-center](https://www.archlinux.org/packages/?name=gnome-control-center) is installed. Then start *gnome-control-center* and navigate to *Region & Language -> Input Sources*. In the header bar, hit the *Login Screen* toggle button and then choose a keyboard layout from the list. Note that the *Login Screen* button will not be visible in the header bar unless multiple users are present on the system [[5]](https://bugzilla.gnome.org/show_bug.cgi?id=741500).

GDM 2.x（legacy GDM）的用户需要将`~/.dmrc`更改为以下内容：

 `~/.dmrc` 
```
[Desktop]
Language=de_DE.UTF-8   # change to your default lang
Layout=de   nodeadkeys # change to your keyboard layout
```

### 更改语言

The system language will be applied to GDM. If a system has multiple users, it is possible to set a language for GDM different to the system language. In this case, firstly ensure that [gnome-control-center](https://www.archlinux.org/packages/?name=gnome-control-center) is installed. Then, start *gnome-control-center* and choose *Region & Language*. In the header bar, check the *Login Screen* toggle button. Finally, click on *Language* and choose your language from the list. You will be prompted for your root password. Note that the *Login Screen* button will not be visible in the header bar unless multiple users are present on the system [[6]](https://bugzilla.gnome.org/show_bug.cgi?id=741500).

**Tip:** By adding 2 different input languages, logging out then selecting your default language GDM will remember your choice once the second option is removed.

### 用户与登录

#### 自动登录

将以下内容添加至`/etc/gdm/custom.conf`以开启自动登陆（将*username*替换为你的用户名）：

 `/etc/gdm/custom.conf` 
```
# Enable automatic login for user
[daemon]
AutomaticLogin=*username*
AutomaticLoginEnable=True
```

**Tip:** If GDM fails after adding these lines, comment them out from a TTY.

or for an automatic login with a delay:

 `/etc/gdm/custom.conf` 
```
[daemon]

TimedLoginEnable=true
TimedLogin=*username*
TimedLoginDelay=1
```

You can set the session used for automatic login (replace `gnome-xorg` with desired session):

 `/var/lib/AccountsService/users/*username*`  `XSession=gnome-xorg` 

#### 免密登录

If you want to bypass the password prompt in GDM then simply add the following line on the first line of `/etc/pam.d/gdm-password`:

```
auth sufficient pam_succeed_if.so user ingroup nopasswdlogin

```

Then, add the group `nopasswdlogin` to your system. See [User group](/index.php/User_group "User group") for group descriptions and group management commands.

Now, add your user to the `nopasswdlogin` group and you will only have to click on your username to login.

**Warning:**

*   **不要**对**root**账户这么做。
*   You won't be able to change your session type at login with GDM anymore. If you want to change your default session type, you will first need to remove your user from the `nopasswdlogin` group.

#### Passwordless shutdown for multiple sessions

GDM uses polkit and logind to gain permissions for shutdown. You can shutdown the system when multiple users are logged in by setting:

 `/etc/polkit-1/localauthority.conf.d/org.freedesktop.logind.policy` 
```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE policyconfig PUBLIC
 "-//freedesktop//DTD PolicyKit Policy Configuration 1.0//EN"
 "[http://www.freedesktop.org/standards/PolicyKit/1.0/policyconfig.dtd](http://www.freedesktop.org/standards/PolicyKit/1.0/policyconfig.dtd)">

<policyconfig>

  <action id="org.freedesktop.login1.power-off-multiple-sessions">
    <description>Shutdown the system when multiple users are logged in</description>
    <message>System policy prevents shutting down the system when other users are logged in</message>
    <defaults>
      <allow_inactive>yes</allow_inactive>
      <allow_active>yes</allow_active>
    </defaults>
  </action>

</policyconfig>
```

You can find all available logind options (e.g. reboot-multiple-sessions) [here](http://www.freedesktop.org/wiki/Software/systemd/logind#Security).

#### 在GDM中开启root登录

It is not advised to login as root, but if necessary you can edit `/etc/pam.d/gdm-password` and add the following line before the line `auth required pam_deny.so`:

`/etc/pam.d/gdm-password`

```
auth            sufficient      pam_succeed_if.so uid eq 0 quiet

```

The file should look something like this:

`/etc/pam.d/gdm-password`

```
...
auth            sufficient      pam_succeed_if.so uid eq 0 quiet
auth            sufficient      pam_succeed_if.so uid >= 1000 quiet
auth            required        pam_deny.so
...

```

You should be able to login as root after restarting GDM.

#### 在登录列表中隐藏用户

The users for the gdm user list are gathered by [AccountsService](https://www.freedesktop.org/wiki/Software/AccountsService/). It will automatically hide system users (UID < 1000). To hide ordinary users from the login list create or edit a file named after the user to hide in `/var/lib/AccountsService/users/` to contain at least:

 `/var/lib/AccountsService/users/<username>` 
```
[User]
SystemAccount=true
```

### Setup default monitor settings

Some [desktop environments](/index.php/Desktop_environments "Desktop environments") store display settings in `~/.config/monitors.xml`. *xrandr* commands are then generated on the base of the file content. GDM has a similar file stored in `/var/lib/gdm/.config/monitors.xml`.

If you have your monitors setup as you like (orientation, primary and so on) in `~/.config/monitors.xml` and want GDM to honor those settings:

```
# cp ~/.config/monitors.xml /var/lib/gdm/.config/monitors.xml

```

Changes will take effect on logout. This is necessary because GDM does not respect `xorg.conf`.

**Note:** If you use GDM under Wayland, you must also use a `monitors.xml` that was created under Wayland. See [GDM issue 224](https://gitlab.gnome.org/GNOME/gdm/issues/224) for more info. Alternatively, you can force GDM to [#使用Xorg作为后端](#使用Xorg作为后端), and use a `monitors.xml` that was created under Xorg.

### Configure X server access permission

You can use the `xhost` command to configure X server access permissions.

For instance, to grant GDM the right to access the X server, use the following command:

 `# xhost +SI:localuser:gdm` 

## 已知问题

### 无法使用NVIDIA（英伟达）闭源驱动

GDM uses the [Wayland](/index.php/Wayland "Wayland") backend by default which conflicts with NVIDIA driver. Turning off the Wayland backend could enable proprietary NVIDIA driver.

### 注销失败

If GDM starts up properly on boot, but fails after repeated attempts on logout, try adding this line to the daemon section of `/etc/gdm/custom.conf`:

```
GdmXserverTimeout=60

```

### Rootless Xorg

参见[Xorg#Rootless Xorg](/index.php/Xorg#Rootless_Xorg "Xorg")。

### 使用Xorg作为后端

The [Wayland](/index.php/Wayland "Wayland") backend is used by default and the [Xorg](/index.php/Xorg "Xorg") backend is used only if the Wayland backend cannot be started. As the Wayland backend has been [reported](https://bugzilla.redhat.com/show_bug.cgi?id=1199890) to cause problems for some users, use of the Xorg backend may be necessary. To use the Xorg backend by default, edit the `/etc/gdm/custom.conf` file and uncomment the following line:

```
#WaylandEnable=false

```

### Incomplete removal of gdm

After removing [gdm](https://www.archlinux.org/packages/?name=gdm), [systemd](/index.php/Systemd "Systemd") may report the following:

```
user 'gdm': directory '/var/lib/gdm' does not exist

```

To remove this warning, login as root and delete the primary user "gdm" and then delete the group "gdm":

```
# userdel gdm
# groupdel gdm

```

Verify that gdm is successfully removed via `pwck` and `grpck`. To round it off, you may want to double-check no [unowned files](/index.php/Pacman/Tips_and_tricks#Identify_files_not_owned_by_any_package "Pacman/Tips and tricks") for gdm remain.

### GDM自动挂起（GNOME 3.28）

GDM uses a separate dconf database to control power management. You can make GDM behave the same way as user sessions by copying the user settings to GDM's dconf database.

```
$ IFS=$'
'; for x in $(sudo -u YOUR_USER gsettings list-recursively org.gnome.settings-daemon.plugins.power); do eval "sudo -u gdm dbus-launch gsettings set $x"; done; unset IFS

```

Or to simply disable auto-suspend (also run the command with `ac` replaced with `battery` to also disable it while running on battery):

```
$ sudo -u gdm dbus-launch gsettings set org.gnome.settings-daemon.plugins.power sleep-inactive-ac-type 'nothing'

```

## 参见

*   [GDM Reference Manual](https://help.gnome.org/admin/gdm/stable/index.html.en)