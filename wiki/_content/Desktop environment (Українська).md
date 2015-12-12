# Desktop environment (Українська)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [Display manager](/index.php/Display_manager "Display manager")
*   [Window manager](/index.php/Window_manager "Window manager")
*   [Xorg](/index.php/Xorg "Xorg")
*   [Default applications](/index.php/Default_applications "Default applications")

Оточення Робочого Столу (DE) це повні системи графічного інтерфейсу користувача (GUI).

Оточення робочого столу зазвичай включають, але не обмежуються цим:

*   Віджети
*   Панелі керування/Панелі
*   Аплети
*   Додатки
*   Значки
*   Шпалери
*   Віконний менеджер

## Contents

*   [1 X Сервер](#X_.D0.A1.D0.B5.D1.80.D0.B2.D0.B5.D1.80)
*   [2 Встановлення Оточення Робочого Столу](#.D0.92.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.BD.D1.8F_.D0.9E.D1.82.D0.BE.D1.87.D0.B5.D0.BD.D0.BD.D1.8F_.D0.A0.D0.BE.D0.B1.D0.BE.D1.87.D0.BE.D0.B3.D0.BE_.D0.A1.D1.82.D0.BE.D0.BB.D1.83)
    *   [2.1 Встановлення KDE в двох словах](#.D0.92.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.BD.D1.8F_KDE_.D0.B2_.D0.B4.D0.B2.D0.BE.D1.85_.D1.81.D0.BB.D0.BE.D0.B2.D0.B0.D1.85)
        *   [2.1.1 Пакети KDE](#.D0.9F.D0.B0.D0.BA.D0.B5.D1.82.D0.B8_KDE)
    *   [2.2 Встановлення GNOME в двох словах](#.D0.92.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.BD.D1.8F_GNOME_.D0.B2_.D0.B4.D0.B2.D0.BE.D1.85_.D1.81.D0.BB.D0.BE.D0.B2.D0.B0.D1.85)
        *   [2.2.1 Пакети GNOME](#.D0.9F.D0.B0.D0.BA.D0.B5.D1.82.D0.B8_GNOME)
    *   [2.3 Встановлення Xfce в двох словах](#.D0.92.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.BD.D1.8F_Xfce_.D0.B2_.D0.B4.D0.B2.D0.BE.D1.85_.D1.81.D0.BB.D0.BE.D0.B2.D0.B0.D1.85)
        *   [2.3.1 Пакети Xfce](#.D0.9F.D0.B0.D0.BA.D0.B5.D1.82.D0.B8_Xfce)
    *   [2.4 Встановлення Enlightenment в двох словах](#.D0.92.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.BD.D1.8F_Enlightenment_.D0.B2_.D0.B4.D0.B2.D0.BE.D1.85_.D1.81.D0.BB.D0.BE.D0.B2.D0.B0.D1.85)
        *   [2.4.1 Enlightenment розробницький випуск 16](#Enlightenment_.D1.80.D0.BE.D0.B7.D1.80.D0.BE.D0.B1.D0.BD.D0.B8.D1.86.D1.8C.D0.BA.D0.B8.D0.B9_.D0.B2.D0.B8.D0.BF.D1.83.D1.81.D0.BA_16)
        *   [2.4.2 Enlightenment розробницький випуск 17](#Enlightenment_.D1.80.D0.BE.D0.B7.D1.80.D0.BE.D0.B1.D0.BD.D0.B8.D1.86.D1.8C.D0.BA.D0.B8.D0.B9_.D0.B2.D0.B8.D0.BF.D1.83.D1.81.D0.BA_17)
        *   [2.4.3 Пакети E17](#.D0.9F.D0.B0.D0.BA.D0.B5.D1.82.D0.B8_E17)
*   [3 Налаштування Оточення Робочого Столу](#.D0.9D.D0.B0.D0.BB.D0.B0.D1.88.D1.82.D1.83.D0.B2.D0.B0.D0.BD.D0.BD.D1.8F_.D0.9E.D1.82.D0.BE.D1.87.D0.B5.D0.BD.D0.BD.D1.8F_.D0.A0.D0.BE.D0.B1.D0.BE.D1.87.D0.BE.D0.B3.D0.BE_.D0.A1.D1.82.D0.BE.D0.BB.D1.83)
    *   [3.1 KDE](#KDE)
    *   [3.2 GNOME](#GNOME)
    *   [3.3 Xfce](#Xfce)
    *   [3.4 E17](#E17)
*   [4 Зовнішні ресурси](#.D0.97.D0.BE.D0.B2.D0.BD.D1.96.D1.88.D0.BD.D1.96_.D1.80.D0.B5.D1.81.D1.83.D1.80.D1.81.D0.B8)

## X Сервер

Для встановлення/використання DE, вам потрібен X(org). Якщо ви дивитесь це Вікі через графічний браузер такий як Firefox чи Konqueror, тоді ви скоріше за все X і DE вже встановлено. Однак, якщо ви встановили Arch використовуючи базовий CD і читаєте це Вікі з терміналу (в брайзері по типу links2), мабуть X у вас не встановлено. Для встановлення X, наберіть наступне в консолі:

```
# pacman -S xorg

```

Для більш детальної інформації про X, дивись статтю про [Xorg](/index.php?title=Xorg_(%D0%A3%D0%BA%D1%80%D0%B0%D1%97%D0%BD%D1%81%D1%8C%D0%BA%D0%B0)&action=edit&redlink=1 "Xorg (Українська) (page does not exist)").

## Встановлення Оточення Робочого Столу

Багато доступних DE для Linux; ось лише декылька з них:

*   [KDE](/index.php?title=KDE_(%D0%A3%D0%BA%D1%80%D0%B0%D1%97%D0%BD%D1%81%D1%8C%D0%BA%D0%B0)&action=edit&redlink=1 "KDE (Українська) (page does not exist)")
*   [GNOME](/index.php/GNOME_(%D0%A3%D0%BA%D1%80%D0%B0%D1%97%D0%BD%D1%81%D1%8C%D0%BA%D0%B0) "GNOME (Українська)")
*   [Xfce](/index.php/Xfce_(%D0%A3%D0%BA%D1%80%D0%B0%D1%97%D0%BD%D1%81%D1%8C%D0%BA%D0%B0) "Xfce (Українська)")
*   [Enlightenment](/index.php?title=Enlightenment_(%D0%A3%D0%BA%D1%80%D0%B0%D1%97%D0%BD%D1%81%D1%8C%D0%BA%D0%B0)&action=edit&redlink=1 "Enlightenment (Українська) (page does not exist)")

### Встановлення KDE в двох словах

KDE можна встановити просто увівши команду з теміналу як супер користувач (root):

```
# pacman -S kde

```

Спочатку вам зададуть запитання чи ви хочете встановити всю групу пакетів KDE. Десь біля 270MB завантаження <sub>(4-2006 для KDE 3.5.2)</sub>. якщо ви не хочете встановлювати всю групу, натисніть 'n', і у вас запитають які KDE пакети вам потрібні. Нижче список усіх пакетів KDE і деталі про них.

#### Пакети KDE

*   arts – Звуковий двигун KDE
*   gwenview – Перегляд зображень KDE
*   kde-Common – Загальні пакети KDE
*   kdeaccessibility – Можливості доступності KDE
*   kdeaddons – Плагіни для konq, noatun, тощо.
*   kdeadmin – Пакети для адміністрування; включає менеджер користувачів
*   kdeartwork – Оформлення (Кольори, теми, малюнки, заставки, тощо.)
*   kdebase – Базові пакети KDE. НЕОБХІДНО
*   kdebindings – Прив’язка кнопок KDE (для розробників)
*   kdeedu – Навчальні програми KDE
*   kdegames – Ігри для KDE
*   kdegraphics – Програми пов’язані з графікою
*   kdelibs – Бібліотеки KDE. НЕОБХІДНО
*   kdemultimedia – Включає програми мультимедіа для KDE
*   kdenetwork – пакети пов’язані з мережею KDE, включає kppp, і т.н.
*   kdepim – Управління персональною інформацією; Korganiser, KMail, тощо.
*   kdesdk – Набір розробника програмного забезпечення KDE
*   kdetoys – Маленькі програми та іграшки для KDE; Очі, Кумедна витрата ресурсів (Amusing Misuse of Resources (AMOR))
*   kdeutils – Трошки додаткових програм; ark, kcalc, і т.н.

Для більш детальної інформації дивись [KDE](/index.php?title=KDE_(%D0%A3%D0%BA%D1%80%D0%B0%D1%97%D0%BD%D1%81%D1%8C%D0%BA%D0%B0)&action=edit&redlink=1 "KDE (Українська) (page does not exist)").

### Встановлення GNOME в двох словах

Ви можете встановити GNOME простим набором команди в root терміналі:

```
# pacman -S gnome

```

Як і в KDE, спершу у вас запитають чи хочете ви встановити вміст всієї групи GNOME. Повний розмір завантаження для встановлення GNOME 125.6MB <sub>(станом на 12-2006)</sub>. Якщо ні, вам прийдеться вибрати пакети для встановлення. Нижче список пакетів GNOME, і пояснення до них.

#### Пакети GNOME

*   gnome-icon-theme – Тема значків для GNOME
*   control-center – Центр керування GNOME
*   epiphany – Веб-брайзер GNOME
*   gnome-applets – Аплети панелі
*   gnome-backgrounds – Тло робочого столу
*   gnome-common – Загальні файли GNOME
*   gnome-desktop – Робочий стіл GNOME
*   gnome-media – GNOME Media Tools
*   gnome-mime-data – Mime Data for GNOME
*   gnome-panel – Панель GNOME
*   gnome-session – Управління сесіями GNOME
*   gnome-themes – Теми для GNOME
*   gnome2-user-docs – Документація користувача GNOME
*   metacity – Віконний Менеджер GNOME
*   nautilus – Файловий менеджер GNOME
*   vte – Віджет терміналу GNOME
*   yelp – Переглядач допомоги GNOME

Для більш детальної інформації дивись [GNOME](/index.php/GNOME_(%D0%A3%D0%BA%D1%80%D0%B0%D1%97%D0%BD%D1%81%D1%8C%D0%BA%D0%B0) "GNOME (Українська)").

### Встановлення Xfce в двох словах

Можна встановити Xfce простим набором команди в root терміналі:

```
# pacman -S xfce4

```

Як і в обох KDE і GNOME, встановлення запитає чи хочете встановити всю групу пакетів Xfce. Загальний об’єм завантаження для Xfce 44.9MB <sub>(станом на 4-2006)</sub>. Якщо виберете встановлення не всієї групи, дивись нижче список для деталей.

#### Пакети Xfce

*   gtk-xfce-engine – Графічний двигун Xfce-GTK
*   libxfce4mcs – Підтримка управління налаштування Xfce.
*   libxfce4util – Функції без-GUI для Xfce
*   libxfcegui4 – GTK віджети для Xfce
*   orage – Календар Xfce
*   thunar – Менеджер файлів
*   xfce-mcs-manager – Менеджер налаштувань.
*   xfce-mcs-plugins – Плагіни для менеджера налаштувань
*   xfce-utils – startxfce4 скрипт, запуск діалогу, тощо.
*   xfce4-appfinder – Пошук застосунків
*   xfce4-iconbox – Просте управління застосунками, схожий до панелі задач.
*   xfce4-mixer – Плагін керування гучністю для панелі
*   xfce4-panel – Панель Xfce
*   xfce4-session – Менеджер сесій
*   xfce4-systray – Плагін системного лотка для панелі
*   xfce4-toys – Маленькі іграшки для Xfce
*   xfce4-trigger-launcher – Тригер запуску плагіну панелі
*   xfdesktop – Дозволяє шпалери робочого столу, значки та меню
*   xfprint – Пакет друку Xfce
*   xfwm4 – Менеджер вікон Xfce
*   xfwm4-themes – Теми для менеджера вікон Xfce

Для більш детальної інформації дивись [Xfce](/index.php/Xfce_(%D0%A3%D0%BA%D1%80%D0%B0%D1%97%D0%BD%D1%81%D1%8C%D0%BA%D0%B0) "Xfce (Українська)").

### Встановлення Enlightenment в двох словах

Enlightenment має дві версії:

*   DR16, старший код, спершу вишущений в 2000 році, і остаточно в 2003.
*   DR17, новіший, все ще в pre-alpha (хоча є досить стиабільним).

#### Enlightenment розробницький випуск 16

Ви можете встановити Enlightenment DR16 просто набравши команду у root терміналі:

```
# pacman -S enlightenment

```

Здається E16 лише віконний менеджер, а не ціле Оточення робочого столу; Дивись [Window Manager](/index.php/Window_Manager_(%D0%A3%D0%BA%D1%80%D0%B0%D1%97%D0%BD%D1%81%D1%8C%D0%BA%D0%B0) "Window Manager (Українська)") для деталей.

#### Enlightenment розробницький випуск 17

Ви можете встановити Enlightenment DR17 з репозиторія спільноти, набравши наступне в root терміналі:

```
# pacman -S e17-svn

```

Встановлення додаткових пакетів:

```
# pacman -S e17-extra-svn

```

Enlightenment DR17 має групи пакетів подібно до KDE, GNOME і Xfce. Нижче список пакетів для групи E17.

#### Пакети E17

*   e – Менеджер вікон
*   ecore – Абстракція подій і модульна зручність
*   edb-devel – Пакер розробника E бази данних
*   edje – Бібліотека абстракції інтерфейсу і інструментів
*   eet – Бібліотека розподілу контейнерів і інструментів
*   embryo – Вбідована скриптова мова для enlightenment
*   emotion – Бібліотека смарт-об’єктів відео для evas
*   entice – Переглядач зображень
*   entrance – E Менеджер дисплею
*   epeg – Для мініатюр JPEG’а
*   epsilon – Бібліотека мініатюр Freedesktop.org
*   esmart – Колекція смарт об’єктів evas
*   etox – Компонування і обробка тексту
*   evas – Бібліотека Canvas
*   ewl – Бібліотека віджет Enlightenment’а
*   imlib2-devel – Візуалізація зображень і бібліотека обробки
*   imlib2_loaders – Завантажувач для Image Rendering and Manipulation Library

Для більшої інформації дивись [Enlightenment](/index.php?title=Enlightenment_(%D0%A3%D0%BA%D1%80%D0%B0%D1%97%D0%BD%D1%81%D1%8C%D0%BA%D0%B0)&action=edit&redlink=1 "Enlightenment (Українська) (page does not exist)") і/або [E17](/index.php?title=E17_(%D0%A3%D0%BA%D1%80%D0%B0%D1%97%D0%BD%D1%81%D1%8C%D0%BA%D0%B0)&action=edit&redlink=1 "E17 (Українська) (page does not exist)").

## Налаштування Оточення Робочого Столу

### KDE

Після встановлення kdeadmin, наберіть в консолі 'kcontrol' (kde3mod), або в K Menu → Системні настройки (KDE 4).

### GNOME

Використовуйте меню параметрів щоб розкрити все що ви забажаєте змінити.

### Xfce

Клацніть правою кнопкою миші на робочому столі і перемістіть вниз до меню настройок. Тут ви можете відкрити менеджер налаштувань.

### E17

Перейдіть по меню E17 (або клійніть лівою кнопкою миші на робочому столі), і перейдіть Налаштування → Панель налаштування.

## Зовнішні ресурси

*   [Вікіпедія:Оточення робочого столу](http://uk.wikipedia.org/wiki/Робоче_середовище)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Desktop_environment_(Українська)&oldid=411569](https://wiki.archlinux.org/index.php?title=Desktop_environment_(Українська)&oldid=411569)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Desktop environments (Українська)](/index.php/Category:Desktop_environments_(%D0%A3%D0%BA%D1%80%D0%B0%D1%97%D0%BD%D1%81%D1%8C%D0%BA%D0%B0) "Category:Desktop environments (Українська)")
*   [Українська](/index.php/Category:%D0%A3%D0%BA%D1%80%D0%B0%D1%97%D0%BD%D1%81%D1%8C%D0%BA%D0%B0 "Category:Українська")