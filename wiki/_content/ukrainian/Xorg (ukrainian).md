Related articles

*   [Autostarting](/index.php/Autostarting "Autostarting")
*   [Display manager](/index.php/Display_manager "Display manager")
*   [Window manager](/index.php/Window_manager "Window manager")
*   [Font configuration](/index.php/Font_configuration "Font configuration")
*   [Cursor themes](/index.php/Cursor_themes "Cursor themes")
*   [Desktop environment](/index.php/Desktop_environment "Desktop environment")
*   [Wayland](/index.php/Wayland "Wayland")
*   [xinit](/index.php/Xinit "Xinit")
*   [xrandr](/index.php/Xrandr "Xrandr")

З [http://www.x.org/wiki/](http://www.x.org/wiki/):

	Проект X.Org забезпечує реалізацію відкритого коду [X Window System](https://uk.wikipedia.org/wiki/X_Window_System/). Робота з розробки здійснюється разом з спільнотою freedesktop.org. Фундація X.Org є освітньою некомерційною корпорацією, Рада якої, керує цією роботою.

**Xorg** (зазвичай називають просто **X**) є найпопулярнішою віконною системою серед користувачів Linux. Її поширеність призвела до того, що вона стала необхідною умовою для додатків з графічним інтерфейсом, що призвело до масового використання у більшості дистрибутивів. Дивіться статтю [X Window System](https://uk.wikipedia.org/wiki/X_Window_System/) у Вікіпедії або перейдіть на [веб-сайт Xorg](http://www.x.org/wiki/), щоб дізнатися більше.

## Contents

*   [1 Встановлення](#Встановлення)
    *   [1.1 Встановлення драйверів](#Встановлення_драйверів)
    *   [1.2 AMD](#AMD)
*   [2 Запуск](#Запуск)
*   [3 Конфігурація](#Конфігурація)
    *   [3.1 Використання .conf файлів](#Використання_.conf_файлів)
    *   [3.2 Використання xorg.conf](#Використання_xorg.conf)
*   [4 Пристрої введення](#Пристрої_введення)
    *   [4.1 Ідентифікація введення](#Ідентифікація_введення)
    *   [4.2 Прискорення миші](#Прискорення_миші)
    *   [4.3 Додаткові кнопки миші](#Додаткові_кнопки_миші)
    *   [4.4 Тачпад](#Тачпад)
    *   [4.5 Тачскрін](#Тачскрін)
    *   [4.6 Налаштування клавіатури](#Налаштування_клавіатури)
*   [5 Налаштування монітору](#Налаштування_монітору)
    *   [5.1 Ручне налаштування](#Ручне_налаштування)
    *   [5.2 Декілька моніторів](#Декілька_моніторів)
        *   [5.2.1 Більш ніж одна графічна карта](#Більш_ніж_одна_графічна_карта)
    *   [5.3 Розмір екрану та DPI](#Розмір_екрану_та_DPI)
        *   [5.3.1 Ручне налаштування DPI](#Ручне_налаштування_DPI)
            *   [5.3.1.1 Пропрієтарний драйвер NVIDIA](#Пропрієтарний_драйвер_NVIDIA)
            *   [5.3.1.2 Застереження, щодо ручного налаштування DPI](#Застереження,_щодо_ручного_налаштування_DPI)
    *   [5.4 Управління енергозбереженням монітора](#Управління_енергозбереженням_монітора)
*   [6 Композит](#Композит)
    *   [6.1 Список композитних менеджерів](#Список_композитних_менеджерів)
*   [7 Поради та підказки](#Поради_та_підказки)
    *   [7.1 Автоматизація](#Автоматизація)
    *   [7.2 Nested X session](#Nested_X_session)
    *   [7.3 Starting GUI programs remotely](#Starting_GUI_programs_remotely)
    *   [7.4 On-demand disabling and enabling of input sources](#On-demand_disabling_and_enabling_of_input_sources)
    *   [7.5 Killing application with hotkey](#Killing_application_with_hotkey)
    *   [7.6 Block TTY access](#Block_TTY_access)
    *   [7.7 Prevent a user from killing X](#Prevent_a_user_from_killing_X)
*   [8 Troubleshooting](#Troubleshooting)
    *   [8.1 General](#General)
    *   [8.2 Black screen, No protocol specified.., Resource temporarily unavailable for all or some users](#Black_screen,_No_protocol_specified..,_Resource_temporarily_unavailable_for_all_or_some_users)
    *   [8.3 DRI with Matrox cards stopped working](#DRI_with_Matrox_cards_stopped_working)
    *   [8.4 Frame-buffer mode problems](#Frame-buffer_mode_problems)
    *   [8.5 Program requests "font '(null)'"](#Program_requests_"font_'(null)'")
    *   [8.6 Recovery: disabling Xorg before GUI login](#Recovery:_disabling_Xorg_before_GUI_login)
    *   [8.7 X clients started with "su" fail](#X_clients_started_with_"su"_fail)
    *   [8.8 X failed to start: Keyboard initialization failed](#X_failed_to_start:_Keyboard_initialization_failed)
    *   [8.9 Rootless Xorg](#Rootless_Xorg)
        *   [8.9.1 Broken redirection](#Broken_redirection)
    *   [8.10 A green screen whenever trying to watch a video](#A_green_screen_whenever_trying_to_watch_a_video)
    *   [8.11 SocketCreateListener error](#SocketCreateListener_error)
    *   [8.12 Invalid MIT-MAGIC-COOKIE-1 key when trying to run a program as root](#Invalid_MIT-MAGIC-COOKIE-1_key_when_trying_to_run_a_program_as_root)
*   [9 See also](#See_also)

## Встановлення

Xorg може бути встановлена з пакунком [xorg-server](https://www.archlinux.org/packages/?name=xorg-server).

Крім того, деякі пакети з групи [xorg-apps](https://www.archlinux.org/groups/x86_64/xorg-apps/) необхідні для певних задач налаштування, вони вказані у відповідних розділах.

Нарешті, також доступна група [xorg](https://www.archlinux.org/groups/x86_64/xorg/), яка включає в себе серверні пакунки Xorg, пакунки з групи [xorg-apps](https://www.archlinux.org/groups/x86_64/xorg-apps/) і шрифтів.

**Tip:** Зазвичай встановлюють [менеджер вікон](/index.php/Display_manager "Display manager") або [середовище стільниці](/index.php/Desktop_environment "Desktop environment") для доповнення X.

### Встановлення драйверів

Ядро Linux включає відео драйвери з відкритим вихідним кодом і підтримку апаратно прискорюваних фрейм-буферів. Однак для підтримки OpenGL і 2D прискорення в X11 потрібне втручання користувача.

По-перше, ідентифікуйте вашу картку:

```
$ lspci | grep -e VGA -e 3D

```

Потім встановіть відповідний драйвер. Ви можете переглянути в базі даних пакунків повний список драйверів відео з відкритим вихідним кодом:

```
$ pacman -Ss xf86-video

```

Xorg автоматично шукає встановлені драйвери:

*   Якщо він не може знайти спеціальний драйвер, встановлений для апаратних засобів (перелічених нижче), він спочатку шукає *fbdev* ([xf86-video-fbdev](https://www.archlinux.org/packages/?name=xf86-video-fbdev)).
*   Якщо це не знайдено, він шукає *vesa* ([xf86-video-vesa](https://www.archlinux.org/packages/?name=xf86-video-vesa)), загальний драйвер, який обробляє велику кількість наборів мікросхем, але не містить жодного 2D або 3D-прискорення.
*   Якщо *vesa* не знайдено, Xorg повернеться до [налаштувань ядра](/index.php/Kernel_mode_setting "Kernel mode setting"), та включить GLAMOR-прискорення (дивись [modesetting(4)](https://jlk.fjfi.cvut.cz/arch/manpages/man/modesetting.4)).

Для того, щоб прискорення відео працювало, і часто для виявлення всіх режимів, які може встановити графічний процесор, потрібний належний драйвер відео:

| Brand | Type | Driver | OpenGL | OpenGL ([multilib](/index.php/Multilib "Multilib")) | Documentation |
| AMD / ATI | Open source | [xf86-video-amdgpu](https://www.archlinux.org/packages/?name=xf86-video-amdgpu) | [mesa](https://www.archlinux.org/packages/?name=mesa) | [lib32-mesa](https://www.archlinux.org/packages/?name=lib32-mesa) | [AMDGPU](/index.php/AMDGPU "AMDGPU") |
| [xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati) | [ATI](/index.php/ATI "ATI") |
| Proprietary | [catalyst](https://aur.archlinux.org/packages/catalyst/) | [catalyst-libgl](https://aur.archlinux.org/packages/catalyst-libgl/) | [lib32-catalyst-libgl](https://aur.archlinux.org/packages/lib32-catalyst-libgl/) | [AMD Catalyst](/index.php/AMD_Catalyst "AMD Catalyst") |
| Intel | Open source | [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) | [mesa](https://www.archlinux.org/packages/?name=mesa) | [lib32-mesa](https://www.archlinux.org/packages/?name=lib32-mesa) | [Intel graphics](/index.php/Intel_graphics "Intel graphics") |
| NVIDIA | Open source | [xf86-video-nouveau](https://www.archlinux.org/packages/?name=xf86-video-nouveau) | [mesa](https://www.archlinux.org/packages/?name=mesa) | [lib32-mesa](https://www.archlinux.org/packages/?name=lib32-mesa) | [Nouveau](/index.php/Nouveau "Nouveau") |
| Proprietary | [nvidia](https://www.archlinux.org/packages/?name=nvidia) | [nvidia-utils](https://www.archlinux.org/packages/?name=nvidia-utils) | [lib32-nvidia-utils](https://www.archlinux.org/packages/?name=lib32-nvidia-utils) | [NVIDIA](/index.php/NVIDIA "NVIDIA") |
| [nvidia-390xx](https://www.archlinux.org/packages/?name=nvidia-390xx) | [nvidia-390xx-utils](https://www.archlinux.org/packages/?name=nvidia-390xx-utils) | [lib32-nvidia-390xx-utils](https://www.archlinux.org/packages/?name=lib32-nvidia-390xx-utils) |
| [nvidia-340xx](https://www.archlinux.org/packages/?name=nvidia-340xx) | [nvidia-340xx-utils](https://www.archlinux.org/packages/?name=nvidia-340xx-utils) | [lib32-nvidia-340xx-utils](https://www.archlinux.org/packages/?name=lib32-nvidia-340xx-utils) |

**Note:**

*   Для NVIDIA Optimus на ноутбуках, в яких використовується вбудована відеокарта в поєднанні з виділеним GPU, дивіться [NVIDIA Optimus](/index.php/NVIDIA_Optimus "NVIDIA Optimus") або [Bumblebee](/index.php/Bumblebee "Bumblebee").
*   Для графіки Intel 4-го покоління і вище див. [Intel graphics#Installation](/index.php/Intel_graphics#Installation "Intel graphics") для доступних драйверів.

Інші відео-драйвери можуть бути знайдені в групі [xorg-drivers](https://www.archlinux.org/groups/x86_64/xorg-drivers/).

Xorg повинен працювати гладко без пропрієтарних драйверів, які зазвичай потрібні лише для розширених функцій, таких як швидка 3D- візуалізація для ігор. Виняток із цього правила - це останні графічні процесори (особливо графічні процесори NVIDIA), які не підтримуються драйверами з відкритим кодом.

### AMD

| GPU architecture | Radeon cards | Open-source driver | Proprietary driver |
| GCN 4
and newer | [варіанти](https://en.wikipedia.org/wiki/List_of_AMD_graphics_processing_units "wikipedia:List of AMD graphics processing units") | [AMDGPU](/index.php/AMDGPU "AMDGPU") | [AMDGPU PRO](/index.php/AMDGPU_PRO "AMDGPU PRO") |
| GCN 3 | [AMDGPU](/index.php/AMDGPU "AMDGPU") | [Catalyst](/index.php/Catalyst "Catalyst") /
[AMDGPU PRO](/index.php/AMDGPU_PRO "AMDGPU PRO") |
| GCN 2 | [AMDGPU](/index.php/AMDGPU "AMDGPU")* / [ATI](/index.php/ATI "ATI") | [Catalyst](/index.php/Catalyst "Catalyst") |
| GCN 1 | [AMDGPU](/index.php/AMDGPU "AMDGPU")* / [ATI](/index.php/ATI "ATI") | [Catalyst](/index.php/Catalyst "Catalyst") |
| TeraScale 2&3 | HD 5000 - HD 6000 | [ATI](/index.php/ATI "ATI") | [Catalyst](/index.php/Catalyst "Catalyst") |
| TeraScale 1 | HD 2000 - HD 4000 | [Catalyst](/index.php/Catalyst "Catalyst") *застарілий* |
| Older | X1000 and older | *недоступний* |

	*: Експериментальні

## Запуск

Команда [Xorg(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/Xorg.1), як правило, не запускається безпосередньо, замість цього, X-сервер стартує з будь-якого з [менеджерів вікон](/index.php/Display_manager "Display manager") або [xinit](/index.php/Xinit "Xinit").

## Конфігурація

**Note:** Arch типово розміщує файли налаштувань в `/usr/share/X11/xorg.conf.d/`, і в більшості випадків не потрібно додаткового налаштування.

Xorg використовує файл налаштувань`xorg.conf` і файли що закінчуються на `.conf` для початкового налаштування: повний список тек, в яких знаходяться ці файли, можна знайти у [xorg.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xorg.conf.5), разом з детальним поясненням усіх доступних варіантів.

### Використання .conf файлів

Каталог `/etc/X11/xorg.conf.d/` зберігає конфігурацію, специфічну для хоста. Ви можете додавати там конфігураційні файли, але вони повинні мати суфікс `.conf`: файли зчитуються в порядку ASCII, тому, відповідно, їхні імена починаються з `*XX*-` (дві цифри і дефіс, для прикладу: 10 читається перед 20). Ці файли аналізуються сервером X під час запуску і обробляються як частина традиційного конфігураційного файлу `xorg.conf`. Зверніть увагу, що при конфліктній конфігурації цей файл буде оброблено *останнім*. З цієї причини найбільш загальні конфігураційні файли слід упорядковувати першими за назвою. Записи конфігурації у файлі `xorg.conf` обробляються наприкінці.

Приклади налаштування дивіться на [fedora wiki](http://fedoraproject.org/wiki/Input_device_configuration#xorg.conf.d).

### Використання xorg.conf

Xorg також можна налаштувати за допомогою `/etc/X11/xorg.conf` або `/etc/xorg.conf`. Ви також можете створити основу для `xorg.conf` з:

```
# Xorg :0 -configure

```

Це має створити файл `xorg.conf.new` в `/root/`, в який можна скопіювати `/etc/X11/xorg.conf`.

**Tip:** Якщо ви вже запустили X-сервер, використовуйте інший дисплей, наприклад `Xorg :2 -configure`.

Крім того, драйвери пропрієтарних відеокарт можуть постачатися з інструментом для автоматичної настройки Xorg: див. Статтю вашого відео-драйвера, [NVIDIA](/index.php/NVIDIA "NVIDIA") або [AMD Catalyst](/index.php/AMD_Catalyst "AMD Catalyst").

**Note:** Ключові слова файлу конфігурації нечутливі до регістру, символи "_" ігноруються. Більшість рядків (включаючи назви опцій) також нечутливі до регістру, пробілу та символу "_".

## Пристрої введення

Для пристроїв введення даних X-сервер типово використовує драйвер libinput ([xf86-input-libinput](https://www.archlinux.org/packages/?name=xf86-input-libinput)), але [xf86-input-evdev](https://www.archlinux.org/packages/?name=xf86-input-evdev) та відповідні драйвери доступні як альтернатива.[[1]](https://www.archlinux.org/news/xorg-server-1191-is-now-in-extra/)

[Udev](/index.php/Udev "Udev"), яка забезпечується як залежність від systemd, буде виявляти апаратні засоби, і обидва драйвера виступатимуть як драйвер введення для гарячого підключення майже для всіх пристроїв, як це типово визначено у файлах конфігурації `10-quirks.conf` та `40-libinput.conf` за шляхом `/usr/share/X11/xorg.conf.d/`.

Після запуску X-серверу, у файлі журналу відображатиметься, який драйвер буде задіяний для окремих пристроїв (зауважте, що найновіше ім'я файлу журналу може змінюватися):

```
$ grep -e "Using input driver " Xorg.0.log

```

Якщо обидва драйвери не підтримують певний пристрій, встановіть потрібний драйвер з групи [xorg-drivers](https://www.archlinux.org/groups/x86_64/xorg-drivers/). Те ж саме зробіть, якщо ви хочете використовувати інший драйвер.

Щоб вплинути на гаряче підключення, див [#Конфігурація](#Конфігурація).

Для більш конкретних інструкцій див. статтю [libinput](/index.php/Libinput "Libinput"), читайте нижче, або [Fedora wiki](https://fedoraproject.org/wiki/Input_device_configuration).

### Ідентифікація введення

Дивіться [Keyboard input#Identifying keycodes in Xorg](/index.php/Keyboard_input#Identifying_keycodes_in_Xorg "Keyboard input").

### Прискорення миші

Дивіться [Mouse acceleration](/index.php/Mouse_acceleration "Mouse acceleration").

### Додаткові кнопки миші

Дивіться [Mouse buttons](/index.php/Mouse_buttons "Mouse buttons").

### Тачпад

Дивіться [libinput](/index.php/Libinput "Libinput") або [Synaptics](/index.php/Synaptics "Synaptics").

### Тачскрін

Дивіться [Touchscreen](/index.php/Touchscreen "Touchscreen").

### Налаштування клавіатури

Дивіться [Keyboard configuration in Xorg](/index.php/Keyboard_configuration_in_Xorg "Keyboard configuration in Xorg").

## Налаштування монітору

### Ручне налаштування

**Note:**

*   Новіші версії Xorg йдуть з автоконфігуруванням, тому ручна конфігурація не потрібна.
*   Якщо Xorg не може виявити якийсь монітор або знайти автоматичного налаштування, можна використовувати файл конфігурації. Загальний випадок, коли це необхідно, це система, яка завантажується без монітора і автоматично запускає Xorg, або з [віртуальної консолі](/index.php/Automatic_login_to_virtual_console "Automatic login to virtual console") при [вході](/index.php/Start_X_at_login "Start X at login"), або з [менеджеру вікон](/index.php/Display_manager "Display manager").

Для конфігурації без-моніторних систем потрібен драйвер [xf86-video-dummy](https://www.archlinux.org/packages/?name=xf86-video-dummy), [встановіть](/index.php/Install "Install") його та створіть файл конфігурації, подібний до цього:

 `/etc/X11/xorg.conf.d/10-headless.conf` 
```
Section "Monitor"
        Identifier "dummy_monitor"
        HorizSync 28.0-80.0
        VertRefresh 48.0-75.0
        Modeline "1920x1080" 172.80 1920 2040 2248 2576 1080 1081 1084 1118
EndSection

Section "Device"
        Identifier "dummy_card"
        VideoRam 256000
        Driver "dummy"
EndSection

Section "Screen"
        Identifier "dummy_screen"
        Device "dummy_card"
        Monitor "dummy_monitor"
        SubSection "Display"
        EndSubSection
EndSection
```

### Декілька моніторів

Дивіться головну статтю [Multihead](/index.php/Multihead "Multihead") для отримання більшої інформації.

Дивіться також інструкції відповідно до вашого GPU:

*   [NVIDIA#Multiple monitors](/index.php/NVIDIA#Multiple_monitors "NVIDIA")
*   [Nouveau#Dual head](/index.php/Nouveau#Dual_head "Nouveau")
*   [AMD Catalyst#Double Screen (Dual Head / Dual Screen / Xinerama)](/index.php/AMD_Catalyst#Double_Screen_(Dual_Head_/_Dual_Screen_/_Xinerama) "AMD Catalyst")
*   [ATI#Multihead setup](/index.php/ATI#Multihead_setup "ATI")

#### Більш ніж одна графічна карта

Ви повинні визначити правильний драйвер для використання і ввести BusID ваших графічних карт.

```
Section "Device"
    Identifier             "Screen0"
    Driver                 "nouveau"
    BusID                  "PCI:0:12:0"
EndSection

Section "Device"
    Identifier             "Screen1"
    Driver                 "radeon"
    BusID                  "PCI:1:0:0"
EndSection

```

Щоби взнати BusID:

 `$ lspci | grep VGA` 
```
01:00.0 VGA compatible controller: nVidia Corporation G96 [GeForce 9600M GT] (rev a1)

```

Bus ID тут 1:0:0.

### Розмір екрану та DPI

DPI X-сервера визначається наступним чином:

1.  Параметр командного рядка -dpi має найвищий пріоритет.
2.  Якщо це не використовується, параметр DisplaySize у конфігураційному файлі Xorg використовується для виведення DPI, враховуючи дозвіл екрана.
3.  Якщо не заданий параметр DisplaySize, значення розміру монітора використовуються з [DDC](https://en.wikipedia.org/wiki/Display_Data_Channel "wikipedia:Display Data Channel") для виведення DPI, враховуючи дозвіл екрана.
4.  Якщо DDC не визначає розмір, 75 DPI використовуються типово.

Щоб отримати правильну кількість точок на дюйм (DPI), розмір дисплея повинен бути розпізнаний або встановлений. Наявність правильного DPI є особливо необхідним, коли потрібні дрібні деталі (наприклад, візуалізація шрифтів). Раніше виробники намагалися створити стандарт для 96 DPI (діагональний монітор розміром 10,3" був би 800x600, монітор 13,2" - 1024x768). В наш час DPI екрану різняться і можуть бути не рівними по горизонталі і вертикалі. Наприклад, 19-дюймовий широкоформатний РК-дисплей на 1440x900 може мати DPI 89x87\. Щоб встановити DPI, сервер Xorg намагається автоматично визначити фізичний розмір екрану монітора за допомогою графічної карти з DDC. ~~Коли сервер Xorg знає фізичний розмір екрану, він зможе встановити правильний DPI в залежності від розміру дозволу.~~

Щоб дізнатися, чи правильно визначено/розраховано розмір дисплея та DPI:

```
$ xdpyinfo | grep -B2 resolution

```

Переконайтеся, що розміри відповідають розміру дисплея. Якщо сервер Xorg не може правильно розрахувати розмір екрану, він типово буде дорівнює 75x75 DPI, і вам доведеться розрахувати його самостійно.

Якщо у вас в документації є інформація про фізичний розмір екрана, вона може бути введена в файл конфігурації Xorg, щоб обчислити відповідний DPI (налаштувати ідентифікатор вашого виводу xrandr) :

```
Section "Monitor"
    Identifier             "DVI-D-0"
    DisplaySize             286 179    # В міліметрах
EndSection

```

Якщо ви бажаєте лише ввести специфікацію вашого монітора, **без** створення повного xorg.conf, створіть новий конфігураційний файл. Наприклад (`/etc/X11/xorg.conf.d/90-monitor.conf`):

```
Section "Monitor"
    Identifier             "<default monitor>"
    DisplaySize            286 179    # В міліметрах
EndSection

```

Якщо у вас немає в документації інформації про ширину та висоту екрана (більшість специфікацій наведено лише за діагональним розміром), можна використовувати власне дозвіл монітора (або співвідношення сторін) і діагональну довжину для обчислення горизонтальних і вертикальних фізичних розмірів. Використання теореми Піфагора на екрані довжини діагоналі 13,3 дюйма з рідною роздільною здатністю 1280x800 (або співвідношенням сторін 16:10):

```
$ echo 'scale=5;sqrt(1280^2+800^2)' | bc  # 1509.43698

```

Це дасть піксельну діагональну довжину і з цим значенням ви зможете виявити фізичні та горизонтальні довжини (і перетворити їх на міліметри):

```
$ echo 'scale=5;(13.3/1509)*1280*25.4' | bc  # 286.43072
$ echo 'scale=5;(13.3/1509)*800*25.4'  | bc  # 179.01920

```

**Note:** Цей розрахунок працює для моніторів з квадратними пікселями; однак, зустрічаються монітори, які можуть стискати форматне співвідношення (наприклад, роздільну здатність 16:10 до 16:9). Якщо це так, ви повинні вимірювати розмір екрану вручну.

#### Ручне налаштування DPI

**Note:** Незважаючи на те, що ви можете встановити будь-яке потрібне dpi, а програми, які використовують Qt і GTK, відповідно масштабуватимуться, рекомендується встановити значення 96, 120 (25% вище), 144 (на 50% вище), 168 (на 75% вище), 192 (100% вище) і т.д., щоб зменшити масштаб артефактів в програмах з GUI, які використовують растрові зображення. Зменшення його нижче 96 точок на дюйм може не зменшити розмір графічних елементів GUI, оскільки, як правило, найнижче dpi для піктограм, становить 96.

Для RandR-сумісних драйверів (наприклад відкритий ATI драйвер), ви можете встановити його:

```
$ xrandr --dpi 144

```

**Note:** Програми, які відповідають встановленим параметрам, не зміняться негайно. Ви повинні їх перезавантажити.

Дивіться [Виконайте команди після старту X](/index.php/Execute_commands_after_X_start "Execute commands after X start") щоб зробити зміни постійними.

##### Пропрієтарний драйвер NVIDIA

DPI можна встановити вручну, якщо ви плануєте використовувати лише одну роздільну здатність ([калькулятор DPI](http://pxcalc.com/)):

```
Section "Monitor"
    Identifier             "Monitor0"
    Option                 "DPI" "96 x 96"
EndSection

```

Ви можете вручну встановити DPI, додавши нижче опції `/etc/X11/xorg.conf.d/20-nvidia.conf` (в секції **Device**):

```
Option              "UseEdidDpi" "False"
Option              "DPI" "96 x 96"

```

##### Застереження, щодо ручного налаштування DPI

GTK дуже часто перевизначає DPI сервера за допомогою додаткового файлу Xresource `Xft.dpi`. Щоб дізнатися, чи відбувається це з вами, перевірте з:

```
$ xrdb -query | grep dpi

```

З версіями бібліотеки GTK після 3.16, коли ця змінна явно не встановлена, GTK встановлює його 96\. Щоб програми GTK підкорялися серверу DPI, вам може знадобитися точно встановити Xft.dpi на те ж значення, що і сервер. Ресурс Xft.dpi - це метод, за допомогою якого деякі настільні середовища примушують DPI до певного значення в особистих налаштуваннях. Серед них KDE та TDE.

### Управління енергозбереженням монітора

[DPMS](/index.php/DPMS "DPMS") (Display Power Management Signaling) це технологія, що визначає функції управління енергозбереженням моніторів за допомогою відеокарти, коли комп'ютер не використовується. Це дозволить монітору автоматично переходити в режим очікування після попередньо визначеного періоду часу.

## Композит

Композитне розширення для X призводить до того, що усе піддерево ієрархії вікна буде відтворено у буфері поза екраном. Програми можуть приймати вміст цього буфера і робити все, що їм подобається. Екранний буфер може бути автоматично об'єднаний у батьківське вікно або об'єднаний зовнішніми програмами, які називаються композитними менеджерами. Докладнішу інформацію див. у наступній статті: [Композитний менеджер вікон](https://uk.wikipedia.org/w/index.php?title=%D0%9A%D0%BE%D0%BC%D0%BF%D0%BE%D0%B7%D0%B8%D1%82%D0%BD%D0%B8%D0%B9_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80_%D0%B2%D1%96%D0%BA%D0%BE%D0%BD&oldid=13646590)

Багато віконних менеджерів (наприклад: [Compiz](/index.php/Compiz "Compiz"), [Enlightenment](/index.php/Enlightenment "Enlightenment"), KWin, Marco, Metacity, Muffin, Mutter, [Xfwm](/index.php/Xfwm "Xfwm")) роблять композицію самостійно. Для інших менеджерів вікон можна використовувати автономний композитний менеджер.

### Список композитних менеджерів

*   **[Compton](/index.php/Compton "Compton")** — Композитний віконний менеджер (форк xcompmgr-dana)

	[https://github.com/yshui/compton](https://github.com/yshui/compton) || [compton](https://www.archlinux.org/packages/?name=compton)

*   **[Xcompmgr](/index.php/Xcompmgr "Xcompmgr")** — Композитний віконний менеджер

	[http://cgit.freedesktop.org/xorg/app/xcompmgr/](http://cgit.freedesktop.org/xorg/app/xcompmgr/) || [xcompmgr](https://www.archlinux.org/packages/?name=xcompmgr)

*   **Unagi** — Модульний композитний менеджер, який написаний на С і базується на XCB

	[http://projects.mini-dweeb.org/projects/unagi](http://projects.mini-dweeb.org/projects/unagi) || [unagi](https://aur.archlinux.org/packages/unagi/)

## Поради та підказки

### Автоматизація

This section lists utilities for automating keyboard / mouse input and window operations (like moving, resizing or raising).

| Tool | Package | Manual | [Keysym](/index.php/Keysym "Keysym")
input | Window
operations | Note |
| xautomation | [xautomation](https://www.archlinux.org/packages/?name=xautomation) | [xte(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xte.1) | Yes | No | Also contains screen scraping tools. Cannot simulate F13+. |
| xdo | [xdo-git](https://aur.archlinux.org/packages/xdo-git/) | [xdo(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xdo.1) | No | Yes | Small X utility to perform elementary actions on windows. |
| xdotool | [xdotool](https://www.archlinux.org/packages/?name=xdotool) | [xdotool(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xdotool.1) | Yes | Yes | [Very buggy](https://github.com/jordansissel/xdotool/issues) and not in active development, e.g: has broken CLI parsing.[[2]](https://github.com/jordansissel/xdotool/issues/14#issuecomment-327968132)[[3]](https://github.com/jordansissel/xdotool/issues/71) |
| xvkbd | [xvkbd](https://aur.archlinux.org/packages/xvkbd/) | [xvkbd(1)](http://t-sato.in.coocan.jp/xvkbd/#option) | Yes | No | Virtual keyboard for Xorg, also has the `-text` option for sending characters. |

See also [Clipboard#Tools](/index.php/Clipboard#Tools "Clipboard") and [an overview of X automation tools](https://venam.nixers.net/blog/unix/2019/01/07/win-automation.html).

### Nested X session

To run a nested session of another desktop environment:

```
$ /usr/bin/Xnest :1 -geometry 1024x768+0+0 -ac -name Windowmaker & wmaker -display :1

```

This will launch a Window Maker session in a 1024 by 768 window within your current X session.

This needs the package [xorg-server-xnest](https://www.archlinux.org/packages/?name=xorg-server-xnest) to be installed.

### Starting GUI programs remotely

See main article: [OpenSSH#X11 forwarding](/index.php/OpenSSH#X11_forwarding "OpenSSH").

### On-demand disabling and enabling of input sources

With the help of *xinput* you can temporarily disable or enable input sources. This might be useful, for example, on systems that have more than one mouse, such as the ThinkPads and you would rather use just one to avoid unwanted mouse clicks.

[Install](/index.php/Install "Install") the [xorg-xinput](https://www.archlinux.org/packages/?name=xorg-xinput) package.

Find the name or ID of the device you want to disable:

```
$ xinput

```

For example in a Lenovo ThinkPad T500, the output looks like this:

 `$ xinput` 
```
⎡ Virtual core pointer                          id=2    [master pointer  (3)]
⎜   ↳ Virtual core XTEST pointer                id=4    [slave  pointer  (2)]
⎜   ↳ TPPS/2 IBM TrackPoint                     id=11   [slave  pointer  (2)]
⎜   ↳ SynPS/2 Synaptics TouchPad                id=10   [slave  pointer  (2)]
⎣ Virtual core keyboard                         id=3    [master keyboard (2)]
    ↳ Virtual core XTEST keyboard               id=5    [slave  keyboard (3)]
    ↳ Power Button                              id=6    [slave  keyboard (3)]
    ↳ Video Bus                                 id=7    [slave  keyboard (3)]
    ↳ Sleep Button                              id=8    [slave  keyboard (3)]
    ↳ AT Translated Set 2 keyboard              id=9    [slave  keyboard (3)]
    ↳ ThinkPad Extra Buttons                    id=12   [slave  keyboard (3)]

```

Disable the device with `xinput --disable *device*`, where *device* is the device ID or name of the device you want to disable. In this example we will disable the Synaptics Touchpad, with the ID 10:

```
$ xinput --disable 10

```

To re-enable the device, just issue the opposite command:

```
$ xinput --enable 10

```

Alternatively using the device name, the command to disable the touchpad would be:

```
$ xinput --disable "SynPS/2 Synaptics TouchPad"

```

### Killing application with hotkey

Run script on hotkey:

```
#!/bin/bash
windowFocus=$(xdotool getwindowfocus);
pid=$(xprop -id $windowFocus | grep PID);
kill -9 $pid

```

Deps: [xorg-xprop](https://www.archlinux.org/packages/?name=xorg-xprop), [xdotool](https://www.archlinux.org/packages/?name=xdotool)

### Block TTY access

To block tty access when in an X add the following to [xorg.conf](#Configuration):

```
Section "ServerFlags"
    Option "DontVTSwitch" "True"
EndSection
```

### Prevent a user from killing X

To prevent a user from killing when it is running add the following to [xorg.conf](#Configuration):

```
Section "ServerFlags"
    Option "DontZap"      "True"
EndSection
```

## Troubleshooting

### General

If a problem occurs, view the log stored in either `/var/log/` or, for the rootless X default since v1.16, in `~/.local/share/xorg/`. [GDM](/index.php/GDM "GDM") users should check the [systemd](/index.php/Systemd "Systemd") journal. [[4]](https://bbs.archlinux.org/viewtopic.php?id=184639)

The logfiles are of the form `Xorg.n.log` with `n` being the display number. For a single user machine with default configuration the applicable log is frequently `Xorg.0.log`, but otherwise it may vary. To make sure to pick the right file it may help to look at the timestamp of the X server session start and from which console it was started. For example:

 `$ grep -e Log -e tty Xorg.0.log` 
```
[    40.623] (==) Log file: "/home/archuser/.local/share/xorg/Xorg.0.log", Time: Thu Aug 28 12:36:44 2014
[    40.704] (--) controlling tty is VT number 1, auto-enabling KeepTty
```

*   In the logfile then be on the lookout for any lines beginning with `(EE)`, which represent errors, and also `(WW)`, which are warnings that could indicate other issues.

*   If there is an *empty* `.xinitrc` file in your `$HOME`, either delete or edit it in order for X to start properly. If you do not do this X will show a blank screen with what appears to be no errors in your `Xorg.0.log`. Simply deleting it will get it running with a default X environment.
*   If the screen goes black, you may still attempt to switch to a different virtual console (e.g. `Ctrl+Alt+F2`), and blindly log in as root. You can do this by typing `root` (press `Enter` after typing it) and entering the root password (again, press `Enter` after typing it).

	You may also attempt to kill the X server with:

	 `# pkill -x X` 

	If this does not work, reboot blindly with:

	 `# reboot` 

*   Check specific pages in [Category:Input devices](/index.php/Category:Input_devices "Category:Input devices") if you have issues with keyboard, mouse, touchpad etc.
*   Search for common problems in [ATI](/index.php/ATI "ATI"), [Intel](/index.php/Intel "Intel") and [NVIDIA](/index.php/NVIDIA "NVIDIA") articles.

### Black screen, No protocol specified.., Resource temporarily unavailable for all or some users

X creates configuration and temporary files in current user's home directory. Make sure there is free disk space available on the partition your home directory resides in. Unfortunately, X server does not provide any more obvious information about lack of disk space in this case.

### DRI with Matrox cards stopped working

If you use a Matrox card and DRI stopped working after upgrading to Xorg, try adding the line:

```
Option "OldDmaInit" "On"

```

to the Device section that references the video card in `xorg.conf`.

### Frame-buffer mode problems

If X fails to start with the following log messages,

```
(WW) Falling back to old probe method for fbdev
(II) Loading sub module "fbdevhw"
(II) LoadModule: "fbdevhw"
(II) Loading /usr/lib/xorg/modules/linux//libfbdevhw.so
(II) Module fbdevhw: vendor="X.Org Foundation"
       compiled for 1.6.1, module version=0.0.2
       ABI class: X.Org Video Driver, version 5.0
(II) FBDEV(1): using default device

Fatal server error:
Cannot run in framebuffer mode. Please specify busIDs for all framebuffer devices

```

[Uninstall](/index.php/Uninstall "Uninstall") the [xf86-video-fbdev](https://www.archlinux.org/packages/?name=xf86-video-fbdev) package.

### Program requests "font '(null)'"

*   Error message: "*unable to load font `(null)'.*"

Some programs only work with bitmap fonts. Two major packages with bitmap fonts are available, [xorg-fonts-75dpi](https://www.archlinux.org/packages/?name=xorg-fonts-75dpi) and [xorg-fonts-100dpi](https://www.archlinux.org/packages/?name=xorg-fonts-100dpi). You do not need both; one should be enough. To find out which one would be better in your case, try `xdpyinfo` from [xorg-xdpyinfo](https://www.archlinux.org/packages/?name=xorg-xdpyinfo), like this:

```
$ xdpyinfo | grep resolution

```

and use what is closer to the shown value.

### Recovery: disabling Xorg before GUI login

If Xorg is set to boot up automatically and for some reason you need to prevent it from starting up before the login/display manager appears (if the system is wrongly configured and Xorg does not recognize your mouse or keyboard input, for instance), you can accomplish this task with two methods.

*   Change default target to rescue.target. See [systemd#Change default target to boot into](/index.php/Systemd#Change_default_target_to_boot_into "Systemd").
*   If you have not only a faulty system that makes Xorg unusable, but you have also set the GRUB menu wait time to zero, or cannot otherwise use GRUB to prevent Xorg from booting, you can use the Arch Linux live CD. Follow the [installation guide](/index.php/Installation_guide#Format_the_partitions "Installation guide") about how to mount and chroot into the installed Arch Linux. Alternatively try to switch into another [tty](/index.php/Tty "Tty") with `Ctrl+Alt` + function key (usually from `F1` to `F7` depending on which is not used by X), login as root and follow steps below.

Depending on setup, you will need to do one or more of these steps:

*   [Disable](/index.php/Disable "Disable") the [display manager](/index.php/Display_manager "Display manager").
*   Disable the [automatic start of the X](/index.php/Start_X_at_login "Start X at login").
*   Rename the `~/.xinitrc` or comment out the `exec` line in it.

### X clients started with "su" fail

If you are getting "Client is not authorized to connect to server", try adding the line:

```
session        optional        pam_xauth.so

```

to `/etc/pam.d/su` and `/etc/pam.d/su-l`. `pam_xauth` will then properly set environment variables and handle `xauth` keys.

### X failed to start: Keyboard initialization failed

If the filesystem (specifically `/tmp`) is full, `startx` will fail. `/var/log/Xorg.0.log` will end with:

```
(EE) Error compiling keymap (server-0)
(EE) XKB: Could not compile keymap
(EE) XKB: Failed to load keymap. Loading default keymap instead.
(EE) Error compiling keymap (server-0)
(EE) XKB: Could not compile keymap
XKB: Failed to compile keymap
Keyboard initialization failed. This could be a missing or incorrect setup of xkeyboard-config.
Fatal server error:
Failed to activate core devices.
Please consult the The X.Org Foundation support at http://wiki.x.org
for help.
Please also check the log file at "/var/log/Xorg.0.log" for additional information.
(II) AIGLX: Suspending AIGLX clients for VT switch

```

Make some free space on the relevant filesystem and X will start.

### Rootless Xorg

Xorg may run with standard user privileges with the help of [systemd-logind(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-logind.8), see [[5]](https://fedoraproject.org/wiki/Changes/XorgWithoutRootRights) and [FS#41257](https://bugs.archlinux.org/task/41257). The requirements for this are:

*   Starting X via [xinit](/index.php/Xinit "Xinit"); display managers are not supported
*   [Kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting"); implementations in proprietary display drivers fail [auto-detection](http://cgit.freedesktop.org/xorg/xserver/tree/hw/xfree86/xorg-wrapper.c#n222) and require manually setting `needs_root_rights = no` in `/etc/X11/Xwrapper.config`.

If you do not fit these requirements, re-enable root rights in `/etc/X11/Xwrapper.config`:

 `/etc/X11/Xwrapper.config`  `needs_root_rights = *yes*` 

See also [Xorg.wrap(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/Xorg.wrap.1) and [Systemd/User#Xorg as a systemd user service](/index.php/Systemd/User#Xorg_as_a_systemd_user_service "Systemd/User").

[GDM](/index.php/GDM "GDM") also runs Xorg without root privileges by default when [Kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting") is used.

#### Broken redirection

While user Xorg logs are stored in `~/.local/share/xorg/Xorg.log`, they do not include the output from the X session. To re-enable redirection, start X with the `-keeptty` flag:

```
exec startx -- -keeptty > ~/.xorg.log 2>&1

```

Or copy `/etc/X11/xinit/xserverrc` to `~/.xserverrc`, and append `-keeptty`. See [[6]](https://bbs.archlinux.org/viewtopic.php?pid=1446402#p1446402).

### A green screen whenever trying to watch a video

Your color depth is set wrong. It may need to be 24 instead of 16, for example.

### SocketCreateListener error

If X terminates with error message "SocketCreateListener() failed", you may need to delete socket files in `/tmp/.X11-unix`. This may happen if you have previously run Xorg as root (e.g. to generate an `xorg.conf`).

### Invalid MIT-MAGIC-COOKIE-1 key when trying to run a program as root

That error means that only the current user has access to the X server. The solution is to give access to root:

```
$ xhost +si:localuser:root

```

That line can also be used to give access to X to a different user than root.

## See also

*   [Xplain](https://magcius.github.io/xplain/article/) - In-depth explanation of the X Window System