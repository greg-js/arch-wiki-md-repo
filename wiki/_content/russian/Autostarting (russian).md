**Состояние перевода:** На этой странице представлен перевод статьи [Autostarting](/index.php/Autostarting "Autostarting"). Дата последней синхронизации: 10 октября 2015\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Autostarting&diff=0&oldid=400561).

Эта статья ссылается на различные методы автоматического запуска сценариев и приложений, когда происходит некоторое конкретное событие, такое как, например, включении или выключении компьютера со входом или выходом из оболочки.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Демоны](#Демоны)
    *   [1.1 Systemd](#Systemd)
*   [2 Cron](#Cron)
*   [3 inotify](#inotify)
*   [4 Коммандные оболочки](#Коммандные_оболочки)
    *   [4.1 /etc/profile](#/etc/profile)
*   [5 Графический](#Графический)
    *   [5.1 Запуск сеанса X](#Запуск_сеанса_X)
    *   [5.2 Desktop entries](#Desktop_entries)
    *   [5.3 GNOME](#GNOME)
    *   [5.4 KDE Plasma](#KDE_Plasma)
    *   [5.5 Xfce](#Xfce)
    *   [5.6 LXDE](#LXDE)
    *   [5.7 LXQt](#LXQt)
    *   [5.8 Fluxbox](#Fluxbox)
    *   [5.9 Openbox](#Openbox)

## Демоны

Вы можете запускать сценарии или приложения, как демоны, см. [демоны](/index.php/Daemon_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Daemon (Русский)").

### Systemd

*Systemd* является базой инициализации по умолчанию, заменяя сценарии инициализации (initscripts). Службы, которые созданы *systemd* могут быть найдены в подпапках `/etc/systemd/system/`. Службы могут быть включены с помощью команды `systemctl`. Для получения более подробной информации о *systemd* и о том, как писать сценарии для автозапуска, смотрите [Systemd](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd (Русский)"). Для автозапуска скриптов, для конкретных пользователей см [systemd/User](/index.php/Systemd/User "Systemd/User").

## Cron

[Cron](/index.php/Cron "Cron") can be used to autostart non-GUI system setup tasks.

## inotify

[inotify-tools](https://www.archlinux.org/packages/?name=inotify-tools) может быть использован для выполнения команд или скриптов по событиям [inotify](https://en.wikipedia.org/wiki/ru:inotify "wikipedia:ru:inotify"), вызванным изменениями файловой системы. Вы можете посмотреть [некоторые примеры](https://techarena51.com/index.php/inotify-tools-example/).

## Коммандные оболочки

Для автозапуска программ в консоли или при входе, Вы можете использовать оболочку для запуска файлов/каталогов. Прочитайте документацию для вашей оболочки, или статью ArchWiki, например [Bash#Configuration files](/index.php/Bash#Configuration_files "Bash") или [Zsh#Автозапуск приложений](/index.php/Zsh_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Автозапуск_приложений "Zsh (Русский)").

Смотрите также [Wikipedia:Unix shell#Configuration files for shells](https://en.wikipedia.org/wiki/Unix_shell#Configuration_files_for_shells "wikipedia:Unix shell").

### /etc/profile

После входа в систему, все Bourne-совместимые исходные оболочки `/etc/profile`, в свою очередь читают любые файлы `*.sh` в `/etc/profile.d/`: эти сценарии не требуют директивы интерпретатора, и они не должны быть исполняемыми. Они используются для настройки среды и определяют настройки для конкретных приложений.

## Графический

Вы можете запускать программы автоматически, когда входите в ваш [Оконный Менеджер](/index.php/Window_manager_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Window manager (Русский)") или [Окружение Рабочего Стола](/index.php/Desktop_environment_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Desktop environment (Русский)").

### Запуск сеанса X

Смотрите [xinitrc](/index.php/Xinitrc_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xinitrc (Русский)") и [xprofile](/index.php/Xprofile_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xprofile (Русский)").

### Desktop entries

Смотрите[Desktop entries#Autostart](/index.php/Desktop_entries#Autostart "Desktop entries").

### GNOME

Смотрите [GNOME (Русский)#Автоматический запуск программ при входе в систему](/index.php/GNOME_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Автоматический_запуск_программ_при_входе_в_систему "GNOME (Русский)").

### KDE Plasma

Смотрите [KDE#Autostarting applications](/index.php/KDE#Autostarting_applications "KDE").

### Xfce

Смотрите [Xfce (Русский)#Автозапуск приложений](/index.php/Xfce_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Автозапуск_приложений "Xfce (Русский)").

### LXDE

Смотрите [LXDE (Русский)#Автозапуск программ](/index.php/LXDE_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Автозапуск_программ "LXDE (Русский)").

### LXQt

Смотрите [LXQt#Autostarting applications](/index.php/LXQt#Autostarting_applications "LXQt").

### Fluxbox

Смотрите [Fluxbox (Русский)#Автозапуск программ](/index.php/Fluxbox_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Автозапуск_программ "Fluxbox (Русский)").

### Openbox

Смотрите [Openbox (Русский)#Автозапуск приложений](/index.php/Openbox_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Автозапуск_приложений "Openbox (Русский)").