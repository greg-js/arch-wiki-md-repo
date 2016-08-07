## Contents

*   [1 Инсталация](#.D0.98.D0.BD.D1.81.D1.82.D0.B0.D0.BB.D0.B0.D1.86.D0.B8.D1.8F)
    *   [1.1 64-битова иснталация](#64-.D0.B1.D0.B8.D1.82.D0.BE.D0.B2.D0.B0_.D0.B8.D1.81.D0.BD.D1.82.D0.B0.D0.BB.D0.B0.D1.86.D0.B8.D1.8F)
*   [2 Звук в Skype](#.D0.97.D0.B2.D1.83.D0.BA_.D0.B2_Skype)
    *   [2.1 Звук в Skype с ALSA (2.0+)](#.D0.97.D0.B2.D1.83.D0.BA_.D0.B2_Skype_.D1.81_ALSA_.282.0.2B.29)

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