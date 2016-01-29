# ASUS N53JN

| **Device** | **Status** | **Modules** |
| Intel | **Working** | xf86-video-intel |
| Nvidia | **Partially Working** | bumblebee |
| Ethernet | **Working** | atl1c |
| Wireless | **Working** | ath9k |
| Audio | **Working** | snd_hda_intel |
| Touchpad | **Working** |
| Camera | **Working** | uvcvideo |
| USB 3.0 | **Working** | xhci_hcd |
| eSATA | **Working** |
| Card Reader | **Working** |
| Function Keys | **Working** |
| Suspend | **Working, look bellow** |

## Contents

*   [1 Hardware](#Hardware)
*   [2 Configuration](#Configuration)
    *   [2.1 CPU](#CPU)
    *   [2.2 Video](#Video)
        *   [2.2.1 Intel](#Intel)
        *   [2.2.2 Nvidia](#Nvidia)
            *   [2.2.2.1 Switching graphic cards](#Switching_graphic_cards)
    *   [2.3 Audio](#Audio)
    *   [2.4 Touchpad](#Touchpad)
    *   [2.5 Webcam](#Webcam)
    *   [2.6 Suspend](#Suspend)

## Hardware

_CPU:_ Intel Core i5 450M, 2.4GHz

_Mainboard:_ Intel HM55

_RAM:_ 4096 MB, 2x 2048 MByte DDR3

_Display:_ 15,6" HD LED (1366x768)

_Graphics adapter:_ NVIDIA GeForce GT 335M - 1024 MB and Intel Core Processor Integrated Graphics Controller

_Soundcard:_ integrated Intel HDA

_Network:_ Atheros Gigabit Ethernet Controller, Atheros AR9285 Wireless Network

_Hard disk:_ Seagate Momentus 500GB 5400rpm SATA

_Webcam:_ IMC Networks

_Touchpad:_ Elantech

## Configuration

### CPU

Works out of the box.

Follow the [CPU frequency scaling](/index.php/CPU_frequency_scaling "CPU frequency scaling") guide to enable speed-stepping. Processor has Intel Turbo Boost which works out of the box, but you can't see the frequncies above 2.4GHz in /proc/cpuinfo. To see the actual frequency use [i7z](https://www.archlinux.org/packages/?name=i7z).

### Video

#### Intel

Follow these guides: [Xorg](/index.php/Xorg "Xorg") and [Intel](/index.php/Intel "Intel")

No problems detected. VGA out and HDMI working.

#### Nvidia

The official proprietary nvidia drivers for linux do not support Nvidia Optimus yet, but there is a workaround in the form of [bumblebee](https://www.archlinux.org/packages/?name=bumblebee). It enables the use of Nvidia graphic card via virtualgl. Just follow the instructions for setting up [bumblebee](/index.php/Bumblebee "Bumblebee") in our wiki. Please note that this laptop has software switch that turns Nvidia graphics card off. You can turn it on using [acpi_call](https://www.archlinux.org/packages/?name=acpi_call).

##### Switching graphic cards

Look at [ASUS N82JV](/index.php/ASUS_N82JV "ASUS N82JV") page.

### Audio

Follow the official documentation: [ALSA](/index.php/ALSA "ALSA") and [PulseAudio](/index.php/PulseAudio "PulseAudio")

In order to make integrated speakers work add to `/etc/modprobe.d/modprobe.conf`:

```
options snd-hda-intel index=0 model=auto

```

And to `/etc/modprobe.d/sound.conf` add:

```
alias snd-card-0 snd-hda-intel
alias sound-slot-0 snd-hda-intel
```

### Touchpad

Follow the [Synaptics](/index.php/Synaptics "Synaptics") guide.

### Webcam

Working, but the picture is refreshing slowly.

### Suspend

The USB unbind hook is no longer necessary as of [Linux 3.5](http://git.kernel.org/?p=linux/kernel/git/torvalds/linux.git;a=commitdiff;h=dbf0e4c7257f8d684ec1a3c919853464293de66e).

The laptop still hangs if you disable nVidia GPU and try to suspend! However, a workaround that works with [ASUS N82JV](/index.php/ASUS_N82JV "ASUS N82JV") consists in blacklisting nouveau. That still allows the user to power the card off in that laptop.

Retrieved from "[https://wiki.archlinux.org/index.php?title=ASUS_N53JN&oldid=328607](https://wiki.archlinux.org/index.php?title=ASUS_N53JN&oldid=328607)"