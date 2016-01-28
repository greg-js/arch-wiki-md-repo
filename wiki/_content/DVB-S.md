# DVB-S

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [DVB-T](/index.php/DVB-T "DVB-T")
*   [MythTV Walkthrough](/index.php/MythTV_Walkthrough "MythTV Walkthrough")

This article describes the setup and use of DVB-S (sat TV) cards on Arch Linux.

**Warning:** This was only tested with the Pinnacle PCTV Sat, and may not work or will not help you with different cards.

## Contents

*   [1 Load required Modules](#Load_required_Modules)
    *   [1.1 Pinnacle PCTV Sat](#Pinnacle_PCTV_Sat)
    *   [1.2 Additional modules: S2-liplianin](#Additional_modules:_S2-liplianin)
        *   [1.2.1 Setup](#Setup)
*   [2 Setup Permissions](#Setup_Permissions)
*   [3 Scanning channels](#Scanning_channels)
    *   [3.1 Using scan](#Using_scan)
    *   [3.2 Using w_scan](#Using_w_scan)
        *   [3.2.1 DiSEqC switch scanning (AKA multiple satellite LNB)](#DiSEqC_switch_scanning_.28AKA_multiple_satellite_LNB.29)
*   [4 Switching channels](#Switching_channels)
*   [5 Software](#Software)
    *   [5.1 Kaffeine](#Kaffeine)
        *   [5.1.1 Importing channel list](#Importing_channel_list)
    *   [5.2 Me-tv](#Me-tv)
    *   [5.3 Klear](#Klear)
    *   [5.4 Xine](#Xine)
*   [6 Additional Resources](#Additional_Resources)
    *   [6.1 TV Cards in general](#TV_Cards_in_general)

## Load required Modules

You have to lookup the chipset of your specific card; tools like **lshwd** may help you.

### Pinnacle PCTV Sat

This card uses bt878 and cx24110 as chipset.

Load them (under root) with:

```
# modprobe dvb-bt8xx
# modprobe cx24110

```

If you want Arch to boot them on startup, add both modules to `MODULES` in `/etc/rc.conf`.

### Additional modules: S2-liplianin

However, there is not a working kernel module for all (especially newer) devices.

Igor M. Liplianin manages some additional modules at his [mercurial repository](https://pikacode.com/liplianin/s2-liplianin/).

#### Setup

First of all, you have to download and prepare the source code.

```
$ hg clone [https://pikacode.com/liplianin/s2-liplianin](https://pikacode.com/liplianin/s2-liplianin)

```

If you do not have installed mercurial, you will get an error message: `hg: command not found`

You can either download the package [mercurial](https://www.archlinux.org/packages/?name=mercurial) and try the obove command again or download the source code from [here](https://pikacode.com/liplianin/s2-liplianin/) and extract it manually.

After obtaining the code, change the working directory to the extracted folder:

```
$ cd s2-liplianin

```

Unfortunately not all modules of liplianin are compatible with recent kernels and cause some trouble if you want to compile them hence you have to exclude these modules from the build process (if you do not need them). You can choose which modules you want to build by executing:

```
$ make config

```

which will create a config file: `v4l/.config`.

**Note:** If you want to edit the config file with another interface, take a look at the 'Module selection rules' section within the file `Install`.

After that, you have to build the chosen modules:

```
$ make

```

**Note:** It is very likely, that some modules will not compile. Try to exclude them (one step earlier) and run 'make' again.

If all configured modules were compiled successfully, you can install the modules at the kernel's default modules directory by executing:

```
# make install

```

After that, reboot your machine.

## Setup Permissions

To use your DVB-S card as user add him to the `video` group:

```
# gpasswd -a [username] video

```

## Scanning channels

**Note:** You can skip this part if you use Kaffeine.

Most applications like szap or xine are needing a channel list created by **scan**, which is part of **dvb-utils**. You will find the dvb-utils package under the name [linuxtv-dvb-apps](https://www.archlinux.org/packages/?name=linuxtv-dvb-apps).

### Using scan

**scan** needs an channel to initialize scanning. In `/usr/share/dvb/dvb-s/` are some files which contain these channels; you will need that one that fits the satellite you are watching from.

The following command will scan all channels and save them to `channels.conf`:

```
$ scan -x0 -t1 -s1 /usr/share/dvb/dvb-s/[your satellite] | tee channels.conf

```

**Note:** The channel file does not have to be called `channels.conf` but it is more convenient as you will see later.

**Note:** Depending on your satellite dish setup you may have to try other arguments.

### Using w_scan

[w_scan](https://aur.archlinux.org/packages/w_scan/)<sup><small>AUR</small></sup> allows for automatic scanning of channels without configuration. Install it then issue:

```
# w_scan -c [your country] > ~/someChannels.conf

```

Alternatively you can also scan using the satellite position like 19.5E for Astra 1\. Scans like that can be done as follows:

```
# w_scan -fs -s S19E5 > ~/someChannels.conf

```

You can also add the -X flag to generate tzap/czap/xine output instead of vdr output.

```
# w_scan -X -c AU > ~/AustraliaChannels.conf

```

#### DiSEqC switch scanning (AKA multiple satellite LNB)

If you have a LNB with a DiSEqC switch in it you can manually select that using the -D option like so:

```
# w_scan -fs -s S23E5 -D 1c > ~/someChannels.conf

```

The above line should work but not all found channels where actually saved. The line below worked perfectly for me:

```
# w_scan -fs -s S23E5 -a 0 -D 1c -o 7 -e 2 > ~/someChannels.conf

```

**Warning:** I did found out that when using a LNB with a DiSEqC switch it is way more convenient to use -X ouptut which you can use in for example mplayer. Just append "-X" before the ">" that you see above.

## Switching channels

**Note:** szap only works with satellite TV.

By using **zap**, which comes with **dvb-utils**, you can switch channels, so you do not have to rely on the abilities of your player.

**szap** needs the channel file we created earlier; it will try `~/.szap/channels.conf` by default. You can move the `channels.conf` there or you can use the `"-c"` command-line option.

Switching channels works like this:

```
$ szap -r [channel]

```

**Note:** szap needs to keep running.

You can list all available channels with:

```
$ szap -q

```

Now you can watch the stream for example with xine:

```
$ xine -g stdin://mpeg2 < /dev/dvb/adapter0/dvr0

```

or with mplayer:

```
$ mplayer /dev/dvb/adapter0/dvr0

```

or with mplayer, but using DVB directly:

```
$ mplayer "dvb://RTL Television"

```

You can find all the channel names by running szap -q (assuming the channel list is also in ~/.szap/channels.conf).

## Software

### Kaffeine

Kaffeine is a really nice player; it supports EPG, time-shifting, and recording. Additionally Kaffeine has built-in channel-searching.

Install it with [kaffeine](https://www.archlinux.org/packages/?name=kaffeine) from the [official repositories](/index.php/Official_repositories "Official repositories").

*   [More Information](https://archlinux.org/packages/search/?q=kaffeine)
*   [Project page](http://kaffeine.sourceforge.net/)

#### Importing channel list

*   Linosaw.de provides [channels.conf](http://www.linowsat.de/settings/vdr.html) files for [VDR](/index.php/VDR "VDR")
*   [conv2conf](http://free.pages.at/cleditor/vdr2kaffeine.htm) converts these files into kaffeine channel list format

### Me-tv

Me-tv is a simple but powerfull dvb-viewer, supporting EPG, recording and channel-searching with a light-weight gui.

It is available in the [AUR](/index.php/AUR "AUR"): [me-tv](https://aur.archlinux.org/packages/me-tv/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/me-tv)]</sup> is the stable version, [me-tv-bzr](https://aur.archlinux.org/packages/me-tv-bzr/)<sup><small>AUR</small></sup> is the development branch.

### Klear

[Klear](http://klear.org) is also a really nice player, but more than 4 years old (last release 2006). It supports EPG, time-shifting, and recording, videotext. Channel-searching is still missing. Install it from AUR: [klear](https://aur.archlinux.org/packages/klear/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/klear)]</sup>.

### Xine

Copy your channel file to `~/.xine/channels.conf`.

Watch a specific channel with following command:

```
$ xine dvb://[channel]

```

or use the playlist editor in Xine

## Additional Resources

### TV Cards in general

*   [Ubuntuusers.de-Wiki](http://wiki.ubuntuusers.de/TV-Karten) (german)

Retrieved from "[https://wiki.archlinux.org/index.php?title=DVB-S&oldid=399529](https://wiki.archlinux.org/index.php?title=DVB-S&oldid=399529)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Multimedia](/index.php/Category:Multimedia "Category:Multimedia")
*   [TV cards](/index.php/Category:TV_cards "Category:TV cards")

Hidden category:

*   [Pages with broken package links](/index.php/Category:Pages_with_broken_package_links "Category:Pages with broken package links")