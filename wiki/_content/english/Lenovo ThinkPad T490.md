## FN Keys

Most FN keys should work out of the box, but if it doesn't, bind mentioned keys to below commands:

*   **F1** button: `amixer set Master toggle`.
*   **F2** button: `amixer set Master 5%-`.
*   **F3** button: `amixer set Master 5%+`.
*   **F4** button: `amixer set Capture toggle`.

## Touchpad

Touchpad is problematic. By default, if you hold the thumb over the button area, the pointer will not move. Once the system is installed, the problem disappears when using KDE, while GNOME still exhibits the issue. In GNOME, use the following to fix the problem:

```
xinput set-prop "SynPS/2 Synaptics TouchPad" 331 1 0

```

Even after doing this, the mouse pointer still jumps around when clicking the button sometimes.