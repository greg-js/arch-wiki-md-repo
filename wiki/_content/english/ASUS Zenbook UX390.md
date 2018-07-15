## Volume increments don't work

Because of the "surround sound" audio hardware on the UX390, you have to tweak a Pulse configuration file to get volume incrementing to work. Otherwise, the volume will either be full or muted, despite appearing to increment.

Edit the analog output path config and add the `Element Master` and `Element LFE` parts below.

 `/usr/share/pulseaudio/alsa-mixer/paths/analog-output.conf.common` 
```
[Element Master]
switch = mute
volume = ignore

[Element PCM]
switch = mute
volume = merge
override-map.1 = all
override-map.2 = all-left,all-right

[Element LFE]
switch = mute
volume = ignore
```

Then, restart PulseAudio and changing the volume should work.

## Headphone jack audio is always muted

Install [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils). Run `alsamixer`, select the "HDA Intel PCH" soud card, and adjust the "Headphone" slider to your liking. To make this persistent you may need to run `sudo alsactl store`.