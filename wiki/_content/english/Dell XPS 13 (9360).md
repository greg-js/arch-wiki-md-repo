| **Device** | **Status** | **Modules** |
| Video | Working | i915 |
| Wireless | Working | ath10k |
| Bluetooth | Working | btusb |
| Audio | Working | snd_hda_intel |
| Touchpad | Working | hid_multitouch (mousedev) |
| Webcam | Working | uvcvideo |
| USB-C / Thunderbolt 3 | Working | ? |
| Wireless switch | Working | intel_hid |
| Function/Multimedia Keys | Working | ? |
| Fingerprint sensor | Not working | ? |

Related articles

*   [Dell XPS 13 (9333)](/index.php/Dell_XPS_13_(9333) "Dell XPS 13 (9333)")
*   [Dell XPS 13 (9343)](/index.php/Dell_XPS_13_(9343) "Dell XPS 13 (9343)")
*   [Dell XPS 13 (9350)](/index.php/Dell_XPS_13_(9350) "Dell XPS 13 (9350)")
*   [Dell XPS 13 (9370)](/index.php/Dell_XPS_13_(9370) "Dell XPS 13 (9370)")
*   [Dell XPS 13 2-in-1 (9365)](/index.php/Dell_XPS_13_2-in-1_(9365) "Dell XPS 13 2-in-1 (9365)")

The Dell XPS 13 Late 2016 (9360) is the fourth-generation model of the XPS 13 line. The laptop is available since October (pre-2017 model) in both a standard edition with Windows installed as well as both a pre-2017 model and a 2017 model (with insignificant hardware differences) Developer Edition with Ubuntu 16.04 "SP1" installed, featuring kernel 4.8 as of now. There is only minor hardware differences between them, mostly in regards to the mainboard microchip manufacturers. Just like the older versions ([9333](/index.php/Dell_XPS_13_(9333) "Dell XPS 13 (9333)"), [9343](/index.php/Dell_XPS_13_(9343) "Dell XPS 13 (9343)") and [9350](/index.php/Dell_XPS_13_(9350) "Dell XPS 13 (9350)")) it is available in different hardware configurations as well. These fourth gen models includes Intel's Kaby Lake CPUs and advertised with up to 16GB LPDDR 1866 MHz RAM and a 1TB PCI SSD. It will now also be available in Rose Gold. Prior to previous information and current specifications available provided by Dell (at least to regular customers), it is not available with the 2133 MHz RAM speed. However, in some models, including those available to employees and possibly Dell partners (and/or business customers), memory speed is indeed available up to 2133 Mhz LPDDR3 (non-upgradable). The same mentioned models are also available with the Intel Core i7-7660U (aswell as i7-7560U) with the Intel 640 Iris Plus onboard graphics. Respective clock frequencies are 2.5 Ghz (up to 4GHz in Turbo-mode) and 2,4 Ghz (up to 3.8 Ghz), respectively.

The installation process for Arch on the XPS 13 does not differ from any other PC. For installation help, please see the [Installation guide](/index.php/Installation_guide "Installation guide") and [UEFI](/index.php/UEFI "UEFI"). This page covers the current status of hardware support on Arch, as well as post-installation recommendations.

