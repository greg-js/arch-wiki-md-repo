## Contents

*   [1 Installation](#Installation)
*   [2 Quirks](#Quirks)
    *   [2.1 Black screen at boot](#Black_screen_at_boot)
    *   [2.2 Some key not working](#Some_key_not_working)
    *   [2.3 No sound](#No_sound)

## Installation

Follow the [installation guide](/index.php/Installation_guide "Installation guide"), also see [Dell 10v](/index.php/Dell_Mini_10v "Dell Mini 10v"), [Dell 1010](/index.php/Dell_Inspiron_Mini_1010 "Dell Inspiron Mini 1010"), [Dell 3531](/index.php/Dell_Inspiron_3531 "Dell Inspiron 3531") or similar.

## Quirks

### Black screen at boot

Try [blacklisting](/index.php/Blacklisting "Blacklisting") in /etc/modprobe.d/ during the [chroot](/index.php/Installation_guide#Configure_the_system "Installation guide") stage of the installation

```
blacklist dell-laptop

```

### Some key not working

Set the keyboard layout to "Dell Laptops Precision M"

### No sound

Try

```
amixer -D pulse set Mute Playback

```