# Lenovo Ideapad y530

## Contents

*   [1 Making stuff work](#Making_stuff_work)
    *   [1.1 Enabling all speakers](#Enabling_all_speakers)
    *   [1.2 Workaround for brightness bug](#Workaround_for_brightness_bug)
    *   [1.3 Switching wifi on/off during work](#Switching_wifi_on.2Foff_during_work)

## Making stuff work

### Enabling all speakers

```
echo "options snd_hda_intel model=lenovo-sky" >> /etc/modprobe.d/modprobe.conf

```

### Workaround for brightness bug

The Lenovo Ideapad Y530 has an unusual implementation of the ACPI system. A patch to the kernel (2.6.29) is being developed. Until its release the following workaround should help control the display brightness beyond the limited ability of the keyboard shortcuts.

To see the list of available options:

```
    cat /proc/acpi/video/VGA/LCDD/brightness

```

Replace XX in the following command with the display intensity you desire.

```
    echo XX > /proc/acpi/video/VGA/LCDD/brightness

```

For full brightness:

```
   echo 65 > /proc/acpi/video/VGA/LCDD/brightness

```

### Switching wifi on/off during work

Any ideas? Currently you have to reboot to make it work.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Lenovo_Ideapad_y530&oldid=351781](https://wiki.archlinux.org/index.php?title=Lenovo_Ideapad_y530&oldid=351781)"