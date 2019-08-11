Ссылки по теме

*   [Сравнение сред рабочего стола](/index.php/%D0%A1%D1%80%D0%B0%D0%B2%D0%BD%D0%B5%D0%BD%D0%B8%D0%B5_%D1%81%D1%80%D0%B5%D0%B4_%D1%80%D0%B0%D0%B1%D0%BE%D1%87%D0%B5%D0%B3%D0%BE_%D1%81%D1%82%D0%BE%D0%BB%D0%B0 "Сравнение сред рабочего стола")
*   [Category:Freedesktop.org (Русский)](/index.php/Category:Freedesktop.org_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Category:Freedesktop.org (Русский)")

**Состояние перевода:** На этой странице представлен перевод статьи [Desktop environment](/index.php/Desktop_environment "Desktop environment"). Дата последней синхронизации: 5 августа 2019\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Desktop_environment&diff=0&oldid=578832).

[Среда рабочего стола](https://en.wikipedia.org/wiki/ru:%D0%A1%D1%80%D0%B5%D0%B4%D0%B0_%D1%80%D0%B0%D0%B1%D0%BE%D1%87%D0%B5%D0%B3%D0%BE_%D1%81%D1%82%D0%BE%D0%BB%D0%B0 "wikipedia:ru:Среда рабочего стола") (**DE**) — реализация [метафоры рабочего стола](https://en.wikipedia.org/wiki/ru:%D0%A0%D0%B0%D0%B1%D0%BE%D1%87%D0%B8%D0%B9_%D1%81%D1%82%D0%BE%D0%BB "wikipedia:ru:Рабочий стол"), состоящая из набора программ, которые разделяют общий графический интерфейс (GUI).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Обзор](#Обзор)
*   [2 Список сред рабочего стола](#Список_сред_рабочего_стола)
    *   [2.1 Официально поддерживаемые](#Официально_поддерживаемые)
    *   [2.2 Неофициально поддерживаемые](#Неофициально_поддерживаемые)
*   [3 Создание персонализированной среды](#Создание_персонализированной_среды)
    *   [3.1 Использование стороннего оконного менеджера](#Использование_стороннего_оконного_менеджера)

## Обзор

Среда рабочего стола объединяет различные компоненты для предоставления единых элементов графического интерфейса, например, значков, панелей, обоев и виджетов рабочего стола. Также большинство сред включают в себя интегрированный набор программ и утилит. Что самое важное, среды рабочего стола предоставляют свой собственный [оконный менеджер](/index.php/%D0%9E%D0%BA%D0%BE%D0%BD%D0%BD%D1%8B%D0%B9_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80 "Оконный менеджер"), который обычно можно заменить совместимым вариантом.

Пользователю даётся возможность настраивать графический интерфейс разными путями. Как правило, среды рабочего стола предоставляют для этого готовые и удобные средства. Следует отметить, что пользователи могут комбинировать и одновременно запускать приложения, написанные для разных сред. Так, пользователь [KDE Plasma](/index.php/KDE_Plasma_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "KDE Plasma (Русский)") может устанавливать и запускать приложения [GNOME](/index.php/GNOME_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GNOME (Русский)"), например, веб-браузер [Epiphany](/index.php/Epiphany "Epiphany"), если он нравится больше, чем Konqueror от KDE. Однако, такой подход имеет и недостаток: многие графические приложения тесно связаны с тем или иным набором библиотек, которые входят в состав "родной" среды. В результате установка множества "неродных" приложений потребует установки большего количества зависимостей. Пользователям, которые экономят место на диске, следует избегать подобных смешанных окружений или выбирать альтернативные программы, которые зависят всего от нескольких внешних библиотек.

Кроме того, приложения в родной среде выглядят более единообразно и лучше в неё интегрируются. Приложения, написанные с использованием разных библиотек компонентов интерфейса, могут по-разному выглядеть (использовать разные наборы иконок и стили оформления компонентов) и вести себя (например, использовать одиночный щелчок по значку вместо двойного или иметь другое поведение drag-and-drop), создавая путаницу или непредсказуемое поведение.

Для установки среды рабочего стола необходим работоспособный сервер X. Подробнее об этом смотрите в статье [Xorg](/index.php/Xorg_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xorg (Русский)"). Также некоторые среды поддерживают [Wayland](/index.php/Wayland_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Wayland (Русский)"), но в большинстве случаев эта поддержка носит экспериментальный характер.

## Список сред рабочего стола

### Официально поддерживаемые

*   **[Budgie](/index.php/Budgie_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Budgie (Русский)")** — рабочая среда, рассчитанная на современного пользователя, где основное внимание уделяется простоте и элегантности.

	[https://getsol.us/](https://getsol.us/) || [budgie-desktop](https://www.archlinux.org/packages/?name=budgie-desktop)

*   **[Cinnamon](/index.php/Cinnamon_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Cinnamon (Русский)")** — Cinnamon стремится предоставить пользователю более привычную и традиционную среду. Cinnamon — форк GNOME 3.

	[http://developer.linuxmint.com/projects/cinnamon-projects.html/](http://developer.linuxmint.com/projects/cinnamon-projects.html/) || [cinnamon](https://www.archlinux.org/packages/?name=cinnamon)

*   **[Deepin](/index.php/Deepin_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Deepin (Русский)")** — интерфейс и приложения Deepin предоставляют интуитивный и элегантный дизайн. Перемещения, обмен, поиск и другие возможности теперь вызывают только удовольствие.

	[https://www.deepin.org/](https://www.deepin.org/) || [deepin](https://www.archlinux.org/groups/x86_64/deepin/)

*   **[Enlightenment](/index.php/Enlightenment_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Enlightenment (Русский)")** — Enlightenment предоставляет эффективный менеджер окон, основанный на библиотеках Enlightenment Foundation, а также другие необходимые компоненты вроде файлового менеджера, значков и виджетов. Он поддерживает темы и его можно запускать на устаревших компьютерах и встраиваемых устройствах.

	[https://www.enlightenment.org/](https://www.enlightenment.org/) || [enlightenment](https://www.archlinux.org/packages/?name=enlightenment)

*   **[GNOME](/index.php/GNOME_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GNOME (Русский)")** — популярная и интуитивная среда рабочего стола, которая поддерживает современный (*GNOME*) и классический (*GNOME Classic*) режимы.

	[https://www.gnome.org/gnome-3/](https://www.gnome.org/gnome-3/) || [gnome](https://www.archlinux.org/groups/x86_64/gnome/)

*   **[GNOME Flashback](/index.php/GNOME_Flashback "GNOME Flashback")** — оболочка для GNOME 3, которая изначально использовалась в нём для режима совместимости. Рабочий стол и технологии похожи на GNOME 2.

	[https://wiki.gnome.org/Projects/GnomeFlashback](https://wiki.gnome.org/Projects/GnomeFlashback) || [gnome-flashback](https://www.archlinux.org/packages/?name=gnome-flashback)

*   **[KDE Plasma](/index.php/KDE_Plasma_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "KDE Plasma (Русский)")** — хорошо известная рабочая среда. Она предоставляет все необходимые современному пользователю средства, тем самым обеспечивая продуктивность с самого начала.

	[https://www.kde.org/plasma-desktop](https://www.kde.org/plasma-desktop) || [plasma](https://www.archlinux.org/groups/x86_64/plasma/)

*   **[LXDE](/index.php/LXDE_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "LXDE (Русский)")** — лёгкая, быстрая и энергосберегающая среда рабочего стола для X11\. Она предлагает современный интерфейс, поддержку различных языков, стандартные сочетания клавиш и дополнительные возможности, например, использование файлового менеджера со вкладками. При этом LXDE старается тратить меньше ресурсов процессора и оперативной памяти, чем другие окружения.

	[https://lxde.org/](https://lxde.org/) || GTK+ 2: [lxde](https://www.archlinux.org/groups/x86_64/lxde/), GTK+ 3: [lxde-gtk3](https://www.archlinux.org/groups/x86_64/lxde-gtk3/)

*   **[LXQt](/index.php/LXQt_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "LXQt (Русский)")** — порт LXDE (Lightweight Desktop Environment) на Qt. LXQt объединяет проекты LXDE-Qt и Razor-qt, предоставляя легковесное, модульное, быстрое и интуитивное окружение рабочего стола.

	[https://lxqt.org/](https://lxqt.org/) || [lxqt](https://www.archlinux.org/groups/x86_64/lxqt/)

*   **[MATE](/index.php/MATE_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "MATE (Русский)")** — MATE предоставляет интуитивный, привлекательный и традиционный рабочий стол. Изначально MATE был форком GNOME 2, но в данный момент использует GTK+ 3.

	[https://mate-desktop.org/](https://mate-desktop.org/) || [mate](https://www.archlinux.org/groups/x86_64/mate/)

*   **[Sugar](/index.php/Sugar "Sugar")** — The Sugar Learning Platform — окружение, состоящее из Комнат (Activities), которые разработаны для помощи в совместном обучении детей 5-12 лет с помощью мультимедийных приложений. Sugar направлен на предоставление детям по всему миру возможности получить качественное образование — на данный момент проект используется примерно миллионом детей на 25 языках в более, чем 40 странах.

	[https://sugarlabs.org/](https://sugarlabs.org/) || [sugar](https://www.archlinux.org/packages/?name=sugar) + [sugar-fructose](https://www.archlinux.org/groups/x86_64/sugar-fructose/)

*   **[Xfce](/index.php/Xfce_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xfce (Русский)")** — Xfce следует традиционной [философии UNIX](https://en.wikipedia.org/wiki/ru:%D0%A4%D0%B8%D0%BB%D0%BE%D1%81%D0%BE%D1%84%D0%B8%D1%8F_Unix "wikipedia:ru:Философия Unix"), основываясь на принципах модульности и повторного использования. Данная среда состоит из множества компонентов, составляющих полноценное современное рабочее окружение, при этом оставаясь относительно лёгким. Эти компоненты распределены по разным пакетам, поэтому вы можете выбирать только нужные, чтобы создать оптимальное рабочее окружение.

	[https://xfce.org/](https://xfce.org/) || [xfce4](https://www.archlinux.org/groups/x86_64/xfce4/)

### Неофициально поддерживаемые

*   **[EDE](/index.php/Equinox_Desktop_Environment "Equinox Desktop Environment")** — простое, быстрое и исключительно лёгкое окружение рабочего стола.

	[https://edeproject.org/](https://edeproject.org/) || [ede](https://aur.archlinux.org/packages/ede/)

*   **[Liri](/index.php/Liri "Liri")** — окружение рабочего стола с современными возможностями и дизайном. Проект объединяет [Hawaii](https://github.com/hawaii-desktop), [Papyros](https://github.com/papyros) и [Liri Project](https://github.com/liri-project). Данное окружение находится в очень экспериментальной стадии разработки.

	[https://liri.io/](https://liri.io/) || [liri-shell-git](https://aur.archlinux.org/packages/liri-shell-git/)

*   **[Lumina](/index.php/Lumina "Lumina")** — легковесное окружение рабочего стола для FreeBSD, написанное на Qt 5 и использующее Fluxbox в качестве оконного менеджера.

	[https://www.lumina-desktop.org/](https://www.lumina-desktop.org/) || [lumina-desktop](https://aur.archlinux.org/packages/lumina-desktop/)

*   **[Moksha](/index.php/Moksha "Moksha")** — форк Enlightenment, использующийся в качестве окружения рабочего стола по умолчанию в дистрибутиве Bodhi Linux на основе Ubuntu.

	[http://www.bodhilinux.com/moksha-desktop/](http://www.bodhilinux.com/moksha-desktop/) || [moksha](https://aur.archlinux.org/packages/moksha/)

*   **[Pantheon](/index.php/Pantheon "Pantheon")** — среда рабочего стола, изначально созданная для дистрибутива elementary OS. Она написана с нуля на основе Vala и GTK3, а внешний вид и удобство напоминают собой GNOME Shell и macOS.

	[https://elementary.io/](https://elementary.io/) || [pantheon-session-git](https://aur.archlinux.org/packages/pantheon-session-git/)

*   **theShell** — среда рабочего стола, старающаяся быть как можно более прозрачной. В ней используются фреймфорк Qt 5 и оконный менеджер KWin.

	[https://vicr123.com/theshell/](https://vicr123.com/theshell/) || [theshell](https://aur.archlinux.org/packages/theshell/)

*   **[Trinity](/index.php/Trinity "Trinity")** — среда рабочего стола для Unix-подобных ОС, сохраняющая общий стиль неподдерживаемой в настоящее время среды KDE 3.5.

	[http://www.trinitydesktop.org/](http://www.trinitydesktop.org/) || См. [Trinity](/index.php/Trinity "Trinity")

## Создание персонализированной среды

Установка среды рабочего стола представляет собой наиболее простой способ получить полноценное графическое окружение. Однако пользователь может создать и персонализировать своё графическое окружение, если существующее не отвечает каким-либо требованиям. В общих чертах, создание своего окружения включает в себя выбор подходящих [оконного менеджера](/index.php/Window_manager_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Window manager (Русский)"), [панели задач](/index.php/%D0%A1%D0%BF%D0%B8%D1%81%D0%BE%D0%BA_%D0%BF%D1%80%D0%B8%D0%BB%D0%BE%D0%B6%D0%B5%D0%BD%D0%B8%D0%B9#Панели_задач_/_доки "Список приложений") и набора программ (который, как минимум, обычно состоит из [эмулятора терминала](/index.php/%D0%A1%D0%BF%D0%B8%D1%81%D0%BE%D0%BA_%D0%BF%D1%80%D0%B8%D0%BB%D0%BE%D0%B6%D0%B5%D0%BD%D0%B8%D0%B9#Эмуляторы_терминала "Список приложений"), [файлового менеджера](/index.php/%D0%A1%D0%BF%D0%B8%D1%81%D0%BE%D0%BA_%D0%BF%D1%80%D0%B8%D0%BB%D0%BE%D0%B6%D0%B5%D0%BD%D0%B8%D0%B9#Файловые_менеджеры "Список приложений") и [текстового редактора](/index.php/%D0%A1%D0%BF%D0%B8%D1%81%D0%BE%D0%BA_%D0%BF%D1%80%D0%B8%D0%BB%D0%BE%D0%B6%D0%B5%D0%BD%D0%B8%D0%B9#Текстовые_редакторы "Список приложений")).

Ниже приведён список программ, которые также обычно входят в состав сред рабочего стола.

*   Средство запуска приложений: [Список приложений#Утилиты запуска приложений](/index.php/%D0%A1%D0%BF%D0%B8%D1%81%D0%BE%D0%BA_%D0%BF%D1%80%D0%B8%D0%BB%D0%BE%D0%B6%D0%B5%D0%BD%D0%B8%D0%B9#Утилиты_запуска_приложений "Список приложений")
*   Регулятор громкости: [Список приложений#Управление громкостью](/index.php/%D0%A1%D0%BF%D0%B8%D1%81%D0%BE%D0%BA_%D0%BF%D1%80%D0%B8%D0%BB%D0%BE%D0%B6%D0%B5%D0%BD%D0%B8%D0%B9#Управление_громкостью "Список приложений")
*   Менеджер буфера обмена: [Список приложений#Менеджеры буфера обмена](/index.php/%D0%A1%D0%BF%D0%B8%D1%81%D0%BE%D0%BA_%D0%BF%D1%80%D0%B8%D0%BB%D0%BE%D0%B6%D0%B5%D0%BD%D0%B8%D0%B9#Менеджеры_буфера_обмена "Список приложений")
*   Композитный менеджер: [Xorg (Русский)#Композит](/index.php/Xorg_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Композит "Xorg (Русский)")
*   Менеджер обоев рабочего стола: [Список приложений#Обои рабочего стола](/index.php/%D0%A1%D0%BF%D0%B8%D1%81%D0%BE%D0%BA_%D0%BF%D1%80%D0%B8%D0%BB%D0%BE%D0%B6%D0%B5%D0%BD%D0%B8%D0%B9#Обои_рабочего_стола "Список приложений")
*   Экранный менеджер: [Экранный менеджер#Список экранных менеджеров](/index.php/%D0%AD%D0%BA%D1%80%D0%B0%D0%BD%D0%BD%D1%8B%D0%B9_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80#Список_экранных_менеджеров "Экранный менеджер")
*   Настройки энергосбережения дисплея: [Display Power Management Signaling (Русский)](/index.php/Display_Power_Management_Signaling_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Display Power Management Signaling (Русский)")
*   Диалог завершения работы: [Oblogout](/index.php/Oblogout "Oblogout")
*   Утилита для монтирования: [Список приложений#Монтирование](/index.php/%D0%A1%D0%BF%D0%B8%D1%81%D0%BE%D0%BA_%D0%BF%D1%80%D0%B8%D0%BB%D0%BE%D0%B6%D0%B5%D0%BD%D0%B8%D0%B9#Монтирование "Список приложений")
*   Демон уведомлений: [Уведомления рабочего стола](/index.php/Desktop_notifications_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Desktop notifications (Русский)")
*   Агент аутентификации Polkit: [Polkit (Русский)#Агенты аутентификации](/index.php/Polkit_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Агенты_аутентификации "Polkit (Русский)")
*   Блокировщик экрана: [Список приложений#Блокировка экрана](/index.php/%D0%A1%D0%BF%D0%B8%D1%81%D0%BE%D0%BA_%D0%BF%D1%80%D0%B8%D0%BB%D0%BE%D0%B6%D0%B5%D0%BD%D0%B8%D0%B9#Блокировка_экрана "Список приложений")
*   Приложения по умолчанию: [XDG MIME Applications (Русский)#mimeapps.list](/index.php/XDG_MIME_Applications_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#mimeapps.list "XDG MIME Applications (Русский)")

### Использование стороннего оконного менеджера

См. раздел "Использование стороннего оконного менеджера" в статье о необходимой среде рабочего стола или же обратитесь к официальной документации.

*   [Budgie#Use a different window manager](/index.php/Budgie#Use_a_different_window_manager "Budgie")
*   [Cinnamon#Use a different window manager](/index.php/Cinnamon#Use_a_different_window_manager "Cinnamon")
*   [GNOME (Русский)#Использование стороннего оконного менеджера](/index.php/GNOME_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Использование_стороннего_оконного_менеджера "GNOME (Русский)")
*   [KDE (Русский)#Использование альтернативного оконного менеджера](/index.php/KDE_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Использование_альтернативного_оконного_менеджера "KDE (Русский)")
*   [LXDE (Русский)#Замена оконного менеджера](/index.php/LXDE_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Замена_оконного_менеджера "LXDE (Русский)")
*   [LXQt (Русский)#Замена Openbox](/index.php/LXQt_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Замена_Openbox "LXQt (Русский)")
*   [MATE (Русский)#Поменять оконный менеджер](/index.php/MATE_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Поменять_оконный_менеджер "MATE (Русский)")
*   [Xfce (Русский)#Оконный менеджер по умолчанию](/index.php/Xfce_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Оконный_менеджер_по_умолчанию "Xfce (Русский)")