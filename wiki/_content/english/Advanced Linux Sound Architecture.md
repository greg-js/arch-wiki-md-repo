Related articles

*   [Advanced Linux Sound Architecture/Example Configurations](/index.php/Advanced_Linux_Sound_Architecture/Example_Configurations "Advanced Linux Sound Architecture/Example Configurations")
*   [Advanced Linux Sound Architecture/Troubleshooting](/index.php/Advanced_Linux_Sound_Architecture/Troubleshooting "Advanced Linux Sound Architecture/Troubleshooting")
*   [Sound system](/index.php/Sound_system "Sound system")
*   [PC speaker](/index.php/PC_speaker "PC speaker")
*   [PulseAudio](/index.php/PulseAudio "PulseAudio")
*   [Open Sound System](/index.php/Open_Sound_System "Open Sound System")

The [Advanced Linux Sound Architecture](https://en.wikipedia.org/wiki/Advanced_Linux_Sound_Architecture "wikipedia:Advanced Linux Sound Architecture") (**ALSA**) provides kernel driven sound card drivers. It replaces the original Open Sound System (OSS).

Besides the sound device drivers, ALSA also bundles a user space driven library for application developers. They can then use those ALSA drivers for high level API development. This enables direct (kernel) interaction with sound devices through ALSA libraries.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 User privileges](#User_privileges)
    *   [1.2 ALSA Utilities](#ALSA_Utilities)
    *   [1.3 OSS compatibility](#OSS_compatibility)
    *   [1.4 PulseAudio compatibility](#PulseAudio_compatibility)
    *   [1.5 ALSA and Systemd](#ALSA_and_Systemd)
    *   [1.6 ALSA Firmware](#ALSA_Firmware)
*   [2 Unmuting the channels](#Unmuting_the_channels)
    *   [2.1 Unmute with amixer](#Unmute_with_amixer)
    *   [2.2 Unmute with alsamixer](#Unmute_with_alsamixer)
    *   [2.3 Unmute 5.1/7.1 sound](#Unmute_5.1.2F7.1_sound)
    *   [2.4 Enable the microphone](#Enable_the_microphone)
    *   [2.5 Test your changes](#Test_your_changes)
    *   [2.6 Additional notes](#Additional_notes)
*   [3 Configuration](#Configuration)
    *   [3.1 Basic syntax](#Basic_syntax)
        *   [3.1.1 Assignments and Separators](#Assignments_and_Separators)
        *   [3.1.2 Data types](#Data_types)
        *   [3.1.3 Operation modes](#Operation_modes)
            *   [3.1.3.1 An example of setting default device using "defaults" node](#An_example_of_setting_default_device_using_.22defaults.22_node)
        *   [3.1.4 Nesting](#Nesting)
        *   [3.1.5 Including configuration files](#Including_configuration_files)
    *   [3.2 Set the default sound card](#Set_the_default_sound_card)
        *   [3.2.1 Select the default PCM via environment variable](#Select_the_default_PCM_via_environment_variable)
        *   [3.2.2 Alternative method](#Alternative_method)
    *   [3.3 Verifying correct sound modules are loaded](#Verifying_correct_sound_modules_are_loaded)
    *   [3.4 Getting S/PDIF output](#Getting_S.2FPDIF_output)
    *   [3.5 System-wide equalizer](#System-wide_equalizer)
        *   [3.5.1 Using ALSAEqual (provides UI)](#Using_ALSAEqual_.28provides_UI.29)
            *   [3.5.1.1 Managing ALSAEqual states](#Managing_ALSAEqual_states)
        *   [3.5.2 Using mbeq](#Using_mbeq)
*   [4 High quality resampling](#High_quality_resampling)
*   [5 Upmixing/downmixing](#Upmixing.2Fdownmixing)
    *   [5.1 Upmixing](#Upmixing)
    *   [5.2 Downmixing](#Downmixing)
*   [6 Dmix](#Dmix)
*   [7 Tips and tricks](#Tips_and_tricks)
    *   [7.1 Hot-plugging a USB sound card](#Hot-plugging_a_USB_sound_card)
    *   [7.2 Simultaneous output](#Simultaneous_output)
    *   [7.3 Keyboard volume control](#Keyboard_volume_control)
    *   [7.4 Virtual sound device using snd-aloop](#Virtual_sound_device_using_snd-aloop)
*   [8 See also](#See_also)

## Installation

ALSA is a set of built-in GNU/Linux kernel modules. Therefore, manual installation is not necessary.

[udev](/index.php/Udev "Udev") will automatically detect your hardware and select needed drivers at boot time, therefore, your sound should already be working. However, your sound may be initially muted. If it is, see [Unmuting the channels](#Unmuting_the_channels).

### User privileges

Usually, local users have permission to play audio and change mixer levels.

To allow remote users to use ALSA, you need to [add](/index.php/Users_and_groups#Group_management "Users and groups") those users to the `audio` group.

**Note:** Adding users to the `audio` group allows direct access to devices. Keep in mind, that this allows applications to exclusively reserve output devices. This may break software mixing or fast-user-switching on multi-seat systems. Therefore, adding a user to the `audio` group is **not** recommended by default; unless you specifically need to [[1]](https://wiki.ubuntu.com/Audio/TheAudioGroup).

### ALSA Utilities

[Install](/index.php/Install "Install") the [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils) package. This contains (among other utilities) the `alsamixer` and `amixer` utilities. *amixer* is a shell command to change audio settings, while *alsamixer* provides a more intuitive [ncurses](https://en.wikipedia.org/wiki/Ncurses "wikipedia:Ncurses") based interface for audio device configuration.

If you need [high quality resampling](#High_quality_resampling) install the [alsa-plugins](https://www.archlinux.org/packages/?name=alsa-plugins) package to enable [upmixing/downmixing](#Upmixing.2Fdownmixing) and other advanced features.

### OSS compatibility

**Note:** This is important if your application complains about missing `/dev/dsp` or `/dev/snd/seq`.

ALSA has some ability to intercept [OSS](/index.php/OSS "OSS") calls and re-route them through ALSA instead. This emulation layer is useful e.g. for legacy applications which try to open `/dev/dsp` and write sound data to them directly. Without OSS or the emulation library, `/dev/dsp` will be missing, and the application will not produce any sound.

If you want [OSS](/index.php/OSS "OSS") applications to work with [dmix](#Dmix), install the [alsa-oss](https://www.archlinux.org/packages/?name=alsa-oss) package as well. Then load the `snd-seq-oss`, `snd-pcm-oss` and `snd-mixer-oss` [kernel modules](/index.php/Kernel_modules "Kernel modules") to enable OSS emulation.

### PulseAudio compatibility

[apulse](https://aur.archlinux.org/packages/apulse/) lets you use ALSA for applications that support only [PulseAudio](/index.php/PulseAudio "PulseAudio") for sound. Usage is simply `$ apulse *yourapplication*`.

### ALSA and Systemd

The [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils) package comes with [systemd](/index.php/Systemd "Systemd") unit configuration files `alsa-restore.service` and `alsa-state.service` by default.

These are automatically installed and activated during installation. Therefore, there is no further action needed. Though, you can check their status using `systemctl`.

**Note:** For reference, ALSA stores its settings in `/var/lib/alsa/asound.state`

### ALSA Firmware

The [alsa-firmware](https://www.archlinux.org/packages/?name=alsa-firmware) package contains firmware that may be required for certain sound cards (e.g. Creative SB0400 Audigy2).

## Unmuting the channels

By default ALSA has all channels muted. Those have to be unmuted manually.

### Unmute with amixer

Unmuting the sound card's master volume can be done by using *amixer*:

```
$ amixer sset Master unmute

```

### Unmute with alsamixer

Unmuting the sound card can be done using *alsamixer*:

```
$ alsamixer

```

The `MM` label below a channel indicates that the channel is muted, and `00` indicates that it is open.

Scroll to the `Master` and `PCM` channels with the `←` and `→` keys and unmute them by pressing the `m` key.

Use the `↑` key to increase the volume and obtain a value of `0` dB gain. The gain can be found in the upper left next to the `Item:` field.

**Note:** If gain is set above 0 dB audible distortion can become present.

### Unmute 5.1/7.1 sound

To get full 5.1 or 7.1 surround sound you will likely need to unmute other channels such as `Front`, `Surround`, `Center`, `LFE` (subwoofer) and `Side`. (Those are channel names with Intel HD Audio, they may vary with different hardware)

**Note:** Please take note that this will not automatically upmix stereo sources (like most music). In order to accomplish that, see [#Upmixing/downmixing](#Upmixing.2Fdownmixing).

### Enable the microphone

To enable your microphone, switch to the Capture tab with `F4` and enable a channel with `Space`. See [ALSA/Troubleshooting#Microphone](/index.php/ALSA/Troubleshooting#Microphone "ALSA/Troubleshooting") if microphone does not work.

### Test your changes

Next, test to see if sound works:

```
$ speaker-test -c 2

```

Change `-c` to fit your speaker setup. Use `-c 8` for 7.1, for instance:

```
$ speaker-test -c 8

```

If audio is being outputted to the wrong device, try manually specifying it with the argument `-D`.

```
$ speaker-test -D default:PCH -c 8

```

`-D` accepts PCM channel names as values, which can be retrieved by running the following:

 `$ aplay -L | grep :CARD` 
```
default:CARD=PCH  # 'default:PCH' is the PCM channel name for -D
sysdefault:CARD=PCH
front:CARD=PCH,DEV=0
surround21:CARD=PCH,DEV=0
surround40:CARD=PCH,DEV=0
surround41:CARD=PCH,DEV=0
surround50:CARD=PCH,DEV=0
surround51:CARD=PCH,DEV=0
surround71:CARD=PCH,DEV=0
```

If that does not work, consult the [#Configuration](#Configuration) section or the [ALSA/Troubleshooting](/index.php/ALSA/Troubleshooting "ALSA/Troubleshooting") page.

### Additional notes

*   If your system has more than one soundcard, then you can switch between them by pressing `F6`

*   Some cards need to have digital output muted or disabled in order to hear analog sound. For the Soundblaster Audigy LS mute the channel labeled `IEC958`.

*   Some machines, (like the Thinkpad T61), have a `Speaker` channel which must be unmuted and adjusted as well.

*   Some machines, (like the Dell E6400) may also require the `Front` and `Headphone` channels to be unmuted and adjusted.

*   If your volume adjustments seem to be lost after you reboot, try running *alsamixer* as root.

## Configuration

The system configuration file is `/etc/asound.conf`, and the per-user configuration file is `~/.asoundrc`.

### Basic syntax

ALSA configuration files follow a simple syntax consisting of hierarchical value to parameter (key) assignments. Below are (modified) excerpts from asoundrc.txt, which is usually found in [alsa-lib](https://www.archlinux.org/packages/?name=alsa-lib) package but can be also reached [here](http://www.alsa-project.org/alsa-doc/alsa-lib/conf.html).

#### Assignments and Separators

Assignments define a value of a given key. There are different assignment types and styles available.

 `Simple assignment` 
```
# This is a comment. Everything after the '#' symbol to the end of the line will be ignored by ALSA.
key = value # Equal signs are usually left out, since space can also be used as an separator.

key value # Equivalent to the example above.
```

Separators are used to indicate the start and end of an assignment, but using commas or whitespace is also possible.

 `Separators` 
```
# The following three assignments are equivalent.
key value0; key valueN;
key value0, key valueN,
key value0 key valueN

key
value0
	key
valueN
```

Compound assignments use braces as separators.

 `Compound assignment` 
```
key {	subkey0 value0;
	subkeyN valueN;	}

key.subkey0 value0; # Equivalent to the example above.
key.subkeyN valueN;
```

For easier reading, it is recommended to use first style for definitions including more than three keys.

Array definitions use brackets as separators.

 `Single array` 
```
key [	"value0";
	"valueN";	]

key.0 "value0"; # Equivalent to the example above
key.N "valueN";
```

Everything depends on user preferences when it comes to different styles of configuration, however one should avoid mixing different styles. Further information on basic configuration can be found [here](http://www.volkerschatz.com/noise/alsa.html#basicconf).

#### Data types

ALSA uses different data types for parameter values, which must be set in the users respective configuration file. Some keys accept multiple data types, while most do not. A list of configuration options and their respective type requirements for PCM plugins can be found [here](http://www.alsa-project.org/alsa-doc/alsa-lib/pcm_plugins.html)

#### Operation modes

There are different operation modes for parsing nodes, the default mode is merge and create. If operation mode is either merge/create or merge type checking is done. Only same type assignments can be merged, so strings cannot be merged with integers. Trying to define a simple assignment in default operation mode to a compound (and vice versa) will also not work.

Prefixes of operation modes:

*   "+" -- merge and create
*   "-" -- merge
*   "?" -- do not override
*   "!" -- override

 `Operation modes` 
```
# Merge/create - If a node does not exist, it is created. If it does exist and types match,
# subkeyN is merged into key.
key.subkeyN valueN;

# Merge/create - Equivalent to above
key.+subkeyN valueN;

# Merge - Node key.subkeyN must already exist and must have same data type
key.-subkeyN valueN;

# No override - Ignore new assignment if key.subkeyN node already exists
key.?subkeyN valueN;

# Override - Removes subkeyN and all keys below it, then creates node key.subkeyN
key.!subkeyN valueN;
```

Using override operation mode, when done correctly, is usually safe, however one should bear in mind, that there might be other necessary keys in a node for proper functioning.

**Warning:** Overriding pcm node itself will most definitely make alsa unusable, since every plugin definition will be deleted. Therefore **do not use !pcm.key** unless you are making a configuration from scratch.

##### An example of setting default device using "defaults" node

Assuming that "defaults" node is set in `/usr/share/alsa/alsa.conf`, where "defaults.pcm.card" and its "ctl" counterpart have assignment values "0" (type integer), user wants to set default pcm and control device to (third) sound card "2" or "SB" for an Azalia sound card.

 `Defaults node` 
```
defaults.ctl.card 2; # Sets default device and control to third card (counting begins with 0).
defaults.pcm.card 2; # This does not change the data type.

defaults.ctl.+card 2; # Equivalent to above.
defaults.pcm.+card 2;

defaults.ctl.-card 2; # Same effect on a default setup, however if defaults node was removed or
defaults.pcm.-card 2; # type has been changed merge operation mode will result in no changes.

defaults.pcm.?card 2; # This does nothing, since this assignment already exists.
defaults.ctl.?card 2;

defaults.pcm.!card "SB"; # The override operation mode is necessary here, because of
defaults.ctl.!card "SB"; # different value types.
```

Using double quotes here automatically sets values data type to string, so in the above example setting defaults.pcm.!card "2" would result in retaining last default device, in this case card 0\. Using double quotes for strings is not mandatory as long as no special characters are used, which ideally should never be the case. This may be irrelevant in other assignments.

**Note:** From a configuration point of view those are not equivalent to setting a compound "default" pcm device, since most users specify addressing type in there also, which actually may be the same, but the assignment itself still differs. Also defaults.pcm.card is referred to multiple times in alsa configuration files, usually as a fallback assignment, where different environment variables take precedence.

#### Nesting

Sometimes it may be useful and even easier to read using nesting in configuration.

 `Nesting PCM plugins` 
```
pcm.azalia {	type hw; card 0	}
pcm.!default {	type plug; slave.pcm "azalia"	}

# is equivalent to

pcm.!default {	type plug; slave.pcm {	type hw; card 0;	}	}

# which is also equivalent to

pcm.!default.type plug;
pcm.default.slave.pcm.type hw;
pcm.default.slave.pcm.card 0;
```

#### Including configuration files

 `Include other configuration files` 
```
</path/to/configuration-file> # Include a configuration file
<confdir:/path/to/configuration-file> # Reference to a global configuration directory
```

### Set the default sound card

In addition to the previous instruction regarding `defaults.pcm.card` and `defaults.pcm.device`, if your sound card order changes on boot, you can specify their order in any file ending with `.conf` in `/etc/modprobe.d` (`/etc/modprobe.d/alsa-base.conf` is suggested). For example, if you want your mia sound card to be #0:

 `/etc/modprobe.d/alsa-base.conf` 
```
options snd_mia index=0
options snd_hda_intel index=1
```

Use `$ cat /proc/asound/modules` to get the loaded sound modules and their order. This list is usually all that is needed for the loading order. Use `$ lsmod | grep snd` to get a devices & modules list. This configuration assumes you have one mia sound card using `snd_mia` and one (e.g. onboard) card using `snd_hda_intel`.

You can also provide an index of `-2` to instruct ALSA to never use a card as the primary one. Distributions such as Linux Mint and Ubuntu use the following settings to avoid USB and other "abnormal" drivers from getting index `0`:

 `/etc/modprobe.d/alsa-base.conf` 
```
options bt87x index=-2
options cx88_alsa index=-2
options saa7134-alsa index=-2
options snd-atiixp-modem index=-2
options snd-intel8x0m index=-2
options snd-via82xx-modem index=-2
options snd-usb-caiaq index=-2
options snd-usb-ua101 index=-2
options snd-usb-us122l index=-2
options snd-usb-usx2y index=-2
options snd-pcsp index=-2
options snd-usb-audio index=-2
```

These changes require a system reboot.

See also [[2]](https://bbs.archlinux.org/viewtopic.php?pid=1446773#p1446773)

#### Select the default PCM via environment variable

**Tip:** An explanation of the terminology of a "card", "device", "subdevice" (a "card" is not a "device") and "PCM" can be found on [wikipedia:Advanced Linux Sound Architecture#Concepts](https://en.wikipedia.org/wiki/Advanced_Linux_Sound_Architecture#Concepts "wikipedia:Advanced Linux Sound Architecture").

Probably it is enough to set ALSA_CARD to the name of the device. First, get the names with `aplay -l`, then set ALSA_CARD to the name which comes after the colon and before the bracket; e.g. if you have

`card 1: HDMI [HDA ATI HDMI], device 3: HDMI 0 [HDMI 0]`

then set ALSA_CARD=HDMI.

Other variables are also checked in the default global configuration:

 `/usr/share/alsa/alsa.conf` 
```
Variable name # Definition
ALSA_CARD # pcm.default pcm.hw pcm.plughw ctl.sysdefault ctl.hw rawmidi.default rawmidi.hw hwdep.hw
ALSA_CTL_CARD # ctl.sysdefault ctl.hw
ALSA_HWDEP_CARD # hwdep.default hwdep.hw
ALSA_HWDEP_DEVICE # hwdep.default hwdep.hw
ALSA_PCM_CARD # pcm.default pcm.hw pcm.plughw
ALSA_PCM_DEVICE # pcm.hw pcm.plughw
ALSA_RAWMIDI_CARD # rawmidi.default rawmidi.hw
ALSA_RAWMIDI_DEVICE # rawmidi.default rawmidi.hw
```

Alternatively, you can override the behavior in your own configuration file, preferably the global one (/etc/asound.conf). Add:

```
pcm.!default {
    type plug
    slave.pcm {
        @func getenv
        vars [ ALSAPCM ]
        default "hw:Audigy2"
    }
}
```

In this case as well, replace `Audigy2` with the name of your device. You can get the names with `aplay -l` or you can also use PCMs like **surround51**. But if you need to use the microphone it is a good idea to select full-duplex PCM as default.

Now you can select the sound card when starting programs by just changing the environment variable `ALSAPCM`. It works fine for all program that do not allow to select the card, for the others ensure you keep the default card. For example, assuming you wrote a downmix PCM called `mix51to20` you can use it with [mplayer](https://www.archlinux.org/packages/?name=mplayer) using the commandline `ALSAPCM=mix51to20 mplayer example_6_channel.wav`

**Note:** Pay attention to default addressing type.

#### Alternative method

**Tip:** This process can be partly automated using [asoundconf](https://aur.archlinux.org/packages/asoundconf/).

First you will have to find out the card and device id that you want to set as the default:

 `$ aplay -l` 
```
**** List of PLAYBACK Hardware Devices ****
card 0: Intel [HDA Intel], device 0: CONEXANT Analog [CONEXANT Analog]
  Subdevices: 1/1
  Subdevice #0: subdevice #0
card 0: Intel [HDA Intel], device 1: Conexant Digital [Conexant Digital]
  Subdevices: 1/1
  Subdevice #0: subdevice #0
card 1: JamLab [JamLab], device 0: USB Audio [USB Audio]
  Subdevices: 1/1
  Subdevice #0: subdevice #0
card 2: Audio [Altec Lansing XT1 - USB Audio], device 0: USB Audio [USB Audio]
  Subdevices: 1/1
  Subdevice #0: subdevice #0
```

**Warning:** Simply setting a `type hw` as default card is equivalent to addressing hardware directly, which leaves the device unavailable to other applications. This method is only recommended if it is a part of a more sophisticated setup `~/.asoundrc` or if user deliberately wants to address sound card directly (digital output through `eic958` or dedicated music server for example).

For example, the last entry in this list has the card ID 2 and the device ID 0\. To set this card as the default, you can either use the system-wide file `/etc/asound.conf` or the user-specific file `~/.asoundrc`. You may have to create the file if it does not exist. Then insert the following options with the corresponding card.

```
pcm.!default {
    type hw
    card 2
}

ctl.!default {
    type hw
    card 2
}

```

**Note:** For the Asus U32U series it seems that card should be set to 1 for both pcm and ctl.

In most cases it is recommended to use sound card names instead of number references, which also solves boot order problem. Therefore the following would be correct for the above example.

```
pcm.!default {
    type hw
    card Audio
}

ctl.!default {
    type hw
    card Audio
}

```

To get valid ALSA card names, use *aplay*:

 `$ aplay -l | awk -F \: '/,/{print $2}' | awk '{print $1}' | uniq` 
```
PCH

```

Alternatively use *cat*, which might return unused devices:

 `$ cat /proc/asound/card*/id` 
```
PCH
ThinkPadEC

```

**Note:** This method could be problematic if your system has several cards of the same (ALSA)name.

The 'pcm' options affect which card and device will be used for audio playback while the 'ctl' option affects which card is used by control utilities like alsamixer .

The changes should take effect as soon as you (re-)start an application (MPlayer etc.). You can also test with a command like *aplay*.

```
$ aplay -D default:PCH *your_favourite_sound.wav*

```

If you receive an error regarding your asound configuration, check the [upstream documentation](http://www.alsa-project.org/main/index.php/Asoundrc#The_default_plugin) for possible changes to the configuration file format.

### Verifying correct sound modules are loaded

You can assume that udev will autodetect your sound properly. You can check this with the command:

 `$ lsmod | grep '^snd' | column -t` 
```
snd_hda_codec_hdmi     22378   4
snd_hda_codec_realtek  294191  1
snd_hda_intel          21738   1
snd_hda_codec          73739   3  snd_hda_codec_hdmi,snd_hda_codec_realtek,snd_hda_intel
snd_hwdep              6134    1  snd_hda_codec
snd_pcm                71032   3  snd_hda_codec_hdmi,snd_hda_intel,snd_hda_codec
snd_timer              18992   1  snd_pcm
snd                    55132   9  snd_hda_codec_hdmi,snd_hda_codec_realtek,snd_hda_intel,snd_hda_codec,snd_hwdep,snd_pcm,snd_timer
snd_page_alloc         7017    2  snd_hda_intel,snd_pcm
```

If the output looks similar, your sound drivers have been successfully autodetected.

**Note:** Since `udev>=171`, the OSS emulation modules (`snd_seq_oss, snd_pcm_oss, snd_mixer_oss`) are not loaded by default: [Load them manually](/index.php/Kernel_modules#Manual_module_handling "Kernel modules"), if they are needed.

You might also want to check the directory `/dev/snd/` for the right device files:

 `$ ls -l /dev/snd` 
```
total 0
crw-rw----  1 root audio 116,  0 Apr  8 14:17 controlC0
crw-rw----  1 root audio 116, 32 Apr  8 14:17 controlC1
crw-rw----  1 root audio 116, 24 Apr  8 14:17 pcmC0D0c
crw-rw----  1 root audio 116, 16 Apr  8 14:17 pcmC0D0p
crw-rw----  1 root audio 116, 25 Apr  8 14:17 pcmC0D1c
crw-rw----  1 root audio 116, 56 Apr  8 14:17 pcmC1D0c
crw-rw----  1 root audio 116, 48 Apr  8 14:17 pcmC1D0p
crw-rw----  1 root audio 116,  1 Apr  8 14:17 seq
crw-rw----  1 root audio 116, 33 Apr  8 14:17 timer
```

**Note:** If requesting help on IRC or the forums, please post the output of the above commands, if requested.

If you have at least the devices **controlC0** and **pcmC0D0p** or similar, then your sound modules have been detected and loaded properly.

If this is not the case, your sound modules have not been detected properly. To solve this, you can try loading the modules manually:

*   Locate the module for your sound card: [ALSA Soundcard Matrix](http://www.alsa-project.org/main/index.php/Matrix:Main) The module will be prefixed with 'snd-' (for example: `snd-via82xx`).
*   [Load the module](/index.php/Kernel_modules#Manual_module_handling "Kernel modules").
*   Check for the device files in `/dev/snd` (see above) and/or try if `alsamixer` or `amixer` have reasonable output.
*   Configure `snd-NAME-OF-MODULE` and `snd-pcm-oss` to [load at boot](/index.php/Kernel_modules#Automatic_module_handling "Kernel modules").

### Getting S/PDIF output

[S/PDIF](https://en.wikipedia.org/wiki/S/PDIF "wikipedia:S/PDIF") is a digital audio interface often used to connect a computer to a digital amplifier (such as a home theatre with 5.1/7.1 surround sound).

**Note:** With some soundcards this disables analog sound output (eg. Sound Blaster Audigy 2).

Depending on what [shell](/index.php/Shell "Shell") you use, add the following line to your shell's configuration file:

```
amixer -c 0 cset name='IEC958 Playback Switch' on

```

You can see the name of your card's digital output with:

```
$ amixer scontrols

```

### System-wide equalizer

#### Using ALSAEqual (provides UI)

Install the [alsaequal](https://aur.archlinux.org/packages/alsaequal/) package. Also install [lib32-alsaequal](https://aur.archlinux.org/packages/lib32-alsaequal/) for 32-bit application support.

After installing the package, add the following to your ALSA configuration file:

 `/etc/asound.conf` 
```
ctl.equal {
    type equal;
}

pcm.plugequal {
    type equal;
    # Modify the line below if you do not
    # want to use sound card 0.
    #slave.pcm "plughw:0,0";
    # by default we want to play from more sources at time:
    slave.pcm "plug:dmix";
}

# pcm.equal {
# If you do not want the equalizer to be your
# default soundcard comment the following
# line and uncomment the above line. (You can
# choose it as the output device by addressing
# it with specific apps,eg mpg123 -a equal 06.Back_In_Black.mp3)
pcm.!default {
    type plug;
    slave.pcm plugequal;
}
```

If you have a x86_64-system and are using [lib32-flashplugin](https://www.archlinux.org/packages/?name=lib32-flashplugin) the sound in flash will not work with the above configuration. The configuration below enables sound in flash, but you have to specify the sound card manually in the line `pcm "hw:0,0"` (use `aplay -l` to list the available sound card and relative card and device number):

 `/etc/asound.conf` 
```
pcm.dmixer {
    type dmix
    ipc_key 2048
    slave {
        pcm "hw:0,0"
        buffer_size 16384
    }
}

ctl.equal {
    type equal;
}

pcm.equalizer {
    type equal
    slave.pcm "plug:dmixer"
}

pcm.!default {
    type plug
    slave.pcm equalizer
}
```

And you are ready to change your equalizer using command

```
$ alsamixer -D equal

```

Note that configuration file is different for each user (until not specified else) it is saved in `~/.alsaequal.bin`. so if you want to use ALSAEqual with [mpd](/index.php/Mpd "Mpd") or another software running under different user, you can configure it using

```
$ su mpd -c 'alsamixer -D equal'

```

or for example, you can make a symlink to your `.alsaequal.bin` in his home...

##### Managing ALSAEqual states

Install the [alsaequal-mgr](https://aur.archlinux.org/packages/alsaequal-mgr/) package.

Configure the equalizer as usual with

```
$ alsamixer -D equal

```

When you are satisfied with the state, you may give it a name ("foo" in this example) and save it:

```
$ alsaequal-mgr save foo

```

The state "foo" can then be restored at a later time with

```
$ alsaequal-mgr load foo

```

You can thus create different equalizer states for games, movies, music genres, VoIP apps, etc. and reload them as necessary.

See the [project page](http://xyne.archlinux.ca/projects/alsaequal-mgr/) and the help message for more options.

#### Using mbeq

**Note:** This method requires the use of a [LADSPA](https://en.wikipedia.org/wiki/LADSPA "wikipedia:LADSPA") plugin which might be CPU intensive during playback. In addition, this was made with stereophonic sound (e.g. headphones) in mind.

Install the [alsa-plugins](https://www.archlinux.org/packages/?name=alsa-plugins), [ladspa](https://www.archlinux.org/packages/?name=ladspa) and [swh-plugins](https://www.archlinux.org/packages/?name=swh-plugins) packages if you do not already have them.

If you have not already created either an `~/.asoundrc` or a `/etc/asound.conf` file, then create either one and insert the following:

 `/etc/asound.conf` 
```
pcm.eq {
    type ladspa

    # The output from the EQ can either go direct to a hardware device
    # (if you have a hardware mixer, e.g. SBLive/Audigy) or it can go
    # to the software mixer shown here.
    #slave.pcm "plughw:0,0"
    slave.pcm "plug:dmix"

    # Sometimes you may need to specify the path to the plugins,
    # especially if you have just installed them.  Once you have logged
    # out/restarted this should not be necessary, but if you get errors
    # about being unable to find plugins, try uncommenting this.
    #path "/usr/lib/ladspa"

    plugins [
    {
        label mbeq
        id 1197
        input {
            # The following setting is just an example, edit to your own taste:
            # bands: 50hz, 100hz, 156hz, 220hz, 311hz, 440hz, 622hz, 880hz, 1250hz, 1750hz, 25000hz,
            # 50000hz, 10000hz, 20000hz
            controls [ -5 -5 -5 -5 -5 -10 -20 -15 -10 -10 -10 -10 -10 -3 -2 ]
            }
        }
    ]
}

# Redirect the default device to go via the EQ - you may want to do
# this last, once you are sure everything is working.  Otherwise all
# your audio programs will break/crash if something has gone wrong.
pcm.!default {
    type plug
    slave.pcm "eq"
}

# Redirect the OSS emulation through the EQ too (when programs are running through "aoss")
pcm.dsp0 {
    type plug
    slave.pcm "eq"
}
```

## High quality resampling

When software mixing is enabled, ALSA is forced to resample everything to the same frequency (48 kHz by default when supported). By default, it will try to use the *speexrate* converter to do so, and fallback to low-quality linear interpolation if it is not available[[3]](http://git.alsa-project.org/?p=alsa-lib.git;a=blob;f=src/pcm/pcm_rate.c;h=2eb4b1b33933dec878d0f25ad118869adac95767;hb=HEAD#l1278). Thus, if you are getting poor sound quality due to bad resampling, the problem can be solved by simply installing the [alsa-plugins](https://www.archlinux.org/packages/?name=alsa-plugins) package.

For even higher quality resampling, you can change the default rate converter to `speexrate_medium` or `speexrate_best`. Both perform well enough that in practice it does not matter which one you choose, so using the best converter is usually not worth the extra CPU cycles it requires.

To change the default converter place the following contents in your `~/.asoundrc` or `/etc/asound.conf`:

 `/etc/asound.conf` 
```
defaults.pcm.rate_converter "speexrate_medium"

```

**Note:** It is also possible to use [libsamplerate](https://www.archlinux.org/packages/?name=libsamplerate) converters, which are only about half as fast as the *speexrate* converters but do not achieve much higher quality. See [discussion](/index.php/Talk:Advanced_Linux_Sound_Architecture#On_high_quality_resampling "Talk:Advanced Linux Sound Architecture").

**Note:** It is also possible to use lavcrate resamplers that use [ffmpeg](https://www.archlinux.org/packages/?name=ffmpeg) With filter sizes of lavcrate_faster:4 lavcrate_fast:8 lavcrate:16 lavcrate_high:32 lavcrate_higher:64 With the last 2 options being equal to Kodi low and medium quality resamplers respectively

**Note:** Some applications (like MPlayer and its forks) do their own resampling by default because some ALSA drivers have incorrect delay reporting when resampling is enabled (hence leading to AV desynchronization), so changing this setting will not have any effect unless you configure them to use ALSA resampling.

## Upmixing/downmixing

### Upmixing

In order for stereo sources like music to be able to saturate a 5.1 or 7.1 sound system, you need to use upmixing. In darker days this used to be tricky and error prone but nowadays plugins exist to easily take care of this task. We will use the `upmix` plugin, included in the [alsa-plugins](https://www.archlinux.org/packages/?name=alsa-plugins) package.

Then add the following to your ALSA configuration file of choice (either `/etc/asound.conf` or `~/.asoundrc`):

```
pcm.upmix71 {
    type upmix
    slave.pcm "surround71"
    delay 15
    channels 8
}

```

You can easily change this example for 7.1 upmixing to 5.1 or 4.0.

The following example adds a new PCM channel that you can use for upmixing. If you want all sound sources to go through this channel, add it as a default below the previous definition like so:

```
pcm.!default "plug:upmix71"

```

The plugin automatically allows multiple sources to play through it without problems so setting is as a default is actually a safe choice. If this is not working, you have to setup your own dmixer for the upmixing PCM like this:

```
pcm.dmix6 {
    type asym
    playback.pcm {
        type dmix
        ipc_key 567829
        slave {
            pcm "hw:0,0"
            channels 6
        }
    }
}
```

and use "dmix6" instead of "surround71". If you experience skipping or distorted sound, consider increasing the buffer_size (to 32768, for example) or use a [high quality resampler](#High_quality_resampling).

### Downmixing

If you want to downmix sources to stereo because you, for instance, want to watch a movie with 5.1 sound on a stereo system, use the `vdownmix` plugin, included in the [alsa-plugins](https://www.archlinux.org/packages/?name=alsa-plugins) package.

Again, in your configuration file, add this:

```
pcm.!surround51 {
    type vdownmix
    slave.pcm "default"
}
pcm.!surround40 {
    type vdownmix
    slave.pcm "default"
}
```

**Note:** This might not be enough to make downmixing working, see [[4]](http://bugs.debian.org/cgi-bin/bugreport.cgi?bug=541786). So, you might also need to add `pcm.!default "plug:surround51"` or `pcm.!default "plug:surround40"`. Only one `vdownmix` plug can be used; if you have 7.1 channels, you will need to use `surround71` instead the configuration above. A good example, which includes a configuration that makes both `vdownmix` and `dmix` working, can be found [here](https://bbs.archlinux.org/viewtopic.php?id=167275).

## Dmix

Mixing enables multiple applications to output sound at the same time. Most discrete sound cards support hardware mixing, which is enabled by default if available. Integrated motherboard sound cards (such as Intel HD Audio), usually do not support hardware mixing. On such cards, software mixing is done by an ALSA plugin called `dmix`. This feature is enabled automatically if hardware mixing is unavailable.

**Note:** Dmix is enabled by default for soundcards which do not support hardware mixing. Dmix is not enabled by default for digital output (S/PDIF) and will require the configuration snippet below.

To manually enable dmix, add the following to your ALSA configuration file:

 `/etc/asound.conf` 
```
pcm.dsp {
    type plug
    slave.pcm "dmix"
}
```

## Tips and tricks

### Hot-plugging a USB sound card

See [Writing Udev rules for ALSA](http://alsa.opensrc.org/Udev).

### Simultaneous output

You might want to play music via external speakers connected via mini jack and internal speakers simultaneously. This can be done by unmuting **Auto-Mute** item using `alsamixer` or `amixer`:

```
$ amixer sset "Auto-Mute" unmute

```

and then unmuting other required items, such as **Headphones**, **Speaker**, **Bass Speaker**...

**Note:** If you have a crackling sound through headphones connector (mini-jack) after, see [here](/index.php/ALSA/Troubleshooting#Crackling_sound_through_mini-jack_.28headphones_connector.29 "ALSA/Troubleshooting").

### Keyboard volume control

Map the following commands to your volume keys: `XF86AudioRaiseVolume`, `XF86AudioLowerVolume`, `XF86AudioMute`

To raise the volume:

```
amixer set Master 5%+

```

To lower the volume:

```
amixer set Master 5%-

```

To toggle mute/unmute of the volume:

```
amixer set Master toggle

```

### Virtual sound device using snd-aloop

You might want a jack alternative to create a virtual recording or play device in order to mix different sources, using the snd-aloop module:

```
modprobe snd-aloop

```

List your new virtual devices using:

```
aplay -l

```

now you can for example using ffmpeg:

```
ffmpeg -f alsa -i hw:1,1,0 -f alsa -i hw:1,1,1 -filter_complex amerge output.mp3

```

In the hw:R,W,N format R is your virtual card device number, W 1 recording devices 0 for writing, R is your sub device you can use all the virtual devices available and play/stop using applications like mplayer:

```
mplayer -ao alsa:device=hw=1,0,0 fileA
mplayer -ao alsa:device=hw=1,0,1 fileB 

```

Another thing you could do with this approach, is using festival to generate a voice into a recording stream using an script like this:

```
#!/bin/bash
echo $1|iconv -f utf-8 -t iso-8859-1| text2wave  > "_tmp_.wav";   
mplayer -ao alsa:device=hw=2,0,0 "_tmp.wav";
rm "_tmp.wav";

```

## See also

*   [ALSA wiki](http://www.alsa-project.org/)
*   [Asoundrc](http://www.alsa-project.org/main/index.php/Asoundrc)
*   [Unofficial ALSA wiki](http://alsa.opensrc.org/)
*   [Advanced ALSA module configuration](http://www.mjmwired.net/kernel/Documentation/sound/alsa/ALSA-Configuration.txt)
*   [HOWTO: compile driver from svn](https://bbs.archlinux.org/viewtopic.php?id=36815)
*   [A close look at ALSA: ALSA concept introduction](http://www.volkerschatz.com/noise/alsa.html)
*   [Linux ALSA sound notes](http://www.sabi.co.uk/Notes/linuxSoundALSA.html)