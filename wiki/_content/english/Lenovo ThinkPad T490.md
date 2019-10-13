<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 FN Keys](#FN_Keys)
*   [2 Touchpad](#Touchpad)
*   [3 Known Issues](#Known_Issues)
    *   [3.1 CPU throttling issue](#CPU_throttling_issue)
    *   [3.2 Speaker noise issue](#Speaker_noise_issue)
    *   [3.3 MicroSD card reader issue](#MicroSD_card_reader_issue)
*   [4 ACPI](#ACPI)
*   [5 Also See](#Also_See)

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

## Known Issues

### CPU throttling issue

With the BIOS Version 1.52 (this problem is known to occur on 1.52, it might still happen on other versions too), the CPU tends to throttle down to 400 MHz earlier than it should. In particular, this can be seen when using [Bumblebee](/index.php/Bumblebee "Bumblebee").

After installing BIOS Version 1.54, this problem is fixed.

### Speaker noise issue

The speaker on the Lenovo Thinkpad T490 may have a high static hissing noise, which doesn't change if you lower the volume, but stops if you mute the speaker or use the headphone jack. This problem can't be fixed completely as of now. Updating to the most current BIOS version will make the speaker silent while it's not playing anything without you having to mute it all the time. But as soon as the user is playing sound, the noise will be back, clearly audible in the background.

Check the [Lenovo Support Website](https://support.lenovo.com/) for the newest BIOS Version.

### MicroSD card reader issue

The microSD card reader does not work. Upon inserting a card, the Linux kernel version 5.3.4 continuously produces the following output and the card does not mount.

```
   mmc0: 1.8V regulator output did not became stable
   mmc0: Skipping voltage switch
   mmc0: Problem switching card into high-speed mode!

```

## ACPI

The default `/etc/acpi/handler.sh` script has a check for the device that looks like this:

```
ac_adapter)
        case "$2" in
            AC|ACAD|ADP0)

```

This will not work, since the T490 device is called `ACPI0003` which is not matched by the above check. The instructions in [Acpid](/index.php/Acpid "Acpid") does mention a pattern that does work and it is recommended to use this instead.

## Also See

*   [Lenovo Forums: A throttling fix is being investigated by Lenovo](https://forums.lenovo.com/t5/Other-Linux-Discussions/X1C6-T480s-low-cTDP-and-trip-temperature-in-Linux/m-p/4535310/highlight/true#M13653).