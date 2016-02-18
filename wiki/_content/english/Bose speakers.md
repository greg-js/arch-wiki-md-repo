In order to get [ALSA](/index.php/ALSA "ALSA") to work with your Bose speakers (after you have properly configured ALSA):

The trick is to set a new default device for ALSA.

First, run

```
$ cat /proc/asound/cards

```

My sample result:

```
0 [Intel          ]: HDA-Intel - HDA Intel  HDA Intel at 0xfdff8000 irq 16
1 [Audio          ]: USB-Audio - Bose USB Audio Bose Corporation Bose USB Audio at  usb-0000:00:1d.2-2, full speed

```

Look at /usr/share/alsa/alsa.conf and the find parameters you need to edit.

```
# defaults
defaults.ctl.card 0
defaults.pcm.card 0

```

Change the default number on both values to the number that corresponds with your card. In my case, this is 1.

Then, select the device in *System > Preferences > Sound* (for Gnome) and change Alsa mixer volume settings.