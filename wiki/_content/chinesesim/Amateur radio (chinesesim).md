Related articles

*   [GNU Radio](/index.php/GNU_Radio "GNU Radio")
*   [RTL-SDR](/index.php/RTL-SDR "RTL-SDR")

业余无线电爱好者（又称“火腿”）自从无线电存在的早期就活跃在相关实验与开发的前沿。在各个无线电频段上，有多种常用的通信模式。 本页面列举了[AUR](/index.php/AUR "AUR")中与业余无线电有关的软件，其中有些可以独立运行，但多数处理数字通信的程序则需要配合无线电硬件或者声卡使用。相关硬件可以购买，也可以自制。

**Warning:** 按国际条约要求，你必须持有政府发放的执照才能使用业余无线电频率。但这些条约只是约束信号的发射；只接收业余无线电信号或下载相关软件是不违法的。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 通用信息](#通用信息)
*   [2 软件列表](#软件列表)
    *   [2.1 AX.25](#AX.25)
    *   [2.2 WSJT](#WSJT)
    *   [2.3 WSPR](#WSPR)
    *   [2.4 Xastir](#Xastir)
    *   [2.5 数字语音](#数字语音)
    *   [2.6 分析工具](#分析工具)
    *   [2.7 日志](#日志)
    *   [2.8 工具](#工具)
    *   [2.9 练习莫尔斯码](#练习莫尔斯码)
    *   [2.10 其他](#其他)

## 通用信息

下面的很多程序都需要使用串口（如/dev/ttyS0）与发射器通信。首先，你的用户需要在uucp用户组中。要将一个用户添加到uucp组中，以root身份运行下面的命令：

```
# gpasswd -a *用户名* uucp

```

之后注销再重新登录。

## 软件列表

*   **Hamlib** — 为无线电硬件和控制程序之间提供了一个通信界面。它只是用于帮助控制电台等硬件，并不是一个能独立使用的程序。

	[https://sourceforge.net/projects/hamlib/](https://sourceforge.net/projects/hamlib/) || [hamlib](https://www.archlinux.org/packages/?name=hamlib)

*   **Soundmodem** — 由Tom Sailer（HB9JNX/AE4WA）编写，它能将声卡作为一个分组无线电的调制解调器，从而能使用多种AX.25通信模式。波特率最高能达到9600bps， 但也取决于硬件配置和具体用途。Soundmodem可以在串口上作为一个KISS调制解调器或者AX.25网络设备。To use soundmodem as an MKISS network device, the kernel must be re-built with MKISS modules. 该链接中有更多信息：[Xastir wiki](http://www.xastir.org/wiki/index.php/HowTo:SoundModem)

	以root身份运行soundmodem:

	 `# soundmodem` 

	If you have configured soundmodem as a KISS modem, you will need to change permissions to make it user-readable:

	 `# chmod 666 /dev/soundmodem0` 

	[http://www.baycom.org/~tom/ham/soundmodem/](http://www.baycom.org/~tom/ham/soundmodem/) || [soundmodem](https://aur.archlinux.org/packages/soundmodem/)

*   **Grig** — 基于Hamlib的简单的控制程序

	[http://groundstation.sourceforge.net/grig/](http://groundstation.sourceforge.net/grig/) || [grig](https://aur.archlinux.org/packages/grig/)

*   **gMFSK** — 支持多种数字模式，使用hamlib和xlog记录日志

	[http://gmfsk.connect.fi](http://gmfsk.connect.fi) || [gmfsk](https://aur.archlinux.org/packages/gmfsk/)

*   **lysdr** — 高度可自定义的无线电界面程序

	[https://github.com/gordonjcp/lysdr](https://github.com/gordonjcp/lysdr) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **linrad** — SM5BSZ编写的软件定义无线电

	[http://www.sm5bsz.com/linuxdsp/linrad.htm](http://www.sm5bsz.com/linuxdsp/linrad.htm) || [linrad](https://aur.archlinux.org/packages/linrad/)

*   **quisk** — N2ADR编写的软件定义无线电

	[http://james.ahlstrom.name/quisk/](http://james.ahlstrom.name/quisk/) || [quisk](https://aur.archlinux.org/packages/quisk/)

*   **owx** — Command-line utility for programming Wouxun radios using CSV spreadsheets.

	[http://owx.chmurka.net](http://owx.chmurka.net) || [owx](https://aur.archlinux.org/packages/owx/)

*   **fldigi** — W1HKJ开发的GUI程序，支持多种数字通信模式

	[http://w1hkj.com/Fldigi.html](http://w1hkj.com/Fldigi.html) || [fldigi](https://aur.archlinux.org/packages/fldigi/)

*   **libfap** — APRS包解析程序

	[http://pakettiradio.net/libfap/](http://pakettiradio.net/libfap/) || [libfap](https://aur.archlinux.org/packages/libfap/)

*   **aprx** — lightweight APRS digipeater and i-Gate interface

	[http://thelifeofkenneth.com/aprx/](http://thelifeofkenneth.com/aprx/) || [aprx](https://aur.archlinux.org/packages/aprx/)

*   **xdx** — 网络客户端

	[http://www.qsl.net/pg4i/linux/xdx.html](http://www.qsl.net/pg4i/linux/xdx.html) || [xdx](https://aur.archlinux.org/packages/xdx/)

*   **qsstv** — 慢扫描电视

	|| [qsstv](https://aur.archlinux.org/packages/qsstv/)

*   **linpsk** — PSK31

	|| [linpsk](https://aur.archlinux.org/packages/linpsk/)

*   **xpsk31** — PSK31，GUI使用GTK+

	[http://www.qsl.net/5b4az/pkg/psk31/xpsk31/xpsk31.html](http://www.qsl.net/5b4az/pkg/psk31/xpsk31/xpsk31.html) || [xpsk31](https://aur.archlinux.org/packages/xpsk31/)

### AX.25

**[AX.25](https://en.wikipedia.org/wiki/AX.25 "wikipedia:AX.25")** — 一个广泛应用于分组无线电的数据链路层协议。它既支持有线连接（如keyboard-to-keyboard contacts, access to local bulletin board systems, and DX clusters），也支持无线连接（如[APRS](https://en.wikipedia.org/wiki/APRS "wikipedia:APRS")）。Linux内核中有对AX.25的原生支持。这里有更多信息：[guide](http://tldp.org/HOWTO/AX25-HOWTO/)[AUR](/index.php/AUR "AUR")中有以下软件可用：

*   [ax25-apps](https://aur.archlinux.org/packages/ax25-apps/)
*   [ax25-tools](https://aur.archlinux.org/packages/ax25-tools/)
*   [libax25](https://aur.archlinux.org/packages/libax25/)
*   [node](https://aur.archlinux.org/packages/node/)

	[http://www.ax25.net/](http://www.ax25.net/) || present in stock kernel

### WSJT

**[WSJT](https://en.wikipedia.org/wiki/WSJT_(Amateur_radio_software) (Weak Signal Communication by K1JT)** — offers a rich variety of features, including specific digital protocols optimized for meteor scatter, ionospheric scatter, and EME (moonbounce) at VHF/UHF, as well as HF skywave propagation. WSJT的开发者是诺贝尔物理学奖得主Joe Taylor，无线电呼号为KIJT。The program can decode fraction-of-a-second signals reflected from ionized meteor trails and steady signals 10 dB below the audible threshold.
WSJT is in ongoing, active development by a team of programmers led by K1JT. WSJT (and the related program WSPR) has the option of being configured with

 `$ ./configure --enable-g95` 

or

 `$ ./configure --enable-gfortran` 

If you build with one and experience problems, edit PKGBUILD to try the other.
WSJT requires access to the serial port; see the note in the Interfacing section above about the uucp group.

	[http://www.physics.princeton.edu/pulsar/K1JT/](http://www.physics.princeton.edu/pulsar/K1JT/) || [wsjt-svn](https://aur.archlinux.org/packages/wsjt-svn/)

### WSPR

**[WSPR](https://en.wikipedia.org/wiki/WSPR_(amateur_radio_software) (Weak Signal Propagation Reporter, pronounced whisper)** — enables the probing of propagation paths on the amateur radio bands using low power transmissions. It was introduced in 2008 by K1JT following the success and widespread adoption of WSJT by the amateur radio community. Stations with Internet access can automatically upload their reception reports to a central database called [WSPRnet](http://wsprnet.org/drupal/), which includes a [mapping facility](http://wsprnet.org/drupal/wsprnet/map)

	[http://physics.princeton.edu/pulsar/K1JT/wspr.html](http://physics.princeton.edu/pulsar/K1JT/wspr.html) || [wspr-svn](https://aur.archlinux.org/packages/wspr-svn/)

### Xastir

**Xastir** — stands for X Amateur Station and Information Reporting. It works with [APRS](https://en.wikipedia.org/wiki/APRS "wikipedia:APRS"), an amateur radio-based system for real time tactical digital communications. Xastir is an open-source program that provides full-featured, client-side access to APRS. It is currently in a state of active development.
Xastir is highly flexible and there are a wide variety of ways it can be configured. For example, it can be evaluated without radio hardware if an Internet connection is available. The wiki at xastir.org is very thorough and gives excellent information on its range of capabilities and setup.
An optional speech feature can be enabled with the [festival](https://www.archlinux.org/packages/?name=festival) package; you will also need a speaker package such as festival-en or festival-english. If you want this option, festival must be installed on your system before building xastir. Launch festival before the xastir program is started for speech to function properly:

 `$ festival --server` 

or you can write a simple script to automate the sequential starting process. There may be problems if other programs such as a media player are accessing sound simultaneously.
The PKGBUILD automatically downloads an 850 kB bundle of .wav files and places them here: `/usr/share/xastir/sounds/`.
These are audio alarm recordings of a North American English speaker that do not require the presence of festival to render. The audio play command `play' in the configure menu may not work; try `aplay' instead.

	[http://www.xastir.org](http://www.xastir.org) || [xastir](https://aur.archlinux.org/packages/xastir/)

### 数字语音

**FreeDV** — 是一个用于 HF 频段的数字语音模式。它使用的是开源免费的 Codec2 语音编解码器，有着窄带宽、低数据速率的特点，特别适用于短波无线电通联。使用FreeDV所需要的只有一台运行Free DV GUI程序的计算机，以及 SSB 模式的电台。对于 Arch Linux，FreeDV 和 Codec2 都可以从 AUR 获取到。两者都需要安装好才能使用 FreeDV！

*   [http://www.rowetel.com/codec2.html](http://www.rowetel.com/codec2.html) [codec2](https://www.archlinux.org/packages/?name=codec2)

	[http://freedv.org](http://freedv.org) || [freedv](https://aur.archlinux.org/packages/freedv/)

### 分析工具

*   [gpredict](https://aur.archlinux.org/packages/gpredict/) – 实时卫星追踪、卫星轨道预测
*   [hamsolar](https://aur.archlinux.org/packages/hamsolar/) – 在桌面上显示当前太阳活动指数
*   [splat](https://aur.archlinux.org/packages/splat/) – 无线电信号传播、损耗和地形分析
*   [sunclock](https://aur.archlinux.org/packages/sunclock/) – Useful for predicting grayline propagation paths
*   [xnec2c](https://aur.archlinux.org/packages/xnec2c/) – 天线模拟软件

### 日志

*   [cqrlog-bin](https://aur.archlinux.org/packages/cqrlog-bin/) – 常见的Linux日志程序
*   [fdlog](https://aur.archlinux.org/packages/fdlog/) – a Field Day Logger with networked nodes
*   [klog](https://aur.archlinux.org/packages/klog/) – 运行在KDE上的业余无线电日志程序
*   [qle](https://aur.archlinux.org/packages/qle/) – QSO 日志记录器和编辑器，用 Perl 编写
*   [tlf](https://aur.archlinux.org/packages/tlf/) – a console mode networked logging and contest program
*   [trustedqsl](https://aur.archlinux.org/packages/trustedqsl/) – QSL application for ARRL's Logbook of the World
*   [xlog](https://aur.archlinux.org/packages/xlog/) – a logging program for amateur radio operators.
*   [yfklog](https://aur.archlinux.org/packages/yfklog/) – 通用的*nix业余无线电日志程序
*   [yfktest](https://aur.archlinux.org/packages/yfktest/) – a logbook program for ham radio contests.

### 工具

*   [cty](https://aur.archlinux.org/packages/cty/) – 实体（国家）、前缀、呼号等信息，供业余无线电日志程序使用
*   [dxcc](https://aur.archlinux.org/packages/dxcc/) – a small program for determining ARRL DXCC entity of a ham radio callsign

### 练习莫尔斯码

*   [aldo](https://aur.archlinux.org/packages/aldo/)
*   [cutecw](https://aur.archlinux.org/packages/cutecw/)
*   [ebook2cw](https://aur.archlinux.org/packages/ebook2cw/)
*   [gtkmmorse](https://aur.archlinux.org/packages/gtkmmorse/)
*   [kochmorse](https://aur.archlinux.org/packages/kochmorse/)
*   [qrq](https://aur.archlinux.org/packages/qrq/)
*   [unixcw](https://aur.archlinux.org/packages/unixcw/)

### 其他

*   [cwirc](https://aur.archlinux.org/packages/cwirc/) – 在IRC上收发莫尔斯码