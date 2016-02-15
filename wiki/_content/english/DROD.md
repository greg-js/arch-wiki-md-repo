[DROD](http://caravelgames.com/Articles/Games.html) is a series of puzzle games with native Linux support.

## Sound problems

```
# pacman -S lib32-alsa-plugins lib32-alsa-oss sdl_mixer
# modprobe snd_mixer_oss
# modprobe snd_pcm_oss
# modprobe snd_seq_oss

```