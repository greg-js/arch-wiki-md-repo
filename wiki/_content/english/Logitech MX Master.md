[Logitech MX Master](http://www.logitech.com/en-us/product/mx-master)

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Usage](#Usage)
*   [2 List of events sent by mouse](#List_of_events_sent_by_mouse)
*   [3 Mappings for extra buttons](#Mappings_for_extra_buttons)
*   [4 Power](#Power)
*   [5 Smart shift](#Smart_shift)
*   [6 Laggy mouse movements in Bluetooth mode](#Laggy_mouse_movements_in_Bluetooth_mode)

## Usage

The mouse should work with no special configuration if using the unified receiver USB dongle. Plug in the dongle, then press the `connect` button on the mouse.

To use [Bluetooth](/index.php/Bluetooth "Bluetooth"), change the channel on the bottom of the mouse, and click the `connect` button. Now, search for the mouse with a bluetooth manager of your choice and pair. In future it should connect as soon as you switch to that channel when your bluetooth is active. If you have problems with the mouse not showing when scanning, see [Bluetooth LE device does not show up in scan](/index.php/Bluetooth#Device_does_not_show_up_in_scan "Bluetooth")

## List of events sent by mouse

| Physical action | detected as |
| Left button | button 1 |
| Press to wheel | button 2 |
| Right button | button 3 |
| Scroll wheel up | button 4 |
| Scroll wheel down | button 5 |
| Press "i" button under wheel | undetectable in linux |
| Scroll hor_wheel right (up) | button 6 |
| Scroll hor_wheel left (down) | button 7 |
| Side-bottom button | button 8 |
| Side-top button | button 9 |
| Thumb button | Ctrl+Alt+Tab |

Notes:

*   It is impossible to move mouse cursor while thumb button is pressed, but possible to use any other actions (pressing buttons and scrolling wheels). Ctrl+Alt+Tab event is sent only after releasing thumb button.
*   If you wish, you can get experience of thumb button like in Windows or Mac. In kde go to System settings → Shortcuts → Global Shortcuts → KWin → Show all windows from all desktops. It is set to ctrl+f10 by default. Set ctrl+alt+tab for this action and apply settings.
*   "I" button under wheel is undetectable in linux, but works as switching wheel between free and rattle mode
*   Logitech gestures (moving mouse up/down/left/right while thumb pressed) are not detected in linux.

## Mappings for extra buttons

The vertical wheel and the two buttons near it should work right away, however the thumb button requires some special treatment, and you might want to remap the rest.

To remap the buttons of the mouse you can use the packages [xbindkeys](https://www.archlinux.org/packages/?name=xbindkeys) and [xautomation](https://www.archlinux.org/packages/?name=xautomation).

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

If using PulseAudio (more info [here](/index.php/Xbindkeys#Volume_control "Xbindkeys")):

```
# thumb wheel up => increase volume
"pactl set-sink-volume @DEFAULT_SINK@ +2%"
   b:6

# thumb wheel down => lower volume
"pactl set-sink-volume @DEFAULT_SINK@ -2%"
   b:7

```

If you prefer to get a visual feedback on how the volume level changes you could use the following lines instead (Tested in GNOME and KDE)

```
# thumb wheel up => increase volume
"xte 'key XF86AudioRaiseVolume'"
   b:6

# thumb wheel down => lower volume
"xte 'key XF86AudioLowerVolume'"
   b:7

```

Now start `xbindkeys`, preferably add that to the autostart list of your desktop environment.

The thumb button is special. With the Logitech software available for Windows and Mac, you would be able to map up to 5 actions to it: by pressing the button or by pressing the button and moving the mouse in one of four directions. As of November 2015, there is no way to enable the direction feature using Arch.

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

Battery status can be read as described on [Logitech Unifying Receiver](/index.php/Logitech_Unifying_Receiver "Logitech Unifying Receiver"). e.g. Solaar ([solaar](https://www.archlinux.org/packages/?name=solaar)) has a system tray utility.

## Smart shift

In order to change the sensitivity of changing the mouse wheel mode (between hyperfast and click-to-click), install [solaar](https://www.archlinux.org/packages/?name=solaar). A slider appears that can be set somewhere between 0 and 50 (inclusive). 0 means always in hyperfast mode, 50 means always in click-to-click mode.

To change the sensitivity, change this value somewhere between 0 and 50.

## Laggy mouse movements in Bluetooth mode

Try this solution: [Bluetooth#Bluetooth mouse laggy movements](/index.php/Bluetooth#Bluetooth_mouse_laggy_movements "Bluetooth")