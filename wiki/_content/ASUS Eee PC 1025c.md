# ASUS Eee PC 1025c

**Note:** This laptop uses a [Poulsbo](/index.php/Poulsbo "Poulsbo") GPU. Hardware acceleration is currently unsupported.

## Contents

*   [1 Bootloader](#Bootloader)
*   [2 Audio](#Audio)
    *   [2.1 Mono format](#Mono_format)
*   [3 HDMI](#HDMI)
    *   [3.1 Video](#Video)
    *   [3.2 Audio](#Audio_2)
        *   [3.2.1 Global](#Global)
        *   [3.2.2 User specific](#User_specific)
        *   [3.2.3 Dynamic](#Dynamic)
*   [4 Screen Brightness](#Screen_Brightness)

## Bootloader

Use i686 even if Intel ARK mentions support for Intel 64\. The Arch ISO will detect i686.

For BIOS legacy boot, create a [USB stick with dd](/index.php/USB_flash_installation_media#Using_dd "USB flash installation media"). Press F2 to go into the boot menu. Choose the entry for your USB stick that doesn't say "UEFI:". The BIOS gives an option for UEFI booting but the option seems to be broken.

## Audio

### Mono format

In case of missing voices, play all sounds in mono format. Using [ALSA](/index.php/ALSA "ALSA") add to `.asoundrc`:

 `~/.asoundrc` 

```
pcm.card0 {
  type hw
  card 0
}

ctl.card0 {
  type hw
  card 0
}

pcm.monocard {
  slave.pcm card0
  slave.channels 2
#  type plug
  type route
  ttable {
   # Copy both input channels to output channel 0 (Left). 
    0.0 1
    1.0 1
   # Send nothing to output channel 1 (Right). 
    0.1 0
    1.1 0
  }
}

ctl.monocard {
  type hw
  card 0
} 

pcm.!default monocard

```

Save and reload ALSA.

To set mono in a [PulseAudio](/index.php/PulseAudio "PulseAudio"), run:

```
 $ pacmd list-sinks | grep name | head -n1 

```

To get the master device name. The output of command will look like this:

```
 name: <alsa_output.pci-0000_00_1b.0.analog-stereo>

```

Put device name (in my case _alsa_output.pci-0000_00_1b.0.analog-stereo_) in field 'master' of the command below:

```
 $ pacmd load-module module-remap-sink sink_name=mono master=alsa_output.pci-0000_00_1b.0.analog-stereo channels=2 channel_map=front-right,mono

```

This only works if PulseAudio is running. To make this permanent, add the pacmd argument last to `/etc/pulse/default.pa`:

```
 # echo "load-module module-remap-sink sink_name=mono master=alsa_output.pci-0000_00_1b.0.analog-stereo channels=2 channel_map=front-right,mono" >> /etc/pulse/default.pa

```

## HDMI

### Video

You have to change the [video driver](/index.php/Poulsbo "Poulsbo"). If the HDMI cable is plugged in, it is enabled on boot. If plugged in after boot, use [xrandr](/index.php/Xrandr "Xrandr") to enable the second monitor:

```
# xrandr --output DVI-0 --auto

```

### Audio

You need to know the number of your sound card and the the HDMI device number:

 `aplay -l` 

```
Karte 0: Intel [HDA Intel], Gerät 0: ALC269VB Analog [ALC269VB Analog]
  Sub-Geräte: 1/1
  Sub-Gerät #0: subdevice #0
Karte 0: Intel [HDA Intel], Gerät 3: HDMI 0 [HDMI 0]
  Sub-Geräte: 1/1
  Sub-Gerät #0: subdevice #0

```

#### Global

In `/usr/share/alsa/alsa.conf` search the lines

```
default.pcm.card 0
default.pcm.device 0

```

If you change the numbers to your card and device (in my case card is 0 and device is 3) and reboot, the audio output switches to HDMI.

#### User specific

See [Advanced Linux Sound Architecture#HDMI Output Does Not Work](/index.php/Advanced_Linux_Sound_Architecture#HDMI_Output_Does_Not_Work "Advanced Linux Sound Architecture").

#### Dynamic

The audio device can also be configured with `/etc/asound.conf` So you can create a script that links asound.conf to a configuration depending on the hdmi cable plugged in or not: (for some reason my HDMI device is listed as DVI)

 `hdmi_switched.sh` 

```
#! /bin/bash
hdmi_status="$(cat /sys/class/drm/card0-DVI-D-1/status)"
ln -f "/etc/alsa/hdmi_$hdmi_status" /etc/alsa/asound.conf
alsactl restore

```

Configuration files:

 `hdmi_connected` 

```
pcm.!default {
      type hw
      card 0
      device 3 
}

```

 `hdmi_disconnected` 

```
pcm.!default {
      type hw
      card 0
      device 0 
}

```

Create a symbolic link to /etc/asound.conf

```
ln -s /etc/alsa/asound.conf /etc/asound.conf

```

If the user is allowed to run the hdmi_switch.sh script and is also allowed to change files in /etc/alsa folder you can bind that script to a key :D If you also want to change to monitor read [this](/index.php/Advanced_Linux_Sound_Architecture#Using_udev_to_automatically_turn_HDMI_audio_on_or_off "Advanced Linux Sound Architecture").

## Screen Brightness

The backlight directory is /sys/class/backlight/acpi_video0\. The display keys are now handled by the kernel.

Retrieved from "[https://wiki.archlinux.org/index.php?title=ASUS_Eee_PC_1025c&oldid=404324](https://wiki.archlinux.org/index.php?title=ASUS_Eee_PC_1025c&oldid=404324)"