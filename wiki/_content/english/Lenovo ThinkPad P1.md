Lenovo ThinkPad P1 was released in 2018 and has up to Intel Core i7-8850H or Xeon E-2176M 6-core processor, up to 64 GB DDR4 RAM, and up to NVIDIA Quadro P2000 graphics.

**Note:** The ThinkPad X1 Extreme is a consumer version of the same laptop which uses extremely similar hardware. Most of the information from [Lenovo ThinkPad X1 Extreme](/index.php/Lenovo_ThinkPad_X1_Extreme "Lenovo ThinkPad X1 Extreme") should be applicable to P1 models as well.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 Do not change to "Discrete Graphics" with BIOS v1.15](#Do_not_change_to_"Discrete_Graphics"_with_BIOS_v1.15)
    *   [1.2 Firmware update](#Firmware_update)
    *   [1.3 Installation with hybrid graphics](#Installation_with_hybrid_graphics)
    *   [1.4 HiDPI screen](#HiDPI_screen)
*   [2 Graphics](#Graphics)
    *   [2.1 Discrete only](#Discrete_only)
        *   [2.1.1 Black screen after X starts with NVIDIA drivers](#Black_screen_after_X_starts_with_NVIDIA_drivers)
    *   [2.2 Hybrid graphics with Bumblebee](#Hybrid_graphics_with_Bumblebee)
    *   [2.3 Hybrid graphics with bbswitch only](#Hybrid_graphics_with_bbswitch_only)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 xbacklight not adjusting screen brightness](#xbacklight_not_adjusting_screen_brightness)
    *   [3.2 System hangs on startup/shutdown](#System_hangs_on_startup/shutdown)

## Installation

### Do not change to "Discrete Graphics" with BIOS v1.15

[https://www.reddit.com/r/thinkpad/comments/a2g0k4/warning_do_not_change_from_hybrid_graphics_to/](https://www.reddit.com/r/thinkpad/comments/a2g0k4/warning_do_not_change_from_hybrid_graphics_to/)

This might potentially brick your device and require Lenovo to replace your motherboard. Apparently verified on BIOS v1.15 and still not resolved.

You will want to use BIOS v1.18 or newer. BIOS v1.17 (released Dec 24, 2018) originally fixed the issue for the mass majority; however, this version has been removed due to additional bricking issues that happen occasionally related to the Hybrid graphics options when changed.

### Firmware update

Before installation, it is recommended that you boot into Windows 10 and use the preinstalled Lenovo Vantage software to install any necessary firmware updates, particularly [this one](https://pcsupport.lenovo.com/us/en/products/LAPTOPS-AND-NETBOOKS/THINKPAD-P-SERIES-LAPTOPS/THINKPAD-P1-TYPE-20MD-20ME/downloads/DS504958).

### Installation with hybrid graphics

Currently the live CD might not boot normally if your BIOS is configured to enable hybrid graphics. See [NVIDIA Optimus](/index.php/NVIDIA_Optimus "NVIDIA Optimus") for details. Two options are possible:

*   Disable hybrid graphics by changing your BIOS settings to "Discrete only" (Be careful, this might brick your latpop: [#Do not change to "Discrete Graphics" with BIOS v1.15](#Do_not_change_to_"Discrete_Graphics"_with_BIOS_v1.15))
*   Alternatively, before booting into live CD, press `e` and add `modprobe.blacklist=nouveau` to your kernel parameters.

If you choose to use the second option, you might also want to include `modprobe.blacklist=nouveau` in your `/boot/loader/entries/arch.conf`.

### HiDPI screen

Some configurations of ThinkPad P1 comes with a HiDPI screen. You may want to run `setfont latarcyrheb-sun32` to make your console font legible during installation.

To make this setting persistent after installation, create `/etc/vconsole.conf` with the following content:

 `/etc/vconsole.conf`  `FONT=latarcyrheb-sun32` 

See [HiDPI](/index.php/HiDPI "HiDPI") for more details.

## Graphics

There are two difficulties with configuring graphics on ThinkPad P1: there is no "integrated graphics only" option in the BIOS, and the external display ports (HDMI, etc.) are wired into the NVIDIA chip. Depending on your needs, you might choose from the following options:

### Discrete only

As the P1 is an hybrid device with both an integrated and discrete video card, the NVIDIA drivers have to be setup to use Optimus in order to properly work with external outputs and the integrated laptop screen. Setup NVIDIA Optimus as instructed in [NVIDIA Optimus#Using nvidia](/index.php/NVIDIA_Optimus#Using_nvidia "NVIDIA Optimus"). Note that this method will keep your NVIDIA graphics card always on, which might dramatically shorten your battery life.

#### Black screen after X starts with NVIDIA drivers

Even if using Optimus, the driver might anyway fail to detect the laptop screen using the auto-generated `xorg.conf` file and you might experience a black screen after X has been started. See [NVIDIA Optimus#No screens found on a laptop/NVIDIA Optimus](/index.php/NVIDIA_Optimus#No_screens_found_on_a_laptop/NVIDIA_Optimus "NVIDIA Optimus") for more details.

If you're able to connect an external monitor and verify it works, you can inspect the `xrandr -q` output to verify only HDMI and Display Port outputs are actually detected. The tool should as well display only external video output connections.

In order to instruct the driver about the integrated laptop screen, the `xorg.conf` file has to be modified to add a `"ConnectedMonitor" Option` to the `Section "Device"` (see [NVIDIA/Troubleshooting#Screen(s) found, but none have a usable configuration](/index.php/NVIDIA/Troubleshooting#Screen(s)_found,_but_none_have_a_usable_configuration "NVIDIA/Troubleshooting"))

Use the following as `xorg.conf` `Section "Device"`

```
  Section "Device"
      Identifier      "nvidia"
      Driver         "nvidia"
      VendorName     "NVIDIA Corporation"
      BusId          "1:0:0"
      Option         "AllowEmptyInitialConfiguration"
      Option	      "ConnectedMonitor" "eDP"
      Option	      "CustomEDID" "eDP:/sys/class/drm/card0-eDP-1/edid"
      Option	      "IgnoreEDID" "false"
      Option	      "UseEDID" "true" 
  EndSection

```

After re-starting X, the integrated screen output should show be now detected and properly usable.

If the laptop screen gets detected but `xrandr` fails to properly detect the available resolutions, remove the `HorizSync` and `Vertrefresh` options from `Section "Monitor"` and restart X

### Hybrid graphics with Bumblebee

See [Bumblebee](/index.php/Bumblebee "Bumblebee") for detailed instructions. If Xorg refuses to start after setting up Bumblebee, try generating an Xorg configuration by running `Xorg -configure` and copy it to `/etc/X11/xorg.conf`.

Because Bumblebee normally disables the NVIDIA card, display outputs such as HDMI might not show up in `xrandr -q`. You may want to refer to [Bumblebee's multi-monitor setup page](https://github.com/Bumblebee-Project/Bumblebee/wiki/Multi-monitor-setup).

### Hybrid graphics with bbswitch only

This method requires manual switching between integrated and discrete graphics mode. Switching between them requires restarting all Xorg instances, although it does not require a restart.

Install the appropriate [NVIDIA](/index.php/NVIDIA "NVIDIA") graphics drivers and [bbswitch](https://www.archlinux.org/packages/?name=bbswitch). Generate an Xorg configuration by running `Xorg -configure` and copy it to `/etc/X11/xorg.conf.intel`. You may also create `/etc/X11/xorg.conf.nvidia`, though it should not be necessary.

You can switch to discrete graphics with the following Bash function:

```
discrete() {
    killall Xorg
    modprobe nvidia_drm
    modprobe nvidia_modeset
    modprobe nvidia
    tee /proc/acpi/bbswitch <<<ON
    cp /etc/X11/xorg.conf.nvidia /etc/X11/xorg.conf
}

```

After this, `xrandr -q` should correctly show `HDMI-0` as one of the outputs. Running `xrandr --auto` will mirror the display on an external monitor. If you want to extend your display with a different DPI, adapt the following command to your needs:

```
$ xrandr --output HDMI-0 --scale 2x2 --right-of eDP-1-1

```

Conversely, you can switch to integrated graphics this way:

```
integrated() {
    killall Xorg
    rmmod nvidia_drm
    rmmod nvidia_modeset
    rmmod nvidia
    tee /proc/acpi/bbswitch <<<OFF
    cp /etc/X11/xorg.conf.intel /etc/X11/xorg.conf
}

```

You need to manually start your X session after switching.

If you are also running [TLP](/index.php/TLP "TLP"), to prevent TLP from blocking system startup or shutdown, you should tell it to leave NVIDIA card alone by uncommenting the following line:

 `/etc/default/tlp`  `RUNTIME_PM_DRIVER_BLACKLIST="amdgpu nouveau nvidia radeon"` 

You may also want to refer to [nvidia-xrun](/index.php/Nvidia-xrun "Nvidia-xrun"), which allows for running a separate X session with NVIDIA graphics.

## Troubleshooting

### xbacklight not adjusting screen brightness

Installing [light-git](https://aur.archlinux.org/packages/light-git/) should help.

### System hangs on startup/shutdown

If you are using hybrid graphics, ensure that your TLP is correctly blacklisting NVIDIA drivers by uncommenting this line:

 `/etc/default/tlp`  `RUNTIME_PM_DRIVER_BLACKLIST="amdgpu nouveau nvidia radeon"` 

Also make sure that the NVIDIA card is turned on before shutdown by running:

```
# modprobe nvidia

```

You can install systemd services to manage this automatically as as follows:

 `/etc/systemd/system/nvidia-enable-power-off.service` 
```
[Unit]
Description=Enable NVIDIA card at shutdown
DefaultDependencies=no

[Service]
Type=oneshot
ExecStart=/bin/sh -c "awk '{print $2}' /proc/acpi/bbswitch > /tmp/gpu_state && echo ON > /proc/acpi/bbswitch"
#ExecStart=/usr/bin/modprobe nvidia

[Install]
WantedBy=shutdown.target
WantedBy=reboot.target
WantedBy=hibernate.target
WantedBy=suspend-then-hibernate.target
WantedBy=sleep.target
WantedBy=suspend.target

```

And a service to disable the card again at resume if it was originally off:

 `/etc/systemd/system/nvidia-disable-resume.service` 
```
[Unit]
Description=Disable NVIDIA card at system resume
DefaultDependencies=no
After=sleep.target
After=suspend.target
After=suspend-then-hibernate.target
After=hibernate.target

[Service]
Type=oneshot
ExecStart=/bin/sh -c 'cat /tmp/gpu_state > /proc/acpi/bbswitch || echo OFF > /proc/acpi/bbswitch'
#ExecStart=/usr/bin/rmmod nvidia

[Install]
#WantedBy=shutdown.target
#WantedBy=reboot.target
WantedBy=sleep.target
WantedBy=suspend.target
WantedBy=suspend-then-hibernate.target
WantedBy=hibernate.target

```