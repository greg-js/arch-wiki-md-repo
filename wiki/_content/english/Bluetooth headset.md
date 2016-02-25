Currently, Arch Linux supports the A2DP profile (Audio Sink) for remote audio playback with the default installation.

**Note:** Bluez5 is only supported by [PulseAudio](/index.php/PulseAudio "PulseAudio") and not by [ALSA](/index.php/ALSA "ALSA"). If you do not want to use PulseAudio, you need to install an older Bluez version from the AUR.

## Contents

*   [1 Headset via Bluez5/PulseAudio](#Headset_via_Bluez5.2FPulseAudio)
    *   [1.1 Troubleshooting](#Troubleshooting)
        *   [1.1.1 Selected audio profile, but headset inactive and audio cannot be redirected](#Selected_audio_profile.2C_but_headset_inactive_and_audio_cannot_be_redirected)
        *   [1.1.2 Pairing fails with AuthenticationFailed](#Pairing_fails_with_AuthenticationFailed)
        *   [1.1.3 Pairing works, but connecting does not](#Pairing_works.2C_but_connecting_does_not)
        *   [1.1.4 Connecting works, but I cannot play sound](#Connecting_works.2C_but_I_cannot_play_sound)
        *   [1.1.5 UUIDs has unsupported type](#UUIDs_has_unsupported_type)
*   [2 Legacy method: ALSA-BTSCO](#Legacy_method:_ALSA-BTSCO)
    *   [2.1 Connecting the headset](#Connecting_the_headset)
        *   [2.1.1 Pairing the headset with your computer](#Pairing_the_headset_with_your_computer)
            *   [2.1.1.1 Using *bluez-gnome*](#Using_bluez-gnome)
            *   [2.1.1.2 Using *passkey-agent*](#Using_passkey-agent)
    *   [2.2 Headset and ALSA Devices](#Headset_and_ALSA_Devices)
    *   [2.3 Headset's multimedia buttons](#Headset.27s_multimedia_buttons)
*   [3 Legacy method: PulseAudio](#Legacy_method:_PulseAudio)
    *   [3.1 Troubleshooting](#Troubleshooting_2)
        *   [3.1.1 Audio sink fails](#Audio_sink_fails)
        *   [3.1.2 Page timeout issue](#Page_timeout_issue)
*   [4 Legacy documentation: ALSA, bluez5 and PulseAudio method](#Legacy_documentation:_ALSA.2C_bluez5_and_PulseAudio_method)
    *   [4.1 Install Software Packages](#Install_Software_Packages)
        *   [4.1.1 Install ALSA and associated libraries](#Install_ALSA_and_associated_libraries)
        *   [4.1.2 Install Bluez5](#Install_Bluez5)
        *   [4.1.3 Install Audacious](#Install_Audacious)
    *   [4.2 Procedure](#Procedure)
        *   [4.2.1 Miscellaneous configuration files](#Miscellaneous_configuration_files)
            *   [4.2.1.1 ALSA /etc/asound.conf](#ALSA_.2Fetc.2Fasound.conf)
            *   [4.2.1.2 /etc/dbus-1/system.d/bluetooth.conf](#.2Fetc.2Fdbus-1.2Fsystem.d.2Fbluetooth.conf)
            *   [4.2.1.3 Tested applications](#Tested_applications)
*   [5 Switch between HSV and A2DP setting](#Switch_between_HSV_and_A2DP_setting)
    *   [5.1 A2DP not working with PulseAudio](#A2DP_not_working_with_PulseAudio)
        *   [5.1.1 Socket interface problem](#Socket_interface_problem)
        *   [5.1.2 Gnome with GDM](#Gnome_with_GDM)
*   [6 Tested headsets](#Tested_headsets)
*   [7 See also](#See_also)

## Headset via Bluez5/PulseAudio

PulseAudio 5.x supports A2DP per default. Make sure the following packages are [installed](/index.php/Install "Install"): [pulseaudio-alsa](https://www.archlinux.org/packages/?name=pulseaudio-alsa), [pulseaudio-bluetooth](https://www.archlinux.org/packages/?name=pulseaudio-bluetooth), [bluez](https://www.archlinux.org/packages/?name=bluez), [bluez-libs](https://www.archlinux.org/packages/?name=bluez-libs), [bluez-utils](https://www.archlinux.org/packages/?name=bluez-utils), [bluez-firmware](https://www.archlinux.org/packages/?name=bluez-firmware). Without [pulseaudio-bluetooth](https://www.archlinux.org/packages/?name=pulseaudio-bluetooth) you won't be able to connect after the next pairing and you won't get any usable error messages.

Start the Bluetooth system:

```
# systemctl start bluetooth

```

Now we can use the *bluetoothctl* command line utility to pair and connect. For troubleshooting and more detailed explanations of *bluetoothctl* see the [Bluetooth](/index.php/Bluetooth "Bluetooth") article. Run

```
# bluetoothctl

```

to be greeted by its internal command prompt. Then enter:

```
# power on
# agent on
# default-agent
# scan on

```

Now make sure that your headset is in pairing mode. It should be discovered shortly. For example,

```
[NEW] Device 00:1D:43:6D:03:26 Lasmex LBT10

```

shows a device that calls itself "Lasmex LBT10" and has MAC address *00:1D:43:6D:03:26*. We will now use that MAC address to initiate the pairing:

```
# pair 00:1D:43:6D:03:26

```

After pairing, you also need to explicitly connect the device (every time?):

```
# connect 00:1D:43:6D:03:26

```

If everything works correctly, you now have a separate output device in [PulseAudio](/index.php/PulseAudio "PulseAudio").

**Note:** The device may be off by default. Select its audio profile (*OFF*, A2DP, HFP) in the "Configuration" tab of [pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol).

You can now redirect any audio through that device using the "Playback" and "Recording" tabs of [pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol).

You can now disable scanning again and exit the program:

```
# scan off
# exit

```

### Troubleshooting

Many users report frustration with getting A2DP/Bluetooth Headsets to work.

#### Selected audio profile, but headset inactive and audio cannot be redirected

Deceptively, this menu is available before the device has been connected; annoyingly it will have no effect. The menu seems to be created as soon as the receiver recognizes the device.

Make sure to run bluetoothctl (with sudo/as root) and connect the device manually. There may be configuration options to remove the need to do this each time, but neither pairing nor trusting induce automatic connecting for me.

#### Pairing fails with AuthenticationFailed

If pairing fails, you can try [disabling SSPMode](https://stackoverflow.com/questions/12888589/linux-command-line-howto-accept-pairing-for-bluetooth-device-without-pin) with:

```
# hciconfig hci0 sspmode 0

```

#### Pairing works, but connecting does not

You might see the following error in *bluetoothctl*:

```
[bluetooth]# connect 00:1D:43:6D:03:26
Attempting to connect to 00:1D:43:6D:03:26
Failed to connect: org.bluez.Error.Failed

```

To further investigate, have a look at the log via one of the following commands:

```
# systemctl status bluetooth
# journalctl -n 20

```

You might see a message like this:

```
bluetoothd[5556]: a2dp-sink profile connect failed for 00:1D:43:6D:03:26: Protocol not available

```

This may be due to the [pulseaudio-bluetooth](https://www.archlinux.org/packages/?name=pulseaudio-bluetooth) package not being installed. Install it if it missing, then restart pulseaudio.

If the issue is not due to the missing package, the problem in this case is that PulseAudio is not catching up. A common solution to this problem is to restart PulseAudio. Note that it is perfectly fine to run *bluetoothctl* as root while PulseAudio runs as user. After restarting PulseAudio, retry to connect. It is not necessary to repeat the pairing.

If restarting PulseAudio does not work, you need to load module-bluetooth-discover.

```
# pactl load-module module-bluetooth-discover

```

The same load-module command can be added to `/etc/pulse/default.pa`.

If that still does not work, or you are using PulseAudio's system-wide mode, also load the following PulseAudio modules (again these can be loaded via your default.pa or system.pa):

```
module-bluetooth-policy
module-bluez5-device
module-bluez5-discover

```

To have your headset auto connect you need to enable PulseAudio's switch-on-connect module. Add the following:

 `/etc/pulse/default.pa` 
```
# automatically switch to newly-connected devices
load-module module-switch-on-connect

```

You then need to tell *bluetoothctl* to trust your Bluetooth headset, or you will see errors like this:

```
bluetoothd[487]: Authentication attempt without agent
bluetoothd[487]: Access denied: org.bluez.Error.Rejected

```

```
[bluetooth]# trust 00:1D:43:6D:03:26

```

After a reboot, your Bluetooth adapter will not power on by default. You need to add a udev rule to power it on:

 `/etc/udev/rules.d/10-local.rules` 
```
# Set bluetooth power up
ACTION=="add", SUBSYSTEM=="bluetooth", KERNEL=="hci[0-9]*", RUN+="/usr/bin/hciconfig %k up"
```

#### Connecting works, but I cannot play sound

Make sure that you see the following messages in your system log:

```
bluetoothd[5556]: Endpoint registered: sender=:1.83 path=/MediaEndpoint/A2DPSource
bluetoothd[5556]: Endpoint registered: sender=:1.83 path=/MediaEndpoint/A2DPSink

```

If you see a message similar to this, you can go on and investigate your PulseAudio configuration. Otherwise, go back and ensure the connection is successful.

When using [GDM](/index.php/GDM "GDM"), another instance of PulseAudio is started, which "captures" your bluetooth device connection. This can be prevented by [masking](/index.php/Mask "Mask") the pulseaudio socket for the GDM user by doing the following:

```
$ mkdir -p ~gdm/.config/systemd/user
$ ln -s /dev/null ~gdm/.config/systemd/user/pulseaudio.socket

```

On next reboot the second instance of PulseAudio will not be started.

#### UUIDs has unsupported type

During pairing you might see this output in *bluetoothctl*:

```
[CHG] Device 00:1D:43:6D:03:26 UUIDs has unsupported type

```

This message is a very common one and can be ignored.

## Legacy method: ALSA-BTSCO

It is much easier to set up your bluetooth headset today, with bluez >= 3.16\. You may want to try the out-of-box python script in [this blog](http://fosswire.com/2008/01/11/a2dp-stereo-linux/) (you need edit the script to work with gconftool-2). There is also a piece of equivalent bash script [here](http://lymanrb.blogspot.com/2008/05/linux.html).

You need your headset's bdaddr. It is of the form *12:34:56:78:9A:BC*. Either find it in the documentation of your headset, on the headset itself or with the **hcitool scan** command.

Install [btsco](https://aur.archlinux.org/packages/btsco/).

To load the kernel module, type:

```
# modprobe snd-bt-sco

```

There will now be an extra audio device. Use `alsamixer -cN` (where N is most likely 1) to set the volume. You can access the device with any alsa-capable application by choosing the device *BT headset*, or with any OSS application by using `/dev/dspN` as the audio device.

But to actually get any sound, you have to connect your headset to the computer first.

### Connecting the headset

If you connect your headset for the first time, read the section about pairing first. To connect to your headset to the computer, use the command

```
$ btsco -f <bdaddr>

```

for example

```
$ btsco -f 12:34:56:78:9A:BC

```

#### Pairing the headset with your computer

The first time you connect the headset, you have to pair it with the computer. To do this, you need your headset's PIN. Depending on your headset you may have to reset the headset and repeat the pairing everytime you used the headset with another bluetooth device.

There are two ways to pair your headset with the computer:

##### Using *bluez-gnome*

Install the *bluez-gnome* package from the community repository. Then start the **bt-applet** program. Once you try to connect to the headset, a window will open and ask for the PIN.

##### Using *passkey-agent*

Before connecting to the headset, enter the command

```
$ passkey-agent --default <pin>

```

where *<pin>* is your headset's PIN. Then try to connect to the headset.

### Headset and ALSA Devices

1\. First if you have not already, [install](/index.php/Install "Install") [bluez](https://www.archlinux.org/packages/?name=bluez) from the [official repositories](/index.php/Official_repositories "Official repositories").

2\. Scan for your device

```
$ hcitool (-i <optional hci#>***) scan

```

3\. Pair your headset with your device:

```
$ bluez-simple-agent (optional hci# ***) XX:XX:XX:XX:XX:XX

```

and put in your pin (0000 or 1234, etc)

4\. Make sure your `/etc/bluetooth/audio.conf` allows A2DP Audio Sinks. Place this line just bellow the [General] heading:

```
Enable=Source,Sink,Media,Socket

```

5\. Add this to your `/etc/asound.conf` file:

```
#/etc/asound.conf

pcm.btheadset {
   type plug
   slave {
       pcm {
           type bluetooth
           device XX:XX:XX:XX:XX:XX 
           profile "auto"
       }   
   }   
   hint {
       show on
       description "BT Headset"
   }   
}
ctl.btheadset {
  type bluetooth
}  

```

6\. Check to see if it has been added to alsa devices

```
$ aplay -L

```

7\. Now play with aplay:

```
$ aplay -D btheadset /path/to/audio/file

```

or Mplayer:

```
$ mplayer -ao alsa:device=btheadset /path/to/audio/or/video/file

```

**Tip:** To find hci# for a usb dongle, type in
```
$ hcitool dev

```

### Headset's multimedia buttons

In order to get your bluetooth headset's multimedia buttons (play, pause, next, previous) working you need to create `/etc/modules-load.d/uinput.conf` containing `uinput`.

## Legacy method: PulseAudio

This one is much easier and more elegant. PulseAudio will seamlessly switch between output devices when the headset is turned on. If you have ALSA as the sound server, you need the following packages installed: [pulseaudio](https://www.archlinux.org/packages/?name=pulseaudio) and [pulseaudio-alsa](https://www.archlinux.org/packages/?name=pulseaudio-alsa).

Now, to configure the audio output to use bluetooth, just install [pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol) and run it to configure the audio output:

```
$ pavucontrol

```

Make sure to take a look at the [PulseAudio](/index.php/PulseAudio "PulseAudio") wiki entry for setting up PulseAudio, especially if you are running KDE.

### Troubleshooting

#### Audio sink fails

Bluetooth headset is connected, but ALSA/PulseAudio fails to pick up the connected device. You will get "Audio sink fails". According to [gentoo wiki](http://wiki.gentoo.org/wiki/Bluetooth_Headset), you have to verify than in `/etc/bluetooth/audio.conf` there is `Enable=Socket` under the `[General]` section heading.

Just do a `# systemctl restart bluetooth` to apply it.

#### Page timeout issue

If you receive this error whilst trying to pair your headset with your system using bluez-simple-agent, then you can try to restart your system and use the graphical bluez applet of your desktop environment.

## Legacy documentation: ALSA, bluez5 and PulseAudio method

[ALSA](/index.php/ALSA "ALSA"), [bluez5](/index.php/Bluez "Bluez"), and [PulseAudio](/index.php/PulseAudio "PulseAudio") work together to allow a wireless [Bluetooth](/index.php/Bluetooth "Bluetooth") headset to play audio. The following method works with a Lenovo T61p laptop and SoundBot SB220 wireless bluetooth headset. The required software stack is extensive and failure to include all components can produce errors which are difficult to understand. The following list of software packages might not be the minimum required set and needs to be examined more closely.

Bluez5 has a regression causing HSP/HFP Telephone profile to not be available. This regression is documented in the [draft release notes for Pulseaudio 5.0](http://www.freedesktop.org/wiki/Software/PulseAudio/Notes/5.0/) which say (in "Notes for packagers"): "PulseAudio now supports BlueZ 5, but only the A2DP profile. BlueZ 4 is still the only way to make HSP/HFP work." ([from here](https://fedoraproject.org/wiki/Common_F20_bugs#bluez5-profile))

### Install Software Packages

The core software components are [ALSA](/index.php/ALSA "ALSA"), Bluez5, [PulseAudio](/index.php/PulseAudio "PulseAudio"). However there are additional libraries which are required. As well as a player which can play audio files. The following section lists the software packages installed in order to connect the headset and play audio over the headset.

#### Install ALSA and associated libraries

[ALSA](/index.php/ALSA "ALSA") works with the linux kernel to provide audio services to user mode software. The following packages are used with the [Bluetooth](/index.php/Bluetooth "Bluetooth") headset: [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils), [alsa-plugins](https://www.archlinux.org/packages/?name=alsa-plugins), [alsa-tools](https://www.archlinux.org/packages/?name=alsa-tools).

#### Install Bluez5

Bluez5 is the latest [Bluetooth](/index.php/Bluetooth "Bluetooth") stack. It is required for [PulseAudio](/index.php/PulseAudio "PulseAudio") to interface with wireless headsets. Required packages: [bluez](https://www.archlinux.org/packages/?name=bluez), [bluez-utils](https://www.archlinux.org/packages/?name=bluez-utils), [bluez-libs](https://www.archlinux.org/packages/?name=bluez-libs).

#### Install Audacious

[Audacious](/index.php/Audacious "Audacious") is a program which plays audio files. It can work directly with [ALSA](/index.php/ALSA "ALSA") or with [PulseAudio](/index.php/PulseAudio "PulseAudio"). Required packages: [audacious](https://www.archlinux.org/packages/?name=audacious), [audacious-plugins](https://www.archlinux.org/packages/?name=audacious-plugins).

### Procedure

Once the required packages are installed, use this procedure to play audio with a bluetooth headset. The high level overview of the procedure is to pair the headset, connect the headset, configure the player and pulse audio controller and then play audio.

Start the bluetooth service as root:

```
# systemctl start bluetooth

```

Verify Bluetooth is started

```
# systemctl status bluetooth
bluetooth.service - Bluetooth service
  Loaded: loaded (/usr/lib/systemd/system/bluetooth.service; disabled)
  Active: active (running) since Sat 2013-12-07 12:31:14 PST; 12s ago
    Docs: man:bluetoothd(8)
Main PID: 3136 (bluetoothd)
  Status: "Running"
  CGroup: /system.slice/bluetooth.service
          └─3136 /usr/lib/bluetooth/bluetoothd

Dec 07 12:31:14 t61p systemd[1]: Starting Bluetooth service...
Dec 07 12:31:14 t61p bluetoothd[3136]: Bluetooth daemon 5.11
Dec 07 12:31:14 t61p systemd[1]: Started Bluetooth service.
Dec 07 12:31:14 t61p bluetoothd[3136]: Starting SDP server
Dec 07 12:31:14 t61p bluetoothd[3136]: Bluetooth management interface 1.3 i...ed
Hint: Some lines were ellipsized, use -l to show in full.

```

Start the PulseAudio daemon. This must be done after X windows is started and as a normal user.

```
$ pulseaudio -D

```

Verify the PulseAudio daemon is running.

```
$ pulseaudio --check -v
I: [pulseaudio] main.c: Daemon running as PID 3186

```

Start up bluetoothctl as root and pair and connect your headset. As a regular user, bluetoothctl will pair but not connect. Perhaps this is related to the config file (shown below) which is setup for what appears to be the root user. Note: the procedure shown below is for an initial pair and connect of the headphone. If the headset is already paired, then the procedure below can be shortened to: power on, agent on, default-agent, connect <mac address>. The mac address can be seen from the devices command output.

```
 $ bluetoothctl 
 [NEW] Controller 00:1E:4C:F4:98:5B t61p-0 [default]
 [NEW] Device 00:1A:7D:12:36:B9 SoundBot SB220
 [bluetooth]# show
 Controller 00:1E:4C:F4:98:5B
       Name: t61p
       Alias: t61p-0
       Class: 0x000000
       Powered: no
       Discoverable: no
       Pairable: yes
       UUID: PnP Information           (00001200-0000-1000-8000-00805f9b34fb)
       UUID: Generic Access Profile    (00001800-0000-1000-8000-00805f9b34fb)
       UUID: Generic Attribute Profile (00001801-0000-1000-8000-00805f9b34fb)
       UUID: A/V Remote Control        (0000110e-0000-1000-8000-00805f9b34fb)
       UUID: A/V Remote Control Target (0000110c-0000-1000-8000-00805f9b34fb)
       UUID: Audio Source              (0000110a-0000-1000-8000-00805f9b34fb)
       UUID: Audio Sink                (0000110b-0000-1000-8000-00805f9b34fb)
       Modalias: usb:v1D6Bp0246d050B
       Discovering: no
 [bluetooth]# power on
 [CHG] Controller 00:1E:4C:F4:98:5B Class: 0x0c010c
 Changing power on succeeded
 [CHG] Controller 00:1E:4C:F4:98:5B Powered: yes
 [bluetooth]# agent on
 Agent registered
 [bluetooth]# default-agent
 Default agent request successful

```

<power on your headset in pairing mode. Eventually you will see what appears to be a mac address.>

```
 [bluetooth]# scan on
 Discovery started
 [CHG] Controller 00:1E:4C:F4:98:5B Discovering: yes
 [CHG] Device 00:1A:7D:12:36:B9 RSSI: -61
 [bluetooth]# pair 00:1A:7D:12:36:B9
 Attempting to pair with 00:1A:7D:12:36:B9
 [CHG] Device 00:1A:7D:12:36:B9 Connected: yes
 [CHG] Device 00:1A:7D:12:36:B9 UUIDs has unsupported type
 [CHG] Device 00:1A:7D:12:36:B9 Paired: yes
 Pairing successful
 [bluetooth]# connect 00:1A:7D:12:36:B9
 [CHG] Device 00:1A:7D:12:36:B9 Connected: yes
 Connection successful
 [bluetooth]# info 00:1A:7D:12:36:B9
 Device 00:1A:7D:12:36:B9
       Name: SoundBot SB220
       Alias: SoundBot SB220
       Class: 0x240404
       Icon: audio-card
       Paired: yes
       Trusted: no
       Blocked: no
       Connected: yes
       LegacyPairing: yes
       UUID: Headset                   (00001108-0000-1000-8000-00805f9b34fb)
       UUID: Audio Sink                (0000110b-0000-1000-8000-00805f9b34fb)
       UUID: A/V Remote Control Target (0000110c-0000-1000-8000-00805f9b34fb)
       UUID: A/V Remote Control        (0000110e-0000-1000-8000-00805f9b34fb)
       UUID: Handsfree                 (0000111e-0000-1000-8000-00805f9b34fb)

```

Start up alsamixer, for simplicity un-mute all your outputs. Oddly enough some can be muted though. The ones I had muted during playback were:

*   Headphones
*   SPIDF

Start up audacious. Use the menu to select PulseAudio as your output. Somewhere I read that bluez5 requires pulseaudio-git and this jives with my experience.

Start up pavucontrol in a terminal. In the Outputs tab select the bluetooth headset.

[screenshot of application settings](http://netskink.blogspot.com/2013/12/pulseaudio-pavucontrol-and-audacious.html)

#### Miscellaneous configuration files

For reference, these settings were also done.

##### ALSA /etc/asound.conf

The settings shown at the top of this page was used, but the additional modification for Intel laptop sound cards.

```
pcm.btheadset {
  type plug
  slave {
    pcm {
      type bluetooth
      device 00:1A:7D:12:36:B9
      profile "auto"
    }
  }
  hint {
    show on
    description "BT Headset"
  }
}
ctl.btheadset {
  type bluetooth
}
options snd-hda-intel model=laptop

```

##### /etc/dbus-1/system.d/bluetooth.conf

The settings here seem to be enabled for root only. See the policy user="root" section. However, if a regular user is specified here, the system fails to start. Someone with more knowledge could explain why.

 `/etc/dbus-1/system.d/bluetooth.conf` 
```
<!-- This configuration file specifies the required security policies for Bluetooth core daemon to work. -->

<!DOCTYPE busconfig PUBLIC "-//freedesktop//DTD D-BUS Bus Configuration 1.0//EN"
  "http://www.freedesktop.org/standards/dbus/1.0/busconfig.dtd">
<busconfig>

  <!-- ../system.conf have denied everything, so we just punch some holes -->

  <policy user="root">
    <allow own="org.bluez"/>
    <allow send_destination="org.bluez"/>
    <allow send_interface="org.bluez.Agent1"/>
    <allow send_interface="org.bluez.MediaEndpoint1"/>
    <allow send_interface="org.bluez.MediaPlayer1"/>
    <allow send_interface="org.bluez.ThermometerWatcher1"/>
    <allow send_interface="org.bluez.AlertAgent1"/>
    <allow send_interface="org.bluez.Profile1"/>
    <allow send_interface="org.bluez.HeartRateWatcher1"/>
    <allow send_interface="org.bluez.CyclingSpeedWatcher1"/>
  </policy>

  <policy at_console="true">
    <allow send_destination="org.bluez"/>
  </policy>

  <!-- allow users of lp group (printing subsystem) to communicate with bluetoothd -->
  <policy group="lp">
    <allow send_destination="org.bluez"/>
  </policy>

  <policy context="default">
    <deny send_destination="org.bluez"/>
  </policy>

</busconfig>

```

##### Tested applications

As noted above this will work easily with audacious. YouTube videos with Chromium and Flash Player will work on some videos. If the video has ads it will not work, but if the video does not have ads it will work. Just make sure that after audacious is working with Bluetooth headset, start Chromium, and navigate to YouTube. Find a video without leading ads, and it should play the audio. If the settings icon has the a menu with two drop-down combo boxes for Speed and Quality it will play.

## Switch between HSV and A2DP setting

This can easily be achieved by the following command where 2 needs to be changed with the correct device number.

```
pacmd set-card-profile 2 a2dp_sink

```

### A2DP not working with PulseAudio

#### Socket interface problem

If PulseAudio fails when changing the profile to A2DP with bluez 4.1+ and PulseAudio 3.0+, you can try disabling the Socket interface from `/etc/bluetooth/audio.conf` by removing the line `Enable=Socket` and adding line `Disable=Socket`.

#### Gnome with GDM

**Note:** Below was tested with Gnome 3.16.2 and PulseAudio 7.0

If PulseAudio fails when changing the profile to A2DP while using GNOME with GDM, you need to prevent GDM from starting its own instance of PulseAudio. Apply the same fix as shown in [#Connecting works, but I cannot play sound](#Connecting_works.2C_but_I_cannot_play_sound).

**Note:** Discussion about this problem can be found [here](https://bbs.archlinux.org/viewtopic.php?id=194006) and [here](https://bbs.archlinux.org/viewtopic.php?id=196689)

## Tested headsets

| Model | Version | Comments | Compatible |
| **Philips SHB9150** | bluez5, pulseaudio 5 | Pause and resume does not work. With at least mpv and Banshee hitting the pause button stops audio output but does not pause the player. | Limited |
| **Philips SHB9100** | Pause and resume is flaky. See [[2]](https://bbs.archlinux.org/viewtopic.php?pid=1315428#p1315428) for the underlying issue and a temporary solution to improve audio quality. | Limited |
| **Philips SHB7000** | Pause and resume is flaky. | Limited |
| **Philips SHB7100** | bluez 5.32, pulseaudio 6.0 | Next/previous buttons work. Pause and resume is flaky (sometimes works in VLC, not at all in Audacious). Tested only A2DP and Handsfree audio out, built-in mic was broken. | Limited |
| **Philips SHB7150** | bluez 5.32, pulseaudio 6.0 | Next/previous buttons work. Pause and resume work in VLC. Tested only A2DP profile. | Yes |
| **Philips SHB5500BK/00** | bluez 5.28, PulseAudio 6.0 | Pause and resume is not working. | Limited |
| **Parrot Zik** | Firmware 1.04\. The microphone is detected, but does not work. Sometimes it lags (but does not stutter); usually this is not noticeable unless playing games, in which case you may switch to a wired connection. | Limited |
| **Sony DR-BT50** | bluez{4,5} | Works for a2dp, see [[3]](http://vlsd.blogspot.com/2013/11/bluetooth-headphones-and-arch-linux.html)). Adapter: D-Link DBT-120 USB dongle. | Yes |
| **Sony SBH50** | bluez5 | Works for a2dp, Adapter: Broadcom Bluetooth 2.1 Device (Vendor=0a5c ProdID=219b Rev=03.43). Requires the `btusb` [module](/index.php/Modprobe "Modprobe"). | Yes |
| **Sony MDR-XB950BT** | pulseaudio | Tested a2dp. Adapter: Grand-X BT40G. Doesn't auto-connect, need to connect manually. Other functionality works fine. | Limited |
| **Sony MUC-M1BT1** | bluez5, [pulseaudio-git](https://aur.archlinux.org/packages/pulseaudio-git/) | Both A2DP & HSP/HFP work fine. | Yes |
| **SoundBot SB220** | bluez5, [pulseaudio-git](https://aur.archlinux.org/packages/pulseaudio-git/) | Yes |
| **Auna Air 300** | bluez5, pulseaudio-git | For some reason, a few restarts were required, and eventually it just started working. | Limited |
| **Sennheiser MM 400-X** | bluez5, pulseaudio 4.0-6 | Yes |
| **Sennheiser MM 550-X Travel** | bluez 5.27-1, pulseaudio 5.0-1 | Next/Previous buttons work out-of-the-box, Play/Pause does not | Yes |
| **Sennheiser URBANITE XL Wireless** | bluez 5.37-2, pulseaudio 7.1-3 | A2DP High Fidelity Playback. Play/Pause/Next/Previous works out-of-the-box. | Yes |
| **Audionic BlueBeats (B-777)** | bluez5, pulseaudio 4.0-6 | Yes |
| **Logitech Wireless Headset** | bluez 5.14, pulseaudio-git | part number PN 981-000381, advertised for use with iPad | Yes |
| **HMDX Jam Classic Bluetooth** | bluez, pulseaudio-git | Yes |
| **PT-810** | bluez 5.14, pulseaudio-git | Generic USB-Powered Bluetooth Audio Receiver with 3.5mm headset jack and a2dp profile. Widely available as "USB Bluetooth Receiver." IDs as PT-810. | Yes |
| **Philips SHB4000WT** | bluez5 | A2DP works, HDP distorted. | Yes |
| **Philips AEA2000/12** | bluez5 | Yes |
| **Nokia BH-104** | bluez4 | Yes |
| **Creative AirwaveHD** | bluez 5.23 | Bluetooth adapter Atheros Communications usb: 0cf3:0036 | Yes |
| **Creative HITZ WP380** | bluez 5.27, pulseaudio 5.0-1 | A2DP Profile only. Buttons work (Play, Pause, Prev, Next). Volume buttons are hardware-only. Auto-connect works but you should include the bluetooth module in "pulseaudio" to switch to it automatically. Clear HD Music Audio (This device support APTx codec but it isn't supported in linux yet). You may have some latency problems which needs pulseaudio restart. | Yes |
| **deleyCON Bluetooth Headset** | bluez 5.23 | Adapter: CSL - USB nano Bluetooth-Adapter V4.0\. Tested a2dp profile. Untested microphone. Does not auto-connect (even when paired and trusted), must connect manually. Play/pause button mutes/unmutes the headphones, not the playback. Playback fwd/bwd buttons do not work (nothing visible with *xev*). | Limited |
| **UE BOOM** | bluez 5.27, pulseaudio-git 5.99 | Update to latest UE BOOM fw 1.3.58\. Sound latency in video solved by configuring pavucontrol. Works with UE BOOM x2. | Yes |
| **LG HBS-730** | bluez 5.30, pulseaudio 6.0 | Works out of box with A2DP profile. | Yes |
| **LG HBS-750** | bluez 5.30, pulseaudio-git 6.0 | Works out of box with A2DP profile. | Yes |
| **Beats Studio Wireless** | bluez 5.28, pulseaudio 6.0 | Works out of box. Not tested multimedia buttons. | Yes |
| **AKG Y45BT** | bluez 5.30, pulseaudio 6.0 | Pause and resume does not work. Needs `Enable=Socket` in `/etc/bluetooth/audio.conf` and `load-module module-bluetooth-discover` in `/etc/pulse/default.pa`. | Yes |
| **Bluedio Turbine/Turbine 2+** | bluez 5.3, pulseaudio 6.0 | HSP/HFP work fine, A2DP work fine. | Yes |
| **Sony SBH20** | bluez 5.30, pulseaudio 6.0 | Works out of box with A2DP profile. | Yes |
| **Nokia BH-111** | bluez 5.30, pulseaudio 6.0 | Works with both HSP/HFP and A2DP. Buttons work in certain apps. | Yes |
| **Sony MDR-ZX330BT** | bluez 5.31, pulseaudio 6.0 | Works out of box (HSP/HFP and A2DP). Buttons work in certain apps. | Yes |
| **Samsung Level Link** | bluez 5.33, pulseaudio 6.0 | Works out of box (HSP/HFP and A2DP). Buttons work in certain apps. | Yes |
| **Bernafon Soundgate 3** | bluez 5.34-2, pulseaudio 7.0-1 | Works (A2DP) after installing blueman-git 2.0.r53.g2a812a8-1. | Yes |
| **JBL E40 BT** | bluez 5.35, pulseaudio 7.0 | Connection works after installing blueberry and blueman. A2DP works after adding Disable=Socket to `/etc/bluetooth/audio.conf`. Media buttons works. | Yes |
| **Sony SBH80** | bluez 5.36, pulseaudio 7.1 | Media buttons do not work. A2DP works after disabling profiles and enabling A2DP in blueman. | Yes |
| **Kitsound Manhattan** | bluez 5.37, pulseaudio 7.13 | All appears to work fine. If Pulseaudio is run as root ( --system) rather than as a user, it often resuls in either a refusal to connect once paired, or else a complete system freeze ( asking for the access PIN )! You have been warned. | Yes |
| **JBL Everest 300** | bluez 5.37, pulseaudio 8.0 | Everything works correctly. Headphones connected with HSP/HFP profile and sound quality was bad, but after switching profile in **pavucontrol** to A2DP sink sound quality went way up (as expected). Pairing went without issues. | Yes |
| **Logitech UE9000** | bluez 5.37, pulseaudio 7.1, gnome 3.18.2 | Audio playback works correctly after gnome/gdm fix [here](https://wiki.archlinux.org/index.php/Bluetooth_headset#Connecting_works.2C_but_I_cannot_play_sound). Audio profile defaults to HSP/HFP. Microphone works in both HSP/HFP and A2DP profiles. Play/Pause and Fwd/Back functions work correctly in Spotify and VLC | Yes |

## See also

Using the same device on Windows and Linux without pairing the device over and over again

*   [Dual booting with a Bluetooth keyboard](http://ubuntuforums.org/showthread.php?p=9363229#post9363229)