[Logitech MX Master](http://www.logitech.com/en-us/product/mx-master)

## Contents

*   [1 Usage](#Usage)
*   [2 Mappings for extra buttons](#Mappings_for_extra_buttons)
*   [3 Power](#Power)
*   [4 Smart shift](#Smart_shift)

## Usage

Mainly, the mouse should work right away with the supplied USB dongle. To get a [Bluetooth](/index.php/Bluetooth "Bluetooth") connection working, change the channel on the bottom of the mouse, and click the `connect` button. Now, search for the mouse with a bluetooth manager of your choice and engage a connection. In future it should connect as soon as you switch to that channel when your bluetooth is active.

## Mappings for extra buttons

The vertical wheel and the two buttons near it should work right away, however the thumb button requires some special threatment, and you might want to remap the rest.

To remap the buttons of the mouse you can use the packages [xbindkeys](/index.php/Xbindkeys "Xbindkeys") and [xautomation](https://www.archlinux.org/packages/?name=xautomation).

*xbindkeys* will redirect the buttons and *xte* (which is included in xautomation) will execute the custom key presses. To do so, create a config file named `.xbindkeysrc` in your home directory.

Here is a sample configuration for the vertical scroll wheel and the two buttons near it:

```
# thumb wheel up => increase volume and unmute      
"amixer -D pulse set Master 4000+ unmute"
   b:6                                   

# thumb wheel down => lower volume       
"amixer -D pulse set Master 4000-"       
   b:7                                   

# backward button => previous song       
"xte 'key XF86AudioPrev'"                
   b:8                                   

# forward button => next song            
"xte 'key XF86AudioNext'"                
   b:9

```

If using PulseAudio (more info [here](/index.php/Xbindkeys#Xbindkeysrc "Xbindkeys")):

```
# thumb wheel up => increase volume
"pactl set-sink-volume @DEFAULT_SINK@ +2%"
   b:6

# thumb wheel down => lower volume
"pactl set-sink-volume @DEFAULT_SINK@ -2%"
   b:7

```

Now start `xbindkeys`, preferably add that to the autostart list of your desktop environment.

The thumb button is special, with the Logitech software available for Windows and Mac, you would be able to map up to 5 actions to it: by pressing the button or by pressing the button and moving the mouse in one of four directions. As of November 2015, there is no way to enable the direction feature using Arch.

If you look at the keys the button triggers you will notice that it sends a series of keys, confusing xbindkeys. You need to add a short sleep here so xbindkeys will only react on the first keys send so we can at least map one action to it:

```
# thumb button => play/pause music         
# Credit to gregmuellegger [https://bbs.archlinux.org/viewtopic.php?pid=1551271#p1551271](https://bbs.archlinux.org/viewtopic.php?pid=1551271#p1551271)                               
# We need a sleep here since the button triggers a few more key codes. 
# It also triggers Control+Mod2+Control_L and Alt+Mod2+Alt_L. The sleep       
# prevents that X receives those keypresses simultaniously. Therefore they    
# might interfere and trigger unwanted actions. By the sleep we make sure that
# the Alt+Left is receive as distinct event.                                  
"sleep 0.1 && xte 'key XF86AudioPlay'"                                        
   m:0xc + c:23

```

Remember that all changes to `~/.xbindkeysrc` require a restart of the xbindkeys process:

```
$ pkill xbindkeys && xbindkeys

```

## Power

Battery status can be read as described on [Logitech Unifying Receiver](/index.php/Logitech_Unifying_Receiver "Logitech Unifying Receiver"). e.g. Solaar ([solaar](https://aur.archlinux.org/packages/solaar/)) has s system tray utility.

## Smart shift

In order to change the sensitivity of changing the mouse wheel mode (between hyperfast and click-to-click), install [solaar-git](https://aur.archlinux.org/packages/solaar-git/). A slider appears that can be set somewhere between 0 and 50 (inclusive). 0 means always in hyperfast mode, 50 means always in click-to-click mode.

To change the sensitivity, change this value somewhere between 0 and 50.