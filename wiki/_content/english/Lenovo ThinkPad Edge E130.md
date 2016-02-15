This article covers the Arch Linux support for the Lenovo ThinkPad Edge E130 laptop.

## Contents

*   [1 Installation](#Installation)
*   [2 Hardware](#Hardware)
    *   [2.1 lspci](#lspci)
*   [3 Configuration](#Configuration)
    *   [3.1 ClickPad & TrackPoint](#ClickPad_.26_TrackPoint)
    *   [3.2 Video](#Video)
    *   [3.3 Ethernet](#Ethernet)
    *   [3.4 Wireless](#Wireless)
        *   [3.4.1 Intel Centrino Wireless-N 2230N](#Intel_Centrino_Wireless-N_2230N)
        *   [3.4.2 Ericsson H5321 gw Mobile Broadband modem](#Ericsson_H5321_gw_Mobile_Broadband_modem)
    *   [3.5 Sound](#Sound)
    *   [3.6 Webcam](#Webcam)
    *   [3.7 Power](#Power)
*   [4 Other](#Other)
    *   [4.1 Hibernation & Suspend](#Hibernation_.26_Suspend)
    *   [4.2 ACPI / Fan control](#ACPI_.2F_Fan_control)
    *   [4.3 Kernel Mode Setting (KMS)](#Kernel_Mode_Setting_.28KMS.29)
    *   [4.4 Plymouth](#Plymouth)

## Installation

No special steps are needed during setup, everyhing (WiFi, Network, Modem) seemed to work from setup media so you can follow [Installation guide](/index.php/Installation_guide "Installation guide") as usual.

## Hardware

Tested model 33588CG (BIOS H4ET92WW v2.52 04/18/2013) on **Kernel 3.11.1** (stable) and **Kernel 3.11.1 with CK1 patchset** (linux-ck-ivybridge package from [Repo-ck](/index.php/Repo-ck "Repo-ck"))

| Device | Working? (Yes/No) |
| Video | Yes (xf86-video-intel and intel-dri for 3D; KMS works too) |
| Ethernet (Realtek RTL8111/8168 Gigabit Ethernet (rev 07)) | Yes (module: r8169) |
| Wireless (Intel Wireless-N 2230 (rev c4)) | Yes (module: iwlwifi) |
| Bluetooth | Yes (module: bluetooth; use blueman for GUI) |
| Audio | Yes (module: snd_hda_intel) |
| Web Camera | Yes (test with skype or this command: mplayer tv:// -tv driver=v4l2 ) |
| Card Reader (Chicony) | Not Tested |
| Modem (Ericcson Modem) | Yes (using NetworkManager with modemmanager) |

### lspci

```
00:00.0 Host bridge: Intel Corporation 3rd Gen Core processor DRAM Controller (rev 09)
00:02.0 VGA compatible controller: Intel Corporation 3rd Gen Core processor Graphics Controller (rev 09)
00:14.0 USB controller: Intel Corporation 7 Series/C210 Series Chipset Family USB xHCI Host Controller (rev 04)
00:16.0 Communication controller: Intel Corporation 7 Series/C210 Series Chipset Family MEI Controller #1 (rev 04)
00:1a.0 USB controller: Intel Corporation 7 Series/C210 Series Chipset Family USB Enhanced Host Controller #2 (rev 04)
00:1b.0 Audio device: Intel Corporation 7 Series/C210 Series Chipset Family High Definition Audio Controller (rev 04)
00:1c.0 PCI bridge: Intel Corporation 7 Series/C210 Series Chipset Family PCI Express Root Port 1 (rev c4)
00:1c.1 PCI bridge: Intel Corporation 7 Series/C210 Series Chipset Family PCI Express Root Port 2 (rev c4)
00:1c.2 PCI bridge: Intel Corporation 7 Series/C210 Series Chipset Family PCI Express Root Port 3 (rev c4)
00:1c.5 PCI bridge: Intel Corporation 7 Series/C210 Series Chipset Family PCI Express Root Port 6 (rev c4)
00:1d.0 USB controller: Intel Corporation 7 Series/C210 Series Chipset Family USB Enhanced Host Controller #1 (rev 04)
00:1f.0 ISA bridge: Intel Corporation HM77 Express Chipset LPC Controller (rev 04)
00:1f.2 SATA controller: Intel Corporation 7 Series Chipset Family 6-port SATA Controller [AHCI mode] (rev 04)
00:1f.3 SMBus: Intel Corporation 7 Series/C210 Series Chipset Family SMBus Controller (rev 04)
03:00.0 Network controller: Intel Corporation Centrino Wireless-N 2230 (rev c4)
04:00.0 Unassigned class [ff00]: Realtek Semiconductor Co., Ltd. RTS5209 PCI Express Card Reader (rev 01)
09:00.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL8111/8168 PCI Express Gigabit Ethernet controller (rev 07)

```

## Configuration

### ClickPad & TrackPoint

The ClickPad works with the xf86-input-synaptic. TrackPoint and extra buttons seem to work too without any extra configuration needed.

### Video

See [Intel graphics](/index.php/Intel_graphics "Intel graphics") and [xrandr](/index.php/Xrandr "Xrandr").

### Ethernet

Works out of the box. Module: **r8169**

### Wireless

#### Intel Centrino Wireless-N 2230N

Works out of the box. Module: **iwlwifi**

#### Ericsson H5321 gw Mobile Broadband modem

Works out of the box. Module: **cdc_mbim**

Tested working with [networkmanager](https://www.archlinux.org/packages/?name=networkmanager) and [modemmanager](https://www.archlinux.org/packages/?name=modemmanager)

### Sound

Works out of the box. Module: **snd-hda-intel**

### Webcam

Works out of the box. Tested using Skype or this command: mplayer tv:// -tv driver=v4l2

### Power

Suspend and Hibernation both work using [pm-utils](/index.php/Pm-utils "Pm-utils") and [systemd](/index.php/Systemd "Systemd")

## Other

You can find more general ThinkPad Edge hardware related information on [ThinkPad Edge](/index.php/ThinkPad_Edge "ThinkPad Edge") page. The sections below provides information on what was tested to work

### Hibernation & Suspend

Follow [Power management#Power management with systemd](/index.php/Power_management#Power_management_with_systemd "Power management") guide. Works as of **systemd-204-3** (CAUTION: current **systemd-207-5** seemed to break hibernation)

### ACPI / Fan control

[Acpid](/index.php/Acpid "Acpid") works, just follow general guidelines. For Fan control use [tpfanco-svn](https://aur.archlinux.org/packages/tpfanco-svn/) (**tpfan-admin** for GUI interface). Follow instructions on [Thinkpad Fan Control](/index.php/Thinkpad_Fan_Control "Thinkpad Fan Control").

### Kernel Mode Setting (KMS)

KMS lets you set high native resolution early during system boot. Follow guidelines in [Kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting") page. Add **i915** in MODULES while editing mkinitcpio.conf for early KMS.

### Plymouth

[Plymouth](/index.php/Plymouth "Plymouth") provides a flicker-free graphical boot processs. Seemed to work without problems.