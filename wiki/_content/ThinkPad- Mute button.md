# ThinkPad: Mute button

## Contents

*   [1 Problem:](#Problem:)
    *   [1.1 Nothing works](#Nothing_works)
    *   [1.2 External Audio still on](#External_Audio_still_on)
*   [2 Solution:](#Solution:)
    *   [2.1 Older IBM ThinkPads](#Older_IBM_ThinkPads)
    *   [2.2 Nothing works:](#Nothing_works:)
    *   [2.3 External Audio still on:](#External_Audio_still_on:)
    *   [2.4 External Audio still on (and you use XFCE):](#External_Audio_still_on_.28and_you_use_XFCE.29:)

## Problem:

The mute button does not work properly on most ThinkPads and IdeaPads with a newer kernel. Two different scenarios occur:

### Nothing works

NaN

### External Audio still on

NaN

## Solution:

### Older IBM ThinkPads

NaN

### Nothing works:

NaN

```
options thinkpad_acpi enabled=0 # enables Mute-Button on ThinkPads with IdeaPad-Firmware 

```

NaN

### External Audio still on:

NaN

```
#tpb-Settings: 

CALLBACK "/root/tp-key-handler" 

OSD off 

```

NaN

```
#!/bin/bash
echo $1 $2
if [ $1 = mute ]; then
	if [ $2 = on ]; then
		mset="off";
	else
		mset="on";
	fi
	sudo -u USERNAME amixer sset Master $mset; # I had to sudo to me, because I use PulseAudio
fi

```

NaN

```
chmod +x /root/tp-key-handler 

```

NaN

That's it - if you have a better Idea, please do not hesitate to edit this page!

### External Audio still on (and you use XFCE):

Go to Applications->Settings->Keyboard->Application Shortcuts tab. Hit Add and for the command, use 'amixer sset Master toggle'. For the key, hit the mute button. Protip, to make sure the led state is correct, start with the led in the opposite state of your mutedness so that when you map the button, it starts out in the correct state. Alternatively, you could just reboot and make sure the led is off before you get into your XFCE session.

Retrieved from "[https://wiki.archlinux.org/index.php?title=ThinkPad:_Mute_button&oldid=392722](https://wiki.archlinux.org/index.php?title=ThinkPad:_Mute_button&oldid=392722)"