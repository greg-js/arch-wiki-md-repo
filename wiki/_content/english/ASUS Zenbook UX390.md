## Volume increments don't work

Because of the "surrond sound" audio hardware on the UX390, you have to tweak a Pulse configuration file to get volume incrementing to work. Otherwise, the volume will either be full or muted, despite appearing to increment.

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