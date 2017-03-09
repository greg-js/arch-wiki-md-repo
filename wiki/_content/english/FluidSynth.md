[FluidSynth](http://www.fluidsynth.org/) is a real-time software synthesizer based on the SoundFont 2 specifications. It is required by [gst-plugins-bad](https://www.archlinux.org/packages/?name=gst-plugins-bad), and thus is installed as a dependency of the [gnome](https://www.archlinux.org/groups/x86_64/gnome/) group.

## Contents

*   [1 Installing FluidSynth](#Installing_FluidSynth)
*   [2 How to use FluidSynth](#How_to_use_FluidSynth)
    *   [2.1 Standalone mode](#Standalone_mode)
    *   [2.2 ALSA daemon mode](#ALSA_daemon_mode)
*   [3 How to convert MIDI to MP3/OGG](#How_to_convert_MIDI_to_MP3.2FOGG)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Conflicting with PulseAudio](#Conflicting_with_PulseAudio)

## Installing FluidSynth

The first step is to [install](/index.php/Install "Install") the [fluidsynth](https://www.archlinux.org/packages/?name=fluidsynth) package.

**However, FluidSynth will not produce any sound yet**. This is because FluidSynth does not include any instrument samples. To produce sound, instrument patches and/or soundfonts need to be installed and fluidsynth configured so it knows where to find them. You can install [SoundFont sample](/index.php/Timidity#SoundFonts "Timidity").

## How to use FluidSynth

There are two ways to use FluidSynth. Either as MIDI player or as daemon adding MIDI support to ALSA.

### Standalone mode

You can simply use fluidsynth to play MIDI files:

```
$ fluidsynth -a alsa -m alsa_seq -l -i /usr/share/soundfonts/FluidR3_GM.sf2 example.midi

```

assuming than you installed [soundfont-fluid](https://www.archlinux.org/packages/?name=soundfont-fluid).

There are many other options to fluidsynth; see manpage or use -h to get help.

One may wish to use pulseaudio instead of alsa as the argument to the -a option.

### ALSA daemon mode

If you want fluidsynth to run as ALSA daemon, edit `/etc/conf.d/fluidsynth` and add your soundfont along with any other changes you would like to make. For e.g., fluidr3:

```
SOUND_FONT=/usr/share/soundfonts/FluidR3_GM.sf2
AUDIO_DRIVER=alsa
OTHER_OPTS='-is -m alsa_seq -r 48000'

```

After that, you can [start/enable](/index.php/Start/enable "Start/enable") the fluidsynth service. Be aware of bug [https://bugs.archlinux.org/task/50122](https://bugs.archlinux.org/task/50122) when using pulseaudio driver

The following will give you an output software MIDI port (in addition of hardware MIDI ports on your system, if any):

 `$ aconnect -o` 
```
client 128: 'FLUID Synth (5117)' [type=user]
   0 'Synth input port (5117:0)'
```

An example of usage for this is aplaymidi:

```
$ aplaymidi -p128:0 example.midi

```

## How to convert MIDI to MP3/OGG

Requires [soundfont-fluid](https://www.archlinux.org/packages/?sort=&q=soundfont-fluid&maintainer=&flagged=) or any other soundfont of your choice.

/usr/share/soundfonts is the default location of FluidR3_GM

Simple command lines to convert midi to mp3:

```
$ fluidsynth -l -T raw -F /usr/share/soundfonts/FluidR3_GM.sf2 example.mid | twolame -b 256 -r example.mp3 

```

Requires [twolame](https://www.archlinux.org/packages/?sort=&q=twolame&maintainer=&flagged=)

Simple command lines to convert midi to ogg:

```
$ fluidsynth -nli -r 48000 -o synth.cpu-cores=2 -T oga -F example.ogg /usr/share/soundfonts/FluidR3_GM.sf2 example.MID

```

Here's a little script to convert multiple midi files to ogg in parallel:

```
#!/bin/bash
maxjobs=$(grep processor /proc/cpuinfo | wc -l)
midi2ogg() {
	name=$(echo $@ | sed -r s/[.][mM][iI][dD][iI]?$//g | sed s/^[.][/]//g)
	for arg; do 
	fluidsynth -nli -r 48000 -o synth.cpu-cores=$maxjobs -F "/dev/shm/$name.raw" /usr/share/soundfonts/FluidR3_GM.sf2 "$@"
	oggenc -r -B 16 -C 2 -R 48000 "/dev/shm/$name.raw" -o "$name.ogg"
	rm "/dev/shm/$name.raw"
	## Uncomment for replaygain tagging
	#vorbisgain -f "$name.ogg" 
	done
}
export -f midi2ogg
find . -regex '.*[.][mM][iI][dD][iI]?$' -print0 | xargs -0 -n 1 -P $maxjobs bash -c 'midi2ogg "$@"' --

```

## Troubleshooting

### Conflicting with PulseAudio

If your *fluidsynth* application is set to use alsa as driver, the sound card will be accessed directly and pulseaudio and applications using pulseaudio will not be able to work properly. You can modify the configuration file `/etc/conf.d/fluidsynth` and change the driver to PulseAudio, then restart *fluidsynth* and PulseAudio:

 `/etc/conf.d/fluidsynth` 
```
AUDIO_DRIVER=pulseaudio
OTHER_OPTS='-m alsa_seq -r 48000'
```