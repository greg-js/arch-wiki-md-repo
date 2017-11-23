Related articles

*   [Kernel modules (Русский)](/index.php/Kernel_modules_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Kernel modules (Русский)")
*   [Advanced Linux Sound Architecture (Русский)](/index.php/Advanced_Linux_Sound_Architecture_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Advanced Linux Sound Architecture (Русский)")

**Состояние перевода:** На этой странице представлен перевод статьи [PC speaker](/index.php/PC_speaker "PC speaker"). Дата последней синхронизации: 21 ноября 2017\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=PC_speaker&diff=0&oldid=497536).

Хотим мы этого или нет, компьютер часто издает звуковые сигналы и другие звуки. Они происходят из различных источников и, как правило, вы можете настроить условие или время для их срабатывания. Для случаев, когда нет звуковой карты или динамиков, и требуется простое аудио оповещение, смотрите раздел [#Beep](#Beep).

Звуковой сигнал компьютера может раздасться из встроенного динамика, колонок или наушников, которые подключены к звуковой карте (в некоторых случаях шум может быть неожиданно громким).

**Примечание:** Звуковые сигналы могут быть вызваны BIOS (базовая система ввода/вывода), OS (операционная система), DE (окружение рабочего стола), или различными приложениями. BIOS вызывает наибольшие проблемы из-за того, что он хранится на чипе EPROM, на материнской плате, и единственным непосредственным управлением, которое доступно пользователю, остается включение/выключение питания. Внести какие-либо изменения для него невозможно, если настройки BIOS не имеют опции, которые вы можете применить, или вы не хотите попробовать перепрограммировать этот чип с соответствующей прошивкой. Сгенерированые BIOS звуковые сигналы задаются не здесь, но вы можете вовсе отсоединить встроенный динамик для отключения всех системных звуков. (Делайте это на свой страх и риск.)

## Contents

*   [1 Отключение PC Speaker](#.D0.9E.D1.82.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_PC_Speaker)
    *   [1.1 Глобально](#.D0.93.D0.BB.D0.BE.D0.B1.D0.B0.D0.BB.D1.8C.D0.BD.D0.BE)
    *   [1.2 Xorg](#Xorg)
    *   [1.3 Терминал](#.D0.A2.D0.B5.D1.80.D0.BC.D0.B8.D0.BD.D0.B0.D0.BB)
    *   [1.4 ALSA](#ALSA)
    *   [1.5 GNOME](#GNOME)
    *   [1.6 Cinnamon](#Cinnamon)
    *   [1.7 GTK+](#GTK.2B)
*   [2 Beep](#Beep)
    *   [2.1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
    *   [2.2 Доступ для обычных (non-root) пользователей](#.D0.94.D0.BE.D1.81.D1.82.D1.83.D0.BF_.D0.B4.D0.BB.D1.8F_.D0.BE.D0.B1.D1.8B.D1.87.D0.BD.D1.8B.D1.85_.28non-root.29_.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D0.B5.D0.B9)
    *   [2.3 Полезные советы](#.D0.9F.D0.BE.D0.BB.D0.B5.D0.B7.D0.BD.D1.8B.D0.B5_.D1.81.D0.BE.D0.B2.D0.B5.D1.82.D1.8B)
*   [3 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Отключение PC Speaker

Отключение конкретного источника звука, в то время, когда остальные продолжают работать, возможно только в том случае, если мы может определить какая часть окружения сгенерировала конкретный звук. Это позволяет выборочно настраивать звуки. Пожалуйста, размещайте свои примеры настроек и конфигураций, которые могут оказаться полезными для других пользователей.

### Глобально

PC speaker может быть отключен [выгрузкой](/index.php/Kernel_modules_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A3.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BC.D0.BE.D0.B4.D1.83.D0.BB.D1.8F.D0.BC.D0.B8_.D0.B2.D1.80.D1.83.D1.87.D0.BD.D1.83.D1.8E "Kernel modules (Русский)") [модуля ядра](/index.php/Kernel_modules_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Kernel modules (Русский)") `pcspkr`:

```
# rmmod pcspkr

```

[Помещение в черный список](/index.php/Kernel_modules_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.97.D0.B0.D0.BF.D1.80.D0.B5.D1.82_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B8 "Kernel modules (Русский)") модуля `pcspkr` предотвратит его загрузку [udev](/index.php/Udev "Udev") при загрузке системы:

```
# echo "blacklist pcspkr" > /etc/modprobe.d/nobeep.conf

```

[Размещение в черном списке в командной строке ядра](/index.php/Kernel_modules_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.97.D0.B0.D0.BF.D1.80.D0.B5.D1.82_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B8 "Kernel modules (Русский)") - еще один способ добиться похожего эффекта. Просто добавьте `modprobe.blacklist=pcspkr` к вашей строке начальной загрузки ядра.

### Xorg

```
$ xset -b

```

You can add this command to a startup file such as `/etc/xprofile` to make it permanent. See [xprofile](/index.php/Xprofile_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xprofile (Русский)") for more information.

### Терминал

Вы можете добавить эту команду в `/etc/profile` или в отдельный файл вроде `/etc/profile.d/disable-beep.sh`:

```
setterm -blength 0

```

Другой способ - это добавить или раскомментировать строку в `/etc/inputrc` или `~/.inputrc`:

```
set bell-style none

```

### ALSA

Для большинства звуковых карт PC speaker отображается как канал [ALSA](/index.php/ALSA "ALSA"), и может называться как *PC Speaker*, *PC Beep*, или *Beep*. Чтобы заглушить динамик, воспользуйтесь *alsamixer* или *amixer*.

```
$ amixer set *channel* 0% mute

```

Для включения звука обратитесь к странице руководства [Advanced Linux Sound Architecture (Русский)#Включить звук каналов](/index.php/Advanced_Linux_Sound_Architecture_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.92.D0.BA.D0.BB.D1.8E.D1.87.D0.B8.D1.82.D1.8C_.D0.B7.D0.B2.D1.83.D0.BA_.D0.BA.D0.B0.D0.BD.D0.B0.D0.BB.D0.BE.D0.B2 "Advanced Linux Sound Architecture (Русский)").

**Совет:** Если вы используете PulseAudio и канал PC speaker не отображается в устройствах ALSA по умолчанию, попробуйте выбрать устройства соответствующей звуковой карты - прокси-контроль PulseAudio может не отображать PC speaker

### GNOME

При использовании GSettings:

```
$ gsettings set org.gnome.desktop.wm.preferences audible-bell false

```

### Cinnamon

В Cinnamon вероятно используется звук "падающей капли". Для его отключения, измените в dconf:

```
$ dconf write /org/cinnamon/desktop/wm/preferences/audible-bell false

```

### GTK+

Добавьте следующую строку в `~/.gtkrc-2.0`:

```
gtk-error-bell = 0

```

Добавьте такую же строку в секцию [Settings] файла `$XDG_CONFIG_HOME/gtk-3.0/settings.ini`:

```
[Settings]
gtk-error-bell = 0

```

Подробно это рассмотрено в [Gnome Developer Handbook](https://developer.gnome.org/gtk3/stable/GtkSettings.html).

## Beep

Beep - это улучшенная программа для подачи звукового сигнала посредством PC speaker. Она может оказаться востребована в ситуациях, когда звуковая карта отсутствует или нет доступных динамиков, но требуется простое звуковое уведомление.

### Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [beep](https://www.archlinux.org/packages/?name=beep).

Возможно, вам потребуется [включить звук](#ALSA) канала PC speaker в [ALSA](/index.php/ALSA "ALSA").

### Доступ для обычных (non-root) пользователей

По умолчанию, `beep` не будет работать, если запущена не с правами суперпользователя. Другие пользователи могут использовать ее при помощи [sudo](/index.php/Sudo_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Sudo (Русский)"). Для передачи группе `users` возможности вызывать `sudo beep` без пароля (например, для использования в скриптах), [следует отредактировать](/index.php/Sudo_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_visudo "Sudo (Русский)") `/etc/sudoers`:

```
%users ALL=(ALL) NOPASSWD: /usr/bin/beep

```

или выдать права только одному пользователю:

```
username ALL=(ALL) NOPASSWD: /usr/bin/beep

```

Также можно настроить бит закрепления в памяти `/usr/bin/beep`:

```
# chmod 4755 /usr/bin/beep

```

Обратите внимание, что при этом **любой** сможет выполнять `/usr/bin/beep` без прав суперпользователя. Изменение также создаст разность между локальной копией и пакетом, о чем будет сообщено в `pacman -Qkk`.

### Полезные советы

В то время, как большинство пользователей устраивает звуковой сигнал по умолчанию, некоторые, возможно, захотят его слегка изменить. Следующий пример позволит сделать звуковой сигнал выше и короче, и повторит два раза.

```
# beep -f 5000 -l 50 -r 2

```

## Смотрите также

*   [xset(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/xset.1), [setterm(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/setterm.1), [readline(3)](http://jlk.fjfi.cvut.cz/arch/manpages/man/readline.3)