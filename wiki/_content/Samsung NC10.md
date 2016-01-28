# Samsung NC10

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

This article aims to provide information on installing and setting up Arch Linux on the Samsung NC10.

A lot of the information is derived from the [Arch Forum](https://bbs.archlinux.org/viewtopic.php?id=58117), and from several hints scattered around in the ArchWiki.

## Contents

*   [1 Common issues](#Common_issues)
*   [2 Installation](#Installation)
*   [3 Configure your installation](#Configure_your_installation)
    *   [3.1 Network](#Network)
    *   [3.2 Video](#Video)
    *   [3.3 Initial brightness](#Initial_brightness)
    *   [3.4 Graphics adapter](#Graphics_adapter)
        *   [3.4.1 External VGA](#External_VGA)
    *   [3.5 Audio](#Audio)
    *   [3.6 Suspend and hibernate](#Suspend_and_hibernate)
    *   [3.7 Fn keys](#Fn_keys)
    *   [3.8 Power saving](#Power_saving)
    *   [3.9 BIOS](#BIOS)

## Common issues

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**This article or section needs language, wiki syntax or style improvements.**

**Reason:** Reformat list, first person (Discuss in [Talk:Samsung NC10#](https://wiki.archlinux.org/index.php/Talk:Samsung_NC10))

*   using KMS (as of xorg-video-intel 2.8.1), No brightness control with xbacklight. ([workaround with setpci](https://bbs.archlinux.org/viewtopic.php?id=74914), the issue might be solved with the next intel driver 2.9)
*   On kernel 3.6.2-1 and 3.6.3-1:
    *   system will not boot unless acpi=off is added as kernel parameter
    *   "dmesg | grep microcode" will show "Atom PSE erratum detected", see [Microcode](/index.php/Microcode "Microcode") page for a solution
*   On kernel 3.17.4-1
    *   I cant [suspend or hibernate](/index.php/Suspend_and_hibernate "Suspend and hibernate"), but with linux-lts 3.14.25-1 it's ok (see also [this section](/index.php/Suspend_and_hibernate#Suspend.2Fhibernate_doesn.27t_work "Suspend and hibernate")).

## Installation

Use the USB image provided at the official download locations or the ISO if you have an external optical drive. You can also use unetbootin to easily create a boot device. If you use an usbkey, be aware that you must (arguably) format it in FAT32.

## Configure your installation

### Network

LAN uses the sky2 module and should work out-of-the-box. Kernels prior to 2.6.37 use the ath5k module for WLAN. Later kernels use brcmsmac/brcmfmac and may require blacklisting bcma. See [Broadcom wireless#brcmsmac/brcmfmac](/index.php/Broadcom_wireless#brcmsmac.2Fbrcmfmac "Broadcom wireless") for details.

### Video

### Initial brightness

The brightness can be set with the following command:

```
setpci -s 00:02.1 F4.B=FF

```

Where FF is the highest level of brightness. This parameter moves in the range 00 to FF. Don't set it too low otherwise your backlight will turn off!

### Graphics adapter

The Video controller is a typical Intel chipset that works with the [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) driver.

To save some interrupts, and therefore power, you can disable dri in your `xorg.conf`. This disables 3D effects; however if you do not need them this could be an option.

```
Section "Device"
Option "NoDRI"
Identifier "Card0"
Driver "intel"
VendorName "Intel Corporation"
BoardName "Mobile 945GME Express Integrated Graphics Controller"
BusID "PCI:0:2:0"
EndSection

```

#### External VGA

External VGA works out of the box with [xorg-xrandr](https://www.archlinux.org/packages/?name=xorg-xrandr).

In order to prevent problems when switching to console or when unplugging the external monitor, make sure to specify the frequency along with the mode, for example :

```
xrandr --output VGA --mode 1280x1024 --rate 60

```

Dual head positioning works also perfectly: [Xorg#Multiple monitors](/index.php/Xorg#Multiple_monitors "Xorg").

### Audio

The audio device is an Intel HD. You will need to follow the instructions at [ALSA#No Sound with Onboard Intel Sound Card](/index.php/ALSA#No_Sound_with_Onboard_Intel_Sound_Card "ALSA") to get output from the main speakers.

Since alsa 1.0.19 distributed in Archlinux repositories, you do not need to manually install alsa driver. Everything is working out of the box: onboard microphone and speakers, audio off on earphone plugging.

**Troubleshooting :**

*   If the volume is too low, or lower than in Windows run alsamixer, and set "front" to 100%.

*   If the microphone does not work, press `F4` in alsamixer and play with the settings (boost to 0, digital and capture to mid-values, and input to front-mic should be a sensible default).

Note that settings can be saved with "alsactl store".

*   One user reported that he had to disable every snd module in his rc.conf except for two: snd_hda_intel and snd_pcm_oss.

*   [deprecated] if the speakers do not mute when you plug in headphones, you may need to compile alsa (i use v1.0.18a ,[here](ftp://ftp.alsa-project.org/pub/driver/alsa-driver-1.0.18a.tar.bz2))

Extract the tar.bz2 and open a console on alsa source folder, install [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils) and execute these commands:

```
$ ./configure --with-cards=hda-intel --with-oss=yes --with-sequencer=yes
$ make
# make install

```

Then configure sound volume with alsamixer and reboot.

### Suspend and hibernate

If you want to use Suspend to RAM using [pm-utils](/index.php/Pm-utils "Pm-utils") then you'll need the following command to resume properly:

```
pm-suspend --quirk-vbestate-restore

```

**Note:** pm-suspend should work correctly without any quirks at the moment.

You can use this command not only to suspend from terminal but also in combination with [acpid](/index.php/Acpid "Acpid").

If after closing the lid your machine doesn't wake up from suspend correctly and needs to be resumed multiple times, you can try using the following workaround. This is an excerpt from `/etc/acpid/handler.sh` file:

```
    button/lid)
       if [ $(/bin/awk '{print $2}' /proc/acpi/button/lid/LID0/state) = closed ]; then
           /usr/sbin/pm-suspend
       fi
       ;;

```

In contrast hibernate works without "modifications" (except the ones mentioned in the [pm-utils](/index.php/Pm-utils "Pm-utils") article).

If you are a kde4/kdemod user you can take advantage of powerdevil (included in kdemod-core/kdemod-kdebase-workspace since release 4.2). Screen brightness, cpu scaling, suspend and hibernate all work flawlessly, without any hack.

Right after resume you may notice (i.e. in powertop) lost support for C2 and C4 CPU states. Those modes are likely to return within several minutes.

### Fn keys

Volume Controls worked out of the box in kdemod 4.2.

To bind the Fn keys to action, read [Extra keyboard keys](/index.php/Extra_keyboard_keys "Extra keyboard keys"). The suspend key (`Fn+ESC`) and disable touchpad (`Fn+F10`) keys should work out of the box. Note that suspend key is handled in /etc/acpi/handler.sh (see "power/sleep" case entry). If you use pm-utils, you should substitute the default action with the call to pm-suspend or pm-hibernate.

As an example, here is how to bind the keys for volume control:

1.  Install [xbindkeys](https://www.archlinux.org/packages/?name=xbindkeys) and [xorg-xbacklight](https://www.archlinux.org/packages/?name=xorg-xbacklight) for brightness control.
2.  Crate a config file in your home directory with the following content:

 `~/.xbindkeysrc` 

```
 "amixer sset Master 2+ &"
     m:0x0 + c:176
 "amixer sset Master 2- &"
     m:0x0 + c:174
 #"amixer sset Master 0 &"
 "amixer sset Master toggle &"
     m:0x0 + c:160
 #"sudo pm-suspend"
 #    m:0x0 + c:223
 "xbacklight +10"
     m:0x0 + c:233
 "xbacklight -10"
     m:0x0 + c:232

```

For your NC10 Fn keysums may differ. If any Fn keys do not work with the above `.xbindkeysrc`, you should check the keysum values with `xbindkeys -k`.

3\. Run `xbindkeys` and volume control should work within an X session!

To add additional bindings, you can get the codes of most of the Fn-keys with `xbindkeys -k`.

For the keys that are not recongnized, see:

```
dmesg | tail

```

This will help to find errors and find the solution.

If your screen is not bright enough, boot into Windows and set the brightness to maximum or just do it the boot process.

### Power saving

See [power saving](/index.php/Power_saving "Power saving").

### BIOS

There is no official support from Samsung on how to upgrade your BIOS from anything else than Windows XP / 7, although there's an exellent guide on how to update your BIOS without Windows installed on your computer at all [here](http://www.voria.org/forum/viewtopic.php?t=248).

Retrieved from "[https://wiki.archlinux.org/index.php?title=Samsung_NC10&oldid=377031](https://wiki.archlinux.org/index.php?title=Samsung_NC10&oldid=377031)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Samsung](/index.php/Category:Samsung "Category:Samsung")

Hidden category:

*   [Pages or sections flagged with Template:Style](/index.php/Category:Pages_or_sections_flagged_with_Template:Style "Category:Pages or sections flagged with Template:Style")