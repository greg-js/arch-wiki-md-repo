# Lenovo ThinkPad X120e

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [IBM ThinkPad X100e](/index.php/IBM_ThinkPad_X100e "IBM ThinkPad X100e")

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

**This article or section is out of date.**

**Reason:** rc.conf, kernel 2.6 (Discuss in [Talk:Lenovo ThinkPad X120e#](https://wiki.archlinux.org/index.php/Talk:Lenovo_ThinkPad_X120e))

Installation instructions for the Lenovo ThinkPad X120e. Should work for X121e too.

## Contents

*   [1 Video drivers](#Video_drivers)
*   [2 Wireless](#Wireless)
*   [3 Audio](#Audio)
*   [4 Input](#Input)
    *   [4.1 TrackPoint scrolling (wheel emulation)](#TrackPoint_scrolling_.28wheel_emulation.29)
    *   [4.2 Disabling the TrackPad](#Disabling_the_TrackPad)
    *   [4.3 TrackPoint speed and sensitivity](#TrackPoint_speed_and_sensitivity)
*   [5 Power saving](#Power_saving)
    *   [5.1 Disable Bluetooth](#Disable_Bluetooth)
    *   [5.2 ATI video card powersaving](#ATI_video_card_powersaving)
    *   [5.3 CPU undervolting](#CPU_undervolting)
        *   [5.3.1 Using PHC](#Using_PHC)
        *   [5.3.2 Using tpc](#Using_tpc)
    *   [5.4 Fan control](#Fan_control)
*   [6 Suspend and hibernation](#Suspend_and_hibernation)
*   [7 See also](#See_also)

## Video drivers

Users have the choice between the open source [ATI](/index.php/ATI "ATI") video driver or the closed source [Catalyst](/index.php/Catalyst "Catalyst") video driver.

## Wireless

The Thinkpad x120e is available with one of two wireless cards.

*   The Realtek BGN Wifi card is currently supported out of the box by the rtl8192ce driver, which was integrated into the Linux kernel as of version 3.2\. This card, however, suffers from access point association and connection stability problems, especially in meshed wireless networks due to poor wireless radius detection. Since driver development by Realtek effectively stopped as of January 2012, the general consensus among many owners online has been to swap out this wireless card for a different better supported half-mini PCI card such as the Intel 6230\. This however requires a BIOS patch to remove Lenovo's hardware restriction on which wireless cards can be used in the computer. More information in regards to that can be found in [this](http://forums.mydigitallife.info/threads/20223-Remove-whitelist-check-add-ID-s-to-break-hardware-restrictions-mod-requests/page175) thread.

*   The Broadcom ABGN Wifi card is currently supported by the b43 driver. This driver is recommended over the broadcom-wl.

(Note from the [ThinkWiki](http://www.thinkwiki.org/wiki/Category:X120e) the Realtek card is either FRU 60Y3247 or 60Y3249, the Broadcom is FRU 60Y3251 - which should work without needing modification of the bios)

## Audio

The kernel modules work, but the HDMI audio is the primary device (not the speaker). You can swap that:

 `$ vim ~/.asoundrc` 

```
defaults.pcm.card 1
defaults.pcm.device 0
defaults.ctl.card 1

```

Note: Alternatively, you can accomplish the same thing by configuring the snd-hda-intel module:

 `$ grep snd-hda-intel /etc/modprobe.d/snd-hda-intel.conf`  `options snd-hda-intel index=1` 

By specifying index you should no longer specify the default in `~/.asoundrc`.

## Input

### TrackPoint scrolling (wheel emulation)

See [TrackPoint](/index.php/TrackPoint "TrackPoint").

### Disabling the TrackPad

If you try to use your x120e lying down you will notice its very easy to hit the TrackPad buttons and invert the functionality of the other inputs(fun). See [Touchpad Synaptics#Synclient](/index.php/Touchpad_Synaptics#Synclient "Touchpad Synaptics") to disable the TrackPad.

### TrackPoint speed and sensitivity

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [TrackPoint](/index.php/TrackPoint "TrackPoint").**

**Notes:** please use the second argument of the template to provide more detailed indications. (Discuss in [Talk:Lenovo ThinkPad X120e#](https://wiki.archlinux.org/index.php/Talk:Lenovo_ThinkPad_X120e))

You can up your trackpoint speed with next command:

```
$ xinput --set-prop 13 'Device Accel Profile' 6

```

If you want this to be permanent speed up add the option to your /etc/X11/xorg.conf.d/20-thinkpad.conf (if this is your X11 trackpoint config, of course):

```
Option		"AccelerationProfile"   "6"

```

To more acceleration profile read man "xorf.conf.d"

## Power saving

See [power saving](/index.php/Power_saving "Power saving").

### Disable Bluetooth

See [Power saving#Bluetooth](/index.php/Power_saving#Bluetooth "Power saving").

### ATI video card powersaving

Under the opensource ATI video card driver you can control the clockspeed of the GPU, see [ATI#Powersaving](/index.php/ATI#Powersaving "ATI").

### CPU undervolting

**Warning:** Undervolting can lead to instability and consequently data loss, only you are responsible if you break something

#### Using PHC

The Fusion Processor can be undervolted with the PHC-K8 tool. See [PHC](/index.php/PHC "PHC") for usage information. For the AMD Fusion you'll want to download [phc-k8](https://aur.archlinux.org/packages/phc-k8/)<sup><small>AUR</small></sup> from the AUR.

**Note:** In order to lower CPU power usage you must actually raise the PHC values. (somewhat counter-intuitive)

"24 26 52" is what I have my E-350 set to. The three numbers represent 1600mhz, 1200mhz and 800mhz.

**Warning:** The three values listed above are stable on MY processor. Due to variables during production, you're chip may be able to be undervolted more or LESS. Feel free to post the stable values that you reach to this wiki.

#### Using tpc

Another method for undervolting is [tpc](https://aur.archlinux.org/packages/tpc/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/tpc)]</sup>. It is more intuitive then PHC tool and needs Kernelmodule _cpuid_ and _msr_.

Information output available cores and current frequencies and voltage:

```
# tpc -l

```

Example how to use:

**Warning:** DO THIS AT YOUR OWN RISK!!!! DON'T USE THIS VALUES!!! Approach yourself to values whitch are working for you! This is just an example how to use tpc

```
# tpc -set core all pstate 2 frequency 825 vcore 0.825   
# tpc -set core all pstate 1 frequency 1320 vcore 1.2250
# tpc -set core all pstate 0 frequency 1650 vcore 1.3000

```

### Fan control

The X120e's fan spins constantly but luckily can be controlled by the user.

**Warning:** Modify fan settings at your own risk, only you are responsible if you toast your laptop or your lap.

**Note:** Even with undervolting the APU produces enough heat to have to occasionally run the fan even at idle.

To enable manual fan control place the following into `/etc/modprobe.d/modprobe.conf`:

```
options thinkpad_acpi fan_control=1

```

Now you have to reload thinkpad_acpi module or reboot your netbook.

```
# rmmod thinkpad_acpi && modprobe thinkpad_acpi

```

Now it should look like that:

```
# cat /proc/acpi/ibm/fan 
status:		disabled
speed:		0
level:		0
commands:	level <level> (<level> is 0-7, auto, disengaged, full-speed)
commands:	enable, disable
commands:	watchdog <timeout> (<timeout> is 0 (off), 1-120 (seconds))

```

At this point the fan will still be safely under the system's control. You can either directly modify the values in /proc/acpi/ibm (NOT RECOMMENDED. e.g. 'echo level 1 > /proc/acpi/ibm/fan') or install a fan control daemon such as [thinkfan](https://aur.archlinux.org/packages/thinkfan/)<sup><small>AUR</small></sup> from the AUR.

## Suspend and hibernation

Suspend works out of the box, but hibernate may fail - the system usually hangs with a black screen and a blinking power button led. To fix this we need to modify the hibernation mode; using pm-utils is just a matter of creaing a file /etc/pm/config.d/hibernate_mode containing a single line:

```
HIBERNATE_MODE="shutdown"

```

## See also

[X120e on ThinkWiki](http://www.thinkwiki.org/wiki/Category:X120e) [Undervolting the AMD Fusion with PHC-tool](http://www.linux-phc.org/forum/viewtopic.php?f=7&t=269)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Lenovo_ThinkPad_X120e&oldid=412575](https://wiki.archlinux.org/index.php?title=Lenovo_ThinkPad_X120e&oldid=412575)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Lenovo](/index.php/Category:Lenovo "Category:Lenovo")