**systemd** 能够处理某些电源相关的 [ACPI](https://en.wikipedia.org/wiki/Advanced_Configuration_and_Power_Interface "wikipedia:Advanced Configuration and Power Interface") 事件，通过 `/etc/systemd/logind.conf` 的下列选项配置：

*   `HandlePowerKey`：按下电源键后的动作
*   `HandleSleepKey`：按下挂起键后的动作
*   `HandleHibernateKey`: 按下休眠键后的动作
*   `HandleLidSwitch`：合上笔记本盖后待机

动作可以是 `ignore`、`poweroff`、`reboot`、`halt`、`suspend`、`hibernate`、`hybrid-sleep`、`lock` 或 `kexec`。

系统默认设置为:

```
HandlePowerKey=poweroff
HandleSuspendKey=suspend
HandleHibernateKey=hibernate
HandleLidSwitch=suspend

```

不用图形界面、或者使用 [i3](/index.php/I3_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "I3 (简体中文)")、[awesome](/index.php/Awesome_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Awesome (简体中文)") 这样简单的桌面管理器时，systemd 可以替代 [acpid](/index.php/Acpid_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Acpid (简体中文)") 处理 ACPI 事件。

**注意:** 运行 `systemctl restart systemd-logind`，使上述更改立即生效。

**注意:** systemd 无法处理交流电源和电池 ACPI 事件，所以还得使用 [Laptop Mode Tools](/index.php/Laptop_Mode_Tools_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Laptop Mode Tools (简体中文)") 或 [acpid](/index.php/Acpid_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Acpid (简体中文)") 工具。

在当前版本的 systemd 中，这些 `Handle` 选项将会被应用到整个系统当中，除非它们被别的程序——例如某个桌面环境中的电源管理器——给“阻止”（inhibited）。如果其它的程序没有阻止这些 `Handle` ，你可能会先被 systemd 挂起你的系统，然后当系统被唤醒之后，电源管理器又会再次将系统挂起。

**警告:** 目前只有[GNOME](/index.php/GNOME "GNOME") 和 [KDE](/index.php/KDE "KDE") 支持 "inhibited" 命令。在其它的桌面管理器同样实现该功能之前，如果你想使用[Xfce](/index.php/Xfce "Xfce")、[acpid](/index.php/Acpid "Acpid") 或者其它程序来管理 ACPI 事件，你需要把 `Handle` 选项设置为 `ignore`。

**注意:** 除了内核默认的待机支持后端（用于处理待机/休眠），systemd 也可以使用其他后端（比如 [Uswsusp](/index.php/Uswsusp "Uswsusp") 或 [TuxOnIce](/index.php/TuxOnIce "TuxOnIce")）。

要令 `systemctl hibernate` 工作，需要按照[休眠](/index.php/Pm-utils#Hibernation_.28suspend2disk.29 "Pm-utils")和 [mkinitcpio 唤醒扩展](/index.php/Pm-utils#Mkinitcpio_Resume_Hook "Pm-utils")的设置步骤进行操作。（不必安装 `pm-utils`）

## Contents

*   [1 休眠时执行的脚本](#.E4.BC.91.E7.9C.A0.E6.97.B6.E6.89.A7.E8.A1.8C.E7.9A.84.E8.84.9A.E6.9C.AC)
    *   [1.1 使用服务文件](#.E4.BD.BF.E7.94.A8.E6.9C.8D.E5.8A.A1.E6.96.87.E4.BB.B6)
    *   [1.2 合并待机和唤醒服务文件](#.E5.90.88.E5.B9.B6.E5.BE.85.E6.9C.BA.E5.92.8C.E5.94.A4.E9.86.92.E6.9C.8D.E5.8A.A1.E6.96.87.E4.BB.B6)
    *   [1.3 使用 /usr/lib/systemd/system-sleep](#.E4.BD.BF.E7.94.A8_.2Fusr.2Flib.2Fsystemd.2Fsystem-sleep)

#### 休眠时执行的脚本

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

至于root/系统级服务（使用 `# systemctl enable root-suspend` 激活）：

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

##### 使用 /usr/lib/systemd/system-sleep

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