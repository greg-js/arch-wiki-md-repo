LMMS is a free cross-platform software which allows you to produce music with your computer. This covers creating melodies and beats, synthesizing and mixing sounds and arranging samples. You can have fun with your MIDI keyboard and much more – all in a user-friendly and modern interface. Furthermore LMMS comes with many ready-to-use instrument and effect plugins, presets and samples.

## Installation

[lmms](https://www.archlinux.org/packages/?name=lmms) is in the offical Archlinux repository, but you may also need the git "master branch" version for the newest improvements.

You will need a [soundfont](/index.php/Timidity#SoundFonts "Timidity") and [Timidity](/index.php/Timidity "Timidity").

If you will use other audio apps like VLC during a single login, you will need a [usermode sound server](/index.php/Sound#Sound_servers "Sound")

Then, you will need to edit the FluidSynth configuration file as mentioned in the package’s [post-installation script](https://projects.archlinux.org/svntogit/packages.git/tree/trunk/fluidsynth.install?h=packages/fluidsynth). For the audio driver, choose the sound server that you installed.

[Start](/index.php/Start "Start") `fluidsynth.service`.

When LMMS starts, it will prompt you with the settings. Go to the audio settings, choose the same interface that you set for FluidSynth, and restart LMMS if you made a switch.