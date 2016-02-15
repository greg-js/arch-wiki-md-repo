**[Rosegarden](http://www.rosegardenmusic.com/)** is a digital audio workstation program written in Qt. It acts as an audio and MIDI sequencer, scorewriter and musical composition and editing tool. It is intended to be a free alternative to such applications as Cubase.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Customizing keyboard shortcuts](#Customizing_keyboard_shortcuts)
*   [3 Usage](#Usage)
    *   [3.1 With Timidity and Pulseaudio](#With_Timidity_and_Pulseaudio)
*   [4 See also](#See_also)

## Installation

[rosegarden](https://www.archlinux.org/packages/?name=rosegarden) is available in the [extra] repository. Be sure to install a [MIDI](/index.php/MIDI "MIDI") setup first.

## Configuration

### Customizing keyboard shortcuts

The keyboard shortcuts in rosegarden can be customized by editing a set of XML configuration files. The first step is to download the default configuration files which are packaged with the source code, and place them in `~/.local/share/rosegarden/rc`. A simple way of doing this is to run

```
$ cd ~/.local/share/rosegarden
$ svn co [http://svn.code.sf.net/p/rosegarden/code/trunk/rosegarden/data/rc](http://svn.code.sf.net/p/rosegarden/code/trunk/rosegarden/data/rc)

```

which will get the configuration files from the development branch of the source code.

**Note:** The above procedure gets the configuration files from the development branch of Rosegarden, which could possibly be incompatible with the stable release. If needed, the `rc` directory can be found at `data/rc` in the stable release's source tarball instead.

Keyboard shortcuts can then be set or modified by editing the appropriate file in `~/.local/share/rosegarden/rc`. For example, in order to map the `Space` bar to play/pause, edit the following lines of `rosegardenmainwindow.rc`

 `~/.local/share/rosegarden/rc/rosegardenmainwindow.rc` 

```
<Action name="play" text="&Play" icon="transport-play" shortcut="Ctrl+Enter, Enter, Media Play, Ctrl+Return, Space" shortcut-context="application" />
<Action name="recordtoggle" text="P&unch in Record" icon="transport-record" shortcut="" shortcut-context="application" />
```

## Usage

### With Timidity and Pulseaudio

Launch [Timidity](/index.php/Timidity "Timidity") as a [daemon](/index.php/Timidity#Daemon "Timidity") before launching Rosegarden :

 `$ timidity -iA` 

This way, Rosegarden will not launch [jackd](/index.php/JACK "JACK") and you'll still be able to hear sound from other running apps.

## See also

*   [Pro Audio](/index.php/Pro_Audio "Pro Audio")