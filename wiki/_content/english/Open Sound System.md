The [Open Sound System](https://en.wikipedia.org/wiki/Open_Sound_System "wikipedia:Open Sound System") (or **OSS**) is an alternative sound architecture for Unix-like and POSIX-compatible systems. OSS version 3 was the original sound system for Linux, but was superseded by the [Advanced Linux Sound Architecture](/index.php/Advanced_Linux_Sound_Architecture "Advanced Linux Sound Architecture") (or **ALSA**) in 2002 when OSS version 4 became proprietary software. OSSv4 became free software again in 2007 when [4Front Technologies](http://www.opensound.com/) released its source code and provided it under the GPL license.

## Contents

*   [1 Comparisons with ALSA](#Comparisons_with_ALSA)
    *   [1.1 OSS Advantages (users)](#OSS_Advantages_.28users.29)
    *   [1.2 OSS Advantages (developers)](#OSS_Advantages_.28developers.29)
    *   [1.3 ALSA advantages over OSS](#ALSA_advantages_over_OSS)
*   [2 Install](#Install)
*   [3 Testing](#Testing)
*   [4 Volume Control Mixer](#Volume_Control_Mixer)
    *   [4.1 Color Definitions](#Color_Definitions)
    *   [4.2 Saving Mixer Levels](#Saving_Mixer_Levels)
    *   [4.3 Other Mixers](#Other_Mixers)
*   [5 Configuring Applications for OSS](#Configuring_Applications_for_OSS)
    *   [5.1 Applications that use GStreamer](#Applications_that_use_GStreamer)
    *   [5.2 Applications that use OpenAL](#Applications_that_use_OpenAL)
    *   [5.3 Audacity](#Audacity)
    *   [5.4 Gajim](#Gajim)
    *   [5.5 MOC](#MOC)
    *   [5.6 MPD](#MPD)
    *   [5.7 MPlayer](#MPlayer)
    *   [5.8 VLC media player](#VLC_media_player)
    *   [5.9 Wine](#Wine)
    *   [5.10 Other applications](#Other_applications)
*   [6 Tips and tricks](#Tips_and_tricks)
    *   [6.1 Using multimedia keys with OSS](#Using_multimedia_keys_with_OSS)
    *   [6.2 Changing the Sample Rate](#Changing_the_Sample_Rate)
    *   [6.3 A simple system tray applet](#A_simple_system_tray_applet)
    *   [6.4 Start ossxmix docked to the system tray on startup](#Start_ossxmix_docked_to_the_system_tray_on_startup)
        *   [6.4.1 KDE](#KDE)
        *   [6.4.2 Gnome](#Gnome)
    *   [6.5 Record sound output from a program](#Record_sound_output_from_a_program)
    *   [6.6 Suspend and Hibernation](#Suspend_and_Hibernation)
    *   [6.7 Changing the Default Sound Output](#Changing_the_Default_Sound_Output)
    *   [6.8 Creative Sound Blaster X-Fi Surround 5.1 SB1090 USB](#Creative_Sound_Blaster_X-Fi_Surround_5.1_SB1090_USB)
    *   [6.9 ALSA emulation](#ALSA_emulation)
        *   [6.9.1 Instructions](#Instructions)
    *   [6.10 Settings for a specific driver](#Settings_for_a_specific_driver)
*   [7 Troubleshooting](#Troubleshooting)
    *   [7.1 Troubleshooting HD Audio devices](#Troubleshooting_HD_Audio_devices)
        *   [7.1.1 Understanding the problem](#Understanding_the_problem)
        *   [7.1.2 Solution](#Solution)
    *   [7.2 MMS sound cracking in Totem](#MMS_sound_cracking_in_Totem)
    *   [7.3 Microphone playing through output channels](#Microphone_playing_through_output_channels)
*   [8 See also](#See_also)

## Comparisons with ALSA

Some advantages and disadvantages compared to using the Advanced Linux Sound Architecture.

### OSS Advantages (users)

*   Per-application volume control.
*   Some legacy cards have better support.

### OSS Advantages (developers)

*   Support for drivers in userspace.
*   Cross-platform (OSS runs on BSDs and Solaris).
*   Smaller and easier to use API.

### ALSA advantages over OSS

*   Better support for USB audio devices.
*   Support for Bluetooth audio devices.
*   Support for [AC'97](https://en.wikipedia.org/wiki/AC%2797 "wikipedia:AC'97") and [HD Audio](https://en.wikipedia.org/wiki/Intel_High_Definition_Audio "wikipedia:Intel High Definition Audio") dial-up soft-modems such as Si3055.
*   Better support for MIDI devices.
*   Support for suspend.
*   Better support for jack detection.
*   Better support for modern hardware.

**Note:**

*   OSS has experimental output support for USB audio devices, but no input.
*   OSS supports MIDI devices with the help of a software synthesizer such as [Timidity](/index.php/Timidity "Timidity") or [FluidSynth](/index.php/FluidSynth "FluidSynth").

## Install

[Install](/index.php/Install "Install") the [oss](https://aur.archlinux.org/packages/oss/) package. There is also a development version of OSS available with the [oss-git](https://aur.archlinux.org/packages/oss-git/) package.

This will install the OSS, run the OSS install script (temporarily disabling the ALSA modules) and install the OSS kernel modules. Since ALSA is enabled by default in the boot scripts, you need to disable it so it does not conflict with OSS. You can do this by [blacklisting](/index.php/Blacklisting "Blacklisting") the `soundcore` module.

After blacklisting the module, you can [enable](/index.php/Daemon "Daemon") the **oss** daemon to start at boot.

In case you are not part of the *audio* group, add yourself and **relogin** for the changes to take effect:

```
# gpasswd -a $USER audio

```

In case OSS is not able to detect your card when starting it, run:

```
# ossdetect -v
# soundoff && soundon

```

## Testing

**Warning:** The default volume is very loud, avoid using earphones and physically lower the volume of your speakers (if possible) before running the test.

**Test OSS by running:**

```
$ osstest

```

You should be able to hear music during the test process. If there is no audio, try to adjust the volume or refer to the [#Troubleshooting](#Troubleshooting) section.

If you want to hear sounds from more than one application simultaneously, you need `vmix`, OSS's software mixer.

**Check that vmix is enabled by running:**

```
$ ossmix -a | grep -i vmix

```

You should see a line like `vmix0-enable ON|OFF (currently ON)`. If you do not see any lines beginning with `vmix`, it probably means that `vmix` has not been attached to your sound device. To attach `vmix`, issue the command:

```
$ vmixctl attach device

```

where *device* is your sound device, e.g. `/dev/oss/oss_envy240/pcm0`.

To avoid having to issue this command manually in the future, you can add it to `/usr/lib/oss/soundon.user`, as suggested [here](http://www.opensound.com/wiki/index.php/Tips_And_Tricks#Changing_the_default_sound_output).

If you get a **"Device or resource busy"** error, you need to add `vmix_no_autoattach=1` to `/usr/lib/oss/conf/osscore.conf` and then reboot.

**See which devices are detected by running:**

```
$ ossinfo

```

You should be able to see your devices listed under *Device Objects* or *Audio Devices*. If the device that you want to use is not at the top of one of these sections, you have to edit `/usr/lib/oss/etc/installed_drivers` and place the driver for your device at the very top. It may be required to do a:

```
$ soundoff && soundon

```

If this does not work, comment all drivers listed except the ones for your device.

## Volume Control Mixer

To control the volume of various devices, mixers levels will need to be set. There are two mixers:

*   **ossmix**: a command-line mixer, similar to the BSD audio mixer `mixerctl`.
*   **ossxmix**: a GTK+-based graphical mixer.

The basic `ossxmix` controls look like:

```
 / High Definition Audio ALC262 \    --------------------------------> 1
/________________________________\________________________________
|                                                                 \
| [x] vmix0-enable [vmix0-rate: 48.000kHz]      vmix0-channels    |--> 2
|                                               [ Stereo [v] ]    |
|                                                                 |
|  __codec1______________________________________________________ |
| |  _jack______________________________________________________ ||--> 3
| | |  _int-speaker_________________   _green_________________  |||
| | | |                             | |                       | |||
| | | |  _mode_____ | |             | |  _mode_____   | |     | |||
| | | | [ mix [v] ] o o [x] [ ]mute | | [ mix  [v] ]  o o [x] | |||
| | | |             | |             | |               | |     | |||
| | | |_____________________________| |_______________________| |||
| | |___________________________________________________________|||
| |______________________________________________________________||
| ___vmix0______________________________________________________  |
| |  __mocp___  O O   _firefox_  O O  __pcm7___  O O            | |--> 4
| | |         | O O  |         | x x |         | O O            | |
| | | | |     | x O  | | |     | x x | | |     | O O            | |
| | | o o [x] | x x  | o o [x] | x x | o o [x] | O O            | |
| | | | |     | x x  | | |     | x x | | |     | O O            | |
| | |_________| x x  |_________| x x |_________| O O            | |
| |_____________________________________________________________| |
|_________________________________________________________________|

```

1.  One tab for each sound card
2.  The `vmix` (virtual mixer) special configurations appear at the top. These include sampling rate and mixer priority.
3.  These are your sound card jack configurations (input and output). Every mixer control that is shown here is provided by your sound card.
4.  Application `vmix` mixer controls and sound meters. If the application is not actively playing a sound it will be labeled as `pcm08, pcm09...` and when the application is playing the application name will be shown.

### Color Definitions

For high definition (HD) audio, `ossxmix` will color jack configurations by their pre-defined jack colors:

| Color | Type | Connector |
| green | front channels (stereo output) | 3.5mm TRS |
| black | rear channels (stereo output) | 3.5mm TRS |
| grey | side channels (stereo output) | 3.5mm TRS |
| gold | center and subwoofer (dual output) | 3.5mm TRS |
| blue | line level (stereo input) | 3.5mm TRS |
| pink | microphone (mono input) | 3.5mm TS |

### Saving Mixer Levels

Mixer levels are saved when you shut off your computer. If you want to save the mixer level immediately, execute as root:

```
# savemixer

```

`savemixer` can be used to write mixer levels to a file with the `-f` switch and restore by the `-L` switch.

### Other Mixers

Other mixers that have support for OSS:

*   **Gnome Volume Control** — for [GNOME](/index.php/GNOME "GNOME").

	[http://library.gnome.org/users/gnome-volume-control/stable/](http://library.gnome.org/users/gnome-volume-control/stable/) || [gnome](https://www.archlinux.org/groups/x86_64/gnome/)

*   **Kmix** — for [KDE](/index.php/KDE "KDE").

	[http://www.kde.org/applications/multimedia/kmix/](http://www.kde.org/applications/multimedia/kmix/) || [kmix](https://www.archlinux.org/packages/?name=kmix)

*   **VolWheel** — After the installation, set it to [autostart](/index.php/Autostarting#On_Xorg_startup "Autostarting") as needed, then enable OSS support by right-clicking on the system tray icon, choosing *Preferences* and then changing:

*   *Driver*: `OSS`.
*   *Default Channel*: `vmix0-outvol` (find out what channel to use with `ossmix`).
*   *Default Mixer*: `ossxmix`.
*   In the *MiniMixer* tab (optional), add `vmix0-outvol` and optionally others.

	[http://oliwer.net/b/volwheel.html](http://oliwer.net/b/volwheel.html) || [volwheel](https://www.archlinux.org/packages/?name=volwheel)

## Configuring Applications for OSS

### Applications that use GStreamer

If you have problems with applications that use GStreamer for audio, you can try removing [pulseaudio](https://www.archlinux.org/packages/?name=pulseaudio) and installing the [gst-plugins-good](https://www.archlinux.org/packages/?name=gst-plugins-good) package which is needed by `oss4sink` and `oss4src`.

### Applications that use OpenAL

By default OpenAL uses ALSA. To change this, simply define the usage of OSS in `/etc/openal/alsound.conf`:

 `/etc/openal/alsound.conf` 
```
drivers=oss

```

### Audacity

If [Audacity](http://audacity.sourceforge.net/) starts, but it complains that it cannot open the device or simply does not play anything, then you may be using `vmix` which prevents Audacity from having exclusive access to your sound device. To fix this, before running Audacity, run:

```
$ ossmix vmix0-enable OFF

```

You can restore `vmix` after closing Audacity with:

```
$ ossmix vmix0-enable ON

```

### Gajim

By default, [Gajim](http://gajim.org/) uses `aplay -q` to play a sound. For OSS you can change it to the equivalent `ossplay -qq` by going to *Edit > Preferences > Advanced*, opening the *Advanced Configuration Editor* and modifying the `soundplayer` variable accordingly.

### MOC

To use [MOC](/index.php/MOC "MOC") with OSS v4.1 you must change `OSSMixerDevice` to `/dev/ossmix` in your configuration file (located in `~/.moc`). For issues with the interface try changing the `OSSMixerChannel` by pressing `w` in `mocp` (to change to the sofware mixer).

### MPD

[MPD](/index.php/MPD "MPD") is configured through `/etc/mpd.conf` or `~/.mpdconf`. Check both of these files, looking for something that looks like:

 `/etc/mpd.conf` 
```
...
audio_output {
    type    "alsa"
    name    "Some Device Name"
}
...
```

If you find an uncommented (the lines do not begin with #'s) ALSA configuration like the one above, comment all of it out, or delete it, and add the following:

 `/etc/mpd.conf` 
```
...
audio_output {
    type    "oss"
    name    "My OSS Device"
}
...
```

Further configuration might not be necessary for all users. However, if you experience issues (in that MPD does not work properly after it has been restarted), or if you like having specific (i.e. more user-configured, less auto-configured) configuration files, the audio output for OSS can be more specifically configured as follows:

*   First, run:

```
$ ossinfo | grep /dev/dsp

```

*   Look for the line that says something similar to `/dev/dsp -> /dev/oss/<SOME_CARD_IDENTIFIER>/pcm0`. Take note of what your `<SOME_CARD_IDENTIFIER>` is, and add these lines to your OSS `audio_output` in your MPD configuration file:

 `/etc/mpd.conf` 
```
...
audio_output {
    type            "oss"
    name            "My OSS Device"
    **device          "/dev/oss/<SOME_CARD_IDENTIFIER>/pcm0"**
    **mixer_device    "/dev/oss/<SOME_CARD_IDENTIFIER>/mix0"**
}
...

```

See also: [Music Player Daemon#System-wide_configuration](/index.php/Music_Player_Daemon#System-wide_configuration "Music Player Daemon").

### MPlayer

If you are using a GUI (SMplayer, GNOME MPlayer, etc.) you can select OSS as the default output in the settings dialogs. If you use [MPlayer](/index.php/MPlayer "MPlayer") from the command-line, you should specify the sound output:

```
$ mplayer -ao oss /some/file/to/play.mkv

```

If you do not want to bother typing it over and over again add `ao=oss` to your configuration file (at `~/.mplayer/config`).

See also: [MPlayer#Configuration](/index.php/MPlayer#Configuration "MPlayer").

### VLC media player

You can select OSS as the default output in the audio settings.

### Wine

To set OSS support in [Wine](/index.php/Wine "Wine") start:

```
$ winecfg

```

and go to the `Audio` tab and select the `OSS Driver`.

See also: [Wine#Sound](/index.php/Wine#Sound "Wine").

### Other applications

*   If you can not get sound from an application not listed here, try looking at the [Configuring Applications for OSSv4](http://www.4front-tech.com/wiki/index.php/Configuring_Applications_for_OSSv4) page.
*   Search for OSS specific packages with [pacman](/index.php/Pacman "Pacman") or by looking in the [AUR](https://aur.archlinux.org/packages.php?K=-oss&start=0&PP=100).

See also: [ossapps](http://www.opensound.com/ossapps.html).

## Tips and tricks

### Using multimedia keys with OSS

An easy way to mute/unmute and increase/decrease the volume is to use the [ossvol](http://www.opensound.com/wiki/index.php/Tips_And_Tricks#ossvol) script.

Download the script and place it at `/usr/bin/ossvol`.

Once you installed it, type:

```
$ ossvol -t

```

to toggle mute, or:

```
$ ossvol -h

```

to see the available commands.

**Note:** If `ossvol` gives an error like **Bad mixer control name(987) 'vol'**, you need to edit the script and change the `CHANNEL` variable to your default channel (usually `vmix0-outvol`).

If you want to use multimedia keys with `ossvol`, see [Extra keyboard keys](/index.php/Extra_keyboard_keys "Extra keyboard keys") and make sure they are properly configured. After that you can use, for example, [Xbindkeys](/index.php/Xbindkeys "Xbindkeys") to bind them to the `ossvol` script. Add the following to your `~/.xbindkeysrc` file:

 `~/.xbindkeysrc` 
```
# Toggle mute
"ossvol -t"
    m:0x0 + c:121
    XF86AudioMute

# Lower volume
"ossvol -d 2"
    m:0x0 + c:122
    XF86AudioLowerVolume

# Raise volume
"ossvol -i 2"
    m:0x0 + c:123
    XF86AudioRaiseVolume

```

and optionally change the multimedia keys with whatever shortcuts you prefer.

### Changing the Sample Rate

Changing the output sample rate is not obvious at first. Sample rates can only be changed by root and `vmix` must be unused by any programs when a change is requested. Before you follow any of these steps, ensure you are going through a receiver/amplifier and using quality speakers and not simply computer speakers. If you are only using computer speakers, do not bother changing anything here as you will not notice a difference.

By default the sample rate is 48000hz. There are several conditions in which you may want to change this. This all depends on your usage patterns. You want the sample rate you are using to match the media you use the most. If your computer has to change the sampling rate of the media to suit the hardware it is likely, though not guaranteed, that you will have a loss in audio quality. This is most noticeable in down sampling (ie. 96000hz → 48000hz). There is an article about this issue in [Stereophile](http://www.stereophile.com/news/121707lucky/) which was [discussed](http://lists.apple.com/archives/coreaudio-api/2008/Jan/msg00272.html) on Apple's *CoreAudio API* mailing list if you wish to learn more about this issue.

Some example sample rates:

	44100hz

	Sample rate of standard [Red Book](https://en.wikipedia.org/wiki/Red_Book_(CD_standard) audio CDs.

	88000hz

	Sample rate of [SACD](https://en.wikipedia.org/wiki/Super_Audio_CD "wikipedia:Super Audio CD") high definition audio discs/downloads. It is rare that your motherboard will support this sample rate.

	96000hz

	Sample rate of most high definition audio downloads. If your motherboard is an [AC'97](https://en.wikipedia.org/wiki/AC%2797 "wikipedia:AC'97") motherboard, this is likely to be your highest bitrate.

	192000hz

	Sample rate of BluRay, and some (very few) high definition downloads. Support for external audio receiver equipment is limited to high end audio. Not all motherboards support this. An example of a motherboard chipset that would support this includes [HD Audio](https://en.wikipedia.org/wiki/Intel_High_Definition_Audio "wikipedia:Intel High Definition Audio").

To check what your sample rate is currently set to, run:

```
ossmix | grep rate

```

You are likely to see `vmix0-rate <decimal value> (currently 48000) (Read-only)`.

If you do not see a `vmix0-rate` (or `vmix1-rate`, etc.) being outputted, then it probably means that `vmix` is disabled. In that case, OSS will use the rate requested by the program which uses the device, so this section does not apply. Exception to this are Envy24 (and Envy24HT) cards that have a special setting `envy24.rate` which has a similar function (see the `oss_envy24` manpage).

To change your sample rate:

1.  First, make sure your card is able to use the new rate. Run `ossinfo -v2` and see if the wanted rate is in the *Native sample rates* output.
2.  As root, run `/usr/lib/oss/scripts/killprocs.sh`. Be aware, this will close any program that currently has an open sound channel.
3.  After all programs occupying `vmix` are terminated, run as root: `vmixctl rate /dev/dsp 96000` replacing the rate with your desired sample rate (and `ossmix envy24.rate 96000` if applicable).
4.  Run `ossmix | grep rate` and check for `vmix0-rate <decimal value> (currently 96000) (Read-only)` to see if you were successful.
5.  **To make the changes permanent** add the following to the `soundon.user` file:

 `/usr/lib/oss/soundon.user` 
```
#!/bin/sh

vmixctl rate /dev/dsp 96000
# ossmix envy24.rate 96000 # uncomment if you have an Envy24(HT) card

exit 0

```

and make it executable:

```
# chmod +x /usr/lib/oss/soundon.user

```

### A simple system tray applet

For those wanting a very lightweight OSS system tray applet see [this one](http://pastebin.furver.se/0xflchkfz/).

To install it:

*   Download [the script](http://pastebin.furver.se/0xflchkfz/0xflchkfz.txt) with whatever name you want (e.g. `ossvolctl`)
*   Make it executable:

```
$ chmod +x ossvolctl

```

*   And copy it to your `/usr/bin`:

```
# cp ossvolctl /usr/bin/ossvolctl

```

or:

```
# install -Dm755 ossvolctl /usr/bin/ossvolctl

```

### Start ossxmix docked to the system tray on startup

#### KDE

Create an application launcher file named `ossxmix.desktop` in you local application launchers directory (`~/.local/share/applications/` with:

 `~/.local/share/applications/ossxmix.desktop` 
```
[Desktop Entry]
Name=Open Sound System Mixer
GenericName=Audio Mixer
Exec=ossxmix -b
Icon=audio-card
Categories=Application;GTK;AudioVideo;Player;
Terminal=false
Type=Application
Encoding=UTF-8

```

To have it autostart with your system, add it to the list in *System Settings > System Administration > Startup and Shutdown > Autostart*.

#### Gnome

As root create a file `/usr/local/bin/ossxmix_bg` with the following content:

 `/usr/local/bin/ossxmix_bg` 
```
#!/bin/sh

exec /usr/bin/ossxmix -b

```

Then go to *System > Preferences > Start Up Applications* and:

*   Click *Add*, type `OSSMIX` in the *Name* field and `/usr/local/bin/ossxmix_bg` in *Command* field then click *Add Button*.
*   Login and logout to see the changes.

### Record sound output from a program

*   [Recording sound output of a program](http://www.opensound.com/wiki/index.php/Tips_And_Tricks#Recording_sound_output_of_a_program).

### Suspend and Hibernation

OSS does not automatically support suspend, it must be manually stopped prior to suspending or hibernating and restarted afterwards.

OSS provides `soundon` and `soundoff` to enable and disable OSS, although they only stop OSS if all processes that use sound are terminated first.

The following script is a rather basic method of automatically unloading OSS prior to suspending and reloading afterwards.

 `/usr/lib/systemd/system-sleep/50osssound.sh` 
```
#!/bin/sh
suspend_osssound()
{
    /usr/lib/oss/scripts/killprocs.sh
    /usr/bin/soundoff
}

resume_osssound()
{
    /usr/bin/soundon
}

case $1 in
    pre)
        suspend_osssound
 	;;
    post)
 	resume_osssound
 	;;
    *) exit $NA
 	;;
esac

```

Save the contents of this script (as root) into `/usr/lib/systemd/system-sleep/50osssound.sh` and make it executable:

```
# chmod a+x /usr/lib/systemd/system-sleep/50osssound.sh

```

**Warning:** This script is rather basic and will terminate any application directly accessing OSS. Save your work prior to suspending/hibernating.

An alternative would be to use [s2ram](/index.php/Suspend_to_RAM "Suspend to RAM") for suspending. Just create a suspend script to `/usr/bin/suspend` and make it executable.

```
 #!/bin/sh

 ## Checking if you are a root or not
 if ! [ -w / ]; then
   echo >&2 "This script must be run as root"
   exit 1
 fi

 s2ram -f

 sleep 2

 systemctl restart oss.service 2>/tmp/oss.txt || echo "OSS restart failed, check /tmp/oss.txt for information"

```

With this, all your apps should be fine.

**Note:** If you are using Opera you must kill `operapluginwrapper` before suspend. To do this add `pid=$(pidof operapluginwrapper) && kill $pid` before `s2ram -f`.

### Changing the Default Sound Output

When running `osstest`, the first test passes for the first channel, but not for the stereo or right channel, it sounds distorted/hisses. If this is what your sound is like, then it is set to the wrong output.

```
*** Scanning sound adapter #-1 ***
/dev/oss/oss_hdaudio0/pcm0 (audio engine 0): HD Audio play front
- Performing audio playback test... 
<left> OK <right> OK <stereo> OK <measured srate 47991.00 Hz (-0.02%)> 

```

The left sounded good, the right and stereo were the distorted ones.

Let the test continue until you get a working output:

```
/dev/oss/oss_hdaudio0/spdout0 (audio engine 5): HD Audio play spdif-out 
- Performing audio playback test... 
<left> OK <right> OK <stereo> OK <measured srate 47991.00 Hz (-0.02%)> 

```

If this passed the test on all left, right and stereo, proceed to next step.

For the command to change the default output see [this OSS wiki article](http://www.opensound.com/wiki/index.php/Tips_And_Tricks#Changing_the_default_sound_output). Change it to what works for you, for example:

```
# ln -sf /dev/oss/oss_hdaudio0/spdout0 /dev/dsp_multich

```

For surround sound (4.0-7.1) choose `dsp_multich`, for only 2 channels, `dsp` is sufficient. See [this](http://manuals.opensound.com/usersguide/dsp.html) for all available devices.

### Creative Sound Blaster X-Fi Surround 5.1 SB1090 USB

This information is taken from the [4front-tech forum](http://www.4front-tech.com/forum/viewtopic.php?f=3&t=3423).

It is surprising to learn that the external card does not work just because of a missing true return value in the function `write_control_value(...)` in `ossusb_audio.c`.

To fix this, a recompile of OSS is necessary, for now.

*   Grab the latest OSS from the Arch Repo

```
[https://projects.archlinux.org/svntogit/community.git/tree/trunk?h=packages/oss](https://projects.archlinux.org/svntogit/community.git/tree/trunk?h=packages/oss)

```

*   Extract it
*   `cd` into the folder
*   run `makepkg --nobuild`
*   `cd` to `src/kernel/drv/oss_usb/` and edit `ossusb_audio.c`: add a `return 1;`.
    *   should look like so:

 `ossusb_audio.c` 
```
static int
write_control_value (ossusb_devc * devc, udi_endpoint_handle_t * endpoint,
                     int ctl, int l, unsigned int v)
{
     return 1;
...

```

*   `cd` to `src/kernel/setup` and edit `srcconf_linux.inc`, search for `-Werror` and remove it, otherwise OSS will not compile.
*   do `makepkg --noextract`

Now you must [install](/index.php/Arch_User_Repository#Installing_packages "Arch User Repository") the package. Remove OSS first if already installed.

### ALSA emulation

You can instruct `alsa-lib` to use OSS as its audio output system. This works as a sort of ALSA emulation.

Note, however, that this method may introduce additional latency in your sound output, and that the emulation is not complete and does not work with all applications. It does not work, for example, with programs that try to detect devices using ALSA.

So, as most applications support OSS directly, use this method only as a last resort.

In the future, more complete methods may be available for emulating ALSA, such as `libsalsa` and `cuckoo`.

#### Instructions

*   [Install](/index.php/Install "Install") the [alsa-plugins](https://www.archlinux.org/packages/?name=alsa-plugins) package.

*   Edit `/etc/asound.conf` as follows.

```
pcm.oss {
   type oss
    device /dev/dsp
}

pcm.!default {
    type oss
    device /dev/dsp
}

ctl.oss {
    type oss
    device /dev/mixer
}

ctl.!default {
    type oss
    device /dev/mixer
}

```

**Note:** If you do not want to use OSS anymore, do not forget to revert changes in `/etc/asound.conf`.

### Settings for a specific driver

If something is not working, there is a possibility that some of your OSS settings are driver specific or just wrong for your driver.

To solve this:

*   Find out which driver is used

 `$ lspci -vnn | grep -i -A 15 audio` 
```
00:1e.2 Multimedia audio controller [0401]: Intel Corporation 82801FB/FBM/FR/FW/FRW (ICH6 Family) AC'97 Audio Controller [8086:266e] (rev 03)
Subsystem: Hewlett-Packard Company NX6110/NC6120 [103c:099c]
Flags: bus master, medium devsel, latency 0, IRQ 21
I/O ports at 2100 [size=256]
I/O ports at 2200 [size=64]
Memory at d0581000 (32-bit, non-prefetchable) [size=512]
Memory at d0582000 (32-bit, non-prefetchable) [size=256]
Capabilities: <access denied>
Kernel driver in use: *oss_ich*
Kernel modules: snd-intel8x0

```

*   Locate configuration file for device in:

```
# cd /usr/lib/oss/conf/

```

*   Try changing defaults. There are only few settings, and they are self explanatory

For example, the setting:

```
ich_jacksense = 1 

```

in `oss_ich.conf` turns on `jack-sense` (which is responsible for recognizing plugged headphones and muting the speaker). Other settings for `jack-sense` can be found in `hdaudio.conf` where you have to change the `hdaudio_jacksense` variable.

*   [Restart](/index.php/Daemon "Daemon") the **oss** daemon for changes take effects.

## Troubleshooting

### Troubleshooting HD Audio devices

#### Understanding the problem

If you have a HD Audio sound device, it is very likely that you will have to adjust some mixer settings before your sound works.

HD Audio devices are very powerful in the sense that they can contain a lot of small circuits (called *widgets*) that can be adjusted by software at any time. These controls are exposed to the mixer, and they can be used, for example, to turn the earphone jack into a sound input jack instead of a sound output jack.

However, there are also bad side effects, mainly because the HD Audio standard is more flexible than it perhaps should be, and because the vendors often only care to get their *official drivers* working.

When using HD Audio devices, you often find disorganized mixer controls, that do not work at all by default, and you are forced to try every mixer control combination possible, until it works.

#### Solution

Open `ossxmix` and try to change every mixer control in the **middle area**, that contains the sound card specific controls, as explained in the [#Volume Control Mixer](#Volume_Control_Mixer) section.

You will probably want to setup a program to record/play continuously in the background (e.g. `ossrecord - | ossplay -` for recording or `osstest -lV` for playing), while changing mixer settings in `ossxmix` in the foreground.

*   Raise every volume control slider.
*   In each option box, try to change the selected option, trying all the possible combinations.
*   If you get noise, try to lower and/or mute some volume controls, until you find the source of the noise.
*   Editing `/usr/lib/oss/conf/oss_hdaudio.conf`, uncommenting and changing `hdaudio_noskip=0` to a value from **0-7** can give you more jack options in `ossxmix`.

**Note:** If you modify this file, [restart](/index.php/Daemon "Daemon") the **oss** daemon for the changes to take effect.

### MMS sound cracking in Totem

If you hear various cracks or strange noises in Totem during playback, you can try using another backend such as [FFmpeg](/index.php/FFmpeg "FFmpeg"). This will not fix the issue that somehow pops up in GStreamer when playing MMS streams but it will give you the option to play it with good sound quality. Playing it in MPlayer is simple:

```
# mplayer mmsh://yourstreamurl

```

### Microphone playing through output channels

By default, OSS plays back the microphone through the speakers. To disable this in `ossxmix` find the *Misc* section and uncheck every `input-mix-mute` box.

## See also

*   [Official Website](http://www.opensound.com/)
*   [OSS Wiki](http://www.opensound.com/wiki)
*   [OSS Forum](http://www.opensound.com/forum/index.php)
*   [Developer Information](http://www.opensound.com/developer/index.html)
*   [Git repository](http://sourceforge.net/p/opensound/git/)
*   [opensound-devel mailing list](http://sourceforge.net/p/opensound/mailman/opensound-devel/)