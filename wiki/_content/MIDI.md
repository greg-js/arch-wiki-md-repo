# MIDI

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

MIDI itself, which stands for "Musical Instrument Digital Interface", is just a protocol and standard for communication between musical instruments and any device that understands the language. It can be used to control an array of synthesizers, make a tin can sound like a drum, or even operate industrial equipments.

The scope of this article, however, will mainly focus on the usage of MIDI in computer systems for playback of files that contain MIDI data. These files usually come with the **.mid** extension, and were hugely popular in the golden days of multimedia computing to share music. In professional music composition/arrangement, it still plays a vital role.

## Contents

*   [1 MIDI File](#MIDI_File)
*   [2 GM Bank](#GM_Bank)
*   [3 Playback](#Playback)
    *   [3.1 Hardware](#Hardware)
        *   [3.1.1 SB Audigy 1 - Emu10k1 WaveTable](#SB_Audigy_1_-_Emu10k1_WaveTable)
    *   [3.2 Software](#Software)
        *   [3.2.1 GStreamer-based players like Totem (GNOME Videos) or Rhythmbox](#GStreamer-based_players_like_Totem_.28GNOME_Videos.29_or_Rhythmbox)
        *   [3.2.2 VLC](#VLC)
        *   [3.2.3 Audacious](#Audacious)
        *   [3.2.4 TiMidity++](#TiMidity.2B.2B)
        *   [3.2.5 FluidSynth](#FluidSynth)

## MIDI File

Without going into the details of what the format is composed of, you just need to understand that a MIDI file eg. **foobar.mid** does not contain any digital audio data, hence no "PCM stream". It is a common misconception that MIDI is a sound file format, and as such you usually see people complaining that music players like Amarok cannot play the file. Here is a very newbie-friendly outline of what a MIDI/MID file contains:

```
**# FOOBAR.MID**
Note ON
  _Use Instrument #1_
  _Play Note C1_
  _Set Volume at 100_
  _Set Pitch at 50_

```

In order for such a file to be useful, there needs to be an "engine" that can translate the data to music. This engine will have a "tone generator", and this is what we call a "synthesizer". So any player that can play back a MIDI file without MIDI-capable hardware (your computer's sound device), has a synthesizer built-in or uses an external one. A typical keyboard (not the thing you are typing on) is actually made up of two components - a MIDI "controller" (the keys) and a synthesizer (tone generator/module; the thing that makes sound).

So up to this point, you should be able to understand that:

*   There needs to be a synthesizer to play a MIDI file.
*   A synthesizer can be hardware or software.
*   Most computer soundcards/chipsets do NOT have synthesizers.
*   You need a synthesizer with a proper "bank" (collection of sounds) to be able to enjoy all the glory of MIDI files.
*   If a certain instrument is not in the bank, your synthesizer will not play anything for notes using that instrument.
*   If a certain instrument in the file corresponds to a different one in the bank, your synthesizer will play a different sound (obviously).

## GM Bank

General MIDI (GM) is a specification to standardise numerous MIDI-related matters, particularly that of instruments layout in a collection of sounds. A "soundbank" which is GM-compatible means that it meets the criteria of General MIDI, and as long as the MIDI file is also GM-compatible (as in nothing extraordinary is defined - such as introducing a new instrument or having one in a different location of the bank), the playback will be as intended since the bank has the correct instrument/handler for the MIDI message/event. One of the most popular soundbank formats is that of **SoundFont**, particularly _SF2_.

*   If you have a soundcard which can make use of soundfonts, you can load a **.sf2** file onto it.

*   If you do not have a soundcard which can make use of soundfonts (basically no hardware synthesizer), you can use a software synthesizer and load the SF2 file. In turn, you can find some way to globally make use of this synthesizer.

## Playback

"Why can I play MIDI with Windows Media Player, then?"

Well, because Windows has a default software synthesizer which acts globally. Even then, it lacks the quality which should be expected of modern computers. If there were a way to do it on Linux, you would be able to play back MIDI from any player too. Perhaps a MIDI server (which will hold a synthesizer of choice like [timidity++](https://www.archlinux.org/packages/?name=timidity%2B%2B) or [fluidsynth](https://www.archlinux.org/packages/?name=fluidsynth)) that sits within the sound server, like Phonon or PulseAudio. Nevertheless, nothing of this sort has been implemented and you can only play MIDI with a player that has a plug-in to source a synthesizer (for example [xmms](https://aur.archlinux.org/packages/xmms/)<sup><small>AUR</small></sup> or [audacious](https://www.archlinux.org/packages/?name=audacious)) or has a synthesizer itself.

### Hardware

_(More details on soundcards and MIDI, possibly links to SBLive MIDI here...)_

If you simply need to play a MIDI file on a MIDI-capable hardware device (e.g. a hardware synthesizer), you can use the `aplaymidi` command. To get the list of the available MIDI ports use the command

```
$ aplaymidi -l

```

Then to play a MIDI file specify it along with an available port of the preferred MIDI device that you got from the output of the previous command, for example like this:

```
$ aplaymidi -p 24:0 midi_file.mid

```

#### SB Audigy 1 - Emu10k1 WaveTable

First, make sure that the **Synth** mixer control is not muted and that **Audigy Analog/Digital output Jack** is set to **[Off]**.

To check and adjust them, use `alsamixer` or your mixer of choice.

Next, build and install the [awesfx](https://aur.archlinux.org/packages/awesfx/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/awesfx)]</sup> package from the [AUR](/index.php/AUR "AUR"). Then, load a SoundFont file on the Emux WaveTable, like so:

```
$ asfxload /path/to/any/file.sf2

```

The .SF2 file can be any SoundFont. If you have access to _2GMGSMT.SF2_ on Windows, you can use that one.

You should be all set now. If you want to play your .mid files in [Audacious](/index.php/Audacious "Audacious"), you will need to configure it as follows:

*   _File > Preferences > Plugins > Input > AMIDI-Plug > Preferences_
    *   _AMIDI PLug (tab) > Backend selection > ALSA Backend_
    *   ALSA Backend (tab)
        *   17:0 Emu10k1 WaveTable Emu10k1 Port 0
        *   17:1 Emu10k1 WaveTable Emu10k1 Port 1
        *   17:2 Emu10k1 WaveTable Emu10k1 Port 2
        *   17:3 Emu10k1 WaveTable Emu10k1 Port 3
        *   _Mixer settings > Soundcard > SB Audigy 1 [SB0092]_
        *   _Mixer control > Synth_

### Software

#### GStreamer-based players like Totem (GNOME Videos) or Rhythmbox

You can play MIDI files on GNOME Videos and all other players using gstreamer as backend after having installed [gst-plugins-bad](https://www.archlinux.org/packages/?name=gst-plugins-bad) (which provides [fluidsynth](https://www.archlinux.org/packages/?name=fluidsynth) as a dependency) and correctly configured Fluidsynth with a [sound sample](/index.php/Timidity#SoundFonts "Timidity"). See [FluidSynth](/index.php/FluidSynth "FluidSynth") for more info.

#### VLC

You can play MIDI files on [VLC](/index.php/VLC "VLC") if you configure the location of the Sound Font file. Previously you need to install a [sound sample](/index.php/Timidity#SoundFonts "Timidity"), as well as the [fluidsynth](https://www.archlinux.org/packages/?name=fluidsynth) package.

In VLC choose _Tools > Preferences_: you have to show all settings. Then, go to _Input/Codecs > Audio codecs > FluidSynth_.

And, if you installed e.g. fluidr3 as wiki says, set the location to:

```
/usr/share/soundfonts/FluidR3_GM2-2.sf2

```

**Note:**

*   Read the [mailing list thread](https://mailman.archlinux.org/pipermail/aur-general/2014-February/027378.html) about merging fluidr3 with [soundfont-fluid](https://www.archlinux.org/packages/?name=soundfont-fluid).
*   Fluidsynth support is not included in the [vlc](https://www.archlinux.org/packages/?name=vlc) package, however it is included in [vlc-git](https://aur.archlinux.org/packages/vlc-git/)<sup><small>AUR</small></sup>.

#### Audacious

[audacious](https://www.archlinux.org/packages/?name=audacious) has a built-in MIDI synthesizer which makes it essentially the easiest way to play a MIDI file with no extra setup. You can specify the soundfont to use for playback in the settings of its MIDI output plugin (File > Preferences > Plugins > Input > AMIDI-Plug > Preferences). As such the only prerequisites you need is the player and a soundfont file.

#### TiMidity++

MIDI to WAVE converter and player. See [TiMidity++](/index.php/Timidity "Timidity").

#### FluidSynth

MIDI player and a daemon adding MIDI support to ALSA. See [FluidSynth](/index.php/FluidSynth "FluidSynth").

Retrieved from "[https://wiki.archlinux.org/index.php?title=MIDI&oldid=410870](https://wiki.archlinux.org/index.php?title=MIDI&oldid=410870)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Multimedia](/index.php/Category:Multimedia "Category:Multimedia")