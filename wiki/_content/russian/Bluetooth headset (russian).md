На данный момент Arch Linux поддерживает профиль A2DP (Аудио выход) для беспроводного проигрывания аудио прямо с обычной установкой.

**Совет:** Самые последние версии [Bluez](/index.php/Bluetooth_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Bluetooth (Русский)") не поддерживают профили Headset/Handsfree. Это означает, что не будет работать микрофон, а также на гарнитурах, не поддерживающих профиль A2DP, не будет работать звук. Если вы хотите использовать гарнитуру через профили Headset/Handsfree, вам придётся пользоваться старыми методами, которым требуется установка некоторых пакетов из [AUR](/index.php/AUR_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AUR (Русский)").

**Совет:** В пакете [pulseaudio-git](https://aur.archlinux.org/packages/pulseaudio-git/) появилась нативная поддержка для профилей Headset/Handsfree и Bluez5.

**Совет:** Bluez5 поддерживает только Pulseaudio, но не ALSA. Если вы не хотите использоваь Pulseaudio, вам нужно установить старую версию Bluez из AUR.

## Contents

*   [1 Гарнитура через Bluez5/Pulseaudio (git)](#.D0.93.D0.B0.D1.80.D0.BD.D0.B8.D1.82.D1.83.D1.80.D0.B0_.D1.87.D0.B5.D1.80.D0.B5.D0.B7_Bluez5.2FPulseaudio_.28git.29)
    *   [1.1 Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
        *   [1.1.1 Pairing works, but connecting does not](#Pairing_works.2C_but_connecting_does_not)
        *   [1.1.2 Connecting works, but I cannot play sound](#Connecting_works.2C_but_I_cannot_play_sound)
        *   [1.1.3 UUIDs has unsupported type](#UUIDs_has_unsupported_type)
*   [2 Legacy method: ALSA-BTSCO](#Legacy_method:_ALSA-BTSCO)
    *   [2.1 Connecting the headset](#Connecting_the_headset)
        *   [2.1.1 Pairing the headset with your computer](#Pairing_the_headset_with_your_computer)
            *   [2.1.1.1 Using *bluez-gnome*](#Using_bluez-gnome)
            *   [2.1.1.2 Using *passkey-agent*](#Using_passkey-agent)
    *   [2.2 Headset and Alsa Devices](#Headset_and_Alsa_Devices)
    *   [2.3 Headset's multimedia buttons](#Headset.27s_multimedia_buttons)
*   [3 Legacy method: PulseAudio](#Legacy_method:_PulseAudio)
    *   [3.1 Troubleshooting](#Troubleshooting)
        *   [3.1.1 Audio sink fails](#Audio_sink_fails)
        *   [3.1.2 Page timeout issue](#Page_timeout_issue)
*   [4 Legacy documentation: ALSA, bluez5 and PulseAudio method](#Legacy_documentation:_ALSA.2C_bluez5_and_PulseAudio_method)
    *   [4.1 Install Software Packages](#Install_Software_Packages)
        *   [4.1.1 Install ALSA and associated libraries](#Install_ALSA_and_associated_libraries)
        *   [4.1.2 Install Bluez5](#Install_Bluez5)
        *   [4.1.3 Install PulseAudio](#Install_PulseAudio)
        *   [4.1.4 Install Audacious](#Install_Audacious)
    *   [4.2 Procedure](#Procedure)
        *   [4.2.1 Miscellaneous Configuration Files](#Miscellaneous_Configuration_Files)
            *   [4.2.1.1 ALSA /etc/asound.conf](#ALSA_.2Fetc.2Fasound.conf)
            *   [4.2.1.2 /etc/dbus-1/system.d/bluetooth.conf](#.2Fetc.2Fdbus-1.2Fsystem.d.2Fbluetooth.conf)
            *   [4.2.1.3 Tested applications](#Tested_applications)
*   [5 Switch between HSV and A2DP setting](#Switch_between_HSV_and_A2DP_setting)
    *   [5.1 A2DP not working with PulseAudio](#A2DP_not_working_with_PulseAudio)
*   [6 Tested Headsets](#Tested_Headsets)
*   [7 See also](#See_also)

## Гарнитура через Bluez5/Pulseaudio (git)

По умолчанию Pulseaudio 5.x поддерживает A2DP. Текущая git версия также поддерживает HFP. Убедитесь, что следующие пакеты установлены:

```
# pacman -S pulseaudio-alsa bluez bluez-libs bluez-utils bluez-firmware

```

Запустите систему bluetooth:

```
# systemctl start bluetooth

```

Теперь, чтобы сопрягаться и подключаться можно использовать команду *bluetoothctl*. Для решения проблем и более подробных примеров по *bluetoothctl* смотрите статью [Bluetooth](/index.php/Bluetooth_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Bluetooth (Русский)"). Выполните

```
# bluetoothctl

```

чтобы войти в его внутреннюю командную строку. Затем введите:

```
# power on
# agent on
# default-agent
# scan on

```

Теперь убедитесь, что ваши наушники находятся в режиме спаривания. Они должны обнаружиться. Например,

```
[NEW] Device 00:1D:43:6D:03:26 Lasmex LBT10

```

показывает устройство, которое представилось как "Lasmex LBT10" и имеет MAC адрес *00:1D:43:6D:03:26*. Мы будем использовать этот MAC адрес для инициализации паринга:

```
# pair 00:1D:43:6D:03:26

```

После паринга с устройством, вы должны явно к нему подключиться (каждый раз?):

```
# connect 00:1D:43:6D:03:26

```

Если всё сработало правильно, у вас должно появиться отдельное устройство вывода в [PulseAudio (Русский)](/index.php/PulseAudio_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "PulseAudio (Русский)"). Теперт вы можете перенаправить любое аудио в это устройство с помощью вкладок "Playback" и "Recording" программы [pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol).

Теперь вы можете отключить сканирование и выйти из программы:

```
# scan off
# exit

```

### Решение проблем

Many users report frustation with getting A2DP to work.

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

The problem in this case is that pulseaudio is not catching up. A common solution to this problem is to restart pulseaudio. Note that it is perfectly fine to run *bluetoothctl* as root while pulseaudio runs as user. After restarting pulseaudio, retry to connect. It is not necessary to repeat the pairing.

If restarting pulseaudio doesn't work, you need to load module-bluetooth-discover.

```
# pactl load-module module-bluetooth-discover

```

The same load-module command can be added to `/etc/pulse/default.pa`.

To have your headset auto connect you need to enable PulseAudio's switch-on-connect module. Add the following:

 `/etc/pulse/default.pa` 
```
# automatically switch to newly-connected devices
load-module module-switch-on-connect

```

You then need to tell *bluetoothctl* to trust your bluetooth headset or you will see errors like this:

```
bluetoothd[487]: Authentication attempt without agent
bluetoothd[487]: Access denied: org.bluez.Error.Rejected

```

```
[bluetooth]# trust 00:1D:43:6D:03:26

```

After a reboot, your bluetooth adapter will not power on by default. You need to add a udev rule to power it on:

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

If you see a message similar to this, you can go on and investigate your pulseaudio configuration. Otherwise, go back and ensure the connection is successful.

#### UUIDs has unsupported type

During pairing you might see this output in *bluetoothctl*:

```
[CHG] Device 00:1D:43:6D:03:26 UUIDs has unsupported type

```

This message is a very common one and can be ignored.

## Legacy method: ALSA-BTSCO

It is much easier to set up your bluetooth headset today, with bluez >= 3.16\. You may want to try the out-of-box [python](/index.php/Python_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Python (Русский)") script in [this blog](http://fosswire.com/2008/01/11/a2dp-stereo-linux/) (you need edit the script to work with gconftool-2). There is also a piece of equivalent [bash](/index.php/Bash_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Bash (Русский)") script [here](http://lymanrb.blogspot.com/2008/05/linux.html).

You need your headset's bdaddr. It is of the form *12:34:56:78:9A:BC*. Either find it in the documentation of your headset, on the headset itself or with the `hcitool scan` command.

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") [btsco](https://aur.archlinux.org/packages/btsco/).

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

### Headset and Alsa Devices

1\. First if you have not already, [install](/index.php/Pacman "Pacman") [bluez](https://www.archlinux.org/packages/?name=bluez) from the [official repositories](/index.php/Official_repositories "Official repositories").

2\. Scan for your device

```
$ hcitool (-i <optional hci#>***) scan

```

3\. Pair your headset with your device:

```
$ bluez-simple-agent (optional hci# ***) XX:XX:XX:XX:XX:XX

```

and put in your pin (0000 or 1234, etc)

4\. Make sure your `/etc/bluetooth/audio.conf` allows A2DP Audio Sinks. Place this line just bellow the [Genera] heading:

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

In order to get your bluetooth headset's multimedia buttons (play, pause, next, previous) working you need to create `/etc/modprobe.d/uinput.conf` containing `uinput`.

## Legacy method: PulseAudio

This one is much easier and more elegant. PulseAudio will seamlessly switch between output devices when the headset is turned on. If you have ALSA as the sound server, you need the following packages installed: [pulseaudio](https://www.archlinux.org/packages/?name=pulseaudio) and [pulseaudio-alsa](https://www.archlinux.org/packages/?name=pulseaudio-alsa).

Now, to configure the audio output to use bluetooth, just install [pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol) and run it to configure the audio output:

```
$ pavucontrol

```

See [this blog](http://dev.funkynerd.com/knowledgebase/articles/5) for further explanations. Make sure to take a look at the [PulseAudio](/index.php/PulseAudio "PulseAudio") wiki entry for setting up PulseAudio, especially if you are running KDE.

### Troubleshooting

#### Audio sink fails

Bluetooth headset is connected, but ALSA/PulseAudio fails to pick up the connected device. You will get "Audio sink fails". According to [gentoo wiki](http://wiki.gentoo.org/wiki/Bluetooth_Headset), you have to verify than in `/etc/bluetooth/audio.conf` there is `Enable=Socket` under the `[General]` section heading.

Just do a `# systemctl restart bluetooth` to apply it.

#### Page timeout issue

If you receive this error whilst trying to pair your headset with your system using bluez-simple-agent, then you can try to restart your system and use the graphical bluez applet of your desktop environment.

## Legacy documentation: ALSA, bluez5 and PulseAudio method

[ALSA](/index.php/ALSA "ALSA"), [bluez5](/index.php/Bluetooth_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Bluetooth (Русский)"), and [PulseAudio](/index.php/PulseAudio "PulseAudio") work together to allow a wireless [Bluetooth](/index.php/Bluetooth_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Bluetooth (Русский)") headset to play audio. The following method works with a Lenovo T61p laptop and SoundBot SB220 wireless bluetooth headset. The required software stack is extensive and failure to include all components can produce errors which are difficult to understand. The following list of software packages might not be the minimum required set and needs to be examined more closely.

Bluez5 has a regression causing HSP/HFP Telephone profile to not be available. This regression is documented in the [draft release notes for Pulseaudio 5.0](http://www.freedesktop.org/wiki/Software/PulseAudio/Notes/5.0/) which say (in "Notes for packagers"): "PulseAudio now supports BlueZ 5, but only the A2DP profile. BlueZ 4 is still the only way to make HSP/HFP work." ([from here](https://fedoraproject.org/wiki/Common_F20_bugs#bluez5-profile))

### Install Software Packages

The core software components are [ALSA](/index.php/ALSA "ALSA"), Bluez5, [Pulseaudio](/index.php/Pulseaudio "Pulseaudio"). However there are additional libraries which are required. As well as a player which can play audio files. The following section lists the software packages installed in order to connect the headset and play audio over the headset.

#### Install ALSA and associated libraries

[ALSA](/index.php/ALSA "ALSA") works with the linux kernel to provide audio services to user mode software. The following packages are used with the [Bluetooth](/index.php/Bluetooth_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Bluetooth (Русский)") headset: [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils), [alsa-plugins](https://www.archlinux.org/packages/?name=alsa-plugins), [alsa-tools](https://www.archlinux.org/packages/?name=alsa-tools).

#### Install Bluez5

Bluez5 is the latest [Bluetooth](/index.php/Bluetooth_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Bluetooth (Русский)") stack. It is required for [PulseAudio](/index.php/PulseAudio "PulseAudio") to interface with wireless headsets. Required packages: [bluez](https://www.archlinux.org/packages/?name=bluez), [bluez-utils](https://www.archlinux.org/packages/?name=bluez-utils), [bluez-libs](https://www.archlinux.org/packages/?name=bluez-libs).

#### Install PulseAudio

[PulseAudio](/index.php/PulseAudio "PulseAudio") interfaces with [ALSA](/index.php/ALSA "ALSA"), Bluez and other user mode programs. The [pulseaudio-git](https://aur.archlinux.org/packages/pulseaudio-git/) package from [AUR](/index.php/AUR "AUR") has capabilities not provided by the stock [pulseaudio](https://www.archlinux.org/packages/?name=pulseaudio) package. The additional capabilities are required by Bluez5\. More info regarding the differences between Bluez5 and PulseAudio are [here.](https://bbs.archlinux.org/viewtopic.php?pid=1302270#p1302270)

Required packages: [pulseaudio-git](https://aur.archlinux.org/packages/pulseaudio-git/), [pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol).

#### Install Audacious

[Audacious](/index.php/Audacious "Audacious") is a program which plays audio files. It can work directly with [ALSA](/index.php/ALSA "ALSA") or with [PulseAudio](/index.php/PulseAudio "PulseAudio"). Required packages: [audacious](https://www.archlinux.org/packages/?name=audacious), [audacious-plugins](https://www.archlinux.org/packages/?name=audacious-plugins).

### Procedure

Once the required packages are installed, use this procedure to play audio with a bluetooth headset. The high level overview of the procedure is to pair the headset, connect the headset, configure the player and pulse audio controller and then play audio.

Start the bluetooth service as root or use sudo

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

Start the pulseaudio daemon. This must be done after X windows is started and as a normal user.

```
$ pulseaudio -D

```

Verify the pulseaudio daemon is running.

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

Start up audacious. Use the menu to select pulseaudio as your output. Somewhere I read that bluez5 requires pulseaudio-git and this jives with my experience.

Start up pavucontrol in a terminal. In the Outputs tab select the bluetooth headset.

[screenshot of application settings](http://netskink.blogspot.com/2013/12/pulseaudio-pavucontrol-and-audacious.html)

#### Miscellaneous Configuration Files

For reference these settings were also done.

##### ALSA /etc/asound.conf

The settings shown at the top of this page was used, but the additional modification for intel laptop soundcards.

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
pacmd set-card-profile 2 a2dp

```

### A2DP not working with PulseAudio

If PulseAudio fails when changing the profile to A2DP with bluez 4.1+ and PulseAudio 3.0+, you can try disabling the Socket interface from `/etc/bluetooth/audio.conf` by removing the line `Enable=Socket` and adding line `Disable=Socket`.

## Tested Headsets

The following Bluetooth headsets have been tested with Arch Linux

*   Philips SHB9100 - Confirmed NOT TO WORK well. Have tried *everything* after a while they cut out. Pause and resume too is flakky and basically the whole wireless bluetooth experience is horrible. The following forum post[[1]](https://bbs.archlinux.org/viewtopic.php?pid=1315428#p1315428) explains an underlying issue and describes a temporary solution which can be used to improve the audio quality pending a proper fix.
*   Parrot Zik - Confirmed to work out of the box with firmware 1.04! The MIC however is detected, but does not work at all. Sometimes it can lag behind (not stutter) but most of the times it is not noticeable unless you playing a game, in which case I would switch to wired which resolves the issue.
*   Sony DR-BT50 works for a2dp both with bluez4 and bluez5 (instructions here[[2]](http://vlsd.blogspot.com/2013/11/bluetooth-headphones-and-arch-linux.html), subject to change). Adapter: D-Link DBT-120 USB dongle.
*   Sony SBH50 works for a2dp with bluez5 and pulseaudio. Adapter: Broadcom Bluetooth 2.1 Device (Vendor=0a5c ProdID=219b Rev=03.43; not sure what the exact model). Does not work until `sudo modprobe btusb`.
*   SoundBot SB220 works with bluez5 and pulseaudio-git.
*   Auna Air 300 works well with bluez5, pulseaudio-git, and e.g. also mocp when running the latter through padsp. For some reason, a few restarts and re-tries were required, and eventually it just started working.
*   Sennheiser MM 400-X works out of the box with bluez5 and pulseaudio 4.0-6
*   Audionic BlueBeats (B-777) works out of the box with bluez5 and pulseaudio 4.0-6
*   Logitech Wireless Headset (part number PN 981-000381, advertised for use with iPad) works with bluez 5.14 and pulseaudio-git.
*   HMDX Jam Classic Bluetooth works with bluez, pulseaudio-git and pavucontrol
*   PT-810 - Generic USB-Powered Bluetooth Audio Receiver with 3.5mm headset jack and a2dp profile. Widely available as "USB Bluetooth Receiver." IDs as PT-810\. Works with bluez 5.14 and pulseaudio-git.
*   Philips SHB4000WT works out of the box with bluez5 and pulseaudio 5.0
*   Philips AEA2000/12 works also out of the box with bluez 5.18-1 (and previous) and pulseaudio 5.0
*   Nokia BH-104 - does not work with bluez5\. It use to work fine with bluez4, but since Gnome requires bluez5 I can't downgrade.
*   Creative AirwaveHD - works with bluez 5.23 and pulseaudio 5.0 with Bluetooth adapter Atheros Communications usb: 0cf3:0036

## See also

Alternative method of connecting a BT headset to Linux:

*   [GaBlog - Connect a bluetooth headset to linux](http://gablog.eu/online/node/80)

Using the same device on Windows and Linux without pairing the device over and over again

*   [Dual booting with a bluetooth keyboard](http://ubuntuforums.org/showthread.php?p=9363229#post9363229)