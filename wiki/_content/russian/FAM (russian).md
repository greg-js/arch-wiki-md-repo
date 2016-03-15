FAM (File Alteration Monitor) — монитор изменения файлов. Демон FAM используется окружениями рабочего стола, такими как [GNOME](/index.php/GNOME_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GNOME (Русский)") и [Xfce](/index.php/Xfce "Xfce") для отслеживания и отображения изменений, вносимых в файловую систему. [KDE](/index.php/KDE "KDE") использует встроенную в ядро подсистему inotify.

Например, FAM используется для:

*   автоматического обновления меню приложений, когда новое приложение установлено
*   обновления файлового менеджера, когда содержимое отображаемой директории изменяется

**Важно:** Демон FAM устарел, и, если возможно, вместо него следует использовать [Gamin](/index.php/Gamin_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Gamin (Русский)"). Gamin более новый и активно поддерживаемый проект, совместимый с FAM и заменяющий его в большинстве случаев.

### Установка

FAM считается устаревшим и был удален из официального репозитория. Однако, вы можете установить [FAM](https://aur.archlinux.org/packages.php?ID=52058) из [Arch User Repository (Русский)](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)") (AUR).

### Конфигурация

Предоставлен демон `fam.service`, см. [systemd (Русский)](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd (Русский)").

## Смотрите также

*   [File alteration monitor](https://en.wikipedia.org/wiki/File_alteration_monitor "wikipedia:File alteration monitor")

*   [FAM, Gamin, inotify](http://www.noah.org/wiki/FAM,_Gamin,_inotify)