[深度桌面环境](https://www.deepin.org/dde/) (Deepin Desktop Environment, DDE) 是 Linux 发行版 Deepin 的桌面环境。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 安装](#安装)
*   [2 启动](#启动)
    *   [2.1 通过显示管理器](#通过显示管理器)
    *   [2.2 通过 xinit](#通过_xinit)
*   [3 配置](#配置)
    *   [3.1 自定义触摸板手势](#自定义触摸板手势)
*   [4 故障排除](#故障排除)
    *   [4.1 从待机状态恢复后没有背景](#从待机状态恢复后没有背景)
    *   [4.2 无线网络无法连接](#无线网络无法连接)
*   [5 报告 Bug](#报告_Bug)

## 安装

如果你想安装一个最小化的 DDE，[安装](/index.php/Help:Reading_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E5.AE.89.E8.A3.85.E8.BD.AF.E4.BB.B6.E5.8C.85 "Help:Reading (简体中文)") [deepin](https://www.archlinux.org/groups/x86_64/deepin/) 组即可。这将安装所有基础组件。

[deepin-extra](https://www.archlinux.org/groups/x86_64/deepin-extra/) 组包含了一些额外的应用程序来提供一个更完整的桌面环境。

要能够使用内置的网络管理，需要安装 [networkmanager](https://www.archlinux.org/packages/?name=networkmanager) 包，并且 `NetworkManager.service` 需要被 [激活并设为开机自启](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E4.BD.BF.E7.94.A8.E5.8D.95.E5.85.83 "Systemd (简体中文)")。

## 启动

### 通过显示管理器

要使用 DDE 默认的 lightdm greeter，你必须修改 `[Seat:*]` 部分下的配置文件以声明：

 `/etc/lightdm/lightdm.conf` 
```
[Seat:*]
...
greeter-session=lightdm-deepin-greeter
```

需要注意的是，非 root 用户需要存在有效的主目录才能使 greeter 工作。

### 通过 xinit

要通过 [xinit](/index.php/Xinit_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Xinit (简体中文)") 使用 DDE，你需要添加一下内容到你的 .xinitrc 文件。

 `~/.xinitrc`  `exec startdde` 

Execute `startx` or `xinit` to start DDE.

**Note:** 如果你想在开机时自动启动xorg，请参阅 [Start X at login](/index.php/Start_X_at_login "Start X at login") .

## 配置

### 自定义触摸板手势

deepin官方没有提供自定义触摸板手势，但我们可以通过修改配置文件的方式来自定义触摸板。

配置文件目录：

```
/usr/share/dde-daemon/gesture.json

```

设置完后注销或重启使其生效

## 故障排除

### 从待机状态恢复后没有背景

由于 NVIDIA 驱动存储其 FBO 的方式[[1]](https://devtalk.nvidia.com/default/topic/787748/linux/-nvidia340xx-archlinux64-gnome3-14-the-background-of-desktop-and-lockscreen-mess-after-resume-from-/post/4367179/#4367179)，从待机状态下恢复后背景突然消失，仅留下一个可能带有一些颜色噪音的白色屏幕。这个 bug 似乎在 GNOME 上游被修复，但在 DDE 中仍然存在。

一个可能的解决方法是在每次计算机从待机中恢复时重启窗口管理器。完成这项任务的一个方式是创建下列的 systemd 服务

 `/etc/systemd/system/resume@.service` 
```
[Unit]
Description=User resume actions
After=suspend.target

[Service]
User=%I
Type=simple
ExecStart=/usr/bin/deepin-wm-restart.sh

[Install]
WantedBy=suspend.target

```

来运行下列的脚本

 `/usr/bin/deepin-wm-restart.sh` 
```
#!/bin/bash
export DISPLAY=:0
deepin-wm --replace

```

一旦在正确的目录中创建了这两个文件，要启用这个脚本，只需要运行这些命令：

```
# chmod +x /usr/bin/deepin-wm-restart.sh
# systemctl enable resume@*user*
# systemctl start resume@*user* 

```

第一个命令使你创建的脚本可执行，第二个命令确保服务始终在开机时启动，最后一个命令使服务立即启动，因此你可以测试解决方法而无需重启。

### 无线网络无法连接

网络管理器会随即生成并设置MAC地址。这是默认选项，如果要禁止它，将下面的几行加入到网络管理器的配置文件中。

 `/etc/NetworkManager/NetworkManager.conf` 
```
[device]
wifi.scan-rand-mac-address=no

```

## 报告 Bug

任何上游或 Arch 打包相关 bug 应在 [这里](https://github.com/linuxdeepin/developer-center/issues) 报告。所有的深度开发人员将看见 bug 报告并且尽可能快地解决它们。