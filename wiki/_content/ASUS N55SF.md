# ASUS N55SF

| **Device** | **Status** | **Modules** |
| Intel graphics | **Working** | xf86-video-intel |
| Nvidia graphics | **Working, see below** | nvidia, bumblebee |
| Graphic outputs | **Not working** | nvidia, bumblebee |
| Ethernet | **Working** | atl1c |
| Wireless | **Working** | iwlan |
| Audio | **Working, see below** | snd_hda_intel |
| Touchpad | **Working** | xf86-input-synaptics |
| Camera | **Working** | uvcvideo |
| USB 3.0 | **Working** | xhci_hcd |
| Card Reader | **Working** |
| Special Keys | **Untested** |
| Power management | **Working, see below** |

## Contents

*   [1 Hardware](#Hardware)
*   [2 Configuration](#Configuration)
    *   [2.1 CPU](#CPU)
    *   [2.2 Video](#Video)
        *   [2.2.1 Intel](#Intel)
        *   [2.2.2 Nvidia](#Nvidia)
        *   [2.2.3 Outputs](#Outputs)
    *   [2.3 Audio](#Audio)
        *   [2.3.1 Subwoofer](#Subwoofer)
            *   [2.3.1.1 Pulseaudio](#Pulseaudio)
            *   [2.3.1.2 Alsa](#Alsa)
    *   [2.4 Backlight](#Backlight)
    *   [2.5 Touchpad](#Touchpad)
    *   [2.6 Webcam](#Webcam)
    *   [2.7 Bluetooth](#Bluetooth)
    *   [2.8 Power management](#Power_management)

## Hardware

_CPU:_ Intel Core i7-2630QM @ 2.00GHz

_Mainboard:_ Intel HM65 Express

_RAM:_ 6/8GB DDR3

_Display:_ 15,6" HD LED (1920x1080)

_Graphics adapter:_ Intel Core Processor Integrated Graphics Controller, NVIDIA GeForce GT 555M

_Soundcard:_ Integrated Intel HDA, Bang & Olufsen speakers with external subwoofer

_Network:_ Atheros Gigabit Ethernet Controller, Intel Centrino Wireless-N 1030

_Hard disk:_ Seagate Momentus 750GB 5400rpm SATA

_Webcam:_ IMC Networks

_Touchpad:_ Synaptics

## Configuration

There is a BIOS update (v207) on Asus support website (go to the english one if you don't find) that fix the numpad bug.

### CPU

Works out of the box.

Follow the [CPU frequency scaling](/index.php/CPU_frequency_scaling "CPU frequency scaling") guide to enable speed-stepping. Processor has Intel Turbo Boost which works out of the box, but you can't see the frequencies above 2.4GHz in `/proc/cpuinfo`. To see the actual frequency [install](/index.php/Install "Install") [i7z](https://www.archlinux.org/packages/?name=i7z).

### Video

#### Intel

Follow these guides: [Xorg](/index.php/Xorg "Xorg") and [Intel](/index.php/Intel "Intel"). You will need to blacklist the nouveau driver (the kernel detects the nvidia card and loads it). Bumblebee will load it as needed, see next section.

 `/etc/modprobe.d/blacklist-nouveau.conf`  `blacklist nouveau` 

#### Nvidia

The official proprietary nvidia drivers for linux do not support Nvidia Optimus yet, but there is a workaround in the form of [bumblebee](https://www.archlinux.org/packages/?name=bumblebee). It enables the use of Nvidia graphic card via virtualgl. Just follow the instructions for setting up [bumblebee](/index.php/Bumblebee "Bumblebee") in our wiki.

#### Outputs

VGA out works fine out of the box. Since the NVIDIA chip is wired to the HDMI out, you can get this working using Bumblebee with xf86-video-intel-virtual-crtc and hybrid-screenclone. See [Bumblebee FAQ](https://github.com/Bumblebee-Project/Bumblebee/wiki/FAQ).

### Audio

Follow the official documentation: [ALSA](/index.php/ALSA "ALSA") or/and [PulseAudio](/index.php/PulseAudio "PulseAudio")

##### Subwoofer

###### Pulseaudio

We need pulseaudio profile which will use surround21 alsa device.

 `/usr/share/pulseaudio/alsa-mixer/profile-sets/default.conf` 

```
...
[Mapping analog-surround-21]
device-strings = surround21:%f
channel-map = front-left,front-right,lfe
paths-output = analog-output analog-output-lineout analog-output-speaker analog-output-desktop-speaker
priority = 10
direction = output
...

```

Lfe remixing must be enabled for remixing third channel.

 `~/.config/pulse/daemon.conf` 

```
enable-lfe-remixing = yes

```

To prevent volume changing of PCM set volume to ignore in:

 `/usr/share/pulseaudio/alsa-mixer/paths/analog-output.conf.common` 

```
[Element PCM]
switch = on
volume = ignore
override-map.1 = all
override-map.2 = all-left,all-right

```

Install [blop](https://www.archlinux.org/packages/?name=blop),[cmt](https://www.archlinux.org/packages/?name=cmt) and [ladspa](https://www.archlinux.org/packages/?name=ladspa) and append these lines to your default.pa if you want to configure subwoofer on every pulseaudio daemon start:

**Note:** Before using this configuration you should change `alsa_output.pci-0000_00_1b.0.analog-stereo-21` to your own name of sink(you can find names of your sinks in pulseaudio with command `$ pactl list sinks` ).

 `~/.config/pulse/default.pa` 

```
load-module module-ladspa-sink  sink_name=ladspa_low_pass master=alsa_output.pci-0000_00_1b.0.analog-stereo-21 plugin=lp4pole_1671 label=lp4pole_fcrcia_oa control=200,0
load-module module-remap-sink   sink_name=remapLFE        master=ladspa_low_pass                               remix=no   channels=1 master_channel_map=lfe                    channel_map=lfe
load-module module-remap-sink   sink_name=remap20         master=alsa_output.pci-0000_00_1b.0.analog-stereo-21 remix=no   channels=2 master_channel_map=front-left,front-right channel_map=front-left,front-right
load-module module-combine-sink sink_name=combine         slaves=remap20,remapLFE                                         channels=3                                           channel_map=front-left,front-right,lfe
set-default-sink combine

```

Commands to control volume:

```
pactl set-sink-volume 0 +10%
pactl set-sink-volume 0 -- -10%
pactl set-sink-mute 0 toggle

```

**Note:** When we compare pulseaudio and alsa low pass filter configuration we find out that subwoofer is less heard, it is because pulseaudio use own remixing method which sends to subwoofer half of left and right channel.

###### Alsa

External subwoofer + low pass filter configuration. Configuration uses [blop](https://www.archlinux.org/packages/?name=blop),[cmt](https://www.archlinux.org/packages/?name=cmt) and [ladspa](https://www.archlinux.org/packages/?name=ladspa).

 `/etc/asound.conf` 

```
# upmix 2channels to 3, one for LFE
pcm.upmix2021 {
    type plug
    slave.pcm lowpass2121
    slave.channels 3
    ttable {
        0.0    1
        1.1    1
        0.2    1
        1.2    1
    }
}

# low pass filter for LFE channel
pcm.lowpass2121 {
    type ladspa
    slave.pcm upmix2121
    path "/usr/lib/ladspa"
    channels 3
    plugins {       
        0 {
            id 1672 # 4 Pole Low-Pass Filter with Resonance (FCRCIA) (1672/lp4pole_fcrcia_oa)
            policy none
            input.bindings.2 "Input";
            output.bindings.2 "Output";
            input { controls [ 200 0 ] }
        }
        1 {
            id 1098
            policy duplicate
            input.bindings.0 "Input";
            output.bindings.0 "Output";        
        }         
    }
}

pcm.upmix2121 {
    type plug
    slave.pcm surround21
    slave.channels 3
    ttable {
        0.0 1
        1.1 1
        2.2 1
    }
}

pcm.!default upmix2021

```

### Backlight

Follow [Backlight](/index.php/Backlight "Backlight") wiki page and use `acpi_backlight=vendor acpi_osi=Linux` as kernel parameter in your [bootloader](/index.php/Bootloader "Bootloader").

### Touchpad

Follow the [Synaptics](/index.php/Synaptics "Synaptics") guide.

### Webcam

Working.

### Bluetooth

Should be working out of the box - just remember to install [bluez-firmware](https://www.archlinux.org/packages/?name=bluez-firmware).

### Power management

The USB unbind hook is no longer necessary as of [Linux 3.5](http://git.kernel.org/?p=linux/kernel/git/torvalds/linux.git;a=commitdiff;h=dbf0e4c7257f8d684ec1a3c919853464293de66e).

Retrieved from "[https://wiki.archlinux.org/index.php?title=ASUS_N55SF&oldid=412029](https://wiki.archlinux.org/index.php?title=ASUS_N55SF&oldid=412029)"