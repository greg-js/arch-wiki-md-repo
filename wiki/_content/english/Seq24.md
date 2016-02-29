## Contents

*   [1 Introduction](#Introduction)
*   [2 How to setup seq24](#How_to_setup_seq24)
*   [3 How to use seq24](#How_to_use_seq24)
*   [4 Setting an instrument](#Setting_an_instrument)
*   [5 Further use](#Further_use)

## Introduction

seq24 is a MIDI sequencer. It has a simple user interface. MIDI ".mid" files are the native file format for seq24.

## How to setup seq24

seq24 can be found in the [AUR](/index.php/AUR "AUR"): [seq24](https://aur.archlinux.org/packages/seq24/).

seq24 is a sequencer only. To be able to listen to your music as you create it, you will need a MIDI device installed on your computer. Follow the instructions on the [timidity](/index.php/Timidity "Timidity") wiki page to easily setup a software MIDI device. Then, when using seq24, (you will learn more about this in external documentation) select one of the "TiMidity ports" in the track editor to connect to a MIDI device. For example, on my computer, one of the devices is "[1] 128:0 (TiMidity port 0)".

## How to use seq24

The documentation for seq24 can be found in the [seq24 manual](http://www.filter24.org/seq24/SEQ24). Please read all the way through this document.

**Note:** Once again, please read through the seq24 manual! It's not very long. seq24 has a very simple and possibly confusing user interface, but is very easy to use once you understand it.

When you feel ready to begin using seq24, you may wish to use this outstanding [tutorial](http://www.linuxjournal.com/article/8304).

## Setting an instrument

To set a MIDI instrument, bring up a track editor window by right clicking a "track box" and selecting "Edit...". Select a MIDI device, or "output bus", and select a MIDI channel. There are 16 channels per MIDI device. Keep in mind that a channel can only play one instrument at a time. (So, you won't be able to play a piano sound on channel 5 and a flute sound on channel 5 at the same time) Also, channel 10 is always percussion. Next, select the "Event" button and select "Program Change". Add a program change event to the first tiny box underneath the keyboard roll by holding down the right mouse button and left clicking on it. Now, select the event box you just created with the left mouse button. You can now use the scroll wheel or right mouse button in the space above the instrument number to change the value of the MIDI instrument. The instrument probably won't be set until the next time you "play" through that section of the track. You can read more about the standard set of MIDI instruments [here](https://en.wikipedia.org/wiki/General_MIDI "wikipedia:General MIDI").

## Further use

seq24 has the ability to connect to other MIDI devices and software through the [JACK](/index.php/JACK "JACK") software, including QSynth, amSynth, and ZynAddSubFX.