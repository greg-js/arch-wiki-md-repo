Related articles

*   [Power management/Suspend and hibernate](/index.php/Power_management/Suspend_and_hibernate "Power management/Suspend and hibernate")
*   [Display Power Management Signaling](/index.php/Display_Power_Management_Signaling "Display Power Management Signaling")
*   [CPU frequency scaling](/index.php/CPU_frequency_scaling "CPU frequency scaling")
*   [Hybrid graphics](/index.php/Hybrid_graphics "Hybrid graphics")
*   [Kernel modules](/index.php/Kernel_modules "Kernel modules")
*   [sysctl](/index.php/Sysctl "Sysctl")
*   [udev](/index.php/Udev "Udev")

[电源管理](https://en.wikipedia.org/wiki/Power_management "wikipedia:Power management")这个功能可以在系统组件不工作时切断其电源或将其切换到低耗电模式。

Arch 中的电源管理包含两个主要部分：

1.  配置与硬件交互的内核
    *   [Kernel parameters](/index.php/Kernel_parameters "Kernel parameters")
    *   [Kernel modules](/index.php/Kernel_modules "Kernel modules")
    *   [udev](/index.php/Udev "Udev") rules
2.  配置用户空间工具，这些工具与内核交互，很多用户空间的工具，配置界面更友好。

## Contents

*   [1 用户空间工具](#.E7.94.A8.E6.88.B7.E7.A9.BA.E9.97.B4.E5.B7.A5.E5.85.B7)
*   [2 用 systemd 进行电源管理](#.E7.94.A8_systemd_.E8.BF.9B.E8.A1.8C.E7.94.B5.E6.BA.90.E7.AE.A1.E7.90.86)
    *   [2.1 ACPI 事件](#ACPI_.E4.BA.8B.E4.BB.B6)
    *   [2.2 电源管理器](#.E7.94.B5.E6.BA.90.E7.AE.A1.E7.90.86.E5.99.A8)
        *   [2.2.1 xss-lock](#xss-lock)
    *   [2.3 休眠和挂起](#.E4.BC.91.E7.9C.A0.E5.92.8C.E6.8C.82.E8.B5.B7)
        *   [2.3.1 混合休眠](#.E6.B7.B7.E5.90.88.E4.BC.91.E7.9C.A0)
    *   [2.4 休眠钩子](#.E4.BC.91.E7.9C.A0.E9.92.A9.E5.AD.90)
        *   [2.4.1 使用服务文件](#.E4.BD.BF.E7.94.A8.E6.9C.8D.E5.8A.A1.E6.96.87.E4.BB.B6)
        *   [2.4.2 合并待机和唤醒服务文件](#.E5.90.88.E5.B9.B6.E5.BE.85.E6.9C.BA.E5.92.8C.E5.94.A4.E9.86.92.E6.9C.8D.E5.8A.A1.E6.96.87.E4.BB.B6)
        *   [2.4.3 延迟休眠服务文件](#.E5.BB.B6.E8.BF.9F.E4.BC.91.E7.9C.A0.E6.9C.8D.E5.8A.A1.E6.96.87.E4.BB.B6)
            *   [2.4.3.1 使用 /usr/lib/systemd/system-sleep 钩子](#.E4.BD.BF.E7.94.A8_.2Fusr.2Flib.2Fsystemd.2Fsystem-sleep_.E9.92.A9.E5.AD.90)

## 用户空间工具

使用这些工具可以简化配置，因为它们的工作方式基本类似，所以请勿同时运行多个程序，以避免冲突。更多电源管理选型请参考 [power management category](/index.php/Category:Power_management "Category:Power management")。下面是一些比较流行的省电工具

*   **aclidswitch** — 简单的电源管理工具，可以根据笔记本是否交流供电定制屏幕翻转、亮度和省电模式。

	[https://github.com/orschiro/aclidswitch](https://github.com/orschiro/aclidswitch) || [aclidswitch-git](https://aur.archlinux.org/packages/aclidswitch-git/)

*   **[acpid](/index.php/Acpid "Acpid")** — 一个支持 netlink 的 ACPI 电源管理事件分发进程。

	[http://sourceforge.net/projects/acpid2/](http://sourceforge.net/projects/acpid2/) || [acpid](https://www.archlinux.org/packages/?name=acpid)

*   **[Laptop Mode Tools](/index.php/Laptop_Mode_Tools "Laptop Mode Tools")** — 配置笔记本电源设置的工具，很多人将其视为省电标准工具，需要的配置比较多。

	[https://github.com/rickysarraf/laptop-mode-tools](https://github.com/rickysarraf/laptop-mode-tools) || [laptop-mode-tools](https://aur.archlinux.org/packages/laptop-mode-tools/)

*   **[pm-utils](/index.php/Pm-utils "Pm-utils")** — 休眠和省电工具(已经停止开发).

	[http://pm-utils.freedesktop.org/](http://pm-utils.freedesktop.org/) || [pm-utils](https://aur.archlinux.org/packages/pm-utils/)

*   **[powertop](/index.php/Powertop "Powertop")** — 检查电源消耗和电源管理的工具，可以协助省电模式的配置。

	[https://01.org/powertop/](https://01.org/powertop/) || [powertop](https://www.archlinux.org/packages/?name=powertop)

*   [systemd](/index.php/Systemd "Systemd")
*   **[TLP](/index.php/TLP "TLP")** — Linux 高级电源管理

	[http://linrunner.de/tlp](http://linrunner.de/tlp) || [tlp](https://www.archlinux.org/packages/?name=tlp)

## 用 systemd 进行电源管理

### ACPI 事件

**systemd** 能够处理某些电源相关的 [ACPI](https://en.wikipedia.org/wiki/Advanced_Configuration_and_Power_Interface "wikipedia:Advanced Configuration and Power Interface") 事件，通过 `/etc/systemd/logind.conf` 或 `/etc/systemd/logind.conf.d/*.conf` 进行配置，请参考 [logind.conf(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/logind.conf.5). 如果系统没有专门的电源管理程序，systemd 可以替换掉原本用来响应这些 ACPI 事件的 [acpid](/index.php/Acpid "Acpid")。

事件的动作可以是 `ignore`, `poweroff`, `reboot`, `halt`, `suspend`, `hibernate`, `hybrid-sleep`, `lock` 或 `kexec`. 休眠或挂起动作需要被正确 [设置](/index.php/Power_management/Suspend_and_hibernate "Power management/Suspend and hibernate"). 如果没有配置事件动作，*systemd* 会使用默认动作。

| 事件处理程序 | 描述 | 默认动作 |
| `HandlePowerKey` | 按下电源键后的动作 | `poweroff` |
| `HandleSuspendKey` | 按下挂起键后的动作 | `suspend` |
| `HandleHibernateKey` | 按下休眠键后触发的动作 | `hibernate` |
| `HandleLidSwitch` | 笔记本翻盖后触发的动作，除了下面的情况 | `suspend` |
| `HandleLidSwitchDocked` | 如果笔记本放到了扩展坞或连接了多个显示器时，笔记本翻盖合上时触发的动作 | `ignore` |

修改后需要运行 `systemctl restart systemd-logind` 使上述更改生效。

**注意:** systemd 无法处理交流电源和电池 ACPI 事件，所以还得使用 [Laptop Mode Tools](/index.php/Laptop_Mode_Tools_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Laptop Mode Tools (简体中文)") 或 [acpid](/index.php/Acpid_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Acpid (简体中文)") 工具。

### 电源管理器

有些 [桌面环境](/index.php/Desktop_environment "Desktop environment") 包含的电源管理器会 [禁用](http://www.freedesktop.org/wiki/Software/systemd/inhibit/)(临时关闭) 某些或全部 *systemd* ACPI 设置。这些电源管理器运行时，请在它们的设置中配置 ACPI 事件的动作，只有不被禁用的事件才能在 `/etc/systemd/logind.conf` 或 `/etc/systemd/logind.conf.d/*.conf` 中配置。

如果电源管理器没有禁用 *systemd* 的事件动作，可能出现 *systemd* 挂起了系统，然后当系统被唤醒之后，电源管理器又再次将系统挂起的情况。截止到 2016 年 12 月，[KDE](/index.php/KDE "KDE"), [GNOME](/index.php/GNOME "GNOME"), [Xfce](/index.php/Xfce "Xfce") 和 [MATE](/index.php/MATE "MATE") 的电源管理器会执行需要的禁用命令。在使用 [acpid](/index.php/Acpid "Acpid") 或其它程序处理 ACPI 事件时，响应的 systemd 动作没有被禁用，可以将 `Handle` 设置为 `ignore`. 请参考 [systemd-inhibit(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-inhibit.1).

#### xss-lock

[xss-lock-git](https://aur.archlinux.org/packages/xss-lock-git/) 订阅 systemd 的 `suspend`, `hibernate`, `lock-session` 和 `unlock-session` 事件，并执行对应的动作(运行屏幕锁定并等待用户解锁或停止锁定). *xss-lock* 还会响应 [DPMS](/index.php/DPMS "DPMS") 事件并执行屏幕锁定和解锁动作。

下面命令可以 [自动启动](/index.php/Autostart "Autostart") xss-lock:

```
xss-lock -- i3lock -n -i *background_image.png* &

```

### 休眠和挂起

*systemd* 提供了挂起到内存，挂起到硬盘和混合休眠命令，使用内核的原生挂起和休眠功能执行响应的动作。systemd 还提供了在休眠前和唤醒后执行自定义动作的机制。除了内核默认的待机支持后端，systemd 也可以使用其他后端（比如 [Uswsusp](/index.php/Uswsusp "Uswsusp") 或 [TuxOnIce](/index.php/TuxOnIce "TuxOnIce")）。

`systemctl suspend` 应该不许要额外的配置，要使用 `systemctl hibernate`，需要先按照 [Suspend and hibernate#Hibernation](/index.php/Suspend_and_hibernate#Hibernation "Suspend and hibernate") 进行设置。

#### 混合休眠

`systemctl hybrid-sleep` 同时执行休眠和挂起，这样如果计算机突然断电(交流电源被拔掉或电池耗尽)，将会从硬盘休眠中恢复。如果没有断电，将从内存挂起中恢复，速度比从硬盘恢复快。因为 "hybrid-sleep" 需要将内存转存到交换空间，所以进入睡眠的时间比 `systemctl suspend` 慢。另外一个选择是使用延迟休眠功能。

### 休眠钩子

使用 `systemctl suspend`、`systemctl hibernate` 或 `systemctl hybrid-sleep` 命令执行待机/休眠时，systemd 不会调用 [pm-utils](/index.php/Pm-utils_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pm-utils (简体中文)")。[pm-utils](/index.php/Pm-utils_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pm-utils (简体中文)") 的钩子扩展（hook）——包括 [自定义钩子](/index.php/Pm-utils_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E5.BB.BA.E7.AB.8B.E4.BD.A0.E8.87.AA.E5.B7.B1.E7.9A.84.E9.92.A9.E5.AD.90 "Pm-utils (简体中文)")——会失效。不过，systemd 提供了两种类似的待机/休眠时执行脚本的机制。

##### 使用服务文件

可以将服务文件附在 suspend.target、hibernate.target 或 sleep.target 中，这样就能在待机/休眠前后执行某些操作。用户级操作和root/系统级操作应该使用不同的服务文件。要启用用户级服务文件，使用 `# systemctl enable suspend@<用户名> && systemctl enable resume@<用户名>`。例如：

 `/etc/systemd/system/suspend@.service` 
```
[Unit]
Description=User suspend actions
Before=sleep.target

[Service]
User=%I
Type=forking
Environment=DISPLAY=:0
ExecStartPre= -/usr/bin/pkill -u %u unison ; /usr/local/bin/music.sh stop ; /usr/bin/mysql -e 'slave stop'
ExecStart=/usr/bin/sflock
ExecStartPost=/usr/bin/sleep 1

[Install]
WantedBy=sleep.target
```
 `/etc/systemd/system/resume@.service` 
```
[Unit]
Description=User resume actions
After=suspend.target

[Service]
User=%I
Type=simple
ExecStartPre=/usr/local/bin/ssh-connect.sh
ExecStart=/usr/bin/mysql -e 'slave start'

[Install]
WantedBy=suspend.target
```

**Note:** As screen lockers may return before the screen is "locked", the screen may flash on resuming from suspend. Adding a small delay via `ExecStartPost=/usr/bin/sleep 1` helps prevent this.

root/系统级服，使用 `root-suspend` 或 `root-resume` 激活：

 `/etc/systemd/system/root-resume.service` 
```
[Unit]
Description=Local system resume actions
After=suspend.target

[Service]
Type=simple
ExecStart=/usr/bin/systemctl restart mnt-media.automount

[Install]
WantedBy=suspend.target
```
 `/etc/systemd/system/root-suspend.service` 
```
[Unit]
Description=Local system suspend actions
Before=sleep.target

[Service]
Type=simple
ExecStart=-/usr/bin/pkill sshfs

[Install]
WantedBy=sleep.target
```

上述服务文件的一些解释（详见 [systemd.service(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.service.5)）：

*   如果设置 `Type=OneShot`，那么可以使用多个 `ExecStart=` 参数。否则只能写一个，替代方案是在 `ExecStartPre` 中添加命令，或使用分号分隔不同命令（见第一个例子，分号前后的空格都是**必须**的）。
*   若命令前加上一个“-”（半角减号），则命令返回非零值时会被忽略、当作正常执行处理。
*   有关调试，最好的方法是用 `journalctl` 查看日志。

##### 合并待机和唤醒服务文件

利用下面这种自定义的一体化待机和唤醒服务，使用单一的钩子扩展即可对不同操作（待机/休眠/混合休眠）的不同阶段（进入/唤醒）进行控制。

例子和解释：

 `/etc/systemd/system/wicd-sleep.service` 
```
[Unit]
Description=Wicd sleep hook
Before=sleep.target
StopWhenUnneeded=yes

[Service]
Type=oneshot
RemainAfterExit=yes
ExecStart=-/usr/share/wicd/daemon/suspend.py
ExecStop=-/usr/share/wicd/daemon/autoconnect.py

[Install]
WantedBy=sleep.target
```

*   `RemainAfterExit=yes`：服务启动后，除非显式地停止，否则就认为是活动的。
*   `StopWhenUnneeded=yes`：服务活动时，如果无其他服务依赖该服务，就停止它。在本例中，该服务会在 sleep.target 停止后停止活动。
*   由于 sleep.target 会被 suspend.target、hibernate.target、hybrid-sleep.target 调用，且 sleep.target 本身设置了 StopWhenUnneeded，该服务文件对以上各种操作都是有效的。

#### 延迟休眠服务文件

An alternative approach is delayed hibernation. This makes use of sleep hooks to suspend as usual but sets a timer to wake up later to perform hibernation. Here, entering sleep is faster than `systemctl hybrid-sleep` since no hibernation is performed initially. However, unlike "hybrid-sleep", at this point there is no protection against power loss via hibernation while in suspension. This caveat makes this approach more suitable for laptops than desktops. Since hibernation is delayed, the laptop battery is only used during suspension and to trigger the eventual hibernation. This uses less power over the long-term than a "hybrid-sleep" which will remain suspended until the battery is drained. Note that if your laptop has a spinning hard disk, when it wakes up from suspend in order to hibernate, you may not want to be moving or carrying the laptop for these few seconds. Delayed hibernation may be desirable both to reduce power use as well as for security reasons (e.g. when using full disk encryption). An example script is located [here](http://superuser.com/questions/298672/linuxhow-to-hibernate-after-a-period-of-sleep). See also [this post](https://bbs.archlinux.org/viewtopic.php?pid=1420279#p1420279) for an updated systemd sleep hook.

A slightly updated version of the service is:

 `/etc/systemd/system/suspend-to-hibernate.service` 
```
[Unit]
Description=Delayed hibernation trigger
Documentation=https://bbs.archlinux.org/viewtopic.php?pid=1420279#p1420279
Documentation=https://wiki.archlinux.org/index.php/Power_management
Conflicts=hibernate.target hybrid-sleep.target
Before=sleep.target
StopWhenUnneeded=true

[Service]
Type=oneshot
RemainAfterExit=yes
Environment="WAKEALARM=/sys/class/rtc/rtc0/wakealarm"
Environment="SLEEPLENGTH=+2hour"
ExecStart=-/usr/bin/sh -c 'echo -n "alarm set for "; date +%%s -d$SLEEPLENGTH | tee $WAKEALARM'
ExecStop=-/usr/bin/sh -c '\
  alarm=$(cat $WAKEALARM); \
  now=$(date +%%s); \
  if [ -z "$alarm" ] || [ "$now" -ge "$alarm" ]; then \
     echo "hibernate triggered"; \
     systemctl hibernate; \
  else \
     echo "normal wakeup"; \
  fi; \
  echo 0 > $WAKEALARM; \
'

[Install]
WantedBy=sleep.target

```

The `Before` and `Conflicts` options ensure it only is run for suspension and not hibernation--otherwise the service will run twice if delayed hibernation is triggered. The `WantedBy` and `StopWhenUnneeded` options are so it is started before sleep and stops upon resume. (Note that the `suspend.target` and `hibernate.target` targets do not stop when unneeded, but `sleep.target` does). [Enable](/index.php/Enable "Enable") the service.

##### 使用 /usr/lib/systemd/system-sleep 钩子

systemd 在待机/休眠时执行 `/usr/lib/systemd/system-sleep/` 里的所有脚本，传递下面两个参数：

*   参数1：若是准备进入待机/休眠状态，则为 `pre`；唤醒时为 `post`。
*   参数2：事件名称，`suspend`，`hibernate` 或 `hybrid-sleep`。

systemd 会同时执行所有脚本，而不是像 [pm-utils](/index.php/Pm-utils_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pm-utils (简体中文)") 那样顺序执行。

脚本输出会记录在相关服务（`systemd-suspend.service`、`systemd-hibernate.service` 或 `systemd-hybrid-sleep.service`）中。通过[日志](#.E6.97.A5.E5.BF.97)查看：

```
# journalctl -b -u systemd-suspend

```

**注意:** 除了使用自定义脚本，还可以利用 `sleep.target`、`suspend.target`、`hibernate.target` 或 `hybrid-sleep.target` 来为单元（unit）添加睡眠状态策略。

脚本示范：

 `/usr/lib/systemd/system-sleep/example.sh` 
```
#!/bin/sh
case $1/$2 in
  pre/*)
    echo "进入 $2 状态..."
    ;;
  post/*)
    echo "从 $2 状态唤醒..."
    ;;
esac
```

记得添加可执行权限：

1.  chmod a+x /usr/lib/systemd/system-sleep/example.sh

详情参见 [systemd.special(7)](http://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.special.7) 和 [systemd-sleep(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-sleep.8)。