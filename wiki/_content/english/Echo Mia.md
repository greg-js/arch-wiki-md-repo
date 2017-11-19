This article will discuss how to setting up the Echo Mia (Midi) soundcard to work under Arch, and how to resolve the hardware mixing issue in ALSA. It also implies that [ALSA](/index.php/ALSA "ALSA") is set up properly. Proper software mixing is found to be possible with dmix with a slightly tweaked `~/.asoundrc`.

## Installation

The Arch kernel includes the Mia modules necessary, however the firmware needs to be obtained by installing the [alsa-firmware](https://www.archlinux.org/packages/?name=alsa-firmware) package. After the firmware is installed, you should consider [blacklisting](/index.php/Blacklisting "Blacklisting") other sound card modules.

Reboot again, confirm that the module is loaded, and is able to play sound.

The *echomixer* program should be installed from the [alsa-tools](https://www.archlinux.org/packages/?name=alsa-tools) package. *echomixer* makes it easier to set up and manage the virtual channels (subdevices) of your soundcard.

## Hardware mixing

When the card is set up, and plays sound correctly, the last part is tricking to make the hardware mixing work as it should. If hardware mixing is already working properly, the last part of this page should be of no interest. However, if the sound card is unable to have more than one stream at the same time, this fix should work around it.

As suspected in this forum thread [[1]](https://bbs.archlinux.org/viewtopic.php?id=36508), Mia is unable to let ALSA pick a free subdevice for the sound card. A stereo stream is considered as two streams for Mia, but ALSA thinks this as one stream, leading to the crash that it will pick a busy subdevice each time it tries to play another stream. To work around this, we have to force ALSA to pick other subdevices. We can do this by splitting the card into four different devices. Example of `/etc/asound.conf`:

```
# /etc/asound.conf
# Hardware mixing for Mia
pcm.!default{
  type hw
  card 0
  subdevice 0
}
ctl.!default{
  type hw
  card 0
}
pcm.mia1{
  type hw
  card 0
  subdevice 2
}
pcm.mia2{
  type hw
  card 0
  subdevice 4
}
pcm.mia3{
  type hw
  card 0
  subdevice 6
}

```

As long as we have programs that are able to pick different devices for ALSA, we can route certain programs to certain devices. For programs that only use the default device, it will be defaulted to use subdevice 0 (and 1). Many popular programs are able to pick devices for themselves. A normal setup of flashplayer in web browser, movie player and a music player can be designated their own devices, which also allows separate volume control of these. Refer to each programs manuals on how to configure these properly.

The dmix alternative if hardware mixing becomes too much of a mess can work with this setup (assumes that MIA is card #0\. YMMV):

```
pcm.!default {
  type plug
  slave.pcm "dmixer"
}
pcm.dmixer {
  type dmix
  ipc_key 2048
  slave {
    pcm "hw:0,0,0" # Changing the "obvious" hw:0,0 to hw:0,0,0 saves the day ...
    period_time 0
    period_size 1024
    buffer_size 4096
    rate 44100
  }
  bindings {
    0 0
    1 1
  }
}
ctl.!default {
  type hw
  card 0
}

```