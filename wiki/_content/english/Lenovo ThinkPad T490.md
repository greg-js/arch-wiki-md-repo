<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 FN Keys](#FN_Keys)
*   [2 Touchpad](#Touchpad)
*   [3 CPU throttling issue](#CPU_throttling_issue)
*   [4 ACPI](#ACPI)

## FN Keys

Most FN keys should work out of the box, but if it doesn't, bind mentioned keys to below commands:

*   **F1** button: `amixer set Master toggle`.
*   **F2** button: `amixer set Master 5%-`.
*   **F3** button: `amixer set Master 5%+`.
*   **F4** button: `amixer set Capture toggle`.

## Touchpad

Touchpad is problematic. By default, if you hold the thumb over the button area, the pointer will not move. Once the system is installed, the problem disappears when using KDE, while GNOME still exhibits the issue. In GNOME, use the following to fix the problem:

```
xinput set-prop 'SynPS/2 Synaptics TouchPad' 'libinput Click Method Enabled' 1 0

```

Even after doing this, the mouse pointer still jumps around when clicking the button sometimes.

## CPU throttling issue

With newer BIOS versions (it happens on at least 1.52, but it could happen older versions too), the CPU tends to throttle down to 400 MHz earlier than it should. In particular, it can be seen when using [Bumblebee](/index.php/Bumblebee "Bumblebee").

This can be worked around by installing [throttled](https://www.archlinux.org/packages/?name=throttled), as explained in [Lenovo ThinkPad T480s](/index.php/Lenovo_ThinkPad_T480s "Lenovo ThinkPad T480s").

## ACPI

The default `/etc/acpi/handler.sh` script has a check for the device that looks like this:

```
ac_adapter)
        case "$2" in
            AC|ACAD|ADP0)

```

This will not work, since the T490 device is called `ACPI0003` which is not matched by the above check. The instructions in [Acpid](/index.php/Acpid "Acpid") does mention a pattern that does work and it is recommended to use this instead.