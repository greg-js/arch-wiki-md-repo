# ThinkPad multimedia buttons

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

**This article is a stub.**

**Notes:** Everything is covered in main articles: [Extra keyboard keys](/index.php/Extra_keyboard_keys "Extra keyboard keys"), [xbindkeys](/index.php/Xbindkeys "Xbindkeys") etc. (Discuss in [Talk:ThinkPad multimedia buttons#](https://wiki.archlinux.org/index.php/Talk:ThinkPad_multimedia_buttons))

## Contents

*   [1 Configuring the mute, volume up and volume down buttons in ArchLinux:](#Configuring_the_mute.2C_volume_up_and_volume_down_buttons_in_ArchLinux:)
    *   [1.1 Step 1 Device Drivers](#Step_1_Device_Drivers)
    *   [1.2 Step 2 Applications](#Step_2_Applications)
    *   [1.3 Configuring Buttons to Software](#Configuring_Buttons_to_Software)

## Configuring the mute, volume up and volume down buttons in ArchLinux:

### Step 1 Device Drivers

Install the necessary device drivers and configure the OS_Linux in the kernel command line.

### Step 2 Applications

Install ALSA and make sure that alsamixer is able to mute/unmute and adjust volume.

### Configuring Buttons to Software

Step one and two are well documented. Search the wiki for other instructions on how to do this.

You are ready to proceed to this step if you can play audio with your favorite application and adjust the sound volume using the alsamixer application in [alsa](/index.php/Alsa "Alsa") package.

This [page](/index.php/Lenovo_ThinkPad_T400#Multimedia_Keys "Lenovo ThinkPad T400") will show you how to use [xev](/index.php/Extra_keyboard_keys#In_Xorg "Extra keyboard keys") to determine the keycodes for the mute, volume up and volume down buttons.

That page also shows how to use [xbindkeys](https://www.archlinux.org/packages/?name=xbindkeys) to setup a .xbindkeysrc.scm file. However, the device settings might vary for your setup. Here is how to use amixer to find your device settings. Use the amixer command with the parameter scontrols. This gives the name for the master volume control.

```
 $ amixer scontrols
 Simple mixer control 'Master',0
 Simple mixer control 'Capture',0
 $

```

Open alsamixer and examine the output as you issue commands to set the volume. As you adjust the volume setting using amixer, you should see the volume level in alsamixer change. Here I am adjusting the volume louder with each invocation of amixer

```
 $ amixer -c 0 sset 'Master',0 40 
 Simple mixer control 'Master',0
   Capabilities: pvolume pvolume-joined pswitch pswitch-joined
   Playback channels: Mono
   Limits: Playback 0 - 74
   Mono: Playback 40 [54%] [-34.00dB] [on]
 $ amixer -c 0 sset 'Master',0 60
 Simple mixer control 'Master',0
   Capabilities: pvolume pvolume-joined pswitch pswitch-joined
   Playback channels: Mono
   Limits: Playback 0 - 74
   Mono: Playback 60 [81%] [-14.00dB] [on]
 $ amixer -c 0 sset 'Master',0 80
 Simple mixer control 'Master',0
   Capabilities: pvolume pvolume-joined pswitch pswitch-joined
   Playback channels: Mono
   Limits: Playback 0 - 74
   Mono: Playback 74 [100%] [0.00dB] [on]
 $

```

This command sets the volume to a specified level, however we want the volume buttons to adjust the current volume. Thus, we use the +/-dB form of the command. This is shown in the final .xbindkeysrc.scm. Likewise the mute button is specified.

```
 $ cat .xbindkeysrc.scm 
   (xbindkey '("XF86AudioRaiseVolume") "amixer -c 0 sset 'Master',0 2dB+")
   (xbindkey '("XF86AudioLowerVolume") "amixer -c 0 sset 'Master',0 2dB-")
   (xbindkey '("XF86AudioMute") "amixer set Master toggle")

```

Restart xwindows and now your media buttons should work.

Retrieved from "[https://wiki.archlinux.org/index.php?title=ThinkPad_multimedia_buttons&oldid=331668](https://wiki.archlinux.org/index.php?title=ThinkPad_multimedia_buttons&oldid=331668)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Lenovo](/index.php/Category:Lenovo "Category:Lenovo")