[Festival](http://www.cstr.ed.ac.uk/projects/festival/) is a general multi-lingual speech synthesis system developed at CSTR ([Centre for Speech Technology Research](http://www.cstr.ed.ac.uk/)).

Festival offers a general framework for building speech synthesis systems as well as including examples of various modules. As a whole it offers full text to speech through a number APIs: from shell level, though a Scheme command interpreter, as a C++ library, from Java, and an Emacs interface. Festival is multi-lingual (currently British English, American English, Italian, Czech and Spanish, with other languages available in prototype.)

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 Using German IMS festival extension with mbrola](#Using_German_IMS_festival_extension_with_mbrola)
*   [2 Configuration](#Configuration)
    *   [2.1 Usage with a Sound Server](#Usage_with_a_Sound_Server)
    *   [2.2 Voices](#Voices)
        *   [2.2.1 HTS compatibility patches](#HTS_compatibility_patches)
        *   [2.2.2 Manual Voice Installs](#Manual_Voice_Installs)
*   [3 Usage](#Usage)
    *   [3.1 Interactive mode (testing voices etc.)](#Interactive_mode_(testing_voices_etc.))
    *   [3.2 Example script](#Example_script)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Can't open /dev/dsp](#Can't_open_/dev/dsp)
    *   [4.2 Alsa playing at wrong speed](#Alsa_playing_at_wrong_speed)
    *   [4.3 aplay Command not found](#aplay_Command_not_found)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [festival](https://www.archlinux.org/packages/?name=festival) package. You need a voice package like [festival-english](https://www.archlinux.org/packages/?name=festival-english) or [festival-us](https://www.archlinux.org/packages/?name=festival-us).

Test festival:

```
$ echo "This is an example. Arch is the best." | festival --tts

```

If your hear all the example text, you successfully installed a TTS system.

If you do not hear anything, see the [Troubleshooting](#Troubleshooting) section. If you have a desktop system you will almost certainly get a message about `/dev/dsp` and need to follow those instructions.

### Using German IMS festival extension with mbrola

You can use the [festival-ims](https://aur.archlinux.org/packages/festival-ims/) package with IMS Stuttgart patches.

The [IMS of the University Stuttgart](http://www.ims.uni-stuttgart.de) developed an extension to festival especially for German language. It uses German voices with [mbrola](https://aur.archlinux.org/packages/mbrola/). To install it, the extension needs to be downloaded from the university's servers (follow the Instructions [here](http://www.ims.uni-stuttgart.de/institut/arbeitsgruppen/phonetik/synthesis/festival_opensource.html)) and the [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") needs to be modified.

Add these two files downloaded from the IMS (do NOT use the third file, `ims_german_1.3-os.fix.tgz`)

```
 ims_german_1.3-os.tgz
 bomp_full.corr.tgz

```

with their md5sums to the *source* variable and place them in the same folder as the PKGBUILD. In the `prepare()` section, include the following lines (at the end of the section):

```
   # add ims config
   sed -i 's/ALSO_INCLUDE +=$/# IMS module for German
ALSO_INCLUDE += ims_german_text/' "$srcdir/festival/config/config.in"
   cat<<EOF >> "$srcdir/festival/lib/sitevars.scm"
 (set! mbrola-path "/usr/share/mbrola/")
 (set! mbrola_progname "/usr/bin/mbrola -e")
 EOF
   echo "(require 'ims_german_opensource)" >> "$srcdir/festival/lib/siteinit.scm"

```

This should install support for the german voices `de1` through `de4`. Install at least one of these voices, e.g. [mbrola-voices-de2](https://aur.archlinux.org/packages/mbrola-voices-de2/), and then use it in festival by selecting the voice via

```
 (voice_german_de2_os)
 (SayText "Hallo Welt.")

```

from the prompt or use it in *text2wave* via

```
 text2wave -o spoken.wav -eval '(voice_german_de2_os)' *inputfile*.txt

```

where `*inputfile*.txt` the input file containing the text to be processed.

## Configuration

There is no global `/etc` configuration file, but you can configure festival with your `~/.festivalrc` file, or by directly editing `/usr/share/festival/festival.scm`. Both of these are scheme files, using scheme syntax and rerun everytime festival is run.

### Usage with a Sound Server

For PulseAudio, add these lines to the end of your `~/.festivalrc` file, or to `/usr/share/festival/festival.scm`:

```
(Parameter.set 'Audio_Required_Format 'aiff)
(Parameter.set 'Audio_Method 'Audio_Command)
(Parameter.set 'Audio_Command "paplay $FILE --client-name=Festival --stream-name=Speech")

```

For ALSA, use these lines instead ([source](http://ubuntuforums.org/showpost.php?p=4058268&postcount=16)):

```
(Parameter.set 'Audio_Method 'Audio_Command)
(Parameter.set 'Audio_Command "aplay -q -c 1 -t raw -f s16 -r $SR $FILE")

```

### Voices

Arch splits the set of official voices into [festival-english](https://www.archlinux.org/packages/?name=festival-english) and [festival-us](https://www.archlinux.org/packages/?name=festival-us). [The AUR](https://aur.archlinux.org/packages/?K=festival) has some others, in various states of maintenance which may or may not be currently working.

To see what voices you currently have installed and what your default is, go into the Festival shell (which is a scheme REPL) and type the following (some space added for clarity):

```
   $ festival

   Festival Speech Synthesis System 2.1:release November 2010
   Copyright (C) University of Edinburgh, 1996-2010\. All rights reserved.

   clunits: Copyright (C) University of Edinburgh and CMU 1997-2010
   clustergen_engine: Copyright (C) CMU 2005-2010
   hts_engine: 
   The HMM-based speech synthesis system (HTS)
   hts_engine API version 1.04 ([http://hts-engine.sourceforge.net/](http://hts-engine.sourceforge.net/))
   Copyright (C) 2001-2010  Nagoya Institute of Technology
                 2001-2008  Tokyo Institute of Technology
   All rights reserved.
   For details type `(festival_warranty)'

   festival> voice_default 
   voice_cmu_us_slt_arctic_hts          ;;<-- THIS IS THE VOICE FESTIVAL SPEAKS WITH

   festival> default-voice-priority-list 
   (kal_diphone                         ;;<-- THIS IS THE HARD-CODED LIST OF VOICES FESTIVAL CAME PRE-AWARE OF
    cmu_us_bdl_arctic_hts
    cmu_us_jmk_arctic_hts
    cmu_us_slt_arctic_hts
    cmu_us_awb_arctic_hts
    ked_diphone
    don_diphone
    rab_diphone
    en1_mbrola
    us1_mbrola
    us2_mbrola
    us3_mbrola
    gsw_diphone
    el_diphone)

   festival> (voice_                    ;;<-- PRESS TAB HERE TO SEE WHAT VOICES FESTIVAL HAS AVAILABLE
   voice_cmu_us_slt_arctic_hts     voice_kal_diphone               voice_nitech_us_slt_arctic_hts  voice_reset
   voice_default                   voice_nitech_us_clb_arctic_hts  voice_rab_diphone

   festival> (voice_cmu_us_slt_arctic_hts) 
   cmu_us_slt_arctic_hts

   festival> (SayText "Arch makes me happy")
   #<Utterance 0x7fb5b8c423b0>

   festival> 

```

To permanently change the default voice you can add a line like this to the end of `~/.festivalrc`:

```
(set! voice_default voice_cmu_us_slt_arctic_hts)

```

You cannot set the voice with festival.scm; to set voices globally, set order of searched voices in `/usr/share/festival/voices.scm`.

#### HTS compatibility patches

Some say that HTS voices for Festival are the best ones freely available. Sadly they are not compatible with Festival >2.1 without patching it (and the new voice versions are not made available for downloading).

You can install the patched version from [AUR](/index.php/AUR "AUR"): [festival-patched-hts](https://aur.archlinux.org/packages/festival-patched-hts/) and [festival-hts-voices-patched](https://aur.archlinux.org/packages/festival-hts-voices-patched/)

#### Manual Voice Installs

You can also get voices straight from [festvox.org](http://festvox.org/festival/downloads.html). In their downloads, the files named `festvox_*.tgz` each contain a different voice, as built by the festival team. They do work, but you will need to manually unzip and move the folder containing the voice to the appropriate place. On a recent Arch, the appropriate place is `/usr/share/festival/voices/english/` and the way to tell what folder contains the voice is to look for a `festvox/` subfolder inside of it.

You can then test that your new voices are found by loading up the festival prompt again.

## Usage

Read a text file:

```
$ festival --tts /path/to/letter.txt

```

Be obnoxious while demonstrating piping

```
$ (echo "Get ready for some pain"; sudo cat /var/log/messages.log) | festival --tts

```

Convert a text file to mp3:

```
$ cat letter.txt | text2wave | lame - file.mp3 && mplayer file.mp3

```

### Interactive mode (testing voices etc.)

festival has an interactive prompt you can use for testing. Some examples (with sample output):

```
$ festival 
[...]
festival> 

```

List available voices:

```
festival> (voice.list)
(cstr_us_awb_arctic_multisyn kal_diphone don_diphone)

```

Set voice:

```
festival> (voice_cstr_us_awb_arctic_multisyn)
#<voice 0x1545b90>

```

Speak:

```
festival> (SayText '"test this is a test oh no a test bla test")
inserting pause after: t.
Inserting pause
[...]
id _63 ; name t ; 
id _65 ; name # ; 
#<Utterance 0x7f7c0c144810>

```

More:

```
festival> help 
"The Festival Speech Synthesizer System: Help

```

Quit: ctrl+d or

```
festival> (quit)

```

### Example script

One classic app that can make use of this is *ping*. Use this script to constantly *ping* a host, and return "Ping" if success, "Fail" if not:

```
#!/bin/bash
while :; do
    ping -c 1 $1 && (echo "Ping" | festival --tts) || (echo "Fail" | festival --tts)
done

```

Note that this does not really work on multisynth voices, as they take a while to prepare before playing.

## Troubleshooting

### Can't open /dev/dsp

If festival returns the following error message:

```
Linux: can't open /dev/dsp

```

See [#Usage with a Sound Server](#Usage_with_a_Sound_Server) above.

### Alsa playing at wrong speed

If the solution above gives you a squeaky voice, you might want to try changing your *aplay* options:

```
(Parameter.set 'Audio_Method 'Audio_Command)
(Parameter.set 'Audio_Command "aplay -Dplug:default -f S16_LE -r $SR $FILE")

```

### aplay Command not found

[Install](/index.php/Install "Install") [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils).

## See also

*   [Festival manual](http://www.cstr.ed.ac.uk/projects/festival/manual/)