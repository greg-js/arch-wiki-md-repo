# Banana Pi

From the [manufacturer](http://www.lemaker.org/):

> Banana Pi is an open-source single-board computer. It can run Android 4.4, Ubuntu, Debian, Rasberry Pi Image, as well as the Cubieboard Image. It uses the AllWinner A20 SoC, and has 1GB DDR3 SDRAM

BananaPi is a minimalist computer built for the [ARMv7-A architecture](https://en.wikipedia.org/wiki/ARMv7-A "wikipedia:ARMv7-A"). [More information about this project](http://www.bananapi.org/) and [technical specification](http://www.bananapi.org/p/product.html).

With its Allwinner SoC, a Banana board usually runs the well documented Sunxi Linux kernel. So for any hardware or kernel related tasks, you should [take a look at the Sunxi Wiki](https://linux-sunxi.org/Main_Page) as well.

## Contents

*   [1 Article preface](#Article_preface)
*   [2 Installing Arch Linux ARM](#Installing_Arch_Linux_ARM)
    *   [2.1 Download the source](#Download_the_source)
    *   [2.2 Installation](#Installation)
*   [3 Network](#Network)
    *   [3.1 SSH](#SSH)
*   [4 X.org driver](#X.org_driver)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 HDMI 1080p resolution](#HDMI_1080p_resolution)
        *   [5.1.1 Manually change the resolution](#Manually_change_the_resolution)
        *   [5.1.2 Automatically set resolution on boot](#Automatically_set_resolution_on_boot)
        *   [5.1.3 Display turns off after idle and does not turn on again](#Display_turns_off_after_idle_and_does_not_turn_on_again)
*   [6 Benchmarks](#Benchmarks)
    *   [6.1 SATA HDD](#SATA_HDD)
    *   [6.2 Network](#Network_2)
*   [7 See also](#See_also)

## Article preface

This article is strongly based on [Raspberry Pi](/index.php/Raspberry_Pi "Raspberry Pi"). Moreover this article is not meant to be an exhaustive setup guide and assumes that the reader has setup an Arch system before. Arch newbies are encouraged to read the [Beginners' guide](/index.php/Beginners%27_guide "Beginners' guide") if unsure how to preform standard tasks such as creating users, managing the system, etc.

## Installing Arch Linux ARM

### Download the source

First make sure you download the right image for your board. Although you can install the image for the Pi on the Pro as well for example, it doesn't include features like wireless support out of the box.

*   [Arch image for Banana Pi](http://www.lemaker.org/portal.php?mod=list&catid=4)
*   [Arch image for Banana Pro](http://www.lemaker.org/portal.php?mod=list&catid=5)

You can get customized images as well, like this [Arch / LXDE distribution for the Pi](http://blog.eldajani.net/banana-pi-arch-linux-customized-distribution/).

### Installation

See the [Banana Pi documentation](http://wiki.lemaker.org/SD_card_installation). You mostly need to download the [Arch Linux image](http://www.lemaker.org/article-26-1.html), unpack it, and dump it to your SD card. If your SD card is larger than 4G, you might want to resize the filesystem with a tool like `parted` etc.

## Network

### SSH

Luckily the [SSH daemon](/index.php/Secure_Shell "Secure Shell") is already installed by default. The default login data is:

| Type | Username | Password |
| Root | `root` | `bananapi` |
| User | `bananapi` | `bananapi` |

## X.org driver

The X.org driver for Banana Pi can be installed with the _xf86-video-fbdev_ package.

## Troubleshooting

### HDMI 1080p resolution

There are two methods to achieve changing the resolution from the default 1280x720/60Hz to 1920x1080/60Hz.

#### Manually change the resolution

Yield all possible HDMI-resolutions:

```
# cat /sys/class/graphics/fb0/modes

```

Change to desired resolution, e.g.:

```
# echo "D:1920x1080p-60" > /sys/class/graphics/fb0/mode

```

#### Automatically set resolution on boot

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

**The factual accuracy of this article or section is disputed.**

**Reason:** Arch does not provide the _sunxi-tools_ package in [official repositories](/index.php/Official_repositories "Official repositories"), so the `pacman -S ...` command in this section is probably specific to Arch Linux ARM. (Discuss in [Talk:Banana Pi#](https://wiki.archlinux.org/index.php/Talk:Banana_Pi))

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**This article or section needs language, wiki syntax or style improvements.**

**Reason:** Does not comply with [Help:Style](/index.php/Help:Style "Help:Style"). (Discuss in [Talk:Banana Pi#](https://wiki.archlinux.org/index.php/Talk:Banana_Pi))

You need to edit the kernel parameters in the `uEnv.txt` and provide the required parameters in `script.bin`. As the `script.bin` is a binary file, you need to use the Sunix tools, to convert it to a `script.fex` text file, make your changes and reconvert it to the `script.bin`. (see also [Sunxi fex guide](http://linux-sunxi.org/Fex_Guide#disp_init_configuration), [Sunix kernel arguments](http://linux-sunxi.org/Kernel_arguments) and [this thread](http://forum.lemaker.org/viewthread.php?action=printable&tid=1881)).

```
$ cd $HOME
$ mkdir $HOME/boot
$ sudo mount /dev/mmcblk0p1 $HOME/boot
$ cp $HOME/boot/script.bin $HOME/script.bin
$ pacman -S sunxi-tools
$ bin2fex $HOME/script.bin $HOME/script.fex

```

Now edit the created `script.fex` with an editor of your choice. Find the `[disp_init]` section and change/add the following parameters:

```
screen0_output_mode = 10
fb0_framebuffer_num = 3
fb0_scaler_mode_enable = 0
sunxi_fb_mem_reserve = 32

```

Save the changes, run `fex2bin`, backup and replace the previous `script.bin`.

```
$ $HOME/sunxi-tools/fex2bin $HOME/script.fex $HOME/script.bin
$ sudo cp $HOME/boot/script.bin $HOME/boot/script.bin.backup
$ sudo cp $HOME/script.bin $HOME/boot/script.bin

```

After creating a backup, you can change the `disp.screen0.output_mode` part of the `$HOME/boot/uEnv.txt` config with root privileges:

```
disp.screen0.output_mode=10:1920x1080p60

```

Unmount the boot partition, reboot and you should have 1080p/60Hz.

#### Display turns off after idle and does not turn on again

If you also have an issue with the display turning off after some idle time and not turning on again, you might want to disable [DPMS](/index.php/DPMS "DPMS"). Therefore add these X11 arguments to the proper configuration of your display manager.

```
-s 0 -dpms

```

For example, if you use [SLiM](/index.php/SLiM "SLiM"), you would modify in your `/etc/slim.conf`:

```
xserver_arguments -nolisten tcp vt07 -s 0 -dpms 

```

If for some reason the display still keeps turning off, e.g. when restarting your receiving device, you can turn it on again, by temporary change the resolution:

```
# echo "D:1280x720p-60" > /sys/class/graphics/fb0/mode
# echo "D:1920x1080p-60" > /sys/class/graphics/fb0/mode

```

## Benchmarks

Of course the following values might differ from yours, as they are dependend on the actual hardware connected (e.g. the HDD), but it might give you a feeling about the Banana Pi performances.

### SATA HDD

I connected two different external HDDs (3,5" with external energy source) via SATA-L to eSATA-I cable to the Banana Pi. My reading/writing results using [dd](/index.php/Benchmarking/Data_storage_devices#Using_dd "Benchmarking/Data storage devices") (average of 3 run times):

 HDD 1 (2 TB) | HDD 2 (4 TB) |
| Reading | 81.8 MB/s | 115.5 MB/s |
| Writing | 37.6 MB/s | 39,4 MB/s |

### Network

Due to the Allwinner A20 SoC limitations the BPi is not able to use the full theoretical bandwidth of the Gigabit Ethernet NIC. Yet the BPi is able to use about 510 MBits per second.

Benchmarking was done using `iperf` (average of 3 run times). Client BPi and Server were connected to a Gigabit capable switch via Gigabit Ethernet.

## See also

*   [Manufacturers FAQ](http://wiki.lemaker.org/FAQ)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Banana_Pi&oldid=412488](https://wiki.archlinux.org/index.php?title=Banana_Pi&oldid=412488)"