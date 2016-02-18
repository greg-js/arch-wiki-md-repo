本文将帮助你在 Arch Linux 中安装网络摄像机。

## Contents

*   [1 识别你的网络摄像机](#.E8.AF.86.E5.88.AB.E4.BD.A0.E7.9A.84.E7.BD.91.E7.BB.9C.E6.91.84.E5.83.8F.E6.9C.BA)
    *   [1.1 pwc](#pwc)
    *   [1.2 qc-usb](#qc-usb)
    *   [1.3 qc-usb-messenger](#qc-usb-messenger)
    *   [1.4 zr364xx](#zr364xx)
    *   [1.5 sn9c102](#sn9c102)
    *   [1.6 gspca](#gspca)
    *   [1.7 stv680](#stv680)
    *   [1.8 linux-uvc](#linux-uvc)
    *   [1.9 ov51x-jpeg](#ov51x-jpeg)
    *   [1.10 r5u870 (Ricoh)](#r5u870_.28Ricoh.29)
    *   [1.11 stk11xx (Syntek)](#stk11xx_.28Syntek.29)
*   [2 确定为你的网络摄像机加载所需的模块](#.E7.A1.AE.E5.AE.9A.E4.B8.BA.E4.BD.A0.E7.9A.84.E7.BD.91.E7.BB.9C.E6.91.84.E5.83.8F.E6.9C.BA.E5.8A.A0.E8.BD.BD.E6.89.80.E9.9C.80.E7.9A.84.E6.A8.A1.E5.9D.97)
*   [3 权限](#.E6.9D.83.E9.99.90)
    *   [3.1 udev](#udev)
    *   [3.2 devfs](#devfs)
*   [4 获取软件以使用你的网络摄像机](#.E8.8E.B7.E5.8F.96.E8.BD.AF.E4.BB.B6.E4.BB.A5.E4.BD.BF.E7.94.A8.E4.BD.A0.E7.9A.84.E7.BD.91.E7.BB.9C.E6.91.84.E5.83.8F.E6.9C.BA)
    *   [4.1 Cheese](#Cheese)
    *   [4.2 GTK+ UVC Viewer (guvcview)](#GTK.2B_UVC_Viewer_.28guvcview.29)
    *   [4.3 Kopete](#Kopete)
    *   [4.4 Kamoso](#Kamoso)
    *   [4.5 xawtv](#xawtv)
    *   [4.6 VLC](#VLC)
    *   [4.7 MPlayer](#MPlayer)
    *   [4.8 FFmpeg](#FFmpeg)
    *   [4.9 ekiga](#ekiga)
    *   [4.10 Sonic-snap](#Sonic-snap)
    *   [4.11 Skype](#Skype)

## 识别你的网络摄像机

识别你的网络摄像机的名称并使用恰当的驱动程序。 下面列出部分网络摄像机的名称，以及它们所需的驱动程序。点击设备名称右边的链接以获取编译模块所需信息及其他相关信息。如果你正确设置并使用其他网络摄像机，请将其名称和驱动程序添加到列表中！

### pwc

*   Creative Labs Webcam Pro Ex （创新实验室网络摄像机专家加强版）
*   Logitech QuickCam Notebook Pro（罗技快看笔记本专用专家版，仅适用于“专家版”机型）
*   Logitech Quickcam Pro 4000
*   Philips ToUCams (not confirmed at the moment, but it's using the pwc driver if I remember correctly)

### [qc-usb](/index.php/Qc-usb "Qc-usb")

*   Dexxa Webcam （Dexxa 网络摄像机）
*   Labtec Webcam (old model) （Labtec 网络摄像机，旧机型）
*   LegoCam
*   Logitech Quickcam Express (old model)（罗技快看加强版，旧机型）
*   Logitech QuickCam Notebook （罗技快看笔记本专用版，非“专家版”机型）
*   Logitech Quickcam Web （罗技快看网络版）

### qc-usb-messenger

*   Logitech Quickcam Messenger
*   Logitech Quickcam Communicate

It is now in the community repo.

**说明：** 如果使用模块gspca不能使qc-usb-messenger正常工作，安装软件包gspcav1。
**说明:** 现在这驱动已经成为kernel 2.6.27的一个模块

### zr364xx

这个驱动可以应用于很多电脑摄像头，比如:

*   Aiptek PocketDV 3300
*   Creative PC-CAM 880
*   Konica Revio 2
*   Genius Digital Camera
*   Maxell Maxcam PRO DV3

你可以在这里找到它所支持全部设备的列表：[here](http://royale.zerezo.com/zr364xx/). 你可以在这里找到一个此驱动的PKGBUILD：[AUR](https://aur.archlinux.org/).

### sn9c102

*   Trust Spacecam series
*   Maxell Smartcam (for notebooks): 352x288 max. resolution @ 3fps

### gspca

支持的列表位于[[1]](http://git.kernel.org/?p=linux/kernel/git/torvalds/linux-2.6.git;a=blob;f=Documentation/video4linux/gspca.txt;hb=HEAD).

**注意:** 此驱动不支持 V4L1。

### stv680

最近两年产于亚洲国家的一些没有产品名的廉价摄像机多使用 stv680 芯片组。绝大多数此类摄像机均为新奇的玩意儿（即 Pencam、 SpyC@m 和 LegoCam）。

*   Aiptek PenCam 系列
*   Digitaldream 系列
*   Dolphin Peripherals 系列
*   Trust SpyC@m 系列
*   Lego LegoCam
*   Welback Coolcam

想要查阅更完整的使用 stv680 芯片组的网络摄像机列表请点击[这里](http://webcam-osx.sourceforge.net/cameras/index.php?orderBy=controller).

### linux-uvc

*   Logitech Quickcam Pro 5000
*   Logitech Quickcam Pro 9000
*   Logitech Quickcam Orbit MP
*   Microdia Pavilion Webcam (on MSI PR200)

You can find a full list of supported UVC devices [here](http://linux-uvc.berlios.de/).

自从 kernel 2.6.26 开始，linux-uvc 已经是kernel的一部分。只需要加载模块 uvcvideo 即可。

***Note:** 但此驱动不支持V4L1。*

### ov51x-jpeg

*   Sony EyeToy
*   Chicony DC-2120
*   Chicony DC-2120 pro
*   Trust Spacecam 320
*   Hercules Webcam Deluxe
*   Hercules Webcam Classic
*   Creative Live! Cam Notebook Pro VF0400
*   Creative Live! Cam Vista IM
*   Creative Live! Cam Vista IM VF0420
*   Creative Vista Webcam VF0330
*   ASUS webcam Model?
*   Philips PCVC820K/00
*   NGS showtime plus
*   HP VGA Webcam with Integrated Microphone

This is a kernel module found in the AUR with some additions to the original driver that provide jpeg decompression.

For me to get my "Creative Live! Cam Vista IM" working with Skype I had to add this line to /etc/modprobe.d/modprobe.conf

```
options ov51x-jpeg forceblock=1

```

### r5u870 (Ricoh)

*   HP Pavilion Webcam
*   HP Webcam 1000
*   Sony VAIO VGP-VCCx

绝大部分索尼的笔记本电脑采用Ricoh的网络摄像机.

请安装 [r5u87x-hg](https://aur.archlinux.org/packages/r5u87x-hg/) (同时提供了固件) 并运行 `loader` 命令。

### stk11xx (Syntek)

*   Integrated camera in lot of Asus laptops
*   Asus A8J, F3S, F5R, F9E, VX2S, V1S, A6T

Just install this [AUR package](https://aur.archlinux.org/packages.php?do_Details=1&ID=12669). It contains the right kernel module.

## 确定为你的网络摄像机加载所需的模块

将网络摄像头的[内核模块](/index.php/Kernel_modules#Loading "Kernel modules") 加入 `/etc/modules-load.d/webcam.conf`。这样一来，当系统启动时，你的网络摄像机模块就会加载到内核中。

如果你的摄像头是使用USB接口，系统 *应该会*自动加载合适的驱动。 如果成功，可以在你插入摄像头之后检查dmesg，应该可以看到如下面的信息.

 `$ dmesg | tail` 
```
sn9c102: V4L2 driver for SN9C10x PC Camera Controllers v1:1.24a
usb 1-1: SN9C10[12] PC Camera Controller detected (vid/pid 0x0C45/0x600D)
usb 1-1: PAS106B image sensor detected
usb 1-1: Initialization succeeded
usb 1-1: V4L2 device registered as /dev/video0
usb 1-1: Optional device control through 'sysfs' interface ready
usbcore: registered new driver sn9c102

```

## 权限

要使用摄像头，首先必须让用户对`/dev/video0`具备权限.

### udev

如果你使用udev (在kernel 2.6.13里是默认的)，你只需把用户加到组**video**中：

```
$ groups

```

用root权限把用户添加到组中：

```
# gpasswd -a <username> video

```

### devfs

将以下两行添加到你的`/etc/devfsd.conf`. 文件中。这将允许普通用户使用`/dev/video0` （你的网络摄像机）。

```
# Give normal users access to webcam
REGISTER        video0       PERMISSIONS     root.users 0660

```

## 获取软件以使用你的网络摄像机

Version 2.6.27 of the Linux kernel supports [many new webcam drivers](http://mxhaard.free.fr/spca5xx.html). Legacy Video4Linux API has been dropped, and these drivers now only support Video4Linux version 2\. Pixel format decoding has been pushed to user space, since Video4Linux version 2 does not support kernel space decoding. The libv4l library provides userland applications with pixel decoding services and will be used by most programs. Other compatibility layers are also available.

**If your device is created but your image looks strange (mine was nearly completely green), you probably need this.**

If the application has V4L2 support but no pixelformat support (eg: cheese) then use the following command:

```
 LD_PRELOAD=/usr/lib/libv4l/v4l2convert.so cheese

```

If the application only supports the older version of V4L (skype is the most popular of this kind of software) then use this command:

```
 LD_PRELOAD=/usr/lib/libv4l/v4l1compat.so skype

```

**Hint:** 为了不用每次都输入长长的命令，根据使用摄像机的类型，可以在~/.bashrc或~/.xinitrc里添加一条命令。比如：

```
 export LD_PRELOAD=/usr/lib/libv4l/v4l2convert.so

```

或者

```
 export LD_PRELOAD=/usr/lib/libv4l/v4l1compat.so

```

### Cheese

Cheese is the GNOME photo/video taking client. It is similar to Photo Booth in Mac OS X. It is now in extra and is also part of the gnome-extra group

### GTK+ UVC Viewer (guvcview)

[guvcview](http://guvcview.berlios.de/) is a simple GTK interface for capturing (with sound!) and viewing video from devices supported by the linux UVC driver. Available in the [guvcview](https://www.archlinux.org/packages/?name=guvcview)。

### Kopete

Kopete is the [KDE](/index.php/KDE "KDE") instant messaging (IM) client. As of KDE 3.5, it has support for MSN and Yahoo! webcams, but not every cam works yet. It is included in the kdenetwork package.

### Kamoso

Application to take pictures and videos out of your webcam for KDE. Available in the AUR: [kamoso](https://www.archlinux.org/packages/?name=kamoso).

### xawtv

这是一个基本的 Video4Linux 设备查看器，尽管它专用于电视调节卡，但其亦可很好地管理网络摄像机。它会在窗口中显示你的网络摄像机所看到的一切。可以使用以下命令安装：

```
# pacman -S xawtv

```

运行以下命令：

```
$ xawtv -c /dev/video0

```

If you're using an nVidia graphic card, and you get an error like

```
X Error of failed request:  XF86DGANoDirectVideoMode
 Major opcode of failed request:  139 (XFree86-DGA)
 Minor opcode of failed request:  1 (XF86DGAGetVideoLL)
 Serial number of failed request:  69
 Current serial number in output stream:  69

```

you should instead run it as:

```
$ xawtv -nodga

```

### VLC

VLC can also be used to view and record your webcam. In VLC's file menu, open the 'Capture Device...' dialog and enter the video and audio device files. Or from the command line, do:

```
$ vlc v4l:// :v4l-vdev="/dev/video0" :v4l-adev="/dev/audio2"

```

This will make VLC mirror your webcam. To take stills, simply choose 'Snapshot' in the 'Video' menu. To record the stream, you add a --sout argument, e.g.

```
$ vlc v4l:// :v4l-vdev="/dev/video0" :v4l-adev="/dev/audio2" --sout "#transcode{vcodec=mp1v,vb=1024,scale=1,acodec=mpga,ab=192,channels=2}:duplicate{dst=std{access=file,mux=mpeg1,dst=/tmp/test.mpg}}"

```

(Obviously a bit overkill with regard to the bitrates but it's fine for testing purposes.) Notice that this will not produce a mirror on the display - in order to see what you're recording, you would need to add the display as a destination to the argument:

```
... :duplicate{dst=display,dst=std{access= ....

```

(Though this can tax older hardware somewhat...)

### MPlayer

使用 [MPlayer](/index.php/MPlayer "MPlayer")来给摄像头截屏，需要在终端中运行下列命令：

```
$ mplayer tv:// -tv driver=v4l2:width=640:height=480:device=/dev/video0 -fps 15 -vf screenshot

```

From here you have to press `s` to take the snapshot. The snapshot will be saved in your current folder as **shotXXXX.png**. 使用如下命令，来录制视频：

```
$ mencoder tv:// -tv driver=v4l2:width=640:height=480:device=/dev/video0:forceaudio:adevice=/dev/dsp -ovc lavc -oac mp3lame -lameopts cbr:br=64:mode=3 -o <filename>.avi

```

按Ctrl+Z停止录制。

### FFmpeg

参见 [FFmpeg#Recording webcam](/index.php/FFmpeg#Recording_webcam "FFmpeg").

### ekiga

这是一款非常类似于 Microsoft Netmeeting 的软件，以前名叫gnomemeeting。 可以使用以下命令安装：

```
# pacman -S ekiga

```

该程序会自动为你设置好一切。

### Sonic-snap

Sonic-snap [[2]](http://www.stolk.org/sonic-snap/) is a viewer/grabber for sn9c102-based webcams **only**. [Available in AUR.](https://aur.archlinux.org/packages.php?ID=6333)

### Skype

新版的skype具备视频支持。 在选项设置中，测试摄像头，可双击全屏。使用一下命令安装：

```
# pacman -S skype

```

如果从 skype 中获得的图片出现颜色不正常，请阅读[使用网络摄像头软件](/index.php/Webcam_Setup_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E8.8E.B7.E5.8F.96.E8.BD.AF.E4.BB.B6.E4.BB.A5.E4.BD.BF.E7.94.A8.E4.BD.A0.E7.9A.84.E7.BD.91.E7.BB.9C.E6.91.84.E5.83.8F.E6.9C.BA "Webcam Setup (简体中文)").

如果运行 x86-64，需要[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") Multilib 仓库中的 [lib32-v4l-utils](https://www.archlinux.org/packages/?name=lib32-v4l-utils)，并用下面命令运行 skype：

```
LD_PRELOAD=/usr/lib32/libv4l/v4l1compat.so skype

```

可以设置 skype 别名或修改 Skype 图标的命令行以方便使用。