Related articles

*   [Sound system](/index.php/Sound_system "Sound system")
*   [Professional audio](/index.php/Professional_audio "Professional audio")

From [Wikipedia:JACK Audio Connection Kit](https://en.wikipedia.org/wiki/JACK_Audio_Connection_Kit "wikipedia:JACK Audio Connection Kit"):

	JACK Audio Connection Kit (or JACK; a recursive acronym) is a professional sound server daemon that provides real-time, low-latency connections for both audio and MIDI data between applications that implement its API.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 JACK2](#JACK2)
    *   [1.2 JACK](#JACK)
    *   [1.3 GUI](#GUI)
*   [2 Basic Configuration](#Basic_Configuration)
    *   [2.1 Overview](#Overview)
    *   [2.2 A shell-based example setup](#A_shell-based_example_setup)
        *   [2.2.1 Details of the shell-based example setup](#Details_of_the_shell-based_example_setup)
    *   [2.3 A GUI-based example setup](#A_GUI-based_example_setup)
    *   [2.4 An alternative GUI-based setup](#An_alternative_GUI-based_setup)
    *   [2.5 Playing nice with ALSA](#Playing_nice_with_ALSA)
    *   [2.6 GStreamer](#GStreamer)
    *   [2.7 PulseAudio](#PulseAudio)
    *   [2.8 Firewire](#Firewire)
    *   [2.9 Network / remote audio](#Network_/_remote_audio)
*   [3 MIDI](#MIDI)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 "Cannot lock down memory area (Cannot allocate memory)" message on startup](#"Cannot_lock_down_memory_area_(Cannot_allocate_memory)"_message_on_startup)
    *   [4.2 jack2 and qjackctl errors](#jack2_and_qjackctl_errors)
    *   [4.3 "ALSA: cannot set channel count to 1 for capture" error in logs](#"ALSA:_cannot_set_channel_count_to_1_for_capture"_error_in_logs)
    *   [4.4 Crackling or pops in audio](#Crackling_or_pops_in_audio)
    *   [4.5 Problems with specific applications](#Problems_with_specific_applications)
        *   [4.5.1 VLC - no audio after starting JACK](#VLC_-_no_audio_after_starting_JACK)
*   [5 See also](#See_also)

## Installation

In order for JACK to work properly, your user needs to be [added](/index.php/Users_and_groups#Group_management "Users and groups") to the `realtime` group for access to higher ulimits defined in `/etc/security/limits.d/99-realtime-privileges.conf` (provided by the [realtime-privileges](https://www.archlinux.org/packages/?name=realtime-privileges) package), which is needed for realtime audio processing.

**Note:** You need to manually add your user to the `realtime` group even if you're using logind, since logind just handles access to direct hardware.

There are two JACK implementations, see [this comparison](https://github.com/jackaudio/jackaudio.github.com/wiki/Q_difference_jack1_jack2) for the difference between the two. In short, Jack 1 and Jack 2 are equivalent implementations of the same protocol. Programs compiled against Jack 1 will work with Jack 2 without recompile (and vice versa).

### JACK2

**JACK2** is a C++ implementation with SMP support. [Install](/index.php/Install "Install") it with the [jack2](https://www.archlinux.org/packages/?name=jack2) package. For 32-bit application support, also install the [lib32-jack2](https://www.archlinux.org/packages/?name=lib32-jack2) package from the [multilib](/index.php/Multilib "Multilib") repository. To use the *jack_control* command, also install the [python-dbus](https://www.archlinux.org/packages/?name=python-dbus) package.

### JACK

**JACK** uses a C API and supports more than one soundcard on Linux (plus MIDI). [Install](/index.php/Install "Install") it with the [jack](https://www.archlinux.org/packages/?name=jack) package. For 32-bit application support, also install the [lib32-jack](https://www.archlinux.org/packages/?name=lib32-jack) package from the [multilib](/index.php/Multilib "Multilib") repository.

### GUI

*   **Cadence** — Set of tools useful for audio production. It performs system checks, manages JACK, calls other tools and make system tweaks.

	[https://kx.studio/Applications:Cadence](https://kx.studio/Applications:Cadence) || [cadence](https://www.archlinux.org/packages/?name=cadence)

*   **Patchage** — Modular patch bay for audio and MIDI systems based on JACK and ALSA.

	[https://drobilla.net/software/patchage](https://drobilla.net/software/patchage) || [patchage](https://www.archlinux.org/packages/?name=patchage)

*   **PatchMatrix** — JACK patch bay in flow matrix style.

	[https://git.open-music-kontrollers.ch/lad/patchmatrix/about/](https://git.open-music-kontrollers.ch/lad/patchmatrix/about/) || [patchmatrix](https://www.archlinux.org/packages/?name=patchmatrix)

*   **QjackCtl** — Simple Qt application to control the JACK sound server daemon.

	[https://qjackctl.sourceforge.io/](https://qjackctl.sourceforge.io/) || [qjackctl](https://www.archlinux.org/packages/?name=qjackctl)

## Basic Configuration

### Overview

The right configuration for your hardware and application needs depends on several factors. Your sound card and CPU will heavily affect how low of latency you can achieve when using JACK.

The mainline Linux kernel now supports realtime scheduling, so using a patched kernel is no longer necessary. However, [linux-rt](https://aur.archlinux.org/packages/linux-rt/) in the AUR is a patched kernel that has some extra patches that can help to get lower latencies.

### A shell-based example setup

JACK2 can be directly launched with the *jackd* executable, or controlled with the D-Bus-based *jack_control* binary. *jack_control* makes it easy to start and configure JACK2 via a shell script. Note that you must install the [python-dbus](https://www.archlinux.org/packages/?name=python-dbus) package to use *jack_control*.

Create a shell script that can be executed at X login:

 `start_jack.sh` 
```
#!/bin/bash

jack_control start
jack_control ds alsa
jack_control dps device hw:HD2
jack_control dps rate 48000
jack_control dps nperiods 2
jack_control dps period 64
sleep 10
a2jmidid -e &
sleep 10
qjackctl &

```

The above will start a working JACK instance which other programs can then utilize. Details of each line follow. When discovering your own best configuration, it is helpful to do trial and error using QjackCtl's GUI with a non-D-Bus JACK2 version.

#### Details of the shell-based example setup

```
jack_control start

```

Starts JACK if it is not already started.

```
jack_control ds alsa

```

Sets JACK to use the ALSA driver set.

```
jack_control dps device hw:HD2

```

Sets JACK to use ALSA-compatible sound card named HD2\. One can find the names with `cat /proc/asound/cards`. Most ALSA tutorials and default configurations use card numbers, but this can get confusing when external MIDI devices are in use; names make it easier.

```
jack_control dps rate 48000

```

Sets JACK to use 48000 khz sampling. Happens to work very well with this card. Some cards only do 44100, many will go much higher. The higher you go, the lower your latency, but the better your card and your CPU have to be, and software has to support this as well.

```
jack_control dps nperiods 2

```

Sets JACK to use 2 periods. 2 is right for motherboard, PCI, PCI-X, etc.; 3 for USB.

```
jack_control dps period 64

```

Sets JACK to use 64 frames per period. Lower is less latency, but the setting in this script gives 2.67 ms latency, which is nicely low without putting too much stress on the particular hardware this example was built for. If a USB sound system were in use it might be good to try 32\. Anything less than 3-4 ms should be fine for realtime synthesis and/or FX, 5 ms is the smallest a human being can detect. QjackCtl will tell you how you are doing; at no-load, which means no clients attached, you will want a max of 3-5% CPU usage, and if you cannot get that without xruns (the red numbers which mean the system cannot keep up with the demands), you will have to improve your hardware.

```
sleep 10

```

Wait for the above to settle.

```
a2jmidid -e &

```

Start the ALSA-to-JACK MIDI bridge. Good for mixing in applications which take MIDI input through ALSA but not JACK.

```
sleep 10

```

Wait for the above to settle.

```
qjackctl &

```

Load QjackCtl. GUI configuration tells it to run in the system tray. It will pick up the JACK session started by D-Bus just fine, and very smoothly too. It maintains the patchbay, the connections between these applications and any other JACK-enabled apps to be started manually. The patchbay is set up using manual GUI, but connections pre-configured in the patchbay are automatically created by QjackCtl itself when apps are started.

### A GUI-based example setup

This example setup utilizes a more GUI focused configuration and management of JACK

*   Install [jack2](https://www.archlinux.org/packages/?name=jack2) and [python-dbus](https://www.archlinux.org/packages/?name=python-dbus).
*   Install [qjackctl](https://www.archlinux.org/packages/?name=qjackctl), and tell your GUI window/desktop system to run it at startup.
*   Make sure QjackCtl is told to:
    *   use the D-Bus interface,
    *   run at startup,
    *   save its configuration to the default location,
    *   start the JACK audio server on application startup,
    *   enable the system tray icon, and
    *   start minimized to system tray.
*   Reboot.
*   After logging in, you will see QjackCtl in your system tray. Left-click on it.
*   Tweak settings in the QjackCtl GUI to lower latency. The Frame Size, Frame Buffer, and Bitrate settings all affect latency. Larger frame sizes lower latency, lower frame buffers lower latency, and higher bitrate settings lower latency, but all increase load on the sound card and your CPU. A Latency of about ~5ms is desirable for direct monitoring of instruments or microphones, as the latency begins to become perceptible at higher latencies.

### An alternative GUI-based setup

If you use JACK for demanding tasks , but every now and then, it's possible to suspend a running pulseaudio session with QjackCtl just when you're using it. On a virgin config, modify the "Server prefix" option in the "Settings" > "Advanced" submenu, so that it states :

```
   pasuspender -- jackd

```

The pulseaudio session should resume fine after you close QjackCtl. Tip courtesy of [this post](https://bbs.archlinux.org/viewtopic.php?pid=1163340#p1163340).

### Playing nice with ALSA

**Note:** There are several bugs in [alsa-lib](https://www.archlinux.org/packages/?name=alsa-lib) and [alsa-plugins](https://www.archlinux.org/packages/?name=alsa-plugins) 1.1.9-2 that will cause audio to not play or errors regarding buffers with this setup. Please read [[1]](https://bbs.archlinux.org/viewtopic.php?id=250116) for workarounds and potential solutions.

To allow Alsa programs to play while jack is running you must install the jack plugin for alsa with [alsa-plugins](https://www.archlinux.org/packages/?name=alsa-plugins).

And enable it by editing (or creating) /etc/asound.conf (system wide settings) to have these lines if you have a simple 2-channel setup:

```
# convert alsa API over jack API
# use it with
# % aplay foo.wav

# use this as default
pcm.!default {
    type plug
    slave.pcm "jack"
    hint.description "Jack Audio"
}
```

If you have a different number of output/input channels or your first two channels aren't the ones you wish to route audio to, you cannot use the predefined jack pcm source from `/etc/alsa/conf.d/50-jack.conf`, but rather something like:

```
# the first jack port goes to an output we don't use and there are no recording devices
pcm.!jack {
   type jack
       playback_ports {
           0 system:playback_2
           1 system:playback_3
       }
}

pcm.!default {
    type plug
    slave.pcm "jack"
    hint.description "Jack Audio"
}
```

You need not restart your computer or anything. Just edit the alsa config files, start up jack, and there you go...

Remember to start it as a **user**. If you start it with `jackd` -d alsa" as user X, it will not work for user Y.

Another approach, using ALSA loopback device (more complex but probably more robust), is described in [this article](https://alsa.opensrc.org/Jack_and_Loopback_device_as_Alsa-to-Jack_bridge).

### GStreamer

GStreamer requires the [gst-plugins-good](https://www.archlinux.org/packages/?name=gst-plugins-good) package to work with JACK, which contains the jackaudiosink plugin that adds JACK playback support.

Further information (outdated): [http://jackaudio.org/faq/gstreamer_via_jack.html](http://jackaudio.org/faq/gstreamer_via_jack.html)

### PulseAudio

If you need to keep [pulseaudio](https://www.archlinux.org/packages/?name=pulseaudio) installed (in the event it is required by other packages, like [gnome-settings-daemon](https://www.archlinux.org/packages/?name=gnome-settings-daemon)), you may want to prevent it from spawning automatically with X and taking over from JACK.

Edit `/etc/pulse/client.conf`, uncomment "autospawn" and set it to "no":

```
;autospawn = yes
autospawn = no

```

*If you want both to play along, see: [PulseAudio/Examples#PulseAudio through JACK](/index.php/PulseAudio/Examples#PulseAudio_through_JACK "PulseAudio/Examples")*

### Firewire

In order to prevent ALSA from messing around with your firewire devices you have to blacklist all firewire related kernel modules. This also prevents PulseAudio from using firewire. Create the following file:

 `/etc/modprobe.d/alsa-no-jack.conf` 
```
blacklist snd-fireworks
blacklist snd-bebob
blacklist snd-oxfw
blacklist snd-dice
blacklist snd-firewire-digi00x
blacklist snd-firewire-tascam
blacklist snd-firewire-lib
blacklist snd-firewire-transceiver
blacklist snd-fireface
blacklist snd-firewire-motu

```

*The list of modules is the most recent available at the time of writing at [Alsa Firewire Improve Repository](https://github.com/takaswie/snd-firewire-improve).*

Now you can unload your loaded firewire modules or reboot.

### Network / remote audio

JACK can be configured to send audio data over a network to a "master" machine, which then outputs the audio to a physical device. This can be useful to mix audio from a number of "slave" computers without requiring additional cables or hardware mixers, and keeping the audio path digital for as long as possible (as hardware mixers with digital inputs are very rare).

The configuration is very simple, however it requires a network that supports multicast traffic (i.e. IGMP snooping must be enabled on managed network switches), and it requires all machines be running the same JACK major version (JACK1 or JACK2) as the protocols are not interoperable between versions. For JACK2, the `netmanager` module must be loaded:

```
master$ jack_load netmanager -i -c

```

The `-i -c` option tells the netmanager to automatically map any incoming connections to the default audio device. Without this, each incoming connection would have to be manually mapped on each connection. You can use `-i -h` instead to see all available options, however note that the options are printed in the `jackd` server output, the `jack_load` command will not show anything.

On the client, JACK must be started in network mode:

```
slave$ jackd -d net

```

The two machines will connect and on the master the new audio source will be visible:

```
master$ jack_lsp
system:playback_1
system:playback_2
remotehost:from_slave_1
remotehost:from_slave_2

```

If you passed the `-c` option to `jack_load` as above, then the remote system will now be able to play audio.

## MIDI

JACK can handle one soundcard very well, and an arbitrary number of MIDI devices (connected e.g. via USB). If you start JACK and want to use a MIDI keyboard or a synthesizer or some other pure MIDI device, you have to start JACK with a proper soundcard (one that actually outputs or inputs PCM sound). As soon you have done that, you can connect the MIDI device. E.g. with QjackCtl ([qjackctl](https://www.archlinux.org/packages/?name=qjackctl)), you click on the connect button and you will find your device listed under JACK-MIDI or ALSA-MIDI, depending on the driver.

For JACK-MIDI, you may want to set the **MIDI Driver** to **seq** or **raw** in QjackCtl *Setup > Settings*. This should make your MIDI device appear under the *MIDI* tab. You can also change the name of the client (from a generic "midi_capture_1" to something more descriptive), if you enable *Setup > Display > Enable client/port aliases* and then *Enable client/port aliases editing (rename)*.

For ALSA-MIDI, make sure to turn on **Enable ALSA Sequencer support** in QjackCtl *Setup > Misc*. This will add the *ALSA* tab in QjackCtl *Connect* window where your MIDI controller will show up.

**Note:** [jack2](https://www.archlinux.org/packages/?name=jack2) does not come with bridging support for legacy ALSA MIDI only applications. Therefore [a2jmidid](https://www.archlinux.org/packages/?name=a2jmidid) is required [until upstream achieves feature parity on this](https://github.com/jackaudio/jack2/issues/362).

For bridging ALSA-MIDI to JACK-MIDI, you may consider using a2jmidid ([a2jmidid](https://www.archlinux.org/packages/?name=a2jmidid)). The following command will export all available ALSA MIDI ports to JACK MIDI ports:

```
$ a2jmidid -e

```

They will be visible in QjackCtl under the *MIDI* tab labelled "a2j" client. You can automate starting of a2jmidid by adding to QjackCtl *Setup > Options > Execute script after Startup*: `/usr/bin/a2jmidid -e &`

**Note:** When connecting MIDI keyboard controllers in QjackCtl, make sure to *Expand All* first and connect the desired *Output Ports* (below the *Readable Clients*) to the *Input Ports* (below the *Writable Clients*). As a shortcut, if you select a writable client instead of individual ports as your destination, it should connect all its currently displayed output ports underneath.

*   **Q:** What is the difference between JACK-MIDI and ALSA-MIDI?
*   **A:** The former has improved timing and sample accurate MIDI event alignment. It extends or may even replace the latter but at this point they both co-exist.

To install some M-Audio MIDI keyboards, you will need the firmware package [midisport-firmware](https://aur.archlinux.org/packages/midisport-firmware/) in the [AUR](/index.php/AUR "AUR"). Also, the snd_usb_audio module has to be available. For more information about specific USB MIDI devices, see [http://alsa.opensrc.org/USBMidiDevices](http://alsa.opensrc.org/USBMidiDevices).

## Troubleshooting

### "Cannot lock down memory area (Cannot allocate memory)" message on startup

See [Realtime process management#Configuring PAM](/index.php/Realtime_process_management#Configuring_PAM "Realtime process management") and ensure that the user is in the `realtime` [user group](/index.php/User_group "User group").

### jack2 and qjackctl errors

Still having the "Cannot allocate memory" and/or "Cannot connect to server socket err = No such file or directory" error(s) when pressing qjackctl's start button?

Please delete `~/.jackdrc`, `~/.config/jack/conf.xml`, `~/.config/rncbc.org/QjackCtl.conf`. Kill *jackdbus* and restart from scratch :) (Thanks to nedko)

Also try running

```
$ fuser /dev/snd/*

```

and check the resulting PID's with

```
$ ps ax | grep [PID here]

```

This will hopefully show the conflicting programs.

### "ALSA: cannot set channel count to 1 for capture" error in logs

Change ALSA input and output channels from 1 to 2

### Crackling or pops in audio

Your CPU or sound card is too weak to handle your settings for JACK. Lower the bitrate, lower the frame size, and raise the frame period in small increments until crackling stops. You can also try changing the sampling rate to 44100 or whatever is natively supported. This allows jack to send audio to the system without having to resample. In [jack2](https://www.archlinux.org/packages/?name=jack2) with `jack_control`, this is accomplished with

```
jack_control dps rate 44100

```

### Problems with specific applications

#### VLC - no audio after starting JACK

Run VLC and change the following menu options:

*   Tools > Preferences
*   Show settings: All
*   Audio > Output modules > Audio output module: JACK audio output
*   Audio > Output modules > JACK: Automatically connect to writable clients (enable)

## See also

*   [Differences between JACK 1 and JACK2](https://github.com/jackaudio/jackaudio.github.com/wiki/Q_difference_jack1_jack2)
*   [JACK FAQ](http://jackaudio.org/faq/)