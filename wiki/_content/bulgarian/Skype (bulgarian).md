## Contents

*   [1 Инсталация](#.D0.98.D0.BD.D1.81.D1.82.D0.B0.D0.BB.D0.B0.D1.86.D0.B8.D1.8F)
    *   [1.1 64-битова иснталация](#64-.D0.B1.D0.B8.D1.82.D0.BE.D0.B2.D0.B0_.D0.B8.D1.81.D0.BD.D1.82.D0.B0.D0.BB.D0.B0.D1.86.D0.B8.D1.8F)
*   [2 Звук в Skype](#.D0.97.D0.B2.D1.83.D0.BA_.D0.B2_Skype)
    *   [2.1 Звук в Skype с ALSA (2.0+)](#.D0.97.D0.B2.D1.83.D0.BA_.D0.B2_Skype_.D1.81_ALSA_.282.0.2B.29)
    *   [2.2 Звук с Skype-OSS (версии по-стари от 2.0)](#.D0.97.D0.B2.D1.83.D0.BA_.D1.81_Skype-OSS_.28.D0.B2.D0.B5.D1.80.D1.81.D0.B8.D0.B8_.D0.BF.D0.BE-.D1.81.D1.82.D0.B0.D1.80.D0.B8_.D0.BE.D1.82_2.0.29)
        *   [2.2.1 А) С емулация на OSS или Kernel OSS за ALSA](#.D0.90.29_.D0.A1_.D0.B5.D0.BC.D1.83.D0.BB.D0.B0.D1.86.D0.B8.D1.8F_.D0.BD.D0.B0_OSS_.D0.B8.D0.BB.D0.B8_Kernel_OSS_.D0.B7.D0.B0_ALSA)
        *   [2.2.2 Б) Настройване на ALSA и dMix за Skype](#.D0.91.29_.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.B2.D0.B0.D0.BD.D0.B5_.D0.BD.D0.B0_ALSA_.D0.B8_dMix_.D0.B7.D0.B0_Skype)
        *   [2.2.3 В) Емулация на OSS с oss2jack](#.D0.92.29_.D0.95.D0.BC.D1.83.D0.BB.D0.B0.D1.86.D0.B8.D1.8F_.D0.BD.D0.B0_OSS_.D1.81_oss2jack)

### Инсталация

За да инсталрите Skype, трябва да включите community repository в /etc/pacman.conf.

Сменете секцията:

```
#[community]
# Add your preferred servers here, they will be used first
#Include = /etc/pacman.d/mirrorlist

```

на:

```
[community]
# Add your preferred servers here, they will be used first
Include = /etc/pacman.d/mirrorlist

```

Вече можете да инсталирате Skype със следната команда:

```
# pacman -S skype

```

#### 64-битова иснталация

Понеже Skype има само 32-нитов binary, няма официален пакет за x86_64 за Arch. Можете да иснталирате bin32-skype от AUR като алтернатива.

### Звук в Skype

Новите версии на Skype (2.0+) имат native поддръжка за [ALSA](/index.php/ALSA "ALSA") , по-старите версии подържат deprecated [OSS](/index.php/OSS "OSS").

#### Звук в Skype с ALSA (2.0+)

Звукът би трябвало да работи без допълнителни настройки. Ако не, можете да изеберете звуково устройство в настройките на Skype. Ако Skype блокира вашето звуково устройство, добавете следното в ~/.asoundrc

```
pcm.dmixout {
  # Just pass this on to the system dmix
  type plug
  slave {
     pcm "dmix"
  }
}

```

След това стартирайте Skype, отидете в звуковите настройки и изберете dmixout като speaker- и ringingdevice.

#### Звук с Skype-OSS (версии по-стари от 2.0)

Този метод не работи с по-новите версии на Skype. Вариант Б) се препоръчва пред другите. С вариант Б) можете да ползвате звука в Skype и други програми. С вариант В) можете също, но е по-трудно да се нагласи.

##### А) С емулация на OSS или Kernel OSS за ALSA

Пуснете Skype и затворете всички останали програми използващи звук. Ако искате да имате звук в други програми освен Skype, вижте вариант Б).

##### Б) Настройване на ALSA и dMix за Skype

Първо, инсталирайте alsa-oss:

```
# pacman -S alsa-oss

```

Добавете следното в "~/.asoundrc": (Ако файлът не съществува, създадете го.

Настройките са благодарение на Lorenzo Colitti.

```
# .asoundrc to use skype at the same time as other audio apps like xmms
#
# Successfully tested on an IBM x40 with i810_audio using Linux 2.6.15 and
# Debian unstable with skype 1.2.0.18-API. No sound daemons (asound, esd, etc.)
# running. However, YMMV.
#
# For background, see:
#
# [https://bugtrack.alsa-project.org/alsa-bug/view.php?id=1228](https://bugtrack.alsa-project.org/alsa-bug/view.php?id=1228)
# [https://bugtrack.alsa-project.org/alsa-bug/view.php?id=1224](https://bugtrack.alsa-project.org/alsa-bug/view.php?id=1224)
#
# (C) 2006-06-03 Lorenzo Colitti - [http://www.colitti.com/lorenzo/](http://www.colitti.com/lorenzo/)
# Licensed under the GPLv2 or later

pcm.skype {
   type asym
   playback.pcm "skypeout"
   capture.pcm "skypein"
}

pcm.skypein {
   # Convert from 8-bit unsigned mono (default format set by aoss when
   # /dev/dsp is opened) to 16-bit signed stereo (expected by dsnoop)
   #
   # We can't just use a "plug" plugin because although the open will
   # succeed, the buffer sizes will be wrong and we'll hear no sound at
   # all.
   type route
   slave {
      pcm "skypedsnoop"
      format S16_LE
   }
   ttable {
      0 {0 0.5}
      1 {0 0.5}
   }
}

pcm.skypeout {
   # Just pass this on to the system dmix
   type plug
   slave {
      pcm "dmix"
   }
}

pcm.skypedsnoop {
   type dsnoop
   ipc_key 1133
   slave {
      # "Magic" buffer values to get skype audio to work
      # If these are not set, opening /dev/dsp succeeds but no sound
      # will be heard. According to the alsa developers this is due
      # to skype abusing the OSS API.
      pcm "hw:0,0"
      period_size 256
      periods 16
      buffer_size 16384
   }
   bindings {
      0 0
   }
}

```

Ако получите грешка:

```
The dmix plugin supports only playback stream

```

добавете следното в .asoundrc :

```
pcm.asymed {
        type asym
        playback.pcm "dmix"
        capture.pcm "dsnoop"
}

pcm.!default {
        type plug
        slave.pcm "asymed"
}

```

От сега нататък, пускайте Skype по следния начин:

```
ALSA_OSS_PCM_DEVICE="skype" aoss skype

```

Можете и да напишете скрипт за стартиране на Skype:

Под root, създайте файла: **/usr/bin/askype**

```
# Little script to run Skype correctly using the modified .asoundrc
# See: [https://wiki.archlinux.org/index.php/Skype](https://wiki.archlinux.org/index.php/Skype) for more information!
#
# Questions/Remarks: profox@debianbox.be

ALSA_OSS_PCM_DEVICE="skype" aoss skype

```

Добавете всички потребители към него:

```
# chmod a+x /usr/bin/askype

```

Можете и да стартирате Skype през графичния интерфейс:

Редактирайте файла: **/usr/share/applications/skype.desktop**

```
[Desktop Entry]
Name=Skype
Comment=P2P software for high-quality voice communication
Exec=askype
Icon=skype.png
Terminal=0
Type=Application
Encoding=UTF-8
Categories=Network;Application;

```

Понякога Skype може да стартира бавно, имайте търпение. :)

##### В) Емулация на OSS с oss2jack

oss2jack е друг вид OSS емулация без да се ползва ALSA директно. Вместо това, oss2jack създава OSS устройство, което пренасочва всичко към JACK (JACK Audio Connection Kit), което пък смесва, и връща output към стандартното устройство на ALSA. За повече информация, посетете [Allow_multiple_programs_to_play_sound_at_once#ALSA_with_oss2jack](/index.php/Allow_multiple_programs_to_play_sound_at_once#ALSA_with_oss2jack "Allow multiple programs to play sound at once").