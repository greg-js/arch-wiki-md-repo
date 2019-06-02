[FluidSynth](http://www.fluidsynth.org/) is a real-time software synthesizer based on the SoundFont 2 specifications. It is optionally used by [gst-plugins-bad](https://www.archlinux.org/packages/?name=gst-plugins-bad).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 Standalone mode](#Standalone_mode)
    *   [2.2 ALSA daemon mode](#ALSA_daemon_mode)
    *   [2.3 SDL_Mixer](#SDL_Mixer)
*   [3 How to convert MIDI to MP3/OGG](#How_to_convert_MIDI_to_MP3/OGG)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Conflicting with PulseAudio](#Conflicting_with_PulseAudio)

## Installation

The first step is to [install](/index.php/Install "Install") the [fluidsynth](https://www.archlinux.org/packages/?name=fluidsynth) package.

You should also install a [SoundFont](https://en.wikipedia.org/wiki/SoundFont "wikipedia:SoundFont") to be able to produce sound. Here is a list of SoundFonts:

*   [freepats-general-midi](https://www.archlinux.org/packages/?name=freepats-general-midi)
*   [soundfont-fluid](https://www.archlinux.org/packages/?name=soundfont-fluid)

## Usage

There are two ways to use FluidSynth. Either as [MIDI](/index.php/MIDI "MIDI") player or as daemon adding MIDI support to [ALSA](/index.php/ALSA "ALSA").

### Standalone mode

You can simply use fluidsynth to play MIDI files:

```
$ fluidsynth -a alsa -m alsa_seq -l -i /usr/share/soundfonts/FluidR3_GM.sf2 example.midi

```

assuming than you installed [soundfont-fluid](https://www.archlinux.org/packages/?name=soundfont-fluid).

There are many other options to fluidsynth; see manpage or use -h to get help.

One may wish to use pulseaudio instead of alsa as the argument to the -a option.

**Tip:** The soundfont does not needed to be specified every time if a symbolic link created for the default soundfont, e.g. `ln -s FluidR3_GM.sf2 /usr/share/soundfonts/default.sf2` 

### ALSA daemon mode

If you want fluidsynth to run as ALSA daemon, edit `/etc/conf.d/fluidsynth` and add your soundfont along with any other changes you would like to make. For e.g., fluidr3:

```
SOUND_FONT=/usr/share/soundfonts/FluidR3_GM.sf2
OTHER_OPTS='-a alsa -m alsa_seq -r 48000'

```

After that, you can [start/enable](/index.php/Start/enable "Start/enable") the fluidsynth service. Note that you can't use root to restart the fluidsynth service, if you're using the pulseaudio driver. Pulseaudio won't allow root to connect, since the pulseaudio server is usually started by the user (and not root). You can solve it by creating a [systemd/User](/index.php/Systemd/User "Systemd/User") service (replacing `multi-user.target` with `default.target` in the copied `fluidsynth.service`).

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

### SDL_Mixer

To use fluidsynth with programs that use SDL_Mixer, you need to specify the soundfont as:

```
 $ SDL_SOUNDFONTS=/usr/share/soundfonts/FluidR3_GM.sf2 ./program

```

## How to convert MIDI to MP3/OGG

Requires [soundfont-fluid](https://www.archlinux.org/packages/?name=soundfont-fluid) or any other soundfont of your choice.

`/usr/share/soundfonts` is the default location of FluidR3_GM

Simple command lines to convert midi to mp3:

```
$ fluidsynth -l -T raw -F - /usr/share/soundfonts/FluidR3_GM.sf2 example.mid | twolame -b 256 -r - example.mp3 

```

Requires [twolame](https://www.archlinux.org/packages/?name=twolame).

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

 `/etc/conf.d/fluidsynth`  `OTHER_OPTS='-a pulseaudio -m alsa_seq -r 48000'`