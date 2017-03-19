**翻译状态：** 本文是英文页面 [Thinkpad Fan Control](/index.php/Thinkpad_Fan_Control "Thinkpad Fan Control") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-03-18，点击[这里](https://wiki.archlinux.org/index.php?title=Thinkpad+Fan+Control&diff=0&oldid=471075)可以查看翻译后英文页面的改动。

在默认情况下由内嵌控制器控制风扇转速。如果您认为风扇转速过低或过大，您可能需要一个守护进程接管控制权。但这是有风险的：您需要负责控制温度。过高的温度会损坏或者缩短笔记本组件的使用寿命。

来自 [http://www.thinkwiki.org/wiki/How_to_control_fan_speed：](http://www.thinkwiki.org/wiki/How_to_control_fan_speed：)

	*出于安全考虑，默认禁止用户控制风扇。若想启用风扇控制，必须在加载内核模块　thinkpad-acpi 时传递参数 fan_control=1*

当前可用于控制风扇的守护进程存在于 [Arch User Repository (简体中文)](/index.php/Arch_User_Repository_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch User Repository (简体中文)") 中， 分别是 [simpfand-git](https://aur.archlinux.org/packages/simpfand-git/) 和 [thinkfan](https://aur.archlinux.org/packages/thinkfan/)。

## 安装

安装 [thinkfan](https://aur.archlinux.org/packages/thinkfan/)。然后查看其文件列表：

```
# pacman -Ql thinkfan

```

请注意 thinkfan 包安装了文件 /usr/lib/modprobe.d/thinkpad_acpi.conf，该文件包含：

```
options thinkpad_acpi fan_control=1

```

因此，默认启用了风扇控制。

```
$ su
# modprobe thinkpad_acpi
# cat /proc/acpi/ibm/fan

```

您应该会看到风扇运行级别默认为 “auto”，您可以向这个文件写入运行级别的方式手动控制风扇转速。thinkfan 守护进程将会自动控制风扇转速。

您需要复制一份默认配置文件（例如 /usr/share/doc/thinkfan/examples/thinkfan.conf.simple) 到 /etc/thinkfan.conf，并尝试修改它。需要在这个配置文件中指定读取哪些传感器，并且也需要指定用户控制风扇转速的接口。一些操作系统提供了 /proc/acpi/ibm/fan，对于其他操作系统，you will need to specify something like

```
hwmon /sys/devices/virtual/thermal/thermal_zone0/temp

```

to use generic hwmon sensors instead of thinkpad-specific ones.

## 运行

您可以通过手动运行 thinkfan 命令测试配置（root用户）：

```
# thinkfan -n

```

and see how it reacts to the load level of whatever other programs you have running.

当您的配置正确时，可通过如下命令启动 thinkfan 守护进程（root 用户）：

```
# systemctl start thinkfan

```

或者在系统启动时自动加载它：

```
# systemctl enable thinkfan

```

## Old packages which have gone missing

[tpfand](https://aur.archlinux.org/packages/tpfand/) and a version that doesn't require [HAL](/index.php/HAL "HAL") [tpfand-no-hal](https://aur.archlinux.org/packages/tpfand-no-hal/) are not actively developed anymore, and no longer available. An additional GTK+ frontend was provided in the [tpfan-admin](https://aur.archlinux.org/packages/tpfan-admin/) package in the [AUR](/index.php/AUR "AUR") which enables the monitoring of temperatures as well as the graphical adjustment of trigger points.

Due to tpfand not beeing actively developed anymore, there was a fork called tpfanco (which in fact uses the same names for the executables as tpfand): [tpfanco-svn](https://aur.archlinux.org/packages/tpfanco-svn/).

The configuration file for tpfand (same for tpfanco) was `/etc/tpfand.conf`.

Additionally, the [tpfand-profiles](https://aur.archlinux.org/packages/tpfand-profiles/) package in the [AUR](/index.php/AUR "AUR") provided the latest fan profiles for various thinkpad models.