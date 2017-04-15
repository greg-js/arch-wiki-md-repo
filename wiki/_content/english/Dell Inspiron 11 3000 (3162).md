| **Device** | **Status** | **Modules** |
| Video | Working | i915, xf86-video-intel |
| Wireless | Working | iwlwifi |
| Audio | Working | snd_hda_intel |
| Touchpad | Working | xf86-input-libinput |
| Camera | Working | linux-uvc |
| Card Reader | Working | rtsx_usb |
| Bluetooth | Working | btusb |

This is an install and configuration guide for the Dell Inspiron 11 3000 (3162) laptop.

For a general overview of laptop-related articles and recommendations, see [Laptop](/index.php/Laptop "Laptop").

## Contents

*   [1 Before Installation](#Before_Installation)
    *   [1.1 Entering Setup](#Entering_Setup)
    *   [1.2 Disabling Secure Boot](#Disabling_Secure_Boot)
    *   [1.3 Disabling Load Legacy Option Rom](#Disabling_Load_Legacy_Option_Rom)
*   [2 Base Install](#Base_Install)
*   [3 Configuration](#Configuration)
    *   [3.1 Video](#Video)
        *   [3.1.1 Drivers](#Drivers)
        *   [3.1.2 Brightness](#Brightness)
    *   [3.2 Wireless](#Wireless)
    *   [3.3 Audio](#Audio)
    *   [3.4 Keyboard](#Keyboard)
    *   [3.5 Touchpad](#Touchpad)
    *   [3.6 Camera](#Camera)
    *   [3.7 Card Reader](#Card_Reader)
    *   [3.8 Bluetooth](#Bluetooth)
    *   [3.9 Suspend & Hibernate](#Suspend_.26_Hibernate)
*   [4 Hardware Details](#Hardware_Details)
    *   [4.1 Specs](#Specs)
    *   [4.2 lspci](#lspci)
    *   [4.3 lsusb](#lsusb)
    *   [4.4 lscpu](#lscpu)

## Before Installation

This laptop uses UEFI. By default secure boot is enabled. Though is should be possible to set up a secure boot loader ([Secure Boot](/index.php/Secure_Boot "Secure Boot")), I chose to simple turn off secure boot. Also, though the laptop does support booting from legacy devices I discovered that this causes serious video issues (you can not boot into the CLI with KMS enabled but disabling KMS prevents X from starting). Simply turning off the legacy boot option fixes this issue.

### Entering Setup

This laptop hides the "Push XXX to enter setup" message during boot.

1.  Power on the laptop
2.  When the Dell logo appears, press ESC
    1.  If timed right, two lines of text will appear in the lower right corner of the screen
3.  Press F2 to enter setup

### Disabling Secure Boot

As mentioned above, disabling Secure Boot permanently may not be necessary but I was unable to find a way to boot the Arch install image without doing so.

Once in setup:

1.  Go to the "Boot" tab
2.  Disable "Secure Boot"

### Disabling Load Legacy Option Rom

With this option enabled the laptop screen would shut off while booting the install media and when booting the installed system unless KMS was disabled. Disabling KMS, however, prevents X from starting as, from what I have read, the xf86-video-intel driver requires KMS.

Once in setup:

1.  Go to the "Boot" tab
2.  Disable "Load Legacy Option Rom"

## Base Install

Once setup has been configured, installation using the [Installation guide](/index.php/Installation_guide "Installation guide") and [General recommendations](/index.php/General_recommendations "General recommendations") proceeded without issue. As this laptop uses an Intel processor, pay attention to the sections covering microcode updates.

## Configuration

### Video

#### Drivers

[xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) works without issue.

#### Brightness

The brightness hotkeys (Fn-F11 & Fn-F12) did not work for me out of the box but they will if you are using a full desktop environment like Gnome or KDE. Still, I had no trouble making the hotkeys work using information found on the [Backlight](/index.php/Backlight "Backlight") and [Extra keyboard keys](/index.php/Extra_keyboard_keys "Extra keyboard keys") pages and my window manager's documentation. My solution involved configuring my window manager to map the XF86MonBrightnessUp and XF86MonBrightnessDown keys to run the appropriate xbacklight command.

### Wireless

Wireless worked with no additional effort on my part. This is fairly important as this model does not include a wired port.

### Audio

Audio using [ALSA](/index.php/ALSA "ALSA") worked immediately after install. I have not needed [PulseAudio](/index.php/PulseAudio "PulseAudio") yet so it remains untested.

### Keyboard

Most of the extra keys did not work for me after install. Some or all will work if you use a full desktop environment like Gnome or KDE though. I was able to configure my window manager to run appropriate commands when the extra keys are pressed. The Enable/Disable wireless key did work without any extra work on my part. However, the page up and page down keys (activated by pressing Fn + PageUp or PageDn) do not work as expected. After pressing and releasing them, the scrolling action will be glitched and will not stop. To fix this create the following [hwdb](/index.php/Map_scancodes_to_keycodes#Using_udev "Map scancodes to keycodes"):

 `/etc/udev/hwdb.d/90-custom-keyboard.hwdb` 
```
evdev:atkbd:dmi:bvn*:bvr*:bd*:svnDell*:pnInspiron*3162:pvr*
 KEYBOARD_KEY_c7=!home
 KEYBOARD_KEY_cf=!end
 KEYBOARD_KEY_c9=!pageup
 KEYBOARD_KEY_d1=!pagedown

```

Pay attention to formatting. This is the first reason why it may not work.

### Touchpad

When I first installed xorg, I installed [xf86-input-evdev](https://www.archlinux.org/packages/?name=xf86-input-evdev) as the only input driver. This caused the touchpad to react like a disembodied touchscreen. I then replaced [xf86-input-evdev](https://www.archlinux.org/packages/?name=xf86-input-evdev) with [xf86-input-libinput](https://www.archlinux.org/packages/?name=xf86-input-libinput) this caused the touchpad to work fine but the keyboard stopped working once I started X. With both [xf86-input-evdev](https://www.archlinux.org/packages/?name=xf86-input-evdev) and [xf86-input-libinput](https://www.archlinux.org/packages/?name=xf86-input-libinput) installed, the keyboard and touchpad both work fine.

### Camera

The camera worked without effort on my part. I tested by installing running guvcview.

### Card Reader

It works as expected.

### Bluetooth

The bluetooth hardware is recognized and the appropriate modules are loaded. I am also able to turn on power and detect other bluetooth devices. Pairing works, and so does file transfer from and to the device.

### Suspend & Hibernate

Suspend and hibernation do work fine with no extra work on my part.

## Hardware Details

### Specs

*   CPU: Intel Celeron N3060
*   GPU: Intel HD 400 (Braswell)
*   RAM: 4 GB DDR3 1600 MHz
*   HDD: 32 GB eMMC
*   Wireless: Intel Centrino Wireless-AC 3160
*   Bluetooth: 4.0
*   Display: 11.6", 1366 x 768 px
*   Camera: 720P (30FPS)
*   Ports: HDMI (1.4a), 1xUSB (3.0), 1xUSB (2.0), 3.5mm Headphone/Microphone, MicroSD Card Reader

### lspci

```
$ lspci
00:00.0 Host bridge: Intel Corporation Atom/Celeron/Pentium Processor x5-E8000/J3xxx/N3xxx Series SoC Transaction Register (rev 35)
00:02.0 VGA compatible controller: Intel Corporation Atom/Celeron/Pentium Processor x5-E8000/J3xxx/N3xxx Integrated Graphics Controller (rev 35)
00:0b.0 Signal processing controller: Intel Corporation Atom/Celeron/Pentium Processor x5-E8000/J3xxx/N3xxx Series Power Management Controller (rev 35)
00:14.0 USB controller: Intel Corporation Atom/Celeron/Pentium Processor x5-E8000/J3xxx/N3xxx Series USB xHCI Controller (rev 35)
00:1a.0 Encryption controller: Intel Corporation Atom/Celeron/Pentium Processor x5-E8000/J3xxx/N3xxx Series Trusted Execution Engine (rev 35)
00:1b.0 Audio device: Intel Corporation Atom/Celeron/Pentium Processor x5-E8000/J3xxx/N3xxx Series High Definition Audio Controller (rev 35)
00:1c.0 PCI bridge: Intel Corporation Atom/Celeron/Pentium Processor x5-E8000/J3xxx/N3xxx Series PCI Express Port #1 (rev 35)
00:1f.0 ISA bridge: Intel Corporation Atom/Celeron/Pentium Processor x5-E8000/J3xxx/N3xxx Series PCU (rev 35)
00:1f.3 SMBus: Intel Corporation Atom/Celeron/Pentium Processor x5-E8000/J3xxx/N3xxx SMBus Controller (rev 35)
01:00.0 Network controller: Intel Corporation Wireless 3160 (rev 83)

```

### lsusb

```
$ lsusb
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 003: ID 0bda:5769 Realtek Semiconductor Corp.
Bus 001 Device 002: ID 8087:07dc Intel Corp.
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

### lscpu

```
$ lscpu
Architecture:          x86_64
CPU op-mode(s):        32-bit, 64-bit
Byte Order:            Little Endian
CPU(s):                2
On-line CPU(s) list:   0,1
Thread(s) per core:    1
Core(s) per socket:    2
Socket(s):             1
NUMA node(s):          1
Vendor ID:             GenuineIntel
CPU family:            6
Model:                 76
Model name:            Intel(R) Celeron(R) CPU  N3060  @ 1.60GHz
Stepping:              4
CPU MHz:               875.585
CPU max MHz:           2480.0000
CPU min MHz:           480.0000
BogoMIPS:              3201.33
Virtualization:        VT-x
L1d cache:             24K
L1i cache:             32K
L2 cache:              1024K
NUMA node0 CPU(s):     0,1
Flags:                 fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush dts acpi mmx fxsr sse sse2 ss ht tm pbe syscall nx rdtscp lm constant_tsc arch_perfmon pebs bts rep_good nopl xtopology nonstop_tsc aperfmperf eagerfpu pni pclmulqdq dtes64 monitor ds_cpl vmx est tm2 ssse3 cx16 xtpr pdcm sse4_1 sse4_2 movbe popcnt tsc_deadline_timer aes rdrand lahf_lm 3dnowprefetch epb tpr_shadow vnmi flexpriority ept vpid tsc_adjust smep erms dtherm ida arat

```