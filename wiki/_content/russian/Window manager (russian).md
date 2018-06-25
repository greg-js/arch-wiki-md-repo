Ссылки по теме

*   [Среда рабочего стола](/index.php/%D0%A1%D1%80%D0%B5%D0%B4%D0%B0_%D1%80%D0%B0%D0%B1%D0%BE%D1%87%D0%B5%D0%B3%D0%BE_%D1%81%D1%82%D0%BE%D0%BB%D0%B0 "Среда рабочего стола")
*   [Оконный менеджер](/index.php/%D0%9E%D0%BA%D0%BE%D0%BD%D0%BD%D1%8B%D0%B9_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80 "Оконный менеджер")
*   [Xorg (Русский)](/index.php/Xorg_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xorg (Русский)")
*   [xinitrc](/index.php/Xinitrc "Xinitrc")
*   [Запуск X при входе](/index.php/%D0%97%D0%B0%D0%BF%D1%83%D1%81%D0%BA_X_%D0%BF%D1%80%D0%B8_%D0%B2%D1%85%D0%BE%D0%B4%D0%B5 "Запуск X при входе")

[Оконный менеджер](https://en.wikipedia.org/wiki/Window_manager или работать отдельно.

## Contents

*   [1 Обзор](#.D0.9E.D0.B1.D0.B7.D0.BE.D1.80)
    *   [1.1 Типы](#.D0.A2.D0.B8.D0.BF.D1.8B)
*   [2 Список оконных менеджеров](#.D0.A1.D0.BF.D0.B8.D1.81.D0.BE.D0.BA_.D0.BE.D0.BA.D0.BE.D0.BD.D0.BD.D1.8B.D1.85_.D0.BC.D0.B5.D0.BD.D0.B5.D0.B4.D0.B6.D0.B5.D1.80.D0.BE.D0.B2)
    *   [2.1 Стековые оконные менеджеры](#.D0.A1.D1.82.D0.B5.D0.BA.D0.BE.D0.B2.D1.8B.D0.B5_.D0.BE.D0.BA.D0.BE.D0.BD.D0.BD.D1.8B.D0.B5_.D0.BC.D0.B5.D0.BD.D0.B5.D0.B4.D0.B6.D0.B5.D1.80.D1.8B)
    *   [2.2 Фреймовые оконные менеджеры](#.D0.A4.D1.80.D0.B5.D0.B9.D0.BC.D0.BE.D0.B2.D1.8B.D0.B5_.D0.BE.D0.BA.D0.BE.D0.BD.D0.BD.D1.8B.D0.B5_.D0.BC.D0.B5.D0.BD.D0.B5.D0.B4.D0.B6.D0.B5.D1.80.D1.8B)
    *   [2.3 Динамические оконные менеджеры](#.D0.94.D0.B8.D0.BD.D0.B0.D0.BC.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8.D0.B5_.D0.BE.D0.BA.D0.BE.D0.BD.D0.BD.D1.8B.D0.B5_.D0.BC.D0.B5.D0.BD.D0.B5.D0.B4.D0.B6.D0.B5.D1.80.D1.8B)
*   [3 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Обзор

Оконные менеджеры работают в роли клиентов оконной системы X, которые управляют внешним видом и поведением прямоугольных фреймов ("окон"), где отображаются элементы интерфейса графических программ. Они добавляют фрейму рамку, панель заголовка, возможность изменять его размер и т. д., а также часто предоставляют дополнительную функциональность — например, создают специальные области на экране для "приклеивания" виджетов ([dockapps](http://windowmaker.org/dockapps/)), как [Window Maker](/index.php/Window_Maker "Window Maker"), или позволяют объединить несколько приложений в одном окне, переключаясь между ними с помощью вкладок, как [Fluxbox](/index.php/Fluxbox_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Fluxbox (Русский)"). Некоторые оконные менеджеры даже включают в свой набор простые утилиты вроде меню запуска программ или графического инструмента для настройки самого менеджера.

Спецификация [Extended Window Manager Hints от X Desktop Group](http://standards.freedesktop.org/wm-spec/wm-spec-latest.html) создана и используется для того, чтобы позволить разным оконным менеджерам единообразно взаимодействовать с сервером X и другими клиентами.

Некоторые оконные менеджеры разрабатываются в рамках более крупных проектов [сред рабочего стола](/index.php/Desktop_environment_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Desktop environment (Русский)"), и, как правило, они теснее интегрируются в среду, создавая более полноценное рабочее окружение, дополненное значками рабочего стола, шрифтами, разнообразными панелями, нескучными обоями и виджетами рабочего стола.

Перед установкой оконного менеджера необходимо установить и настроить сервер X. Подробную информацию вы сможете получить на странице [Xorg](/index.php/Xorg_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xorg (Русский)").

### Типы

*   [Стековые](#.D0.A1.D1.82.D0.B5.D0.BA.D0.BE.D0.B2.D1.8B.D0.B5_.D0.BE.D0.BA.D0.BE.D0.BD.D0.BD.D1.8B.D0.B5_.D0.BC.D0.B5.D0.BD.D0.B5.D0.B4.D0.B6.D0.B5.D1.80.D1.8B) (также *плавающие*) оконные менеджеры следуют традиционной метафоре рабочего стола, которая используется в коммерческих операционных системах Windows и OS X. Окна отображаются подобно листкам бумаги на столе, накладываясь и перекрывая друг друга. Список статей о стековых оконных менеджерах смотрите на странице [стековые оконные менеджеры](/index.php/Category:Stacking_WMs_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Category:Stacking WMs (Русский)").
*   [Фреймовые](#.D0.A4.D1.80.D0.B5.D0.B9.D0.BC.D0.BE.D0.B2.D1.8B.D0.B5_.D0.BE.D0.BA.D0.BE.D0.BD.D0.BD.D1.8B.D0.B5_.D0.BC.D0.B5.D0.BD.D0.B5.D0.B4.D0.B6.D0.B5.D1.80.D1.8B) оконные менеджеры располагают окна на экране в виде плиток (фреймов) так, что они не перекрывают друг друга. Как правило, фреймовые оконные менеджеры подразумевают активное использование клавиатуры для управления окнами, и имеют слабую поддержку мыши (либо не имеют ее вовсе). Фреймовые оконные менеджеры могут предлагать набор стандартных расположений фреймов или позволять задавать их вручную. Список статей о фреймовых оконных менеджерах смотрите на странице [фреймовые оконные менеджеры](/index.php/Category:Tiling_WMs_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Category:Tiling WMs (Русский)").
*   [Динамические](#.D0.94.D0.B8.D0.BD.D0.B0.D0.BC.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8.D0.B5_.D0.BE.D0.BA.D0.BE.D0.BD.D0.BD.D1.8B.D0.B5_.D0.BC.D0.B5.D0.BD.D0.B5.D0.B4.D0.B6.D0.B5.D1.80.D1.8B) оконные менеджеры позволяют динамически переключаться между двумя режимами — стековым и фреймовым. Список статей о динамических оконных менеджерах смотрите на странице [динамические оконные менеджеры](/index.php/Category:Dynamic_WMs_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Category:Dynamic WMs (Русский)").

Сравнение популярных оконных менеджеров вы можете найти на страницах [Сравнение тайловых оконных менеджеров](/index.php/%D0%A1%D1%80%D0%B0%D0%B2%D0%BD%D0%B5%D0%BD%D0%B8%D0%B5_%D1%82%D0%B0%D0%B9%D0%BB%D0%BE%D0%B2%D1%8B%D1%85_%D0%BE%D0%BA%D0%BE%D0%BD%D0%BD%D1%8B%D1%85_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80%D0%BE%D0%B2 "Сравнение тайловых оконных менеджеров") и [Wikipedia:Comparison of X window managers](https://en.wikipedia.org/wiki/Comparison_of_X_window_managers "wikipedia:Comparison of X window managers").

## Список оконных менеджеров

### Стековые оконные менеджеры

*   **[2bwm](/index.php/2bwm "2bwm")** — Быстрый стековый менеджер, отличающийся наличием двойной рамки у окон на основе mcwm, написанной Майклом Карделлом. В 2bwm вся функциональность доступна с клавиатуры, однако, мышь также может быть использована для управления окнами. Имя недавно было сменено с mcwm-beast на 2bwm.

	[https://github.com/venam/2bwm](https://github.com/venam/2bwm) || [2bwm](https://aur.archlinux.org/packages/2bwm/)

*   **aewm** — Современный, минималистичный оконный менеджер для X11\. Полностью управляется мышью, но содержит также набор команд, которые похожи на команды vi. Созданный уже очень давно (1997) для того, чтобы выжать максимум из старых машин с небольшим количеством памяти, полностью неинтуитивный и враждебный для новичков, но в каком-то отношении весьма быстрый и элегантный.

	[http://www.red-bean.com/decklin/aewm/](http://www.red-bean.com/decklin/aewm/) || [aewm](https://aur.archlinux.org/packages/aewm/)

*   **[AfterStep](https://en.wikipedia.org/wiki/AfterStep "wikipedia:AfterStep")** — Оконный менеджер для X Window System. Изначально повторяющий внешний вид интерфейса NeXTStep, он предоставляет конечным пользователям гармоничный, чистый и элегантный рабочий стол. Целью разработки AfterStep является предоставления возможности гибкой настройки рабочего стола, эстетичного дизайна при эффективном использовании системных ресурсов.

	[http://www.afterstep.org/](http://www.afterstep.org/) || [afterstep](https://aur.archlinux.org/packages/afterstep/)

*   **[Blackbox](https://en.wikipedia.org/wiki/Blackbox "wikipedia:Blackbox")** — Быстрый и легкий оконный менеджер для X Window System, без всех этих раздражающих зависимостей. Blackbox написан на C++ и содержит полностью собственный код (хотя реализация графики идентична таковой в WindowMaker).

	[http://blackboxwm.sourceforge.net/](http://blackboxwm.sourceforge.net/) || [blackbox](https://www.archlinux.org/packages/?name=blackbox)

*   **[Compiz](/index.php/Compiz "Compiz")** — Композитный менеджер на основе OpenGL, использующий GLX_EXT_texture_from_pixmap для использования изображений окон в качестве текстур. У него есть гибкая система плагинов и он спроектирован для работы на большинстве графических ускорителей.

	[https://launchpad.net/compiz](https://launchpad.net/compiz) || [compiz](https://aur.archlinux.org/packages/compiz/)

*   **[cwm](/index.php/Cwm "Cwm")** — Изначально отделившийся от evilwm, но позже переписанный с нуля. cwm нацелен на простоту, и при этом предлагает некоторые полезные возможности, такие как поиск окон.

	[http://monkey.org/~marius/cwm/cwm.1.a](http://monkey.org/~marius/cwm/cwm.1.a) || [cwm](https://aur.archlinux.org/packages/cwm/)

*   **[Enlightenment](/index.php/Enlightenment "Enlightenment")** — Это не просто оконный менеджер для X11, но и целый набор библиотек, которые помогут вам создать отличные пользовательские интерфейсы с много меньшими затратами времени и сил, чем при использовании более консервативных тулкитов, не говоря уже о других оконных менеджерах.

	[http://www.enlightenment.org/](http://www.enlightenment.org/) || [enlightenment](https://www.archlinux.org/packages/?name=enlightenment)

*   **[evilwm](/index.php/Evilwm "Evilwm")** — Минималистичный оконный менеджер для X Window System. Минималистичный тут не значит, что этот менеджер голый и неюзабельный — под этим просто понимается, что он в нем отказались от всего, что делает неюзабельными другие оконные менеджеры.

	[http://www.6809.org.uk/evilwm/](http://www.6809.org.uk/evilwm/) || [evilwm](https://aur.archlinux.org/packages/evilwm/)

*   **[Fluxbox](/index.php/Fluxbox "Fluxbox")** — Оконный менеджер для X, основанный на коде Blackbox 0.61.1\. Нетребователен к ресурсам и практичен в использовании, при этом полон возможностей для создания простой и очень быстрой рабочей среды. Он написан на C++ и имеет лицензию MIT.

	[http://www.fluxbox.org/](http://www.fluxbox.org/) || [fluxbox](https://www.archlinux.org/packages/?name=fluxbox)

*   **[Flwm](https://en.wikipedia.org/wiki/FLWM "wikipedia:FLWM")** — Попытка совместить лучшие идеи из разных оконных менеджеров. Основное влияние и кодовую базу получил от wm2 автора Криса Каннама.

	[http://flwm.sourceforge.net/](http://flwm.sourceforge.net/) || [flwm](https://aur.archlinux.org/packages/flwm/)

*   **[FVWM](/index.php/FVWM "FVWM")** — Экстремально навороченный ICCCM-совместимый много-виртуально-десктопный оконный менеджер для X Window System. Находится в активной разработке и имеет отзывчивую техподдержку.

	[http://www.fvwm.org/](http://www.fvwm.org/) || [fvwm](https://www.archlinux.org/packages/?name=fvwm)

*   **[Gala](http://elementaryos.org/journal/meet-gala-window-manager)** — Симпатичный оконный менеджер из Elementary OS, является частью [Pantheon](/index.php/Pantheon "Pantheon"). Также, являясь композитным менеджером, работает на libmutter.

	[https://launchpad.net/gala](https://launchpad.net/gala) || [gala-bzr](https://aur.archlinux.org/packages/gala-bzr/)

*   **Goomwwm** — Оконный менеджер X11, написанный на C по методологии "чистой комнаты". Он предоставляет возможность гибкого управления окнами посредством клавиатуры: есть хоткеи для переключения окон, изменения размеров, перемещения, укладывания плиткой и других операций. Он также быстрый, легкий, знает, что такое Xinerama и совместим с EWMH везде, где только это возможно.

	[http://aerosuidae.net/goomwwm/](http://aerosuidae.net/goomwwm/) || [goomwwm](https://aur.archlinux.org/packages/goomwwm/)

*   **[IceWM](/index.php/IceWM "IceWM")** — Оконный менеджер для X Window System. Целью своей ставит стремление к скорости, простоте и старается как можно меньше раздражать пользователя при работе.

	[http://www.icewm.org/](http://www.icewm.org/) || [icewm](https://www.archlinux.org/packages/?name=icewm)

*   **[JWM](/index.php/JWM "JWM")** — Оконный менеджер для X11 Window System. JWM написан на C и использует только Xlib.

	[http://joewing.net/projects/jwm/index.shtml](http://joewing.net/projects/jwm/index.shtml) || [jwm](https://www.archlinux.org/packages/?name=jwm)

*   **Karmen** — Оконный менеджер для X, написанный Йоханом Винхуйзеном. "Создан, чтобы просто работать". Тут нет никаких файлов настройки и других зависимостей, кроме Xlib. Karmen совместим с ICCCM и EWMH.

	[http://karmen.sourceforge.net/](http://karmen.sourceforge.net/) || [karmen](https://aur.archlinux.org/packages/karmen/)

*   **[KWin](https://en.wikipedia.org/wiki/KWin "wikipedia:KWin")** — Стандартный оконный менеджер KDE 4.0\. Имеет встроенную поддержку композитного режима, что делает его также композитным менеджером. Это позволяет KWin использовать разнообразные графические эффекты, подобно Compiz, при этом также предоставляя все возможности с предыдущих релизов KDE (например, очень неплохую интеграцию со средой, гибкость в настройке, предотвращения потери фокуса, надежный механизм обработки сбоев приложений/тулкитов и т. д.).

	[https://techbase.kde.org/Projects/KWin](https://techbase.kde.org/Projects/KWin) || [kwin](https://www.archlinux.org/packages/?name=kwin) [kdebase-workspace](https://aur.archlinux.org/packages/kdebase-workspace/) [kwin-git](https://aur.archlinux.org/packages/kwin-git/)

*   **lwm** — Оконный менеджер для X, который всеми силами прячется от вас. Вы не увидите значков, кнопок, панелей, меню, ничего: если вам что-нибудь из этого нужно, устанавливайте сторонние программы. Здесь нет никаких настроек вообще: если они вам нужны, используйте другой оконный менеджер — такой, который поможет вашей операционной системе оккупировать все свободное пространство на вашем жестком диске, а потом примется за вашу оперативную память.

	[http://www.jfc.org.uk/software/lwm.html](http://www.jfc.org.uk/software/lwm.html) || [lwm](https://www.archlinux.org/packages/?name=lwm)

*   **Marco** — Оконный менеджер MATE, форк Metacity.

	[https://github.com/mate-desktop/marco](https://github.com/mate-desktop/marco) || [marco](https://www.archlinux.org/packages/?name=marco)

*   **[Metacity](https://en.wikipedia.org/wiki/Metacity "wikipedia:Metacity")** — Этот оконный менеджер стремится быть компактным и стабильным, при этом просто тихо выполнять свою работу и не отвлекать пользователя.

	[http://blogs.gnome.org/metacity/](http://blogs.gnome.org/metacity/) || [metacity](https://www.archlinux.org/packages/?name=metacity)

*   **[Mutter](https://en.wikipedia.org/wiki/Mutter_(window_manager) "wikipedia:Mutter (window manager)")** — Оконный и композитный менеджер для GNOME, основанный на Clutter; использует OpenGL.

	[http://git.gnome.org/browse/mutter/](http://git.gnome.org/browse/mutter/) || [mutter](https://www.archlinux.org/packages/?name=mutter)

*   **[Openbox](/index.php/Openbox "Openbox")** — Очень гибкий в настройке оконный менеджер нового поколения с расширенной поддержкой разнообразных стандартов. Визуальный стиль *box хорошо известен своей минималистичностью. Openbox предоставляет большое количество возможностей для разработчиков тем оформления, чем предыдущие реализации *box.

	[http://openbox.org/wiki/Main_Page](http://openbox.org/wiki/Main_Page) || [openbox](https://www.archlinux.org/packages/?name=openbox)

*   **[pawm](/index.php/Pawm "Pawm")** — Оконный менеджер для X Window system. Он не предоставит вам рабочий стол и не утомит тысячами бесполезных опций. Вместо этого, он включает в себя только те компоненты, которые нужны для запуска ваших приложений X и в то же время имеет простой и дружелюбный интерфейс.

	[http://www.pleyades.net/pawm/](http://www.pleyades.net/pawm/) || [pawm](https://aur.archlinux.org/packages/pawm/)

*   **[PekWM](/index.php/PekWM "PekWM")** — Оконный менеджер, некогда основывавшийся на aewm++, но теперь уже далеко от него ушедший. У него сильно больший набор возможностей, например группировка окон (аналогично Ion, PWM, или Fluxbox), auto-properties, Xinerama, keygrabber с поддержкой наборов ключей и многое другое.

	[http://www.pekwm.org/projects/pekwm](http://www.pekwm.org/projects/pekwm) || [pekwm](https://www.archlinux.org/packages/?name=pekwm)

*   **rio** — Оконный менеджер для X11, схожий с Plan9\. На деле это форк [9wm](https://aur.archlinux.org/packages/9wm/) с некоторыми изменениями. Здесь нет значков, кнопок, заголовков окон, настроек. Поддерживается перемещение, перестройка, удаление (закрытие), сокрытие окон и виртуальных рабочих столов из простого меню. Rio использует все три кнопки мыши и не нацелен на управление с клавиатуры.

	[http://swtch.com/plan9port/](http://swtch.com/plan9port/) || [rio](https://aur.archlinux.org/packages/rio/)

*   **[Sawfish](/index.php/Sawfish "Sawfish")** — Расширяемый оконный менеджер, который использует скриптовый язык наподобие Lisp. Многие высокоуровневые функции также реализованы на Lisp.

	[http://sawfish.wikia.com/wiki/Main_Page](http://sawfish.wikia.com/wiki/Main_Page) || [sawfish](https://aur.archlinux.org/packages/sawfish/)

*   **TinyWM** — Оконный менеджер Tiny, который автор создал, чтобы поупражняться в минимализме. Он может быть весьма полезен в обучении основ построения оконных менеджеров. Включает в себя около 50 строк кода на C. Есть также версия на [python](/index.php/Python_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Python (Русский)"), которая использует python-xlib.

	[http://incise.org/tinywm.html](http://incise.org/tinywm.html) || [tinywm](https://aur.archlinux.org/packages/tinywm/)

*   **[twm](/index.php/Twm "Twm")** — Оконный менеджер для X Window System. Он предоставляет заголовки окон, рамки, несколько способов управления значками, макросы, а также поддержку горячих клавиш

	[http://cgit.freedesktop.org/xorg/app/twm/](http://cgit.freedesktop.org/xorg/app/twm/) || [xorg-twm](https://www.archlinux.org/packages/?name=xorg-twm)

*   **[UWM](https://en.wikipedia.org/wiki/UDE "wikipedia:UDE")** — Оконный менеджер UDE.

	[http://udeproject.sourceforge.net/](http://udeproject.sourceforge.net/) || [ude](https://aur.archlinux.org/packages/ude/)

*   **WindowLab** — Компактный и простой оконный менеджер. Имеет свои отличительные особенности.

	[http://nickgravgaard.com/windowlab/](http://nickgravgaard.com/windowlab/) || [windowlab](https://aur.archlinux.org/packages/windowlab/)

*   **[Window Maker](/index.php/Window_Maker "Window Maker")** — Оконный менеджер для X11, изначально разработанный для поддержки интеграции для GNUstep Desktop Environment. Везде, где возможно, он повторяет элегантный стиль графического интерфейса NEXTSTEP. Он быстрый, обладает широкими возможностями, прост в настройке и использовании. Это свободное ПО, созданное благодаря вкладу разработчиков со всего мира.

	[http://windowmaker.org/](http://windowmaker.org/) || [windowmaker](https://aur.archlinux.org/packages/windowmaker/)

*   **WM2** — Оконный менеджер для X. Он предоставляет необычный стиль оформления окон и настолько скромную функциональность, насколько его автору кажется приемлемым для оконного менеджера. wm2 ненастраиваемый: вы можете только редактировать исходный код и пересобирать его. Он точно не для тех, кому нужен дружелюбный оконный менеджер.

	[http://www.all-day-breakfast.com/wm2/](http://www.all-day-breakfast.com/wm2/) || [wm2](https://aur.archlinux.org/packages/wm2/)

*   **[Xfwm](/index.php/Xfwm "Xfwm")** — Оконный менеджер [Xfce](/index.php/Xfce "Xfce") управляет отображением окон на экране, предоставляет привлекательное оформление окон, управляет виртуальными рабочими столами и умеет работать с несколькими экранами. Предоставляет собственный композитный режим (благодаря расширению X.Org Composite) для прозрачности и теней. Оконный менеджер Xfce также включает редактор сочетаний клавиш для команд пользователя, а также панель настроек для конфигурирования.

	[http://www.xfce.org/projects/xfwm4/](http://www.xfce.org/projects/xfwm4/) || [xfwm4](https://www.archlinux.org/packages/?name=xfwm4)

### Фреймовые оконные менеджеры

*   **[Bspwm (Русский)](/index.php/Bspwm_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Bspwm (Русский)")** — Фреймовый оконный менеджер, который предоставляет окна как листья бинарного дерева. Есть поддержка EWMH и нескольких мониторов, а еще он настраивается и управляется посредством сообщений.

	[https://github.com/baskerville/bspwm](https://github.com/baskerville/bspwm) || [bspwm](https://www.archlinux.org/packages/?name=bspwm)

*   **dswm** — Оконный менеджер Deep Space является ответвлением от [Stumpwm](/index.php/Stumpwm "Stumpwm").

	[https://github.com/dss-project/dswm](https://github.com/dss-project/dswm) || [dswm](https://aur.archlinux.org/packages/dswm/)

*   **[Herbstluftwm](/index.php/Herbstluftwm "Herbstluftwm")** — Фреймовый оконный менеджер для X11, использующий Xlib и Glib. Размещение фреймов основано на принципе разделения областей экрана на подфреймы, которые, в свою очередь, также могут быть разделены снова (все как в i3/musca). Тэги (виртуальные рабочие столы) могут быть добавлены или убраны "на лету". Каждый тэг имеет собственную схему размещения. Только один тег может быть отображен на каждом мониторе, но, в целом, теги независимы от экранов (как в xmonad). Он настраивается в рантайме посредством IPC-вызовов от herbstclient. Поэтому файл настроек — это просто скрипт, который запускается при старте системы (как в to wmii/musca).

	[http://herbstluftwm.org](http://herbstluftwm.org) || [herbstluftwm](https://www.archlinux.org/packages/?name=herbstluftwm)

*   **howm** — Легкий фреймовый оконный менеджер для X11, который подражает vi, предлагая для своего управления операторы, движения и режимы. Настройка выполняется в заголовочном файле `config.h`.

	[https://github.com/HarveyHunt/howm](https://github.com/HarveyHunt/howm) || [howm-x11](https://aur.archlinux.org/packages/howm-x11/)

*   **[Ion3](/index.php/Ion3 "Ion3")** — Фреймовые оконный менеджер с поддержкой вкладок для X11, разработанный для управления с клавиатуры. Он был одним из первых в новой волне фреймовых оконных менеджеров (вместе с которым следовал LarsWM, имеющий несколько иной подход) и с тех пор относится к несколько другой категории оконных менеджеров X11\. Он использует Lua как встроенный интерпретатор, который выполняет всю настройку.

	[http://tuomov.iki.fi/software](http://tuomov.iki.fi/software) || [ion3](https://aur.archlinux.org/packages/ion3/)

*   **[Notion](/index.php/Notion "Notion")** — Фреймовый оконный менеджер с поддержкой вкладок для X Window System.
    *   Фреймы: вы разделяете экран на неперекрывающиеся фреймы. Каждое окно занимает целиком один фрейм.
    *   Вкладки: фрейм может иметь несколько окон внутри, но отображается всегда только одно — окно текущей вкладки.
    *   Статичность: большинство фреймовых менеджеров динамические, что значит, что они автоматически изменяют размер и передвигают фреймы при появлении и исчезновении окон. Notion, однако, не делает этого самостоятельно.

	Notion — форк Ion3.

	[http://notion.sf.net/](http://notion.sf.net/) || [notion](https://www.archlinux.org/packages/?name=notion)

*   **[Ratpoison](/index.php/Ratpoison "Ratpoison")** — Простой оконный менеджер без объемных зависимостей, ненужных эффектов, и декораций окон. Ratpoison настраивается в обычном текстовом файле. Информационная панель в Ratpoison несколько необычная, и показывается только по необходимости. Она предоставляет возможность запуска приложений и отображает уведомления. Ratpoison не включает в себя системный трей.

	[http://www.nongnu.org/ratpoison/](http://www.nongnu.org/ratpoison/) || [ratpoison](https://www.archlinux.org/packages/?name=ratpoison)

*   **[Stumpwm](/index.php/Stumpwm "Stumpwm")** — Фреймовый оконный менеджер для X11, нацеленный на управление с клавиатуры, и написанный целиком на Common Lisp. Stumpwm старается одновременно быть гибок в настройке и кастомизации, и при этом визуально минималистичен. Различные хуки позволяют подключить вашу собственную функциональность, а сам менеджер может быть перенастроен и перезагружен без полного перезапуска. Здесь нет декораций окон, значков, кнопок и системного трея. Информационная панель может быть настроена для постоянного отображения, либо появляться только по требованию.

	[http://www.nongnu.org/stumpwm/](http://www.nongnu.org/stumpwm/) || [stumpwm-git](https://aur.archlinux.org/packages/stumpwm-git/)

*   **[subtle](/index.php/Subtle "Subtle")** — Фреймовый оконный менеджер с несколько нестандартным подходом.

	[http://subforge.org/projects/subtle](http://subforge.org/projects/subtle) || [subtle](https://aur.archlinux.org/packages/subtle/)

*   **[WMFS](/index.php/WMFS "WMFS")** — Оконный менеджер From Scratch (*"созданный с нуля"*) — легкий и гибкий в настройке фреймовый оконный менеджер для X. Поддерживает шрифты Xft (FreeType), совместим со спецификациями EWMH, Xinerama и [xrandr](/index.php/Xrandr "Xrandr"). WMFS может управляться vi-подобными командами (ViWMFS).

	[https://github.com/xorg62/wmfs](https://github.com/xorg62/wmfs) || [wmfs](https://aur.archlinux.org/packages/wmfs/)

*   **[WMFS](/index.php/WMFS2 "WMFS2")** — Последователь WMFS, обратно с ним несовместимый. Он еще более минималистичен, но в него были добавлены и некоторые новые особенности.

	[https://github.com/xorg62/wmfs](https://github.com/xorg62/wmfs) || [wmfs2-git](https://aur.archlinux.org/packages/wmfs2-git/)

### Динамические оконные менеджеры

*   **[awesome](/index.php/Awesome_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Awesome (Русский)")** — Гибко настраиваемый с помощью скриптового интерпретатора Lua оконный менеджер для X нового поколения, очень быстрый и расширяемый. Выпускается под лицензией GNU GPLv2\. Имеет встроенные системный трей, панель информации и панель запуска приложений. Доступно множество расширений, написанных на Lua. Awesome использует XCB вместо Xlib, что дает лучшую производительность.

	[http://awesome.naquadah.org/](http://awesome.naquadah.org/) || [awesome](https://www.archlinux.org/packages/?name=awesome)

*   **[catwm](/index.php/Catwm "Catwm")** — Компактный оконный менеджер, даже более простой чем dwm, написанный на C. Настройка выполняется редактированием заголовочного файла config.h и перекомпиляцией.

	[https://github.com/pyknite/catwm](https://github.com/pyknite/catwm) || [catwm-git](https://aur.archlinux.org/packages/catwm-git/)

*   **[dwm](/index.php/Dwm "Dwm")** — Оконный менеджер Dynamic Window Manager для X. Управляет окнами в фреймовом, полноэкранном и стековом режимах. Все схемы размещения могут быть изменены динамически. Не включает в себя трей или панель запуска, хотя неплохо интегрируется с dmenu (все-таки, у них один автор). Настраивается модификацией кода C с последующей перекомпиляцией.

	[http://dwm.suckless.org/](http://dwm.suckless.org/) || [dwm](https://aur.archlinux.org/packages/dwm/)

*   **[echinus](/index.php/Echinus "Echinus")** — Простой и легкий фреймовый и стековый оконный менеджер для X11\. Изначально являясь форком dwm с более простой настройкой, echinus стал полноценным репарентинговым оконным менеджером с поддержкой EWMH. Имеет панель задач [ourico](https://aur.archlinux.org/packages/ourico/), совместимую с EWMH.

	[http://plhk.ru](http://plhk.ru) || [echinus](https://aur.archlinux.org/packages/echinus/)

*   **euclid-wm** — Простой и легкий фреймовый и стековый оконный менеджер для X11 с поддержкой сворачивания окон. Настройки и сочетания клавиш задаются в текстовом файле. Изначально являясь форком *dwm* с более простой настройкой, он стал полноценным репарентинговым оконным менеджером с поддержкой EWMH. Имеет панель задач [ourico](https://aur.archlinux.org/packages/ourico/), совместимую с EWMH.

	[http://euclid-wm.sourceforge.net/index.php](http://euclid-wm.sourceforge.net/index.php) || [euclid-wm](https://aur.archlinux.org/packages/euclid-wm/)

*   **[i3](/index.php/I3_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "I3 (Русский)")** — Фреймовый оконный менеджер, написанный полностью с нуля. i3 был создан оттого, что wmii, наш любимый оконный менеджер, не предоставлял некоторых возможностей, которые мы хотели (например, работа на нескольких мониторах работала со сбоями), развивался медленно и был сложен в освоении и кастомизации (отсутствовала документация/комментарии в исходном коде). i3 заметно отличается в плане поддержки нескольких экранов и реализации метафоры дерева. Интерфейс Plan 9 не был реализован для более быстрой работы менеджера.

	[http://i3wm.org/](http://i3wm.org/) || [i3-wm](https://www.archlinux.org/packages/?name=i3-wm)

*   **[monsterwm](/index.php/Monsterwm "Monsterwm")** — Легкий и минималистичный, но динамический фреймовый оконный менеджер. Стремится быть настолько компактным, насколько это возможно: на данный момент, вместе с настройками, занимает всего 700 строк кода. Он предоставляет четыре набора схем размещения (вертикальный стек, нижний стек, сетка и полноэкранный) по умолчанию, а также может работать в чисто стековом режиме. Есть поддержка работы на нескольких мониторах. Каждый монитор и виртуальный рабочий стол имеет собственные настройки, отдельные от остальных. Настройка выполняется целиком модификацией исходного кода C, и после нее необходимо перекомпилировать оконный менеджер. Доступно множество патченных версий, которые поддерживаются параллельно основной ветке.

	[https://github.com/c00kiemon5ter/monsterwm](https://github.com/c00kiemon5ter/monsterwm) || [monsterwm-git](https://aur.archlinux.org/packages/monsterwm-git/)

*   **[FrankenWM](/index.php/FrankenWM "FrankenWM")** — Продолжение *monsterwm* с правильно реализованным стековым режимом. Из добавленных возможностей: новые схемы размещения (fibonacci, equal stack, dual stack), рамки и отступы можно настраивать, сворачивание/разворачивание отдельных окон, возможность показать/спрятать все окна и прочее

	[https://github.com/sulami/FrankenWM](https://github.com/sulami/FrankenWM) || [frankenwm-git](https://aur.archlinux.org/packages/frankenwm-git/)

*   **[Musca](/index.php/Musca "Musca")** — Простой динамический оконный менеджер для X, с возможностями, взятыми из *ratpoison* и *dwm*. По умолчанию Musca работает как фреймовый оконный менеджер. Пользователь определяет, как экран разбивается на неперекрывающиеся фреймы (при этом не ограничен в схеме размещения). Окна приложений всегда целиком заполняют свой фрейм, за исключением временных и всплывающих окон, которые отображаются в стековом режиме над основным окном приложения.

	[http://aerosuidae.net/musca.html](http://aerosuidae.net/musca.html) || [musca](https://aur.archlinux.org/packages/musca/)

*   **[snapwm](/index.php/Snapwm "Snapwm")** — Легкий динамический фреймовый оконный менеджер с упором на простую настройку и возможность выбора. Имеет встроенную панель с переключателем рабочих столов и место для размещения текста. Есть пять фреймовых схем: вертикальная, полноэкранная, горизонтальная, сетка и стековая. Поддерживаются также такие возможности, как, поддержка цветов, независимых рабочих столов, выбор стратегии размещения окон, перезагрузка настроек, прозрачность, интеграция с [dmenu](/index.php/Dmenu "Dmenu"), работа на нескольких экранах и многое другое.

	[https://github.com/moetunes/Nextwm](https://github.com/moetunes/Nextwm) || [snapwm-git](https://aur.archlinux.org/packages/snapwm-git/)

*   **[spectrwm](/index.php/Spectrwm "Spectrwm")** — Компактный динамический фреймовый оконный менеджер для X11, на который в свое время повлияли *xmonad* и *dwm*. Старается занимать как можно меньше места на экране, предоставляя возможность распорядиться им для более важных вещей. Настраивается в текстовом файле. Написан хакерами для хакеров и стремится быть легким, компактным и быстрым. Имеет встроенную строку статуса.

	[https://opensource.conformal.com/wiki/spectrwm](https://opensource.conformal.com/wiki/spectrwm) || [spectrwm](https://www.archlinux.org/packages/?name=spectrwm)

*   **[Qtile](/index.php/Qtile "Qtile")** — Полнофункциональный фреймовый оконный менеджер, написанный на Python. Qtile простой, компактный и расширяемый. Легко создавать собственные схемы размещения, виджеты и встроенные команды. Настраивается этот менеджер также изменением кода Python, таким образом, вы получаете всю мощь языка для удовлетворения любых собственных нужд.

	[https://github.com/qtile/qtile](https://github.com/qtile/qtile) || [qtile-git](https://aur.archlinux.org/packages/qtile-git/)

*   **[Wingo](/index.php/Wingo "Wingo")** — Полнофункциональный гибридный оконный менеджер, который позволяет отображать разные рабочие столы на нескольких экранах, при этом позволяя на одном экране работать во фреймовом режиме, а на другом — в стековом одновременно. Wingo предоставляет также собственный язык для написания скриптов. Поддерживаются темы и пользовательские хуки. Wingo написан на [Go](/index.php/Go_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Go (Русский)") и не имеет зависимостей.

	[https://github.com/BurntSushi/wingo](https://github.com/BurntSushi/wingo) || [wingo-git](https://aur.archlinux.org/packages/wingo-git/)

*   **[wmii](/index.php/Wmii "Wmii")** — Компактный динамический фреймовый оконный менеджер для X11\. Поддерживаются скрипты; есть интерфейс файловой системы 9P, а также поддержка классического и фреймового (Acme-подобного) режимов. Настраивается с помощью скрипта на Bash и [rc (оболочка Plan 9)](http://rc.cat-v.org). Есть встроенная панель статуса и панель запуска приложений, а также системный трей (`witray`).

	[http://wmii.suckless.org/](http://wmii.suckless.org/) || [wmii](https://aur.archlinux.org/packages/wmii/)

*   **[xmonad](/index.php/Xmonad_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xmonad (Русский)")** — Динамический фреймовый оконный менеджер для X11, написанный и настраиваемый на Haskell. В обычном менеджере, вы тратите кучу времени на размещение окон, а затем на их поиск. Xmonad делает жизнь проще, автоматизируя эти процессы. После изменения в настройках, xmonad необходимо перекомпилировать, поэтому должен быть установлен компилятор Haskell (больше 100 Мбайт). Большая библиотека [xmonad-contrib](https://www.archlinux.org/packages/?name=xmonad-contrib) предоставляет множество дополнительных возможностей.

	[http://xmonad.org/](http://xmonad.org/) || [xmonad](https://www.archlinux.org/packages/?name=xmonad)

## Смотрите также

*   [http://www.gilesorr.com/wm/](http://www.gilesorr.com/wm/)