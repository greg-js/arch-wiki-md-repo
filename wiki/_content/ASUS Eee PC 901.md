# ASUS Eee PC 901

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

**This article or section is out of date.**

**Reason:** please use the first argument of the template to provide a brief explanation. (Discuss in [Talk:ASUS Eee PC 901#](https://wiki.archlinux.org/index.php/Talk:ASUS_Eee_PC_901))

This page contains instructions, tips, pointers, and links for installing and configuring Arch Linux on the ASUS EEE 901 PC.

Most of the article can also be applied to eeepc-models which are similar to the 901 such the 901H, 1000 and 1000H. If you discover a configuration or software option applicable to a certain model that differs from what is described in this article, please add it, with a note about which model the suggestion pertains to.

## Contents

*   [1 Install tips for the Asus Eee PC](#Install_tips_for_the_Asus_Eee_PC)
*   [2 Kernel installation and configuration](#Kernel_installation_and_configuration)
*   [3 OS configuration](#OS_configuration)
    *   [3.1 Networking: ethernet](#Networking:_ethernet)
    *   [3.2 Networking: wireless](#Networking:_wireless)
    *   [3.3 ACPI (hotkeys)](#ACPI_.28hotkeys.29)
        *   [3.3.1 Option 1: acpi-eeepc-generic](#Option_1:_acpi-eeepc-generic)
        *   [3.3.2 Option 2: configure the stock kernel ACPI features](#Option_2:_configure_the_stock_kernel_ACPI_features)
        *   [3.3.3 ASUS OSD](#ASUS_OSD)
    *   [3.4 Bluetooth](#Bluetooth)
    *   [3.5 Webcam](#Webcam)
    *   [3.6 Audio](#Audio)
    *   [3.7 X](#X)
        *   [3.7.1 Video](#Video)
            *   [3.7.1.1 Connecting an external monitor](#Connecting_an_external_monitor)
            *   [3.7.1.2 Letterboxing with XRandR](#Letterboxing_with_XRandR)
        *   [3.7.2 Mouse and Synaptics driver](#Mouse_and_Synaptics_driver)
        *   [3.7.3 Miscellaneous](#Miscellaneous)
*   [4 Performance tips](#Performance_tips)
    *   [4.1 Speedstep](#Speedstep)
    *   [4.2 Boot Booster](#Boot_Booster)
    *   [4.3 Hardware overview for 901](#Hardware_overview_for_901)

## Install tips for the Asus Eee PC

This wiki page supplements these pages: **[Beginners' guide](/index.php/Beginners%27_guide "Beginners' guide")**, the **[Official Install Guide](/index.php/Installation_guide "Installation guide")**, and **[Installing Arch Linux on the Asus EEE PC](/index.php/Installing_Arch_Linux_on_the_Asus_EEE_PC "Installing Arch Linux on the Asus EEE PC")**. Please refer to those guides _first_ before following the eeepc-specific pointers on this page.

Most of this information is from the Arch Forum EEE 901 [thread](https://bbs.archlinux.org/viewtopic.php?id=53464). Consult this thread, and other resources on the Arch forum, for more details and discussion.

## Kernel installation and configuration

Follow the Arch Linux installation Guide to install the latest stock distribution from USB media or CDROM. Install the **BASE** and **DEVEL** package categories. Reboot your PC.

As of the advent of kernel 2.6.30, all drivers needed for the EEE 901 are included in the Arch Linux stock kernel. In case you would like to compile your own kernel, make sure that you build the following modules:

Network card:

```
Device Drivers - Ethernet (1000Mbit) - Atheros L1E Gigabit Ethernet support

```

WiFi card:

```
Device Drivers - Staging Drivers - Ralink 2860

```

Eee Hotkey stuff:

```
Device Drivers - X86 Platform Specific Device Drivers - EeePC Hotkey Driver

```

Video Camera:

```
Device Drivers - Multimedia Devices - Video Capture adapters - V4L USB devices - USB Video Class (UVC)

```

Sound Card:

```
Device Drivers - Sound card support - ALSA - PCI Sound devices - Intel HDA - Build Realtek HDA codec

```

Touchpad:

```
Device Drivers - Input Device support - Mice - PS/2 mouse - Synaptics & Elantech PS/2 protocol ext.

```

For flawless operation with the eee-control FSB frequency changing mechanism, you have to compile

```
Device Drivers - I2C support - I2C Hardware Bus support - Intel 82801 (ICH)

```

as a **module**.

For more general information about building custom Arch Linux kernels, see [Kernel Compilation](/index.php/Kernel_Compilation "Kernel Compilation").

## OS configuration

To support the devices listed below, make sure the module `eeepc_laptop` is loaded on boot using `modules.d` directory:

 `/etc/modules-load.d/eeepc_laptop` 

```
eeepc_laptop

```

### Networking: ethernet

Ethernet (wired) network access should work right out of the box with **atl1e** module.

### Networking: wireless

From Kernel 3.0, The staging driver rt2860sta is replaced by mainline driver rt2800pci. See [Wireless network configuration#rt2860 and rt2870](/index.php/Wireless_network_configuration#rt2860_and_rt2870 "Wireless network configuration").

After a bios-upgrade the wireless-card of the Eee PC will be disabled by default, so if you have any troubles with wlan check that it is enabled in the bios.

```
# enable
echo 1 > /sys/devices/platform/eeepc/rfkill/rfkill0/state
# disable
echo 0 > /sys/devices/platform/eeepc/rfkill/rfkill0/state

```

Here's a working example wpa_supplicant config file:

```
ctrl_interface=/var/run/wpa_supplicant
# change ap_scan to 2 if running into problems
ap_scan=1
fast_reauth=1
eapol_version=1

network={
  key_mgmt=NONE
}

network={
  ssid="WPA"
  scan_ssid=1
  proto=WPA
  key_mgmt=WPA-PSK
  pairwise=TKIP
  group=TKIP
  #psk="passphrase"
  psk=hexkey
}

network={
  ssid="WEP"
  scan_ssid=1
  key_mgmt=NONE
  #wep_key0="passphrase"
  wep_key0=hexkey
  wep_tx_keyidx=0
}

```

Your mileage may vary, but experience seems to show that the `ap_scan=1` parameter is critical. Try tweaking the other "header" settings, too, if you continue to experience problems.

### ACPI (hotkeys)

#### Option 1: acpi-eeepc-generic

Install [acpi-eeepc-generic](https://aur.archlinux.org/packages/acpi-eeepc-generic/)<sup><small>AUR</small></sup>. For this package to work, make sure the **eeepc_laptop** and **rfkill** modules are loaded at boot.

Consult the notes included with the install for instructions on configuring `/etc/conf.d/acpi-eeepc-generic.conf`.

This will enable all the `Fn + xx` keys and the four silver hotkey buttons buttons as configured in the default Xandros distribution, with some minor variations. Edit the `/etc/conf.d/acpi-eeepc-generic.conf` file to change or modify the behavior of the function keys.

#### Option 2: configure the stock kernel ACPI features

Enable the ASUS_LAPTOP (_Device Drivers > Misc Devices_) switch in your kernel config and turn off ACPI_ASUS switch (_Power managment options > ACPI_).

To enable the FN keys, the WLAN and Camera on/off toggles, etc., activate the EEEPC_LAPTOP switch also (_Device Drivers > Misc Devices_).

You can use Robertek's PKGBUILD and files for **acpi-www901** at [http://robertek.brevnov.net/files/linux/arch/acpi-eee901/](http://robertek.brevnov.net/files/linux/arch/acpi-eee901/) as a base to incorporate the stock kernel modules and ASUS OSD into the ACPI system.

Note: The kernel interfaces `/proc/acpi/asus` or `/proc/acpi/eee` are not available with the **eeepc_laptop** module. The corresponding **eeepc_laptop** interfaces are files in: `/sys/devices/platform/eeepc/`. You may need to edit some of the scripts under `/etc/acpi/` to point to the correct paths. Also easier links to the interfaces can be found inside of /sys/class/ . For instance the first battery is in /sys/class/power_supply/BAT0/ .

#### ASUS OSD

Asus OSD is included as part of the **acpi-eee901** package. Simply add the command `asusosd &` to your desktop manager startup script, or create the file `/etc/xdg/autostart/asusosd.desktop` with these contents:

```
[Desktop Entry]
Encoding=UTF-8
Name=ASUS OSD
Comment=ASUS OSD
Exec=/usr/bin/asusosd
Terminal=false
Type=Application
StartupNotify=false
Hidden=false

```

### Bluetooth

Currently, Bluetooth is not enabled with the `Fn+F2` hotkey. To communicate with Bluetooth devices, make sure Bluetooth has been enabled in the BIOS.

To enable/disable bluetooth from the command line :

```
 # enable
 echo 1 > /sys/devices/platform/eeepc/bt
 # disable
 echo 0 > /sys/devices/platform/eeepc/bt

```

Install the [bluez](https://www.archlinux.org/packages/?name=bluez) package. Make sure the **bluetooth** module is loaded.

See the Arch Linux [Bluetooth](/index.php/Bluetooth "Bluetooth") and [Bluetooth mouse](/index.php/Bluetooth_mouse "Bluetooth mouse") wiki pages for more information about configuring and using Bluetooth devices.

### Webcam

To enable/disable the camera:

```
# enable
echo 1 > /sys/devices/platform/eeepc/camera
# disable
echo 0 > /sys/devices/platform/eeepc/camera

```

To record video and take photos, you may use [cheese](https://www.archlinux.org/packages/?name=cheese) or the [wxcam](https://www.archlinux.org/packages/?name=wxcam) package.

To simply test the camera, you may use `mplayer`:

```
mplayer -fps 15 tv://

```

The webcam is reported to work with Skype.

### Audio

Audio output is enabled with the default ALSA drivers distributed with the kernels. You may need to install the **alsa-lib** and **alsa-utils** packages to get full functionality. Make sure the **snd-hda-intel** module is loaded.

Both the microphone and PC speakers should work out-of-the-box with current versions of the kernel and ALSA drivers. A common gotcha: if you're not getting any sound, did you run `alsamixer` and unmute your channels?

See the Arch Linux [ALSA](/index.php/ALSA "ALSA") wiki page for more information about configuring and using ALSA.

### X

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

**This article or section is out of date.**

**Reason:** This section is out-of-date, and needs to be cleaned up. (Discuss in [Talk:ASUS Eee PC 901#](https://wiki.archlinux.org/index.php/Talk:ASUS_Eee_PC_901))

#### Video

You will need the [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) video driver.

To set-up the touchpad, (including two-fingers scrolling & tapping), just install [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics) (no xorg.conf required).

Some users have reported problems with vsync and the **xf86-video-intel** driver. These problems may be partially solved in the application (see this forum [post](https://bbs.archlinux.org/viewtopic.php?pid=416645#p416645).)

##### Connecting an external monitor

The xrandr utility (part of Xorg) can be used to switch into screen modes appropriate either for the EeePC's LCD or an externally connected monitor. Running `xrandr -q` will show you the available output devices and the supported modes. Then run the tool as follows:

```
xrandr --output LVDS --off  --output VGA --auto   # disable LCD, enable monitor
xrandr --output LVDS --auto --output VGA --auto   # enable both
etc.

```

Your monitor will probably support a bigger resolution than the LCD. To make use of that additional screen space, tell the X server to create an appropriately large framebuffer by adding the "Virtual" directive to the Screen/Display section in `/etc/X11/xorg.conf`:

```
Section "Screen"
  Identifier "Screen0"
  Device     "Card0"
  Monitor    "Monitor0"
  DefaultDepth     24
  SubSection "Display"
      Viewport   0 0
      Depth     24
      Virtual 1600 1200   # max resolution is 1600x1200
  EndSubSection
EndSection

```

On the LCD, the additional space will be unused, but when switching to the external monitor, the screen will be. Note that some window managers (such as ratpoison) might need to be restarted to realize that the visible screen size has changed.

##### Letterboxing with XRandR

If you have set up your X server and kernel to use KMS you might have some trouble getting a 800x600 resolution letterboxed (centered) rather than stretched, which might be unpleasant in some programs that do not support 1024x600 such as older games. This is because with KMS the xrandr syntax is a bit different [[1]](https://bugs.freedesktop.org/show_bug.cgi?id=24331). To get a centered 800x600 visual field on your 1024x600 panel run:

```
$ xrandr --output LVDS1 --set "scaling mode" "Center"
$ xrandr -s 800x600

```

Replace "800x600" with "1024x600" to go back to the native resolution.

#### Mouse and Synaptics driver

To enable the Synaptics drivers, first install the [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics) package.

You also need the [xf86-input-evdev](https://www.archlinux.org/packages/?name=xf86-input-evdev) driver for Xorg.

Then make these changes to `/etc/X11/xorg.conf`:

```
Section "ServerLayout"
  Identifier     "ArchLinux"
  Screen      0  "Screen0"
  InputDevice    "keyboard"
  InputDevice    "mouse"
  **InputDevice    "synaptics"**
EndSection

[...]

Section "Files"
  **#    RgbPath      "/usr/share/X11/rgb"**
  ModulePath   "/usr/lib/xorg/modules"
  FontPath     "/usr/share/fonts/misc"
  FontPath     "/usr/share/fonts/100dpi:unscaled"
  FontPath     "/usr/share/fonts/75dpi:unscaled"
  FontPath     "/usr/share/fonts/TTF"
  FontPath     "/usr/share/fonts/Type1"
EndSection

Section "Module"
  Load  "GLcore"
  Load  "glx"
  Load  "record"
  Load  "dri"
  Load  "extmod"
  Load  "xtrap"
  Load  "dbe"
  Load  "freetype"
  **Load  "synaptics"**
EndSection

[...]

Section "InputDevice"
  Identifier  "mouse"
  Driver      "mouse"
  Option        "Device" "/dev/input/mice"
  Option        "Protocol" "IMPS/2"
  Option        "Emulate3Buttons" "yes"
  Option        "ZAxisMapping" "4 5"
  Option        "CorePointer"
EndSection

**Section "InputDevice"**
  **Identifier  "synaptics"**
  **Driver      "synaptics"**
  **Option      "Device"           "/dev/psaux"**
  **Option      "Protocol"         "auto-dev"**
  **Option      "PalmDetect"       "0"**
  **Option      "SHMConfig"        "true"**
  **Option      "SendCoreEvents"   "yes"**
  **Option      "RBCornerButton"   "0"**
  **Option      "RTCornerButtom"   "0"**
  **Option      "TapButton1"       "1"**
  **Option      "TapButton2"       "2"**
  **Option      "TapButton3"       "3"**
  **Option      "AccelFactor"   "0.0320"**
  **Option      "MaxSpeed"      "0.72"**
  **Option      "MinSpeed"      "0.6"**
  **Option      "Emulate3Buttons"       "true"**
  **Option      "TouchPadOff"       "0"**
  **Option      "LBCornerButton"        "2"**
  **Option      "LeftEdge"      "60"**
  **Option      "RightEdge"     "1070"**
  **Option      "TopEdge"       "90"**
  **Option      "BottomEdge"    "680"**
  **Option      "VertTwoFingerScroll"   "1"**
  **Option      "HorizTwoFingerScroll"  "1"**
  **Option      "HorizScrollDelta"  "20"**
  **Option      "LockedDrags"   "1"**
  **Option      "CoastingSpeed" "0.13"**
  **Option      "CircularScrolling"     "1"**
  **Option      "CircScrollTrigger"     "8"     # 8=Top Left Corner**
**EndSection**

```

The latest version of the Elantech touchpad driver patch is available at [http://arjan.opmeer.net/elantech/](http://arjan.opmeer.net/elantech/) or here [mac how to](http://www.mac-how.net/) You'll need to apply this patch to your kernel source, then recompile the kernel. This patch has been tested on the 2.6.27.6 and 2.6.27.7 kernels.

#### Miscellaneous

If you do not have an `xorg.conf` file, and want to configure the keyboard layout on the fly:

```
# Set keyboard to cz with qwerty
setxkbmap cz qwerty

```

To configure the mouse speed:

```
# Set mouse movement and acceleration (you need to tweak this to your needs)
xset m 2 1

```

## Performance tips

The following tweaks can be used to improve performance and/or power consumption.

### Speedstep

Speedstep is included by default in the Linux 2.6.x kernel.

The **zen-eee901** kernels contain the Speedstep modules. Create a proper module file in `/etc/module.d` to load `acpi-cpufreq` at boot:

 `/etc/module.d/acpi-cpufreq.conf` 

```
acpi-cpufreq

```

See [here](http://rffr.de/acpi) for more information.

For more information on overclocking the Asus EEE PC line, see [http://wiki.eeeuser.com/howto:overclockfsb](http://wiki.eeeuser.com/howto:overclockfsb)

**Note:** Speedstep is applicable to the 901 as it's CPU is of the Intel Atom family. The eee 900 and 904 use an Intel Celeron M CPU and so should use the p4-clockmod module instead.

### Boot Booster

Enable Asus Boot Booster feature in BIOS to skip some tests during boot.

```
Boot > Boot Settings Configuration > Quick Boot > [Enabled]

```

### Hardware overview for 901

The following hardware is used in the Asus EEE 901:

```
* CPU: 1.6GHz N270 Intel Atom
* RAM: 1024 MB, DDR2 667
* ports: 3x USB, VGA
* LAN/ethernet: Atheros L1e 1000 Mbit
* WLAN: Ralink rt2860 802.11b/g/n
* Bluetooth, webcam 1.3 Mpix
* Card reader: SD, SDHC, MMC
* touchpad: "Multi-touch" elantech
* display: 1024x600 8.9"
* weight: 1 kg
* battery: Li-ion, 6600mAh
* HDD: 4 + 8GB, empty slot for 1,8" (remove of the 8GB module needed)
* Graphics:  Intel GM950 core, 945GME chipset

```

```
00:00.0 Host bridge: Intel Corporation Mobile 945GME Express Memory Controller Hub (rev 03)
00:02.0 VGA compatible controller: Intel Corporation Mobile 945GME Express Integrated Graphics Controller (rev 03)
00:02.1 Display controller: Intel Corporation Mobile 945GM/GMS/GME, 943/940GML Express Integrated Graphics Controller (rev 03)
00:1b.0 Audio device: Intel Corporation 82801G (ICH7 Family) High Definition Audio Controller (rev 02)
00:1c.0 PCI bridge: Intel Corporation 82801G (ICH7 Family) PCI Express Port 1 (rev 02)
00:1c.1 PCI bridge: Intel Corporation 82801G (ICH7 Family) PCI Express Port 2 (rev 02)
00:1c.2 PCI bridge: Intel Corporation 82801G (ICH7 Family) PCI Express Port 3 (rev 02)
00:1c.3 PCI bridge: Intel Corporation 82801G (ICH7 Family) PCI Express Port 4 (rev 02)
00:1d.0 USB Controller: Intel Corporation 82801G (ICH7 Family) USB UHCI Controller #1 (rev 02)
00:1d.1 USB Controller: Intel Corporation 82801G (ICH7 Family) USB UHCI Controller #2 (rev 02)
00:1d.2 USB Controller: Intel Corporation 82801G (ICH7 Family) USB UHCI Controller #3 (rev 02) 
00:1d.3 USB Controller: Intel Corporation 82801G (ICH7 Family) USB UHCI Controller #4 (rev 02)
00:1d.7 USB Controller: Intel Corporation 82801G (ICH7 Family) USB2 EHCI Controller (rev 02)
00:1e.0 PCI bridge: Intel Corporation 82801 Mobile PCI Bridge (rev e2)
00:1f.0 ISA bridge: Intel Corporation 82801GBM (ICH7-M) LPC Interface Bridge (rev 02)
00:1f.2 IDE interface: Intel Corporation 82801GBM/GHM (ICH7 Family) SATA IDE Controller (rev 02)
00:1f.3 SMBus: Intel Corporation 82801G (ICH7 Family) SMBus Controller (rev 02)
01:00.0 Network controller: RaLink Device 0781

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=ASUS_Eee_PC_901&oldid=408675](https://wiki.archlinux.org/index.php?title=ASUS_Eee_PC_901&oldid=408675)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [ASUS](/index.php/Category:ASUS "Category:ASUS")

Hidden category:

*   [Pages or sections flagged with Template:Out of date](/index.php/Category:Pages_or_sections_flagged_with_Template:Out_of_date "Category:Pages or sections flagged with Template:Out of date")