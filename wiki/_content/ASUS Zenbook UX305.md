# ASUS Zenbook UX305

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

**This article is a stub.**

**Notes:** please use the first argument of the template to provide more detailed indications. (Discuss in [Talk:ASUS Zenbook UX305#](https://wiki.archlinux.org/index.php/Talk:ASUS_Zenbook_UX305))

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**This article or section needs language, wiki syntax or style improvements.**

**Reason:** Early-stage draft, logging noise easily reproducable by owners of the particular hardware and distracts from actual workarounds (Discuss in [Talk:ASUS Zenbook UX305#](https://wiki.archlinux.org/index.php/Talk:ASUS_Zenbook_UX305))

This page contains instructions, tips, pointers, and links for installing and configuring Arch Linux on the [ASUS Zenbook UX305](http://www.asus.com/Notebooks_Ultrabooks/ASUS_ZENBOOK_UX305/Features/).

Hardware reference from UX305-FB041H. Model available since **12 feb 2015**.

## Contents

*   [1 Hardware lists](#Hardware_lists)
*   [2 Compatibility](#Compatibility)
    *   [2.1 Touchpad](#Touchpad)
    *   [2.2 Wifi](#Wifi)
    *   [2.3 Graphics](#Graphics)
    *   [2.4 QHD monitor](#QHD_monitor)
    *   [2.5 Function Keys](#Function_Keys)
        *   [2.5.1 Brightness Keys](#Brightness_Keys)
*   [3 See also](#See_also)

## Hardware lists

See [[1]](https://gist.github.com/anonymous/6363a5462af10ee18c0c) for specific hardware information.

See [[2]](https://gist.github.com/precurse/6dc1990cd000551c8f11) for UX305CA (Skylake) hardware information

## Compatibility

### Touchpad

See [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics") for details.

Multi-touch scrolling works as of kernel 3.16.

If default Palm Detection doesn't work well, one can manually disable part of the trackpad by setting AreaEdge properties.

You can do this on the fly or add these parameters in the config file:

```
 $ synclient AreaLeftEdge=500
 $ synclient AreaRightEdge=2500

```

**UX305C:**

Touchpad does not work at all. "i8042.nomux=1 i8042.noloop=1" do not work when appended to the kernel parameter line. Nothing shows in xinput

This is how the device appears in dmesg:

```
 pnp 00:04: Plug and Play ACPI device, IDs ATK3001 PNP030b (active)

```

There appears to be a bug filed: [[3]](https://bugzilla.kernel.org/show_bug.cgi?id=108581)

Anecdote: Fedora 23 on a UX305CA had several problems including the trackpad problem. All went away when rawhide kernel kernel-4.4.0.0.rc6.git1.2.fc24.x86_64 was installed. My best guess is that Skylake support in 4.4 plus the Fedora i2c driver fix is what made everything work. The Fedora 23 kernel-4.2.8-300.fc23.x86_64 had all these problems: improper screen resolution detection, at least some fn + arrow keys didn't generate PgUp etc, trackpad missing. I'm not sure how to translate this to Arch but I hope that it helps.

**Workaround**: I compiled 4.4.0-rc7 with the first 16 patches applied from [http://pkgs.fedoraproject.org/cgit/kernel.git/tree/](http://pkgs.fedoraproject.org/cgit/kernel.git/tree/), using the .config from my stock -ARCH kernel. Trackpad worked immediately on reboot

```
 $ xinput 
 Virtual core pointer                    	id=2	[master pointer  (3)]
   Virtual core XTEST pointer              	id=4	[slave  pointer  (2)]
   Logitech USB-PS/2 Optical Mouse         	id=9	[slave  pointer  (2)]
   Elan Touchpad                           	id=11	[slave  pointer  (2)]

```

### Wifi

Intel Dual Band wifi. Should work with recent kernels. 3.10+ with iwlwifi. See [Wireless network configuration#iwlwifi](/index.php/Wireless_network_configuration#iwlwifi "Wireless network configuration") for details.

### Graphics

As of [linux](https://www.archlinux.org/packages/?name=linux) 3.16, virtual terminals show a blank screen.

UEFI results with memory changes for the Intel graphic card:

```
 With 32-256MB memory assignment in bios: Works.
 With 512MB memory assignment: **X11 breaks**. 1/3th upper-part of screen semi works (swapped and mis-alligned), rest is noise/snow.

```

Bug: [https://bugzilla.redhat.com/show_bug.cgi?id=1151757](https://bugzilla.redhat.com/show_bug.cgi?id=1151757)

```
 Kernel 3.16 boots with usable tty/x11 via bootparam: nomodeset

```

See also [Intel graphics#SNA issues](/index.php/Intel_graphics#SNA_issues "Intel graphics").

### QHD monitor

Some models include a 3200x1800 screen, which display very tiny characters.

For Firefox and Thunderbird, add the below property in the about:config area

```
 layout.css.devPixelsPerPx=2.

```

### Function Keys

Kernel 3.16 with `acpi_listen`, when pressing `Fn+F12` (volup), `Fn+F11` (voldown), `Fn+F10` (mute), `F9` (disable mousepad):

```
 button/volumeup VOLUP 00000080 00000000 K
 button/volumedown VOLDN 00000080 00000000 K
 button/mute MUTE 00000080 00000000 K
 PNP0C14:00 000000ff 00000000

```

The light(sensor?) button (fn+a) returns:

```
 PNP0C14:00 000000ff 00000000

```

Tested with:

```
# modprobe -D asus-laptop

```

And/Or:

```
# modprobe -D asus-nb-wmi

```

No effect so far. Investigate.

#### Brightness Keys

For whatever reason, `xev` does not return any events for the standard brightness keys, but `F3` and `F4` seem to be detected as `XF86KbdBrightnessDown` and `XF86KbdBrightnessUp`, respectively.

## See also

*   [ASUS Zenbook UX303](/index.php/ASUS_Zenbook_UX303 "ASUS Zenbook UX303")
*   [https://wiki.debian.org/InstallingDebianOn/Asus/UX31a](https://wiki.debian.org/InstallingDebianOn/Asus/UX31a)
*   [https://wiki.debian.org/InstallingDebianOn/Asus/UX301LA](https://wiki.debian.org/InstallingDebianOn/Asus/UX301LA)

Retrieved from "[https://wiki.archlinux.org/index.php?title=ASUS_Zenbook_UX305&oldid=414086](https://wiki.archlinux.org/index.php?title=ASUS_Zenbook_UX305&oldid=414086)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [ASUS](/index.php/Category:ASUS "Category:ASUS")