## Input devices

### Keyboard

To use multimedia keys you need to set keyboard model in /etc/X11/xorg.conf

```
   Option "XkbModel" "hpdv9500"

```

Add this section into /usr/share/X11/xkb/symbols/inet

```
   // Hewlett-Packard Pavilion dv9500
   partial alphanumeric_keys
   xkb_symbols "hpdv9500" {
    key <I10> { [ XF86AudioPrev		] };
    key <I19> { [ XF86AudioNext		] };
    key <I20> { [ XF86AudioMute		] };
    key <I22> { [ XF86AudioPlay, XF86AudioPause ] };
    key <I24> { [ XF86AudioStop		] };
    key <I2E> { [ XF86AudioLowerVolume		] };
    key <I30> { [ XF86AudioRaiseVolume		] };
    key <I32> { [ XF86WWW			] };
    key <PAUS> { [ Pause			] };
   };

```

And finally add

```
   hpdv9500

```

to section "! $inetkbds = ..." in /usr/share/X11/xkb/rules/xorg. Now you can restart X server and set keyboard shortcuts in your music player

### Touchpad

See [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics").