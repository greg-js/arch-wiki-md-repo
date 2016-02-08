# PulseAudio/Examples

## Contents

*   [1 Set default input sources](#Set_default_input_sources)
*   [2 Set the defaulting output source](#Set_the_defaulting_output_source)
*   [3 Simultaneous HDMI and analog output](#Simultaneous_HDMI_and_analog_output)
*   [4 HDMI output configuration](#HDMI_output_configuration)
    *   [4.1 Finding HDMI output](#Finding_HDMI_output)
    *   [4.2 Testing for the correct card](#Testing_for_the_correct_card)
    *   [4.3 Manually configuring PulseAudio to detect the Nvidia HDMI](#Manually_configuring_PulseAudio_to_detect_the_Nvidia_HDMI)
    *   [4.4 Automatically switch audio to HDMI](#Automatically_switch_audio_to_HDMI)
*   [5 Surround sound systems](#Surround_sound_systems)
    *   [5.1 Splitting front/rear](#Splitting_front.2Frear)
    *   [5.2 Splitting 7.1 into 5.1+2.0](#Splitting_7.1_into_5.1.2B2.0)
    *   [5.3 Disabling LFE remixing](#Disabling_LFE_remixing)
*   [6 PulseAudio over network](#PulseAudio_over_network)
    *   [6.1 TCP support (networked sound)](#TCP_support_.28networked_sound.29)
    *   [6.2 TCP support with anonymous clients](#TCP_support_with_anonymous_clients)
    *   [6.3 Zeroconf (Avahi) publishing](#Zeroconf_.28Avahi.29_publishing)
    *   [6.4 Switching the PulseAudio server used by local X clients](#Switching_the_PulseAudio_server_used_by_local_X_clients)
    *   [6.5 When everything else seems to fail](#When_everything_else_seems_to_fail)
*   [7 ALSA monitor source](#ALSA_monitor_source)
*   [8 Monitor specific output](#Monitor_specific_output)
*   [9 PulseAudio through JACK](#PulseAudio_through_JACK)
    *   [9.1 The new new way](#The_new_new_way)
    *   [9.2 The new way](#The_new_way)
    *   [9.3 The old way](#The_old_way)
        *   [9.3.1 QjackCtl with start-up/shutdown scripts](#QjackCtl_with_start-up.2Fshutdown_scripts)
*   [10 PulseAudio through OSS](#PulseAudio_through_OSS)
*   [11 PulseAudio from within a chroot (e.g. 32-bit chroot in 64-bit install)](#PulseAudio_from_within_a_chroot_.28e.g._32-bit_chroot_in_64-bit_install.29)
*   [12 Disabling automatic spawning of PulseAudio server](#Disabling_automatic_spawning_of_PulseAudio_server)
*   [13 Disabling pulseaudio daemon altogether](#Disabling_pulseaudio_daemon_altogether)
*   [14 Remap stereo to mono](#Remap_stereo_to_mono)
*   [15 Swap left/right channels](#Swap_left.2Fright_channels)
*   [16 PulseAudio as a minimal unintrusive dumb pipe to ALSA](#PulseAudio_as_a_minimal_unintrusive_dumb_pipe_to_ALSA)

## Set default input sources

List available input sources

 `$ pacmd list-sources | grep -e device.string -e 'name:'` 

```
name: <input>
 device.string = "hw:2"
name: <oss_input.dsp>
 device.string = "/dev/dsp"
name: <alsa_output.pci-0000_04_01.0.analog-stereo.monitor>
name: <combined.monitor>
```

For permanent store in the _default.pa_ file.

Set OSS as input

```
load-module module-oss device=/dev/dsp sink_name=alsa_output.pci-0000_04_01.0.analog-stereo mmap=1

```

Make it default

```
set-default-source alsa_output.pci-0000_04_01.0.analog-stereo.monitor

```

Set ALSA as input

```
load-module module-alsa-source source_name=input device=hw:2

```

Make it default

```
set-default-source input

```

For temporary use

```
$ pacmd "load-module module-alsa-source source_name=input device=hw:2"
$ pacmd "set-default-source input"

```

## Set the defaulting output source

**Note:** Use aplay to list devices that is a part of the [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils) package and is not required to output to multiple sources. It is required to list playback devices therefore users can remove this package when finished with it.

To select an alternative source as the default output you can list all sources:

 `$ aplay -l | grep card` 

```
card 0: CMI8768 [C-Media CMI8768], device 0: CMI8738-MC8 [C-Media PCI DAC/ADC]
card 0: CMI8768 [C-Media CMI8768], device 1: CMI8738-MC8 [C-Media PCI 2nd DAC]
card 0: CMI8768 [C-Media CMI8768], device 2: CMI8738-MC8 [C-Media PCI IEC958]
card 1: HDMI [HDA Intel HDMI], device 3: HDMI 0 [HDMI 0]
card 1: HDMI [HDA Intel HDMI], device 7: HDMI 1 [HDMI 1]
card 1: HDMI [HDA Intel HDMI], device 8: HDMI 2 [HDMI 2]
```

To chose _card 0, device 0_ edit the `/etc/pulse/default.pa` file and add

```
load-module module-alsa-sink device=hw:0,0

```

Determine the name of the new source, which has a * in front of index:

 `$ pacmd list-sinks | grep -e 'name:' -e 'index'` 

```
  * index: 0
	name: <alsa_output.pci-0000_04_01.0.analog-stereo>
    index: 1
	name: <combined>

```

For setting it as default in the `/etc/pulse/default.pa` you can use

```
set-default-sink alsa_output.pci-0000_04_01.0.analog-stereo

```

When done then you can logout/login or restart PulseAudio manually for these changes to take effect.

**Note:**

*   The sinks that are set as default are marked with `*` in front of the index.
*   The numbering of sinks is not guaranteed to be persistent, so all sinks in the `default.pa` file should be identified by the name.
*   For quick identification at runtime (e.g. to manage sound volume), you can use the sink index instead of the sink name:

    ```
    $ pactl set-sink-volume 0 +3%
    $ pactl set-sink-volume 0 -- -3%
    $ pactl set-sink-mute 0 toggle

    ```

*   To avoid unnecessary overriding of 100% normal volume it is better to use alternative utilities for managing of sound. See the [forum thread](https://bbs.archlinux.org/viewtopic.php?id=124513) for more information.

## Simultaneous HDMI and analog output

PulseAudio allows for simultaneous output to multiple sources. In this example, some applications are configured to use HDMI while others are configured to use analog. Multiple applications are able to receive audio at the same time.

```
$ aplay -l
**** List of PLAYBACK Hardware Devices ****
card 0: Intel [HDA Intel], device 0: ALC889A Analog [ALC889A Analog]
  Subdevices: 0/1
  Subdevice #0: subdevice #0
card 0: Intel [HDA Intel], device 1: ALC889A Digital [ALC889A Digital]
  Subdevices: 1/1
  Subdevice #0: subdevice #0
card 0: Intel [HDA Intel], device 3: HDMI 0 [HDMI 0]
  Subdevices: 0/1
  Subdevice #0: subdevice #0
```

Or by using the the `pacmd` command:

 `$ pacmd list-sinks  | grep -e 'name:'  -e 'alsa.device ' -e 'alsa.subdevice '` 

```
	name: <alsa_output.pci-0000_00_1b.0.analog-stereo>
		alsa.subdevice = "0"
		alsa.device = "0"
```

The key to a configuration like this is to understand that whatever is selected in pavucontrol under _Configuration > Internal Audio_ is the default device. Load _pavucontrol > Configuration_ and select HDMI as the profile.

To setup the analog device as a secondary source, add the following to the `/etc/pulse/default.pa` configuration at the beginning, before any other modules are loaded:

```
### Load analog device
load-module module-alsa-sink device=hw:0,0
load-module module-combine-sink sink_name=combined
set-default-sink combined

```

Restart PulseAudio, run _pavucontrol_ and select the "Output Devices" tab. Three settings should be displayed:

1.  Internal Audio Digital Stereo (HDMI)
2.  Internal Audio
3.  Simultaneous output to Internal Audio Digital Stereo (HDMI), Internal Audio

Now start a program that will use PulseAudio such as MPlayer, VLC, mpd, etc. and switch to the "Playback" tab. A drop-down list should be available for the running program to select one of the three sources.

Also see [this thread](https://bbs.archlinux.org/viewtopic.php?id=118026) for a variation on this theme and [PulseAudio FAQ](http://www.freedesktop.org/wiki/Software/PulseAudio/FAQ#Can_I_use_PulseAudio_to_playback_music_on_two_sound_cards_simultaneously.3F).

## HDMI output configuration

As outlined in [ftp://download.nvidia.com/XFree86/gpu-hdmi-audio-document/gpu-hdmi-audio.html#_issues_in_pulseaudio](ftp://download.nvidia.com/XFree86/gpu-hdmi-audio-document/gpu-hdmi-audio.html#_issues_in_pulseaudio) unless the HDMI port is the first output, PulseAudio will not be able to have any audio when using certain graphics cards with HDMI audio support. This is because of a bug in PulseAudio where it will only select the first HDMI output on a device. A work around posted further down is to first find which HDMI output is working by using the aplay utility from ALSA.

The original title for this section indicated the problem is specific to nVidia cards. As seen in [this forum thread](https://bbs.archlinux.org/viewtopic.php?id=133222) other cards are affected as well. The rest of the section will use an nVidia card as a case-study but the solution should carry over for people using other affected cards.

### Finding HDMI output

Then find the working output by listing the available cards

```
# aplay -l

```

```
sample output:
 **** List of PLAYBACK Hardware Devices ****
 card 0: NVidia [HDA NVidia], device 0: ALC1200 Analog [ALC1200 Analog]
   Subdevices: 1/1
   Subdevice #0: subdevice #0
 card 0: NVidia [HDA NVidia], device 3: ALC1200 Digital [ALC1200 Digital]
   Subdevices: 1/1
   Subdevice #0: subdevice #0
 card 1: NVidia_1 [HDA NVidia], device 3: HDMI 0 [HDMI 0]
   Subdevices: 1/1
   Subdevice #0: subdevice #0
 card 1: NVidia_1 [HDA NVidia], device 7: HDMI 0 [HDMI 0]
   Subdevices: 0/1
   Subdevice #0: subdevice #0
 card 1: NVidia_1 [HDA NVidia], device 8: HDMI 0 [HDMI 0]
   Subdevices: 1/1
   Subdevice #0: subdevice #0
 card 1: NVidia_1 [HDA NVidia], device 9: HDMI 0 [HDMI 0]
   Subdevices: 1/1
   Subdevice #0: subdevice #0

```

### Testing for the correct card

Now a list of the detected cards is known, users will need to test for which one is outputting to the TV/monitor

```
# aplay -D plughw:1,3 /usr/share/sounds/alsa/Front_Right.wav

```

where 1 is the card and 3 is the device substitute in the values listed from the previous section. If there is no audio, then try substituting a different device (on my card I had to use card 1 device 7)

### Manually configuring PulseAudio to detect the Nvidia HDMI

Having identified which HDMI device is working, PulseAudio can be forced to use it via an edit to `/etc/pulse/default.pa`:

```
# load-module module-alsa-sink device=hw:1,7

```

where the 1 is the card and the 7 is the device found to work in the previous section

restart pulse audio

```
 $ pulseaudio -k
 $ pulseaudio --start

```

open the sound settings manager, make sure that under the hardware tab the graphics cards HDMI audio is set to "Digital Stereo (HDMI) Output" (My graphics card audio is called "GF100 High Definition Audio Controller").

Then, open the output tab. There should now be two HDMI outputs for the graphics card. Test which one works by selecting one of them, and then using a program to play audio. For example, use VLC to play a movie, and if it does not work, then select the other.

### Automatically switch audio to HDMI

Create a script to switch to the desired audio profile if an HDMI cable is plugged in:

 `/usr/local/bin/hdmi_sound_toggle.sh` 

```
#!/bin/bash
USER_NAME=$(w -hs | awk -v vt=tty$(fgconsole) '$0 ~ vt {print $1}')
USER_ID=$(id -u "$USER_NAME")
HDMI_STATUS=$(</sys/class/drm/card0/*HDMI*/status)

export PULSE_SERVER="unix:/run/user/"$USER_ID"/pulse/native"

if [[ $HDMI_STATUS == connected ]]
then
   sudo -u "$USER_NAME" pactl --server "$PULSE_SERVER" set-card-profile 0 output:hdmi-stereo+input:analog-stereo
else
   sudo -u "$USER_NAME" pactl --server "$PULSE_SERVER" set-card-profile 0 output:analog-stereo+input:analog-stereo
fi

```

Make the script executable:

```
chmod +x /usr/local/bin/hdmi_sound_toggle.sh

```

Create a udev rule to run this script when the status of the HDMI change:

**Note:** udev rule can't directly run a script, a workaround is to use a .service to run this script

 `/etc/udev/rules.d/99-hdmi_sound.rules`  `KERNEL=="card0", SUBSYSTEM=="drm", ACTION=="change", RUN+="/usr/bin/systemctl start hdmi_sound_toggle.service"` 

Finally, create the .service file required by the udev rule above:

 `/etc/systemd/system/hdmi_sound_toggle.service` 

```
[Unit]
Description=hdmi sound hotplug

[Service]
Type=simple
RemainAfterExit=no
ExecStart=/usr/local/bin/hdmi_sound_toggle.sh

[Install]
WantedBy=multi-user.target
```

To make the change effective don't forget to reload the udev rules:

```
udevadm control --reload-rules

```

A reboot can be required.

## Surround sound systems

Many people have a surround sound card, but have speakers for just two channels, so PulseAudio cannot really default to a surround sound setup. To enable all of the channels, edit `/etc/pulse/daemon.conf`: uncomment the default-sample-channels line (i.e. remove the semicolon from the beginning of the line) and set the value to **6**. For a _5.1_ setup, or **8** for a _7.1_ setup etc.

```
# Default
default-sample-channels=2
# For 5.1
default-sample-channels=6
# For 7.1
default-sample-channels=8

```

If your channels are not correclty mapped or the volume controls for the individual channels do not work as expected in pavucontrol, and you have a HDMI and an anlog soundcard, then try to add the following line to `/etc/pulse/default.pa`

```
load-module module-combine channels=6 channel_map=front-left,front-right,rear-left,rear-right,front-center,lfe

```

Note that this example is for a 5.1 setup.

After doing the edit, restart PulseAudio.

### Splitting front/rear

Connect speakers to front analog output and headphones to rear output. It would be useful to split front/rear to separate sinks. Add to `/etc/pulse/default.pa`:

```
 load-module module-remap-sink sink_name=speakers remix=no master=alsa_output.pci-0000_05_00.0.analog-surround-40 channels=2 master_channel_map=front-left,front-right channel_map=front-left,front-right
 load-module module-remap-sink sink_name=headphones remix=no master=alsa_output.pci-0000_05_00.0.analog-surround-40 channels=2 master_channel_map=rear-left,rear-right channel_map=front-left,front-right

```

Make sure to replace alsa_output.pci-0000_05_00.0.analog-surround-40 with the sound card name shown in 'pacmd list-sinks'. Now you have 2 additional sinks which can be used separately. You can choose 'sink_name' freely, as long as there is no sink with that name already. The 'remix' parameter controls whether the audio should be down-/upmixed to match the channels in the sink.

**Tip:** If pulseaudio fails with `master sink not found`, comment out the remapping lines, start PulseAudio and verify your card output is set to the one you specified (e.g. analog surround 4.0). Alternatively, try using a [sink index](#Set_the_defaulting_output_source) instead of a sink name.

### Splitting 7.1 into 5.1+2.0

Similar to the example above, you can also split a 7.1 configuration into 5.1 surround and stereo output devices. Set your card to 7.1 mode, then add the following lines to `/etc/pulse/default.pa`:

```
 load-module module-remap-sink sink_name=Surround remix=no master=alsa_output.pci-0000_00_14.2.analog-surround-71 channels=6 master_channel_map=front-left,front-right,rear-left,rear-right,front-center,lfe channel_map=front-left,front-right,rear-left,rear-right,front-center,lfe
 load-module module-remap-sink sink_name=Stereo remix=yes master=alsa_output.pci-0000_00_14.2.analog-surround-71 channels=2 master_channel_map=front-left,front-right channel_map=front-left,front-right

```

Make sure to replace alsa_output.pci-0000_00_14.2 with your sound card name, get it by running 'pacmd list-sinks'. This configuration will use the front/rear/center+lfe (green/black/orange) jacks for the 5.1 sink and the side (grey) jack for the stereo sink. It will also downmix any audio to stereo for the stereo sink, but will not touch the 5.1 output.

**Tip:** If pulseaudio fails with `master sink not found`, comment out the remapping lines, start PulseAudio and verify your card output is set to analog surround 7.1\. Alternatively, try using a [sink index](#Set_the_defaulting_output_source) instead of a sink name.

**Note:** The `remix=yes` parameter will only work if you also have `enable-remixing = yes` in your `/etc/pulse/daemon.conf` (default).

### Disabling LFE remixing

By default, PulseAudio remixes the number of channels to the default-sample-channels and since version 7 it also remixes the LFE channel. If you wish to disable LFE remixing, uncomment the line:

```
; enable-lfe-remixing = yes

```

and replace yes with no:

```
enable-lfe-remixing = no

```

then restart Pulseaudio.

## PulseAudio over network

One of PulseAudio's unique features is its ability to stream audio from clients over TCP to a server running the PulseAudio daemon reliably within a LAN.

To accomplish this, one needs to enable module-native-protocol-tcp.

### TCP support (networked sound)

To enable the TCP module, add this to (or uncomment, if already there) `/etc/pulse/default.pa` on both the client and server:

```
load-module module-native-protocol-tcp

```

For this to work, it is a requirement that both the client and server share the same cookie. Ensure that the clients and server share the same cookie file found under `~/.config/pulse/cookie`. It does not matter whose cookie file you use (the server or a client's), just that the server and client(s) share the same one.

Note: If experiencing trouble connecting, use (on server)

```
pacmd list-modules

```

### TCP support with anonymous clients

If it is undesirable to copy the cookie file from clients, anonymous clients can access the server by giving these parameters to module-native-protocol-tcp on the server (again in `/etc/pulse/default.pa`):

```
 load-module module-native-protocol-tcp auth-ip-acl=127.0.0.1;192.168.0.0/24 auth-anonymous=1

```

Change the LAN IP subnet to match that of the those clients you wish to have access to the server.

### Zeroconf (Avahi) publishing

For the remote PulseAudio server to appear in the PulseAudio Device Chooser (`pasystray`), load the appropriate zeroconf modules, and enable the [Avahi](/index.php/Avahi "Avahi") [daemon](/index.php/Daemon "Daemon").

On both machines, run:

```
$ systemctl start avahi-daemon
$ systemctl enable avahi-daemon

```

On the server, add `load-module module-zeroconf-publish` to `/etc/pulse/default.pa`, on the client, add `load-module module-zeroconf-discover` to `/etc/pulse/default.pa`. Now redirect any stream or complete audio output to the remote PulseAudio server by selecting the appropriate sink.

If you have issues with the remote syncs appearing on the client, try restarting the Avahi daemon on the server to rebroadcast the available interfaces.

### Switching the PulseAudio server used by local X clients

To switch between servers on the client from within X, the `pax11publish` command can be used. For example, to switch from the default server to the server at hostname foo:

```
$ pax11publish -e -S foo

```

Or to switch back to the default:

```
$ pax11publish -e -r

```

Note that for the switch to become apparent, the programs using Pulse must be restarted.

### When everything else seems to fail

The following is a quick fix and NOT a permanent solution

On the server:

```
 $ paprefs 

```

Go to Network Access -> Enable access to local sound devices (Also check both 'Allow discover' and 'Don't require authentication').

On the client:

```
 $ export PULSE_SERVER=server.ip && mplayer test.mp3

```

## ALSA monitor source

To be able to record from a monitor source (a.k.a. "What-U-Hear", "Stereo Mix"), use `pactl list` to find out the name of the source in PulseAudio (e.g. `alsa_output.pci-0000_00_1b.0.analog-stereo.monitor`). Then add lines like the following to `/etc/asound.conf` or `~/.asoundrc`:

```
pcm.pulse_monitor {
  type pulse
  device alsa_output.pci-0000_00_1b.0.analog-stereo.monitor
}

ctl.pulse_monitor {
  type pulse
  device alsa_output.pci-0000_00_1b.0.analog-stereo.monitor
}

```

Now you can select `pulse_monitor` as a recording source.

Alternatively, you can use pavucontrol to do this: make sure you have set up the display to "All input devices", then select "Monitor of [your sound card]" as the recording source.

## Monitor specific output

It is possible to monitor a specific output, for example to stream audio from a music player into a VOIP application. Simply create a null output device:

```
pactl load-module module-null-sink sink_name=<name>

```

In Pulseaudio Volume Control (pavucontrol), under the "Playback" tab, change the output of an application to <name>, and in the recording tab change the input of an application to "Monitor of <name>". Audio will now be outputted from one application into the other.

## PulseAudio through JACK

### The new new way

This configuration only works with jackdbus (JACK2 compiled with D-Bus support). It also requires the [pulseaudio-jack](https://www.archlinux.org/packages/?name=pulseaudio-jack) package. Make sure that `/etc/pulse/default.pa` contains a line:

```
load-module module-jackdbus-detect [...]

```

(where [...] can be any options supported by this module, usually `channels=2`.

As described on the [Jack-DBUS Packaging](https://github.com/jackaudio/jackaudio.github.com/wiki/JackDbusPackaging) page:

_Server auto-launching is implemented as D-Bus call that auto-activates JACK D-Bus service, in case it is not already started, and starts the JACK server. Correct interaction with PulseAudio is done using a D-Bus based audio card "acquire/release" mechanism. When JACK server starts, it asks this D-Bus service to acquire the audio card and PulseAudio will unconditionally release it. When JACK server stops, it releases the audio card that can be grabbed again by PulseAudio._

`module-jackdbus-detect.so` dynamically loads and unloads module-jack-sink and module-jack-source when jackdbus is started and stopped.

If PulseAudio sound does not work, check with `pavucontrol` to see if the relevant programs appear in the playback tab. If not, add the following to `~/.asound.conf` or `/etc/asound.conf` to redirect ALSA to PulseAudio:

```
pcm.pulse {
    type pulse
}

ctl.pulse {
    type pulse
}

pcm.!default {
    type pulse
}
ctl.!default {
    type pulse
}

```

If it still does not work, check with `pavucontrol` in the playback tab and make sure the relevant programs are outputting to PulseAudio JACK Sink instead of your audio card (which JACK has control of, so it will not work).

### The new way

The basic idea is that killing PulseAudio is a bad idea because it may crash any apps using PulseAudio and disrupt any audio playing.

The flow of how this setup works:

1.  PulseAudio releases the sound card
2.  JACK grabs sound card and starts up
3.  script redirects PulseAudio to JACK
4.  manually send PulseAudio apps to JACK output (pavucontrol may come in helpful for this)
5.  use JACK programs etc
6.  via script, stop redirecting PulseAudio to JACK
7.  stop JACK and release sound card
8.  PulseAudio grabs sound card and reroutes audio to it directly

With QJackCTL, set up these scripts:

`pulse-jack-pre-start.sh` set it up as the execute script on startup script

```
#!/bin/bash
pacmd suspend true

```

`pulse-jack-post-start.sh` set this one up as execute script after startup

```
#!/bin/bash
pactl load-module module-jack-sink channels=2
pactl load-module module-jack-source channels=2
pacmd set-default-sink jack_out
pacmd set-default-source jack_in

```

`pulse-jack-pre-stop.sh` "execute script on shutdown"

```
#!/bin/bash
SINKID=$(pactl list | grep -B 1 "Name: module-jack-sink" | grep Module | sed 's/[^0-9]//g')
SOURCEID=$(pactl list | grep -B 1 "Name: module-jack-source" | grep Module | sed 's/[^0-9]//g')
pactl unload-module $SINKID
pactl unload-module $SOURCEID
sleep 5

```

`pulse-jack-post-stop.sh` "execute script after shutdown"

```
#!/bin/bash
pacmd suspend false

```

### The old way

The JACK-Audio-Connection-Kit is popular for audio work, and is widely supported by Linux audio applications. It fills a similar niche as PulseAudio, but with more of an emphasis on professional audio work. In particular, audio applications such as Ardour and Audacity (recently) work well with Jack.

PulseAudio provides module-jack-source and module-jack-sink which allow PulseAudio to be run as a sound server above the JACK daemon. This allows the usage of per-volume adjustments and the like for the apps which need it, play-back apps for movies and audio, while allowing low-latency and inter-app connectivity for sound-processing apps which connect to JACK. However, this will prevent PulseAudio from directly writing to the sound card buffers, which will increase overall CPU usage.

To just try PA on top of JACK, have PA load the necessary modules on start:

```
pulseaudio -L module-jack-sink -L module-jack-source

```

To use PulseAudio with JACK, JACK must be started before PulseAudio, using whichever method one prefers. PulseAudio then needs to be started loading the two relevant modules. Edit `/etc/pulse/default.pa`, and change the following region:

```
### Load audio drivers statically (it is probably better to not load
### these drivers manually, but instead use module-hal-detect --
### see below -- for doing this automatically)
#load-module module-alsa-sink
#load-module module-alsa-source device=hw:1,0
#load-module module-oss device="/dev/dsp" sink_name=output source_name=input
#load-module module-oss-mmap device="/dev/dsp" sink_name=output source_name=input
#load-module module-null-sink
#load-module module-pipe-sink

### Automatically load driver modules depending on the hardware available
.ifexists module-udev-detect.so
load-module module-udev-detect
.else
### Alternatively use the static hardware detection module (for systems that
### lack udev support)
load-module module-detect
.endif

```

to the following:

```
### Load audio drivers statically (it is probably better to not load
### these drivers manually, but instead use module-hal-detect --
### see below -- for doing this automatically)
#load-module module-alsa-sink
#load-module module-alsa-source device=hw:1,0
#load-module module-oss device="/dev/dsp" sink_name=output source_name=input
#load-module module-oss-mmap device="/dev/dsp" sink_name=output source_name=input
#load-module module-null-sink
#load-module module-pipe-sink
load-module module-jack-source
load-module module-jack-sink

### Automatically load driver modules depending on the hardware available
#.ifexists module-udev-detect.so
#load-module module-udev-detect
#.else
### Alternatively use the static hardware detection module (for systems that
### lack udev support)
#load-module module-detect
#.endif

```

Basically, this prevents module-udev-detect from loading. module-udev-detect will always try to grab the sound card (JACK has already done that, so this will cause an error). Also, the JACK source and sink must be explicitly loaded.

#### QjackCtl with start-up/shutdown scripts

Using the settings listed above, use QjackCtl to execute a script upon startup and shutdown to load/unload PulseAudio. Part of the reason users may wish to do this is that the above changes disable PulseAudio's automatic hardware detection modules. This particular setup is for using PulseAudio in an exclusive fashion with JACK, though the scripts could be modified to unload and load an alternate non-JACK setup, but killing and starting PulseAudio while programs might be using it would become problematic.

**Note:** padevchooser in the following example is deprecated. It is replaced by pasystray

The following example could be used and modified as necessary as a startup script that daemonizes PulseAudio and loads the _padevchooser_ program (optional, needs to be built from AUR) called `jack_startup`:

```
#!/bin/bash
#Load PulseAudio and PulseAudio Device Chooser

pulseaudio -D
padevchooser&

```

as well as a shutdown script to kill PulseAudio and the Pulse Audio Device Chooser, as another example called `jack_shutdown` also in the home directory:

```
#!/bin/bash
#Kill PulseAudio and PulseAudio Device Chooser

pulseaudio --kill
killall padevchooser

```

Both scripts need to be made executable:

```
chmod +x jack_startup jack_shutdown

```

then with QjackCtl loaded, click on the _Setup_ button and then the _Options_ tab and tick both "Execute Script after Startup:" And "Execute Script on Shutdown:" and put either use the ... button or type the path to the scripts (assuming the scripts are in the home directory) `~/jack_startup` and `~/jack_shutdown` making sure to save the changes.

## PulseAudio through OSS

Add the following to `/etc/pulse/default.pa`:

```
load-module module-oss

```

Then start PulseAudio as usual, making sure that sinks and sources are defined for OSS devices.

## PulseAudio from within a chroot (e.g. 32-bit chroot in 64-bit install)

Since a chroot sets up an alternative root for the running/jailing of applications, PulseAudio must be installed within the chroot itself (`pacman -S pulseaudio` within the chroot environment).

PulseAudio, if not set up to connect to any specific server (this can be done in `/etc/pulse/client.conf`, through the PULSE_SERVER environment variable, or through publishing to the local X11 properties using module-x11-publish), will attempt to connect to the local pulse server, failing which it will spawn a new pulse server. Each pulse server has a unique ID based on the machine-id value in `/var/lib/dbus`. To allow for chrooted apps to access the pulse server, the following directories must be mounted within the chroot:-

```
/run
/var/lib/dbus
/tmp
~/config/.pulse

```

`/dev/shm` should also be mounted for efficiency and good performance. Note that mounting /home would normally also allow sharing of the `~/.pulse` folder.

PulseAudio selects the path to the socket via XDG_RUNTIME_DIR, so be sure to drag it along when you chroot as a normal user using [sudo](/index.php/Sudo "Sudo") (see [Sudo#Environment variables](/index.php/Sudo#Environment_variables "Sudo")).

For specific direction on accomplishing the appropriate mounts, please refer to the wiki on installing a bundled 32-bit system, especially the [additional section](/index.php/Install_bundled_32-bit_system_in_Arch64#Allow_32-bit_applications_access_to_64-bit_PulseAudio "Install bundled 32-bit system in Arch64") specific to PulseAudio.

## Disabling automatic spawning of PulseAudio server

Some users may prefer to manually start the PulseAudio server before running certain programs and then stop the PulseAudio server when they are finished. A simple way to accomplish this is to edit `~/.config/pulse/client.conf` or `/etc/pulse/client.conf` and change `autospawn = yes` to `autospawn=no`. Make sure the line is uncommented as well.

 `~/.config/pulse/client.conf #or /etc/pulse/client.conf` 

```
autospawn=no

```

Now you can manually start the pulseaudio server with

```
$ pulseaudio --start

```

and stop it with

```
$ pulseaudio --kill

```

This setting is also respected by the default pulseaudio dektop session startup script `start-pulseaudio-x11` which is executed from `/etc/xdg/autostart/pulseaudio.desktop`.

## Disabling pulseaudio daemon altogether

To disable the pulseaudio daemon completely, and thereby preventing it from starting, one can add `daemon-binary=/bin/true` to the configuration file.

 `~/.config/pulse/client.conf #or /etc/pulse/client.conf` 

```
daemon-binary=/bin/true

```

## Remap stereo to mono

Remap a stereo input-sink to a mono sink by creating a virtual sink. It would be useful if you only have one speaker. Add to `/etc/pulse/default.pa`:

```
load-module module-remap-sink master=alsa_output.pci-0000_00_1f.5.analog-stereo sink_name=mono channels=2 channel_map=mono,mono
# Optional: Select new remap as default
set-default-sink mono

```

(replace alsa_output.pci-0000_00_1f.5.analog-stereo in the sound card name shown from `pacmd list-sinks`)

Switch player between virtual mono sink and real stereo sink.

## Swap left/right channels

Swap/reverse stereo channels by creating a virtual sink. Add to `/etc/pulse/default.pa`:

```
load-module module-remap-sink sink_name=reverse-stereo master=alsa_output.pci-0000_00_1f.5.analog-stereo channels=2 master_channel_map=front-right,front-left channel_map=front-left,front-right
set-default-sink reverse-stereo

```

(replace alsa_output.pci-0000_00_1f.5.analog-stereo in the sound card name shown from `pacmd list-sinks`)

[module-remap-sink documentation](http://www.freedesktop.org/wiki/Software/PulseAudio/Documentation/User/Modules/#index12h3)

## PulseAudio as a minimal unintrusive dumb pipe to ALSA

Some people do not want to run PulseAudio all the time for various reasons. This example will turn the full fledged audio server into an unobstrusive dumb pipe to ALSA devices that automatically starts **and** stops itself when done, allowing applications that requires PulseAudio to fully function while not touching any ALSA setting nor setting itself as the default ALSA device.

This configuration tells native PA clients to autospawn the daemon when they need it, then the daemon is configured to autoexit as soon as all clients have disconnected. The daemon itself uses a plain simple static configuration that uses your configured `pcm.!default` ALSA devices and nothing more. No replacement of ALSA's default, no playing with mixer levels, nothing but record/playback. Also make sure [pulseaudio-alsa](https://www.archlinux.org/packages/?name=pulseaudio-alsa) is **not** installed so standard ALSA clients don't default to pulse. `alsamixer` functions properly as well as any other ALSA clients. Also make sure common frameworks like Xine, Gstreamer and Phonon are configured to use ALSA: by default if they detect PulseAudio is installed they will try to use it before ALSA.

 `/etc/pulse/daemon.conf` 

```
# Replace these with the proper values
exit-idle-time = 0 # Exit as soon as unneeded
flat-volumes = yes # Prevent messing with the master volume

```

 `/etc/pulse/client.conf` 

```
# Replace these with the proper values

# Applications that uses PulseAudio *directly* will spawn it,
# use it, and pulse will exit itself when done because of the
# exit-idle-time setting in daemon.conf
autospawn = yes

```

 `/etc/pulse/default.pa` 

```
# Replace the *entire* content of this file with these few lines and
# read the comments

.fail
    # Set tsched=0 here if you experience glitchy playback. This will
    # revert back to interrupt-based scheduling and should fix it.
    #
    # Replace the device= part if you want pulse to use a specific device
    # such as "dmix" and "dsnoop" so it doesn't lock an hw: device.

    # INPUT/RECORD
    load-module module-alsa-source device="default" tsched=1

    # OUTPUT/PLAYBACK
    load-module module-alsa-sink device="default" tsched=1 

    # Accept clients -- very important
    load-module module-native-protocol-unix

.nofail
.ifexists module-x11-publish.so
    # Publish to X11 so the clients know how to connect to Pulse. Will
    # clear itself on unload.
    load-module module-x11-publish
.endif

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=PulseAudio/Examples&oldid=419557](https://wiki.archlinux.org/index.php?title=PulseAudio/Examples&oldid=419557)"