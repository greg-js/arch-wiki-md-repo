Ссылки по теме

*   [Экранный менеджер](/index.php/%D0%AD%D0%BA%D1%80%D0%B0%D0%BD%D0%BD%D1%8B%D0%B9_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80 "Экранный менеджер")

**Важно:** Проект SliM заброшен ([домашняя страница проекта](http://slim.berlios.de/) не работает, осталось только [зеркало для скачки](http://sourceforge.net/projects/slim.berlios/)) и SLIM не полностью совместим с [systemd](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd (Русский)"), в том числе с *logind* сеансами. Рекомендуется использовать другой [Экранный менеджер](/index.php/%D0%AD%D0%BA%D1%80%D0%B0%D0%BD%D0%BD%D1%8B%D0%B9_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80 "Экранный менеджер") или [Xinitrc](/index.php/Xinitrc "Xinitrc").

[SLiM](http://sourceforge.net/projects/slim.berlios/) - это акроним словосочетания **S**imple **L**og**i**n **M**anager (простой менеджер входа). SLIM является легковесным, легко настраеваемым, требует минимум зависимостей и не требует ни одну из зависимостей для окружений рабочего стола [GNOME](/index.php/GNOME_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GNOME (Русский)") или [KDE](/index.php/KDE_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "KDE (Русский)"). Поэтому SLIM оставляет систему легковесной, что подойдёт для пользователей легковесных рабочих столов, таких как [Xfce](/index.php/Xfce_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xfce (Русский)"), [Openbox](/index.php/Openbox_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Openbox (Русский)"), and [Fluxbox](/index.php/Fluxbox_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Fluxbox (Русский)").

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [2.1 Включение SLiM](#.D0.92.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_SLiM)
*   [3 Одиночные Среды](#.D0.9E.D0.B4.D0.B8.D0.BD.D0.BE.D1.87.D0.BD.D1.8B.D0.B5_.D0.A1.D1.80.D0.B5.D0.B4.D1.8B)
*   [4 Автоматический вход](#.D0.90.D0.B2.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8.D0.B9_.D0.B2.D1.85.D0.BE.D0.B4)
*   [5 Выбор окружения](#.D0.92.D1.8B.D0.B1.D0.BE.D1.80_.D0.BE.D0.BA.D1.80.D1.83.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F)
    *   [5.1 Версия ≤1.3.5](#.D0.92.D0.B5.D1.80.D1.81.D0.B8.D1.8F_.E2.89.A41.3.5)
    *   [5.2 Версия ≥1.3.6](#.D0.92.D0.B5.D1.80.D1.81.D0.B8.D1.8F_.E2.89.A51.3.6)
*   [6 Темы](#.D0.A2.D0.B5.D0.BC.D1.8B)
*   [7 Советы и Хитрости](#.D0.A1.D0.BE.D0.B2.D0.B5.D1.82.D1.8B_.D0.B8_.D0.A5.D0.B8.D1.82.D1.80.D0.BE.D1.81.D1.82.D0.B8)
    *   [7.1 Изменение курсора](#.D0.98.D0.B7.D0.BC.D0.B5.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BA.D1.83.D1.80.D1.81.D0.BE.D1.80.D0.B0)
    *   [7.2 Общие темы для Slim и Рабочего Стола](#.D0.9E.D0.B1.D1.89.D0.B8.D0.B5_.D1.82.D0.B5.D0.BC.D1.8B_.D0.B4.D0.BB.D1.8F_Slim_.D0.B8_.D0.A0.D0.B0.D0.B1.D0.BE.D1.87.D0.B5.D0.B3.D0.BE_.D0.A1.D1.82.D0.BE.D0.BB.D0.B0)
    *   [7.3 Выключение, перезагрузка, режим сна, выход, запуск терминала из SLIM](#.D0.92.D1.8B.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5.2C_.D0.BF.D0.B5.D1.80.D0.B5.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B0.2C_.D1.80.D0.B5.D0.B6.D0.B8.D0.BC_.D1.81.D0.BD.D0.B0.2C_.D0.B2.D1.8B.D1.85.D0.BE.D0.B4.2C_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D1.82.D0.B5.D1.80.D0.BC.D0.B8.D0.BD.D0.B0.D0.BB.D0.B0_.D0.B8.D0.B7_SLIM)
    *   [7.4 Ошибка с выключением заставки](#.D0.9E.D1.88.D0.B8.D0.B1.D0.BA.D0.B0_.D1.81_.D0.B2.D1.8B.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5.D0.BC_.D0.B7.D0.B0.D1.81.D1.82.D0.B0.D0.B2.D0.BA.D0.B8)
    *   [7.5 Информация сесий в Slim](#.D0.98.D0.BD.D1.84.D0.BE.D1.80.D0.BC.D0.B0.D1.86.D0.B8.D1.8F_.D1.81.D0.B5.D1.81.D0.B8.D0.B9_.D0.B2_Slim)
    *   [7.6 Настройка DPI в Slim](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_DPI_.D0.B2_Slim)
    *   [7.7 Используйте случайные темы](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D1.83.D0.B9.D1.82.D0.B5_.D1.81.D0.BB.D1.83.D1.87.D0.B0.D0.B9.D0.BD.D1.8B.D0.B5_.D1.82.D0.B5.D0.BC.D1.8B)
    *   [7.8 Автомонтирование шифрованной /home при входе в систему](#.D0.90.D0.B2.D1.82.D0.BE.D0.BC.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.88.D0.B8.D1.84.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.BD.D0.BE.D0.B9_.2Fhome_.D0.BF.D1.80.D0.B8_.D0.B2.D1.85.D0.BE.D0.B4.D0.B5_.D0.B2_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.83)
*   [8 Ссылки](#.D0.A1.D1.81.D1.8B.D0.BB.D0.BA.D0.B8)

## Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") [slim](https://www.archlinux.org/packages/?name=slim) из [официальных репозиториев](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)").

## Настройка

**Примечание:** SLiM больше не поддерживает сессию 'по умолчанию', если включено несколько сессий. Это не заметно, если пытаетесь выйти, п потом обратно войти в ту же сессию.

Начиная с версии **1.3.6-2**, SLiM может автоматически определить установленные окружения рабочего стола и оконные менеджеры. Это достигается с помощью использования `sessiondir /usr/share/xsessions/` в `/etc/slim.conf`. Поэтому тем, кто устанавливал прошлую версию SLiM будет необходимо внести изменения в `/etc/slim.conf` и [xinitrc](/index.php/Xinitrc "Xinitrc"), соответственно.

### Включение SLiM

**Примечание:** [slim](https://www.archlinux.org/packages/?name=slim) зависит от *systemd-logind*.

[Включите](/index.php/%D0%92%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D0%B5 "Включите") SLiM сервис `slim.service`:

```
# systemctl enable slim.service

```

Предполагается, что до этого вы отключили включённый ранее дисплейный менеджер. Если это не так, измените [цель по умолчанию](/index.php/Systemd#Change_default_target_to_boot_into "Systemd").

## Одиночные Среды

Чтобы настроить загрузку определенной среды в SLIM , просто отредактируйте **~/.xinitrc** чтобы он выглядел следующим образом:

```
#!/bin/sh

#
# ~/.xinitrc
#
# Executed by startx (запустите ваш оконный менеджер отсюда)
#

exec [команда сеанса]

```

*   Примечание: Если у вас нет файла ~/.xinitrc, вы можете создать его (например с помощью nano). По умолчанию slim ищет этот файл для всех пользователей и будет жаловаться что "не может выполнить команду login " если нет такого файла в домашнем каталоге пользователя.

Замените ***[команду сеанса]*** соответствующей командой вашей вашего сеанса.Для примера:

Для запуска Openbox:

```
exec openbox-session

```

Для запуска Fluxbox:

```
exec fluxbox

```

или

```
exec startfluxbox

```

Для запуска Xfce:

```
exec startxfce4

```

Для запуска LXDE:

```
exec startlxde

```

Для запуска GNOME:

```
exec gnome-session

```

Для запуска KDE:

```
exec startkde

```

Для запуска FVWM2:

```
exec fvwm2

```

Для запуска FVWM-crystal:

```
exec fvwm-crystal

```

Для запуска Awesome:

```
exec awesome

```

Для запуска i3:

```
exec i3

```

Для запуска Enlightenment

```
exec enlightenment_start

```

Если ваше рабочее окружение, не перечислено здесь, обратитесь к документации по программному обеспечению

## Автоматический вход

Для того, чтобы сделать возможным автоматический вход в систему(без ввода пароля), необходимо раскомментировать следующие строки в /etc/slim.conf

```
# default_user        simone

```

Раскомментируйте эту строку и замените simone на имя Вашего пользователя.

```
# auto_login          no

```

Расскоментируйте эту строку и замените no на yes. Это позволит использовать автоматический вход.

## Выбор окружения

### Версия ≤1.3.5

Если вам нужна возможность выбора окружения рабочего стола из списка, SLiM нужно настроить следующим образом.

Поместите правило, подобное этому в ваш файл ~/.xinitrc и отредактируйте переменную сессий в /etc/slim.conf, соответственно именам ваших сессий. Вы можете выбрать рабочее окружение во времени входа нажав F1.

```
# сессия, которая начнётся если пользователь не выбрал рабочее окружение
DEFAULT_SESSION=twm

case $1 in
kde)
	exec startkde
	;;
xfce4)
	exec startxfce4
	;;
icewm)
	icewmbg &
	icewmtray &
	exec icewm
	;;
wmaker)
	exec wmaker
	;;
blackbox)
	exec blackbox
	;;
*)
	exec $DEFAULT_SESSION
	;;
esac

```

Скачать: [http://svn.berlios.de/svnroot/repos/slim/trunk/xinitrc.sample](http://svn.berlios.de/svnroot/repos/slim/trunk/xinitrc.sample)

Документация Slim: [http://slim.berlios.de/manual.php](http://slim.berlios.de/manual.php)

### Версия ≥1.3.6

**Примечание:** As of version 1.3.6-2 SLiM makes use of `/usr/share/xsessions/` in order to find currently available desktop environments. If you have a prior version of SLiM installed you will have to add this directory as the value of the 'sessiondir' option to your `slim.conf` file. SLiM then passes the appropriate executable to `~/.xinitrc` as an argument. Instead of a case statement, a basic multiple environments setup now only requires the addition of this to `~/.xinitrc`: `exec $1` 

## Темы

Установка тем для Slim:

```
# pacman -S slim-themes archlinux-themes-slim

```

<tt>archlinux-themes-slim</tt> пакеты содержат различные темы.Проверте <tt>/usr/share/slim/themes</tt> чтобы увидеть доступные темы и просмотреть их.

Измените строку current_theme в /etc/slim.conf из "default" на название темы на ваш выбор:

```
# nano /etc/slim.conf

```

```
#current_theme       default
current_theme       archlinux-simplyblack

```

Для предварительного просмотра тем, если не установлен Xorg server, выполните команду:

```
slim -p /usr/share/slim/themes/<theme name>

```

Для того, чтобы закрыть просмотр, наберите "exit" в поле логина и нажмите Enter. Дополнительные пакеты тем могут быть найдены в [AUR](/index.php/AUR "AUR").

# Советы и Хитрости

## Изменение курсора

Если вам не нравится курсор "Х", и вы хотите его изменить, например на стрелку, используйте [slim-cursor пакет из AUR](https://aur.archlinux.org/packages.php?ID=21053).

После установки, отредактируйте / ETC / slim.conf и раскомментируйте строку:

```
cursor   left_ptr

```

Это даст вам нормальную стрелку взамен. Эти настройки сделаны для курсора xsetroot .Вы можете посмотреть доступные курсоры [здесь](http://cvsweb.xfree86.org/cvsweb/*checkout*/xc/lib/X11/cursorfont.h?rev=HEAD&content-type=text/plain) или в /usr/share/icons/<your-cursor-theme>/cursors/.

Для того, чтобы изменять тему курсора на экране входа, добавьте в фаил /usr/share/icons/default/index.theme следующее содержание:

```
[Icon Theme]
Inherits=<your-cursor-theme>

```

Замените <your-cursor-theme> на имя темы курсоров которую вы хотите использовать, например whiteglass.

## Общие темы для Slim и Рабочего Стола

Простой способ обмена темами между Slim и вашим рабочим столом, это создание символической ссылки от вашего файла тем рабочего стола до дефолтной темы в Slim.

```
# mv /usr/share/slim/themes/default/background.jpg /usr/share/slim/themes/default/background.old.jpg
# ln -s /path/to/mywallpaper.jpg /usr/share/slim/themes/default/background.jpg

```

Теперь ваши темы, обои Slim и рабочего стола будут одинаковыми,будет видно сглаживание и переход при загрузке настольной системы. (Вы должны держать дефолтную тему в файле настроек /etc/slim.conf чтобы этот трюк работал)

## Выключение, перезагрузка, режим сна, выход, запуск терминала из SLIM

Вы можете выключать, перезагружать, выходить, и даже запускать терминал с экрана входа SLIM.Для этого введите соответствующее значение в поле имя пользователя и пароля, в поле пароля:

*   Для того, чтобы запускать терминал, введите **console** как имя пользователя(устанавливается по умолчанию на xterm, которое должно настраиваться отдельно.В файле <tt>/etc/slim.conf</tt> можно изменить предпочитаемый терминал)
*   Для выключения, введите **halt** как имя пользователя
*   Для перезагрузки, введите **reboot** как имя пользователя
*   Для выхода, введите **exit** как имя пользователя
*   Для режима сна, введите **suspend** как имя пользователя (Suspend отключён по умолчанию, отредактируйте <tt>/etc/slim.conf</tt> раскомментируйте строку <tt>suspend_cmd</tt> , если необходимо модифицировать приостановить саму команду (e.g. change ***/usr/sbin/suspend*** to ***sudo /usr/sbin/pm-suspend***))

## Ошибка с выключением заставки

Если вы используете заставку и slim,и иногда вы не можете выключить или перезагрузить из меню в gnome, xfce, lxde or others. и т.д Проверьте ваши файлы настроек /etc/slim.conf и /etc/splash.conf, установите DEFAULT_TTY=7 также, как xserver_arguments vt07.

## Информация сесий в Slim

По умолчанию, Slim не регистрирует сесии в utmp и wtmp какие причины, кто, последний раз.. на недостоверную информацию. Чтобы это исправить, отредактируйте ваш slim.conf следующим образом:

```
 sessionstart_cmd    /usr/bin/sessreg -a -l $DISPLAY %user
 sessionstop_cmd     /usr/bin/sessreg -d -l $DISPLAY %user

```

## Настройка DPI в Slim

Если вы установили DPI с аргументом -dpi 96 in /etc/X11/xinit/xserverrc и это не работает со slim. Отредактируйте ваш slim.conf следующим образом:

```
 xserver_arguments   -nolisten tcp vt07 

```

to

```
 xserver_arguments   -nolisten tcp vt07 -dpi 96

```

## Используйте случайные темы

Используйте current_theme переменную как запятую, для разделения списка произвольного набора тем.

## Автомонтирование шифрованной /home при входе в систему

Можете использовать [pam_mount](/index.php/Pam_mount#Slim "Pam mount")

Пример файла /etc/pam.d/slim:

```
 auth            requisite       pam_nologin.so
 auth            required        pam_env.so
 auth            required        pam_unix.so
 auth   required  pam_ecryptfs.so unwrap
 auth            optional        pam_mount.so
 account         required        pam_unix.so
 password  required  pam_ecryptfs.so
 password        required        pam_unix.so
 password        optional        pam_mount.so
 session         required        pam_limits.so
 session         required        pam_unix.so
 session         optional        pam_mount.so
 session         optional        pam_loginuid.so
 session         optional        pam_ck_connector.so

```

**Примечание:** Важно помнить, что в настоящее время нет команды отображения меню в SLIM. Нужно запомнить стандартные команды, перечисленые в ["Выключение, перезагрузка,...."](#.D0.92.D1.8B.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5.2C_.D0.BF.D0.B5.D1.80.D0.B5.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B0.2C_.D1.80.D0.B5.D0.B6.D0.B8.D0.BC_.D1.81.D0.BD.D0.B0.2C_.D0.B2.D1.8B.D1.85.D0.BE.D0.B4.2C_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D1.82.D0.B5.D1.80.D0.BC.D0.B8.D0.BD.D0.B0.D0.BB.D0.B0_.D0.B8.D0.B7_SLIM) и т.д. Эти команды используются в поле Имя пользователя, которое всегда отображается.

# Ссылки

*   [SLiM домашняя страница](http://slim.berlios.de/)