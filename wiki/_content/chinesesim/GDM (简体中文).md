**翻译状态：** 本文是英文页面 [GDM](/index.php/GDM "GDM") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-09-14，点击[这里](https://wiki.archlinux.org/index.php?title=GDM&diff=0&oldid=399844)可以查看翻译后英文页面的改动。

来自 [GDM - GNOME显示管理器](http://projects.gnome.org/gdm/about.html):

	*GDM是一种GNOME显示环境的管理器, 它是一个运行在后台的小程序（脚本）, runs your X sessions,显示一个登录界面并在你忘记密码的时候告诉你无法登录.GDM比xdm在任何方面都做的更好,也没有xdm那么多的漏洞. 它没有使用任何来自xdm的代码. 它支持 XDMCP, and in fact extends XDMCP a little bit in places where I thought xdm was lacking (but is still compatible with xdm's XDMCP).*

[显示管理器](/index.php/Display_manager_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Display manager (简体中文)")为[Xorg](/index.php/Xorg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Xorg (简体中文)")用户们提供了图形化登录提示。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
    *   [1.1 GDM as the default greeter](#GDM_as_the_default_greeter)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
    *   [2.1 Log-in screen background image](#Log-in_screen_background_image)
    *   [2.2 Log-in screen logo](#Log-in_screen_logo)
    *   [2.3 Changing the GDM cursor theme](#Changing_the_GDM_cursor_theme)
    *   [2.4 Larger font for log-in screen](#Larger_font_for_log-in_screen)
    *   [2.5 Turning off the sound](#Turning_off_the_sound)
    *   [2.6 Make the power button interactive](#Make_the_power_button_interactive)
    *   [2.7 GDM keyboard layout](#GDM_keyboard_layout)
        *   [2.7.1 GNOME Control Center](#GNOME_Control_Center)
        *   [2.7.2 GDM 2.x layout](#GDM_2.x_layout)
    *   [2.8 Change the language](#Change_the_language)
    *   [2.9 自动登录](#.E8.87.AA.E5.8A.A8.E7.99.BB.E5.BD.95)
    *   [2.10 无密码登录](#.E6.97.A0.E5.AF.86.E7.A0.81.E7.99.BB.E5.BD.95)
    *   [2.11 Passwordless shutdown for multiple sessions](#Passwordless_shutdown_for_multiple_sessions)
    *   [2.12 Add or edit GDM sessions](#Add_or_edit_GDM_sessions)
    *   [2.13 GDM root 登录](#GDM_root_.E7.99.BB.E5.BD.95)
    *   [2.14 Hide user from login list](#Hide_user_from_login_list)
    *   [2.15 Rotate login screen](#Rotate_login_screen)
    *   [2.16 xrandr at login](#xrandr_at_login)
    *   [2.17 Configure X server access permission](#Configure_X_server_access_permission)
    *   [2.18 Enabling tap-to-click](#Enabling_tap-to-click)
*   [3 疑难解答](#.E7.96.91.E9.9A.BE.E8.A7.A3.E7.AD.94)
    *   [3.1 Failure to start with AMD Catalyst driver](#Failure_to_start_with_AMD_Catalyst_driver)
    *   [3.2 GDM注销失败](#GDM.E6.B3.A8.E9.94.80.E5.A4.B1.E8.B4.A5)
    *   [3.3 Xorg 1.16](#Xorg_1.16)
    *   [3.4 Use Xorg backend](#Use_Xorg_backend)
    *   [3.5 Xorg 1.16](#Xorg_1.16_2)
    *   [3.6 Use Xorg backend](#Use_Xorg_backend_2)
    *   [3.7 gconf-sanity-check-2 exited with status 256](#gconf-sanity-check-2_exited_with_status_256)
    *   [3.8 GDM总是使用默认US-键盘布局](#GDM.E6.80.BB.E6.98.AF.E4.BD.BF.E7.94.A8.E9.BB.98.E8.AE.A4US-.E9.94.AE.E7.9B.98.E5.B8.83.E5.B1.80)
        *   [3.8.1 GDM 2.x](#GDM_2.x)
        *   [3.8.2 GDM 3.x](#GDM_3.x)
        *   [3.8.3 GDM在设置自动登录后无法启动](#GDM.E5.9C.A8.E8.AE.BE.E7.BD.AE.E8.87.AA.E5.8A.A8.E7.99.BB.E5.BD.95.E5.90.8E.E6.97.A0.E6.B3.95.E5.90.AF.E5.8A.A8)
*   [4 参阅](#.E5.8F.82.E9.98.85)

## 安装

GDM (是[gnome-extra](https://www.archlinux.org/groups/x86_64/gnome-extra/)的一部分)，可以通过[官方软件仓库](/index.php/Official_repositories "Official repositories")中的[gdm](https://www.archlinux.org/packages/?name=gdm)软件包进行单独[安装](/index.php/Pacman "Pacman").

### GDM as the default greeter

GDM 软件包提供了`gdm.service`。开机自动启动：

```
# systemctl enable gdm

```

纯systemd启动的话，无法进入图形界面时，可以开启[graphical.target](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E7.9B.AE.E6.A0.87.E8.A1.A8 "Systemd (简体中文)")来实现。

```
# systemctl -f enable graphical.target

```

同时一般还需要启动`NetworkManager.service`：

```
# systemctl enable NetworkManager.service

```

要使用`~/.xinitrc`文件将参数传递给 X 服务（当它启动时），例如 **xmodmap** 或 **xsetroot**，可以向[xprofile](/index.php/Xprofile "Xprofile")添加同样命令，例如：

 `~/.xprofile` 
```
#!/bin/sh

#
# ~/.xprofile
#
# Executed by gdm at login
#

xmodmap -e "pointer=1 2 3 6 7 4 5" # set mouse buttons up correctly
xsetroot -solid black              # sets the background to black

```

## 配置

你再也不能使用gdmsetup命令来配置2.28版本以上的GDM。这个命令已经被移除，而且GDM已经被标准化，成为GNOME的一部分。

你可以从AUR获取并安装[gdm3setup](https://aur.archlinux.org/packages/gdm3setup/)从而配置GDM，也可以使用以下介绍的方法。

配置X服务访问权限

 `# xhost +SI:localuser:gdm` 

要配置GDM主题，使用以下命令：

 `$ sudo -u gdm gnome-appearance-properties` 

实用此命令查看更多配置选项

 `$ sudo -u gdm gconf-editor` 

并修改以下层次（hierarchies）：

```
/apps/gdm/simple-greeter
/desktop/gnome/interface
/desktop/gnome/background

```

如果这些命令失败，并返回诸如 ”cannot open display"之类的错误，你可以通过将它们添加到GDM的自动启动从而在GDM启动时带起这两个窗口。要做到这一点需先创建这些项目（entry）(以 root 身份运行）

 `# cp -t /usr/share/gdm/autostart/LoginWindow/ /usr/share/applications/gnome-appearance-properties.desktop /usr/share/applications/gconf-editor.desktop` 

然后注销你的用户回到GDM。在登录窗口出现后这两个窗口也应该出现。将GDM配置成你想要的样子，然后关闭窗口并重新登录。当你做完了，并想停止这个窗口随着GDM打开，运行这个（以 root 身份）：

 `# rm /usr/share/gdm/autostart/LoginWindow/gnome-appearance-properties.desktop /usr/share/gdm/autostart/LoginWindow/gconf-editor.desktop` 
**注意:** 通过注销/配置的方式，你可以在你配置的时候看到变化。

对于更多信息和高级设置，请阅读[这个](http://library.gnome.org/admin/gdm/2.28/configuration.html.en).

请注意，在xorg-server的1.6.1版本中，`Ctrl`+`Alt`+`Backspace`将再也不会重启GDM。对于重新启用这种行为的介绍，参见[Ctrl-Alt-Backspace无法退出X](/index.php/Xorg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#Ctrl-Alt-Backspace.E6.97.A0.E6.B3.95.E9.80.80.E5.87.BAX "Xorg (简体中文)").

### Log-in screen background image

**Note:** Since GNOME 3.16, GNOME Shell themes are now stored binary files (gresource).

Firstly, you need to extract the existing GNOME Shell theme to a folder in your home directory. You can do this using the following script:

 `extractgst.sh` 
```
#!/bin/sh

workdir=${HOME}/shell-theme
if [ ! -d ${workdir}/theme ]; then
  mkdir -p ${workdir}/theme
fi
gst=/usr/share/gnome-shell/gnome-shell-theme.gresource

for r in `gresource list $gst`; do
        gresource extract $gst $r >$workdir${r/#\/org\/gnome\/shell/}
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
    <file>close-window.svg</file>
    <file>close.svg</file>
    <file>corner-ripple-ltr.png</file>
    <file>corner-ripple-rtl.png</file>
    <file>dash-placeholder.svg</file>
    <file>filter-selected-ltr.svg</file>
    <file>filter-selected-rtl.svg</file>
    <file>gnome-shell.css</file>
    <file>gnome-shell-high-contrast.css</file>
    <file>logged-in-indicator.svg</file>
    <file>**filename**</file>
    <file>more-results.svg</file>
    <file>no-events.svg</file>
    <file>no-notifications.svg</file>
    <file>noise-texture.png</file>
    <file>page-indicator-active.svg</file>
    <file>page-indicator-inactive.svg</file>
    <file>page-indicator-checked.svg</file>
    <file>page-indicator-hover.svg</file>
    <file>process-working.svg</file>
    <file>running-indicator.svg</file>
    <file>source-button-border.svg</file>
    <file>summary-counter.svg</file>
    <file>toggle-off-us.svg</file>
    <file>toggle-off-intl.svg</file>
    <file>toggle-on-us.svg</file>
    <file>toggle-on-intl.svg</file>
    <file>ws-switch-arrow-up.png</file>
    <file>ws-switch-arrow-down.png</file>
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

Set `background-size` to the resolution that GDM uses, this might not necessarily be the resolution of the image. For a list of display resolutions see [Display resolution](https://en.wikipedia.org/wiki/Display_resolution#Computer_monitors). Again, set **filename** to be the name of the background image.

Finally, compile the theme using the following command:

```
$ glib-compile-resources gnome-shell-theme.gresource.xml

```

Then copy the resulting `gnome-shell-theme.gresource` file to the `/usr/share/gnome-shell` directory.

Restart GDM - you should find that it is using your preferred background image.

For more information, please see the following [forum thread](https://bbs.archlinux.org/viewtopic.php?id=197036).

### Log-in screen logo

To display a logo on your log-in screen, follow the instructions below.

Create the directory to store the logo:

```
# mkdir /opt/login

```

Create the necessary configuration file:

```
# touch /etc/dconf/db/gdm.d/02-logo

```

Copy this text into the file:

```
[org/gnome/login-screen]
logo='/opt/login/logo.png'

```

Copy your logo of choice into the directory:

```
# cp [YOUR FILE] /opt/login/logo.png

```

where [YOUR FILE] needs to be a path to a PNG image.

Update dconf:

```
# dconf update

```

### Changing the GDM cursor theme

See [Cursor themes#GDM](/index.php/Cursor_themes#GDM "Cursor themes").

### Larger font for log-in screen

Click on the accessibility icon at the top right of the screen (a white circle with the silhouette of a person in the centre) and check the 'Large Text' option.

Alternatively, follow the instructions below:

Create the necessary configuration file:

```
# touch /etc/dconf/db/gdm.d/03-scaling

```

Copy this text into the file:

```
[org/gnome/desktop/interface]
text-scaling-factor='1.25'

```

Update dconf:

```
# dconf update

```

### Turning off the sound

This tweak disables the audible feedback heard when the system volume is adjusted (via keyboard) on the login screen.

Create the necessary configuration file:

```
# touch /etc/dconf/db/gdm.d/04-sound

```

Copy this text into the file:

```
[org/gnome/desktop/sound]
event-sounds='false'

```

Update dconf:

```
# dconf update

```

### Make the power button interactive

The default installation sets the power button to suspend the system. ***Power off*** or ***Show dialog*** is a better choice.

Create the necessary configuration file:

```
# touch /etc/dconf/db/gdm.d/05-power

```

Copy this text into the file:

```
[org/gnome/settings-daemon/plugins/power button]
power='interactive'
hibernate='interactive'

```

Update dconf:

```
# dconf update

```

**Warning:** Please note that the [acpid](/index.php/Acpid "Acpid") daemon also handles the "power button" and "hibernate button" events. Running both systems at the same time may lead to unexpected behaviour.

### GDM keyboard layout

See [Keyboard configuration in Xorg#Using X configuration files](/index.php/Keyboard_configuration_in_Xorg#Using_X_configuration_files "Keyboard configuration in Xorg").

**Tip:** See [Wikipedia:ISO 3166-1](https://en.wikipedia.org/wiki/ISO_3166-1 "wikipedia:ISO 3166-1") for a list of keymaps.

#### GNOME Control Center

If the package [gnome-control-center](https://www.archlinux.org/packages/?name=gnome-control-center) is installed, the keyboard layout(s) can be configured using a grapical frontend:

```
Settings > Keyboard > Input Sources > Login Screen

```

#### GDM 2.x layout

Users of legacy GDM may need to follow the instructions below:

Edit `~/.dmrc`:

 `~/.dmrc` 
```
[Desktop]
Language=de_DE.UTF-8   # change to your default lang
Layout=de   nodeadkeys # change to your keyboard layout
```

### Change the language

To change the GDM language, edit the file `/var/lib/AccountsService/users/gdm` and change the language line using the correct UTF-8 value for your language. You should see something similar to the text below:

 `/var/lib/AccountsService/users/gdm` 
```
[User]
Language=fr_FR.UTF-8
XSession=
SystemAccount=true
```

Now just reboot your computer.

Once you have rebooted, if you look at the `/var/lib/AccountsService/users/gdm` file again, you will see that the language line is cleared — do not worry, the language change has been preserved.

### 自动登录

想要以GDM自动登录，将以下添加到`/etc/gdm/custom.conf`（将username替换成你想要自动登录的用户):

 `/etc/gdm/custom.conf` 
```
# Enable automatic login for user
[daemon]
AutomaticLogin=username
AutomaticLoginEnable=True

```

或以delay自动登录：

 `/etc/gdm/custom.conf` 
```
[daemon]
# for login with delay
TimedLoginEnable=true
TimedLogin=username
TimedLoginDelay=1

```

### 无密码登录

如果你想省略GDM的密码提示，只要简单地将以下行添加到`/etc/pam.d/gdm`:

```
auth sufficient pam_succeed_if.so user ingroup nopasswdlogin

```

**确保**此行正确地在包含"pam_unix.so"的第一行前。

然后，添加用户组**nopasswdlogin**到你的系统中。你可以通过 系统>管理>用户和用户组（System > Administration > Users and Groups） 进行图形化操作。参见[Groups](/index.php/Groups "Groups")中关于用户组的描述和管理命令。

现在，当你使用 系统>管理>用户和用户组（命令：users-admin）并将你的用户设成”密码：不在登陆时询问“（检查”在登陆时不询问密码“选项），你的用户将会被自动添加到”nopasswdlogin“用户组 and viola，你只要简单地仅仅点击你的用户民就可以正确登录，密码完全被省略了！

**注意:** 在GNOME 3中，users-admin和系统菜单似乎已被移除

**警告:** <u>不要</u>对***ROOT***账户这样做!

### Passwordless shutdown for multiple sessions

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

### Add or edit GDM sessions

Each session is a `.desktop` file located at `/usr/share/xsessions/`.

**To add a new session:**

1\. Copy an existing `.desktop` file to use as a template for a new session:

```
$ cd /usr/share/xsessions
# cp gnome.desktop other.desktop

```

2\. Modify the template `.desktop` file to open the required window manager:

```
# nano other.desktop

```

If you happen to have KDM installed in parallel, you can alternatively open the new session in KDM which will create the new `.desktop` file. Then return to using GDM and the new session will be available.

See also [Display manager#Session list](/index.php/Display_manager#Session_list "Display manager").

### GDM root 登录

不建议以root登录，但如果需要，你可以编辑`/etc/pam.d/gdm-password`并添加以下一行在 `auth required pam_deny.so`之前:

```
auth            sufficient      pam_succeed_if.so uid eq 0 quiet

```

这时文件应该看起来像这样:

```
...
auth            sufficient      pam_succeed_if.so uid eq 0 quiet
auth            sufficient      pam_succeed_if.so uid >= 1000 quiet
auth            required        pam_deny.so
...

```

你应该就能在重启GDM后以 root 登录了。

### Hide user from login list

The users for the gdm user list are gathered by accountsservice. It will automatically hide system users (UID < 1000). To hide ordinary users from the login list create or edit a file named after the user to hide in `/var/lib/AccountsService/users/` to contain at least:

 `/var/lib/AccountsService/users/<username>` 
```
[User]
SystemAccount=true
```

### Rotate login screen

If you have your monitors setup as you like (orientation, primary and so on) in `~/.config/monitors.xml` and want GDM to honor those settings:

```
# cp ~/.config/monitors.xml /var/lib/gdm/.config/monitors.xml

```

Changes will take effect on logout. This is necessary because GDM does not respect `xorg.conf`.

### xrandr at login

If you want to run a script using xrandr that affects the login screen you must add a script in `/etc/X11/xinit/xinitrc.d` since GDM is not respecting or launching the scripts in `/etc/gdm/Init`.

For example, to select automatically a external screen connected through HDMI:

```
#!/bin/sh
EXTERNAL_OUTPUT="HDMI1"
INTERNAL_OUTPUT="eDP1"
if (xrandr | grep $EXTERNAL_OUTPUT | grep " connected "); then
    xrandr --output $INTERNAL_OUTPUT --off --output $EXTERNAL_OUTPUT --auto
else
    xrandr --output $INTERNAL_OUTPUT --auto
fi

```

### Configure X server access permission

You can use the `xhost` command to configure X server access permissions.

For instance, to grant GDM the right to access the X server, use the following command:

 `# xhost +SI:localuser:gdm` 

### Enabling tap-to-click

Tap-to-click is disabled in GDM (and GNOME) by default, but you can easily enable it with a dconf setting.

**Note:** If you want to do this under X, you have to first set up correct X server access permissions - see [#Configure X server access permission](#Configure_X_server_access_permission).

To directly enable tap-to-click, use:

 `# sudo -u gdm gsettings set org.gnome.desktop.peripherals.touchpad tap-to-click true` 

If you prefer to do this with a GUI, use:

 `# sudo -u gdm dconf-editor` 

To check the if it was set correctly, use:

 `$ sudo -u gdm gsettings get org.gnome.desktop.peripherals.touchpad tap-to-click` 

## 疑难解答

### Failure to start with AMD Catalyst driver

Downgrade the [xorg-server](https://www.archlinux.org/packages/?name=xorg-server) package or try to use another [display manager](/index.php/Display_manager "Display manager") like [LightDM](/index.php/LightDM "LightDM").

### GDM注销失败

如果GDM在引导时正确启动，但在重复尝试注销后失败，尝试将此行添加到`/etc/gdm/custom.conf`的daemon区段:

```
GdmXserverTimeout=60

```

### Xorg 1.16

See [Xorg#Rootless Xorg (v1.16)](/index.php/Xorg#Rootless_Xorg_.28v1.16.29 "Xorg").

### Use Xorg backend

As of GDM version 3.16, the [Wayland](/index.php/Wayland "Wayland") backend is used by default and the [Xorg](/index.php/Xorg "Xorg") backend is used only if the Wayland backend cannot be started. As the Wayland backend has been [reported](https://bugzilla.redhat.com/show_bug.cgi?id=1199890) to cause problems for some users, use of the Xorg backend may be necessary. To use the Xorg backend by default, edit the `/etc/gdm/custom.conf` file and uncomment the following line:

```
#WaylandEnable=false

```

### Xorg 1.16

See [Xorg#Rootless Xorg (v1.16)](/index.php/Xorg#Rootless_Xorg_.28v1.16.29 "Xorg").

### Use Xorg backend

As of GDM version 3.16, the [Wayland](/index.php/Wayland "Wayland") backend is used by default and the [Xorg](/index.php/Xorg "Xorg") backend is used only if the Wayland backend cannot be started. As the Wayland backend has been [reported](https://bugzilla.redhat.com/show_bug.cgi?id=1199890) to cause problems for some users, use of the Xorg backend may be necessary. To use the Xorg backend by default, edit the `/etc/gdm/custom.conf` file and uncomment the following line:

```
#WaylandEnable=false

```

### gconf-sanity-check-2 exited with status 256

如果GDM弹出一个关于gconf-sanity-check-2的错误，你可能需要检查在/home 和 /etc/gconf/gconf.xml.system (the latter should be 755)中的权限。 如果GDM依然显示这个错误信息，尝试清空GDM的目录（GDM home）。以 Root 身份运行：

```
rm -rf /var/lib/gdm/.*

```

如果还是不行，尝试将/tmp的所有者和权限设为：

```
# chown -R root:root /tmp
# chmod 777 /tmp

```

### GDM总是使用默认US-键盘布局

问题：键盘布局总被切换成us；键盘布局总是在一个信键盘插上后被重置。解决方法：

#### GDM 2.x

编辑 ~/.dmrc

```
[Desktop]
Language=de_DE.UTF-8   # change to your default lang
Layout=de   nodeadkeys # change to your keyboard layout

```

#### GDM 3.x

将下面内容加入`/etc/X11/xorg.conf.d/10-evdev.conf`,将 fr 替换为您要使用的键盘

 `/etc/X11/xorg.conf.d/10-evdev.conf` 
```
Section "InputClass"
        Identifier "evdev keyboard catchall"
        MatchIsKeyboard "on"
        MatchDevicePath "/dev/input/event*"
        Driver "evdev"
        **Option "XkbLayout" "fr"**
EndSection
```

**警告:** 加入`**keyboard** InputClass` 段，而不是 pointer 段。

#### GDM在设置自动登录后无法启动

编辑 `/etc/gdm/custom.conf`，注释掉"AutomaticLoginEnable" 和 "AutomaticLogin".

```
# GDM configuration storage

[daemon]

#AutomaticLoginEnable=True
#AutomaticLogin=user
...
EndSection
```

## 参阅

*   [GDM Reference Manual](https://help.gnome.org/admin/gdm/stable/index.html.en)