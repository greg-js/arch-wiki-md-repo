E17 - это разрабатываемая версия 17 (DR17) [среды рабочего стола](/index.php/Desktop_environment_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Desktop environment (Русский)") [Enlightenment](/index.php/Enlightenment "Enlightenment"), включает в себя менеджер окон Enlightenment и библиотеки Enlightenment Foundation Libraries (EFL), предоставляющие дополнительные функции окружения рабочего стола, такие как набор инструментов, объектное полотно, абстрактные объекты. E17 в разработке с 2005 года, но в феврале 2011 EFL увидели свой первый стабильный 1.0 релиз. Менеджер окон Enlightement всё ещё в стадии бета, но вполне пригоден для использования. Множество людей используют E17 для ежедневной работы без каких-либо проблем.

## Contents

*   [1 Установка E17](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_E17)
    *   [1.1 Из репозитория community (снапшотов SVN)](#.D0.98.D0.B7_.D1.80.D0.B5.D0.BF.D0.BE.D0.B7.D0.B8.D1.82.D0.BE.D1.80.D0.B8.D1.8F_community_.28.D1.81.D0.BD.D0.B0.D0.BF.D1.88.D0.BE.D1.82.D0.BE.D0.B2_SVN.29)
    *   [1.2 Дополнительные пакеты aur](#.D0.94.D0.BE.D0.BF.D0.BE.D0.BB.D0.BD.D0.B8.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D1.8B.D0.B5_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D1.8B_aur)
    *   [1.3 Компиляция и сборка с помощью скрипта ArchE17](#.D0.9A.D0.BE.D0.BC.D0.BF.D0.B8.D0.BB.D1.8F.D1.86.D0.B8.D1.8F_.D0.B8_.D1.81.D0.B1.D0.BE.D1.80.D0.BA.D0.B0_.D1.81_.D0.BF.D0.BE.D0.BC.D0.BE.D1.89.D1.8C.D1.8E_.D1.81.D0.BA.D1.80.D0.B8.D0.BF.D1.82.D0.B0_ArchE17)
    *   [1.4 Компиляция с помощью easy_e17.sh](#.D0.9A.D0.BE.D0.BC.D0.BF.D0.B8.D0.BB.D1.8F.D1.86.D0.B8.D1.8F_.D1.81_.D0.BF.D0.BE.D0.BC.D0.BE.D1.89.D1.8C.D1.8E_easy_e17.sh)
        *   [1.4.1 Update_e17.sh](#Update_e17.sh)
*   [2 Запуск E17](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_E17)
*   [3 Установка тем](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D1.82.D0.B5.D0.BC)
*   [4 Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
*   [5 Ссылки](#.D0.A1.D1.81.D1.8B.D0.BB.D0.BA.D0.B8)

## Установка E17

### Из репозитория community (снапшотов SVN)

*   Устанавливаем "базу" Е17:

```
pacman -S  enlightenment

```

*   Также можно установить эмулятор терминала:

```
pacman -S terminology

```

### Дополнительные пакеты aur

*   [econcentration-git](https://aur.archlinux.org/packages/econcentration-git/) – Карточная игра
*   [ecrire-git](https://aur.archlinux.org/packages/ecrire-git/) – Текстовый редактор
*   [elbow-git](https://aur.archlinux.org/packages/elbow-git/) – Веб браузер
*   [eluminance-git](https://aur.archlinux.org/packages/eluminance-git/) – Браузер фотографий
*   [emprint-git](https://aur.archlinux.org/packages/emprint-git/) – Скриншот инструмент
*   [enjoy-git](https://aur.archlinux.org/packages/enjoy-git/) – [Enjoy](https://trac.enlightenment.org/e/wiki/Enjoy) Музыкальный проигрыватель
*   [epad](https://aur.archlinux.org/packages/epad/) – Текстовый редактор
*   [eperiodique](https://aur.archlinux.org/packages/eperiodique/) – [Eperiodique](http://eperiodique.sourceforge.net/) periodic table viewer
*   [ephoto-git](https://aur.archlinux.org/packages/ephoto-git/) – [Ephoto](https://trac.enlightenment.org/e/wiki/Ephoto) Просмотрщик картинок
*   [epour](https://aur.archlinux.org/packages/epour/) and [epour-git](https://aur.archlinux.org/packages/epour-git/) – Epour Bittorrent клиент
*   [epymc-git](https://aur.archlinux.org/packages/epymc-git/) – E Python Media Center
*   [equate-git](https://aur.archlinux.org/packages/equate-git/) – Equate каркулятор
*   [eruler-git](https://aur.archlinux.org/packages/eruler-git/) – Eruler on-screen ruler and measurement tools
*   [efbb-git](https://aur.archlinux.org/packages/efbb-git/) – Escape from Booty Bay angry birds style game
*   [elemines-git](https://aur.archlinux.org/packages/elemines-git/) – [Elemines](http://elemines.sourceforge.net/) minesweeper style game
*   [espionage-git](https://aur.archlinux.org/packages/espionage-git/) – Espionage D-Bus inspector
*   [ev-git](https://aur.archlinux.org/packages/ev-git/) – ev simple picture viewer
*   [e_cho-git](https://aur.archlinux.org/packages/e_cho-git/) – E_Cho simon style game
*   [e_jeweled-git](https://aur.archlinux.org/packages/e_jeweled-git/) – E_Jeweled bejeweled style game
*   [rage](https://aur.archlinux.org/packages/rage/) and [rage-git](https://aur.archlinux.org/packages/rage-git/) – Rage video player

*   Теперь вы готовы к запуску e17\. Запустить e17 можно разными способами:
    *   Добавьте строку 'enlightenment_start' в файл ~/.xinitrc
    *   Добавьтe 'entranced' (находится в e17-extra-cvs) в список модулей в /etc/rc.conf
    *   Добавьте строку 'x:5:respawn:/usr/sbin/entranced -nodaemon >& /dev/null' в /etc/inittab

Наслаждайтесь!

**Примечание:** e17 - все еще альфа-версия. В будущем может возникнуть ситуация, что среда будет работать некорректно или нестабильно. Хотя все пакеты проверяются прежде, чем добавляются в репозиторий, что-то может работать не так как нужно. Поэтому вы можете сохранить пакеты для предыдущей версии на вашем компьютере, чтобы потом откатиться назад если нужно.

Если вы заметили некоторые странности в поведении программ, есть несколько вещей, которые вы можете сделать. Сначала проверьте, будут ли программы вести себя некорректно с темой, выставленной по умолчани.. Удалите ~/.e (вы можете сделать резервную копию сначала). Если вы уверены, что все-таки нашли ошибку, пожалуйста сообщите об этом непосредственно разработчикам e17\. Если вы не уверены, что это - ошибка в программном обеспечении или в пакете, сообщите об этом в багтрекер репозитория community.

### Компиляция и сборка с помощью скрипта ArchE17

Вы можете собрать свои собственные пакеты E17 для Arch Linux с помощью маленькой программы на питоне, называемой [ArchE17](https://dev.archlinux.org/~ronald/e17.html).

### Компиляция с помощью easy_e17.sh

`easy_e17.sh` компилирует E17 из исходников и устанавливает его в `/opt/e17`. Он не создает пакетов и поэтому не разрешает зависимости автоматически.

1.  Возьмите скрипт из [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)"): [easy-e17](https://aur.archlinux.org/packages/easy-e17/)
2.  Если нужно, отредактируйте `/etc/easy_e17.conf`
3.  Для установки E17 запустите от имени суперпользователя `# easy_e17.sh -i`
4.  Отредактируйте `/etc/profile`, записав `/opt/e17/bin` в список `PATH`. Например, Вы можете добавить такую строку в конце файла: `PATH="$PATH:/opt/e17/bin"`

Если Вы обнаружите какие-нибудь ошибки при попытке установки E17, в первую очередь убедитесь, что это не проблемы, связанные с зависимостями. В противном случае вручную разрешите зависимости и продолжайте установку e17.

Для обновления E17 без использования следующей программы, запустите от имени суперпользователя `# easy_e17.sh -u`.

#### Update_e17.sh

`update_e17.sh` - сделанный на zenity скрипт для работы в связке с `easy_e17.sh`. Он делает проще некоторые моменты, связанные с обновлением e17, поскольку может сохранять и восстанавливать Вашу svn-ветку E17 (в случае повреждения), а также откатиться назад на указанную версию (опять же, в случае повреждения) или даже сообщить Вам о появлении новой версии в svn-ветке E17\. Дополнительная информация об этом необязательном компоненте находится [на этой странице](http://cafelinux.org/OzOs/content/how-administer-your-ozos-e17-desktop). Скрипт можно взять в [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)"): [oz-e17-tools](https://aur.archlinux.org/packages/oz-e17-tools/).

## Запуск E17

Если Вы используете *startx* или простой [экранный менеджер](/index.php/%D0%AD%D0%BA%D1%80%D0%B0%D0%BD%D0%BD%D1%8B%D0%B9_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80 "Экранный менеджер"), такой как XDM или [SLiM](/index.php/SLiM_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "SLiM (Русский)"), добавьте или раскомментируйте следующую строку в [xinitrc](/index.php/Xinitrc_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xinitrc (Русский)"):

```
exec enlightenment_start

```

Более продвинутые экранные менеджеры, такие как [GDM](/index.php/GDM "GDM") и KDM автоматически обнаружат E17 благодаря файлу `/usr/share/xsessions/enlightenment.desktop` из пакета `e-svn`.

## Установка тем

Много тем можно найти на [exchange.enlightenment.org](http://exchange.enlightenment.org/). И на [e17-stuff.org](http://www.e17-stuff.org).

Вы можете установить тему (имеют формат .edj) из конфигурационных диалогов.

You can also change the theme for the etk toolkit (the one which is used by exhibit). You can start the dialog to change the etk toolkit by starting /usr/bin/etk_prefs

## Решение проблем

*   Если курсоры иксов не доступны или неправильно отображаются, установите 'libxcursor'.
*   Если не работает переключение раскладки клавиатуры ни через Х-ы, ни через HAL, то можно воспользоваться следующим вариантом:

```
# vim ~/bin/set_us-ru_kbd
  #!/bin/sh
  setxkbmap -layout us,ru -option grp:lctrl_lshift_toggle,grp_led:scroll -variant winkeys
# chmod +x ~/bin/set_us-ru_kbd

```

*   Если шрифты очень маленькие и не читаемые на вашем экране или же по другим причинам, то установите следующие пакеты:

```
pacman -S ttf-dejavu ttf-bitstream-vera

```

## Ссылки

*   [Exchange.enlightenment.org](http://exchange.enlightenment.org/)
*   [Gentoo e17 Howto](http://gentoo-wiki.com/HOWTO_emerge_e17);
*   [Рекомендуемые приложения](http://archux.com/page/application-recommendations)
*   [Установка и настройка E17](http://archux.com/page/installing-and-setting-e17)