Reflector 是一个脚本程序，从[镜像状态](https://www.archlinux.org/mirrors/status/)页面获取镜像列表，过滤出还在更新的页面并根据速度排列，然后覆盖文件`/etc/pacman.d/mirrorlist`。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 用法](#.E7.94.A8.E6.B3.95)
    *   [2.1 示例](#.E7.A4.BA.E4.BE.8B)
    *   [2.2 Systemd Service](#Systemd_Service)
    *   [2.3 Systemd 定时](#Systemd_.E5.AE.9A.E6.97.B6)
        *   [2.3.1 AUR](#AUR)
            *   [2.3.1.1 reflector-timer](#reflector-timer)
            *   [2.3.1.2 reflector-timer-weekly](#reflector-timer-weekly)

## 安装

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装")软件包 [reflector](https://www.archlinux.org/packages/?name=reflector)。

## 用法

**警告:**

*   在下面的例子中, `/etc/pacman.d/mirrorlist` 会被覆盖。在运行之前请先备份。
*   同步或更新 [Pacman](/index.php/Pacman "Pacman")前请确保 `/etc/pacman.d/mirrorlist`不包含任何奇怪的内容.

To see all of the available commands, run the following command:

```
# reflector --help

```

### 示例

通过下载速度进行排序，筛选前五位镜像并写入到`/etc/pacman.d/mirrorlist`:

```
# reflector --verbose -l 5 --sort rate --save /etc/pacman.d/mirrorlist

```

Verbosely rate the 200 most recently synchronized HTTP servers, sort them by download rate, and overwrite the file `/etc/pacman.d/mirrorlist`:

```
# reflector --verbose -l 200 -p http --sort rate --save /etc/pacman.d/mirrorlist

```

Verbosely rate the 200 most recently synchronized HTTPS servers located in the US, sort them by download rate, and overwrite the file `/etc/pacman.d/mirrorlist`:

```
# reflector --verbose --country 'United States' -l 200 -p https --sort rate --save /etc/pacman.d/mirrorlist

```

### Systemd Service

 `/etc/systemd/system/reflector.service` 
```
[Unit]
Description=Pacman mirrorlist update

[Service]
Type=oneshot
ExecStart=/usr/bin/reflector --protocol https --latest 30 --number 20 --sort rate --save /etc/pacman.d/mirrorlist

```

Then [starting](/index.php/Start "Start") `reflector.service` will update your mirrorlist.

To update your mirrorlist every time your computer boots you can enable the following service definition.

 `/etc/systemd/system/reflector.service` 
```
[Unit]
Description=Pacman mirrorlist update
Requires=network-online.target
After=network-online.target

[Service]
Type=oneshot
ExecStart=/usr/bin/reflector --protocol https --latest 30 --number 20 --sort rate --save /etc/pacman.d/mirrorlist

[Install]
RequiredBy=multi-user.target

```

Make sure you [activate the appropriate services](http://www.freedesktop.org/wiki/Software/systemd/NetworkTarget/) so that `network.target` really reflects your network status.

### Systemd 定时

如果你想每周一次运行 `reflector.service`:

 `/etc/systemd/system/reflector.timer` 
```
[Unit]
Description=Run reflector weekly

[Timer]
OnCalendar=weekly
RandomizedDelaySec=12h
Persistent=true

[Install]
WantedBy=timers.target

```

然后仅需 [启动](/index.php/Start "Start")`reflector.timer`.

#### AUR

[Install](/index.php/Install "Install") the [reflector-timer](https://aur.archlinux.org/packages/reflector-timer/) package to run *reflector* daily, or install the [reflector-timer-weekly](https://aur.archlinux.org/packages/reflector-timer-weekly/) to run it weekly.

##### reflector-timer

The default configuration is:

 `/usr/share/reflector-timer/reflector.conf` 
```
AGE=6
COUNTRY=Germany
LATEST=30
NUMBER=20
SORT=rate

```

To override this configuration, edit `/etc/conf.d/reflector.conf`:

 `/etc/conf.d/reflector.conf` 
```
COUNTRY=US

```

Be sure to [enable](/index.php/Enable "Enable") `reflector.timer`.

##### reflector-timer-weekly

The default configuration is:

 `/etc/reflector.conf` 
```
--save /etc/pacman.d/mirrorlist
--country China
--sort rate

```

Each line (except that begins with '#') should be valid `reflector` option.

Be sure to [enable](/index.php/Enable "Enable") `reflector.timer`.