As of kernel 4.5, the Intel Kaby Lake architecture is supported.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Content Adaptive Brightness Control](#Content_Adaptive_Brightness_Control)
*   [2 Power Saving](#Power_Saving)
    *   [2.1 Disabling SD-Card reader](#Disabling_SD-Card_reader)
    *   [2.2 CPU Undervolting](#CPU_Undervolting)
    *   [2.3 NVM Express SSD](#NVM_Express_SSD)
    *   [2.4 Graphics adapter](#Graphics_adapter)
*   [3 Video](#Video)
*   [4 Wireless](#Wireless)
*   [5 Bluetooth](#Bluetooth)
*   [6 Thunderbolt 3 / USB 3.1](#Thunderbolt_3_/_USB_3.1)
    *   [6.1 Ethernet repeatedly disconnects/reconnects with Dell USB-C adapter (DA200)](#Ethernet_repeatedly_disconnects/reconnects_with_Dell_USB-C_adapter_(DA200))
    *   [6.2 USB-C Compatibility Chart](#USB-C_Compatibility_Chart)
    *   [6.3 Thunderbolt Firmware updates](#Thunderbolt_Firmware_updates)
*   [7 SATA controller](#SATA_controller)
*   [8 Touchpad](#Touchpad)
    *   [8.1 Remove psmouse errors from dmesg](#Remove_psmouse_errors_from_dmesg)
*   [9 Touchscreen](#Touchscreen)
    *   [9.1 Gestures](#Gestures)
    *   [9.2 Scrolling in Firefox](#Scrolling_in_Firefox)
*   [10 Keyboard Backlight](#Keyboard_Backlight)
*   [11 Hidden Keyboard Keys](#Hidden_Keyboard_Keys)
    *   [11.1 Unobtrusive mode](#Unobtrusive_mode)
*   [12 Firmware Updates](#Firmware_Updates)
*   [13 Sleep to idle (s2idle, S0ix)](#Sleep_to_idle_(s2idle,_S0ix))
*   [14 Troubleshooting](#Troubleshooting)
    *   [14.1 EFISTUB does not boot](#EFISTUB_does_not_boot)
    *   [14.2 Not waking from suspend](#Not_waking_from_suspend)
    *   [14.3 Power Drain after waking from standby](#Power_Drain_after_waking_from_standby)
    *   [14.4 Popping sound on headphones/external speakers](#Popping_sound_on_headphones/external_speakers)
    *   [14.5 Crackling sound with screen changes](#Crackling_sound_with_screen_changes)
    *   [14.6 Coil Whine](#Coil_Whine)
    *   [14.7 Freezing after waking from suspend](#Freezing_after_waking_from_suspend)
    *   [14.8 Continuous hissing sound with headphones](#Continuous_hissing_sound_with_headphones)
    *   [14.9 Blank screen issue after booting](#Blank_screen_issue_after_booting)
*   [15 Fingerprint sensor](#Fingerprint_sensor)
*   [16 See Also](#See_Also)

## Content Adaptive Brightness Control

In the XPS 13 the display panels (both FHD and QHD+) come with Content Adaptive Brightness Control (usually referred to as CABC or DBC) embedded in the panel firmware - it adjusts the screen brightness depending on the content displayed on the screen. While it saves a bit of power, it is generally undesirable, especially for Linux users who are likely to be switching between dark and light screen content. Dell has issued a fix for this, however it is only available to run in Windows. The fix is available [directly from Dell](http://www.dell.com/support/home/us/en/04/drivers/driversdetails?driverId=312K3&lwp=rt).

To test if your XPS 13 is affected by the CABC, go to this [test page](http://tylerwatt12.com/dc/). It is possible to apply Dell's firmware update using a portable Windows 10 on a USB device:

1.  Install (for example) [woeusb-git](https://aur.archlinux.org/packages/woeusb-git/)
2.  Download a Windows 10 ISO from [Microsoft's website](https://www.microsoft.com/en-in/software-download/windows10ISO)
3.  Create a portable Windows 10 installation [using woeusb](https://www.addictivetips.com/ubuntu-linux-tips/make-windows-usb-drive-on-linux-woeusb/)
4.  Boot the XPS 13 from your Windows 10 USB device (F12)
5.  In Windows, download and install the latest driver for the [Intel Graphics controller](https://www.dell.com/support/home/us/en/04/drivers/driversdetails?driverId=RFGHP)
6.  Then download and install [this tool](http://www.dell.com/support/home/us/en/04/drivers/driversdetails?driverId=312K3) to update the panel firmware. The tool gives you the option to disable CABC
7.  Reboot (from USB)
8.  Reboot to Arch Linux and rerun the [test](http://tylerwatt12.com/dc/)

## Power Saving

It's possible to save around ~10/20% energy with somes tricks.

### Disabling SD-Card reader

The SD-Card adapter can be disabled in BIOS settings to save ~0.5W.

### CPU Undervolting

It's possible to undervolt CPU and GPU with [intel-undervolt](/index.php/Undervolting_CPU#intel-undervolt "Undervolting CPU")

This is an example of best stable values for a I5-7200u (depend of your cpu):

```
CPU (0): -160.16 mV
GPU (1): -125.00 mV
CPU Cache (2): -89.84 mV

```

Edit the config file

```
$ nano /etc/intel-undervolt.conf

```

This is an example for i5-7200u

```
# CPU Undervolting

undervolt 0 'CPU' -160
undervolt 1 'GPU' -125
undervolt 2 'CPU Cache' -90
undervolt 3 'System Agent' 0
undervolt 4 'Analog I/O' 0

# Daemon Update Interval

interval 5000

```

then enable/start the daemon :)

```
$ systemctl enable intel-undervolt
$ systemctl start intel-undervolt

```

### NVM Express SSD

For some devices it might be necessary to set a higher value for the `nvme_core.default_ps_max_latency_us` parameter to enable all power saving states. This parameter has to be set on the [kernel command line](/index.php/Kernel_command_line "Kernel command line").

For the Toshiba 512GB SSD used in some models of the XPS 13 the value to enable all states is 170000 (the combined latency of entering and leaving the highest power state, add `nvme_core.default_ps_max_latency_us=170000` to your kernel command line). For the 1TB SSD this valued should be increased to 180000 instead. To check if all states are enabled you can use the [nvme-cli](https://www.archlinux.org/packages/?name=nvme-cli) package, which provides the `nvme-cli` command:

```
# nvme get-feature -f 0x0c -H /dev/nvme0
get-feature:0xc (Autonomous Power State Transition), Current value:0x000001
Autonomous Power State Transition Enable (APSTE): Enabled
Auto PST Entries  .................
Entry[ 0]   
.................
Idle Time Prior to Transition (ITPT): 1500 ms
Idle Transition Power State   (ITPS): 3
.................
Entry[ 1]   
.................
Idle Time Prior to Transition (ITPT): 1500 ms
Idle Transition Power State   (ITPS): 3
.................
Entry[ 2]   
.................
Idle Time Prior to Transition (ITPT): 1500 ms
Idle Transition Power State   (ITPS): 3
.................
Entry[ 3]   
.................
Idle Time Prior to Transition (ITPT): 8500 ms
Idle Transition Power State   (ITPS): 4
.................

```

If the power states are enabled there should be values for ITPT and ITPS in the first entries. Also the ITPS-value of the last filled entry should be the highest power saving-state of the SSD (which can be viewed using `smartctl -a /dev/nvme0` or `nvme id-ctrl /dev/nvme0`).

### Graphics adapter

For the HD 620 graphics card the following modules are working: (see [Intel graphics#Module-based options](/index.php/Intel_graphics#Module-based_options "Intel graphics"))

```
modeset=1 enable_fbc=1 

```

The first argument is to enable modesetting if it's not set by default. The second argument is needed to activate framebuffer compression power savings. These values should work well!

```
enable_guc=3

```

This argument is used to enable GuC updates. GuC is a small proprietary binary blob released by intel to update the GuC binary in faster intervals than the kernel release does. It is used for graphics workload scheduling on the various graphics parallel engines. More details at ([https://01.org/linuxgraphics/downloads/firmware](https://01.org/linuxgraphics/downloads/firmware)). The GuC binary for kaby lake is included since firmware release linux-firmware 20170217 in the official repository. HuC is also a binary blob from intel. It's designed to offload some of the media functions from the CPU to GPU. As of kernel 4.12, HuC is loaded if GuC is enabled. One can check with 'cat /sys/kernel/debug/dri/0/i915_huc_load_status' and 'cat /sys/kernel/debug/dri/0/i915_guc_load_status'.

```
enable_psr=1

```

Panel Self Refresh (PSR) is working for eDP 1.3 and up and does stop the creation of new frames when the screen content is static to save energy. If you experience problems with PSR try to set 'disable_power_well=0' or disable otherwise. It may also be required to add the `modconf` hook to [Mkinitcpio](/index.php/Mkinitcpio#HOOKS "Mkinitcpio") to avoid a hang after resume on both Xorg and Wayland.

**Note:** Some users have reported problems with `enable_psr==1` where on first boot or after resume the panel stays black once reaching the [desktop environment](/index.php/Desktop_environment "Desktop environment"), only refreshing after switching to and from a tty. In this case it is required to simply remove the option.

```
NOT WORKING: semaphores=1 

```

The semaphore option is NOT working for kaby lake CPUs and won't enable even if you set the option to 1.

## Video

The video should work with the `i915` driver of the current [linux](https://www.archlinux.org/packages/?name=linux) kernel. Consult [Intel graphics](/index.php/Intel_graphics "Intel graphics") for a detailed installation and configuration guide as well as for [Intel graphics#Troubleshooting](/index.php/Intel_graphics#Troubleshooting "Intel graphics").

If you have the QHD+ (3200x1800) model, also check out [HiDPI](/index.php/HiDPI "HiDPI") for UI scaling configurations.

*But there might be video issues left for this model. **Please help by contributing any feedback** about similar issues you might have experience(d) to this bugreport ([https://bugs.freedesktop.org/show_bug.cgi?id=100671](https://bugs.freedesktop.org/show_bug.cgi?id=100671)).*

## Wireless

The Killer 1535 Wirless Adapter is functional and the ath10k firmware is included in recent linux kernel versions. The connection speed reported by iw is limited to 1-6Mbits/s. However this is just the output being wrong. The real connection speed is not limited to this value.

[Some users are experiencing issues](http://en.community.dell.com/support-forums/network-internet-wireless/f/3324/t/19998908?pi41127=3), where the connection is dropped under heavy load but reconnects within a brief moment. This might not be noticed during browsing at all but becomes apparent in online games. There is [a firmware update proposed by DELL](http://en.community.dell.com/techcenter/os-applications/f/4613/p/20002634/20994007#20994007) to fix the issue, but it might not fix all the issues. In at least one case the new firmware did not fix the connection loss / low connection speed problem. Signs of this problem seems to be two kinds of messages in dmesg:

```
pcieport 0000:00:1c.4: AER: Corrected error received: id=00e4
pcieport 0000:00:1c.4: PCIe Bus Error: severity=Corrected, type=Data Link Layer, id=00e4(Transmitter ID)
pcieport 0000:00:1c.4:   device [8086:9d14] error status/mask=00001000/00002000
pcieport 0000:00:1c.4:    [12] Replay Timer Timeout  

```

And also:

```
CPU: 3 PID: 1410 Comm: irq/133-ath10k_ Not tainted 
Hardware name: Dell Inc. XPS 13 9360/0839Y6, BIOS 2.1.0 08/02/2017
Call Trace:
  <IRQ>
  dump_stack+0x63/0x82
  __warn+0xcb/0xf0
  warn_slowpath_null+0x1d/0x20
  net_rx_action+0x274/0x3a0
  ? irq_finalize_oneshot.part.35+0xe0/0xe0

```

As of February 2018, Dell support suggests to update the firmware of the network adapter in the following way:

1.  Confirm that you have QCA6174 checking the output of `sudo lspci`
2.  [Download](https://codeload.github.com/kvalo/ath10k-firmware/zip/master) the latest firmware and extract the contents from [git](https://github.com/kvalo/ath10k-firmware)
3.  Substitute the `QCA6174` folder in `/lib/firmware/ath10k/` with the one downloaded
4.  Inside the new folder, rename `firmware-4.bin_WLAN.RM.2.0-00180-QCARMSWPZ-1` to `firmware-4.bin`
5.  Reboot and test the new Killer Wi-Fi firmware

Update: Internet connection dropped even with the firmware from the above fix. Using the newer firmware `firmware-6.bin_WLAN.RM.4.4.1-00102-QCARMSWP-1` by downloading that file from [https://github.com/kvalo/ath10k-firmware/blob/master/QCA6174/hw3.0/4.4.1.c1/firmware-6.bin_RM.4.4.1.c1-00042-QCARMSWP-1](https://github.com/kvalo/ath10k-firmware/blob/master/QCA6174/hw3.0/4.4.1.c1/firmware-6.bin_RM.4.4.1.c1-00042-QCARMSWP-1), copying it to `/usr/lib/firmware/ath10k/QCA6174/hw3.0/` and renaming it to `firmware-6.bin` fixes this. Reboot and verify that this newer firmware is used by verifying that `dmesg | grep ath` outputs:

```
ath10k_pci 0000:3a:00.0: firmware ver RM.4.4.1.c1-00042-QCARMSWP-1 api 6 features wowlan,ignore-otp crc32 40fb7bdd

```

BIOS version 2.9.0 manages to make these crashes occur no matter what firmware you load. Updating to at least version 2.10.0 resolves this issue. Alternatively, installing an [Intel WiFi card](https://www.amazon.com/Intel-Dual-Band-Wireless-Ac-8265/dp/B01MZA1AB2) solves the problem.

## Bluetooth

After following the instructions given at [Bluetooth](/index.php/Bluetooth "Bluetooth") tethering of internet connections via phone works immediately.

See [Troubleshooting](#Freezing_after_waking_from_suspend) when having issues with Bluetooth and suspend (blinking CapsLock).

## Thunderbolt 3 / USB 3.1

The USB-C port supports Thunderbolt 3, Displayport-over-USB-C and USB power delivery as well as USB 3.1.

### Ethernet repeatedly disconnects/reconnects with Dell USB-C adapter (DA200)

Use of a power management package (such as [TLP](/index.php/TLP "TLP")) may cause the ethernet adapter to repeatedly disconnect and reconnect. If this happens, disable/blacklist USB autosuspend for the ethernet adapter. (On my laptop, this is the device <tt>Bus 004 Device 007: ID 0bda:8153 Realtek Semiconductor Corp</tt> in the output of <tt>lsusb</tt>.)

Also disabling or reducing power of wifi may help: [http://en.community.dell.com/support-forums/network-internet-wireless/f/3324/t/19995423](http://en.community.dell.com/support-forums/network-internet-wireless/f/3324/t/19995423)

### USB-C Compatibility Chart

**Note:** *A comprehensive and up to date list of USB type C adapters and hubs is present in the [discussion](/index.php/Talk:Dell_XPS_13_(9360)#USB-C_Compatibility_Chart "Talk:Dell XPS 13 (9360)") page.*

### Thunderbolt Firmware updates

The thunderbolt controller in the laptop has an embedded firmware. The laptop ships with firmware version NVM 18, and the most recent available version from Dell's website is NVM 26\. If encountering compatibility problems with Thunderbolt accessories (such as the DA-200), the firmware may need to be updated. If you have fwupd (see: [#Firmware Updates](#Firmware_Updates)) set up then you should receive this update automatically. Otherwise, you can install it manually as follows.

Dell maintained a github repository with the firmware, but abandoned it now that the firmware is on LVFS. The current version is available as `0x075B_secure.bin` (or 0x082A for newer model, see instructions below) inside the [Windows package](http://www.dell.com/support/home/us/en/19/drivers/driversdetails?driverId=4FC9M). This can be extracted with [p7zip](https://www.archlinux.org/packages/?name=p7zip).

Here is a short list of steps to update the Thunderbolt-Firmware on linux 4.13+ (use at your own risk):

*   Force enable the thunderbolt controller (or plug in a device to enable it)

```
# echo 1 | sudo tee /sys/bus/wmi/devices/86CCFD48-205E-4A77-9C48-2021CBEDE341/force_power 

```

*   Check your model ID. If it's 0x082A, use the 0x082A firmware instead of the 0x075B one.

```
# cat /sys/bus/thunderbolt/devices/0-0/device

```

*   Flash the 9360 firmware from the thunderbolt-nvm-linux repository to a non active NVME memory spot

```
# dd if=payloads/0x075B.bin of=/sys/bus/thunderbolt/devices/0-0/nvm_non_active0/nvmem

```

*   Trigger the update process

```
# echo 1 > /sys/bus/thunderbolt/devices/0-0/nvm_authenticate

```

*   At this point, your screen should flickr a couple of time. Verify that the update is done by checking that authenticate returns 0

```
# cat /sys/bus/thunderbolt/devices/0-0/nvm_authenticate

```

*   Verify the new nvme version (it should return 26.1)

```
# cat /sys/bus/thunderbolt/devices/0-0/nvm_version

```

*   Put the controller back in normal mode

```
# echo 0 | sudo tee /sys/bus/wmi/devices/86CCFD48-205E-4A77-9C48-2021CBEDE341/force_power

```

## SATA controller

When the SATA-controller is set to `RAID On` in BIOS, the SSD is not recognized, because the kernel does not support remapped AHCI device, see [[1]](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=aecec8b60422118b52e3347430ba9382e57d6d76). Set to `AHCI` before attempting to install Arch.

## Touchpad

The touchpad has no explicit buttons. The button is built into the pad's surface. There is a small line printed on the pad separating left/right click areas, and libinput does the same separation in software.

Libinput also provides a middle button – to issue a middle click, simply press on the middle area right between the virtual left and right buttons (i.e. on the small printed separator line).

### Remove psmouse errors from dmesg

If `dmesg | grep -i psmouse` returns an error, but your touchpad still works, then it might be a good idea to disable `psmouse`. First create a config file:

```
# nano /etc/modprobe.d/modprobe.conf

blacklist psmouse

```

Then add this file to `/etc/mkinitcpio.conf`:

```
...
FILES=(/etc/modprobe.d/modprobe.conf)
...

```

Rebuild your initial ramdisk image (see [Mkinitcpio#Image creation and activation](/index.php/Mkinitcpio#Image_creation_and_activation "Mkinitcpio")).

## Touchscreen

The touchscreen works without additional configuration. The bug resulting in a disabled touchscreen after resume was fixed with kernel 4.8.5.

### Gestures

Refer to [libinput#Gestures](/index.php/Libinput#Gestures "Libinput") for information about the current development state and available methods.

### Scrolling in Firefox

See [Firefox/Tweaks#Pixel-perfect trackpad scrolling](/index.php/Firefox/Tweaks#Pixel-perfect_trackpad_scrolling "Firefox/Tweaks"). This enables both touchscreen scrolling and high-res trackpad scrolling.

## Keyboard Backlight

By default, the keyboard backlight turns off after 10 seconds of inactivity. Some users might find this too short and annoying. The delay can be increased (or decreased) by editing this file:

```
/sys/devices/platform/dell-laptop/leds/dell\:\:kbd_backlight/stop_timeout

```

You can also change the brightness (0-2) by editing the following file. This is identical to pressing F10 on your keyboard:

```
/sys/devices/platform/dell-laptop/leds/dell\:\:kbd_backlight/brightness

```

## Hidden Keyboard Keys

There are additional Fn+<Key> (sequences) that are not marked at all on the keyboard but underlying hardware generates them anyway. Here they are (if you find more add them to the table below):

<caption>Hidden Fn Keys</caption>
| Fn+<Key> | Resulting key (sequence) |
| Fn+Ins | XF86Sleep |
| Fn+Super_L | Super_R |
| Fn+B | Pause |
| Fn+R | Print |
| Fn+S | Scroll_Lock |
| Fn+A / D / E / F / G / T / Q / W | XF86Launch3 |

### Unobtrusive mode

If enabled in BIOS, pressing Fn+F7 will disable sound, keyboard and screen backlight, the charging LED and the LED on the power button. Unfortunately there seems to be no way to disable just the LEDs- some users recommend black electrical tape. The output of `smbios-token-ctl -d` only list changes related to screen, keyboard and sound when unobtrusive mode is active.

## Firmware Updates

Dell provides firmware updates via [fwupd](/index.php/Fwupd "Fwupd"). Please note if you have used a bind mount partition for /boot or are booting via legacy BIOS/CSM instead of UEFI, you will not be able to use the fwupd utility - instead use the method below.

Alternatively, the BIOS update can be downloaded from the [Dell website](https://www.dell.com/support/home/us/en/19/product-support/product/xps-13-9360-laptop/drivers) (filter by "BIOS") and placed in a location accessible to the firmware. This could be the '/boot' folder, or a FAT32 formatted USB stick. Then restart your laptop and hit F12 while starting. In the boot menu choose firmware update and select the downloaded file.

## Sleep to idle (s2idle, S0ix)

According to the method described in an [Intel article](https://01.org/blogs/qwang59/2018/how-achieve-s0ix-states-linux), this device supports Low Power S0 Idle (S0ix).

To try S0ix, write `freeze` to `/sys/power/state` (see [Power management/Suspend and hibernate](/index.php/Power_management/Suspend_and_hibernate "Power management/Suspend and hibernate")). The system should behave like it is sleeping, except the power button light is on. Press power button to wake up.

S0ix can be used as an alternative to "Sleep to RAM", by changing the following systemd configuration:

 `/etc/systemd/sleep.conf` 
```
[Sleep]
SuspendState=freeze mem standby

```

You may need to prevent the xHCI controller from waking up the system. Write `XHC` to `/proc/acpi/wakeup`, or write `disabled` to `/sys/devices/pci0000:00/0000:00:14.0/power/wakeup`. Different models may have different PCI ID for the xHCI controller, see the 4th column of `grep XHC /proc/acpi/wakeup`.

To make the change permanent, put a file to `/etc/tmpfiles.d`:

 `/etc/tmpfiles.d/disable-xhci-wakeup.conf` 
```
w /sys/devices/pci0000:00/0000:00:14.0/power/wakeup - - - - disabled

```

If you want to enable waking up by key press:

 `/etc/tmpfiles.d/enable-key-press-wakeup.conf` 
```
# Enable key press to wakeup
w /sys/devices/platform/i8042/serio0/power/wakeup - - - - enabled
```

## Troubleshooting

### EFISTUB does not boot

The BIOS does not pass any boot parameters to the kernel. Use a UEFI [boot loader](/index.php/Boot_loader "Boot loader") instead.

It is possible to work around this issue by bulding single file EFI images containing the parameters. See [[2]](https://github.com/xdever/arch-efiboot).

### Not waking from suspend

Update the BIOS to 1.0.7 to patch this issue.

### Power Drain after waking from standby

Some users recognised ~2W more power consumption after waking up from standby. Go to the UEFI Firmware Settings (tap the F2 key when the Dell logo appears) and uncheck the 'Enable Thunderbolt Boot Support'. You may use [powertop](https://www.archlinux.org/packages/?name=powertop) or [powerstat-git](https://aur.archlinux.org/packages/powerstat-git/) to reproduce and check this behaviour yourself.

### Popping sound on headphones/external speakers

Power saving being enabled on the audio chip will cause the hissing and popping to appear.

Have a look at [ALSA troubleshooting#Pops when starting and stopping playback](/index.php/ALSA_troubleshooting#Pops_when_starting_and_stopping_playback "ALSA troubleshooting") and [ALSA troubleshooting#Popping sound after resuming from suspension](/index.php/ALSA_troubleshooting#Popping_sound_after_resuming_from_suspension "ALSA troubleshooting").

If you are using [tlp](https://www.archlinux.org/packages/?name=tlp), it will activate power saving by default when on battery. Edit `/etc/default/tlp` and disable it.

### Crackling sound with screen changes

Some users experienced a weird crackling, white noise sound when the display is changing its contents after waking the computer from S3 sleep..

This issue should be patched as of the 4.14.15 kernel.

If you're still encountering this issue, try manually applying this patch[[3]](https://lkml.org/lkml/2018/1/22/169). Adding the kernel parameter `i915 enable_guc=1` as described in [Intel graphics](/index.php/Intel_graphics "Intel graphics") might also help, however multiple people have reported that this does not fix the problem completely.

### Coil Whine

Unfortunately Dell still did not fix this issue and the sound for my model was very loud. The issue seems to be connected to the graphic card. For some users, it is possible to reduce it a lot by activating frame buffer compression "enable_fbc=1" [Intel graphics#Framebuffer compression (enable_fbc)](/index.php/Intel_graphics#Framebuffer_compression_(enable_fbc) "Intel graphics"). The coil whine will then start again under heavy graphic load. For the touchscreen model, this may be very often, due to the high resolution screen. In a similar vein, the display can be run at a lower resolution, again reducing the load on the graphics card.

### Freezing after waking from suspend

Installing [xf86-video-intel-git](https://aur.archlinux.org/packages/xf86-video-intel-git/) is [reported](https://bbs.archlinux.org/viewtopic.php?pid=1698282#p1698282) to fix this.

When using a bluetooth device (confirmed for a Logitech MX Anywhere 2S and gnome), the computer frequently does not respond and the LED on CapsLock blinks. Using the solution from [launchpad](https://bugs.launchpad.net/dell-sputnik/+bug/1766825/comments/26) helps in this case.

### Continuous hissing sound with headphones

Open alsamixer and set "Headphone Mic Boost" gain to 10 dB (See discussion on [reddit](https://www.reddit.com/r/Dell/comments/4j1zz4/headphones_have_static_noise_with_ubuntu_1604_on/)). Note that this does reduce the volume slightly.

You may also run the equivalent command:

```
$ amixer -c PCH cset 'name=Headphone Mic Boost Volume' 1

```

PulseAudio will rewrite these ALSA settings on each boot. So if you use PulseAudio you may change its config to make the setting permanent:

 `/usr/share/pulseaudio/alsa-mixer/paths/analog-input-headphone-mic.conf` 
```
[Element Headphone Mic Boost]
required-any = any
switch = select
# Replace "volume = merge" by:
volume = 1
override-map.1 = all
override-map.2 = all-left,all-right

```
 `/usr/share/pulseaudio/alsa-mixer/paths/analog-input-internal-mic.conf` 
```
[Element Headphone Mic Boost]
switch = off
# Replace "volume = off" by:
volume = 1

```

This change will be overwritten by an upgrade of PulseAudio though. To make these changes persistent across upgrades you can use a pacman hook:

 `/etc/pacman.d/hooks/headphones_hissing.hook` 
```
[Trigger]
Operation = Install
Operation = Upgrade
Type = Package
Target = pulseaudio

[Action]
Description = Set default Headphone Mic Boost volume to 1...
When = PostTransaction
Exec = /usr/bin/sed -i '/\[Element Headphone Mic Boost\]/,/^$/s/volume = .*/volume = 1/' /usr/share/pulseaudio/alsa-mixer/paths/analog-input-internal-mic.conf /usr/share/pulseaudio/alsa-mixer/paths/analog-input-headphone-mic.conf

```

Alternatively, you can avoid these changes to files under /usr by calling amixer at startup. The first solution would be to add the command above to the profile of your shell (`~/.bash_profile` in case of bash). Or you set up a systemd user service that is pulled in by PulseAudio:

 `~/.config/systemd/user/headphones_hissing.service` 
```
[Unit]
Description=Disable hissing sound with headphones
After=pulseaudio.service
PartOf=pulseaudio.service

[Service]
Type=oneshot
ExecStart=amixer -c PCH cset 'name=Headphone Mic Boost Volume' 1

[Install]
WantedBy=pulseaudio.service

```

Enable the unit with `systemctl --user enable headphones_hissing.service`.

To give these benefits to the other users on your system, you can set this globally, i.e. call amixer in `/etc/profile` and put the systemd unit in `/etc/systemd/user/headphones_hissing.service` and enable it globally by using the `--global` option respectively.

### Blank screen issue after booting

If using "late start" [KMS](/index.php/KMS "KMS") (the default) and the screen goes blank when loading modules, it may help to add `i915` and `intel_agp` to the initramfs or using a special [kernel parameter](/index.php/Kernel_parameter "Kernel parameter"). Consult [Intel graphics#Blank screen during boot, when "Loading modules"](/index.php/Intel_graphics#Blank_screen_during_boot,_when_"Loading_modules" "Intel graphics") for more information about the kernel parameter way and have a look at [Kernel mode setting#Early KMS start](/index.php/Kernel_mode_setting#Early_KMS_start "Kernel mode setting") for a guide on how to setup the modules for the initramfs.

## Fingerprint sensor

Dell officially does not support fingerprint reader functionality [[4]](http://en.community.dell.com/techcenter/os-applications/f/4613/t/20006668), however an effort on reverse engineering the protocol of Validity 138a:0090, 138a:0094, 138a:0097 fingerprint readers can be found at github [[5]](https://github.com/nmikhailov/Validity90).

## See Also

*   [Arch Forum thread for Dell XPS 13 (9360)](https://bbs.archlinux.org/viewtopic.php?id=217865)
*   [Service Manual for Dell XPS 13 (9360)](http://topics-cdn.dell.com/pdf/xps-13-9360-laptop_service%20manual2_en-us.pdf)
*   [How to achieve S0ix states in Linux*](https://01.org/blogs/qwang59/2018/how-achieve-s0ix-states-linux)
*   [Best practice to debug Linux* suspend/hibernate issues](https://01.org/blogs/rzhang/2015/best-practice-debug-linux-suspend/hibernate-issues)