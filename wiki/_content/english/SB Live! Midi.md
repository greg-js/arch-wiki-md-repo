*SB Live!* uses a wavetable synthesizer for its MIDI output. Therefore, in order to get MIDI output you need to load the SoundFont banks into the card. This is done by the `asfxload` utility from `awesfx` package.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Which bank to load?](#Which_bank_to_load?)
    *   [2.2 Automating](#Automating)

## Installation

[Install](/index.php/Install "Install") the [awesfx](https://aur.archlinux.org/packages/awesfx/) package.

Copy the SoundFont files from your SB Live driver CD somewhere on your hdd. On the SB Live! Value CD, they are named: `2GMGSMT.SF2`, `4GMGSMT.SF2` and `8MBGMSFX.SF2`.

Load the bank by executing `asfxload *bankfile*`. See `man sfxload` for more advanced options. Some users have reported that `snd_emu10k1_synth` needs to be preloaded in order for this to work.

## Configuration

### Which bank to load?

The bank names (at least for SB Live! Value) correspond to their respective sizes (2 Mb, 4 Mb, 8 Mb). The bigger the bank is, the better the quality, although more RAM is also used, since SB Live Value doesn't have its own memory banks.

### Automating

Put `asfxload *fullbankfilepathname*` into `/etc/rc.local`.

It should be sfxload, not asfxload. You might also need to modprobe snd-seq-oss. The line to put in /etc/rc.local that I have is:

```
sfxload -D *n* /usr/share/sounds/sf2/CT4MGM.SF2

```

*n* is the number of sound cards. 0 is first sound card, 1 second and so on.