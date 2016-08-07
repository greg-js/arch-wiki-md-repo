The Lenovo P50 is a quad core Intel Skylake Laptop.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 External video](#External_video)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Sluggish graphics performance with HD Graphics 530 (Skylake GT2)](#Sluggish_graphics_performance_with_HD_Graphics_530_.28Skylake_GT2.29)
    *   [3.2 High CPU chromium bug](#High_CPU_chromium_bug)
    *   [3.3 High fan speed on low CPU load](#High_fan_speed_on_low_CPU_load)
    *   [3.4 Mouse cursor disappears after screen unlocks](#Mouse_cursor_disappears_after_screen_unlocks)
    *   [3.5 Touchpad active even if disabled in BIOS](#Touchpad_active_even_if_disabled_in_BIOS)
    *   [3.6 Prevent tap clicking while typing](#Prevent_tap_clicking_while_typing)
    *   [3.7 Video compression artifacts in VLC](#Video_compression_artifacts_in_VLC)
*   [4 lspci](#lspci)

## Installation

If you have the 4K display, console fonts will be extremely small. Run `setfont sun12x22` to make them a bit bigger.

After that, follow the [Beginner's guide](/index.php/Beginner%27s_guide "Beginner's guide") to install Arch.

## Configuration

### External video

External video using the Mini DisplayPort seems to work most reliably when the BIOS is configured to use only the discrete graphics card. To use Xorg with this configuration, install [nvidia](https://www.archlinux.org/packages/?name=nvidia) and create a `/etc/X11/xorg.conf.d/20-nvidia.conf` file with the following contents:

```
   Section "Device"
       Identifier "Device0"
       Driver "nvidia"
       VendorName "NVIDIA Corporation"
       Option "NoLogo" "true"
   EndSection

```

## Troubleshooting

### Sluggish graphics performance with HD Graphics 530 (Skylake GT2)

When running with the native 4K resolution, performance can appear sluggish. This might be improved in the UEFI BIOS by increasing the amout of RAM the Intel graphics adapter should take from the DRAM from 256MB to the maximum 512MB.

### High CPU chromium bug

Chromium takes too long to even display the "new tab" page with the small previews and uses 100% CPU on all cores for several seconds if 5-6 new tabs get open simultaneously when using the Intel Graphics. This might be due to some hardware acceleration bug maybe related to: [Corruption/Unresponsiveness in Chromium and Firefox with Intel Graphics](/index.php/Intel_graphics#Corruption.2FUnresponsiveness_in_Chromium_and_Firefox "Intel graphics") but has not been tested yet. But it is simply enough to deactivate hardware acceleration in the chromium settings GUI. Another workaround that seems to work with keeping hardware acceleration enabled is activating the flag

```
--ignore-gpu-blacklist

```

by creating the file ".config/chromium-flag" and adding the flag.

### High fan speed on low CPU load

Even with just low CPU load and only a browser open the fan keeps to switch on and speed up to full power. This behaviour can be at least reduced a bit by only using Intel Graphics and completely powering down the NVIDIA optimus card that uses the same cooling system [Power down discrete GPU](/index.php/Hybrid_graphics#Fully_Power_Down_Discrete_GPU "Hybrid graphics"). This seems due to a low temperature trigger value for the nvidia chip fan.

### Mouse cursor disappears after screen unlocks

This is a known bug with light-locker and the Intel graphics driver. To work around it, switch to a console (Ctrl-Alt-F1) and back to X (Alt-F7). For more information, see

*   [https://bugs.launchpad.net/ubuntu/+source/xserver-xorg-video-intel/+bug/492782](https://bugs.launchpad.net/ubuntu/+source/xserver-xorg-video-intel/+bug/492782)
*   [https://bugs.launchpad.net/ubuntu/+source/xserver-xorg-video-intel/+bug/1568604](https://bugs.launchpad.net/ubuntu/+source/xserver-xorg-video-intel/+bug/1568604)
*   [https://github.com/the-cavalry/light-locker/issues/80](https://github.com/the-cavalry/light-locker/issues/80)
*   [https://bugs.freedesktop.org/show_bug.cgi?id=94677](https://bugs.freedesktop.org/show_bug.cgi?id=94677)

### Touchpad active even if disabled in BIOS

The touchpad may be enabled in Linux even if it's disabled in the BIOS. To disable it, run

```
xinput set-prop "SynPS/2 Synaptics TouchPad" "Device Enabled" 0

```

in an appropriate startup file (e.g., `~/.xprofile`). To check the device name to use, run

```
xinput list

```

### Prevent tap clicking while typing

The touchpad is very sensitive so it often happens that while typing the cursor is moved from unwanted clicks. Best solution is to deactivate tap click for the touchpad and use the harware buttons.

This can be done either in the settings of your graphical desktop enviroment (Gnome3 works after installing libinput drivers) or directly from the shell temporarily with:

```
synclient TapButton1=0

```

This change can be made permament by changing the Xorg configuration.

### Video compression artifacts in VLC

When running on the Nvidia dGPU, if you see compression artifacts when playing videos in VLC, go to Tools -> Preferences -> Input / Codecs and set "Hardware-accelerated decoding" to "Disable".

## lspci

```
00:00.0 Host bridge: Intel Corporation Skylake Host Bridge/DRAM Registers (rev 07)
00:01.0 PCI bridge: Intel Corporation Skylake PCIe Controller (x16) (rev 07)
00:02.0 VGA compatible controller: Intel Corporation Device 191d (rev 06)
00:14.0 USB controller: Intel Corporation Sunrise Point-H USB 3.0 xHCI Controller (rev 31)
00:14.2 Signal processing controller: Intel Corporation Sunrise Point-H Thermal subsystem (rev 31)
00:16.0 Communication controller: Intel Corporation Sunrise Point-H CSME HECI #1 (rev 31)
00:17.0 SATA controller: Intel Corporation Sunrise Point-H SATA controller [AHCI mode] (rev 31)
00:1b.0 PCI bridge: Intel Corporation Sunrise Point-H PCI Root Port #17 (rev f1)
00:1c.0 PCI bridge: Intel Corporation Sunrise Point-H PCI Express Root Port #1 (rev f1)
00:1c.2 PCI bridge: Intel Corporation Sunrise Point-H PCI Express Root Port #3 (rev f1)
00:1c.4 PCI bridge: Intel Corporation Sunrise Point-H PCI Express Root Port #5 (rev f1)
00:1d.0 PCI bridge: Intel Corporation Sunrise Point-H PCI Express Root Port #9 (rev f1)
00:1d.4 PCI bridge: Intel Corporation Sunrise Point-H PCI Express Root Port #13 (rev f1)
00:1f.0 ISA bridge: Intel Corporation Sunrise Point-H LPC Controller (rev 31)
00:1f.2 Memory controller: Intel Corporation Sunrise Point-H PMC (rev 31)
00:1f.3 Audio device: Intel Corporation Sunrise Point-H HD Audio (rev 31)
00:1f.4 SMBus: Intel Corporation Sunrise Point-H SMBus (rev 31)
00:1f.6 Ethernet controller: Intel Corporation Ethernet Connection (2) I219-LM (rev 31)
01:00.0 VGA compatible controller: NVIDIA Corporation GM107GLM [Quadro M2000M] (rev ff)
02:00.0 Non-Volatile memory controller: Samsung Electronics Co Ltd NVMe SSD Controller (rev 01)
04:00.0 Network controller: Intel Corporation Wireless 8260 (rev 3a)
3e:00.0 Non-Volatile memory controller: Samsung Electronics Co Ltd NVMe SSD Controller (rev 01)
3f:00.0 Unassigned class [ff00]: Realtek Semiconductor Co., Ltd. RTS525A PCI Express Card Reader (rev 01)

```

`lsusb` returns something like:

```
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 004: ID 138a:0090 Validity Sensors, Inc.
Bus 001 Device 003: ID 04f2:b52c Chicony Electronics Co., Ltd
Bus 001 Device 006: ID 8087:0a2b Intel Corp.
Bus 001 Device 005: ID 0765:5010 X-Rite, Inc.
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```