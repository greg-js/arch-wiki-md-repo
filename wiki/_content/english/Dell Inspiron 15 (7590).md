**Note:** This page refers to the 7590 revision of the Inspiron 15\. Most of it also applies to the Vostro 7590 and the Inspiron 15 7591

| **Device** | **Status** | **Modules** |
| Video | Working | i915 |
| Wireless | Working | iwlwifi |
| Bluetooth | Working | btusb |
| Audio | Working | snd_hda_intel |
| Touchpad | Working | hid_multitouch |
| Webcam | Working | uvcvideo |
| USB-C / Thunderbolt 3 | Working | intel_wmi_thunderbolt |
| Wireless switch | Working | intel_hid |
| Function/Multimedia Keys | Working | ? |

Related articles

*   [Dell XPS 15 7590](/index.php/Dell_XPS_15_7590 "Dell XPS 15 7590")
*   [Dell XPS 15 9550](/index.php/Dell_XPS_15_9550 "Dell XPS 15 9550")
*   [Dell XPS 15 9560](/index.php/Dell_XPS_15_9560 "Dell XPS 15 9560")
*   [Dell XPS 15 9570](/index.php/Dell_XPS_15_9570 "Dell XPS 15 9570")

The Dell Inspiron 15 (7590) was released in May 2019, some country released it called Vostro 7590, and the aluminum alloy body version is Inspiron 7591\. They use the same BIOS and Motherboard.

