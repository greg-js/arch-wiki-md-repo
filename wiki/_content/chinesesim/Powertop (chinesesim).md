**翻译状态：** 本文是英文页面 [Powertop](/index.php/Powertop "Powertop") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-09-25，点击[这里](https://wiki.archlinux.org/index.php?title=Powertop&diff=0&oldid=491174)可以查看翻译后英文页面的改动。

**PowerTOP** 是一个Intel提供的在用户空间、内核和硬件层面的节电工具。它可以监视进程，并显示哪些进程利用CPU并从空闲状态唤醒它，从而识别具有特殊高功率需求的应用程序。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 使用](#.E4.BD.BF.E7.94.A8)
    *   [2.1 保存设置](#.E4.BF.9D.E5.AD.98.E8.AE.BE.E7.BD.AE)
*   [3 疑难解决](#.E7.96.91.E9.9A.BE.E8.A7.A3.E5.86.B3)
    *   [3.1 Error: Cannot load from file](#Error:_Cannot_load_from_file)
    *   [3.2 校准测量数据](#.E6.A0.A1.E5.87.86.E6.B5.8B.E9.87.8F.E6.95.B0.E6.8D.AE)
*   [4 更多信息](#.E6.9B.B4.E5.A4.9A.E4.BF.A1.E6.81.AF)

## 安装

安装 [powertop](https://www.archlinux.org/packages/?name=powertop)。

## 使用

PowerTOP提供进一步降低功耗的方法。然而在控制台，PowerTOP不显示参数。

*   使用sudo或root用户运行`powertop`可进入powertop界面。

*   如果你使用powertop更改了设置，在系统重启后，这些设置将恢复原状态。

*   使用powertop生成一个参数报告： `# powertop --html=powerreport.html`

用浏览器阅览参数报告，可使用报告的“调整”选项卡查看该工具建议用于保存电源的实际参数。您可以使用`awk -F '</?td ?>' '/tune/ { print $4 }' powerreport.html`命令提取报告。

### 保存设置

有两种方法保存其设置，使其在重启后依然应用先前的设置。

*   使用 [Kernel modules (简体中文)](/index.php/Kernel_modules_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Kernel modules (简体中文)")、 [Udev (简体中文)](/index.php/Udev_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Udev (简体中文)") 和[sysctl](/index.php/Sysctl "Sysctl")来使其在系统启动时应用设置。相关细节请看[Power management (简体中文)](/index.php/Power_management_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Power management (简体中文)")。
*   使用poertop的 `--auto-tune` 参数，该参数会使得所有的可调整项变成GOOD,为使其在系统启动时就生效，可使用systemd 服务使其开启自启动。添加该文件：

 `/etc/systemd/system/powertop.service` 
```
[Unit]
Description=Powertop tunings

[Service]
ExecStart=/usr/bin/powertop --auto-tune
RemainAfterExit=true

[Install]
WantedBy=multi-user.target
```

然后执行：

```
 # systemctl enable powertop

```

## 疑难解决

### Error: Cannot load from file

如果在启动 powertop 时遇到如下错误，可能是因为 powertop 没有收集到足够的数据，请在电池供电的情况下多运行一段时间，收集更多的数据。

```
Loaded 39 prior measurements
Cannot load from file /var/cache/powertop/saved_parameters.powertop
Cannot load from file /var/cache/powertop/saved_parameters.powertop

```

### 校准测量数据

如果测量结果不准确，可能需要先校准 powertop: 运行 powertop 是增加 `--calibrate` 参数.

**Note:** 校准时会开关背光、wifi 等功能，再校准时不要触碰机器。

```
# powertop --calibrate

```

## 更多信息

*   [Official site](https://01.org/powertop/)
*   [Wikipedia article](https://en.wikipedia.org/wiki/Powertop "wikipedia:Powertop")