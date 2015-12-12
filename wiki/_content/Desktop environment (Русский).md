# Desktop environment (Русский)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Ссылки по теме

*   [Экранный менеджер](/index.php/%D0%AD%D0%BA%D1%80%D0%B0%D0%BD%D0%BD%D1%8B%D0%B9_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80 "Экранный менеджер")
*   [Оконный менеджер](/index.php/%D0%9E%D0%BA%D0%BE%D0%BD%D0%BD%D1%8B%D0%B9_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80 "Оконный менеджер")
*   [Xorg (Русский)](/index.php/Xorg_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xorg (Русский)")
*   [Default applications](/index.php/Default_applications "Default applications")

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

**Эта страница нуждается в сопроводителе**

Статья не гарантирует актуальность информации. Помогите русскоязычному сообществу поддержкой подобных страниц. См. [Команда переводчиков ArchWiki](/index.php/%D0%9A%D0%BE%D0%BC%D0%B0%D0%BD%D0%B4%D0%B0_%D0%BF%D0%B5%D1%80%D0%B5%D0%B2%D0%BE%D0%B4%D1%87%D0%B8%D0%BA%D0%BE%D0%B2_ArchWiki "Команда переводчиков ArchWiki")

[Среда рабочего стола](https://en.wikipedia.org/wiki/ru:%D0%A1%D1%80%D0%B5%D0%B4%D0%B0_%D1%80%D0%B0%D0%B1%D0%BE%D1%87%D0%B5%D0%B3%D0%BE_%D1%81%D1%82%D0%BE%D0%BB%D0%B0 "wikipedia:ru:Среда рабочего стола") предоставляет полнофункциональное графическое окружение для системы, включающее набор графических приложений, утилит и компонентов рабочего стола. Как правило, среды рабочего стола базируются на одном из графических тулкитов, таких как [GTK+](/index.php/GTK%2B "GTK+") или [Qt](/index.php/Qt_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Qt (Русский)").

## Contents

*   [1 Обзор](#.D0.9E.D0.B1.D0.B7.D0.BE.D1.80)
*   [2 Список сред рабочего стола](#.D0.A1.D0.BF.D0.B8.D1.81.D0.BE.D0.BA_.D1.81.D1.80.D0.B5.D0.B4_.D1.80.D0.B0.D0.B1.D0.BE.D1.87.D0.B5.D0.B3.D0.BE_.D1.81.D1.82.D0.BE.D0.BB.D0.B0)
    *   [2.1 Официально поддерживаемые](#.D0.9E.D1.84.D0.B8.D1.86.D0.B8.D0.B0.D0.BB.D1.8C.D0.BD.D0.BE_.D0.BF.D0.BE.D0.B4.D0.B4.D0.B5.D1.80.D0.B6.D0.B8.D0.B2.D0.B0.D0.B5.D0.BC.D1.8B.D0.B5)
    *   [2.2 Неофициально поддерживаемые](#.D0.9D.D0.B5.D0.BE.D1.84.D0.B8.D1.86.D0.B8.D0.B0.D0.BB.D1.8C.D0.BD.D0.BE_.D0.BF.D0.BE.D0.B4.D0.B4.D0.B5.D1.80.D0.B6.D0.B8.D0.B2.D0.B0.D0.B5.D0.BC.D1.8B.D0.B5)
*   [3 Сравнение сред рабочего стола](#.D0.A1.D1.80.D0.B0.D0.B2.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D1.81.D1.80.D0.B5.D0.B4_.D1.80.D0.B0.D0.B1.D0.BE.D1.87.D0.B5.D0.B3.D0.BE_.D1.81.D1.82.D0.BE.D0.BB.D0.B0)
    *   [3.1 Потребление ресурсов](#.D0.9F.D0.BE.D1.82.D1.80.D0.B5.D0.B1.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D1.80.D0.B5.D1.81.D1.83.D1.80.D1.81.D0.BE.D0.B2)
    *   [3.2 Схожесть окружений](#.D0.A1.D1.85.D0.BE.D0.B6.D0.B5.D1.81.D1.82.D1.8C_.D0.BE.D0.BA.D1.80.D1.83.D0.B6.D0.B5.D0.BD.D0.B8.D0.B9)
*   [4 Создание своей среды](#.D0.A1.D0.BE.D0.B7.D0.B4.D0.B0.D0.BD.D0.B8.D0.B5_.D1.81.D0.B2.D0.BE.D0.B5.D0.B9_.D1.81.D1.80.D0.B5.D0.B4.D1.8B)

## Обзор

Кроме стандартных компонентов рабочего стола, большинство сред включают в себя интегрированный набор программ. Также среды рабочего стола предоставляют свой собственный [оконный менеджер](/index.php/%D0%9E%D0%BA%D0%BE%D0%BD%D0%BD%D1%8B%D0%B9_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80 "Оконный менеджер"), который обычно можно заменить альтернативным вариантом из совместимых.

Пользователю дается возможность настраивать графический интерфейс разными путями. Как правило, среды рабочего стола предоставляют графические средства настройки.

Пользователи могут одновременно запускать приложения, написанные для разных сред. Например, в KDE можно запускать приложения GNOME. Так, вы можете заменить стандартный веб-браузер KDE — Konqueror на Epiphany, если он вам больше нравится. Однако, такой подход имеет и недостаток: многие графические приложения тесно связаны с тем или иным набором библиотек, которые входят в состав "родной" среды. В результате установка множества "неродных" приложений потребует установки большего количества зависимостей. Пользователям, которые экономят место на диске, следует избегать установки [раздутых](https://en.wikipedia.org/wiki/ru:%D0%A0%D0%B0%D0%B7%D0%B4%D1%83%D1%82%D0%BE%D0%B5_%D0%BF%D1%80%D0%BE%D0%B3%D1%80%D0%B0%D0%BC%D0%BC%D0%BD%D0%BE%D0%B5_%D0%BE%D0%B1%D0%B5%D1%81%D0%BF%D0%B5%D1%87%D0%B5%D0%BD%D0%B8%D0%B5 "wikipedia:ru:Раздутое программное обеспечение") программ, написанных для других сред.

Кроме того, обычно приложения в родной среде выглядят более единообразно и лучше в нее интегрируются. Приложения, написанные с использованием разных библиотек компонентов интерфейса могут выглядеть по-разному (использовать разные наборы иконок, стиль оформления компонентов и т. д.) и по-разному себя вести (например, может не работать перетаскивание мышью).

Перед установкой среды рабочего стола необходимо установить, и, возможно, настроить сервер X. Подробнее об этом смотрите на странице [Xorg](/index.php/Xorg_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xorg (Русский)").

## Список сред рабочего стола

### Официально поддерживаемые

*   **[Cinnamon](/index.php/Cinnamon_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Cinnamon (Русский)")** — стремится предоставить пользователю более привычную, традиционную среду в стиле GNOME 2, но с использованием технологий GNOME 3.

[http://cinnamon.linuxmint.com/](http://cinnamon.linuxmint.com/) || [cinnamon](https://www.archlinux.org/packages/?name=cinnamon)

*   **[Enlightenment](/index.php/E17_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "E17 (Русский)")** — предоставляет эффективный менеджер окон, основанный на библиотеках Enlightenment Foundation. Его можно запускать на устаревших компьютерах и встраиваемых устройствах, при этом существует поддержка тем, значков рабочего стола и виджетов, а также встроенный файловый менеджер.

[http://www.enlightenment.org/](http://www.enlightenment.org/) || [enlightenment](https://www.archlinux.org/packages/?name=enlightenment)

*   **[GNOME](/index.php/GNOME_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GNOME (Русский)")** — популярная и интуитивная среда рабочего стола, которая включает современный (_GNOME_) и классический (_GNOME Classic_) режимы.

[http://www.gnome.org/gnome-3/](http://www.gnome.org/gnome-3/) || [gnome](https://www.archlinux.org/groups/x86_64/gnome/)

*   **[KDE](/index.php/KDE_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "KDE (Русский)")** — предоставляет большое количество встроенных приложений, а также гибкий в настройке рабочий стол в качестве оболочки. Эти приложения могут быть запущены и в других средах, но KDE обеспечивает наилучшую интеграцию с ними.

[http://www.kde.org/](http://www.kde.org/) || KDE 4: [kdebase](https://www.archlinux.org/groups/x86_64/kdebase/), KDE 5: [plasma-next](https://www.archlinux.org/groups/x86_64/plasma-next/)<sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): package not found]</sup>

*   **[LXDE](/index.php/LXDE_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "LXDE (Русский)")** — облегченная среда рабочего стола для X11 — быстрая и легкая среда, созданная сообществом разработчиков со всего мира. Она предлагает современный интерфейс, поддержку языков и стандартные сочетания клавиш. При этом LXDE старается тратить как можно меньше ресурсов компьютера и обеспечивать минимальное энергопотребление.

[http://lxde.org/](http://lxde.org/) || [lxde](https://www.archlinux.org/groups/x86_64/lxde/)

*   **[MATE](/index.php/MATE_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "MATE (Русский)")** — предоставляет интуитивный традиционный рабочий стол для пользователей Linux. Mate — форк GNOME 2.

[http://www.mate-desktop.org/](http://www.mate-desktop.org/) || [mate](https://www.archlinux.org/groups/x86_64/mate/)

*   **[Xfce](/index.php/Xfce_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xfce (Русский)")** — следует традиционной философии UNIX, основываясь на принципах модульности и повторного использования. Он состоит из множества компонентов, которые составляют полноценное современное рабочее окружение, при этом оставаясь относительно легким. Эти компоненты распределены по разным пакетам, поэтому вы можете выбирать какие из них вам нужны.

[http://www.xfce.org/](http://www.xfce.org/) || [xfce4](https://www.archlinux.org/groups/x86_64/xfce4/)

### Неофициально поддерживаемые

*   **[Budgie Desktop](/index.php/Budgie_Desktop "Budgie Desktop")** — легкая и современных среда рабочего стола, направленная на простоту и элегантность. По внешнему виду напоминает рабочий стол Chrome/Chromium OS.

[https://evolve-os.com/budgie/](https://evolve-os.com/budgie/) || [budgie-desktop-git](https://aur.archlinux.org/packages/budgie-desktop-git/)<sup><small>AUR</small></sup>

*   **[Deepin Desktop Environment](/index.php/Deepin_Desktop_Environment "Deepin Desktop Environment")** — стандартная среда рабочего стола дистрибутива Linux Deepin. По сути является измененной оболочкой GNOME Shell

[http://www.linuxdeepin.com/](http://www.linuxdeepin.com/) || [deepin-desktop-environment](https://aur.archlinux.org/packages/deepin-desktop-environment/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/deepin-desktop-environment)]</sup>

*   **[EDE](/index.php/Equinox_Desktop_Environment "Equinox Desktop Environment")** — рабочий стол, созданный быть простым, исключительно легким и быстрым.

[http://equinox-project.org/](http://equinox-project.org/) || [ede](https://aur.archlinux.org/packages/ede/)<sup><small>AUR</small></sup>

*   **[GNOME Flashback](/index.php/GNOME_Flashback "GNOME Flashback")** — оболочка для GNOME 3, которая изначально использовалась в нем для режима совместимости. Рабочий стол и технологии аналогичны GNOME 2.

[https://wiki.gnome.org/GnomeFlashback](https://wiki.gnome.org/GnomeFlashback) || [gnome-flashback](https://www.archlinux.org/packages/?name=gnome-flashback)

*   **GNUstep** — свободная объектно-ориентированная кросс-платформенная среда разработки, которая стремится к простоте и элегантности.

[http://gnustep.org/](http://gnustep.org/) || [windowmaker](https://www.archlinux.org/packages/?name=windowmaker) [gworkspace](https://aur.archlinux.org/packages/gworkspace/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/gworkspace)]</sup>

*   **[Hawaii](/index.php/Hawaii "Hawaii")** — легкое, последовательное и быстрое окружение на основе Qt 5, QtQuick и [Wayland](/index.php/Wayland_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Wayland (Русский)"), и созданное с целью предложить удобный интерфейс независимо от устройства, на котором запущено.

[http://www.maui-project.org/](http://www.maui-project.org/) || [hawaii-meta-git](https://aur.archlinux.org/packages/hawaii-meta-git/)<sup><small>AUR</small></sup>

*   **[LXQt](/index.php/Razor-qt_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Razor-qt (Русский)")** — порт LXDE на Qt. Рабочее окружение LXQt позиционируется как легковесное, быстрое и удобное, имеющее модульную архитектуру и продолжающее развитие LXDE и Razor-qt, вобрав в себя лучшие черты обеих оболочек.

[http://lxqt.org/](http://lxqt.org/) || [lxqt](https://www.archlinux.org/groups/x86_64/lxqt/)

*   **Maynard** — среда рабочего стола, разработанная для [Raspberry Pi](/index.php/Raspberry_Pi "Raspberry Pi") (но им не ограничивающаяся), работающая на [Wayland](/index.php/Wayland_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Wayland (Русский)").

[https://github.com/raspberrypi/maynard](https://github.com/raspberrypi/maynard) || [maynard-git](https://aur.archlinux.org/packages/maynard-git/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/maynard-git)]</sup>

*   **[Pantheon](/index.php/Pantheon "Pantheon")** — среда, созданная для дистрибутива elementary OS. Написана с нуля на основе тулкитов Vala и GTK3\. Рабочий стол построен с упором на удобство и внешний вид и напоминает собой GNOME Shell и Mac OS X.

[http://elementaryos.org/](http://elementaryos.org/) || [pantheon-session-bzr](https://aur.archlinux.org/packages/pantheon-session-bzr/)<sup><small>AUR</small></sup>

*   **[ROX](/index.php/ROX "ROX")** — быстрый и удобный рабочий стол, в котором сделан упор на возможности все и везде перетаскивать мышью (drag-&-drop). Интерфейс обращается вокруг файлового менеджера, который строго следует принципу UNIX "все является файлом". Цель проекта — сделать систему, которая хорошо спроектирована и четко представлена. Подход ROX — использовать множество небольших приложений вместе, чем создавать комбайны "все-в-одном".

[http://rox.sourceforge.net/desktop/](http://rox.sourceforge.net/desktop/) || [rox](https://www.archlinux.org/packages/?name=rox)

*   **[Sugar](/index.php/Sugar "Sugar")** — The Sugar Learning Platform — окружение, состоящее из набора мультимедийных программ, разработанных для помощи в обучении детям 5-12 лет. Sugar направлен на то, чтобы предоставить детям по всему миру возможность получить качественное образование.

[http://wiki.sugarlabs.org/](http://wiki.sugarlabs.org/) || [sugar](https://aur.archlinux.org/packages/sugar/)<sup><small>AUR</small></sup>

*   **[Trinity](/index.php/Trinity "Trinity")** — среда рабочего стола, являющаяся ответвлением от кодовой базы неподдерживаемой в настоящее время среды KDE 3.

[http://www.trinitydesktop.org/](http://www.trinitydesktop.org/) || Смотрите [Trinity](/index.php/Trinity "Trinity")

*   **[Unity](/index.php/Unity "Unity")** — оболочка для GNOME, разработанная Canonical для Ubuntu.

[http://unity.ubuntu.com/](http://unity.ubuntu.com/) || [unity](https://aur.archlinux.org/packages/unity/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/unity)]</sup>

## Сравнение сред рабочего стола

_В этом разделе приведена сравнительная таблица с популярными средами рабочего стола. Помните, что получение личного опыта использования — единственный эффективный способ определить, какая среда рабочего стола вам лучше всего подходит._

Смотрите также страницу [Wikipedia:Comparison of X Window System desktop environments](https://en.wikipedia.org/wiki/Comparison_of_X_Window_System_desktop_environments "wikipedia:Comparison of X Window System desktop environments").

<table class="wikitable"><caption>Обзор сред рабочего стола</caption>

<tbody>

<tr>

<th>Среда рабочего стола</th>

<th>Графический тулкит</th>

<th>Оконный менеджер</th>

<th>Панель задач</th>

<th>Эмулятор терминала</th>

<th>Файловый менеджер</th>

<th>Калькулятор</th>

<th>Текстовый редактор</th>

<th>Просмотр изображений</th>

<th>Плеер</th>

<th>Браузер</th>

<th>Менеджер входа</th>

</tr>

<tr>

<td>[Budgie Desktop](/index.php/Budgie_Desktop "Budgie Desktop")</td>

<td>[GTK+](/index.php/GTK%2B "GTK+") 3  
[gtk3](https://www.archlinux.org/packages/?name=gtk3)</td>

<td>budgie-wm  
[budgie-desktop-git](https://aur.archlinux.org/packages/budgie-desktop-git/)<sup><small>AUR</small></sup></td>

<td>budgie-panel  
[budgie-desktop-git](https://aur.archlinux.org/packages/budgie-desktop-git/)<sup><small>AUR</small></sup></td>

<td>[GNOME Terminal](https://en.wikipedia.org/wiki/GNOME_Terminal "wikipedia:GNOME Terminal")  
[gnome-terminal](https://www.archlinux.org/packages/?name=gnome-terminal)</td>

<td>[GNOME Files](/index.php/GNOME_Files "GNOME Files")  
[nautilus](https://www.archlinux.org/packages/?name=nautilus)</td>

<td>[GNOME Calculator](https://en.wikipedia.org/wiki/GNOME_Calculator "wikipedia:GNOME Calculator")  
[gnome-calculator](https://www.archlinux.org/packages/?name=gnome-calculator)</td>

<td>[gedit](/index.php/Gedit "Gedit")  
[gedit](https://www.archlinux.org/packages/?name=gedit)</td>

<td>[Eye of GNOME](https://en.wikipedia.org/wiki/Eye_of_GNOME "wikipedia:Eye of GNOME")  
[eog](https://www.archlinux.org/packages/?name=eog)</td>

<td>[Budgie Media Player](https://github.com/evolve-os/budgie-media-player)  
[budgie-git](https://aur.archlinux.org/packages/budgie-git/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/budgie-git)]</sup></td>

<td>[Chromium](/index.php/Chromium "Chromium")  
[chromium](https://www.archlinux.org/packages/?name=chromium)</td>

<td>[GDM](/index.php/GDM "GDM")  
[gdm](https://www.archlinux.org/packages/?name=gdm)</td>

</tr>

<tr>

<td>[Cinnamon](/index.php/Cinnamon "Cinnamon")</td>

<td>[GTK+](/index.php/GTK%2B "GTK+") 3  
[gtk3](https://www.archlinux.org/packages/?name=gtk3)</td>

<td>Muffin  
[muffin](https://www.archlinux.org/packages/?name=muffin)</td>

<td>Cinnamon  
[cinnamon](https://www.archlinux.org/packages/?name=cinnamon)</td>

<td>[GNOME Terminal](https://en.wikipedia.org/wiki/GNOME_Terminal "wikipedia:GNOME Terminal")  
[gnome-terminal](https://www.archlinux.org/packages/?name=gnome-terminal)</td>

<td>[Nemo](/index.php/Nemo "Nemo")  
[nemo](https://www.archlinux.org/packages/?name=nemo)</td>

<td>[GNOME Calculator](https://en.wikipedia.org/wiki/GNOME_Calculator "wikipedia:GNOME Calculator")  
[gnome-calculator](https://www.archlinux.org/packages/?name=gnome-calculator)</td>

<td>[gedit](/index.php/Gedit "Gedit")  
[gedit](https://www.archlinux.org/packages/?name=gedit)</td>

<td>[Eye of GNOME](https://en.wikipedia.org/wiki/Eye_of_GNOME "wikipedia:Eye of GNOME")  
[eog](https://www.archlinux.org/packages/?name=eog)</td>

<td>[Totem](https://en.wikipedia.org/wiki/Totem_(software) "wikipedia:Totem (software)")  
[totem](https://www.archlinux.org/packages/?name=totem)</td>

<td>[Firefox](/index.php/Firefox "Firefox")  
[firefox](https://www.archlinux.org/packages/?name=firefox)</td>

<td>[LightDM](/index.php/LightDM "LightDM") GTK+ Greeter  
[lightdm-gtk3-greeter](https://www.archlinux.org/packages/?name=lightdm-gtk3-greeter)<sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): replaced by [lightdm-gtk-greeter](https://www.archlinux.org/packages/?name=lightdm-gtk-greeter)]</sup></td>

</tr>

<tr>

<td>[Deepin Desktop Environment](/index.php/Deepin_Desktop_Environment "Deepin Desktop Environment")</td>

<td>[GTK+](/index.php/GTK%2B "GTK+") 3  
[gtk3](https://www.archlinux.org/packages/?name=gtk3)</td>

<td>[Compiz](/index.php/Compiz "Compiz")  
[compiz](https://aur.archlinux.org/packages/compiz/)<sup><small>AUR</small></sup></td>

<td>Dock  
[deepin-desktop-environment](https://aur.archlinux.org/packages/deepin-desktop-environment/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/deepin-desktop-environment)]</sup></td>

<td>Deepin Terminal  
[deepin-terminal](https://www.archlinux.org/packages/?name=deepin-terminal)</td>

<td>[GNOME Files](/index.php/GNOME_Files "GNOME Files")  
[nautilus](https://www.archlinux.org/packages/?name=nautilus)</td>

<td>[GNOME Calculator](https://en.wikipedia.org/wiki/GNOME_Calculator "wikipedia:GNOME Calculator")  
[gnome-calculator](https://www.archlinux.org/packages/?name=gnome-calculator)</td>

<td>[gedit](/index.php/Gedit "Gedit")  
[gedit](https://www.archlinux.org/packages/?name=gedit)</td>

<td>[Eye of GNOME](https://en.wikipedia.org/wiki/Eye_of_GNOME "wikipedia:Eye of GNOME")  
[eog](https://www.archlinux.org/packages/?name=eog)</td>

<td>DPlayer  
[deepin-media-player](https://aur.archlinux.org/packages/deepin-media-player/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/deepin-media-player)]</sup></td>

<td>[Firefox](/index.php/Firefox "Firefox")  
[firefox](https://www.archlinux.org/packages/?name=firefox)</td>

<td>[LightDM](/index.php/LightDM "LightDM") Deepin Greeter  
[deepin-desktop-environment](https://aur.archlinux.org/packages/deepin-desktop-environment/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/deepin-desktop-environment)]</sup></td>

</tr>

<tr>

<td>[EDE](/index.php/Equinox_Desktop_Environment "Equinox Desktop Environment")</td>

<td>[FLTK](http://www.fltk.org/)  
[fltk](https://www.archlinux.org/packages/?name=fltk)</td>

<td>[PekWM](/index.php/PekWM "PekWM")  
[ede](https://aur.archlinux.org/packages/ede/)<sup><small>AUR</small></sup></td>

<td>EDE Panel  
[ede](https://aur.archlinux.org/packages/ede/)<sup><small>AUR</small></sup></td>

<td>[XTerm](/index.php/Xterm "Xterm")  
[xterm](https://www.archlinux.org/packages/?name=xterm)</td>

<td>Fluff  
[fluff](https://aur.archlinux.org/packages/fluff/)<sup><small>AUR</small></sup></td>

<td>Calculator  
[ede](https://aur.archlinux.org/packages/ede/)<sup><small>AUR</small></sup></td>

<td>Editor  
[fltk-editor](https://aur.archlinux.org/packages/fltk-editor/)<sup><small>AUR</small></sup></td>

<td>Image Viewer  
[ede](https://aur.archlinux.org/packages/ede/)<sup><small>AUR</small></sup></td>

<td>flmusic  
[flmusic](https://aur.archlinux.org/packages/flmusic/)<sup><small>AUR</small></sup></td>

<td>[Dillo](/index.php/Dillo "Dillo")  
[dillo](https://www.archlinux.org/packages/?name=dillo)</td>

<td>[XDM](/index.php/XDM "XDM")  
[xorg-xdm](https://www.archlinux.org/packages/?name=xorg-xdm)</td>

</tr>

<tr>

<td>[Enlightenment](/index.php/Enlightenment "Enlightenment")</td>

<td>[Elementary](https://phab.enlightenment.org/w/elementary/)  
[elementary](https://www.archlinux.org/packages/?name=elementary)</td>

<td>Enlightenment  
[enlightenment](https://www.archlinux.org/packages/?name=enlightenment)</td>

<td>Enlightenment  
[enlightenment](https://www.archlinux.org/packages/?name=enlightenment)</td>

<td>[Terminology](http://www.enlightenment.org/p.php?p=about/terminology)  
[terminology](https://www.archlinux.org/packages/?name=terminology)</td>

<td>[EFM](https://phab.enlightenment.org/w/efm/)  
[enlightenment](https://www.archlinux.org/packages/?name=enlightenment)</td>

<td>Equate  
[equate-git](https://aur.archlinux.org/packages/equate-git/)<sup><small>AUR</small></sup></td>

<td>Ecrire  
[ecrire-git](https://aur.archlinux.org/packages/ecrire-git/)<sup><small>AUR</small></sup></td>

<td>[Ephoto](https://trac.enlightenment.org/e/wiki/Ephoto)  
[ephoto-git](https://aur.archlinux.org/packages/ephoto-git/)<sup><small>AUR</small></sup></td>

<td>[Rage](http://www.enlightenment.org/p.php?p=about/rage)  
[rage](https://aur.archlinux.org/packages/rage/)<sup><small>AUR</small></sup></td>

<td>Elbow  
[elbow-git](https://aur.archlinux.org/packages/elbow-git/)<sup><small>AUR</small></sup></td>

<td>[XDM](/index.php/XDM "XDM")  
[xorg-xdm](https://www.archlinux.org/packages/?name=xorg-xdm)</td>

</tr>

<tr>

<td>[GNOME](/index.php/GNOME "GNOME")</td>

<td>[GTK+](/index.php/GTK%2B "GTK+") 3  
[gtk3](https://www.archlinux.org/packages/?name=gtk3)</td>

<td>[Mutter](https://en.wikipedia.org/wiki/Mutter_(window_manager) "wikipedia:Mutter (window manager)")  
[mutter](https://www.archlinux.org/packages/?name=mutter)</td>

<td>[GNOME Shell](https://en.wikipedia.org/wiki/GNOME_Shell "wikipedia:GNOME Shell")  
[gnome-shell](https://www.archlinux.org/packages/?name=gnome-shell)</td>

<td>[GNOME Terminal](https://en.wikipedia.org/wiki/GNOME_Terminal "wikipedia:GNOME Terminal")  
[gnome-terminal](https://www.archlinux.org/packages/?name=gnome-terminal)</td>

<td>[GNOME Files](/index.php/GNOME_Files "GNOME Files")  
[nautilus](https://www.archlinux.org/packages/?name=nautilus)</td>

<td>[GNOME Calculator](https://en.wikipedia.org/wiki/GNOME_Calculator "wikipedia:GNOME Calculator")  
[gnome-calculator](https://www.archlinux.org/packages/?name=gnome-calculator)</td>

<td>[gedit](/index.php/Gedit "Gedit")  
[gedit](https://www.archlinux.org/packages/?name=gedit)</td>

<td>[Eye of GNOME](https://en.wikipedia.org/wiki/Eye_of_GNOME "wikipedia:Eye of GNOME")  
[eog](https://www.archlinux.org/packages/?name=eog)</td>

<td>[Totem](https://en.wikipedia.org/wiki/Totem_(software) "wikipedia:Totem (software)")  
[totem](https://www.archlinux.org/packages/?name=totem)</td>

<td>[Epiphany](/index.php/Epiphany "Epiphany")  
[epiphany](https://www.archlinux.org/packages/?name=epiphany)</td>

<td>[GDM](/index.php/GDM "GDM")  
[gdm](https://www.archlinux.org/packages/?name=gdm)</td>

</tr>

<tr>

<td>[GNOME Flashback](/index.php/GNOME_Flashback "GNOME Flashback")</td>

<td>[GTK+](/index.php/GTK%2B "GTK+") 3  
[gtk3](https://www.archlinux.org/packages/?name=gtk3)</td>

<td>[Metacity](https://en.wikipedia.org/wiki/Metacity "wikipedia:Metacity")  
[metacity](https://www.archlinux.org/packages/?name=metacity)</td>

<td>[GNOME Panel](https://en.wikipedia.org/wiki/GNOME_Panel "wikipedia:GNOME Panel")  
[gnome-panel](https://www.archlinux.org/packages/?name=gnome-panel)</td>

<td>[GNOME Terminal](https://en.wikipedia.org/wiki/GNOME_Terminal "wikipedia:GNOME Terminal")  
[gnome-terminal](https://www.archlinux.org/packages/?name=gnome-terminal)</td>

<td>[GNOME Files](/index.php/GNOME_Files "GNOME Files")  
[nautilus](https://www.archlinux.org/packages/?name=nautilus)</td>

<td>[GNOME Calculator](https://en.wikipedia.org/wiki/GNOME_Calculator "wikipedia:GNOME Calculator")  
[gnome-calculator](https://www.archlinux.org/packages/?name=gnome-calculator)</td>

<td>[gedit](/index.php/Gedit "Gedit")  
[gedit](https://www.archlinux.org/packages/?name=gedit)</td>

<td>[Eye of GNOME](https://en.wikipedia.org/wiki/Eye_of_GNOME "wikipedia:Eye of GNOME")  
[eog](https://www.archlinux.org/packages/?name=eog)</td>

<td>[Totem](https://en.wikipedia.org/wiki/Totem_(software) "wikipedia:Totem (software)")  
[totem](https://www.archlinux.org/packages/?name=totem)</td>

<td>[Epiphany](/index.php/Epiphany "Epiphany")  
[epiphany](https://www.archlinux.org/packages/?name=epiphany)</td>

<td>[GDM](/index.php/GDM "GDM")  
[gdm](https://www.archlinux.org/packages/?name=gdm)</td>

</tr>

<tr>

<td>GNUstep</td>

<td>[GNUstep](http://gnustep.org/)  
[gnustep-core](https://www.archlinux.org/groups/x86_64/gnustep-core/)</td>

<td>[Window Maker](/index.php/Window_Maker "Window Maker")  
[windowmaker](https://www.archlinux.org/packages/?name=windowmaker)</td>

<td>[Window Maker](/index.php/Window_Maker "Window Maker")  
[windowmaker](https://www.archlinux.org/packages/?name=windowmaker)</td>

<td>[Terminal](http://gap.nongnu.org/terminal/index.html)  
[gnustep-terminal](https://aur.archlinux.org/packages/gnustep-terminal/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/gnustep-terminal)]</sup></td>

<td>[GWorkspace](http://www.gnustep.org/experience/GWorkspace.html)  
[gworkspace](https://aur.archlinux.org/packages/gworkspace/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/gworkspace)]</sup></td>

<td>[Calculator](http://www.gnustep.org/experience/examples.html)  
[gnustep-examples](https://aur.archlinux.org/packages/gnustep-examples/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/gnustep-examples)]</sup></td>

<td>[Ink](http://www.gnustep.org/experience/examples.html)  
[gnustep-examples](https://aur.archlinux.org/packages/gnustep-examples/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/gnustep-examples)]</sup></td>

<td>[LaternaMagica](http://gap.nongnu.org/laternamagica/index.html)  
[laternamagica](https://aur.archlinux.org/packages/laternamagica/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/laternamagica)]</sup></td>

<td>[Cynthiune](http://gap.nongnu.org/cynthiune/index.html)  
[cynthiune](https://aur.archlinux.org/packages/cynthiune/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/cynthiune)]</sup></td>

<td>[SWK Browser](http://wiki.gnustep.org/index.php/SimpleWebKit)  
[swkbrowser-svn](https://aur.archlinux.org/packages/swkbrowser-svn/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/swkbrowser-svn)]</sup></td>

<td>[XDM](/index.php/XDM "XDM")  
[xorg-xdm](https://www.archlinux.org/packages/?name=xorg-xdm)</td>

</tr>

<tr>

<td>[Hawaii](/index.php/Hawaii "Hawaii")</td>

<td>[Qt](/index.php/Qt "Qt") 5  
[qt5-base](https://www.archlinux.org/packages/?name=qt5-base)</td>

<td>Weston  
[weston](https://www.archlinux.org/packages/?name=weston)</td>

<td>Hawaii Shell  
[hawaii-shell-git](https://aur.archlinux.org/packages/hawaii-shell-git/)<sup><small>AUR</small></sup></td>

<td>Terminal  
[hawaii-terminal-git](https://aur.archlinux.org/packages/hawaii-terminal-git/)<sup><small>AUR</small></sup></td>

<td>Swordfish  
[swordfish-git](https://aur.archlinux.org/packages/swordfish-git/)<sup><small>AUR</small></sup></td>

<td>[SpeedCrunch](http://speedcrunch.org/)  
[speedcrunch-git](https://aur.archlinux.org/packages/speedcrunch-git/)<sup><small>AUR</small></sup></td>

<td>JuffEd  
[juffed-git](https://aur.archlinux.org/packages/juffed-git/)<sup><small>AUR</small></sup></td>

<td>EyeSight  
[eyesight-git](https://aur.archlinux.org/packages/eyesight-git/)<sup><small>AUR</small></sup></td>

<td>SMPlayer  
[smplayer](https://www.archlinux.org/packages/?name=smplayer)</td>

<td>QupZilla  
[qupzilla](https://www.archlinux.org/packages/?name=qupzilla)</td>

<td>-</td>

</tr>

<tr>

<td>[KDE](/index.php/KDE "KDE") 4</td>

<td>[Qt](/index.php/Qt "Qt") 4  
[qt4](https://www.archlinux.org/packages/?name=qt4)</td>

<td>[KWin](https://en.wikipedia.org/wiki/KWin "wikipedia:KWin")  
[kdebase-workspace](https://www.archlinux.org/packages/?name=kdebase-workspace)</td>

<td>[Plasma Desktop](https://en.wikipedia.org/wiki/KDE_Plasma_4#Desktop "wikipedia:KDE Plasma 4")  
[kdebase-workspace](https://www.archlinux.org/packages/?name=kdebase-workspace)</td>

<td>[Konsole](http://konsole.kde.org/)  
[kdebase-konsole](https://www.archlinux.org/packages/?name=kdebase-konsole)<sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): replaced by [konsole](https://www.archlinux.org/packages/?name=konsole)]</sup></td>

<td>[Dolphin](http://dolphin.kde.org/)  
[kdebase-dolphin](https://www.archlinux.org/packages/?name=kdebase-dolphin)<sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): replaced by [dolphin](https://www.archlinux.org/packages/?name=dolphin)]</sup></td>

<td>[KCalc](http://www.kde.org/applications/utilities/kcalc/)  
[kdeutils-kcalc](https://www.archlinux.org/packages/?name=kdeutils-kcalc)<sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): replaced by [kcalc](https://www.archlinux.org/packages/?name=kcalc)]</sup></td>

<td>[KWrite/Kate](http://kate-editor.org/)  
[kdebase-kwrite](https://www.archlinux.org/packages/?name=kdebase-kwrite)<sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): replaced by [kwrite](https://www.archlinux.org/packages/?name=kwrite)]</sup> [kdesdk-kate](https://www.archlinux.org/packages/?name=kdesdk-kate)<sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): replaced by [kate](https://www.archlinux.org/packages/?name=kate)]</sup></td>

<td>[Gwenview](http://gwenview.sourceforge.net/)  
[kdegraphics-gwenview](https://www.archlinux.org/packages/?name=kdegraphics-gwenview)<sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): replaced by [gwenview](https://www.archlinux.org/packages/?name=gwenview)]</sup></td>

<td>[Dragon Player](http://www.kde.org/applications/multimedia/dragonplayer/)  
[kdemultimedia-dragonplayer](https://www.archlinux.org/packages/?name=kdemultimedia-dragonplayer)<sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): replaced by [dragon](https://www.archlinux.org/packages/?name=dragon)]</sup></td>

<td>[Konqueror](http://www.konqueror.org/)  
[kdebase-konqueror](https://www.archlinux.org/packages/?name=kdebase-konqueror)</td>

<td>[KDM](/index.php/KDM "KDM")  
[kdebase-workspace](https://www.archlinux.org/packages/?name=kdebase-workspace)</td>

</tr>

<tr>

<td>[KDE](/index.php/KDE "KDE") 5</td>

<td>[Qt](/index.php/Qt "Qt") 4/5  
[qt4](https://www.archlinux.org/packages/?name=qt4) [qt5-base](https://www.archlinux.org/packages/?name=qt5-base)</td>

<td>[KWin](https://en.wikipedia.org/wiki/KWin "wikipedia:KWin")  
[kwin](https://www.archlinux.org/packages/?name=kwin)</td>

<td>[Plasma Desktop](https://en.wikipedia.org/wiki/KDE_Plasma_5#Desktop "wikipedia:KDE Plasma 5")  
[plasma-desktop](https://www.archlinux.org/packages/?name=plasma-desktop)</td>

<td>[Konsole](http://konsole.kde.org/)  
[kdebase-konsole](https://www.archlinux.org/packages/?name=kdebase-konsole)<sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): replaced by [konsole](https://www.archlinux.org/packages/?name=konsole)]</sup></td>

<td>[Dolphin](http://dolphin.kde.org/)  
[kdebase-dolphin](https://www.archlinux.org/packages/?name=kdebase-dolphin)<sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): replaced by [dolphin](https://www.archlinux.org/packages/?name=dolphin)]</sup></td>

<td>[KCalc](http://www.kde.org/applications/utilities/kcalc/)  
[kdeutils-kcalc](https://www.archlinux.org/packages/?name=kdeutils-kcalc)<sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): replaced by [kcalc](https://www.archlinux.org/packages/?name=kcalc)]</sup></td>

<td>[KWrite/Kate](http://kate-editor.org/)  
[kdebase-kwrite](https://www.archlinux.org/packages/?name=kdebase-kwrite)<sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): replaced by [kwrite](https://www.archlinux.org/packages/?name=kwrite)]</sup> [kdesdk-kate](https://www.archlinux.org/packages/?name=kdesdk-kate)<sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): replaced by [kate](https://www.archlinux.org/packages/?name=kate)]</sup></td>

<td>[Gwenview](http://gwenview.sourceforge.net/)  
[kdegraphics-gwenview](https://www.archlinux.org/packages/?name=kdegraphics-gwenview)<sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): replaced by [gwenview](https://www.archlinux.org/packages/?name=gwenview)]</sup></td>

<td>[Dragon Player](http://www.kde.org/applications/multimedia/dragonplayer/)  
[kdemultimedia-dragonplayer](https://www.archlinux.org/packages/?name=kdemultimedia-dragonplayer)<sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): replaced by [dragon](https://www.archlinux.org/packages/?name=dragon)]</sup></td>

<td>[Konqueror](http://www.konqueror.org/)  
[kdebase-konqueror](https://www.archlinux.org/packages/?name=kdebase-konqueror)</td>

<td>SDDM  
[sddm](https://www.archlinux.org/packages/?name=sddm)</td>

</tr>

<tr>

<td>[LXDE](/index.php/LXDE "LXDE")</td>

<td>[GTK+](/index.php/GTK%2B "GTK+") 2  
[gtk2](https://www.archlinux.org/packages/?name=gtk2)</td>

<td>[Openbox](/index.php/Openbox "Openbox")  
[openbox](https://www.archlinux.org/packages/?name=openbox)</td>

<td>[LXPanel](http://wiki.lxde.org/en/LXPanel)  
[lxpanel](https://www.archlinux.org/packages/?name=lxpanel)</td>

<td>[LXTerminal](http://wiki.lxde.org/en/LXTerminal)  
[lxterminal](https://www.archlinux.org/packages/?name=lxterminal)</td>

<td>[PCManFM](/index.php/PCManFM "PCManFM")  
[pcmanfm](https://www.archlinux.org/packages/?name=pcmanfm)</td>

<td>[Galculator](http://galculator.sourceforge.net/)  
[galculator-gtk2](https://www.archlinux.org/packages/?name=galculator-gtk2)</td>

<td>[Leafpad](http://tarot.freeshell.org/leafpad/)  
[leafpad](https://www.archlinux.org/packages/?name=leafpad)</td>

<td>[GPicView](http://wiki.lxde.org/en/GPicView)  
[gpicview](https://www.archlinux.org/packages/?name=gpicview)</td>

<td>[LXMusic](http://wiki.lxde.org/en/LXMusic)  
[lxmusic](https://www.archlinux.org/packages/?name=lxmusic)</td>

<td>[Firefox](/index.php/Firefox "Firefox")  
[firefox](https://www.archlinux.org/packages/?name=firefox)</td>

<td>[LXDM](/index.php/LXDM "LXDM")  
[lxdm](https://www.archlinux.org/packages/?name=lxdm)</td>

</tr>

<tr>

<td>[LXQt](/index.php/LXQt "LXQt")</td>

<td>[Qt](/index.php/Qt "Qt") 5  
[qt5-base](https://www.archlinux.org/packages/?name=qt5-base)</td>

<td>[Openbox](/index.php/Openbox "Openbox")  
[openbox](https://www.archlinux.org/packages/?name=openbox)</td>

<td>LXQt Panel  
[lxqt-panel](https://www.archlinux.org/packages/?name=lxqt-panel)</td>

<td>QTerminal  
[qterminal](https://aur.archlinux.org/packages/qterminal/)<sup><small>AUR</small></sup></td>

<td>PCManFM-Qt  
[pcmanfm-qt](https://www.archlinux.org/packages/?name=pcmanfm-qt)</td>

<td>[SpeedCrunch](http://speedcrunch.org/)  
[speedcrunch-git](https://aur.archlinux.org/packages/speedcrunch-git/)<sup><small>AUR</small></sup></td>

<td>JuffEd  
[juffed-git](https://aur.archlinux.org/packages/juffed-git/)<sup><small>AUR</small></sup></td>

<td>LxImage-Qt  
[lximage-qt](https://aur.archlinux.org/packages/lximage-qt/)<sup><small>AUR</small></sup></td>

<td>SMPlayer  
[smplayer](https://www.archlinux.org/packages/?name=smplayer)</td>

<td>QupZilla  
[qupzilla](https://www.archlinux.org/packages/?name=qupzilla)</td>

<td>SDDM  
[sddm](https://www.archlinux.org/packages/?name=sddm)</td>

</tr>

<tr>

<td>[MATE](/index.php/MATE "MATE")</td>

<td>[GTK+](/index.php/GTK%2B "GTK+") 2  
[gtk2](https://www.archlinux.org/packages/?name=gtk2)</td>

<td>Marco  
[marco](https://www.archlinux.org/packages/?name=marco)</td>

<td>MATE Panel  
[mate-panel](https://www.archlinux.org/packages/?name=mate-panel)</td>

<td>MATE Terminal  
[mate-terminal](https://www.archlinux.org/packages/?name=mate-terminal)</td>

<td>Caja  
[caja](https://www.archlinux.org/packages/?name=caja)</td>

<td>[Galculator](http://galculator.sourceforge.net/)  
[galculator-gtk2](https://www.archlinux.org/packages/?name=galculator-gtk2)</td>

<td>pluma  
[pluma](https://www.archlinux.org/packages/?name=pluma)</td>

<td>Eye of MATE  
[eom](https://www.archlinux.org/packages/?name=eom)</td>

<td>Whaaw!  
[whaawmp](https://www.archlinux.org/packages/?name=whaawmp)</td>

<td>[Midori](/index.php/Midori "Midori")  
[midori](https://www.archlinux.org/packages/?name=midori)</td>

<td>[LightDM](/index.php/LightDM "LightDM") GTK+ Greeter  
[lightdm-gtk2-greeter](https://aur.archlinux.org/packages/lightdm-gtk2-greeter/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): replaced by [lightdm-gtk-greeter](https://www.archlinux.org/packages/?name=lightdm-gtk-greeter)]</sup></td>

</tr>

<tr>

<td>Maynard</td>

<td>[GTK+](/index.php/GTK%2B "GTK+") 3  
[gtk3](https://www.archlinux.org/packages/?name=gtk3)</td>

<td>Weston  
[weston](https://www.archlinux.org/packages/?name=weston)</td>

<td>Maynard  
[maynard-git](https://aur.archlinux.org/packages/maynard-git/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/maynard-git)]</sup></td>

<td>[GNOME Terminal](https://en.wikipedia.org/wiki/GNOME_Terminal "wikipedia:GNOME Terminal")  
[gnome-terminal](https://www.archlinux.org/packages/?name=gnome-terminal)</td>

<td>[GNOME Files](/index.php/GNOME_Files "GNOME Files")  
[nautilus](https://www.archlinux.org/packages/?name=nautilus)</td>

<td>[GNOME Calculator](https://en.wikipedia.org/wiki/GNOME_Calculator "wikipedia:GNOME Calculator")  
[gnome-calculator](https://www.archlinux.org/packages/?name=gnome-calculator)</td>

<td>[gedit](/index.php/Gedit "Gedit")  
[gedit](https://www.archlinux.org/packages/?name=gedit)</td>

<td>[Eye of GNOME](https://en.wikipedia.org/wiki/Eye_of_GNOME "wikipedia:Eye of GNOME")  
[eog](https://www.archlinux.org/packages/?name=eog)</td>

<td>[Totem](https://en.wikipedia.org/wiki/Totem_(software) "wikipedia:Totem (software)")  
[totem](https://www.archlinux.org/packages/?name=totem)</td>

<td>[Epiphany](/index.php/Epiphany "Epiphany")  
[epiphany](https://www.archlinux.org/packages/?name=epiphany)</td>

<td>-</td>

</tr>

<tr>

<td>[Pantheon](/index.php/Pantheon "Pantheon")</td>

<td>[GTK+](/index.php/GTK%2B "GTK+") 3  
[gtk3](https://www.archlinux.org/packages/?name=gtk3)</td>

<td>[Gala](https://launchpad.net/gala)  
[gala-bzr](https://aur.archlinux.org/packages/gala-bzr/)<sup><small>AUR</small></sup></td>

<td>[Plank](https://launchpad.net/plank)/[Wingpanel](https://launchpad.net/wingpanel)  
[plank](https://www.archlinux.org/packages/?name=plank) [wingpanel](https://aur.archlinux.org/packages/wingpanel/)<sup><small>AUR</small></sup></td>

<td>[Pantheon Terminal](https://launchpad.net/pantheon-terminal)  
[pantheon-terminal](https://www.archlinux.org/packages/?name=pantheon-terminal)</td>

<td>[Pantheon Files](https://launchpad.net/pantheon-files)  
[pantheon-files](https://www.archlinux.org/packages/?name=pantheon-files)</td>

<td>[GNOME Calculator](https://en.wikipedia.org/wiki/GNOME_Calculator "wikipedia:GNOME Calculator")  
[gnome-calculator](https://www.archlinux.org/packages/?name=gnome-calculator)</td>

<td>[Scratch](https://launchpad.net/scratch)  
[scratch-text-editor](https://www.archlinux.org/packages/?name=scratch-text-editor)</td>

<td>[Shotwell](https://en.wikipedia.org/wiki/Shotwell_(software) "wikipedia:Shotwell (software)")  
[shotwell](https://www.archlinux.org/packages/?name=shotwell)</td>

<td>[Totem](https://en.wikipedia.org/wiki/Totem_(software) "wikipedia:Totem (software)")  
[totem](https://www.archlinux.org/packages/?name=totem)</td>

<td>[Midori](/index.php/Midori "Midori")  
[midori-gtk3](https://www.archlinux.org/packages/?name=midori-gtk3)<sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): replaced by [midori](https://www.archlinux.org/packages/?name=midori)]</sup></td>

<td>[LightDM](/index.php/LightDM "LightDM") Pantheon Greeter  
[lightdm-pantheon-greeter](https://aur.archlinux.org/packages/lightdm-pantheon-greeter/)<sup><small>AUR</small></sup></td>

</tr>

<tr>

<td>[ROX](/index.php/ROX "ROX")</td>

<td>[GTK+](/index.php/GTK%2B "GTK+") 2  
[gtk2](https://www.archlinux.org/packages/?name=gtk2)</td>

<td>[OroboROX](http://rox.sourceforge.net/desktop/OroboROX.html)  
[oroborox](https://aur.archlinux.org/packages/oroborox/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/oroborox)]</sup></td>

<td>[ROX-Filer](http://rox.sourceforge.net/desktop/ROX-Filer.html)  
[rox](https://www.archlinux.org/packages/?name=rox)</td>

<td>[ROXTerm](http://roxterm.sourceforge.net/)  
[roxterm-gtk2](https://aur.archlinux.org/packages/roxterm-gtk2/)<sup><small>AUR</small></sup></td>

<td>[ROX-Filer](http://rox.sourceforge.net/desktop/ROX-Filer.html)  
[rox](https://www.archlinux.org/packages/?name=rox)</td>

<td>[Galculator](http://galculator.sourceforge.net/)  
[galculator-gtk2](https://www.archlinux.org/packages/?name=galculator-gtk2)</td>

<td>[Edit](http://rox.sourceforge.net/desktop/Edit.html)  
[rox-edit](https://aur.archlinux.org/packages/rox-edit/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/rox-edit)]</sup></td>

<td>[Picky](http://rox.sourceforge.net/desktop/picky.html)  
<small>not packaged? [search in AUR](https://aur.archlinux.org/packages/?K=picky)</small></td>

<td>[MusicBox](http://rox.sourceforge.net/desktop/Software/Audio_Video/MusicBox.html)  
<small>not packaged? [search in AUR](https://aur.archlinux.org/packages/?K=musicbox)</small></td>

<td>[Midori](/index.php/Midori "Midori")  
[midori](https://www.archlinux.org/packages/?name=midori)</td>

<td>[LightDM](/index.php/LightDM "LightDM") GTK+ Greeter  
[lightdm-gtk2-greeter](https://aur.archlinux.org/packages/lightdm-gtk2-greeter/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): replaced by [lightdm-gtk-greeter](https://www.archlinux.org/packages/?name=lightdm-gtk-greeter)]</sup></td>

</tr>

<tr>

<td>[Sugar](/index.php/Sugar "Sugar")</td>

<td>[GTK+](/index.php/GTK%2B "GTK+") 3  
[gtk3](https://www.archlinux.org/packages/?name=gtk3)</td>

<td>[Metacity](https://en.wikipedia.org/wiki/Metacity "wikipedia:Metacity")  
[metacity](https://www.archlinux.org/packages/?name=metacity)</td>

<td>Sugar  
[sugar](https://aur.archlinux.org/packages/sugar/)<sup><small>AUR</small></sup></td>

<td>Terminal  
[sugar-activity-terminal](https://aur.archlinux.org/packages/sugar-activity-terminal/)<sup><small>AUR</small></sup></td>

<td>Sugar Journal  
[sugar](https://aur.archlinux.org/packages/sugar/)<sup><small>AUR</small></sup></td>

<td>Calculate  
[sugar-activity-calculate](https://aur.archlinux.org/packages/sugar-activity-calculate/)<sup><small>AUR</small></sup></td>

<td>Write  
[sugar-activity-write](https://aur.archlinux.org/packages/sugar-activity-write/)<sup><small>AUR</small></sup></td>

<td>ImageViewer  
[sugar-activity-imageviewer](https://aur.archlinux.org/packages/sugar-activity-imageviewer/)<sup><small>AUR</small></sup></td>

<td>Jukebox  
[sugar-activity-jukebox](https://aur.archlinux.org/packages/sugar-activity-jukebox/)<sup><small>AUR</small></sup></td>

<td>Browse  
[sugar-activity-browse](https://aur.archlinux.org/packages/sugar-activity-browse/)<sup><small>AUR</small></sup></td>

<td>[LightDM](/index.php/LightDM "LightDM") GTK+ Greeter  
[lightdm-gtk3-greeter](https://www.archlinux.org/packages/?name=lightdm-gtk3-greeter)<sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): replaced by [lightdm-gtk-greeter](https://www.archlinux.org/packages/?name=lightdm-gtk-greeter)]</sup></td>

</tr>

<tr>

<td>[Trinity](/index.php/Trinity "Trinity")</td>

<td>[Qt](/index.php/Qt "Qt") 3</td>

<td>TWin</td>

<td>Kicker</td>

<td>Konsole</td>

<td>Konqueror</td>

<td>KCalc</td>

<td>Kwrite / Kate</td>

<td>Kuickshow</td>

<td>Kaffeine</td>

<td>Konqueror</td>

<td>TDM</td>

</tr>

<tr>

<td>[Unity](/index.php/Unity "Unity")</td>

<td>[GTK+](/index.php/GTK%2B "GTK+") 3  
[gtk3](https://www.archlinux.org/packages/?name=gtk3)</td>

<td>[Compiz](/index.php/Compiz "Compiz")  
[compiz-ubuntu](https://aur.archlinux.org/packages/compiz-ubuntu/)<sup><small>AUR</small></sup></td>

<td>Unity  
[unity](https://aur.archlinux.org/packages/unity/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/unity)]</sup></td>

<td>[GNOME Terminal](https://en.wikipedia.org/wiki/GNOME_Terminal "wikipedia:GNOME Terminal")  
[gnome-terminal](https://www.archlinux.org/packages/?name=gnome-terminal)</td>

<td>[GNOME Files](/index.php/GNOME_Files "GNOME Files")  
[nautilus-ubuntu](https://aur.archlinux.org/packages/nautilus-ubuntu/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/nautilus-ubuntu)]</sup></td>

<td>[GNOME Calculator](https://en.wikipedia.org/wiki/GNOME_Calculator "wikipedia:GNOME Calculator")  
[gnome-calculator](https://www.archlinux.org/packages/?name=gnome-calculator)</td>

<td>[gedit](/index.php/Gedit "Gedit")  
[gedit](https://www.archlinux.org/packages/?name=gedit)</td>

<td>[Eye of GNOME](https://en.wikipedia.org/wiki/Eye_of_GNOME "wikipedia:Eye of GNOME")  
[eog](https://www.archlinux.org/packages/?name=eog)</td>

<td>[Totem](https://en.wikipedia.org/wiki/Totem_(software) "wikipedia:Totem (software)")  
[totem](https://www.archlinux.org/packages/?name=totem)</td>

<td>[Firefox](/index.php/Firefox "Firefox")  
[firefox](https://www.archlinux.org/packages/?name=firefox)</td>

<td>[LightDM](/index.php/LightDM "LightDM") Unity Greeter  
[lightdm-unity-greeter](https://aur.archlinux.org/packages/lightdm-unity-greeter/)<sup><small>AUR</small></sup></td>

</tr>

<tr>

<td>[Xfce](/index.php/Xfce "Xfce")</td>

<td>[GTK+](/index.php/GTK%2B "GTK+") 2  
[gtk2](https://www.archlinux.org/packages/?name=gtk2)</td>

<td>[Xfwm4](http://docs.xfce.org/xfce/xfwm4/start)  
[xfwm4](https://www.archlinux.org/packages/?name=xfwm4)</td>

<td>[Xfce Panel](http://docs.xfce.org/xfce/xfce4-panel/start)  
[xfce4-panel](https://www.archlinux.org/packages/?name=xfce4-panel)</td>

<td>[Terminal](http://www.xfce.org/projects/terminal)  
[xfce4-terminal](https://www.archlinux.org/packages/?name=xfce4-terminal)</td>

<td>[Thunar](/index.php/Thunar "Thunar")  
[thunar](https://www.archlinux.org/packages/?name=thunar)</td>

<td>[Galculator](http://galculator.sourceforge.net/)  
[galculator-gtk2](https://www.archlinux.org/packages/?name=galculator-gtk2)</td>

<td>Mousepad  
[mousepad](https://www.archlinux.org/packages/?name=mousepad)</td>

<td>[Ristretto](http://goodies.xfce.org/projects/applications/ristretto)  
[ristretto](https://www.archlinux.org/packages/?name=ristretto)</td>

<td>[Parole](http://goodies.xfce.org/projects/applications/parole)  
[parole](https://www.archlinux.org/packages/?name=parole)</td>

<td>[Midori](/index.php/Midori "Midori")  
[midori](https://www.archlinux.org/packages/?name=midori)</td>

<td>[LightDM](/index.php/LightDM "LightDM") GTK+ Greeter  
[lightdm-gtk2-greeter](https://aur.archlinux.org/packages/lightdm-gtk2-greeter/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): replaced by [lightdm-gtk-greeter](https://www.archlinux.org/packages/?name=lightdm-gtk-greeter)]</sup></td>

</tr>

</tbody>

</table>

### Потребление ресурсов

Среди всех окружений рабочего стола, GNOME и KDE наиболее требовательны к ресурсам компьютера. Полные версии этих сред не только занимают больше места на диске чем более легкие альтернативы (Enlightenment, LXDE, LXQt и Xfce), но также требуют больше процессорного времени и оперативной памяти для работы. Все дело в том, что GNOME и KDE позиционируют тебя как полнофункциональные (_full-featured_) среды: они предоставляют наиболее полное и интегрированное окружение рабочего стола.

Enlightenment, LXDE, LXQt и Xfce, напротив, являются легковесными (_lightweight_) средами. Они хорошо работают на более старом оборудовании и в общем потребляют меньше системных ресурсов. Это достигается отказом от возможностей, которые могут быть полезны только небольшому количеству пользователей, и концентрацией на действительно важной функциональности.

### Схожесть окружений

Многие пользователи отмечают, что интерфейс KDE во многом похож на окружение Windows, а GNOME ближе к системам Mac. Это достаточно субъективное сравнение, так как любая из этих сред может быть настроена чтобы в той или иной степени эмулировать интерфейсы Windows или Mac. Читайте подробнее на страницах [Больше ли KDE похож на Windows, чем GNOME?](http://www.psychocats.net/ubuntucat/is-kde-more-windows-like-than-gnome/) и [KDE против GNOME](http://www.jeffwu.net/?p=71). Также обратите внимание на статью [Linux — не Windows](http://linux.oneandoneis2.org/LNW.htm).

## Создание своей среды

Установка среды рабочего стола представляет собой наиболее простой и быстрый способ получить полноценное рабочее окружение. Однако, если вас не устраивает ни одна из предлагаемых сред, вы можете собрать свое собственное окружение. В общих чертах, создание своего окружения включает в себя выбор подходящего [оконного менеджера](/index.php/Window_manager_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Window manager (Русский)"), [панели задач](/index.php/%D0%A1%D0%BF%D0%B8%D1%81%D0%BE%D0%BA_%D0%BF%D1%80%D0%B8%D0%BB%D0%BE%D0%B6%D0%B5%D0%BD%D0%B8%D0%B9#.D0.9F.D0.B0.D0.BD.D0.B5.D0.BB.D0.B8_.D0.B7.D0.B0.D0.B4.D0.B0.D1.87_.2F_.D0.B4.D0.BE.D0.BA.D0.B8 "Список приложений") и набора программ (как минимум, пригодятся [эмулятор терминала](/index.php/%D0%A1%D0%BF%D0%B8%D1%81%D0%BE%D0%BA_%D0%BF%D1%80%D0%B8%D0%BB%D0%BE%D0%B6%D0%B5%D0%BD%D0%B8%D0%B9#.D0.AD.D0.BC.D1.83.D0.BB.D1.8F.D1.82.D0.BE.D1.80.D1.8B_.D1.82.D0.B5.D1.80.D0.BC.D0.B8.D0.BD.D0.B0.D0.BB.D0.B0 "Список приложений"), [файловый менеджер](/index.php/%D0%A1%D0%BF%D0%B8%D1%81%D0%BE%D0%BA_%D0%BF%D1%80%D0%B8%D0%BB%D0%BE%D0%B6%D0%B5%D0%BD%D0%B8%D0%B9#.D0.A4.D0.B0.D0.B9.D0.BB.D0.BE.D0.B2.D1.8B.D0.B5_.D0.BC.D0.B5.D0.BD.D0.B5.D0.B4.D0.B6.D0.B5.D1.80.D1.8B "Список приложений"), и [текстовый редактор](/index.php/%D0%A1%D0%BF%D0%B8%D1%81%D0%BE%D0%BA_%D0%BF%D1%80%D0%B8%D0%BB%D0%BE%D0%B6%D0%B5%D0%BD%D0%B8%D0%B9#.D0.A2.D0.B5.D0.BA.D1.81.D1.82.D0.BE.D0.B2.D1.8B.D0.B5_.D1.80.D0.B5.D0.B4.D0.B0.D0.BA.D1.82.D0.BE.D1.80.D1.8B "Список приложений")).

Ниже приведен список программ, которые также обычно входят в состав сред рабочего стола.

*   Запуск программ: [Список приложений#Утилиты запуска приложений](/index.php/%D0%A1%D0%BF%D0%B8%D1%81%D0%BE%D0%BA_%D0%BF%D1%80%D0%B8%D0%BB%D0%BE%D0%B6%D0%B5%D0%BD%D0%B8%D0%B9#.D0.A3.D1.82.D0.B8.D0.BB.D0.B8.D1.82.D1.8B_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA.D0.B0_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D0.B9 "Список приложений")
*   Буфер обмена: [Список приложений#Менеджеры буфера обмена](/index.php/%D0%A1%D0%BF%D0%B8%D1%81%D0%BE%D0%BA_%D0%BF%D1%80%D0%B8%D0%BB%D0%BE%D0%B6%D0%B5%D0%BD%D0%B8%D0%B9#.D0.9C.D0.B5.D0.BD.D0.B5.D0.B4.D0.B6.D0.B5.D1.80.D1.8B_.D0.B1.D1.83.D1.84.D0.B5.D1.80.D0.B0_.D0.BE.D0.B1.D0.BC.D0.B5.D0.BD.D0.B0 "Список приложений")
*   Композитный менеджер: [Список композитных менеджеров](/index.php/Xorg#List_of_composite_managers "Xorg")
*   Менеджер обоев рабочего стола: [Список приложений#Обои рабочего стола](/index.php/%D0%A1%D0%BF%D0%B8%D1%81%D0%BE%D0%BA_%D0%BF%D1%80%D0%B8%D0%BB%D0%BE%D0%B6%D0%B5%D0%BD%D0%B8%D0%B9#.D0.9E.D0.B1.D0.BE.D0.B8_.D1.80.D0.B0.D0.B1.D0.BE.D1.87.D0.B5.D0.B3.D0.BE_.D1.81.D1.82.D0.BE.D0.BB.D0.B0 "Список приложений")
*   Экранный менеджер: [Экранный менеджер#Список экранных менеджеров](/index.php/%D0%AD%D0%BA%D1%80%D0%B0%D0%BD%D0%BD%D1%8B%D0%B9_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80#.D0.A1.D0.BF.D0.B8.D1.81.D0.BE.D0.BA_.D1.8D.D0.BA.D1.80.D0.B0.D0.BD.D0.BD.D1.8B.D1.85_.D0.BC.D0.B5.D0.BD.D0.B5.D0.B4.D0.B6.D0.B5.D1.80.D0.BE.D0.B2 "Экранный менеджер")
*   Отключение дисплея для экономии батареи: [DPMS](/index.php/Display_Power_Management_Signaling_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Display Power Management Signaling (Русский)")
*   Диалог завершения работы: [Список приложений#Диалоги завершения работы](/index.php/%D0%A1%D0%BF%D0%B8%D1%81%D0%BE%D0%BA_%D0%BF%D1%80%D0%B8%D0%BB%D0%BE%D0%B6%D0%B5%D0%BD%D0%B8%D0%B9#.D0.94.D0.B8.D0.B0.D0.BB.D0.BE.D0.B3.D0.B8_.D0.B7.D0.B0.D0.B2.D0.B5.D1.80.D1.88.D0.B5.D0.BD.D0.B8.D1.8F_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D1.8B "Список приложений")
*   Уведомления рабочего стола: [Уведомления рабочего стола](/index.php/Desktop_notifications_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Desktop notifications (Русский)")
*   Агент Polkit: [Агенты аутентификации Polkit](/index.php/Polkit#Authentication_agents "Polkit")
*   Блокировщик экрана: [Список приложений#Блокировка экрана](/index.php/%D0%A1%D0%BF%D0%B8%D1%81%D0%BE%D0%BA_%D0%BF%D1%80%D0%B8%D0%BB%D0%BE%D0%B6%D0%B5%D0%BD%D0%B8%D0%B9#.D0.91.D0.BB.D0.BE.D0.BA.D0.B8.D1.80.D0.BE.D0.B2.D0.BA.D0.B0_.D1.8D.D0.BA.D1.80.D0.B0.D0.BD.D0.B0 "Список приложений")
*   Микшер: [Список приложений#Управление громкостью](/index.php/%D0%A1%D0%BF%D0%B8%D1%81%D0%BE%D0%BA_%D0%BF%D1%80%D0%B8%D0%BB%D0%BE%D0%B6%D0%B5%D0%BD%D0%B8%D0%B9#.D0.A3.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B3.D1.80.D0.BE.D0.BC.D0.BA.D0.BE.D1.81.D1.82.D1.8C.D1.8E "Список приложений")

Retrieved from "[https://wiki.archlinux.org/index.php?title=Desktop_environment_(Русский)&oldid=411568](https://wiki.archlinux.org/index.php?title=Desktop_environment_(Русский)&oldid=411568)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Desktop environments (Русский)](/index.php/Category:Desktop_environments_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Category:Desktop environments (Русский)")
*   [Русский](/index.php/Category:%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9 "Category:Русский")