[PulseAudio](https://en.wikipedia.org/wiki/PulseAudio "wikipedia:PulseAudio") serves as a proxy to sound applications using existing kernel sound components like [ALSA](/index.php/ALSA "ALSA") or [OSS](/index.php/OSS "OSS"). Since ALSA is included in Arch Linux by default, the most common deployment scenarios include PulseAudio with ALSA.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Front-ends](#Front-ends)
*   [2 Configuration](#Configuration)
    *   [2.1 Configuration files](#Configuration_files)
        *   [2.1.1 daemon.conf](#daemon.conf)
        *   [2.1.2 default.pa](#default.pa)
        *   [2.1.3 client.conf](#client.conf)
    *   [2.2 Configuration command](#Configuration_command)
*   [3 Running](#Running)
    *   [3.1 Starting manually](#Starting_manually)
*   [4 Back-end configuration](#Back-end_configuration)
    *   [4.1 ALSA](#ALSA)
        *   [4.1.1 Expose PulseAudio sources, sinks and mixers to ALSA](#Expose_PulseAudio_sources.2C_sinks_and_mixers_to_ALSA)
        *   [4.1.2 ALSA/dmix without grabbing hardware device](#ALSA.2Fdmix_without_grabbing_hardware_device)
    *   [4.2 OSS](#OSS)
        *   [4.2.1 ossp](#ossp)
        *   [4.2.2 padsp wrapper](#padsp_wrapper)
    *   [4.3 GStreamer](#GStreamer)
    *   [4.4 OpenAL](#OpenAL)
    *   [4.5 libao](#libao)
*   [5 Equalizer](#Equalizer)
    *   [5.1 Load equalizer sink and dbus-protocol module](#Load_equalizer_sink_and_dbus-protocol_module)
    *   [5.2 GUI front-end](#GUI_front-end)
    *   [5.3 Load equalizer and dbus module on every boot](#Load_equalizer_and_dbus_module_on_every_boot)
*   [6 Applications](#Applications)
    *   [6.1 QEMU](#QEMU)
    *   [6.2 AlsaMixer.app](#AlsaMixer.app)
    *   [6.3 XMMS2](#XMMS2)
    *   [6.4 KDE Plasma Workspaces and Qt4](#KDE_Plasma_Workspaces_and_Qt4)
    *   [6.5 Audacious](#Audacious)
    *   [6.6 Java/OpenJDK 6](#Java.2FOpenJDK_6)
    *   [6.7 Music Player Daemon (MPD)](#Music_Player_Daemon_.28MPD.29)
    *   [6.8 MPlayer](#MPlayer)
    *   [6.9 guvcview](#guvcview)
*   [7 Tips and tricks](#Tips_and_tricks)
    *   [7.1 Keyboard volume control](#Keyboard_volume_control)
    *   [7.2 Play sound from a non-interactive shell (systemd service, cron)](#Play_sound_from_a_non-interactive_shell_.28systemd_service.2C_cron.29)
    *   [7.3 X11 Bell Events](#X11_Bell_Events)
    *   [7.4 Switch on connect](#Switch_on_connect)
*   [8 Troubleshooting](#Troubleshooting)
*   [9 See also](#See_also)

## Installation

Install the [pulseaudio](https://www.archlinux.org/packages/?name=pulseaudio) package.

Some PulseAudio modules have been [split](https://www.archlinux.org/news/pulseaudio-split/) from the main package and must be installed separately if needed:

*   [pulseaudio-bluetooth](https://www.archlinux.org/packages/?name=pulseaudio-bluetooth): Bluetooth (Bluez) support
*   [pulseaudio-equalizer](https://www.archlinux.org/packages/?name=pulseaudio-equalizer): Equalizer sink (qpaeq)
*   [pulseaudio-gconf](https://www.archlinux.org/packages/?name=pulseaudio-gconf): GConf support (paprefs)
*   [pulseaudio-jack](https://www.archlinux.org/packages/?name=pulseaudio-jack): JACK sink, source and jackdbus detection
*   [pulseaudio-lirc](https://www.archlinux.org/packages/?name=pulseaudio-lirc): Infrared (LIRC) volume control
*   [pulseaudio-xen](https://www.archlinux.org/packages/?name=pulseaudio-xen): Xen paravirtual sink
*   [pulseaudio-zeroconf](https://www.archlinux.org/packages/?name=pulseaudio-zeroconf): Zeroconf (Avahi/DNS-SD) support

**Note:** Some confusion can be made between [ALSA](/index.php/ALSA "ALSA") and PulseAudio. ALSA includes both Linux kernel component with sound card drivers, and a userspace component, `libalsa`.[[1]](http://www.alsa-project.org/main/index.php/Download) PulseAudio builds only on the kernel component, but offers compatibility with `libalsa` through [pulseaudio-alsa](https://www.archlinux.org/packages/?name=pulseaudio-alsa).[[2]](http://www.freedesktop.org/wiki/Software/PulseAudio/FAQ/#index14h3)

### Front-ends

There are a number of front-ends available for controlling the PulseAudio daemon:

*   GTK GUIs: [paprefs](https://www.archlinux.org/packages/?name=paprefs) and [pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol)
*   Volume control via mapped keyboard keys: [pulseaudio-ctl](https://aur.archlinux.org/packages/pulseaudio-ctl/)
*   Console (CLI) mixers: [ponymix](https://www.archlinux.org/packages/?name=ponymix) and [pamixer](https://www.archlinux.org/packages/?name=pamixer)
*   Console (curses) mixer: [pulsemixer](https://aur.archlinux.org/packages/pulsemixer/)
*   Web volume control: [PaWebControl](https://github.com/Siot/PaWebControl)
*   System tray icon: [pasystray](https://aur.archlinux.org/packages/pasystray/), [pasystray-git](https://aur.archlinux.org/packages/pasystray-git/)
*   KF5 plasma applet: [kmix](https://www.archlinux.org/packages/?name=kmix) and [plasma-pa](https://www.archlinux.org/packages/?name=plasma-pa)
*   If you want to use Bluetooth Headsets or other Bluetooth Audio Devices together with PulseAudio see the [Bluetooth headset](/index.php/Bluetooth_headset "Bluetooth headset") Article.

## Configuration

### Configuration files

By default, PulseAudio is configured to automatically detect all sound cards and manage them. It takes control of all detected ALSA devices and redirect all audio streams to itself, making the PulseAudio daemon the central configuration point. The daemon should work mostly out of the box, only requiring a few minor tweaks.

PulseAudio will first look for configuration files in home directory `~/.config/pulse`, then in system wide `/etc/pulse`.

PulseAudio runs as a server daemon that can run either system-wide or on per-user basis using a client/server architecture. The daemon by itself does nothing without its modules except to provide an API and host dynamically loaded modules. The audio routing and processing tasks are all handled by various modules. You can find a detailed list of all available modules at [Pulseaudio Loadable Modules](http://www.freedesktop.org/wiki/Software/PulseAudio/Documentation/User/Modules/). To enable them you can just add a line `load-module <module-name-from-list>` to `~/.config/pulse/default.pa`.

**Tip:**

*   It is strongly suggested not to edit system wide configuration files, but rather edit user ones. Create the `~/.config/pulse` directory, then copy the system configuration files into it and edit according to your need.
*   Make sure you keep user configuration in sync with changes to the packaged files in `/etc/pulse/`. Otherwise, PulseAudio may refuse to start due to configuration errors.
*   There is usually no need to add your user to the `audio` group, as PulseAudio uses [udev](/index.php/Udev "Udev") and *logind* to give access dynamically to the currently "active" user. Exceptions would include running the machine headless so that there is no currently "active" user.

#### daemon.conf

Defines base settings like the default sample rates used by modules, resampling methods, realtime scheduling and various other settings related to the server process. These can not be changed at runtime without restarting the PulseAudio daemon. The defaults are sensible for most users.

**Note:** PulseAudio does not perform tilde expansion on paths in this file. Use absolute paths for any files.

<caption>Notable configuration options</caption>
| Option | Description |<caption></caption>
| system-instance | Run the daemon as a system-wide instance. Highly discouraged as it can introduce security issues. Useful on (headless) systems that have no real local users. Defaults to `no`. |<caption></caption>
| resample-method | Which resampler to use when audio with incompatible sample rates needs to be passed between modules (e.g. playback of 96kHz audio on hardware which only supports 48kHz). The available resamplers can be listed with `$ pulseaudio --dump-resample-methods`. Choose the best tradeoff between CPU usage and audio quality for the present use-case.
**Tip:** In some cases PulseAudio will generate a high CPU load. This can happen when multiple streams are resampled (individually). If this is a common use-case in a workflow, it should be considered to create an additional sink at a matching sample rate which can then be fed into the main sink, resampling only once.
 |<caption></caption>
| flat-volumes | `flat-volumes` scales the device-volume with the volume of the "loudest" application. For example, raising the VoIP call volume will raise the hardware volume and adjust the music-player volume so it stays where it was, without having to lower the volume of the music-player manually. Defaults to `yes` upstream, but to `no` within Arch.
**Note:** The default behavior upstream can sometimes be confusing and some applications, unaware of this feature, can set their volume to 100% at startup, potentially blowing your speakers or your ears. This is why Arch defaults to the classic (ALSA) behavior by setting this to `no`.
 |<caption></caption>
| default-fragments | Audio samples are split into multiple fragments of `default-fragment-size-msec` each. The larger the buffer is, the less likely audio will skip when the system is overloaded. On the downside this will increase the overall latency. Increase this value if you have issues. |

#### default.pa

This file is a startup script and is used to configure modules. It is actually parsed and read after the daemon has finished initializing and additional commands can be sent at runtime using `$ pactl` or `$ pacmd`. The startup script can also be provided on the command line by starting PulseAudio in a terminal using `$ pulseaudio -nC`. This will make the daemon load the CLI module and will accept the configuration directly from the command line, and output resulting information or error messages on the same terminal. This can be useful when debugging the daemon or just to test various modules before setting them permanently on disk. The manual page is quite self-explanatory, consult `man pulse-cli-syntax` for the details of the syntax.

**Tip:**

*   Rather than being a complete copy, `~/.config/pulse/default.pa` can start with the line `.include /etc/pulse/default.pa` and then just override the defaults.
*   Run `$ pacmd list-sinks|egrep -i 'index:|name:'` to list available sinks. The present default sink is marked with an asterisk.
*   Edit `~/.config/pulse/default.pa` to insert/alter the set-default-sink command using the sink's name as the numbering cannot be guaranteed repeatable.

#### `client.conf`

This is the configuration file read by every PulseAudio client application. It is used to configure runtime options for individual clients. It can be used to set and configure the default sink and source statically as well as allowing (or disallowing) clients to automatically start the server if not currently running.

### Configuration command

The main command to configure a server during runtime is `$ pacmd`. Run `$ pacmd --help` for a list options, or just run `$ pacmd` to enter the shell interactive mode and `Ctrl+d` to exit. All modifications will immediately be applied.

Once your new settings have been tested and meet your needs, edit the `default.pa` accordingly to make the change persistent. See [PulseAudio/Examples](/index.php/PulseAudio/Examples "PulseAudio/Examples") for some basic settings.

**Tip:** leave the `load-module module-default-device-restore` line in the `default.pa` file untouched. It will allow you to restart the server in its default state, thus dismissing any wrong setting.

It is important to understand that the "sources" (processes, capture devices) and "sinks" (sound cards, servers, other processes) accessible and selectable through PulseAudio depend upon the current hardware "Profile" selected. These "Profiles" are those ALSA "pcms" listed by the command `aplay -L`, and more specifically by the command `pacmd list-cards`, which will include a line "index:", a list beginning "profiles:", and a line "active profile: <...>" in the output, among other things.

The "active profile" can be set with the command `pacmd set-card-profile INDEX PROFILE`, with *no* comma separating INDEX and PROFILE, where INDEX is just the number on the line "index:" and a PROFILE name is everything shown from the beginning of any line under "profile:" to just *before* the colon and first space, as shown by the command `pacmd list-cards`. For instance, `pacmd set-card-profile 0 output:analog-stereo+input:analog-stereo`.

It may be easier to select a "Profile" with a graphical tool like `pavucontrol`, under the "Configuration" tab, or KDE System Settings, "Multimedia/Audio and Video Settings", under the "Audio Hardware Setup" tab. Each audio "Card", which are those devices listed by the command `aplay -l`, or again by the command `pacmd list-cards`, will have its own selectable "Profile". When a "Profile" has been selected, the then available "sources" and "sinks" can be seen by using the commands `pacmd list-sources` and `pacmd list-sinks`. Note that the "index" of the available sources and sinks will change each time a card profile is changed.

The selected "Profile" can be an issue for some applications, especially the Adobe Flash players, typically `/usr/lib/mozilla/plugins/libflashplayer.so` and `/usr/lib/PepperFlash/libpepflashplayer.so`. Often, these Flash players will only work when one of the Stereo profiles is selected, and otherwise, will play video with no sound, or will simply "crash". When all else fails, you might try selecting a different profile.

Of course, when configuring some variation of Surround Sound in PulseAudio, the appropriate Surround profile will have to be selected, before Surround Sound will work, or in order to do things like remap the speaker channels.

## Running

Since [version 7.0](http://www.freedesktop.org/wiki/Software/PulseAudio/Notes/7.0/), PulseAudio on Arch uses socket activation. [By default](https://projects.archlinux.org/svntogit/packages.git/commit/trunk?h=packages/pulseaudio&id=419bd740dc8), `pulseaudio.socket` is enabled for the [systemd/User](/index.php/Systemd/User "Systemd/User") instance.

**Note:**

*   To disable `pulseaudio.socket`, make sure that `$XDG_CONFIG_HOME/systemd/user/` exists and run `systemctl --user mask pulseaudio.socket`.
*   Many [desktop environments](/index.php/Desktop_environments "Desktop environments") autostart programs based on [desktop files](/index.php/Desktop_entries#Autostart "Desktop entries") in the `/etc/xdg/autostart/` directory. In this case, PulseAudio will be launched automatically regardless of the socket activation status.

For more information, see [PulseAudio: Running](http://www.freedesktop.org/wiki/Software/PulseAudio/Documentation/User/Running/).

### Starting manually

PulseAudio can be manually started with:

```
$ pulseaudio --start

```

And stopped with:

```
$ pulseaudio --kill

```

## Back-end configuration

### ALSA

Install the [pulseaudio-alsa](https://www.archlinux.org/packages/?name=pulseaudio-alsa) package. It contains the necessary `/etc/asound.conf` for configuring ALSA to use PulseAudio. Also make sure that `~/.asoundrc` does not exist, it would override the `/etc/asound.conf` file.

Also install [lib32-libpulse](https://www.archlinux.org/packages/?name=lib32-libpulse) and [lib32-alsa-plugins](https://www.archlinux.org/packages/?name=lib32-alsa-plugins) if you run a x86_64 system and want to have sound for 32-bit [multilib](/index.php/Multilib "Multilib") programs like Wine, Skype and Steam.

To prevent applications from using ALSA's OSS emulation and bypassing PulseAudio (thereby preventing other applications from playing sound), make sure the module `snd_pcm_oss` is not being loaded at boot. If it is currently loaded (`lsmod | grep oss`), disable it by executing:

```
# rmmod snd_pcm_oss

```

#### Expose PulseAudio sources, sinks and mixers to ALSA

Although [pulseaudio-alsa](https://www.archlinux.org/packages/?name=pulseaudio-alsa) contains the necessary configuration file to allow ALSA applications to use PulseAudio's default device, ALSA's `pulse` plugin is more versatile than that:

 `~/.asoundrc (or /etc/asound.conf)` 
```
# Create an alsa input/output using specific PulseAudio sources/sinks
 pcm.pulse-example1 {
     type pulse
     device "my-combined-sink" # name of a source or sink
     fallback "pulse-example2" # if combined not available
 }

 pcm.pulse-example2 {
     type pulse
     device "other-sound-card" # name of a source or sink
     # example: device "alsa_output.pci-0000_00_1b.0.analog-stereo"
 }

 # Create an alsa mixer using specific PulseAudio sources/sinks
 # these can be tested with "alsamixer -D pulse-example3"
 ctl.pulse-example3 {
     type pulse
     device "my-output" # name of source or sink to control

     # example: always control the laptop speakers:
     # device "alsa_output.pci-0000_00_1b.0.analog-stereo"
     fallback "pulse-example4" # supports fallback too
 }

 # Mixers also can control a specific source and sink, separately:
 ctl.pulse-example4 {
     type pulse
     sink "my-usb-headphones"
     source "my-internal-mic"

     # example: output to HDMI, record using internal
     sink "alsa_output.pci-0000_01_00.1.hdmi-stereo-extra1"
     source "alsa_input.pci-0000_00_1b.0.analog-stereo"
 }

 # These can override the default mixer (example: for pnmixer integration)
 ctl.!default {
     type pulse
     sink "alsa_output.pci-0000_01_00.1.hdmi-stereo-extra1"
     source "alsa_input.pci-0000_00_1b.0.analog-stereo"
 }
```

The [soure code](http://git.alsa-project.org/?p=alsa-plugins.git;a=tree;f=pulse;hb=HEAD) can be read to know all available options.

#### ALSA/dmix without grabbing hardware device

**Note:** This section describes alternative configuration, which is generally **not** recommended.

You may want to use ALSA directly in most of your applications while still being able to use applications which require PulseAudio at the same time. The following steps allow you to make PulseAudio use dmix instead of grabbing ALSA hardware device.

*   Remove package [pulseaudio-alsa](https://www.archlinux.org/packages/?name=pulseaudio-alsa), which provides compatibility layer between ALSA applications and PulseAudio. After this your ALSA apps will use ALSA directly without being hooked by Pulse.

*   Edit `/etc/pulse/default.pa`.

	Find and uncomment lines which load back-end drivers. Add **device** parameters as follows. Then find and comment lines which load autodetect modules.

```
load-module module-alsa-sink **device=dmix**
load-module module-alsa-source **device=dsnoop**
# load-module module-udev-detect
# load-module module-detect

```

*   *Optional:* If you use [kdemultimedia-kmix](https://www.archlinux.org/packages/?name=kdemultimedia-kmix) you may want to control ALSA volume instead of PulseAudio volume:

```
$ echo export KMIX_PULSEAUDIO_DISABLE=1 > ~/.kde4/env/kmix_disable_pulse.sh
$ chmod +x ~/.kde4/env/kmix_disable_pulse.sh

```

*   Now, reboot your computer and try running ALSA and PulseAudio applications at the same time. They both should produce sound simultaneously.

	Use [pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol) to control PulseAudio volume if needed.

### OSS

There are multiple ways of making OSS-only programs output to PulseAudio:

#### ossp

Install [ossp](https://www.archlinux.org/packages/?name=ossp) package and start `osspd.service`.

#### padsp wrapper

Programs using OSS can work with PulseAudio by starting it with padsp (included with PulseAudio):

```
$ padsp OSSprogram

```

A few examples:

```
$ padsp aumix
$ padsp sox foo.wav -t ossdsp /dev/dsp

```

You can also add a custom wrapper script like this:

 `/usr/local/bin/OSSProgram` 
```
#!/bin/sh
exec padsp /usr/bin/OSSprogram "$@"

```

Make sure `/usr/local/bin` comes before `/usr/bin` in your **PATH**.

### GStreamer

Install [gst-plugins-good](https://www.archlinux.org/packages/?name=gst-plugins-good), or [gstreamer0.10-good-plugins](https://www.archlinux.org/packages/?name=gstreamer0.10-good-plugins) if your intended program has a legacy [GStreamer](/index.php/GStreamer "GStreamer") implementation.

### OpenAL

OpenAL Soft should use PulseAudio by default, but can be explicitly configured to do so: `/etc/openal/alsoft.conf`  `drivers=pulse,alsa` 

### libao

Edit the libao configuration file:

 `/etc/libao.conf`  `default_driver=pulse` 

Be sure to remove the `dev=default` option of the alsa driver or adjust it to specify a specific Pulse sink name or number.

**Note:** You could possibly also keep the libao standard of outputting to the *alsa* driver and its default device if you install [pulseaudio-alsa](https://www.archlinux.org/packages/?name=pulseaudio-alsa) since the ALSA default device then **is** PulseAudio.

## Equalizer

**Warning:** The equalizer module is considered unstable and might be removed from PulseAudio. For more, see the [mailing list](https://lists.freedesktop.org/archives/pulseaudio-discuss/2014-March/020174.html).

PulseAudio has an integrated 10-band equalizer system. In order to use the equalizer do the following:

Install [pulseaudio-equalizer](https://www.archlinux.org/packages/?name=pulseaudio-equalizer):

### Load equalizer sink and dbus-protocol module

```
$ pactl load-module module-equalizer-sink
$ pactl load-module module-dbus-protocol

```

### GUI front-end

run:

```
$ qpaeq

```

**Note:** If qpaeq has no effect, install [pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol) and change "ALSA Playback on" to "FFT based equalizer on ..." while the media player is running.

### Load equalizer and dbus module on every boot

Edit the `/etc/pulse/default.pa` or `~/.config/pulse/default.pa` file with your favorite editor and append the following lines:

```
### Load the integrated PulseAudio equalizer and D-Bus module
load-module module-equalizer-sink
load-module module-dbus-protocol

```

**Note:** The equalizer sink needs to be loaded after the master sink is already available.

## Applications

### QEMU

The audio driver used by QEMU is set with the `QEMU_AUDIO_DRV` environment variable:

```
$ export QEMU_AUDIO_DRV=pa

```

Run the following command to get QEMU's configuration options related to PulseAudio:

```
$ qemu-system-x86_64 -audio-help | awk '/Name: pa/' RS=

```

The listed options can be exported as environment variables, for example:

```
$ export QEMU_PA_SINK=alsa_output.pci-0000_04_01.0.analog-stereo.monitor
$ export QEMU_PA_SOURCE=input
```

To get list of the supported emulation audio drivers

```
$ qemu-system-x86_64 -soundhw help

```

To use e.g. `ac97` driver for the guest use the `-soundhw ac97` commnad with QEMU.

**Note:** Video graphic card emulated drivers for the guest machine may also cause a problem with the sound quality. Test one by one to make it work. You can list possible options with `qemu-system-x86_64 -h | grep vga`.

### AlsaMixer.app

Make [alsamixer.app](https://aur.archlinux.org/packages/alsamixer.app/) dockapp for the [windowmaker](https://www.archlinux.org/packages/?name=windowmaker) use pulseaudio, e.g.

```
$ AlsaMixer.app --device pulse

```

Here is a two examples where the first one is for ALSA and the other one is for pulseaudio. You can run multiple instances of it. Use the `-w` option to choose which of the control buttons to bind to the mouse wheel.

```
# AlsaMixer.app -3 Mic -1 Master -2 PCM --card 0 -w 1
# AlsaMixer.app --device pulse -1 Capture -2 Master -w 2

```

**Note:** It can use only those output sinks that set as default.

### XMMS2

Make it switch to pulseaudio output

```
$ nyxmms2 server config output.plugin pulse

```

and to alsa

```
$ nyxmms2 server config output.plugin alsa

```

To make xmms2 use a different output sink, e.g.

```
 $ nyxmms2 server config pulse.sink alsa_output.pci-0000_04_01.0.analog-stereo.monitor

```

See also the official guide [[3]](https://xmms2.org/wiki/Using_the_application).

### KDE Plasma Workspaces and Qt4

PulseAudio will automatically be used by KDE/Qt4 applications. It is supported by default in the KDE sound mixer. For more information see the [KDE page in the PulseAudio wiki](http://www.pulseaudio.org/wiki/KDE). One useful tidbit from that page is to add `load-module module-device-manager` to `/etc/pulse/default.pa`.

If the phonon-gstreamer backend is used for Phonon, GStreamer should also be configured as described in [#GStreamer](#GStreamer).

### Audacious

[Audacious](/index.php/Audacious "Audacious") natively supports PulseAudio. In order to use it, set Audacious Preferences -> Audio -> Current output plugin to 'PulseAudio Output Plugin'.

### Java/OpenJDK 6

Create a wrapper for the Java executable using padsp as seen on the [Java sound with PulseAudio](/index.php/Java#Java_sound_with_PulseAudio "Java") page.

### Music Player Daemon (MPD)

[configure](http://mpd.wikia.com/wiki/PulseAudio) [MPD](/index.php/MPD "MPD") to use PulseAudio. See also [MPD/Tips and Tricks#MPD and PulseAudio](/index.php/MPD/Tips_and_Tricks#MPD_and_PulseAudio "MPD/Tips and Tricks").

### MPlayer

[MPlayer](/index.php/MPlayer "MPlayer") natively supports PulseAudio output with the `-ao pulse` option. It can also be configured to default to PulseAudio output, in `~/.mplayer/config` for per-user, or `/etc/mplayer/mplayer.conf` for system-wide:

 `/etc/mplayer/mplayer.conf`  `ao=pulse` 

### guvcview

[guvcview](https://www.archlinux.org/packages/?name=guvcview) when using the PulseAudio input from a [Webcam](/index.php/Webcam "Webcam") may have the audio input suspended resulting in no audio being recorded. You can check this by executing:

```
$ pactl list sources

```

If the audio source is "suspended" then modifying the following line in `/etc/pulse/default.pa` and changing:

```
load-module module-suspend-on-idle

```

to

```
#load-module module-suspend-on-idle

```

And then either restarting PulseAudio or your computer will only idle the input source instead of suspending it. guvcview will then correctly record audio from the device.

## Tips and tricks

### Keyboard volume control

Map the following commands to your volume keys: `XF86AudioRaiseVolume`, `XF86AudioLowerVolume`, `XF86AudioMute`

First find out which sink corresponds to the audio output you'd like to control. To list available sinks:

```
pactl list sinks short

```

Suppose sink 0 is to be used, to raise the volume:

```
sh -c "pactl set-sink-mute 0 false ; pactl set-sink-volume 0 +5%"

```

To lower the volume:

```
sh -c "pactl set-sink-mute 0 false ; pactl set-sink-volume 0 -5%"

```

To mute/unmute the volume:

```
pactl set-sink-mute 0 toggle

```

To mute/unmute the microphone:

```
pactl set-source-mute 1 toggle

```

### Play sound from a non-interactive shell (systemd service, cron)

Set `XDG_RUNTIME_DIR` before the command (replace `*user_id*` with the ID of the user running PulseAudio):

```
XDG_RUNTIME_DIR=/run/user/*user_id* paplay /usr/share/sounds/freedesktop/stereo/complete.oga

```

Or use `machinectl`:

```
# machinectl shell .host --uid=*user_id* /usr/bin/paplay /usr/share/sounds/freedesktop/stereo/complete.oga

```

### X11 Bell Events

To get pulseaudio to handle X11 bell events, run the following commands after the X11 session has been started:

```
pactl upload-sample /usr/share/sounds/freedesktop/stereo/bell.oga x11-bell
pactl load-module module-x11-bell sample=x11-bell display=$DISPLAY

```

To adjust the volume of the X11 bell, run the following command:

```
xset b 100

```

100 is a percentage. This requires the [xorg-xset](https://www.archlinux.org/packages/?name=xorg-xset) package. See [Autostarting](/index.php/Autostarting "Autostarting") for a way to run these commands automatically when the X11 session is started.

### Switch on connect

This is a module used to switch the output sound to the newly connected device. For example, if you plug in a USB headset, the output will be switched to that. If you unplug it, the output will be set back to the last device. This used to be quite buggy but got a lot of attention in PulseAudio 8.0 and should work quite well now.

If you just want to test the module then you can load it at runtime by calling:

```
# pactl load-module module-switch-on-connect

```

If you want to make the change persistent you will have to add it to your local pulseaudio settings or to /etc/pulse/default.pa (system wide effect). In either case, add this line:

```
load-module module-switch-on-connect

```

On KDE/Plasma5 you should furthermore disable module-device-manager. As soon as Plasma5 is started it loads (via start-pulseaudio-x11) the module module-device-manager for pulseaudio to manage the devices. But that module apparently conflicts with module-switch-on-connect. Therefore you should disable that module by editing /bin/start-pulseaudio-x11 and commenting the lines for KDE. Simply logout and login again and in order to renew your pulseaudio session. On connect switching should now work properly.

## Troubleshooting

See [PulseAudio/Troubleshooting](/index.php/PulseAudio/Troubleshooting "PulseAudio/Troubleshooting").

## See also

*   [.asoundrc on ALSA wiki](http://www.alsa-project.org/main/index.php/Asoundrc)
*   [PulseAudio official site](http://www.pulseaudio.org/)
*   [PulseAudio FAQ](http://www.freedesktop.org/wiki/Software/PulseAudio/FAQ/)