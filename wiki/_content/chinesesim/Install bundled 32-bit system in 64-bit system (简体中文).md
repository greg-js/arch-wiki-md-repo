**注意:** 这里的步骤不会试图改变 32 位目录之外的任何东西。要是发生了这样的事，那是糟糕的错误。

这个指南是写给那些确实需要运行 32 位程序并希望容易地安装它们的人。由于 Arch64 试图成为一个纯粹的 64 位发行版，开发者们不打算提供兼容库以便使系统干净些。现在虽然已经有了一些，但它们的 PKBGUILD 仅仅是下载 32 位二进制包并重新打包而成，并不是从源代码编译而来。所以，如果你想要重新编译这些包，你也需要这个32位子系统。

重要事项：如果你自定义了内核配置(config)，你需要确保“CONFIG_IA32_EMULATION=y”这个选项设置好。否则，该 64 位内核将不能访问这里的 32 位 chroot 环境。对原配的 Arch64 内核而言，这通常是默认选项。

## Contents

*   [1 安装基本的 32 位系统](#.E5.AE.89.E8.A3.85.E5.9F.BA.E6.9C.AC.E7.9A.84_32_.E4.BD.8D.E7.B3.BB.E7.BB.9F)
*   [2 Create an Arch32 Daemon Script and Systemd Service](#Create_an_Arch32_Daemon_Script_and_Systemd_Service)
*   [3 配置新系统](#.E9.85.8D.E7.BD.AE.E6.96.B0.E7.B3.BB.E7.BB.9F)
    *   [3.1 配置文件](#.E9.85.8D.E7.BD.AE.E6.96.87.E4.BB.B6)
    *   [3.2 配置 chroot](#.E9.85.8D.E7.BD.AE_chroot)
    *   [3.3 考虑清除软件包缓存](#.E8.80.83.E8.99.91.E6.B8.85.E9.99.A4.E8.BD.AF.E4.BB.B6.E5.8C.85.E7.BC.93.E5.AD.98)
*   [4 在 64 位环境下运行 32 位应用程序](#.E5.9C.A8_64_.E4.BD.8D.E7.8E.AF.E5.A2.83.E4.B8.8B.E8.BF.90.E8.A1.8C_32_.E4.BD.8D.E5.BA.94.E7.94.A8.E7.A8.8B.E5.BA.8F)
    *   [4.1 下载安装schroot](#.E4.B8.8B.E8.BD.BD.E5.AE.89.E8.A3.85schroot)
    *   [4.2 配置](#.E9.85.8D.E7.BD.AE)
    *   [4.3 运行 32 位应用程序](#.E8.BF.90.E8.A1.8C_32_.E4.BD.8D.E5.BA.94.E7.94.A8.E7.A8.8B.E5.BA.8F)
    *   [4.4 显示问题](#.E6.98.BE.E7.A4.BA.E9.97.AE.E9.A2.98)
    *   [4.5 发声](#.E5.8F.91.E5.A3.B0)
    *   [4.6 Firefox发声脚本示例](#Firefox.E5.8F.91.E5.A3.B0.E8.84.9A.E6.9C.AC.E7.A4.BA.E4.BE.8B)
    *   [4.7 wine 脚本示例](#wine_.E8.84.9A.E6.9C.AC.E7.A4.BA.E4.BE.8B)
    *   [4.8 注意事项](#.E6.B3.A8.E6.84.8F.E4.BA.8B.E9.A1.B9)
*   [5 另类安装方法](#.E5.8F.A6.E7.B1.BB.E5.AE.89.E8.A3.85.E6.96.B9.E6.B3.95)

## 安装基本的 32 位系统

首先创建 32 位子目录。

```
mkdir /opt/arch32

```

生成供子系统使用的 pacman 配置文件。注意，这里是直接拷贝到 /opt/arch32 目录下，而不是 /opt/arch32/etc。后面安装pacman相关包的时候，这两个文件存在的话就会出错，所以我们使用一个临时的位置来存放它们。在安装完成之后，可以删除这两个文件，系统就干净了。

```
sed -e 's/x86_64/i686/g' /etc/pacman.d/mirrorlist > /opt/arch32/mirrorlist
sed -e 's@/etc/pacman.d/mirrorlist@/opt/arch32/mirrorlist@g' /etc/pacman.conf > /opt/arch32/pacman.conf

```

在下面的 pacman 命令中使用了_--root_选项，这会使得_/var/log/pacman.log_、_/var/lib/pacman/db.lck_等文件创建在_/opt/arch32_目录下。这样，pacman 的日志文件将是_/opt/arch32/var/log/pacman.log_, 不会和64位的主系统混在一起。因此，并不需要在_/opt/arch32/pacman.conf_文件里添加_LogFile_指令，也不需要_--logfile_命令行选项，除非你想要把它们放在其它地方。

_--cachedir_选项用来设置包缓存的目录，默认是 /var/cache/pacman/pkg，现在要设置为 /opt/arch32/var/cache/pacman/pkg。对于有经验的用户，也可以使用外部的一个目录，这样在完成基本系统的安装后，/opt/arch32目录不会含有任何软件包，比较干净。今后要把 32 位子系统推倒重来的时候也比较方便，不需要重复下载软件包。

这两个目录需要预先创建，因此要执行：

```
mkdir -p /opt/arch32/var/{cache/pacman/pkg,lib/pacman}

```

_--config_选项设置 pacman 配置文件的位置，默认是 /etc/pacman.conf，现在要把它改为 /opt/arch32。

现在同步 pacman 数据库：

```
pacman --root /opt/arch32 --cachedir /opt/arch32/var/cache/pacman/pkg --config /opt/arch32/pacman.conf -Sy

```

安装基本系统：

```
pacman --root /opt/arch32 --cachedir /opt/arch32/var/cache/pacman/pkg --config /opt/arch32/pacman.conf -S base base-devel

```

如果不打算在chroot环境里面编译包，可以不安装base-devel组：

```
pacman --root /opt/arch32 --cachedir /opt/arch32/var/cache/pacman/pkg --config /opt/arch32/pacman.conf -S base

```

**注意：**你可能需要在一条命令里更新pacman数据库并安装基本系统：

```
pacman --root /opt/arch32 --cachedir /opt/arch32/var/cache/pacman/pkg --config /opt/arch32/pacman.conf -Sy base base-devel

```

现在可以删除临时的pacman配置文件了：

```
rm /opt/arch32/{pacman.conf,mirrorlist}

```

## Create an Arch32 Daemon Script and Systemd Service

 `/etc/systemd/system/arch32.service` 

```
[Unit]
Description=32-bit chroot

[Service]
Type=oneshot
RemainAfterExit=yes
ExecStart=/usr/local/bin/arch32 start
ExecStop=/usr/local/bin/arch32 stop

[Install]
WantedBy=multi-user.target

```

 `/usr/local/bin/arch32` 

```
#!/bin/bash

# Add '/var/run /var/lib/dbus' to the list to enable pulseaudio.
dirs=(/dev /dev/pts /dev/shm /tmp /home)

case $1 in
    start)
        for d in "${dirs[@]}"; do
            mount -o bind $d /opt/arch32$d
        done
        ;;
    stop)
        for (( i = ${#dirs[@]} - 1; i >= 0; i-- )); do
            umount "/opt/arch32${dirs[i]}"
        done
        umount /opt/arch32/{proc,sys}
        ;;
    *)
        echo "usage: $0 (start|stop)"
        exit 1
esac
```

Be sure to make the init script executable:

```
# chmod +x /usr/local/bin/arch32

```

Enable the service as any other systemd service.

## 配置新系统

### 配置文件

首先，从主系统链接/拷贝一些有用的配置文件:

```
cd /opt/arch32/etc

cp /etc/passwd* .
cp /etc/shadow* .
cp /etc/group* .
cp /etc/sudoers .  # note: 创建此文件前请先安装 Sudo

cp /etc/rc.conf .
cp /etc/resolv.conf .

cp /etc/localtime .
cp /etc/locale.gen .
cp /etc/profile.d/locale.sh profile.d

cp /etc/vimrc .
cp /etc/mtab .

```

Be sure to include the "." character. .

### 配置 chroot

Chroot 到新系统:

```
/etc/rc.d/arch32 start
xhost +local:
chroot /opt/arch32

```

强烈建议你在“32位chroot环境”里面使用一个特别的 bash 提示符，以便区分你的状况。比如，在**PS1**字符串前面添加**ARCH32**。你可以在“.bashrc”或者其它配置文件里设定。

处理区域设置

```
/usr/sbin/locale-gen
pacman -S ttf-bitstream-vera ttf-ms-fonts wqy-zenhei

```

**注意:** 至少需要一种字体，否则显示不出字来。如果不装中文字体，将不能在32位环境下使用中文。

同时，记住“/etc/pacman.conf”现在是 32 位环境下的默认配置文件。[community] 仓库现在也默认开启了。

在执行以上pacman命令前，确保你把“/etc/pacman.d/mirrorlist”下面至少一个镜像取消注释。如果全部都注释掉了，pacman会报告“未预期的错误”。

现在你可以装上你想要的任何应用程序了.

```
pacman -S acroread opera
pacman -S mozilla-firefox
pacman -S libxmu flashplugin
pacman -S mplayer-plugin

```

在我们的32位环境，基本系统里有很多包其实用不着。你可以把这些包清除，释放一些空间。这些清除工作必须在**32位chroot环境**下进行，且必须在**chroot**之后才能运行！ 以下是可以删除的包列表:

```
pacman -Rd mkinitcpio
pacman -R linux grub dhcpcd rp-pppoe ppp xfsprogs reiserfsprogs jfsutils hdparm hwdetect syslog-ng logrotate lvm2 dcron wpa_supplicant pcmciautils

```

### 考虑清除软件包缓存

**注意**: 这条命令需要运行**不**仅一次。由于软件包是累积的，为了释放 pacman 缓存你必须隔一段时间运行该命令一次：

```
pacman -Scc

```

如果磁盘空间不是很紧张，建议不要清除它，而是把缓存备份到别处。这样，当32位子系统不够干净（充满了不需要的垃圾包）时，可以简单地删除整个目录，然后恢复缓存后重来。这样可以省下很多不必要的程序包下载。

## 在 64 位环境下运行 32 位应用程序

### 下载安装schroot

把来自 community 仓库的“schroot”包安装到 64 位系统上：

```
pacman -S schroot

```

### 配置

Schroot 已经默认配置好可以运行在我们的 Arch32 chroot环境下，所以你只要检查一下 /etc/schroot.conf 文件的 [Arch32] 节是否和你的系统配置相符即可。

你可能还需要编辑 `/etc/schroot/mount-arch32` 文件，看看之前写在 Arch32 脚本里面的 mount 锚点是否都在。当应用程序通过schroot运行的时候，它是看不到不在 `/etc/schroot/mount-arch32` 中列出的目录的。

例如，对于前面提到的 pulseAudio 支持，需要在 `/etc/schroot/mount-arch32` 文件中添加

```
/var/lib/dbus	/var/lib/dbus	none	rw,bind		0	0

```

这样一行。

### 运行 32 位应用程序

最后，要使用所安装的 32 位程序的话只要执行：

```
schroot -p -- opera -notrayicon

```

这会在32位环境下运行 Opera， 且没有系统托盘图标。

### 显示问题

如果收到如下错误信息

```
X Error of failed request: BadLength (poly request too large or internal Xlib length error)

```

先试试运行一些需要视频加速的应用程序，确保你已经在 chroot 环境下安装了适合的显示驱动。例如

```
pacman -S nvidia

```

### 发声

最常用的 32 位应用程序是flash，比如说上 YouTube。

要让 firefox 里的 flash 播放器出声，打开一个终端并且 chroot 到 32 位子系统：

```
chroot /opt/arch32

```

然后在那里装上 alsa-oss：

```
pacman -S alsa-oss

```

然后输入：

```
export FIREFOX_DSP="aoss"

```

每次进入 32 位系统均需要执行这一 export 命令。因此你应该考虑把它放进一个自动执行的脚本里面。

最后，运行 Firefox 就可以了。

### Firefox发声脚本示例

打开一个文本编辑器，另存以下内容为 /usr/bin/firefox32 （用超级用户，或者 sudo）：

```
#!/bin/sh
schroot -p firefox $1;export FIREFOX_DSP="aoss"
```

使该脚本可执行：

```
sudo chmod +x /usr/bin/firefox32

```

现在，如果愿意你可以为firefox创建一个别名：

```
alias firefox="firefox32"

```

把以上命令加入 $HOME/.bashrc 文件后面，然后在bash里运行一下就可以让它马上生效。或者你也可以把桌面环境所有启动器指向 firefox32，如果你仍然希望运行64位的firefox。

### wine 脚本示例

为了编译 wine, 你需要先装上 32 位系统。为了让[PulseAudio](http://art.ified.ca/?page_id=40)能用也许需要打打补丁，这时必须编译 wine。

把 wine 别名加到 .bashrc （或者类似的文件）里： Add following to .bashrc (or similiar) alias for wine:

```
alias wine='schroot -pqd $(pwd) -- wine'

```

注意 -q 参数使 schroot 运行于安静模式，效果就**仿佛**在运行真正的wine一样。

### 注意事项

如果你还在使用老的 dchroot 而不是这里介绍的schroot，你应该用_-d_选项而不是_-s_。

## 另类安装方法

在上面的安装过程中，我们把 base 组装在了目标系统。正如前面所看到的，有许多包其实没有必要装在子系统上。为了得到一个更干净、更精简的32位子系统，可以不在子系统内安装 pacman 及其相关包，而是依赖于64位系统的 pacman。但是，32位子系统必须拥有自己的软件包数据库。

首先还是要创建 32 位主目录

```
mkdir /opt/arch32

```

然后生成配置文件。这一次，我们永久依赖这些文件来安装随后的软件，因此**不要**把它们删除。

```
sed -e 's/x86_64/i686/g' /etc/pacman.d/mirrorlist > /opt/arch32/mirrorlist
sed -e 's@/etc/pacman.d/mirrorlist@/opt/arch32/mirrorlist@g' /etc/pacman.conf > /opt/arch32/pacman.conf

```

创建 pacman 所需的目录。如果你象我一样使用外部的 cache 目录，请自行修改一下此命令。

```
mkdir -p /opt/arch32/var/{cache/pacman/pkg,lib/pacman}

```

创建 pacman32 的别名（添加如下命令到 .bashrc 或者类似脚本里）：

```
alias pacman32="pacman --root /opt/arch32 --cachedir /opt/arch32/var/cache/pacman/pkg --config /opt/arch32/pacman.conf"

```

同步 pacman 数据库

```
pacman32 -Sy

```

安装 bash 以及一些必要软件

```
pacman32 -S filesystem licenses bash sed coreutils gzip

```

然后参照前面所述，创建 /etc/rc.d/Arch32 脚本，拷贝配置文件，即可进入 chroot 环境。此后，所有 pacman 命令均需在64位系统下运行 pacman32 代替。

此方法的优点是无须担心删除无用的包，只有真正需要用到的包才会被安装。