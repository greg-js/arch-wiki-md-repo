TiMidity++ is a [software synthesizer](https://en.wikipedia.org/wiki/software_synthesizer "wikipedia:software synthesizer") that can play MIDI files without a hardware synthesizer. It can either render to the sound card in real time, or it can save the result to a file, such as a PCM .wav file.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 SoundFonts](#SoundFonts)
        *   [2.1.1 Freepats](#Freepats)
        *   [2.1.2 Fluidr3](#Fluidr3)
    *   [2.2 Daemon](#Daemon)
*   [3 Usage](#Usage)
    *   [3.1 Play files](#Play_files)
        *   [3.1.1 Standalone mode](#Standalone_mode)
        *   [3.1.2 Daemon mode](#Daemon_mode)
        *   [3.1.3 Connect to virtual MIDI device](#Connect_to_virtual_MIDI_device)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 TiMidity++ does not play MIDI files](#TiMidity.2B.2B_does_not_play_MIDI_files)
    *   [4.2 Daemon mode plays sound out of pace](#Daemon_mode_plays_sound_out_of_pace)
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 Convert files](#Convert_files)
    *   [5.2 How to make DOSBox use TiMidity++](#How_to_make_DOSBox_use_TiMidity.2B.2B)
*   [6 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [timidity++](https://www.archlinux.org/packages/?name=timidity%2B%2B) package from the [official repositories](/index.php/Official_repositories "Official repositories").

You should also install a [SoundFont](https://en.wikipedia.org/wiki/SoundFont "wikipedia:SoundFont") to be able to produce sound. Here is a list of SoundFonts:

*   [timidity-freepats](https://www.archlinux.org/packages/?name=timidity-freepats).
*   [soundfont-fluid](https://www.archlinux.org/packages/?name=soundfont-fluid)

## Configuration

First you should add yourself to the audio group.

```
# gpasswd -a <user> audio

```

### SoundFonts

Configure your preferred SoundFont.

#### Freepats

The [Freepats](http://freepats.zenvoid.org/) project provides a set of instrument samples which are compatible with TiMidity++.

To use Freepats with TiMidity, add the following lines to `timidity.cfg`:

 `/etc/timidity++/timidity.cfg` 
```
dir /usr/share/timidity/freepats
source /etc/timidity++/freepats/freepats.cfg

```

#### Fluidr3

There are other SoundFonts available. To install the [soundfont-fluid](https://www.archlinux.org/packages/?name=soundfont-fluid) SoundFont, append its path to the TiMidity++ configuration file:

 `/etc/timidity++/timidity.cfg` 
```
soundfont /usr/share/soundfonts/FluidR3_GM.sf2

```

### Daemon

[Start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") the `timidity.service`.

If you are using [PulseAudio](/index.php/PulseAudio "PulseAudio"), that may not work. You may want to add the following command as an auto start program in your desktop environment. Or, if you just want to start TiMidity++ in daemon mode once, you can use the following command which will make console output viewable:

```
$ timidity -iA

```

You can also use [Systemd/User](/index.php/Systemd/User "Systemd/User") to write an user TiMidity++ service. To do so, write a `timidity.service` file in `~/.config/systemd/user/` like that one :

 `/etc/systemd/user/timidity.service` 
```
[Unit]
Description=TiMidity++ Daemon
After=sound.target

[Service]
ExecStart=/usr/bin/timidity -iA -Os

[Install]
WantedBy=default.target

```

Then enable the service with:

```
 $ systemctl --user enable timidity.service

```

## Usage

### Play files

There are two ways to use TiMidity++. Either as MIDI player or as daemon adding MIDI support to [ALSA](/index.php/ALSA "ALSA").

#### Standalone mode

You can simply use TiMidity++ to play MIDI files:

```
$ timidity example.midi

```

Add option `-in` or `-ig` for a text-based/gtk+ interface. E.g. as a Xfce/GNOME user you may want to set MIDI files to open with the custom command `timidity -ig`. There are many other options to TiMidity++. See `man timidity` or use `-h` to get help.

The GTK+ interface offers such features as a playlist, track length estimates, volume control, a file load dialog box, play and pause buttons, rewind and fast forward buttons, as well as options to change the pitch of or speed up or slow down the playback of a midi file.

#### Daemon mode

If you are runing TiMidity++ as a [daemon](#Daemon) (ALSA sequencer client), it will provide MIDI output support for other programs such as rosegarden, aplaymidi, vkeybd, etc.

This will give you four output software MIDI ports (in addition of hardware MIDI ports on your system, if any):

 `$  aconnect -o` 
```
client 128: 'TiMidity' [type=user]
    0 'TiMidity port 0 '
    1 'TiMidity port 1 '
    2 'TiMidity port 2 '
    3 'TiMidity port 3 '
```

You can now play MIDI files using aplaymidi:

```
$ aplaymidi filename.mid --port 128:0

```

Another example is **vkeybd**, a virtual MIDI keyboard for X.

You can [install](/index.php/Install "Install") [vkeybd](https://aur.archlinux.org/packages/vkeybd/) from the [AUR](/index.php/AUR "AUR").

```
$ vkeybd --addr 128:0

```

Option `--addr 128:0` connects the input (readable) software MIDI port provided by vkeybd to the first output (writable) ALSA port provided by Timidity. Alternatively you can use aconnect, [aconnectgui](https://aur.archlinux.org/packages/aconnectgui/), [patchage](https://www.archlinux.org/packages/?name=patchage) or kaconnect. As a result when you play around with the keys on the vkeybd TiMidity++ plays the appropriate notes.

#### Connect to virtual MIDI device

Once you have the TiMidity++ daemon running and it is working with aplaymidi, you can connect it to a virtual MIDI device that will work in programs such as rosegarden or scala.

Load the `snd-virmidi` **kernel module** and (optionally) configure it to be loaded at boot. Read [Kernel modules](/index.php/Kernel_modules "Kernel modules") for more information.

Use aconnect to verify the port numbers:

 `$ aconnect -o` 
```
client 14: 'Midi Through' [type=kernel]
     0 'Midi Through Port-0'
 client 20: 'Virtual Raw MIDI 1-0' [type=kernel]
     0 'VirMIDI 1-0     '
 client 21: 'Virtual Raw MIDI 1-1' [type=kernel]
     0 'VirMIDI 1-1     '
 client 22: 'Virtual Raw MIDI 1-2' [type=kernel]
     0 'VirMIDI 1-2     '
 client 23: 'Virtual Raw MIDI 1-3' [type=kernel]
     0 'VirMIDI 1-3     '
 client 128: 'TiMidity' [type=user]
     0 'TiMidity port 0 '
     1 'TiMidity port 1 '
     2 'TiMidity port 2 '
     3 'TiMidity port 3 '
```

Now create the connection:

```
$ aconnect 20:0 128:0

```

You should now have a working MIDI output device on your system (`/dev/snd/midiC1D0`).

## Troubleshooting

### TiMidity++ does not play MIDI files

It may be that your SoundFile is not set up correctly. Just run:

```
$ timidity example.midi

```

If you find a line like this in the terminal output, your SoundFile is not set up properly.

```
No instrument mapped to tone bank 0, program XX - \
this instrument will not be heard

```

Make sure you've installed some samples and your SoundFile is added to `/etc/timidity++/timidity.cfg`. See [SoundFonts](#SoundFonts) for more details.

### Daemon mode plays sound out of pace

TiMidity++'s ALSA output module (default) may cause this issue in ALSA server mode. Try another output option, for example, **libao**:

```
$ timidity -iA -OO

```

And test it using aplaymidi. If this does not work, you may want to configure [JACK](/index.php/JACK "JACK") and set TiMidity++'s output to jack.

## Tips and tricks

### Convert files

TiMidity++ can also convert MIDI files into other formats. The following command saves the resulting sound to a WAV file:

```
$ timidity *input.mid* -Ow -o *out.wav*

```

To convert to another formats, you can use [FFmpeg](/index.php/FFmpeg "FFmpeg"). This will convert it to mp3:

```
$ timidity *input.mid* -Ow -o - | ffmpeg -i - -acodec libmp3lame -ab 256k *out.mp3*

```

### How to make DOSBox use TiMidity++

**Note:** The following method is tested in version [DOSBox](/index.php/DOSBox "DOSBox") 0.72

First of all, you need to write a config file. Input the following in [DOSBox](/index.php/DOSBox "DOSBox") to create a configuration file:

```
config -writeconf dosbox.conf

```

you can replace `dosbox.conf` by any name that you want, add a dot in front of it if you want to hide it.

Make sure you started TiMidity++ as [daemon](#Daemon) as the instructions above, use the **aconnect** command.

Edit this configuration file with any editor, go to the section:

 `dosbox.conf` 
```
[midi]
mpu401=intelligent
device=default
config=
```

put the ALSA connection port into the back of *config=*, in default:

```
config=128:0

```

Restart DOSBox within a terminal so you can see its debug messages, by no accident you should see a successful initiation on port 128:0.

## See also

*   [USB MIDI keyboards](/index.php/USB_MIDI_keyboards "USB MIDI keyboards")