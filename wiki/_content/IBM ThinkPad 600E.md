# IBM ThinkPad 600E

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

**This article or section is out of date.**

**Reason:** Contains references to rc.conf, which is deprecated (Discuss in [Talk:IBM ThinkPad 600E#](https://wiki.archlinux.org/index.php/Talk:IBM_ThinkPad_600E))

## Contents

*   [1 To install:](#To_install:)
    *   [1.1 Audio](#Audio)
    *   [1.2 USB](#USB)
    *   [1.3 Graphics](#Graphics)
    *   [1.4 Software](#Software)
    *   [1.5 ACPI and APM](#ACPI_and_APM)
*   [2 See also](#See_also)

### To install:

Follow usual Arch Linux Guide except for the points below. The 600E sound card is notoriously challenging to configure in GNU/Linux.

#### Audio

Firstly the laptop BIOS must be set to Initialize and Quick Boot must be off. Then run alsaconf, which sould now pick up the sound card and write a new /etc/modprobe.d/modprobe.conf. If hotplug still tries to load cs461x and fails then blacklist it (/etc/hotplug/blacklist). You can also add the correct driver (snd-cs4236) to the MODULES variable of /etc/rc.conf so that it loads before hotplug starts.

The thinkpad also behaves differently on reset than it does on power on. The sound card driver may not load on reset.

Pcmcia_cs appears to trash the sound card driver on boot. You do not really need pcmcia_cs as hotplug should handle all but very old 16bit pcmcia cards. If you really want it then it is possible to stop it from probing certain ports and irq's. Otherwise you can just fix this by reloading the kernel module. Add this to your /etc/rc.local:

```
rmmod snd-cs4236
modprobe snd-cs4236
alsactl restore

```

You need to reload the alsa values because the sound card forgets its volume settings.

If you still have problems these settings may help. The /etc/rc.conf should include:

```
MOD_BLACKLIST=(snd_cs46xx snd_cs461x snd_cs4232 pcihp)
MODULES=(snd_cs4236)

```

Your /etc/modprobe.d/modprobe.conf should include:

```
options snd-cs4236 isapnp=0 cport=0x538 port=0x530 sb_port=0x220 fm_port=0x388 irq=5 dma1=1 dma2=0
alias snd-card-0 snd-cs4236

```

#### USB

The kernel cannot insert the pciehp module for some strange reason. Skip it by adding it to /etc/hotplug/blacklist

USB devices can be quite tempremental. The solution appears to be set pci=noacpi as a kernel argument.

#### Graphics

The graphics card is a Neomagic card (driver is **neomagic**). To play DVD's you will need to pass an 'OverlayMem' option to the driver. The video device section in /etc/X11/xorg.conf should look like this:

```
Section "Device"
	Identifier  "Card0"
	Driver      "neomagic"
	VendorName  "Neomagic Corporation"
	BoardName   "NM2200 [MagicGraph 256AV]"
	VideoRam    2560
	BusID       "PCI:1:0:0"
	Option      "OverlayMem"	"829440"
EndSection

```

N.B. DVD playback only works with a display depth of 16bit as there is not enough video RAM for 32bit depth. The LCD screen is capable of 1024x768.

#### Software

There is a package called **thinkpad** that installs a number of modules specific to thinkpads. A related packege called **tpctl** supplies a configuration program that allows you to change thinkpad specific stuff. To get it working you need to create the thinkpad devices in /dev.

#### ACPI and APM

Both ACPI and APM work in this machine without any big problems. The stock Arch Linux kernel comes with ACPI so just use that. If the machine refuses to poweroff or ACPI isn't working ACPI=FORCE maybe needed.

## See also

*   This report has been listed in the [Linux Laptop and Notebook Installation Survey: IBM](http://tuxmobil.org/ibm.html).
*   [The 600E section on ThinkWiki](http://www.thinkwiki.org/wiki/Category:600E)

Retrieved from "[https://wiki.archlinux.org/index.php?title=IBM_ThinkPad_600E&oldid=382938](https://wiki.archlinux.org/index.php?title=IBM_ThinkPad_600E&oldid=382938)"