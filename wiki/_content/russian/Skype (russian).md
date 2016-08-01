## Contents

*   [1 Skype](#Skype)
    *   [1.1 Установка Skype](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_Skype)
    *   [1.2 Звук в Skype](#.D0.97.D0.B2.D1.83.D0.BA_.D0.B2_Skype)
        *   [1.2.1 Skype ALSA Sound (2.0+)](#Skype_ALSA_Sound_.282.0.2B.29)
        *   [1.2.2 Skype-OSS Sound (Pre-2.0)](#Skype-OSS_Sound_.28Pre-2.0.29)
            *   [1.2.2.1 А. С OSS или эмуляция OSS в ядре для ALSA](#.D0.90._.D0.A1_OSS_.D0.B8.D0.BB.D0.B8_.D1.8D.D0.BC.D1.83.D0.BB.D1.8F.D1.86.D0.B8.D1.8F_OSS_.D0.B2_.D1.8F.D0.B4.D1.80.D0.B5_.D0.B4.D0.BB.D1.8F_ALSA)
            *   [1.2.2.2 B. Обеспечение работы ALSA + DMIX в Skype](#B._.D0.9E.D0.B1.D0.B5.D1.81.D0.BF.D0.B5.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D1.8B_ALSA_.2B_DMIX_.D0.B2_Skype)
            *   [1.2.2.3 Использование OSS-эмуляции oss2jack](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_OSS-.D1.8D.D0.BC.D1.83.D0.BB.D1.8F.D1.86.D0.B8.D0.B8_oss2jack)
*   [2 Безопасность Skype](#.D0.91.D0.B5.D0.B7.D0.BE.D0.BF.D0.B0.D1.81.D0.BD.D0.BE.D1.81.D1.82.D1.8C_Skype)
    *   [2.1 AppArmor](#AppArmor)
    *   [2.2 Docker](#Docker)
    *   [2.3 TOMOYO](#TOMOYO)
        *   [2.3.1 Доступ к полученным файлам](#.D0.94.D0.BE.D1.81.D1.82.D1.83.D0.BF_.D0.BA_.D0.BF.D0.BE.D0.BB.D1.83.D1.87.D0.B5.D0.BD.D0.BD.D1.8B.D0.BC_.D1.84.D0.B0.D0.B9.D0.BB.D0.B0.D0.BC)
    *   [2.4 Sandfox](#Sandfox)
*   [3 Плагин Skype для Pidgin](#.D0.9F.D0.BB.D0.B0.D0.B3.D0.B8.D0.BD_Skype_.D0.B4.D0.BB.D1.8F_Pidgin)

## Skype

Skype — бесплатное программное обеспечение с закрытым кодом, обеспечивающее шифрованную голосовую связь через Интернет между компьютерами (VoIP), а также платные услуги для связи с абонентами обычной телефонной сети. Возможна организация конференц-связи (до 25 абонентов, включая инициатора), передача текстовых сообщений и файлов, а также видеосвязь.

### Установка Skype

[Установите](/index.php/Pacman "Pacman") [skype](https://aur.archlinux.org/packages/skype/) из [официального репозитория](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)") или добавьте репозиторий [multilib](/index.php/Multilib "Multilib") для 64-битной системы:

```
[multilib]
# Add your preferred servers here, they will be used first
Include = /etc/pacman.d/mirrorlist

```

Теперь можно установить Skype:

```
# pacman -S skype

```

Запустить Skype легко. Наберите `skype` в терминале или сделайте двойной клик на иконке Skype на рабочем столе, или в меню вашего РО.

Так же попробуйте [Tox](/index.php/Tox_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Tox (Русский)"), установив [tox-git](https://aur.archlinux.org/packages/tox-git/) из [AUR](/index.php/AUR "AUR"): это отличная, свободная, открытая и лёгкая в освоении альтернатива гегемонии skype, находящяася сейчас в стадии активной разработки.

### Звук в Skype

Начиная с версии 4.3, Skype требует [PulseAudio](/index.php/PulseAudio "PulseAudio") для голосовой связи, вероломно отказавшись от поддержки [ALSA](/index.php/ALSA "ALSA").

[apulse](https://aur.archlinux.org/packages/apulse/) (и [lib32-apulse](https://aur.archlinux.org/packages/lib32-apulse/) для пользователей x86_64) из [AUR](/index.php/AUR "AUR") эмулирует *PulseAudio*, не требуя установки PulseAudio. Запустите Skype с:

```
$ apulse skype

```

или для x86_64:

```
$ apulse32 skype

```

Смотрите [ALSA/Troubleshooting#Setting the default microphone/capture device](/index.php/ALSA/Troubleshooting#Setting_the_default_microphone.2Fcapture_device "ALSA/Troubleshooting") и последующие разделы, если микрофон не работает.

Если всё работает, измените [desktop entry](/index.php/Desktop_entries "Desktop entries") в `/usr/share/applications/skype.desktop` что бы строка с Exec читалась как:

```
Exec=/usr/bin/apulse32 /usr/bin/skype  %U

```

#### Skype ALSA Sound (2.0+)

В идеале, звук должен работать "из коробки", если вы не можете выбрать звуковое устройство для использования в Skype или если у вас есть проблемы с Skype: он блокирует звуковое устройство, то вам нужно только добавить следующие строки в ваш ~/.asoundrc :

```
  pcm.dmixout {
  # Just pass this on to the system dmix
  type plug
  slave {
     pcm "dmix"
    }
  }

```

После этого вы можете запустить Skype, пойти в опции аудио и выберите dmixout в качестве оратора и ringing device.

#### Skype-OSS Sound (Pre-2.0)

Если у вас есть последняя версия Skype, то OSS не будет работать, что и не нужно; посмотрите на "важные заметки" в начале этой страницы. Вариант B предпочтительнее, чем другие варианты. При варианте B можно использовать Skype и другие программы воспроизведения звука тоже. При варианте C вы можете сделать это, но вариант B проще в настройке.

##### А. С OSS или эмуляция OSS в ядре для ALSA

Запустите "Skype" и убедитесь, что другие программы не используют вашу звуковую карту. Если вы хотите использовать Skype и другие программы, использующие звук, посмотрите на вариант B.

##### B. Обеспечение работы ALSA + DMIX в Skype

Для начала, вы должны установить пакет alsa-oss из репозитория:

```
# pacman -S alsa-oss

```

Добавьте следующие строки в "~ /.asoundrc" (файл ".asoundrc" в вашем домашнем каталоге) Если файл не существует, просто создайте его!:

**Примечание:** Большое спасибо за это Lorenzo Colitti!

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
  # We cannot just use a "plug" plugin because although the open will
  # succeed, the buffer sizes will be wrong and we will hear no sound at
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

Если после этого вы увидите сообщение об ошибке:

```
The dmix plugin supports only playback stream

```

Тогда добавьте следующее в ваш .asoundrc:

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

Теперь запускайте Skype, таким образом, каждый раз, когда вы хотите его использовать:

```
# ALSA_OSS_PCM_DEVICE="skype" aoss skype

```

При желании вы можете создать сценарий, для запуска Skype:

В режиме суперпользователя, создайте файл: /usr/bin/askype:

```
# Little script to run Skype correctly using the modified .asoundrc
# See: [Skype](/index.php/Skype "Skype") for more information!
#
# Questions/Remarks: profox@debianbox.be 
ALSA_OSS_PCM_DEVICE="skype" aoss skype

```

Теперь убедитесь, что каждый пользователь имеет права на исполнение файла:

```
# chmod a+x /usr/bin/askype

```

Вы также можете исправить пункт меню, чтобы вы могли запускать Skype из меню WM: Отредактируйте файл: /usr/share/applications/skype.desktop

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

Иногда для запуска Skype требуется время, но, как только он запустится, все должно работать!

##### Использование OSS-эмуляции oss2jack

Oss2jack - это еще один способ эмуляции OSS без прямого использования ALSA. Вместо этого *oss2jack* создает устройство OSS, чтобы JACK (Jack Audio Connection Kit) выводил звук на стандартное устройство ALSA. Для получения дополнительной информации по настройке, пожалуйста, обратитесь к статье [Advanced Linux Sound Architecture (Русский)](/index.php/Advanced_Linux_Sound_Architecture_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Advanced Linux Sound Architecture (Русский)").

## Безопасность Skype

Есть несколько причин, по которым следует ограничить доступ Skype к вашему компьютеру:

*   Бинарники skype не поддаются декомпиляции, так что ни кто не смог узнать, что они действительно делают.
*   Некоторое количество шифрованного трафика идёт даже если вы не используете Skype для переписки или голосовой связи в данный момент.
*   ...

Больше информации на [[1]](http://www1.cs.columbia.edu/~salman/skype/index.html).

### AppArmor

Обратитесь к странице [AppArmor](/index.php/AppArmor "AppArmor") для инструкций по установке AppArmor.

В пользовательских инструментах для AppArmor можно найти шаблоны профилей. В том числе и Skype. Скопируйте следующую строку в папку с профилями AppArmor:

```
# cp -ip /usr/share/apparmor/extra-profiles/usr.bin.skype /etc/apparmor.d/

```

По неясным причинам, профиль не завершён - вы можете отредактировать его позднее. Вот пример для Skype 4:

```
#include <tunables/global>

/usr/bin/skype {
  #include <abstractions/audio>
  #include <abstractions/consoles>
  #include <abstractions/dbus-session>
  #include <abstractions/gnome>
  #include <abstractions/kde>
  #include <abstractions/nameservice>
  #include <abstractions/video>

  # Executables
  /usr/bin/skype ixmr,
  /usr/lib{,32}/skype/skype ixmr,
  /usr/bin/xdg-open PUxmr,
  /usr/bin/kde4-config PUxmr,

  # Файлы настройки
  owner @{HOME}/.Skype/ rw,
  owner @{HOME}/.Skype/** krw,
  owner @{HOME}/.config/Skype/ rw,
  owner @{HOME}/.config/Skype/** krw,

  # Папка загрузок
  owner @{HOME}/Public/ rw,
  owner @{HOME}/Public/** krw,

  # Библиотеки
  /usr/lib{,32}/libv4l/v4l2convert.so mr,
  /usr/share/skype/lib/libQtWebKit.so.4 mr,

  # Общие данные
  /usr/share/skype/ r,
  /usr/share/skype/** r,

  # Устройства
  /dev/ r,
  /dev/video[0-9]* mrw,

  # Системная информация
  /etc/machine-id r,
  @{PROC}/sys/kernel/{ostype,osrelease} r,
  @{PROC}/sys/vm/overcommit_memory r,
  @{PROC}/[0-9]*/net/arp r,
  owner @{PROC}/[0-9]*/cmdline r,
  owner @{PROC}/[0-9]*/status r,
  owner @{PROC}/[0-9]*/task/ r,
  owner @{PROC}/[0-9]*/task/[0-9]*/stat r,
  owner @{PROC}/[0-9]*/fd/ r,
  /sys/devices/system/cpu/ r,
  /sys/devices/system/cpu/cpu[0-9]*/cpufreq/scaling_{cur_freq,max_freq} r,
  /sys/devices/pci*/*/usb[0-9]*/*/*/modalias r,
  /sys/devices/pci*/*/usb[0-9]*/*/*/video4linux/video[0-9]*/dev r,
  /sys/devices/pci*/*/usb[0-9]*/*/{idVendor,idProduct,speed} r,

  # Это, вероятно, должно пойти на соответствующие абстракции
  /etc/asound.conf r,
  owner @{HOME}/.config/fontconfig/fonts.conf r,
  owner @{HOME}/.config/gtk-3.0/bookmarks r,
  owner @{HOME}/.config/oxygen-gtk/argb-apps.conf rw,
  owner @{HOME}/.config/pulse/cookie krw,
  owner @{HOME}/.icons/** r,
  owner @{HOME}/.kde4/share/config/kdeglobals krw,
  owner @{HOME}/.kde4/share/config/gtkrc-2.0 r,
  owner @{HOME}/.kde4/share/config/oxygenrc r,
  /usr/share/icons/*/index.theme kr,
  /usr/share/nvidia/nvidia-application-profiles-*-rc r,

  # Запреты
  deny owner @{HOME}/.mozilla/ r,
  deny owner @{HOME}/.mozilla/** r,
  deny /sys/devices/virtual/dmi/** r,
}
```

**Примечание:** Данный пример подразумевает что Skype настроен сохранять полученные файлы в `~/Public`. Вы можете свободно менять её под ваши параметры.

Для использования профиля, удостоверьтесь что `securityfs` примонтирован,

```
# mount -t securityfs securityfs /sys/kernel/security

```

Загрузите профиль командой:

```
# apparmor_parser -r /etc/apparmor.d/usr.bin.skype

```

Теперь вы можете запускать Skype ограниченно для своего пользователя. Запреты пишутся в `messages.log`.

### Docker

Есть возможность использовать Skype в безопасном контйнере [Docker](/index.php/Docker "Docker"). Программа заработает по тунелю SSH с сопроваждением X11 и звуком через PulseAudio's Network Server.

Скачайте подготовленный образ docker с [официальной страницы](https://index.docker.io/u/tomparys/skype/), или посмотрите инструкцию, как сделать всё самому [тут](https://github.com/tomparys/docker-skype-pulseaudio).

### TOMOYO

Заметьте, что данный раздел описывает использование TOMOYO 2.5\. Смотрите установку [TOMOYO Linux#TOMOYO Linux 2.x](/index.php/TOMOYO_Linux#TOMOYO_Linux_2.x "TOMOYO Linux").

**Примечание:** Не забудьте заполнить сначала папку `/etc/tomoyo` запустив: `/usr/lib/tomoyo/init_policy`

*   Откройте файл `/etc/tomoyo/exception_policy.conf` и добавьте строки:

```
path_group SKYPE_DIRS /home/\*/.Skype/
path_group SKYPE_DIRS /home/\*/.Skype/\{\*\}/
path_group SKYPE_DIRS /home/\*/.config/Skype/\{\*\}/
path_group SKYPE_DIRS /usr/share/skype/\{\*\}/
path_group SKYPE_DIRS /tmp/skype-\*/
path_group SKYPE_DIRS /tmp/skype-\*/\{\*\}/
path_group SKYPE_DIRS /home/\*/Downloads/tmp/\{\*\}/
path_group SKYPE_FILES /home/\*/.Skype/\{\*\}/\*
path_group SKYPE_FILES /home/\*/.config/Skype/\{\*\}/\*
path_group SKYPE_FILES /usr/share/skype/\{\*\}/\*
path_group SKYPE_FILES /home/\*/.Skype/\*
path_group SKYPE_FILES /home/\*/.config/Skype/\*
path_group SKYPE_FILES /usr/share/skype/\*
path_group SKYPE_FILES /tmp/skype-\*/\{\*\}/\*
path_group SKYPE_FILES /home/\*/Downloads/tmp/\{\*\}/\*
path_group SKYPE_FILES /home/\*/Downloads/tmp/\*
path_group ICONS_DIRS /usr/share/icons/\{\*\}/
path_group ICONS_FILES /usr/share/icons/\{\*\}/\*
path_group ICONS_FILES /usr/share/icons/\*
initialize_domain /usr/bin/skype from any
initialize_domain /usr/lib32/skype/skype from any
```

Заметьте, что папки `/home/*/Downloads/tmp` единственные папки куда Skype позволенно **сохранять** полученные файлы и из которых позволенно **посылать** оные.

*   Затем откройте `/etc/tomoyo/domain_policy.conf` и добавьте строки:

```
<kernel> /usr/bin/skype
use_profile 3
use_group 0

misc env \*
file read /bin/bash
file read /usr/bin/bash
file read/write /dev/tty
file read /usr/lib/locale/locale-archive
file read /usr/lib/gconv/gconv-modules
file read /usr/bin/skype
file read /usr/lib32/skype/skype
file execute /usr/lib32/skype/skype exec.realpath="/usr/lib32/skype/skype" exec.argv[0]="/usr/lib32/skype/skype"

<kernel> /usr/lib32/skype/skype
use_profile 3
use_group 0

file append /dev/snd/pcm\*
file chmod /home/\*/.Skype/ 0700
file create /home/\*/.cache/fontconfig/\* 0600-0666
file create /tmp/qtsingleapp-\*-lockfile 0600-0666
file create @SKYPE_FILES 0600-0666
file create /dev/shm/pulse-shm-\* 0700-0777
file execute /usr/bin/firefox
file execute /usr/bin/gnome-open
file execute /usr/bin/notify-send
file execute /usr/bin/opera
file execute /usr/bin/xdg-open
file ioctl /dev/snd/\* 0-0xFFFFFFFFFFFFFFFF
file ioctl /dev/video0 0-0xFFFFFFFFFFFFFFFF
file ioctl anon_inode:inotify 0x541B
file ioctl socket:[family=1:type=2:protocol=0] 0x8910
file ioctl socket:[family=1:type=2:protocol=0] 0x8933
file ioctl socket:[family=2:type=1:protocol=6] 0x541B
file ioctl socket:[family=2:type=2:protocol=17] 0x541B
file ioctl socket:[family=2:type=2:protocol=17] 0x8912
file ioctl socket:[family=2:type=2:protocol=17] 0x8927
file ioctl socket:[family=2:type=2:protocol=17] 0x8B01
file ioctl socket:[family=2:type=2:protocol=17] 0x8B1B
file ioctl socket:[family=2:type=2:protocol=17] 0x8B15
file ioctl socket:[family=2:type=2:protocol=17] 0x8B05
file link/rename /home/\*/.cache/fontconfig/\* /home/\*/.cache/fontconfig/\*
file mkdir /home/\*/.cache/fontconfig/\* 0600
file mkdir @SKYPE_DIRS 0700-0777
file mksock /tmp/qtsingleapp-\* 0755
file read /dev/urandom
file read/write/unlink/truncate /dev/shm/pulse-shm-\*
file read /etc/fonts/conf.avail/\*.conf
file read /etc/fonts/conf.d/\*.conf
file read /etc/fonts/fonts.conf
file read /etc/group
file read /etc/host.conf
file read /etc/hosts
file read /etc/machine-id
file read /etc/nsswitch.conf
file read /etc/resolv.conf
file read /home/\*/.ICEauthority
file read /home/\*/.XCompose
file read /home/\*/.Xauthority
file read /home/\*/.Xdefaults
file read /home/\*/.fontconfig/\*
file read /home/\*/.config/fontconfig/\*
file read /home/\*/.config/pulse/cookie
file read /usr/lib/locale/locale-archive
file read /usr/lib32/gconv/UTF-16.so
file read /usr/lib32/gconv/gconv-modules
file read /usr/lib32/libv4l/v4l2convert.so
file read /usr/lib32/libv4l/plugins/libv4l-mplane.so
file read /usr/lib32/pulseaudio/libpulsecommon-5.0.so
file read /usr/lib32/qt/plugins/bearer/libq\*bearer.so
file read /usr/lib32/qt/plugins/iconengines/libqsvgicon.so
file read /usr/lib32/qt/plugins/imageformats/libq\*.so
file read /usr/lib32/qt/plugins/inputmethods/libqimsw-multi.so
file read /usr/lib32/skype/skype
file read /usr/share/X11/locale/\*/Compose
file read /usr/share/X11/locale/\*/XLC_LOCALE
file read /usr/share/X11/locale/compose.dir
file read /usr/share/X11/locale/locale.alias
file read /usr/share/X11/locale/locale.dir
file read /usr/share/alsa/alsa.conf
file read /usr/share/alsa/cards/\*.conf
file read /usr/share/alsa/pcm/\*.conf
file read /usr/share/fonts/\*/\*/\*
file read /usr/share/locale/\*/LC_MESSAGES/\*.mo
file read /usr/share/ca-certificates/mozilla/\*.crt
file read /var/cache/fontconfig/\*.cache-4
file read @ICONS_FILES
file read proc:/sys/vm/overcommit_memory
file read /sys/devices/\*/\*/\*/\*/\*/modalias
file read /sys/devices/\*/\*/\*/\*/\*/video4linux/video0/dev
file read /sys/devices/\*/\*/\*/\*/idProduct
file read /sys/devices/\*/\*/\*/\*/idVendor
file read /sys/devices/\*/\*/\*/\*/speed
file read /sys/devices/system/cpu/cpu0/cpufreq/scaling_cur_freq
file read /sys/devices/system/cpu/cpu0/cpufreq/scaling_max_freq
file read /sys/devices/system/cpu/online
file read/write /dev/snd/\*
file read/write /dev/video0
file read/write/truncate /home/\*/.config/Trolltech.conf
file read/write/unlink /home/\*/.cache/fontconfig/\*
file read/write/unlink /tmp/qtsingleapp-\*
file read/write/unlink/truncate @SKYPE_FILES
file rename @SKYPE_DIRS @SKYPE_DIRS
file rename @SKYPE_FILES @SKYPE_FILES
file rmdir @SKYPE_DIRS
misc env \*
network inet dgram bind 0.0.0.0 0-65535
network inet dgram bind 127.0.0.1 0
network inet dgram bind/send 0.0.0.0-255.255.255.255 0-65535
network inet stream bind/listen 0.0.0.0 0-65535
network inet stream connect 0.0.0.0-255.255.255.255 0-65535
network unix stream bind/listen/connect /tmp/qtsingleapp-\*
network unix stream connect /tmp/.ICE-unix/\*
network unix stream connect /var/run/dbus/system_bus_socket
network unix stream connect /var/run/nscd/socket
network unix stream connect \000/tmp/.ICE-unix/\*
network unix stream connect \000/tmp/.X11-unix/X0
network unix stream connect \000/tmp/dbus-\*
network unix stream connect /run/user/1000/pulse/native

<kernel> /usr/lib32/skype/skype /usr/bin/xdg-open
use_profile 0
use_group 0

<kernel> /usr/lib32/skype/skype /usr/bin/gnome-open
use_profile 0
use_group 0

<kernel> /usr/lib32/skype/skype /usr/bin/notify-send
use_profile 0
use_group 0
```

*   По окончанию редактирования перезагрузите конфигурационные файлы TOMOYO, выполнив команды:

```
# tomoyo-loadpolicy -df < /etc/tomoyo/domain_policy.conf
# tomoyo-loadpolicy -ef < /etc/tomoyo/exception_policy.conf
```

Теперь Skype в песочнице.

Заметьте, что данные настройки созданы для 64-битной системы Arch, и некоторые из ваших ioctls и путей библиотек могут отличаться от указанных выше. Итак, что бы довести до ума ваши настройки TOMOYO для Skype загрузите демон `tomoyo-auditd`:

```
# systemctl start tomoyo-auditd

```

Затем отправляйтесь в папку `/var/log/tomoyo` и наблюдайте за `reject_003.log`:

```
$ tail -f reject_003.log

```

Вывод данной команды продемонстрирует вам отброшенные действия Skype, так что вы сможете добавить их в файл `domain_policy.conf` если потребуется.

Посмотрите [[2]](http://tomoyo.sourceforge.jp/2.5/index.html.en) для детализированной инструкции настройки TOMOYO.

#### Доступ к полученным файлам

По умолчанию `skype` хранит полученные файлы с допуском 600 (только владелец имеет доступ к ним). Можно использовать [incron](https://www.archlinux.org/packages/?name=incron) для автоматического доступа к скачиваемым файлам.

**Примечание:** Этот пример подразумевает, что ваши скачанные файлы skype кладёт в `/home/skype/downloads`

Делаем папки home и download доступными Skype:

```
# chmod 755 /home/skype /home/skype/downloads

```

Установим incron из пакета [incron](https://www.archlinux.org/packages/?name=incron) доступного в [официальных репозиториях](/index.php/%D0%9E%D1%84%D0%B8%D1%86%D0%B8%D0%B0%D0%BB%D1%8C%D0%BD%D1%8B%D1%85_%D1%80%D0%B5%D0%BF%D0%BE%D0%B7%D0%B8%D1%82%D0%BE%D1%80%D0%B8%D1%8F%D1%85 "Официальных репозиториях"), активируем и запустим `incrond` [используя systemd](/index.php/Systemd#Using_units "Systemd"). Откроем incrontab для пользователя root:

```
# incrontab -e

```

Добавим задание incron:

```
/home/skype/downloads IN_CREATE chmod 644 $@/$#

```

Сохраним изменения и выйдем из редактора incrontab.

Для проверки работоспособности incron просто войдите в папку skype/donwload и создайте тестовый файл:

```
# cd /home/skype/downloads
# install -m 600 /dev/null test.txt
# ls -l test.txt

```

Права на фал должны быть 644 или -rw-r--r--

(По желанию) симлинкуйте папку skype/download в папку home:

```
$ ln -s /home/skype/downloads ~/skype_files

```

### Sandfox

[sandfox](https://aur.archlinux.org/packages/sandfox/) включает профиль, который позволяет запускать Skype в [chroot](/index.php/Change_root_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Change root (Русский)"). Вам также может очень захотеться установить [sandfox-extras](https://aur.archlinux.org/packages/sandfox-extras/) для слаженной работы с [systemd](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd (Русский)").

В случае проблем проверьте связи с профилем [#AppArmor](#AppArmor) или запустите (от имени суперпользователя):

```
$ sandfox --verbose skype

```

## Плагин Skype для Pidgin

Смотрите раздел [Pidgin (Русский)#Плагин Skype](/index.php/Pidgin_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.9F.D0.BB.D0.B0.D0.B3.D0.B8.D0.BD_Skype "Pidgin (Русский)").