[Logitech MX Master](http://www.logitech.com/en-us/product/mx-master)

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Usage](#Usage)
*   [2 Mappings for extra buttons](#Mappings_for_extra_buttons)
    *   [2.1 Logiops](#Logiops)
    *   [2.2 Xbindkeys](#Xbindkeys)
*   [3 Power](#Power)
*   [4 Smart shift](#Smart_shift)
    *   [4.1 Logiops](#Logiops_2)
    *   [4.2 Solaar](#Solaar)
*   [5 Laggy mouse movements in Bluetooth mode](#Laggy_mouse_movements_in_Bluetooth_mode)

## Usage

The mouse should work with no special configuration if using the unified receiver USB dongle. Plug in the dongle, then press the `connect` button on the mouse.

To use [Bluetooth](/index.php/Bluetooth "Bluetooth"), change the channel on the bottom of the mouse, and click the `connect` button. Now, search for the mouse with a bluetooth manager of your choice and pair. In future it should connect as soon as you switch to that channel when your bluetooth is active. If you have problems with the mouse not showing when scanning, see [Bluetooth LE device does not show up in scan](/index.php/Bluetooth#Device_does_not_show_up_in_scan "Bluetooth")

The mouse exists in 3 versions:

*   Mx Master.
*   Mx Master 2s.
*   Mx Master 3.

The functionalities are the same.

## Mappings for extra buttons

Installing [#Logiops](#Logiops) [logiops-git](https://aur.archlinux.org/packages/logiops-git/) it is possible to acquire everything this mouse has to offer:

*   Easy programmable buttons.
*   DPI selection.
*   Smartshift (hyperfast and click-to-clic wheel mode).
*   HiresScroll.
*   Gestures.

It is possible to use just [#Xbindkeys](#Xbindkeys) and tweak the desktop shortcuts to obtain some customization, but with some caveats (look notes below).

### Logiops

It can be executed as application via command line by running

```
# logid

```

Or as a service by systemd.

```
# systemctl start logid

```

The configuration lives in /etc/logid.cfg. But the package comes with no configuration. One needs to create this specifying the name of the device to be used. To obtain that name launching from cli

```
# logid -v

```

The name of the detected device is printed.

Then you can create the configuration file. As example look at [https://github.com/PixlOne/logiops/blob/master/logid.example.cfg](https://github.com/PixlOne/logiops/blob/master/logid.example.cfg) or this one:

 `/etc/logid.cfg` 
```
devices: (
{
    name: "MX Master 3";
    smartshift:
    {
        on: true;
        threshold: 30;
    };
    hiresscroll:
    {
        hires: false;
        invert: false;
        target: false;
    };
    dpi: 1000;

    buttons: (
        {
            cid: 0xc3;
            action =
            {
                type: "Gestures";
                gestures: (
                    {
                        direction: "Up";
                        mode: "OnRelease";
                        action =
                        {
                            type: "Keypress";
                            keys: ["KEY_LEFTCTRL", "KEY_F10"];
                        };
                    },
                    {
                        direction: "Down";
                        mode: "OnRelease";
                        action =
                        {
                            type: "Keypress";
                            keys: ["KEY_LEFTCTRL", "KEY_F7"];
                        };
                    },
#                    {
#                        direction: "Left";
#                        mode: "OnRelease";
#                        action =
#                        {
#                            type: "CycleDPI";
#                            dpis: [50, 500, 1000, 1500, 2000, 3000, 4000];
#                        };
#                    },
                    {
                        direction: "Left";
                        mode: "OnRelease";
                        action =
                        {
                            type: "Keypress";
                            keys: ["KEY_LEFTMETA", "KEY_LEFT"];
                        };
                    },

#                    {
#                        direction: "Right";
#                        mode: "OnRelease";
#                        action =
#                        {
#                            type = "ToggleHiresScroll";
#                        }
#                    },
                    {
                        direction: "Right";
                        mode: "OnRelease";
                        action =
                        {
                            type: "Keypress";
                            keys: ["KEY_LEFTMETA", "KEY_RIGHT"];
                        }
                    },

                    {
                        direction: "None"
                        mode: "NoPress"
                    }
                );
            };
        },
        {
            cid: 0xc4;
            action =
            {
                type = "ToggleSmartshift";
            };
        },
        {
            # Next tab instead of fwd in history, Comment to default behavior
            cid: 0x53;
            action =
            {
                type :  "Keypress";
                keys: ["KEY_LEFTCTRL", "KEY_PAGEUP"];
            };
        },
        {
            # Previous tab instead of back in history, Comment to default behavior
            cid: 0x56;
            action =
            {
                type :  "Keypress";
                keys: ["KEY_LEFTCTRL", "KEY_PAGEDOWN"];
            };
        }
    );
},
{
# Another device to configure
name: "Other Logitech USB Receiver";

}
);
```

It's documented in [https://github.com/PixlOne/logiops/wiki/Configuration](https://github.com/PixlOne/logiops/wiki/Configuration) .

### Xbindkeys

List of events sent by mouse

| Physical action | detected as |
| Left button | button 1 |
| Press to wheel | button 2 |
| Right button | button 3 |
| Scroll wheel up | button 4 |
| Scroll wheel down | button 5 |
| Press "i" button under wheel | Not detected by xbindkeys |
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

### Logiops

The button below the wheel can be used to toggle it, set the control id 0xc4 in buttons definitions in /etc/logid.cfg as this:

 `/etc/logid.cfg` 
```
...
        {
            cid: 0xc4;
            action =
            {
                type = "ToggleSmartshift";
            };
        },
...
```

### Solaar

In order to change the sensitivity of changing the mouse wheel mode (between hyperfast and click-to-click), install [solaar](https://www.archlinux.org/packages/?name=solaar). A slider appears that can be set somewhere between 0 and 50 (inclusive). 0 means always in hyperfast mode, 50 means always in click-to-click mode.

To change the sensitivity, change this value somewhere between 0 and 50.

## Laggy mouse movements in Bluetooth mode

Try this solution: [Bluetooth#Bluetooth mouse laggy movements](/index.php/Bluetooth#Bluetooth_mouse_laggy_movements "Bluetooth")