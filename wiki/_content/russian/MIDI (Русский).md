MIDI, или «Musical Instrument Digital Interface», представляет собой просто протокол и стандарт для совместной работы музыкальных инструментов и любых устройств, поддерживающих этот протокол. Он может использоваться для управления множеством синтезаторов, которые все вместе могут звучать как ударные инструменты, или даже изображать индустриальный шум.

Рамки этой статьи, тем не менее, охватывают главным образом преимущественно использование MIDI в компьютерных системах для воспроизведения файлов, содержащих данные MIDI. Эти файлы обычно имеют расширение **.mid**, и когда-то широко использовались для распространения музыки. В профессиональном сочинении/аранжировке музыки MIDI продолжает играть жизненно важную роль.

## Contents

*   [1 MIDI File](#MIDI_File)
*   [2 GM Bank](#GM_Bank)
*   [3 Playback](#Playback)
    *   [3.1 Hardware](#Hardware)
    *   [3.2 Software](#Software)
        *   [3.2.1 VLC](#VLC)
        *   [3.2.2 Timidity++](#Timidity.2B.2B)
        *   [3.2.3 FluidSynth](#FluidSynth)
*   [4 External Links](#External_Links)

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

In order for such a file to be useful, there needs to be an "engine" that can translate the data to music. This engine will have a "tone generator", and this is what we call a "synthesizer". So any player that can play back a MIDI file without MIDI-capable hardware (your computer's sound device), has a synthesizer built-in or uses an external one. A typical keyboard (not the QWERTY thing you are typing on) is actually made up of two components - a MIDI "controller" (the keys) and a synthesizer (tone generator/module; the thing that makes sound).

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

Well, because Windows has a default software synthesizer which acts globally. Even then, it lacks the quality which should be expected of modern computers. If there were a way to do it on Linux, you would be able to play back MIDI from any player too. Perhaps a MIDI server (which will hold a synthesizer of choice like TiMidity++ or FluidSynth) that sits within the sound server, like Phonon or PulseAudio. Nevertheless, nothing of this sort has been implemented and you can only play MIDI with a player that has a plug-in to source a synthesizer or has a synthesizer itself. Such an example is XMMS.

### Hardware

(Details on soundcards and MIDI, possibly link to SBLive MIDI here..)

### Software

(Details on options available, like TiMidity++ or FluidSynth. Can be merged or linked if page exists, eg. there is an article for [Timidity](/index.php/Timidity "Timidity") already.)

#### VLC

You can play MIDI files on VLC if you configure the location of the Sound Font file. Previously you need install a [sound sample](/index.php/Timidity#SoundFonts "Timidity").

On VLC -> Tools -> Preferences

You have to show all settings. Then, go to input/codecs -> audio codecs -> FluidSynth.

And, if you installed fluidr3 as wiki says, set the location to:

/usr/share/soundfonts/fluidr3/FluidR3GM.SF2

#### [Timidity++](/index.php/Timidity "Timidity")

MIDI to WAVE converter and player.

#### [FluidSynth](/index.php/FluidSynth "FluidSynth")

MIDI player and a daemon adding MIDI support to ALSA.

## External Links

[set up midi](http://home.roadrunner.com/~infofiles/midi.html)