Здесь представлен список графических оболочек для [pacman](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pacman (Русский)"). В список включены полнофункциональные графические интерфейсы, информационные инструмены и различные уведомители для системного трея. Перечень програмного обеспечения разбит на категории в зависимости от использования Gtk или Qt.

**Важно:** Ни одна из представленных ниже программ не поддерживается официальными разработчиками Arch Linux/Pacman.

## Contents

*   [1 Оболочки для Pacman](#.D0.9E.D0.B1.D0.BE.D0.BB.D0.BE.D1.87.D0.BA.D0.B8_.D0.B4.D0.BB.D1.8F_Pacman)
    *   [1.1 X11](#X11)
    *   [1.2 GNOME/GTK+](#GNOME.2FGTK.2B)
    *   [1.3 KDE/Qt](#KDE.2FQt)
    *   [1.4 NCurses](#NCurses)
*   [2 Браузер пакетов Pacman / AUR](#.D0.91.D1.80.D0.B0.D1.83.D0.B7.D0.B5.D1.80_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.BE.D0.B2_Pacman_.2F_AUR)
*   [3 Вывод оповещений в системном трее](#.D0.92.D1.8B.D0.B2.D0.BE.D0.B4_.D0.BE.D0.BF.D0.BE.D0.B2.D0.B5.D1.89.D0.B5.D0.BD.D0.B8.D0.B9_.D0.B2_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D0.BD.D0.BE.D0.BC_.D1.82.D1.80.D0.B5.D0.B5)
*   [4 Неактивные программы](#.D0.9D.D0.B5.D0.B0.D0.BA.D1.82.D0.B8.D0.B2.D0.BD.D1.8B.D0.B5_.D0.BF.D1.80.D0.BE.D0.B3.D1.80.D0.B0.D0.BC.D0.BC.D1.8B)

## Оболочки для Pacman

### X11

*   **PacmanXG4** — Графическая оболочка для pacman. Не требует GTK и QT, только Хorg. Позволяет решать следующие задачи:

*   установка, удаление и обновление пакетов;
*   поиск пакетов / фильтр пакетов;
*   предоставление информации о пакетах, включая скриншоты;
*   откат пакетов (требуется утилита downgrade из AUR);
*   обновление базы данных пакетов, синхронизация зеркал;
*   обновление системы в один клик;
*   поддержка [yaourt](/index.php/Yaourt_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Yaourt (Русский)").

	**Скриншоты:** [http://almin-soft.fsay.net/index.php?pacmanxg/4x-hide/pacmanxg-4x-screenshots](http://almin-soft.fsay.net/index.php?pacmanxg/4x-hide/pacmanxg-4x-screenshots)

	**Прямая ссылка на двоичный файл:** [http://almin-soft.fsay.net/data/files/pacmanxg/download.php?get=pacmanXG4.tar.bz2](http://almin-soft.fsay.net/data/files/pacmanxg/download.php?get=pacmanXG4.tar.bz2)

	[http://almin-soft.fsay.net/](http://almin-soft.fsay.net/) || [pacmanxg4-bin](https://aur.archlinux.org/packages/pacmanxg4-bin/)

### GNOME/GTK+

*   **Wakka** — Основанный на gtk пакетный менеджер для Arch Linux, являющийся продолжением GtkPacman. Цель проекта: почистить код и переработать программу для увеличения стабильности и расширяемости.

	**Скриншоты:** [http://mibloglinux.wordpress.com/2011/05/23/wakka-interfaz-grafica-para-pacman/](http://mibloglinux.wordpress.com/2011/05/23/wakka-interfaz-grafica-para-pacman/)

	[https://code.google.com/p/wakka-package-manager/](https://code.google.com/p/wakka-package-manager/) || [wakka](https://aur.archlinux.org/packages/wakka/)

*   **GNOME PackageKit** — набор утилит для управления пакетами, поддерживающий различные пакетные менеджеры. Использует консольный пакетный менеджер *alpm* и обладает следующим функционалом:

*   установка и удаление пакетов из репозиториев;
*   периодическая синхронизация базы данных пакетов и предложение обновиться;
*   установка пакетов из архивов;
*   поиск пакетов по названию, описанию, категории или файлам;
*   отображение зависимостей пакетов, файлов и обратных зависимостей;
*   игнорирование пакетов из `IgnorePkgs` и "заморозка" с `HoldPkgs`;
*   показ дополнительных зависимостей, файлов *.pacnew* и т.д.

	Вы можете изменить ключ удаления с `-Rc` на `-Rsc`. Для этого следует в *dconf* установить ключ `org.gnome.packagekit.enable-autoremove`

**Tip:** Вместо PulseAudio можно установить из AUR пакет [gnome-settings-daemon-nopulse](https://aur.archlinux.org/packages/gnome-settings-daemon-nopulse/).

	[http://packagekit.org/](http://packagekit.org/) || [gnome-packagekit](https://www.archlinux.org/packages/?name=gnome-packagekit)

### KDE/Qt

*   **KPackageKit/Apper** — графическая оболочка для [PackageKit](http://www.packagekit.org/). Интеграция с pacman осуществляется с пакетом [packagekit](https://www.archlinux.org/packages/?name=packagekit), получившего поддержку со стороны pacman. Из системных настроек KDE, с помощью данного графического инструмента, можно выполнить следующее:

*   установка, удаление и обновление пакетов;
*   поиск пакетов / фильтр пакетов;
*   предоставление информации о пакетах;
*   обновление базы данных пакетов;
*   выбор репозиториев для обновления;
*   автоматическое обновление базы данных (ежечасно, ежедневно и т.д.);
*   автоматическое обновление пакетов.

	Несмотря на то, что pacman поддерживает PackageKit недавно, серьезных проблем замечено не было, при этом обеспечивается простота в использовании и хорошая интеграция с KDE (и PolicyKit).

	**Скриншоты:** [http://kde-apps.org/content/show.php/Apper?content=84745](http://kde-apps.org/content/show.php/Apper?content=84745)

	[http://kde-apps.org/content/show.php/Apper?content=84745](http://kde-apps.org/content/show.php/Apper?content=84745) || [apper](https://aur.archlinux.org/packages/apper/)

*   **AppSet** — современная и функциональная графическая оболочка для пакетных менеджеров. AppSet имеет следующие особенности:

*   сортировка программ по разделам (игры, оффис, мультимедиа, интернет и т.д.);
*   показ во встроенном веб-браузере домашних страниц выбранных пакетов;
*   отображение новостей;
*   обновление, установка и удаление пакетов;
*   иконка в трее для вывода информации о доступных обновлениях;
*   периодическое обновление базы данных;
*   информирование о зависимостях (например, при попытке удаления пакета, который требуется другому пакету);
*   команда очистки кэша (освобождение дискового пространства);
*   умное определение программы для получения администраторских привилегий, т.е. используется установленная в системе kdesu, gksu или, в случае использования xterm, команда sudo);
*   поддержка AUR с помощью бэкэнда Packer.

	AppSet зависит только от библиотеки Qt. Может использоваться в любом окружении. В настоящее время работает только в ArchLinux и только с pacman.

	**Скриншоты** [http://sourceforge.net/project/screenshots.php?group_id=376825](http://sourceforge.net/project/screenshots.php?group_id=376825)

	[http://appset.sourceforge.net/](http://appset.sourceforge.net/) || [appset-qt](https://aur.archlinux.org/packages/appset-qt/)

### NCurses

*   **pcurses** — оболочка к пакетному менеджеру на curses, позволяет:

*   фильтрация и поиск любых пакетов по регулярным выражениям и свойствам.
*   настраиваемая цветовая кодировка.
*   настраиваемая сортировка.
*   выполнение внешних команд.
*   поддержка пользовательских макросов и горячих клавиш.

	**Скриншоты** [https://bbs.archlinux.org/viewtopic.php?id=122749](https://bbs.archlinux.org/viewtopic.php?id=122749)

	[https://github.com/schuay/pcurses](https://github.com/schuay/pcurses) || [pcurses](https://www.archlinux.org/packages/?name=pcurses)

## Браузер пакетов Pacman / AUR

*   **PkgBrowser** — приложение для поиска и просмотра пакетов для Arch, отображает подробную информацию о выбранных пакетах.

*   Поиск и просмотр пакетов для Arch, которые находятся в AUR.
*   Чисто информационное приложение, которое не может быть использовано для установки, удаления и обновления пакетов.
*   По сути относится к CLI-у управления пакетами в pacman.
*   Более подробную информацию по использованию можно получить в меню помощи.

	**Тема на форуме:** [https://bbs.archlinux.org/viewtopic.php?id=117297](https://bbs.archlinux.org/viewtopic.php?id=117297)

	[https://code.google.com/p/pkgbrowser/](https://code.google.com/p/pkgbrowser/) || [pkgbrowser](https://aur.archlinux.org/packages/pkgbrowser/)

*   **Pacinfo** — приложение для просмотра установленных пакетов и отображение такой информации, как скриншоты, установленные файлы, дата установки и прочее. Написано на Mono/GTK#

	[https://code.google.com/p/pacinfo/](https://code.google.com/p/pacinfo/) || [pacinfo](https://aur.archlinux.org/packages/pacinfo/)

## Вывод оповещений в системном трее

*   **Aarchup** — форк archup. Имеет те же возможности, что и archup, плюс некоторые дополнительные. Для поиска различий между ними изучите [changelog](https://bbs.archlinux.org/viewtopic.php?id=119129).

	**Скриншоты**: [http://i.imgur.com/yTNvg.png](http://i.imgur.com/yTNvg.png)

	[https://github.com/aericson/aarchup/](https://github.com/aericson/aarchup/) || [aarchup](https://aur.archlinux.org/packages/aarchup/)

*   **pacman-notifier** — Написан на Ruby, использует Gtk. Отображает иконку в системном трее и, для новых пакетов, всплывающие уведомления (используется libnotify).

	**Скриншоты**: [https://github.com/v01d/pacman-notifier/wiki](https://github.com/v01d/pacman-notifier/wiki)

	[https://github.com/v01d/pacman-notifier/wiki](https://github.com/v01d/pacman-notifier/wiki) || [pacman-notifier](https://aur.archlinux.org/packages/pacman-notifier/)

*   **Pacupdate** — маленькое приложение, уведомляющее пользователя о доступности обновлений для Arch Linux. Если Pacupdate обнаружит, что доступны обновления, будет выведено уведомление в системном трее.

	[https://code.google.com/p/pacupdate/](https://code.google.com/p/pacupdate/) || [pacupdate-svn](https://aur.archlinux.org/packages/pacupdate-svn/)

*   **Yapan (Yet Another Package mAnager Notifier)** — написан на C++ и [Qt](/index.php/Qt_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Qt (Русский)"). Поддерживает другие пакетные менеджеры, такие как *clyde* или [yaourt](/index.php/Yaourt_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Yaourt (Русский)"), отображает значок в системном трее и, при доступности обновлений, показывает соответствующее всплывающее уведомление.

	**Скриншоты**: [https://bitbucket.org/otsug/yapan/wiki/Home](https://bitbucket.org/otsug/yapan/wiki/Home)

	**Тема на форуме**: [https://bbs.archlinux.org/viewtopic.php?id=113078](https://bbs.archlinux.org/viewtopic.php?id=113078)

	[https://bitbucket.org/otsug/yapan/wiki/Home](https://bitbucket.org/otsug/yapan/wiki/Home) || [yapan](https://aur.archlinux.org/packages/yapan/)

*   **ZenMan** — оболочка для PacMan (уведомлялка в трее об обновлениях) для GTK/GNOME/zenity/libnotify.

	**Скриншоты**: [http://show.harvie.cz/screenshots/zenman-screenshot-2.png](http://show.harvie.cz/screenshots/zenman-screenshot-2.png)

	[https://aur.archlinux.org/packages.php?ID=25948](https://aur.archlinux.org/packages.php?ID=25948) || [zenman](https://aur.archlinux.org/packages/zenman/)

*   **pkgnotify.sh** — простой 14-ти строчный скрипт, показывающий количество доступных обновлений в заголовке окна [dzen2](https://www.archlinux.org/packages/?name=dzen2), а список обновлений - во вспомогательном окне. Зависит от [dzen2](https://www.archlinux.org/packages/?name=dzen2), [inotify-tools](https://www.archlinux.org/packages/?name=inotify-tools), [package-query](https://aur.archlinux.org/packages/package-query/) и, опционально, приложения для работы с AUR (по умолчанию *yaourt*).

	**Скриншоты**: [http://andreasbwagner.tumblr.com/post/853471635/arch-linux-update-notifier-for-dzen2](http://andreasbwagner.tumblr.com/post/853471635/arch-linux-update-notifier-for-dzen2)

	[http://pointfree.net/repo/?r=dzen2_scripts;a=headblob;f=/src/pkgnotify/pkgnotify.sh](http://pointfree.net/repo/?r=dzen2_scripts;a=headblob;f=/src/pkgnotify/pkgnotify.sh) || pkgnotify

*   **kalu** — маленькое приложение на C, добавляет иконку в системный трей и выводит уведомления о новостях Arch Linux, обновлениях пакетов из репозиториев, обновлениях пакетов из AUR, и следит за обновлением самого AUR (обновления для неустановленных пакетов). Также имеет графический интерфейс для обновления системы.

	**Скриншоты**: [http://mywaytoarch.tumblr.com/post/19350380240/keep-arch-linux-up-to-date-with-kalu](http://mywaytoarch.tumblr.com/post/19350380240/keep-arch-linux-up-to-date-with-kalu)

	**Тема на форуме**: [https://bbs.archlinux.org/viewtopic.php?id=135773](https://bbs.archlinux.org/viewtopic.php?id=135773)

	[https://bitbucket.org/jjacky/kalu](https://bitbucket.org/jjacky/kalu) || [kalu](https://aur.archlinux.org/packages/kalu/)

## Неактивные программы

*   [pacmanXG 2x series](https://aur.archlinux.org/packages.php?ID=52039/), графическая оболочка для Pacman и *yaourt*, не зависящая от GTK или QT
*   [GtkPacman](http://gtkpacman.berlios.de/), оболочка на GTK
*   [Guzuta](http://guzuta.berlios.de/), оболочка на GTK
*   [Shaman](http://chakra-linux.org/wiki/index.php/Shaman), GUI использующий библиотеку *libalpm* Pacman’а
*   [pacmon](http://code.google.com/p/pacmon/), графические всплывающие уведомления
*   [Paku](https://gna.org/projects/paku/), альтернативный GUI для Pacman
*   [YAPG](http://www.kde-apps.org/content/show.php/YAPG+-+Yet+Another+Pacman+Gui+?content=60052) список GUI на kde-apps.org
*   [zenity_pacgui](http://sourceforge.net/projects/zenitypacgui/), графическая оболочка Zenity для Pacman