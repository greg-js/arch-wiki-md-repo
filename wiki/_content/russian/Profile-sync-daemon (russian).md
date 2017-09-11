[Profile-sync-daemon](https://aur.archlinux.org/packages/Profile-sync-daemon/) (psd) — небольшой псевдо-демон, предназначенный для переноса профилей браузеров в tmpfs (ОЗУ) и синхронизации с постоянным хранилищем (HDD/SSD) используя rsync. Демон автоматически производит резервные копии на случай возникновения сбоев.

## Contents

*   [1 Преимущества psd](#.D0.9F.D1.80.D0.B5.D0.B8.D0.BC.D1.83.D1.89.D0.B5.D1.81.D1.82.D0.B2.D0.B0_psd)
*   [2 Установка и настройка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.B8_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [2.1 Редактируем файл с конфигурацией](#.D0.A0.D0.B5.D0.B4.D0.B0.D0.BA.D1.82.D0.B8.D1.80.D1.83.D0.B5.D0.BC_.D1.84.D0.B0.D0.B9.D0.BB_.D1.81_.D0.BA.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D0.B5.D0.B9)
*   [3 Поддерживаемые браузеры](#.D0.9F.D0.BE.D0.B4.D0.B4.D0.B5.D1.80.D0.B6.D0.B8.D0.B2.D0.B0.D0.B5.D0.BC.D1.8B.D0.B5_.D0.B1.D1.80.D0.B0.D1.83.D0.B7.D0.B5.D1.80.D1.8B)
*   [4 Использование psd](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_psd)
    *   [4.1 Проверка конфигурации](#.D0.9F.D1.80.D0.BE.D0.B2.D0.B5.D1.80.D0.BA.D0.B0_.D0.BA.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D0.B8)
    *   [4.2 Режим чистки](#.D0.A0.D0.B5.D0.B6.D0.B8.D0.BC_.D1.87.D0.B8.D1.81.D1.82.D0.BA.D0.B8)
    *   [4.3 Запуск и завершение psd](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D0.B8_.D0.B7.D0.B0.D0.B2.D0.B5.D1.80.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_psd)
*   [5 Поддерживаемые дистрибутивы](#.D0.9F.D0.BE.D0.B4.D0.B4.D0.B5.D1.80.D0.B6.D0.B8.D0.B2.D0.B0.D0.B5.D0.BC.D1.8B.D0.B5_.D0.B4.D0.B8.D1.81.D1.82.D1.80.D0.B8.D0.B1.D1.83.D1.82.D0.B8.D0.B2.D1.8B)
    *   [5.1 Установка частоты синхронизации (опционально)](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D1.87.D0.B0.D1.81.D1.82.D0.BE.D1.82.D1.8B_.D1.81.D0.B8.D0.BD.D1.85.D1.80.D0.BE.D0.BD.D0.B8.D0.B7.D0.B0.D1.86.D0.B8.D0.B8_.28.D0.BE.D0.BF.D1.86.D0.B8.D0.BE.D0.BD.D0.B0.D0.BB.D1.8C.D0.BD.D0.BE.29)
*   [6 FAQ](#FAQ)
    *   [6.1 Что такое overlayfs и зачем его использовать?](#.D0.A7.D1.82.D0.BE_.D1.82.D0.B0.D0.BA.D0.BE.D0.B5_overlayfs_.D0.B8_.D0.B7.D0.B0.D1.87.D0.B5.D0.BC_.D0.B5.D0.B3.D0.BE_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D1.8C.3F)
    *   [6.2 Overlayfs требует больше памяти для размещения моего профиля/профилей в /run/user/xxxx. Как мне выделить больше?](#Overlayfs_.D1.82.D1.80.D0.B5.D0.B1.D1.83.D0.B5.D1.82_.D0.B1.D0.BE.D0.BB.D1.8C.D1.88.D0.B5_.D0.BF.D0.B0.D0.BC.D1.8F.D1.82.D0.B8_.D0.B4.D0.BB.D1.8F_.D1.80.D0.B0.D0.B7.D0.BC.D0.B5.D1.89.D0.B5.D0.BD.D0.B8.D1.8F_.D0.BC.D0.BE.D0.B5.D0.B3.D0.BE_.D0.BF.D1.80.D0.BE.D1.84.D0.B8.D0.BB.D1.8F.2F.D0.BF.D1.80.D0.BE.D1.84.D0.B8.D0.BB.D0.B5.D0.B9_.D0.B2_.2Frun.2Fuser.2Fxxxx._.D0.9A.D0.B0.D0.BA_.D0.BC.D0.BD.D0.B5_.D0.B2.D1.8B.D0.B4.D0.B5.D0.BB.D0.B8.D1.82.D1.8C_.D0.B1.D0.BE.D0.BB.D1.8C.D1.88.D0.B5.3F)
    *   [6.3 Моя система аварийно завершила работу и не была синхронизирована. Что мне делать?](#.D0.9C.D0.BE.D1.8F_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D0.B0_.D0.B0.D0.B2.D0.B0.D1.80.D0.B8.D0.B9.D0.BD.D0.BE_.D0.B7.D0.B0.D0.B2.D0.B5.D1.80.D1.88.D0.B8.D0.BB.D0.B0_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D1.83_.D0.B8_.D0.BD.D0.B5_.D0.B1.D1.8B.D0.BB.D0.B0_.D1.81.D0.B8.D0.BD.D1.85.D1.80.D0.BE.D0.BD.D0.B8.D0.B7.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B0._.D0.A7.D1.82.D0.BE_.D0.BC.D0.BD.D0.B5_.D0.B4.D0.B5.D0.BB.D0.B0.D1.82.D1.8C.3F)
    *   [6.4 Где я могу найти снимок?](#.D0.93.D0.B4.D0.B5_.D1.8F_.D0.BC.D0.BE.D0.B3.D1.83_.D0.BD.D0.B0.D0.B9.D1.82.D0.B8_.D1.81.D0.BD.D0.B8.D0.BC.D0.BE.D0.BA.3F)
    *   [6.5 Как восстановить снимок?](#.D0.9A.D0.B0.D0.BA_.D0.B2.D0.BE.D1.81.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.B8.D1.82.D1.8C_.D1.81.D0.BD.D0.B8.D0.BC.D0.BE.D0.BA.3F)
    *   [6.6 Может ли psd удалить снимки автоматически?](#.D0.9C.D0.BE.D0.B6.D0.B5.D1.82_.D0.BB.D0.B8_psd_.D1.83.D0.B4.D0.B0.D0.BB.D0.B8.D1.82.D1.8C_.D1.81.D0.BD.D0.B8.D0.BC.D0.BA.D0.B8_.D0.B0.D0.B2.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8.3F)
*   [7 Поддержка](#.D0.9F.D0.BE.D0.B4.D0.B4.D0.B5.D1.80.D0.B6.D0.BA.D0.B0)
*   [8 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Преимущества psd

Цели psd:

1.  Простота в использовании.
2.  Уменьшение износа жесткого диска.
3.  Увеличение скорости работы браузера.

Профили, кэш, и прочие пользовательские данные браузера переносятся с помощью psd в tmpfs (ОЗУ), соответственно операции ввода/вывода браузера перенаправляются в оперативную память. Таким образом, уменьшается износ жесткого диска, повышается отказоустойчивость и скорость работы браузера: время доступа к оперативной памяти составляет порядка наносекунд, в свою очередь, время доступа обычного жесткого диска приблизительно в 1,000,000 раз выше и составляет порядка миллисекунд.

**Примечание:** Такие браузеры как Chromium, Firefox, Midori и Rekonq хранят файлы кеша в **отдельном** от профиля каталоге. Изменение этого поведения программы не входит в задачи profile-sync-daemon. Пользователям рекомендуется обратиться к разделу [Chromium tweaks#Cache in tmpfs](/index.php/Chromium_tweaks#Cache_in_tmpfs "Chromium tweaks") для Chromium и к статье [Firefox Ramdisk](/index.php/Firefox_Ramdisk "Firefox Ramdisk") для Firefox, где описаны возможные решения проблемы. Наиболее простое решение будет переносом каталога с кешом (например, `/home/$USER/.cache/<browser>/<profile>/`) в каталог с профилем браузера, например `/home/$USER/.mozilla/firefox/<profile>/cache`, и создать символьную ссылку из стандартного пути в новый. Таким образом, profile-sync-daemon автоматически будет учитывать каталог с кешем.

## Установка и настройка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [profile-sync-daemon](https://aur.archlinux.org/packages/profile-sync-daemon/).

### Редактируем файл с конфигурацией

Произведите первый запуск psd, это создаст файл `$XDG_CONFIG_HOME/psd/psd.conf`, который содержит все опции.

**Примечание:** Любые изменения произведённые в этом файле вступят в силу только после перезапуска psd посредством пользовательского systemd сервиса.

```
$ psd
First time running psd so please edit /home/facade/.config/psd/psd.conf to your liking and run again.

```

*   Опционально включите использование overlayfs для улучшения скорости синхронизации и уменьшить количество необходимой памяти. Для этого используйте переменную USE_OVERLAYFS. Пользователю понадобятся sudo права доступа к `/usr/bin/psd-overlay-helper` для использования этой опции, а также ядро должно поддерживать overlayfs версии 22 или новее. Смотрите FAQ ниже чтобы узнать подробности.
*   Опционально укажите названия веб-браузеров, профили которых необходимо перенести в ОЗУ, посредством массива BROWSERS. Если в этой переменной ничего не указано, по умолчанию перенесутся все найденные профили поддерживаемых браузеров.
*   По необходимости можете указать путь к tmpfs разделу с помощью переменной VOLATILE.
*   По необходимости можете выключить создание резервных копий профиля (не рекоммендуется) с помощью переменной USE_BACKUPS.

Пример: Допустим что у вас установлены браузеры Chromium, Opera и Midori, однако вы хотите перенести профили в ОЗУ только для Chromium и Opera:

```
# List browsers separated by spaces to include in the sync. Useful if you do not
# wish to have all possible browser profiles sync'ed.
#
# Possible values:
#  chromium
#  chromium-dev
#  conkeror.mozdev.org
#  epiphany
#  firefox
#  firefox-trunk
#  google-chrome
#  google-chrome-beta
#  google-chrome-unstable
#  heftig-aurora
#  icecat
#  luakit
#  midori
#  opera
#  opera-developer
#  opera-beta
#  qupzilla
#  palemoon
#  rekonq
#  seamonkey
#  vivaldi
#
# If the following is commented out (default), then all available/supported 
# browsers will be sync'ed, separated by comma
BROWSERS="chromium opera"

```

## Поддерживаемые браузеры

В настоящее время следующие браузеры поддерживаются:

*   [Chromium](/index.php/Chromium "Chromium")
*   [chromium-dev](/index.php/AUR "AUR")
*   [conkeror-git](https://aur.archlinux.org/packages/conkeror-git/)
*   [Epiphany](/index.php/Epiphany "Epiphany")
*   [Firefox](/index.php/Firefox "Firefox") (stable, beta и aurora)
*   [google-chrome](https://aur.archlinux.org/packages/google-chrome/)
*   [google-chrome-beta](https://aur.archlinux.org/packages/google-chrome-beta/)
*   [google-chrome-dev](https://aur.archlinux.org/packages/google-chrome-dev/)
*   [Версия Aurora от heftig](https://bbs.archlinux.org/viewtopic.php?id=117157)
*   [icecat](https://aur.archlinux.org/packages/icecat/)
*   [Luakit](/index.php/Luakit "Luakit")
*   [Midori](/index.php/Midori "Midori")
*   [Opera](/index.php/Opera "Opera")
*   Qupzilla
*   [rekonq](https://aur.archlinux.org/packages/rekonq/)
*   [seamonkey](https://www.archlinux.org/packages/?name=seamonkey)
*   [vivaldi](https://aur.archlinux.org/packages/vivaldi/)

## Использование psd

### Проверка конфигурации

Запуск с опцией 'parse' показывает что именно *psd* будет делать, основываясь на конфигурации в `$XDG_CONFIG_HOME/psd/psd.conf`, а также выведет прочую полезную информацию.

```
$ psd p
Profile-sync-daemon v6.03 on Arch Linux.

 Systemd service is currently active.
 Systemd resync service is currently active.
 Overlayfs v23 is currently active.

Psd will manage the following per /home/facade/.config/psd/psd.conf settings:

 browser/psname:  chromium/chromium
 owner/group:     facade/100
 sync target:     /home/facade/.config/chromium
 tmpfs dir:       /run/user/1000/facade-chromium
 profile size:    93M
 overlayfs size:  39M
 recovery dirs:   2 <- delete with the c option
  dir path/size:  /home/facade/.config/chromium-backup-crashrecovery-20150117_171359 (92M)
  dir path/size:  /home/facade/.config/chromium-backup-crashrecovery-20150119_112204 (93M)

 browser/psname:  firefox/firefox
 owner/group:     facade/100
 sync target:     /mnt/data/docs/facade/mozilla/firefox/f8cv8bfu.default
 tmpfs dir:       /run/user/1000/facade-firefox-f8cv8bfu.default
 profile size:    145M
 overlayfs size:  13M
 recovery dirs:   none

```

Как показано в выводе и указано выше, если в массиве BROWSERS не задан конкретный список браузеров, *psd* будет синхронизировать все профили поддерживаемых браузеров, которые он сможет найти для данного пользователя.

### Режим чистки

Режим чистки удалит все резервные копии. Запускайте этот режим только если вы уверенны что собранные резервные копии больше не понадобятся.

```
$ psd c

Profile-sync-daemon v6.03 on Arch Linux.

Deleting 2 crashrecovery dirs for profile /home/facade/.config/chromium
 /home/facade/.config/chromium-backup-crashrecovery-20150117_171359
 /home/facade/.config/chromium-backup-crashrecovery-20150119_112204

```

### Запуск и завершение psd

В последних версиях psd поддерживается только systemd как демон инициализации. Psd включает в себя пользовательский systemd сервис для запуска и завершения psd (psd.service).

Для пользователей, незнакомых с пользовательским режимом systemd, используйте следующую команду для запуска сервиса psd:

```
$ systemctl --user [option] psd.service

```

Доступные опции: start stop enable disable status

## Поддерживаемые дистрибутивы

*psd* представляет из себя обычный bash-скрипт и должен работать на любом дистрибутиве Linux. Многие дистрибутивы предоставляют официальные и пользовательские пакеты для установки psd. На [официальном сайте](https://github.com/graysky2/profile-sync-daemon#installation-from-distro-packages) доступен список пакетов и инструкции по установке.

### Установка частоты синхронизации (опционально)

Предоставленный с пакетом таймер настроен на синхронизацию с интервалом в один час. Пользователь может легко установить другой желаемый интервал, редактируя файл установок таймера. В примере ниже таймер установлен на сихронизацию с интервалом в 10 минут.

 `/etc/systemd/system/psd-resync.timer.d/frequency.conf` 
```
[Unit]
Description=Timer for Profile-sync-daemon - 10min

[Timer]
# Empty value resets the list of timers
OnUnitActiveSec=
OnUnitActiveSec=10min

```

См. [systemd.timer(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.timer.5) для получения дополнительной информации о настройке таймеров.

## FAQ

### Что такое overlayfs и зачем его использовать?

Overlayfs это простая файловая система, включенная в ядро Linux с версии 3.18.0\. В psd, начиная с версии 5.54, overlayfs можно использовать, чтобы уменьшить занимаемую демоном psd память в tmpfs и ускорить операции синхронизации с диском. Особенность метода в том, что overlayfs записывает только измененные данные, а не весь профиль. Те же функции восстановления, которые использует psd в своем режиме по умолчанию, также активны при работе в режиме overlayfs. Чтобы включить режим Overlayfs, нужно раскомментировать строку USE_OVERLAYFS="yes" в `$XDG_CONFIG_HOME/psd/psd.conf` и затем перезапустить демон.

Существует несколько версий overlayfs, доступных в ядре Linux в различных дистрибутивах. В версиях 22 и ниже есть модуль под названием 'overlayfs', а в более новых версиях (23 и выше) есть модуль под названием 'overlay' -- обратите внимание на отсутствие 'fs' в новой версии. psd автоматически обнаружит overlayfs, доступный в вашем ядре, если тот настроен на его использование.

Начиная с версии psd 6.05, пользователи, желающие использовать этот режим, ДОЛЖНЫ иметь права sudo (без запроса на ввод пароля) для файла `/usr/bin/psd-overlay-helper` или же глобально. Следующая строка в файле `/etc/sudoers` предоставит пользователю эти права. Добавьте её с помощью `/usr/bin/visudo` от имени root:

```
foo ALL=NOPASSWD: /usr/bin/psd-overlay-helper

```

См. пример в разделе "Проверка конфигурации" выше, в котором показана система, использующая overlayfs для иллюстрации возможностей экономии памяти.

Обратите внимание на строку "overlayfs size" в сравнении со строкой "profile size" для каждого профиля. Имейте в виду, что эти цифры будут меняться в зависимости от объема данных, записываемых в профиль, но при обычном использовании размер overlayfs всегда будет меньше размера профиля.

### Overlayfs требует больше памяти для размещения моего профиля/профилей в /run/user/xxxx. Как мне выделить больше?

Стандартный способ контроля размера /run/user это директива RuntimeDirectorySize в logind.conf (подробнее см. man-страницу для logind.conf). По умолчанию используется 10% физической памяти, но можно безопасно ее увеличить. Помните, что tmpfs использует только то, что фактически используется; Указанное здесь число является только максимально допустимым.

### Моя система аварийно завершила работу и не была синхронизирована. Что мне делать?

Скорее всего, "последняя целая" резерваная копия of ваших профилей браузеров все ещё в сохранности у вас на жестком диске. При перезапуске `psd` (например, при перезагрузке), выполняется проверка, чтобы убедиться, что символическая ссылка на копию в tmpfs вашего профиля недействительна. Если она недействительна, psd снимет "последнюю целую" резервную копию, прежде чем вернуть её на место.

Эта опция больше для проверки, что *psd* работоспособен и любая потеря данных была по причине чего-то другого.

**Примечание:** Пользователи могут полностью отключить функцию моментального снимка/резервного копирования, раскомментировав и установив переменную USE_BACKUPS в значение 'no' в `$XDG_CONFIG_HOME/psd/psd.conf`, если нужно.

### Где я могу найти снимок?

Это зависит от браузера. Вы найдете моментальный снимок в том же каталоге, что и профиль браузера, и он будет содержать отметку даты и времени, которая соответствует времени, когда был сделан снимок. Например, для chromium это будет `~/.config/chromium-backup-crashrecovery-20130912_153310` -- конечно, отметка времени у вас будет своя.

### Как восстановить снимок?

*   Остановить `psd`.
*   Убедиться, что нет символьной ссылки на директорию профиля браузера в tmpfs. Если есть, *psd* не был завершен корректно по другим причинам.
*   Переместите "плохую" копию профиля в резервную копию (не удаляйте ничего просто так).
*   Скопируйте каталог с моментальным снимком туда, куда нужно для конкретного браузера.

Пример для браузера Chromium:

```
mv ~/.config/chromium ~/.config/chromium-bad
cp -a ~/.config/chromium-backup-crashrecovery-20130912_153310 ~/.config/chromium

```

Теперь вы можете запустить Chromium, который будет использовать скопированный резервный снимок. Если все в порядке, закройте браузер и перезапустите psd. На этом этапе вы можете безопасно удалить `~/.config/chromium-backup-crashrecovery-20130912_153310`.

### Может ли psd удалить снимки автоматически?

Да, запустите psd с ключом "clean" для удаления снимков.

## Поддержка

Пишите в [тему на форуме (англ.)](https://bbs.archlinux.org/viewtopic.php?pid=1026974) для комментариев и прочих обсуждений.

## Смотрите также

*   [http://www.webupd8.org/2013/02/keep-your-browser-profiles-in-tmpfs-ram.html](http://www.webupd8.org/2013/02/keep-your-browser-profiles-in-tmpfs-ram.html)
*   [http://bernaerts.dyndns.org/linux/250-ubuntu-tweaks-ssd](http://bernaerts.dyndns.org/linux/250-ubuntu-tweaks-ssd)