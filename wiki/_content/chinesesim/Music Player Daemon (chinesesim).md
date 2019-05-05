相关文章

*   [MPD/Tips and Tricks](/index.php/MPD/Tips_and_Tricks "MPD/Tips and Tricks")
*   [MPD/Troubleshooting](/index.php/MPD/Troubleshooting "MPD/Troubleshooting")

**翻译状态：** 本文是英文页面 [Music_Player_Daemon](/index.php/Music_Player_Daemon "Music Player Daemon") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-01-17，点击[这里](https://wiki.archlinux.org/index.php?title=Music_Player_Daemon&diff=0&oldid=352912)可以查看翻译后英文页面的改动。

**[MPD](http://mpd.wikia.com)** (**m**usic **p**layer **d**aemon) 是一个服务器-客户端架构的音频播放器. 功能包括音频播放, 播放列表管理和音乐库维护，所有功能占用的资源都很少. 你需要一个独立的 [客户端](#Clients) 与它进行交互。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 安装](#安装)
*   [2 设置](#设置)
    *   [2.1 全局配置](#全局配置)
        *   [2.1.1 音乐目录](#音乐目录)
        *   [2.1.2 启动 MPD](#启动_MPD)
            *   [2.1.2.1 套接字启动](#套接字启动)
        *   [2.1.3 配置音频](#配置音频)
        *   [2.1.4 更改用户](#更改用户)
        *   [2.1.5 MPD 启动时间轴](#MPD_启动时间轴)
    *   [2.2 本地配置（单用户）](#本地配置（单用户）)
        *   [2.2.1 在 tty 登陆时自启动](#在_tty_登陆时自启动)
        *   [2.2.2 在 X 下自启动](#在_X_下自启动)
        *   [2.2.3 通过 systemd 自启动](#通过_systemd_自启动)
        *   [2.2.4 脚本配置](#脚本配置)
    *   [2.3 多 mpd 实例设置](#多_mpd_实例设置)
*   [3 客户端](#客户端)
    *   [3.1 命令行下](#命令行下)
    *   [3.2 图形界面下](#图形界面下)
    *   [3.3 Web界面](#Web界面)
*   [4 参阅](#参阅)

## 安装

安装 [mpd](https://www.archlinux.org/packages/?name=mpd)，或者开发版本—[mpd-git](https://aur.archlinux.org/packages/mpd-git/)。

**注意:** [Mopidy](http://www.mopidy.com) 是另一个选择，使用 Python 实现。可以通过 [mopidy](https://www.archlinux.org/packages/?name=mopidy) 和 [mopidy-git](https://aur.archlinux.org/packages/mopidy-git/)获得。注意这不是一个完全的 MPD [代替品](http://docs.mopidy.com/en/latest/ext/mpd/#limitations)。Mopidy 与 MPD 相比的优势在于它具有从 Spotify，SoundCloud 和 Google Play Music 等云服务播放音乐的插件。然而，mopidy 项目不是那么活跃，并且许多插件在一段时间内会变得不可用或者很奇怪。

## 设置

MPD 可以本地运行(单用户设置)、全局运行(为所有用户设置)，也可以同时运行多个实例。将 MPD 设置成哪种方式运行取决于它被如何使用，例如，设置成本地运行就很适合桌面系统。

为了使 MPD 能够播放音频，需要先设置好 [ALSA](/index.php/Advanced_Linux_Sound_Architecture_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Advanced Linux Sound Architecture (简体中文)") 或者 [OSS](/index.php/Open_Sound_System_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Open Sound System (简体中文)") (可选 [PulseAudio](/index.php/PulseAudio_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "PulseAudio (简体中文)"))。

MPD 的配置文件是 `mpd.conf`，运行方式不同，文件的位置也不同。下面是常用的配置选项:

*   `pid_file` - MPD进程ID存储文件
*   `db_file` - 音乐数据库
*   `state_file` - 记录MPD当前状态
*   `playlist_directory` - 播放列表存储文件夹
*   `music_directory` - MPD在这个文件夹中扫描音乐
*   `sticker_file` - 标签数据库

### 全局配置

**警告:** 使用 PulseAudio 并且将 mpd 设置为全局配置的用户可能需要 [一个小技巧](/index.php/Music_Player_Daemon/Tips_and_tricks#Local_(with_separate_mpd_user) "Music Player Daemon/Tips and tricks") 来作为自己的用户运行 mpd！

The default /etc/mpd.conf keeps the setup in /var/lib/mpd which is assigned to user as well as primary group mpd.

#### 音乐目录

音乐目录需要通过 `/etc/mpd.conf` 文件中的 `music_directory` 参数来设置：

```
music_directory "/path/to/music"

```

MPD需要拥有 **所有** 音乐收藏父目录的 `+x` 权限并且可以读包含音乐的目录，这经常与用户的音乐目录的默认设置冲突。

有很多方法可以解决这个问题，下面是其中不错的一个

*   [将 MPD 作为用户运行](#本地配置（单用户）)
*   将 mpd 用户添加到登录组，并授予用户目录组权限。

```
# gpasswd -a mpd <your login group>
$ chmod 710 /home/<your home dir>

```

*   采取以下方式将音乐集合放到不同的路径

（a）完全移动 （b）绑定挂载 （c）使用 [Btrfs 子卷](/index.php/Btrfs#Subvolumes "Btrfs")（需要将这一永久改变写入 `/etc/fstab` 中）。可以使用 [Access Control Lists](/index.php/Access_Control_Lists "Access Control Lists") 调整备用目录的权限。

MPD 配置必须仅包含一个目录，如果音乐集包含在多个目录下，那么在 `/var/lib/mpd` 的主音乐目录下创建符号链接。记得为被链接的目录设置相应的权限。

#### 启动 MPD

可以使用 [systemd](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#使用单元 "Systemd (简体中文)") 来控制 MPD 服务，即`mpd.service`，第一次启动 MPD 时会花费一些时间，因为 MPD 会扫描音乐目录。

安装一个客户端程序 ([ncmpc](https://www.archlinux.org/packages/?name=ncmpc) 是一个轻便易用的客户端程序)，享受音乐吧！

##### 套接字启动

如果启用了 `mpd.socket`，但没有启用 `mpd.service`，systemd 不会立刻启动 mpd，而是会监听相应的套接字。当一个 mpd 客户端试图连接其中的套接字，systemd 将启动 `mpd.service`， 然后透明地将端口的控制权交给 mpd 进程。

如果你希望监听不同的 UNIX 套接字或者网络端口（甚至是每个类型的多个套接字），或者你完全不希望监听网络端口。你需要 **添加/编辑/删除** `mpd.socket` 文件中 `[Socket]` 章节下的 `"ListenStream="` 行，**并且**更改 `/etc/mpd.conf` 文件中的相应行（具体查看 [mpd.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mpd.conf.5)）。

#### 配置音频

[ALSA](/index.php/ALSA "ALSA") 用户需要做以下设备定义，使用声卡名字或者 pcm (aplay --list-pcms) 代替下面的 `My Sound Card` 字段。

 `/etc/mpd.conf` 
```
audio_output {
        type            "alsa"
        name            "My Sound Card"
        mixer_type      "software"      # optional
}
```

`mixer_type "software"` 选项告诉 'mpd' 使用自己的独立软件音量控制。

[PulseAudio](/index.php/PulseAudio "PulseAudio") 用户需要做以下修改：

 `/etc/mpd.conf` 
```
audio_output {
        type            "pulse"
        name            "pulse audio"
}
```

PulseAudio 支持多种高级操作。例如：将音频传输到不同的机器。MPD 的高级设置参考 [Music Player Daemon Community Wiki](http://mpd.wikia.com/wiki/PulseAudio)。

#### 更改用户

更改用户组，可能会导致 MPD 运行出现以下类似错误： `output: Failed to open "My ALSA Device"`， `[alsa]: Failed to open ALSA device "default": No such file or directory` ，`player_thread: problems opening audio device while playing "Song Name.mp3"`

这是因为 MPD 用户需要是 *audio* 组的成员来访问 `/dev/snd/` 下的音频设备。将 MPD 用户添加到 *audio* 组里来解决这个问题。

```
# gpasswd -a **mpd** audio

```

#### MPD 启动时间轴

下面列出的是 MPD 正常启动的时间轴，用以描述何时 MPD 放弃超级用户权限，而使用配置中用户组的权限。

1.  以 root 身份通过 systemd 启动 MPD 后，MPD 首先读取 `/etc/mpd.conf` 文件。
2.  然后 MPD 读取 `/etc/mpd.conf` 中的用户变量，从 root 切换到该用户。
3.  最后 MPD 读取 `/etc/mpd.conf` 中的设置内容，根据内容配置自己。

注意，MPD 会改变运行用户，从 root 切换到 `/etc/mpd.conf` 文件中命名的一个用户。这样，在配置文件中使用 `~` 会正确的指向 home 用户目录，而不是 root 目录。将所有的 `~` 修改成 `/home/username` 来避免在 MPD 行为这一方面上的困惑很有必要。

### 本地配置（单用户）

MPD 可以被配置为单用户（而不是全局配置 MPD 的典型方法）。以普通用户运行 MPD 有以下好处：

*   一个可以包含所有 MPD 配置文件的单独目录 `~/.config/mpd/` （或者 `$HOME` 下的任一目录）。
*   更容易避免不可预见的读/写权限错误。

好的做法是为所有需要的文件和播放列表创建一个单独目录。该目录可以是任何一个你可以读写的目录。例如： `~/.config/mpd/` 或者 `~/.mpd/`。本章节假设该目录是 `~/.config/mpd/`，其对应 `$XDG_CONFIG_HOME` （ [XDG Base Directory Specification](http://standards.freedesktop.org/basedir-spec/basedir-spec-latest.html) 的部分）的缺省值 。

MPD 首先搜索配置文件 `$XDG_CONFIG_HOME/mpd/mpd.conf`，其次搜索 `~/.mpdconf`。还可以通过命令行参数指定其他路径。

将示例配置文件复制到所需的位置。例如：

```
$ cp /usr/share/doc/mpd/mpdconf.example ~/.config/mpd/mpd.conf

```

编辑 `~/.config/mpd/mpd.conf` 并且指定所需文件：

 `~/.config/mpd/mpd.conf` 
```
# Required files
db_file            "~/.config/mpd/database"
log_file           "~/.config/mpd/log"

# Optional
music_directory    "~/Music"
playlist_directory "~/.config/mpd/playlists"
pid_file           "~/.config/mpd/pid"
state_file         "~/.config/mpd/state"
sticker_file       "~/.config/mpd/sticker.sql"

```

创建所有上述配置中提及的文件和目录：

```
$ mkdir ~/.config/mpd/playlists
$ touch ~/.config/mpd/{database,log,pid,state,sticker.sql}

```

当配置了所需文件的路径后，就可以启动 MPD 了。要指定配置文件的自定义位置，运行：

```
$ mpd *config_file*

```

#### 在 tty 登陆时自启动

要使 MPD 在登陆时启动，在 `~/.profile` （或者其他的 [自启动文件](/index.php/Autostarting#Shells "Autostarting") ）中添加以下命令：

```
# MPD daemon start (if no other user instance exists)
[ ! -s ~/.config/mpd/pid ] && mpd

```

#### 在 X 下自启动

如果你安装了[桌面环境](/index.php/Desktop_environment_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Desktop environment (简体中文)")，编辑下面的文件并将其放到 `~/.config/autostart/` ：

 `~/.config/autostart/mpd.desktop` 
```
[Desktop Entry]
Encoding=UTF-8
Type=Application
Name=Music Player Daemon
Comment=Server for playing audio files
Exec=mpd
StartupNotify=false
Terminal=false
Hidden=false
X-GNOME-Autostart-enabled=false

```

如果没有使用桌面环境，将 [#在 tty 登陆时自启动](#在_tty_登陆时自启动) 中的命令加入到 [自启动文件](/index.php/Autostarting#Graphical "Autostarting")。

#### 通过 systemd 自启动

**注意:** 本章节假设 systemd 用户会话管理器已经运行。具体信息查看 [systemd/User (简体中文)](/index.php/Systemd/User_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Systemd/User (简体中文)")。

[mpd](https://www.archlinux.org/packages/?name=mpd) 提供了用户服务文件 `/usr/lib/systemd/user/mpd.service`。配置文件预计存在 `~/.mpdconf` 或者 `~/.config/mpd/mpd.conf` 中，如果想要使用不同的路径，参考 [systemd (简体中文)#修改现存单元文件](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#修改现存单元文件 "Systemd (简体中文)")。进程不会以 root 启动，所以在 MPD 配置文件中不能使用 `user` 和 `group` 变量，进程已经拥有用户权限，因此没有必要进一步更改他们。

所有你需要做的是启用和启动 `mpd` [用户服务](/index.php/Systemd/User_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Systemd/User (简体中文)")。

**注意:**

*   [mpd](https://www.archlinux.org/packages/?name=mpd) 也提供了系统服务文件 `/usr/lib/systemd/system/mpd.service`，但是当以 root 身份启动进程时，进程不会读取用户配置文件而是会回落到 `/etc/mpd.conf`。[全局配置](#全局配置) 中已经介绍过了。
*   确保停用任何以前用过的启动 mpd 的方法。

#### 脚本配置

Rasi 创建了一个脚本，该脚本可以创建合适的目录结构、配置文件，并且提示用户音乐目录的位置。可以在 [这里](http://dl.53280.de/mpdsetup.sh) 下载。

### 多 mpd 实例设置

**在运行 icecast 服务器中很有用**

如果第二个 mpd （例如：通过网络使用 icecast 输出来分享音乐）使用和上一个 mpd 相同的音乐和播放列表，只需要复制上一个的配置文件来创建一个新文件（例如：`/home/username/.mpd/config-icecast`），并且更改 log_file, error_file, pid_file 和 state_file 的参数（例如：`mpd-icecast.log`, `mpd-icecast.error` 等等），使用相同的音乐目录路径和播放列表目录将确保第二个 mpd 和第一个 mpd 使用相同的音乐收藏。在第一个 mpd 守护进程下创建和编辑播放列表也会影响第二个守护进程。不需要为第二个守护进程创建相同的播放列表。以相同的方式从上述 `~/.xinitrc` 调用第二个守护进程。（仅仅需要确保使用不同的端口号，这样不会和第一个 mpd 守护进程冲突）。

**更好的方法：卫星模式设置**

上述的方法在工作过程中，当两个 mpd 实例写相同的数据库文件时，在理论上可能导致数据库问题。MPD 有一种卫星模式，该模式下，一个实例可以从另一个已经运行的 mpd 实例上接受数据库。

在 config-icecast 中添加以下代码，host 和 port 反映了主要 mpd 服务器的主机和端口。

```
   database {
   plugin "proxy"
   host "localhost"
   port "6600"
   }

```

## 客户端

需要安装独立客户端才能控制mpd。 常用的有这些：

### 命令行下

*   **mpc** — 简单的基于KISS原则的客户端。 拥有所有的基本功能。

	[http://mpd.wikia.com/wiki/Client:Mpc](http://mpd.wikia.com/wiki/Client:Mpc) || [mpc](https://www.archlinux.org/packages/?name=mpc)

*   **ncmpc** — 一个使用NCursers的客户端。

	[http://mpd.wikia.com/wiki/Client:Ncmpc](http://mpd.wikia.com/wiki/Client:Ncmpc) || [ncmpc](https://www.archlinux.org/packages/?name=ncmpc)

*   **[ncmpcpp](/index.php/Ncmpcpp "Ncmpcpp")** — 差不多是完全克隆ncmpc的客户端， 但是有一些用C++写成的新功能(tag editor, search engine)

	[http://unkart.ovh.org/ncmpcpp/](http://unkart.ovh.org/ncmpcpp/) || [ncmpcpp](https://www.archlinux.org/packages/?name=ncmpcpp)

*   **pms** — Highly configurable and accessible ncurses client

	[http://pms.sourceforge.net/](http://pms.sourceforge.net/) || [pmus](https://aur.archlinux.org/packages/pmus/)

*   **vimpc** — 基于ncurses的MPD客户端， 使用类似vi的快捷键

	[http://sourceforge.net/projects/vimpc/](http://sourceforge.net/projects/vimpc/) || [vimpc](https://aur.archlinux.org/packages/vimpc/)

### 图形界面下

*   **Ario** — 一个功能非常丰富的 GTK2 界面的客户端，灵感来自于 Rhythmbox。

	[http://ario-player.sourceforge.net/](http://ario-player.sourceforge.net/) || [ario](https://www.archlinux.org/packages/?name=ario)

*   **QmpdClient** — 用 Qt 4.x 写的图形客户端。

	[http://bitcheese.net/wiki/QMPDClient](http://bitcheese.net/wiki/QMPDClient) || [qmpdclient](https://aur.archlinux.org/packages/qmpdclient/)

*   **Sonata** — 一个用 Python 写的客户端，非常优雅。

	[http://www.nongnu.org/sonata/](http://www.nongnu.org/sonata/) || [sonata](https://www.archlinux.org/packages/?name=sonata)

*   **gmpc** — GTK2 写的 MPD 前端。被设计为轻量且易用，同时也对所有的 MPD 的特性提供完全访问。为用户提供几种不同的方法来浏览音乐。可以通过很多可获得的插件来扩展。

	[http://gmpclient.org/](http://gmpclient.org/) || [gmpc](https://aur.archlinux.org/packages/gmpc/)

*   **Cantata** — 多功能的 Qt4, Qt5 或者 KDE4 客户端，具有很多可配置的接口。

	[https://code.google.com/p/cantata/](https://code.google.com/p/cantata/) || [cantata](https://www.archlinux.org/packages/?name=cantata)

### Web界面

*   **Patchfork** — 用 PHP 和 Ajax 写的 web 客户端

	[http://mpd.wikia.com/wiki/Client:Pitchfork](http://mpd.wikia.com/wiki/Client:Pitchfork) || [patchfork-git](https://aur.archlinux.org/packages/patchfork-git/).

在 [mpd wiki](http://mpd.wikia.com/wiki/Clients) 上可以查看到客户端列表。

## 参阅

*   [Sorted List of MPD Clients](http://mpd.wikia.com/wiki/Clients)
*   [MPD forum](http://www.musicpd.org/forum/)