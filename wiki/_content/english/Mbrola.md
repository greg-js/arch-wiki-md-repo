[mbrola](http://tcts.fpms.ac.be/synthesis/mbrola.html) is a non-free [phonemes-to-audio](http://nvoq.com/sites/default/files/marketing/White%20Paper_Demystifying%20Speech%20Recognition%20by%20Charles%20Corfield_July2012.pdf) program to use with text-to-speech applications. It is free to use for non-commercial, non-military applications.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Add voices](#Add_voices)
*   [2 Testing](#Testing)
*   [3 Install a text-to-phonemes program](#Install_a_text-to-phonemes_program)
    *   [3.1 LLiaphon](#LLiaphon)

## Installation

[Install](/index.php/Install "Install") the [mbrola](https://aur.archlinux.org/packages/mbrola/) package.

### Add voices

Packages named *mbrola-voices-xxx* are available in the [AUR](https://aur.archlinux.org/packages.php?K=mbrola-voices)

**Note:** these packages have been built by a script so if something is wrong, please leave a comment for the package maintainer.

## Testing

Once you have installed the wanted voice(s) go to the directory of the installed language:

```
$ cd /usr/share/mbrola/us1/

```

then list the test files:

```
$ ls TEST/

```

If there are no test files for this language, try with another language or skip to [#Install a text-to-phonemes program](#Install_a_text-to-phonemes_program).

Else choose a test file (files with .pho extension) and try:

```
$ mbrola ./us1 ./TEST/mbrola.pho ~/test.wav; aplay ~/test.wav; rm ~/test.wav

```

If the installation worked ok, you should hear the voice now.

Note that we this test did not give a text file to *mbrola* but a phoneme file. To make it a text-to-speech system, see below.

## Install a text-to-phonemes program

To obtain a full TTS system we need a text-to-phonemes program compatible with mbrola: [List of TTS programs compatible with mbrola](http://tcts.fpms.ac.be/synthesis/mbrola.html).

### LLiaphon

[LLiaPhon](http://gna.org/projects/lliaphon) is a TTS program which uses mbrola.

[Install](/index.php/Install "Install") [lliaphon](https://aur.archlinux.org/packages/lliaphon/).

Once you installed both, try this command:

```
$ export MBROLA_VOICE=/usr/share/mbrola/us1/us1;echo "That is a test."|lliaphon|play_ola

```