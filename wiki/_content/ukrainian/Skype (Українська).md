## Contents

*   [1 Skype](#Skype)
    *   [1.1 Встановлення Skype](#.D0.92.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.BD.D1.8F_Skype)
        *   [1.1.1 Інсталяція на 64-бітних системах](#.D0.86.D0.BD.D1.81.D1.82.D0.B0.D0.BB.D1.8F.D1.86.D1.96.D1.8F_.D0.BD.D0.B0_64-.D0.B1.D1.96.D1.82.D0.BD.D0.B8.D1.85_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D0.B0.D1.85)
    *   [1.2 Звук в Skype](#.D0.97.D0.B2.D1.83.D0.BA_.D0.B2_Skype)
        *   [1.2.1 Skype ALSA Sound (2.0+)](#Skype_ALSA_Sound_.282.0.2B.29)
        *   [1.2.2 Skype-OSS Sound (Pre-2.0)](#Skype-OSS_Sound_.28Pre-2.0.29)
            *   [1.2.2.1 А. С OSS или эмуляция OSS в ядре для ALSA](#.D0.90._.D0.A1_OSS_.D0.B8.D0.BB.D0.B8_.D1.8D.D0.BC.D1.83.D0.BB.D1.8F.D1.86.D0.B8.D1.8F_OSS_.D0.B2_.D1.8F.D0.B4.D1.80.D0.B5_.D0.B4.D0.BB.D1.8F_ALSA)
            *   [1.2.2.2 B. Забезпечення роботи ALSA + DMIX в Skype](#B._.D0.97.D0.B0.D0.B1.D0.B5.D0.B7.D0.BF.D0.B5.D1.87.D0.B5.D0.BD.D0.BD.D1.8F_.D1.80.D0.BE.D0.B1.D0.BE.D1.82.D0.B8_ALSA_.2B_DMIX_.D0.B2_Skype)
            *   [1.2.2.3 C. Використання OSS эмуляції oss2jack](#C._.D0.92.D0.B8.D0.BA.D0.BE.D1.80.D0.B8.D1.81.D1.82.D0.B0.D0.BD.D0.BD.D1.8F_OSS_.D1.8D.D0.BC.D1.83.D0.BB.D1.8F.D1.86.D1.96.D1.97_oss2jack)

## Skype

Skype - безкоштовне програмне забезпечення з закритим кодом, що забезпечує шифрований голосовий зв'язок через Інтернет між комп'ютерами (VoIP), а також платні послуги для зв'язку з абонентами звичайної телефонної мережі. Можлива організація конференц-зв'язку (до 25 абонентів, включаючи ініціатора), передача текстових повідомлень і файлів, а також відеозв'язок.

### Встановлення Skype

Для інсталювання Skype ви повинні в файлі /etc/pacman.conf додати репозиторій [community]:

```
[community]
# Add your preferred servers here, they will be used first
Include = /etc/pacman.d/mirrorlist

```

Тепер можна інсталювати Skype:

```
# pacman -S skype

```

#### Інсталяція на 64-бітних системах

Skype пропонується тільки в якості пакета для 32-бітних систем, і тому не існує пакетів в офіціальних репозиторіях для x86_64\. Попри це, Ви можете інсталювати 32-bit Skype з AUR, або Ви можете інсталювати його вручну, виконавши наступні команды: Спочатку, створюємо робочую директорію:

```
$ cd ~ && mkdir temp-skype-install

```

Видаляемо всі попередні версії Skype:

```
$ sudo rm -rf /usr/share/skype/ && sudo rm -rf /usr/bin/skype

```

Потім, скачуємо Skype:

```
$ wget [http://www.skype.com/go/getskype-linux-beta-static](http://www.skype.com/go/getskype-linux-beta-static) 
$ tar xvf skype_static-2.1.0.81.tar.bz2 && cd skype_static-2.1.0.81 

```

**Note:** Користувачі **Kopete**, хто хоче використовувати Skype API повинні отримати динамічно зв’язані пакети.

Інсталюємо Skype:

```
$ sudo mkdir /usr/share/skype/ 
$ sudo mv avatars/ /usr/share/skype/ 
$ sudo mv icons/ /usr/share/skype/ 
$ sudo mv lang/ /usr/share/skype/ 
$ sudo mv sounds/ /usr/share/skype/ 
$ sudo mv skype /usr/bin/ 

```

Та видаляемо робочу директорію:

```
$ cd ~ && rm -rf temp-skype-install

```

**Note:** Ви можете використати сценарій, котрий робить усе вище описане автоматично: $ wget [http://tinyurl.com/arch-skype-install](http://tinyurl.com/arch-skype-install) -O-

**Note:** Також Вам необхідні 32-bit бібліотеки, які можна отримати: # pacman -S lib32

### Звук в Skype

Останні версії Skype (2,0 +) мають вбудовану підтримку ALSA, більш ранні версії підтримують тільки застарілі OSS.

#### Skype ALSA Sound (2.0+)

В ідеалі, звук повинен працювати "з коробки", якщо ви не можете вибрати звуковий пристрій для використання в Skype або якщо Ви маєте проблеми зі Skype: він блокує звуковий пристрій, то Вам потрібно тільки додадти наступні строки в Ваш ~/.asoundrc :і

```
  pcm.dmixout {
  # Just pass this on to the system dmix
  type plug
  slave {
     pcm "dmix"
    }
  }

```

Після цього Вы можете запустити Skype, піти в опції аудіо та оберіть dmixout в якості оратора і ringing device.

#### Skype-OSS Sound (Pre-2.0)

Если у вас есть последняя версия Skype, то OSS не будет работать, что и не нужно; посмотрите на "важные заметки" в начале этой страницы. Вариант B предпочтительнее, чем другие варианты. При варианте B можно использовать Skype и другие программы воспроизведения звука тоже. При варианте C вы можете сделать это, но вариант B проще в настройке.

##### А. С OSS или эмуляция OSS в ядре для ALSA

Запустіть "Skype" та переконайтеся, що інші програми не використовують Вашу звукову карту. Якщо Ви хочете викристовувати Skype та інші програми, що використовують звук, подивіться на варіант B.

##### B. Забезпечення роботи ALSA + DMIX в Skype

Для початку, Ви повинні должны заінсталювати пакет alsa-oss з репозиторія:

```
# pacman -S alsa-oss

```

Додайте наступні строки в "~ /.asoundrc" (файл ".asoundrc" у Вашому домашньому каталозі). Якщо файл не існує, просто створіть його!:

**Note:** Велика подяка за це Lorenzo Colitti!

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

Якщо післе цього Ви побачите повідомлення про помилку:

```
The dmix plugin supports only playback stream

```

Тоді додайте наступне в Ваш .asoundrc:

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

Тепер запускайте Skype, таким чином, кожен раз, коли Ви хочете його використоувати:

```
# ALSA_OSS_PCM_DEVICE="skype" aoss skype

```

При желании вы можете создать сценарий, для запуска Skype:

В режимі суперкорстувача, створіть файл: /usr/bin/askype:

```
# Little script to run Skype correctly using the modified .asoundrc
# See: [https://wiki.archlinux.org/index.php/Skype](https://wiki.archlinux.org/index.php/Skype) for more information!
#
# Questions/Remarks: profox@debianbox.be 
ALSA_OSS_PCM_DEVICE="skype" aoss skype

```

Тепер запевніться, що кожен користувач має права на виконання файла:

```
# chmod a+x /usr/bin/askype

```

Вы також можете виправити пункт меню, щоб Ви могли запускати Skype з меню WM: Відредагуйте файл: /usr/share/applications/skype.desktop

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

Інколи для запуска Skype потрібен час, але як тільки він запуститься все повинно працювати!

##### C. Використання OSS эмуляції oss2jack

Oss2jack це ще один спосіб для OSS эмуляції без використання ALSA напряму. Замість цього, oss2jack сстворює пристрій OSS, що JACK (Jack Audio Connection Kit) потім виводить на стандартний пристрій ALSA. Для отримання додаткової інформації з налаштування, будь ласка, зверніться до [Allow_multiple_programs_to_play_sound_at_once#ALSA_with_oss2jack](/index.php/Allow_multiple_programs_to_play_sound_at_once#ALSA_with_oss2jack "Allow multiple programs to play sound at once").