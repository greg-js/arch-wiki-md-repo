[LMMS](https://lmms.io/) is a free cross-platform software which allows you to produce music with your computer. This covers creating melodies and beats, synthesizing and mixing sounds and arranging samples. You can have fun with your MIDI keyboard and much more – all in a user-friendly and modern interface. Furthermore LMMS comes with many ready-to-use instrument and effect plugins, presets and samples.

## Installation

[lmms](https://www.archlinux.org/packages/?name=lmms) is in the offical Archlinux repository. Alternatively, because LMMS has seen many changes since the stable release at time of writing, you may want [lmms-git](https://aur.archlinux.org/packages/lmms-git/) for the latest in upstream development, or [lmms-beta-bin](https://aur.archlinux.org/packages/lmms-beta-bin/) for a pre-compiled pre-release version. See [[1]](https://github.com/LMMS/lmms/releases) for release notes.

As always, if you want to use multiple audio applications simultaneously but your hardware does not natively support this, you will need either a [usermode sound server](/index.php/Sound#Sound_servers "Sound"), or to configure ALSA [dmix](/index.php/Alsa#Dmix "Alsa").

## MIDI and soundfonts

Depending on your setup and the installation method, you might need to manually setup a [soundfont](/index.php/Timidity#SoundFonts "Timidity") and [Timidity](/index.php/Timidity "Timidity").

Then, you will need to edit the FluidSynth configuration file as mentioned in the package’s [post-installation script](https://projects.archlinux.org/svntogit/packages.git/tree/trunk/fluidsynth.install?h=packages/fluidsynth). For the audio driver, choose the sound server that you installed.

[Start](/index.php/Start "Start") `fluidsynth.service`.

When LMMS starts, it will prompt you with the settings. Go to the audio settings, choose the same interface that you set for FluidSynth, and restart LMMS if you made a switch.