The installation process for Arch on the Inspiron 15 does not differ from any other PC. For installation help, please see the [Installation guide](/index.php/Installation_guide "Installation guide") and [UEFI](/index.php/UEFI "UEFI"). This page covers the current status of hardware support on Arch, as well as post-installation recommendations.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 UEFI](#UEFI)
*   [2 Graphics](#Graphics)
    *   [2.1 Display](#Display)
    *   [2.2 Graphics Configuration](#Graphics_Configuration)
        *   [2.2.1 Intel Only](#Intel_Only)
        *   [2.2.2 Optimus Configuration (Hybrid Intel and Nvidia)](#Optimus_Configuration_(Hybrid_Intel_and_Nvidia))
            *   [2.2.2.1 PRIME Offload](#PRIME_Offload)
            *   [2.2.2.2 arch-prime-git](#arch-prime-git)
*   [3 Wifi](#Wifi)
*   [4 Keyboard](#Keyboard)
*   [5 Power Saving](#Power_Saving)
    *   [5.1 Enable thermald](#Enable_thermald)
    *   [5.2 Enable TLP](#Enable_TLP)
    *   [5.3 CPU Undervolting](#CPU_Undervolting)
*   [6 Firmware Updates](#Firmware_Updates)
*   [7 Thermal Modes / Fan profiles](#Thermal_Modes_/_Fan_profiles)
*   [8 Touchpad](#Touchpad)
    *   [8.1 Sensitivity](#Sensitivity)
*   [9 USB Type-C ports](#USB_Type-C_ports)
*   [10 Troubleshooting](#Troubleshooting)
    *   [10.1 I/O Operating is very slow](#I/O_Operating_is_very_slow)
    *   [10.2 Freezing while resume from suspend](#Freezing_while_resume_from_suspend)
    *   [10.3 No audio from 3.5mm headphone jack port](#No_audio_from_3.5mm_headphone_jack_port)

## UEFI

Before installing it is necessary to modify some UEFI Settings. They can be accessed by pressing the F2 key repeatedly when booting.

*   Change the SATA Mode from the default "RAID" to "AHCI". This will allow Linux to detect the NVME SSD. If dual booting with an existing Windows installation, Windows will not boot after the change but [this can be fixed without a reinstallation](https://triplescomputers.com/blog/uncategorized/solution-switch-windows-10-from-raidide-to-ahci-operation/).
*   Disable secure boot to allow Linux to boot.

Booting and installing from a microSD card is also possible, as long as SD Card and SD Card Boot are both enabled in the UEFI setup.

## Graphics

### Display

The video should work with the `i915` driver of the current [linux](https://www.archlinux.org/packages/?name=linux) kernel. Consult [Intel graphics](/index.php/Intel_graphics "Intel graphics") for a detailed installation and configuration guide as well as for [Intel graphics#Troubleshooting](/index.php/Intel_graphics#Troubleshooting "Intel graphics").

If you have the 4K (3840x2160) model, also check out [HiDPI](/index.php/HiDPI "HiDPI") for UI scaling configurations.

### Graphics Configuration

The Dell Inspiron 15 7590 has Intel HD Graphics 630 integrated graphics, and some models have an Nvidia GeForce GTX 1650 dedicated card as well in a hybrid configuration.

For computers with only integrated graphics, just install the [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) driver.

If your Inspiron has a hybrid graphics configuration (GTX1650 + HD Graphics 630) and you want to maximize battery life you can just use the Intel Graphics.

#### Intel Only

If your model comes with an nVidia card which you don't use then you can try to disable it with an ACPI command. Depending on the model, this can have a small to profound effect on the laptop's temperature and battery life (it can more than double battery life!)

*   Install the Intel video driver using the [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) package.
*   Blacklist the `nvidia` & `nouveau` modules [Kernel modules#Blacklisting](/index.php/Kernel_modules#Blacklisting "Kernel modules")
*   Power down the GPU [with an ACPI command](/index.php/Hybrid_graphics#Fully_Power_Down_Discrete_GPU "Hybrid graphics")

#### Optimus Configuration (Hybrid Intel and Nvidia)

##### PRIME Offload

Follow the instructions for [PRIME](/index.php/PRIME "PRIME"). In the case of this laptop, there are only two required steps:

*   Once the [NVIDIA](/index.php/NVIDIA "NVIDIA") drivers are installed, install the [nvidia-prime](https://www.archlinux.org/packages/?name=nvidia-prime) package, and use the `prime-run` command to run applications that should run on the dGPU.
*   Follow the steps outlined in the "Automatic Setup" section on this page: [https://download.nvidia.com/XFree86/Linux-x86_64/435.17/README/dynamicpowermanagement.html](https://download.nvidia.com/XFree86/Linux-x86_64/435.17/README/dynamicpowermanagement.html)

**Warning:** Without the second step above, the dGPU will remain powered, and will drain your battery quicker.

**Note:** The power-saving features described in the second step are available only for the GTX 1650\. If your laptop comes with the older GTX 1050, you may do better to use the older switching method (described below).

##### arch-prime-git

**Note:** [arch-prime-git](https://aur.archlinux.org/packages/arch-prime-git/) has been obsoleted upstream in favour of [PRIME#PRIME render offload](/index.php/PRIME#PRIME_render_offload "PRIME").

You can use [arch-prime-git](https://aur.archlinux.org/packages/arch-prime-git/) to switch the graphics card. Make sure you have installed [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel), `nvidia` driver, and [bbswitch-dkms](https://www.archlinux.org/packages/?name=bbswitch-dkms), then run `sudo prime-select service restore` before first time using it. Here is an example of using `prime-select` below:

```
$ sudo prime-select boot intel2    # select default card at boot with [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel)
$ sudo prime-select nvidia         # select nvidia graphics card for next login
$ sudo prime-select get-current    # display driver currently configured

```

*   Switching graphics card by logout may cause wifi function in `NetworkManager` stop working, you can `systemctl restart NetworkManager` to solve it.
*   The [Optimus](/index.php/Optimus "Optimus") setup consists of the integrated Intel chip connected to the laptop screen and the Nvidia card runs through this. As such, the Nvidia chip cannot be used without the Intel chip (some other laptops have the option in BIOS to turn Intel off and use just Nvidia, but not this laptop).

## Wifi

The Wifi adapter contains a Intel(R) Wireless-AC 9560 160MHz module. It should work out of the box with the `iwlwifi` driver in recent [linux](https://www.archlinux.org/packages/?name=linux) kernels.

## Keyboard

The keyboard backlight has a feature that makes it automatically turn off after a given timeout. This timeout can be adjusted by writing into `/sys/class/leds/dell\:\:kbd_backlight/stop_timeout`. For example,

```
echo "5m" > /sys/class/leds/dell\:\:kbd_backlight/stop_timeout

```

This would set the timeout to 5 minutes.

## Power Saving

### Enable thermald

[Thermald](/index.php/CPU_frequency_scaling#thermald "CPU frequency scaling") is a daemon created by Intel to control CPU heat more intelligently than the laptop's firmware is capable of. It [plays nicely](https://linrunner.de/en/tlp/docs/tlp-faq.html#install-config) with TLP.

### Enable TLP

The [TLP](/index.php/TLP "TLP") may increase battery life.

You can monitor the used power and also the temperature of your machine with the [s-tui](https://www.archlinux.org/packages/?name=s-tui) tool.

### CPU Undervolting

It's possible to undervolt CPU and GPU with intel-undervolt

This is an example of stable values for i7-9750H (depend of your cpu):

```
CPU (0): -155.27 mV
GPU (1): -110.35 mV
CPU Cache (2): -139.65 mV
System Agent (3): -0.00 mV
Analog I/O (4): -0.00 mV

```

Edit the config file

```
$ nano /etc/intel-undervolt.conf

```

This is an example for i7-9750H

```
# CPU Undervolting

undervolt 0 'CPU' -155
undervolt 1 'GPU' -110
undervolt 2 'CPU Cache' -140
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

## Firmware Updates

Dell provides firmware updates via Linux Vendor Firmware Service (LVFS). Refer to [Flashing BIOS from Linux#fwupd](/index.php/Flashing_BIOS_from_Linux#fwupd "Flashing BIOS from Linux") for additional information. A package is readily available at [fwupd](https://www.archlinux.org/packages/?name=fwupd). Updates are provided for the Thunderbolt controller as well. [There is an issue](https://github.com/dell/thunderbolt-nvm-linux/issues/10) where the Thunderbolt version number is detected as `00.00` after reflashing (currently being investigated).

Dell has also released updates to the SSD firmware, but these can only be updated from Windows, not from Linux.

## Thermal Modes / Fan profiles

Just like in Windows by using Dell Power Manager you can set the thermal configuration and behavior of the fans and CPU of your machine. This is done within a terminal with the commands below, or via a [KDE Plasma widget](https://store.kde.org/p/1282623):

To find out what thermal mode is set to type:

```
# smbios-thermal-ctl -g

```

To find all available thermal modes type:

```
# smbios-thermal-ctl -i

```

And finally to set the desired thermal mode that you identified with the command before type:

```
# smbios-thermal-ctl --set-thermal-mode=THERMAL_MODE

```

*   "Quiet" profile limits CPU power to 25W and thus reduces overall system performance.
*   "Balanced" and "Performance" profiles remove this limit.

## Touchpad

### Sensitivity

By default, the [libinput](/index.php/Libinput "Libinput") driver might not have the desired sensitivity. The acceleration can be changed via [xinput](/index.php/Xinput "Xinput") as follows:

```
 xinput --set-prop $(xinput | grep 'DELL.*Touchpad' | awk '{print $6}' | sed 's/id=//g') 'libinput Accel Speed' 0.5

```

## USB Type-C ports

## Troubleshooting

### I/O Operating is very slow

While running `sudo`, `htop`, `lspci` and so on, then get freezing or very slow, to fix it below:

If you're running over Linux Kernel 5.2, while staying in bootloader, add kernel parameter `nomodeset` to boot, then add `nouveau` to blacklist ([Kernel module#Blacklisting](/index.php/Kernel_module#Blacklisting "Kernel module"))

### Freezing while resume from suspend

Add these kernel parameters: `acpi_rev_override=1 acpi_osi=Linux mem_sleep_default=deep`

*   S0ix(or S2idle) suspend mode may cause freezing, only S3 can work properly.

### No audio from 3.5mm headphone jack port

In `pavucontrol`, try changing the Pulseaudio output profile from "Analog Stereo Output" to "Analog Stereo Duplex".