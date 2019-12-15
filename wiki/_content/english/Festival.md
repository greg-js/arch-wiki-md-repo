[Festival](http://www.cstr.ed.ac.uk/projects/festival/) is a general multi-lingual speech synthesis system developed at CSTR ([Centre for Speech Technology Research](http://www.cstr.ed.ac.uk/)). It offers a general framework for building speech synthesis systems as well as including examples of various modules. As a whole it offers full text to speech through a number APIs: from shell level, though a Scheme command interpreter, as a C++ library, from Java, and an Emacs interface. Festival is multi-lingual (currently British English, American English, Italian, Czech and Spanish, with other languages available in prototype.)

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 German IMS](#German_IMS)
*   [2 Configuration](#Configuration)
    *   [2.1 Sound server](#Sound_server)
    *   [2.2 Voices](#Voices)
        *   [2.2.1 Manually](#Manually)
*   [3 Usage](#Usage)
    *   [3.1 Interactive](#Interactive)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Can't open /dev/dsp](#Can't_open_/dev/dsp)
    *   [4.2 Alsa playing at wrong speed](#Alsa_playing_at_wrong_speed)
    *   [4.3 Command aplay not found](#Command_aplay_not_found)
    *   [4.4 Server](#Server)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [festival](https://www.archlinux.org/packages/?name=festival) package. Voices are available with [festival-us](https://www.archlinux.org/packages/?name=festival-us) and [festival-english](https://www.archlinux.org/packages/?name=festival-english) packages.

### German IMS

The [IMS of the University Stuttgart](http://www.ims.uni-stuttgart.de) developed an extension to Festival especially for German language (see [here](http://www.ims.uni-stuttgart.de/institut/arbeitsgruppen/phonetik/synthesis/festival_opensource.html)). It uses German voices with [mbrola](https://aur.archlinux.org/packages/mbrola/). To use it, install [festival-ims](https://aur.archlinux.org/packages/festival-ims/) with IMS Stuttgart patches. This should add support for the german voices *de1* through *de4*. Install at least one of the voices (listed as optional dependencies), e.g. [mbrola-voices-de2](https://aur.archlinux.org/packages/mbrola-voices-de2/).

## Configuration

There is no global `/etc/` configuration file, but you can configure festival with your `~/.festivalrc` file, or by directly editing `/usr/share/festival/festival.scm`. Both of these are scheme files, using scheme syntax and rerun everytime festival is run.

### Sound server

The following allows Festival to work if audio from other sources is already playing. Add to your config:

For PulseAudio:

```
(Parameter.set 'Audio_Required_Format 'aiff)
(Parameter.set 'Audio_Method 'Audio_Command)
(Parameter.set 'Audio_Command "paplay $FILE --client-name=Festival --stream-name=Speech")

```

For ALSA: [[1]](http://web.archive.org/web/20110522202347/http://ubuntuforums.org/showthread.php?t=171182&page=3)

```
(Parameter.set 'Audio_Method 'Audio_Command)
(Parameter.set 'Audio_Command "aplay -q -c 1 -t raw -f s16 -r $SR $FILE")

```

### Voices

Arch splits the set of official voices into [festival-us](https://www.archlinux.org/packages/?name=festival-us) (recommended) and [festival-english](https://www.archlinux.org/packages/?name=festival-english). The [AUR](https://aur.archlinux.org/packages/?K=festival) has some others, in various states of maintenance which may or may not be currently working.

To see what voices are currently installed and what the default is, first enter Festival's [#Interactive](#Interactive) shell (a REPL scheme). To permanently change the default voice add it to your config, for example:

```
(set! voice_default voice_cmu_us_rms_cg)

```

#### Manually

You can also get voices straight from Festvox [[2]](http://festvox.org/festival/downloads.html) [[3]](http://festvox.org/packed/festival/2.5/voices/). You will need to unzip and move the folder containing the voice to `/usr/share/festival/voices/` and the way to tell what folder contains the voice is to look for a `festvox/` subfolder inside of it. You can then test that your new voices are found by loading up the festival prompt.

## Usage

To read a text file:

```
$ festival --tts *text_file*

```

To read a selection you highlighted with the cursor:

```
$ xsel | festival --tts

```

Convert a text file to an mp3 audio:

```
$ text2wave *text_file* | lame - *text*.mp3

```

Record audio with a select voice:

```
$ text2wave -o *output*.wav -eval '(voice_german_de2_os)' *text_file*

```

### Interactive

Festival has an interactive prompt you can use for testing. Type `festival` to enter it. The following are some examples:

To show the voice festival speaks with:

```
voice_default 

```

To list available voices:

```
(voice.list)

```

To select another voice, enter `(*voice_name*)`. For example:

```
(voice_cmu_us_rms_cg)

```

To hear it speak:

```
(SayText "Arch makes me happy") 

```

To list available commands:

```
help

```

To exit the shell:

```
(quit)

```

## Troubleshooting

### Can't open /dev/dsp

If festival returns the following error message:

```
Linux: can't open /dev/dsp

```

See [#Sound server](#Sound_server) above.

### Alsa playing at wrong speed

If the solution above gives you a squeaky voice, you might want to try changing your *aplay* options:

```
(Parameter.set 'Audio_Method 'Audio_Command)
(Parameter.set 'Audio_Command "aplay -Dplug:default -f S16_LE -r $SR $FILE")

```

### Command aplay not found

Install the [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils) package.

### Server

Install [festival-freebsoft-utils](https://aur.archlinux.org/packages/festival-freebsoft-utils/) to use Festival with Speech Dispatcher (i.e. in Firefox's Reader).

## See also

*   [Festival manual](http://festvox.org/docs/manual-2.4.0/)