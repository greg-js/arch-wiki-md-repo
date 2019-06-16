**翻译状态：** 本文是英文页面 [Redshift](/index.php/Redshift "Redshift") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2019-6-12，点击[这里](https://wiki.archlinux.org/index.php?title=Redshift&diff=0&oldid=575179)可以查看翻译后英文页面的改动。

来自 [Redshift project web page](http://jonls.dk/redshift/):

	[Redshift](https://en.wikipedia.org/wiki/Redshift_(software) 会根据你的周围环境调节屏幕色温，如果你晚上在屏幕前工作，这可能帮助你减少对眼睛的伤害。 这个程序启发于 [f.lux](http://justgetflux.com)。

**注意:** Redshift 不支持 [Wayland](/index.php/Wayland "Wayland") 因为它无法调节色温 [[1]](https://github.com/jonls/redshift/issues/55)。查看 [Wayland#Gamma](/index.php/Wayland#Gamma "Wayland") 了解更多。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 安装](#安装)
    *   [1.1 前端](#前端)
*   [2 使用](#使用)
    *   [2.1 快速开始](#快速开始)
    *   [2.2 自动启动](#自动启动)
*   [3 配置](#配置)
    *   [3.1 Automatic location based on GeoClue2](#Automatic_location_based_on_GeoClue2)
    *   [3.2 Automatic location based on GPS](#Automatic_location_based_on_GPS)
    *   [3.3 Use real screen brightness](#Use_real_screen_brightness)
*   [4 疑难解答](#疑难解答)
    *   [4.1 Screen 1 could not be found](#Screen_1_could_not_be_found)
    *   [4.2 点击托盘图表不工作](#点击托盘图表不工作)
    *   [4.3 Redshift 让屏幕在设置的色温值和默认的色温值之间快速闪烁](#Redshift_让屏幕在设置的色温值和默认的色温值之间快速闪烁)
    *   [4.4 Redshift 使用命令启动时可以工作 但是以 systemd service 启动失败](#Redshift_使用命令启动时可以工作_但是以_systemd_service_启动失败)
    *   [4.5 Redshift temporarily resets using some wine apps that reset gamma values](#Redshift_temporarily_resets_using_some_wine_apps_that_reset_gamma_values)
    *   [4.6 Redshift GDBus.Error:org.freedesktop.DBus.Error.AccessDenied on start](#Redshift_GDBus.Error:org.freedesktop.DBus.Error.AccessDenied_on_start)
*   [5 参见](#参见)

## 安装

安装 [redshift](https://www.archlinux.org/packages/?name=redshift) 包。或者安装 [redshift-minimal](https://aur.archlinux.org/packages/redshift-minimal/) 包（最小依赖版本）。

### 前端

*redshift-gtk* 命令 来自 [redshift](https://www.archlinux.org/packages/?name=redshift) 包 提供托盘图标用于控制 Redshift。 请参阅可选的依赖。

另外，也可以使用这些前端 [redshiftgui-bin](https://aur.archlinux.org/packages/redshiftgui-bin/) (GTK) 和 [redshift-qt](https://aur.archlinux.org/packages/redshift-qt/), [redshiftconf](https://aur.archlinux.org/packages/redshiftconf/) 或者 [plasma5-applets-redshift-control](https://www.archlinux.org/packages/?name=plasma5-applets-redshift-control) 和 [plasma5-applets-redshift-control-git](https://aur.archlinux.org/packages/plasma5-applets-redshift-control-git/) (Qt)。

## 使用

Redshift 需要你的位置才能开始运行 (除非使用 `-O` 选项)，即需要你所在位置的经纬度。Redshift 使用一些程序获得你的位置。如果这些程序不工作 (比如这些程序都没有安装), 你需要手动输入你的位置。

### 快速开始

以基本的设置启动：

```
$ redshift -l *LATITUDE*:*LONGITUDE*

```

*LATITUDE* 为所在位置的维度 ， *LONGITUDE* 为所在位置的经度。

立即更改屏幕色温：

```
$ redshift -P -O *TEMPERATURE*

```

*TEMPERATURE* 为期望的色温值 (介于 `1000` 和 `25000` 之间)。

### 自动启动

有几个选项可以自动启动Redshif：

*   鼠标右键点击托盘图标选择 *Autostart* 当 *redshift-gtk* 或者 *plasma5-applets-redshift-control* 已经启动的时候。
*   放置 Redshift [Desktop entry](/index.php/Desktop_entry "Desktop entry") 在 `~/.config/autostart/` 或通过添加 `redshift` 到你的窗口管理器或者桌面环境的 [Autostarting](/index.php/Autostarting "Autostarting") 方法中。
*   使用 [Systemd/User](/index.php/Systemd/User "Systemd/User")。 软件提供了两个 srvices: `redshift.service` 和 `redshift-gtk.service`。激活哪一个服务取决于你是否想要显示系统托盘图表。

**Note:**

*   The Redshift service files contain `Restart=always` so they will restart infinitely. See [systemd.service(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.service.5).
*   When using a systemd user service, [Xorg](/index.php/Xorg "Xorg") must be started before execution of the service, which is not the case without a [Display manager](/index.php/Display_manager "Display manager"). Otherwise you will get `RANDR Query Version' returned error -1` and `Initialization of randr failed`.

## 配置

Redshift 会读取配置文件 `~/.config/redshift/redshift.conf` [[2]](https://github.com/jonls/redshift/releases/tag/v1.12) （如果该文件存在的话）。 然而，Redshift 不会自动创建这个文件, 因此你可能需要手动创建它。配置文件示例：[redshift.conf.sample](https://raw.githubusercontent.com/jonls/redshift/master/redshift.conf.sample)。

### Automatic location based on GeoClue2

In order to allow access Redshift to use GeoClue2, add the following lines to `/etc/geoclue/geoclue.conf`:

 `/etc/geoclue/geoclue.conf` 
```
[redshift]
allowed=true
system=false
users=
```

[Restart](/index.php/Restart "Restart") `redshift.service` and/or any other Redshift instance to apply the changes.

**Note:**

*   This workaround is not needed with Geoclue2 version 2.5.0 and above.
*   If using [GNOME](/index.php/GNOME "GNOME"), also toggle Location Services to "On" in *Settings > Privacy*.
*   Due possible bugs with geoclue2 and Redshift [[3]](https://github.com/jonls/redshift/issues/318), it may be required to use the `manual` location-provider instead, e.g. for Paris:

 `~/.config/redshift/redshift.conf` 
```
[redshift]
...
; Set the location-provider: 'geoclue2', 'manual'
; type 'redshift -l list' to see possible values.
; The location provider settings are in a different section.
location-provider=manual

...

; Keep in mind that longitudes west of Greenwich (e.g. the Americas)
; are negative numbers.
[manual]
lat=48.853
lon=2.349
```

*   If using [i3wm](/index.php/I3wm "I3wm") or similar, you will also need to enable the geoclue agent on startup. As well as `systemctl --user enable redshift-gtk` or `redshift` user service.

 `~/.i3/config` 
```
...
exec --no-startup-id /usr/lib/geoclue-2.0/demos/agent
...
```

### Automatic location based on GPS

You can also use [gpsd](https://www.archlinux.org/packages/?name=gpsd) to automatically determine your [GPS](/index.php/GPS "GPS") location and use it as an input for Redshift. Create the following script and pass `$lat` and `$lon` to `redshift -l $lat;$lon`:

```
#!/bin/bash
date
#gpsdata=$( gpspipe -w -n 10 |   grep -m 1 lon )
gpsdata=$( gpspipe -w | grep -m 1 TPV )
lat=$( echo "$gpsdata"  | jsawk 'return this.lat' )
lon=$( echo "$gpsdata"  | jsawk 'return this.lon' )
alt=$( echo "$gpsdata"  | jsawk 'return this.alt' )
dt=$( echo "$gpsdata" | jsawk 'return this.time' )
echo "$dt"
echo "You are here: $lat, $lon at $alt"

```

For more information, see [this](https://bbs.archlinux.org/viewtopic.php?pid=1389735#p1389735) forums thread.

### Use real screen brightness

Redshift has a brightness adjustment setting, but it does not work the way most people might expect. In fact it is a fake brightness adjustment obtained by manipulating the gamma ramps, which means that it does not reduce the backlight of the screen. [[4]](http://jonls.dk/redshift/#known-bugs-and-limitations)

Changing screen backlight is possible with redshift hooks and [xorg-xrandr](https://www.archlinux.org/packages/?name=xorg-xrandr) and [xorg-xbacklight](https://www.archlinux.org/packages/?name=xorg-xbacklight) but, please see [Backlight#xbacklight](/index.php/Backlight#xbacklight "Backlight") as there are some limitations and you may have to find another method of controlling the backlight depending on your hardware.

You need to create a file in `~/.config/redshift/hooks` and make it executable. You can use and edit the following example:

```
$ mkdir -p ~/.config/redshift/hooks

```

Create and adjust the following script:

 `~/.config/redshift/hooks/brightness.sh` 
```
#!/bin/sh

# Set brightness via xbrightness when redshift status changes

# Set brightness values for each status.
# Range from 1 to 100 is valid
brightness_day=100
brightness_transition=50
brightness_night=10
# Set fade time for changes to one minute
fade_time=60000

if [ "$1" = period-changed ]; then
	case $3 in
		night)
			xbacklight -set $brightness_night -time $fade_time
			;;
		transition)
			xbacklight -set $brightness_transition -time $fade_time
			;;
		daytime)
			xbacklight -set $brightness_day -time $fade_time
			;;
	esac
fi
```

Make it [executable](/index.php/Executable "Executable"):

```
$ chmod +x ~/.config/redshift/hooks/brightness.sh

```

[Restart](/index.php/Restart "Restart") the `redshift.service` to apply changes.

Check the service status as it should **not** contain the following message:

```
redshift[..]: No outputs have backlight property

```

## 疑难解答

### Screen 1 could not be found

修改配置文件 "redshift.conf" 将 "screen 1" 改为 "screen 0"。

### 点击托盘图表不工作

安装 [libappindicator-gtk3](https://www.archlinux.org/packages/?name=libappindicator-gtk3)。 请看 [redshift issue 363](https://github.com/jonls/redshift/issues/363) and [FS#49971](https://bugs.archlinux.org/task/49971).

### Redshift 让屏幕在设置的色温值和默认的色温值之间快速闪烁

确认没有多个Redshift实例在同时运行。

### Redshift 使用命令启动时可以工作 但是以 systemd service 启动失败

[systemd](/index.php/Systemd "Systemd") unit 有一行在 `redshift.service` 文件中，要求必须在`display-manager.service` unit 被一个显示管理器 [display manager](/index.php/Display_manager "Display manager") 启动后才能启动。 如果你不使用显示管理器, 编辑 `redshift.service` 用户服务文件删除 `After=display-manager.service` 行. 运行 `systemctl --user daemon-reload` 后服务应该会正确初始化。

### Redshift temporarily resets using some wine apps that reset gamma values

If you notice that using some wine apps, redshift seems to reset temporarily upon launch, or adjusting settings, or etc, then there is a useful registry key that seems to alleviate this. See [[5]](https://www.winehq.org/pipermail/wine-bugs/2015-January/403770.html) and [[6]](https://wiki.winehq.org/UsefulRegistryKeys). Set or create the string value

 `HKEY_CURRENT_USER\Software\Wine\X11 Driver`  `UseXVidMode="N"` 

using the registry editor, or import/set it otherwise.

### Redshift GDBus.Error:org.freedesktop.DBus.Error.AccessDenied on start

If running `$ redshift` and you are getting:

 `$ redshift` 
```
Trying location provider `geoclue2'...
Using provider `geoclue2'.
Unable to start GeoClue client: GDBus.Error:org.freedesktop.DBus.Error.AccessDenied: 'redshift' disallowed, no agent for UID 1000.
Unable to connect to GeoClue.
Unable to get location from provider.

```

or running `$ redshift-gtk` and getting the similar error:

 `$ redshift-gtk` 
```
Failed to run Redshift
Trying location provider `geoclue2'...
Unable to start GeoClue client:
GDBus.Error:org.freedesktop.DBus.Error.AccessDenied:
'redshift' disallowed, no agent for UID 1000.
Unable to connect to GeoClue.
Unable to get location from provider.

```

You can create a [systemd](/index.php/Systemd "Systemd") unit file in `~/.config/systemd/user/geoclue-agent.service` with the following config:

 `~/.config/systemd/user/geoclue-agent.service` 
```
[Unit]
Description=redshift needs to get a (geo)clue

[Service]
ExecStart=/usr/lib/geoclue-2.0/demos/agent

[Install]
WantedBy=default.target
```

Start and enable the service with systemctl: `$ systemctl --user enable --now geoclue-agent.service` and try running redshift again.

If you still get the same error, it may be because of geoclue being locked down to a few programs by default. Try adding the following lines to `/etc/geoclue/geoclue.conf` (see [redshift issue 158](https://github.com/jonls/redshift/issues/158#issuecomment-71329118) and [FS#40360](https://bugs.archlinux.org/task/40360)) and run `$ redshift` again:

 `/etc/geoclue/geoclue.conf` 
```
[redshift]
allowed=true
system=false
users=
```

## 参见

*   [Redshift website](http://jonls.dk/redshift)
*   [Redshift on github](http://github.com/jonls/redshift)
*   [Wikipedia:Redshift (software)](https://en.wikipedia.org/wiki/Redshift_(software) "wikipedia:Redshift (software)")
*   Similar software: [[7]](https://github.com/jumper149/blugon) [blugon](https://aur.archlinux.org/packages/blugon/), [xflux-gui-git](https://aur.archlinux.org/packages/xflux-gui-git/)