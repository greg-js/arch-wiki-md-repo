## Contents

*   [1 Důležitá poznámka](#D.C5.AFle.C5.BEit.C3.A1_pozn.C3.A1mka)
*   [2 Instalace Skype](#Instalace_Skype)
*   [3 Tak dotoho](#Tak_dotoho)
    *   [3.1 A. OSS nebo Kernel OSS emulace ALSy](#A._OSS_nebo_Kernel_OSS_emulace_ALSy)
    *   [3.2 B. ALSA a dMix](#B._ALSA_a_dMix)
    *   [3.3 C. Použití OSS emulace s oss2jack](#C._Pou.C5.BEit.C3.AD_OSS_emulace_s_oss2jack)

### Důležitá poznámka

Nová beta verze Skypu má nativní podporu Alsy. Pokud máte tuto verzi, není nuté provádět tyto kroky!

### Instalace Skype

Balíček Skype se nachází v repozitáří community. Pokud tento repozitář nemáte aktivovaný, změňte následující řádky v souboru /etc/pacman.conf:

```
#[community]
# Add your preferred servers here, they will be used first
#Include = /etc/pacman.d/community

```

na

```
[community]
# Add your preferred servers here, they will be used first
Include = /etc/pacman.d/community

```

Nyní nainstaluje Skype přes pacman:

```
# pacman -S skype

```

### Tak dotoho

(Nejpreferovanější je možnost B) S možností B můžete používat Skype **a** zároveň nechat přehrávat ostatní programy zvuk. S možností C můžete dělat o samé, ale možnost B se jedodušeji nastavuje

##### A. OSS nebo Kernel OSS emulace ALSy

Spusťte "skype" a ujistěte se, že žádné ostatní programy nepoužívají vaší zvukovou kartu. Pokud chcete používat Skype **a** zároveň přehrávat zvuk v jiných programech, mrkněte do bodu B.

##### B. ALSA a dMix

Nejprve potřebujeme naisntalovat balíček alsa-oss:

```
# pacman -S alsa-oss

```

A přidat následující skript do "~/.asoundrc". Pokud soubor neexistuje, vytvořte jej.

Díky Lorenzu Colittimu za sepsaní tohoto skriptíku!

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

Teď pusťte skype stejným způsobem, jako to budete dělat příště:

```
ALSA_OSS_PCM_DEVICE="skype" aoss skype

```

Případně si na spouštění skypu můžete udělat skript:

Jako root vytvořte tento soubor **/usr/bin/askype**

```
# Little script to run Skype correctly using the modified .asoundrc
# See: [https://wiki.archlinux.org/index.php/Skype](https://wiki.archlinux.org/index.php/Skype) for more information!
#
# Questions/Remarks: profox@debianbox.be

ALSA_OSS_PCM_DEVICE="skype" aoss skype

```

Nyní se ujistěte, že ho může používat každý

```
# chmod a+x /usr/bin/askype

```

Můžete také upravit menu ve svém okenním manažeru, aby se skype spouštěl přes ten skript:

Upravte soubor **/usr/share/applications/skype.desktop**

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

Občas to trvá chvílku déle, než Skype naskočí, ale když už jednou naběhne, tak to fugnuje.

##### C. Použití OSS emulace s oss2jack

oss2jack je jiný způsob jak dosáhnout OSS emulace bez přímého použití ALSy. Místo toho, oss2jack vytvoří OSS zařízení, které přesměrovává vše do JACK (JACK Audio Connecion Kit), který zapíná mixování a poté to posílá na na standartní zařízení ALSA. Pro více informací o nastavení tohoto, mrkněte na [Umožnění více programům přehrávat zvuk v tom samém čase](/index.php?title=Umo%C5%BEn%C4%9Bn%C3%AD_v%C3%ADce_program%C5%AFm_p%C5%99ehr%C3%A1vat_zvuk_v_tom_sam%C3%A9m_%C4%8Dase&action=edit&redlink=1 "Umožnění více programům přehrávat zvuk v tom samém čase (page does not exist)")