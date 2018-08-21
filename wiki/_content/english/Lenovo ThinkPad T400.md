Related articles

*   [Lenovo ThinkPad T400s](/index.php/Lenovo_ThinkPad_T400s "Lenovo ThinkPad T400s")

Installation instructions for the Lenovo ThinkPad T400.

## Contents

*   [1 System Specification](#System_Specification)
*   [2 Installation](#Installation)
*   [3 Network](#Network)
    *   [3.1 Ethernet](#Ethernet)
    *   [3.2 Wireless](#Wireless)
        *   [3.2.1 Intel chipset](#Intel_chipset)
        *   [3.2.2 Realtek chipset](#Realtek_chipset)
    *   [3.3 Modem](#Modem)
    *   [3.4 Bluetooth](#Bluetooth)
*   [4 Graphics/Xorg Configuration](#Graphics.2FXorg_Configuration)
    *   [4.1 Integrated Graphics](#Integrated_Graphics)
    *   [4.2 Discrete Graphics](#Discrete_Graphics)
    *   [4.3 Switchable Graphics](#Switchable_Graphics)
    *   [4.4 Synaptic, UltraNav](#Synaptic.2C_UltraNav)
*   [5 Audio](#Audio)
*   [6 Multimedia Keys](#Multimedia_Keys)
    *   [6.1 Mute](#Mute)
*   [7 ACPI](#ACPI)
*   [8 SUSPEND-RESUME](#SUSPEND-RESUME)
*   [9 Dock](#Dock)

## System Specification

Note, [ThinkPad T400](https://en.wikipedia.org/wiki/ThinkPad_T_Series "wikipedia:ThinkPad T Series") is available in a few hardware variants. Check the [ThinkWiki](http://www.thinkwiki.org) where details of hardware specification are discussed in the [T400](http://www.thinkwiki.org/wiki/Category:T400) category.

Below is an overview of the T400 specifications as originally used to start this article:

*   CPU : Intel® Core™2 Duo Processor T9400 (6M Cache, 2.53 GHz, 1066 MHz FSB)
*   Memory : 3GB PC3-8500 DDR3
*   WiFi : Intel WiFi Link 5300
*   Hard-Drive : 160GB, 7200rpm
*   Optical Drive : DVD Recordable
*   Integrated Graphics : Intel 4500MHD
*   Discrete Graphics : AMD M82XT Hybrid 256 MB (ATI Mobility Radeon HD 3470)
*   Screen : 14.1" WXGA+ TFT with LED Backlight
*   Gigabit Ethernet, Modem
*   Express Card & PC Card Slots
*   Integrated Bluetooth PAN
*   No camera
*   No fingerprint reader
*   No Intel Turbo Memory

## Installation

Even with the latest BIOS update,T400 BIOS does not support EFI, but can handle GPT disk.

## Network

### Ethernet

The [kernel module](/index.php/Kernel_module "Kernel module") to get the network card to work is `e1000e`.

### Wireless

Lenovo offers different options in wireless hardware:

#### Intel chipset

*   Wifi link 5100 and 5300

See [Wireless network configuration#Intel](/index.php/Wireless_network_configuration#Intel "Wireless network configuration").

#### Realtek chipset

*   Rtl8192SE

```
 11b/g/n Wireless Lan Mini-PCI Express Adapter II
 03:00.0 Network controller: Realtek Semiconductor Co., Ltd. Device 8172 (rev 10)

```

See [http://www.thinkwiki.org/wiki/ThinkPad_11b/g/n_Wireless_LAN_Mini-PCI_Express_Adapter_II](http://www.thinkwiki.org/wiki/ThinkPad_11b/g/n_Wireless_LAN_Mini-PCI_Express_Adapter_II) for more details.

### Modem

There is a module "hsfmodem" provided by [http://www.linuxant.com/](http://www.linuxant.com/).

### Bluetooth

If you have [thinkpad-acpi](http://www.thinkwiki.org/wiki/Thinkpad-acpi) kernel module loaded, you can enable and disable Bluetooth from command line. To enable:

 `# echo 1 > /sys/devices/platform/thinkpad_acpi/bluetooth_enable` 

To disable:

 `# echo 0 > /sys/devices/platform/thinkpad_acpi/bluetooth_enable` 

To disable or enable Bluetooth at startup, add one of the above commands to `/etc/rc.local`.

The bluetooth module requires `uhci_hcd`. Make sure `/etc/modprobe.d/modprobe.conf` does not blacklist it.

For everything else related to Bluetooth, follow the procedure described in [Bluetooth](/index.php/Bluetooth "Bluetooth") section of the Arch Wiki.

## Graphics/Xorg Configuration

Note that it's possible to switch the graphics adapter by only restarting X, but It's quite useless since you can't power up/down a graphic-card without rebooting. So it's either both graphic-card on at all times, or do the switching in the BIOS.

So please press the ThinkVantag-button» during boot up and enable either the Integrated or the Discrete graphics cards in your BIOS's "Config->Display" menu.

### Integrated Graphics

After installing [xorg](/index.php/Xorg#Installation "Xorg"), I installed the [xf86-video-intel drivers](/index.php/Intel "Intel").

### Discrete Graphics

See [ATI](/index.php/ATI "ATI") for the open-source driver or [AMD Catalyst](/index.php/AMD_Catalyst "AMD Catalyst") for the proprietary driver.

### Switchable Graphics

[ATI#Hybrid graphics/AMD Dynamic Switchable Graphics](/index.php/ATI#Hybrid_graphics.2FAMD_Dynamic_Switchable_Graphics "ATI")

### Synaptic, UltraNav

You may need to install the `xf86-input-synaptics` package.

If you want to be able to use horizontal and vertical scroll with your touchpad add this lines to your xorg.conf

```
Section "Module"
 ......
 Load    "synaptics"
EndSection

Section "InputDevice"
 Identifier  "Touchpad"
 Driver    "synaptics"
 Option    "AlwaysCore"
 Option    "Device" "/dev/input/mouse1"
 Option    "Protocol" "auto-dev"
 Option    "SendCoreEvents"  "true"
 Option    "LeftEdge"    "1632"
 Option    "RightEdge"     "5312"
 Option    "TopEdge"     "1575"
 Option    "BottomEdge"    "4281"
 Option    "FingerLow"     "25"
 Option    "FingerHigh"    "30"
 Option    "MaxTapTime"    "180"
 Option    "MaxTapMove"    "220"
 Option    "VertScrollDelta"   "100"
 Option    "MinSpeed"    "0.06"
 Option    "MaxSpeed"    "0.12"
 Option    "AccelFactor"     "0.0010"
 Option    "VertEdgeScroll"  "on"
 Option    "HorizEdgeScroll"   "on"
 # Option HorizScrollDelta""0"                               
 Option    "SHMConfig"   "on"
EndSection 

```

for trackpoint with third button paste & scroll add these few lines to xorg.conf too

```
Section "InputDevice"
 Identifier  "Trackpoint"
 Driver      "mouse"
 Option "CorePointer"
 Option "Device" "/dev/input/mice"
 Option "Protocol" "Auto"
 Option "Emulate3Buttons"
 Option "Emulate3Timeout" "50"
 Option "EmulateWheel" "on"
 Option "EmulateWheelTimeout" "200" # adjust third button paste timeout. 
 Option "EmulateWheelButton" "2"
 Option "YAxisMapping" "4 5"
 Option "XAxisMapping" "6 7"
 Option "YAxisMapping" "4 5"
EndSection

```

finally update your layout

```
Section "ServerLayout"
 InputDevice    "Trackpoint" "CorePointer"
 InputDevice    "Touchpad"
 InputDevice    "Keyboard0" "CoreKeyboard"
EndSection

```

## Audio

Once you have [ALSA](/index.php/ALSA "ALSA") installed, fire up alsamixer and make sure that sound is not muted. You might also want to press the Volume Up or Volume Down button. It seems than the Mute button mutes everything, even system beeps. Pressing the Volume Up or Volume Down button can unmute, but not pressing the Mute button again.

Here's the modules I have loaded that are relevant to sound :

```
  $ lsmod | grep snd
  snd_seq_oss            35584  0
  snd_seq_midi_event      9344  1 snd_seq_oss
  snd_seq                58336  4 snd_seq_oss,snd_seq_midi_event
  snd_seq_device          9364  2 snd_seq_oss,snd_seq
  snd_hda_intel         474672  2
  snd_hwdep              10632  1 snd_hda_intel
  snd_pcm_oss            45568  0
  snd_pcm                82440  2 snd_hda_intel,snd_pcm_oss
  snd_timer              24720  2 snd_seq,snd_pcm
  snd_page_alloc         10640  2 snd_hda_intel,snd_pcm
  snd_mixer_oss          18944  1 snd_pcm_oss
  snd                    64840  16    snd_seq_oss,snd_seq,snd_seq_device,snd_hda_intel,snd_hwdep,snd_pcm_oss,snd_pcm,snd_timer,snd_mixer_oss
  soundcore               9632  1 snd

```

Additionally, there is a patch for the audio driver for conexant's chipsets provided by [http://www.linuxant.com](http://www.linuxant.com) which can be downloaded at [http://www.linuxant.com/alsa-driver/](http://www.linuxant.com/alsa-driver/).

## Multimedia Keys

The screen brightness controls and the flashlight work without any tweaking. The other keys can be mapped using [xev](/index.php/Extra_keyboard_keys#In_Xorg "Extra keyboard keys") and xbindkeys. By following [this guide](http://wiki.linuxquestions.org/wiki/Configuring_keyboards#Enabling_Keyboard_Multimedia_Keys) you should be able to get everything working, but here's summary :

*   First, open a terminal and type `xev`. This starts the "Event tester".
*   Place your cursor on the "Event tester" window.
*   When you press a key on your keyboard or move your mouse, it should get displayed in a terminal. For instance, this is what shows up if you press Fn+F2

```
   KeyRelease event, serial 33, synthetic NO, window 0x3000001,
   root 0x86, subw 0x0, time 5537544, (76,110), root:(81,938),
   state 0x0, **keycode 146** (keysym 0x0, **NoSymbol**), same_screen YES,
   XLookupString gives 0 bytes:
   XFilterEvent returns: False

```

It basically says that **keycode 146** is not bound (**NoSymbol**). Here are all the keycodes of all multimedia buttons:

```
  Volume Down : keycode 174
  Volume Up : keycode 176
  Fn+F2 : keycode 146
  Fn+F3 : keycode 241
  Fn+F4 : keycode 223
  Fn+F5 : Not responding to events ??
  Fn+F7 : keycode 214
  Fn+F8 : keycode 249
  Fn+F9 : keycode 207
  Fn+F12 : keycode 165
  Fn+Up : keycode 164
  Fn+Down : keycode 162
  Fn+Left : keycode 144
  Fn+Right : keycode 153
  Fn+Home : keycode 212
  Fn+End : keycode 101

```

*   Type `xmodmap -pke > ~/.Xmodmap` in a terminal. This creates a file, `.Xmodmap`, containing your current keyboard mapping.
*   Now open the file with a text editor and find the keycodes you're interested in. You can map any keycode with a symbol from [this list](http://wiki.linuxquestions.org/wiki/XF86_keyboard_symbols).
*   To get your new `.Xmodmap` loaded when you start X, just add `xmodmap ~/.Xmodmap` to your .xinitrc.
*   To get your new `.Xmodmap` loaded immediately, type `xmodmap ~/.Xmodmap` in a terminal.

To assign functions to your newly bound keys, see [Keyboard configuration in Xorg#Keybinding](/index.php/Keyboard_configuration_in_Xorg#Keybinding "Keyboard configuration in Xorg").

To use `xbindkeys`,

*   Start by installing it

```
  pacman -S xbindkeys

```

*   Then add `xbindkeys &` to your .xinitrc.
*   And finally, in your home directory, create a file called `.xbindkeysrc.scm` with content that would look something like

```
  (xbindkey '("XF86Standby") "sudo killall dhcpcd && sudo pm-suspend")
  (xbindkey '("XF86AudioRaiseVolume") "amixer set Master 2dB+ unmute")
  (xbindkey '("XF86AudioLowerVolume") "amixer set Master 2dB- unmute")

```

Note, in more recent Arch (kernel 3.4.2, xorg-server 1.12.2, laptop-mode-tools 1.61), on the T400, related keys combinations binding seems to be:

*   Fn+2 → XF86ScreenSaver
*   Fn+4 → XF86Sleep & XF86Wakeup
*   Fn+12 → XF86Suspend

Now, the actual action will performed on XF86Sleep or XF86Suspend is configurable in session policy, so it may vary (e.g. depending on desktop environment). If nomenclature of XF86Standby, XF86Hibernate or XF86Sleep is confusing, check the thread [suspend / hibernate nomenclature](http://thread.gmane.org/gmane.linux.acpi.devel/37554) for in-depth explanation.

### Mute

To get the mute button to work, it is necessary to pass the string `acpi_osi="Linux"` to the kernel as a boot parameter. In GRUB2, add it to the "linux" line. See [here](http://www.thinkwiki.org/wiki/Mute_button) for more details.

With the 3.1 bios, it seems that the mute button works normally (set it up the same as the volume buttons with, for instance, "amixer set Master toggle").

## ACPI

To enable the fan speed control, it's necessary to load the thinkpad_acpi with option fan_control=1\. After the thinkpad_acpi module is loaded with this option, you can monitor and adjust the fan speed via /proc/acpi/ibm/fan.

## SUSPEND-RESUME

People have been having issues with suspend resume with the current intel xf86-video-intel 2.4.3.1 drivers in combination with the 4500mhd chipset. This is apparently an issue with concurrency as adding the following script (with mod 755) in /etc/pm/sleep.d fixes things. to some extent...

```
#!/bin/sh
# Workaround for concurrency bug in xserver-xorg-video-intel 2:2.4.1-1ubuntu10.
# Save this as /etc/pm/sleep.d/00CPU 

. "/usr/lib/pm-utils/functions"

case "$1" in
	hibernate|suspend)
		for i in /sys/devices/system/cpu/cpu*/online ; do
			echo 0 >$i
		done
		;;
	thaw|resume) 
		sleep 10	# run with one core for 10 secs
		for i in /sys/devices/system/cpu/cpu*/online ; do
			echo 1 >$i
		done
		;;
	*)
		;;
esac

```

## Dock

See [dockd](/index.php/Dockd "Dockd").

From [http://ubuntu-virginia.ubuntuforums.org/showpost.php?p=6105510&postcount=12](http://ubuntu-virginia.ubuntuforums.org/showpost.php?p=6105510&postcount=12) petri4 on the ubuntu forums.