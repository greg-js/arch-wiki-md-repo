Touchpad is problematic. By default, if you hold the thumb over the button area, the pointer will not move. Once the system is installed, the problem disappears when using KDE, while GNOME still exhibits the issue. In GNOME, use the following to fix the problem:

```
xinput set-prop "SynPS/2 Synaptics TouchPad" 331 1 0

```

Even after doing this, the mouse pointer still jumps around when clicking the button sometimes.