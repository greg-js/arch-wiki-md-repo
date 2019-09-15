Ссылки по теме

*   [PulseAudio/Примеры](/index.php/PulseAudio/%D0%9F%D1%80%D0%B8%D0%BC%D0%B5%D1%80%D1%8B "PulseAudio/Примеры")
*   [PulseAudio/Решение проблем](/index.php/PulseAudio/%D0%A0%D0%B5%D1%88%D0%B5%D0%BD%D0%B8%D0%B5_%D0%BF%D1%80%D0%BE%D0%B1%D0%BB%D0%B5%D0%BC "PulseAudio/Решение проблем")

**Состояние перевода:** На этой странице представлен перевод статьи [PulseAudio](/index.php/PulseAudio "PulseAudio"). Дата последней синхронизации: 6 декабря 2017\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=PulseAudio&diff=0&oldid=500843).

[PulseAudio](https://en.wikipedia.org/wiki/ru:PulseAudio "wikipedia:ru:PulseAudio") - это многофункциональный звуковой сервер, предназначенный для работы в качестве прослойки между вашими приложениями и аппаратными устройствами, либо [ALSA](/index.php/ALSA "ALSA") или [OSS](/index.php/OSS "OSS"). Он также с легкостью может передавать аудио по сети между локальными устройствами используя [Avahi](/index.php/Avahi "Avahi"), если тот доступен. Несмотря на то, что основная цель заключена в простоте настройки звука, его модульная архитектура позволяет более опытным пользователям конфигурировать демон в соответствии со своими нуждами.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Установка](#Установка)
    *   [1.1 Интерфейсы](#Интерфейсы)
*   [2 Настройка](#Настройка)
    *   [2.1 Файлы настроек](#Файлы_настроек)
        *   [2.1.1 daemon.conf](#daemon.conf)
        *   [2.1.2 default.pa](#default.pa)
        *   [2.1.3 client.conf](#client.conf)
    *   [2.2 Команда настроек](#Команда_настроек)
*   [3 Выполнение](#Выполнение)
*   [4 Настройка бакэндов](#Настройка_бакэндов)
    *   [4.1 ALSA](#ALSA)
        *   [4.1.1 Раскрытие источников, устройств вывода и микшеров PulseAudio для ALSA](#Раскрытие_источников,_устройств_вывода_и_микшеров_PulseAudio_для_ALSA)
        *   [4.1.2 ALSA/dmix без захвата аппаратного устройства](#ALSA/dmix_без_захвата_аппаратного_устройства)
    *   [4.2 OSS](#OSS)
        *   [4.2.1 ossp](#ossp)
        *   [4.2.2 Оболочка padsp](#Оболочка_padsp)
    *   [4.3 GStreamer](#GStreamer)
    *   [4.4 OpenAL](#OpenAL)
    *   [4.5 libao](#libao)
*   [5 Эквалайзер](#Эквалайзер)
    *   [5.1 Загрузка устройства вывода эквалайзера и модуля dbus-protocol](#Загрузка_устройства_вывода_эквалайзера_и_модуля_dbus-protocol)
    *   [5.2 Графический интерфейс](#Графический_интерфейс)
    *   [5.3 Загрузка эквалайзера и модуля DBus при каждой загрузке системы](#Загрузка_эквалайзера_и_модуля_DBus_при_каждой_загрузке_системы)
    *   [5.4 Альтернативные эквалайзеры](#Альтернативные_эквалайзеры)
*   [6 Приложения](#Приложения)
    *   [6.1 QEMU](#QEMU)
    *   [6.2 AlsaMixer.app](#AlsaMixer.app)
    *   [6.3 XMMS2](#XMMS2)
    *   [6.4 Рабочая область KDE Plasma и Qt4](#Рабочая_область_KDE_Plasma_и_Qt4)
    *   [6.5 Audacious](#Audacious)
    *   [6.6 Music Player Daemon (MPD)](#Music_Player_Daemon_(MPD))
    *   [6.7 MPlayer](#MPlayer)
    *   [6.8 guvcview](#guvcview)
*   [7 Сетевой звук](#Сетевой_звук)
    *   [7.1 Базовая настройка с прямым подключением](#Базовая_настройка_с_прямым_подключением)
        *   [7.1.1 На сервере](#На_сервере)
        *   [7.1.2 На клиентской машине](#На_клиентской_машине)
*   [8 Советы и хитрости](#Советы_и_хитрости)
    *   [8.1 Регулировка звука клавиатурой](#Регулировка_звука_клавиатурой)
    *   [8.2 Проигрывание звука через неинтерактивную оболочку (служба systemd, cron)](#Проигрывание_звука_через_неинтерактивную_оболочку_(служба_systemd,_cron))
    *   [8.3 Сигналы событий X11](#Сигналы_событий_X11)
    *   [8.4 Переключение при подключении](#Переключение_при_подключении)
    *   [8.5 Скрипт для переключения аналоговых выходов](#Скрипт_для_переключения_аналоговых_выходов)
*   [9 Решение проблем](#Решение_проблем)
*   [10 Смотрите также](#Смотрите_также)

## Установка

Установите пакет [pulseaudio](https://www.archlinux.org/packages/?name=pulseaudio).

Некоторые модули PulseAudio были [отделены](https://www.archlinux.org/news/pulseaudio-split/) от основного пакета и должны быть установлены самостоятельно, если требуются:

*   [pulseaudio-bluetooth](https://www.archlinux.org/packages/?name=pulseaudio-bluetooth): поддержка Bluetooth (Bluez)
*   [pulseaudio-equalizer](https://www.archlinux.org/packages/?name=pulseaudio-equalizer): эквалайзер устройств вывода (qpaeq)
*   [pulseaudio-gconf](https://www.archlinux.org/packages/?name=pulseaudio-gconf): поддержка GConf (paprefs)
*   [pulseaudio-jack](https://www.archlinux.org/packages/?name=pulseaudio-jack): определение устройств вывода, источников [JACK](/index.php/JACK "JACK") и jackdbus
*   [pulseaudio-lirc](https://www.archlinux.org/packages/?name=pulseaudio-lirc): инфракрасный контроль громкости (LIRC)
*   [pulseaudio-zeroconf](https://www.archlinux.org/packages/?name=pulseaudio-zeroconf): поддержка Zeroconf (Avahi/DNS-SD)

**Примечание:** При взаимодействии [ALSA](/index.php/ALSA "ALSA") и PulseAudio могут быть некоторые проблемы. ALSA включает компоненты ядра Linux с драйверами звуковой карты, также как и компоненты окружения пользователя, `libalsa`.[[1]](http://www.alsa-project.org/main/index.php/Download) PulseAudio строится только на компонентах ядра, но предлагает совместимость с `libalsa` через [pulseaudio-alsa](https://www.archlinux.org/packages/?name=pulseaudio-alsa).[[2]](http://www.freedesktop.org/wiki/Software/PulseAudio/FAQ/#index14h3)

### Интерфейсы

Существует множество интерфейсов для управления демоном PulseAudio:

*   Настройка/управление громкостью (графический): [pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol)
*   Базовая настройка демона (графический): [paprefs](https://www.archlinux.org/packages/?name=paprefs)
*   Управление громкостью через установленные сочетания клавиш клавиатуры: [pulseaudio-ctl](https://aur.archlinux.org/packages/pulseaudio-ctl/), [pavolume-git](https://aur.archlinux.org/packages/pavolume-git/)
*   Консольные (CLI) микшеры: [ponymix](https://www.archlinux.org/packages/?name=ponymix) и [pamixer](https://www.archlinux.org/packages/?name=pamixer)
*   Консольные (curses) микшеры: [pulsemixer](https://www.archlinux.org/packages/?name=pulsemixer)
*   Контроль громкости по сети: [PaWebControl](https://github.com/Siot/PaWebControl)
*   Иконки панели задач: [pasystray](https://www.archlinux.org/packages/?name=pasystray), [pasystray-git](https://aur.archlinux.org/packages/pasystray-git/), [pasystray-gtk2-standalone](https://aur.archlinux.org/packages/pasystray-gtk2-standalone/), и [pasystray-gtk3-standalone](https://aur.archlinux.org/packages/pasystray-gtk3-standalone/)

**Совет:** Неавтономная (non-standalone) версия `pasystray` может быть установлена сразу и с GTK2, и с GTK3\. Выбор производится при установке. Версия в виде отдельной программы (standalone) устанавливает только одну.

*   Plasma-апплет KF5: [kmix](https://www.archlinux.org/packages/?name=kmix) и [plasma-pa](https://www.archlinux.org/packages/?name=plasma-pa)
*   Плагин Xfce4: [xfce4-pulseaudio-plugin](https://www.archlinux.org/packages/?name=xfce4-pulseaudio-plugin), [pa-applet-git](https://aur.archlinux.org/packages/pa-applet-git/)
*   Если вы хотите использовать Bluetooth гарнитуру или другие Bluetooth аудио устройства с PulseAudio, смотрите раздел статьи [Bluetooth гарнитура](/index.php?title=Bluetooth_%D0%B3%D0%B0%D1%80%D0%BD%D0%B8%D1%82%D1%83%D1%80%D0%B0&action=edit&redlink=1 "Bluetooth гарнитура (page does not exist)").

## Настройка

### Файлы настроек

По умолчанию PulseAudio настроен на управление и автоматическое обнаружение всех звуковых карт. Он берёт под свой контроль все обнаруженные устройства ALSA, и перенаправляет все аудиопотоки на себя, делая демон PulseAudio центральной точкой настроек. Демон, в основном, должен работать "из коробки", требуя только нескольких незначительных изменений настроек.

PulseAudio будет сначала смотреть файлы настроек в домашнем каталоге `~/.config/pulse`, а затем в общесистемном `/etc/pulse`.

PulseAudio работает как демон сервера, который может работать или общесистемно или для каждого пользователя, с помощью архитектуры клиент/сервер. Без своих **модулей** демон сам по себе ничего не делает, кроме обеспечения API и размещения динамически загружаемых модулей. Вся маршрутизация аудио и обработка задач обрабатывается различными модулями. Вы можете найти подробный список всех доступных модулей в [Загружаемые Модули Pulseaudio (Англ.)](http://www.freedesktop.org/wiki/Software/PulseAudio/Documentation/User/Modules/). Чтобы включить их, Вы можете добавить строку `load-module <имя модуля из списка>` в `~/.config/pulse/default.pa`.

**Совет:**

*   Настоятельно советуем не редактировать общесистемные файлы настроек, вместо них редактируйте пользовательские. Создайте каталог `~/.config/pulse`, затем скопируйте (`cp /etc/pulse/ ~/.config/pulse`) файлы настроек системы в него, и редактируйте согласно Вашим требованиям.
*   Убедитесь, что Вы держите пользовательские настройки в синхронизации с изменениями в пакетных файлах `/etc/pulse/`. Иначе, PulseAudio может отказаться запускаться из-за ошибки в настройках.
*   Нет необходимости добавлять Вашего пользователя к группе audio, поскольку он использует [udev](/index.php/Udev_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Udev (Русский)") и *logind* для динамичного предоставления доступа к "в настоящее время активному" пользователю. Исключение составляют клиентские (headless) машины, в которых нет понятия текущий "активный" пользователь.

#### daemon.conf

Определяет основные настройки, такие как: частоты дискретизации по умолчанию, используемые модулями, методы повторной выборки, планирование в реальном времени, и другие различные настройки, связанные с серверным процессом. Они не могут быть изменены во время выполнения, без перезапуска демона PulseAudio. Значения по умолчанию подходят для большинства пользователей.

**Примечание:** PulseAudio не поддерживает использование тильды (~) в описании путей в этом файле. Используйте абсолютные пути для любых файлов.

<caption>Известные параметры настроек</caption>
| Опция | Описание |<caption></caption>
| system-instance (системный экземпляр) | Запустит демон как [общесистемный](https://www.freedesktop.org/wiki/Software/PulseAudio/Documentation/User/SystemWide/) экземпляр. [Крайне нежелательно](https://www.freedesktop.org/wiki/Software/PulseAudio/Documentation/User/WhatIsWrongWithSystemWide/), поскольку это может привести к проблемам безопасности. Полезно в [системах с несколькими пользователями](/index.php/Xorg_multiseat "Xorg multiseat") и (headless) системах, не имеющих никаких настоящих локальных пользователей. Значение по умолчанию `no`. |<caption></caption>
| avoid-resampling (избегать методы дискретизации) | Со значением `avoid-resampling = yes`, PulseAudio автоматически настроит частоту дискретизации аппаратного обеспечения в соответствии с той, которую использует приложение, при условии, что аппаратное обеспечение ее поддерживает (необходим [PA 11](https://www.freedesktop.org/wiki/Software/PulseAudio/Notes/11.0/) или новее) |<caption></caption>
| resample-method (метод частоты дискретизации) | Какой метод частоты дискретизации (resampler) использовать, когда звук с несовместимыми частотами дискретизации должен быть передан между модулями (например, воспроизведение звука на 96 кГц на аппаратном обеспечении, поддерживающим только 48 кГц). Доступные resampler'ы могут быть перечислены с помощью `$ pulseaudio --dump-resample-methods`. Выберите и используйте лучший компромисс между загрузкой процессора и качеством звука.
**Совет:** В некоторых случаях PulseAudio будет генерировать высокую нагрузку на процессор. Это может произойти, когда несколько потоков передискретизируются (индивидуально). Если это используется в выбранном общем рабочем процессе, его следует продумать, чтобы создать дополнительное устройство вывода (sink) с соответствующей частотой дискретизации, которое может передавать в основное устройство вывода (main sink), передискретизируя только один раз.
 |<caption></caption>
| flat-volumes | `flat-volumes` масштабирует громкость устройства с громкостью "самого громкого" приложения. Например, повышение громкости вызова VoIP повысит аппаратную громкость и скорректирует звук аудиоплеера, таким образом, что понижать громкость аудиоплеера вручную нет необходимости. Значение по умолчанию `yes`, но в сборке для Arch - `no`.
**Примечание:** Поведение значения по умолчанию, иногда, может сбивать с толку, и некоторые приложения не зная об этой функции, могут регулировать свою громкость к 100% при запуске, потенциально создавая неожиданно громкий звук. Для восстановления классического поведения (ALSA), установите это значение в `no`.
 |<caption></caption>
| default-fragments (фрагменты по умолчанию) | Аудиосэмплы разделяются на многократные фрагменты `default-fragment-size-msec`. Чем больше буфер, тем менее вероятен пропуск звука, когда система будет перегружена. С другой стороны это увеличит общую величину задержки. Увеличьте это значение, если у Вас есть проблемы. |

#### default.pa

Этот файл является сценарием запуска и используется для настройки модулей. Он анализируется и читается после завершения инициализации демона. Дополнительные команды могут быть отправлены во время выполнения с помощью `$ pactl` или `$ pacmd`. Сценарий запуска также может быть указан в командной строке, путем запуска PulseAudio в терминале, с помощью `$ pulseaudio -nC`. Это заставит демона загрузить модуль CLI и принимать настройки непосредственно из командной строки, выдавать получающуюся информацию или сообщения об ошибках на том же терминале. Это может быть полезно при отладке демона или тестирования различных модулей, перед постоянной установкой их на диск. Обратитесь к странице руководства [pulse-cli-syntax(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pulse-cli-syntax.5), для пояснений элементов синтаксиса

**Совет:**

*   Вместо создания полной копии, файл `~/.config/pulse/default.pa` может начинаться со строки `.include /etc/pulse/default.pa` и далее блок с переназначением параметров по умолчанию.
*   Для перечисления доступных устройств вывода, выполните `$ pacmd list-sinks|egrep -i 'index:|name:'`. Задействованное в настоящее время устройство вывода по умолчанию, отмечено звёздочкой (*).
*   Редактируйте `~/.config/pulse/default.pa` для вставки/изменения команды установленного_по_умолчанию_устройства_вывода, использующей имя устройства вывода, поскольку повторная нумерация не может быть гарантирована.

#### client.conf

Это файл настроек, читающийся каждым клиентским приложением PulseAudio. Он используется для настройки опций во время выполнения для отдельных клиентов. Может использоваться чтобы устанавливать и настраивать устройство вывода по умолчанию и для статического запуска, а также позволять (или запрещать) клиентам автоматический запуск сервера, если он в настоящее время не работает.

### Команда настроек

Основная команда для настройки сервера во время выполнения является `$ pacmd`. Для списка опций выполните `$ pacmd --help`, или для входа в интерактивный режим оболочки выполните `$ pacmd` и `Ctrl+d` для выхода. Все модификации будут сразу применены.

После того, как новые настройки были проверены и удовлетворили Ваши потребности, соответственно отредактируйте `default.pa`, чтобы изменения стали постоянными. Для некоторых основных настроек, смотрите [PulseAudio/Examples (Русский)](/index.php/PulseAudio/Examples_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "PulseAudio/Examples (Русский)").

**Совет:** Оставьте нетронутой строку `load-module module-default-device-restore` в файле `default.pa`. Это позволит вам перезапустить сервер в состояние по умолчанию, таким образом избегая любых неправильных установок.

Важно понять, что "sources" (источники) (процессы, устройства захвата) и доступные "sinks" (устройства вывода/приемники) (звуковые карты, серверы, другие процессы) можно выбрать через PulseAudio, это зависит от текущих аппаратных средств выбранного "Profile" (профиля). Эти "Профили" являются теми ALSA "pcms" перечисленные командой `aplay -L`, и более конкретно командой `pacmd list-cards`, которая будет включать строку "index:" (индекс), список начинающийся с "profiles:" (профилей) и строку "active profile: <...>" (активный профиль) на выводе, среди других вещей.

"active profile" (Активный профиль) может быть установлен командой `pacmd set-card-profile INDEX PROFILE` без запятой ( `,` ) разделяющей INDEX и PROFILE, где INDEX является просто числом на строке "index:" и имя PROFILE является всем показанным с начала любой строки под "профилем": *до* двоеточия и первого пробела, как показано командой `pacmd list-cards`. Например, `pacmd set-card-profile 0 output:analog-stereo+input:analog-stereo`.

"Профиль" проще выбрать с графическим инструментом, таким как `pavucontrol`, под вкладкой "Configuration" (Настройка) или Параметрами настройки системы KDE, "Мультимедийные/Аудио и Параметры видео", под вкладкой "Audio Hardware Setup". Каждая аудио "Карта", которая является устройством, перечисленным командой `aplay -l`, или командой `pacmd list-cards`, будет иметь свой собственный выбор "Профиля". Когда "Профиль" был выбран, то доступные "источники" и "приемники" можно увидеть при помощи команд `pacmd list-sources` и `pacmd list-sinks`. Обратите внимание на то, что "индекс" доступных источников и приемников изменятся каждый раз, когда изменяется профиль карты.

Выбранный "Профиль" может вызывать проблемы у некоторых приложений, особенно Adobe Flash Player, обычно `/usr/lib/mozilla/plugins/libflashplayer.so` и `/usr/lib/PepperFlash/libpepflashplayer.so`. Часто, эти флэш-плееры будут работать только тогда, когда выбран один из профилей Стерео, иначе видео будет проигрываться без звука или просто "откажется" воспроизводиться. Когда все остальное перестало работать, Вы можете попробовать выбрать другой профиль.

Конечно, при настройке некоторых вариаций Surround Sound (Объёмного Звука) в PulseAudio, должен быть выбран соответствующий профиль Surround. Прежде чем объёмный звук будет работать, сделайте такие вещи, как переназначение каналов динамиков (speaker channels).

## Выполнение

PulseAudio на Arch имеет `pulseaudio.socket`, который включен по умолчанию для экземпляра [systemd/Пользователь](/index.php/Systemd/%D0%9F%D0%BE%D0%BB%D1%8C%D0%B7%D0%BE%D0%B2%D0%B0%D1%82%D0%B5%D0%BB%D1%8C "Systemd/Пользователь"). Это значит, что по необходимости PulseAudio запустится автоматически.

**Примечание:**

*   Для отключения `pulseaudio.socket` удостоверьтесь, что `$XDG_CONFIG_HOME/systemd/user` существует, и выполните `systemctl --user mask pulseaudio.socket`
*   Многие [окружения рабочих столов](/index.php/Desktop_environment_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Desktop environment (Русский)") автоматически запускают программы на основе [файлов desktop](/index.php/Desktop_entries_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Автозапуск "Desktop entries (Русский)") из каталога `/etc/xdg/autostart/`. В этом случае PulseAudio будет запущен автоматически независимо от состояния активации сокета

Для получения дополнительной информации посмотрите [PulseAudio: Выполнение](http://www.freedesktop.org/wiki/Software/PulseAudio/Documentation/User/Running/).

## Настройка бакэндов

### ALSA

Если у вас есть приложения, которые совсем не поддерживают PulseAudio, но используют ALSA, они будут пытаться получить доступ напрямую к звуковой карте через ALSA, минуя PulseAudio. Таким образом, звуковая карта перестанет быть доступной для PulseAudio. Вследствие чего, все приложения, использующие PulseAudio, перестанут работать, как описано [здесь](/index.php/PulseAudio/Troubleshooting_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Единственное_указанное_устройство_является_"фиктивным_выходом"_или_вновь_подключенные_карты_не_определяются "PulseAudio/Troubleshooting (Русский)"). Чтобы этого избежать, вам необходимо установить пакет [pulseaudio-alsa](https://www.archlinux.org/packages/?name=pulseaudio-alsa). Он содержит файл `/etc/asound.conf` необходимый для настройки возможности ALSA использовать PulseAudio. Также убедитесь, что файл `~/.asoundrc` отсутствует, так как при его наличии, он будет переопределять настройки из файла `/etc/asound.conf`.

Пожалуйста, также установите [lib32-libpulse](https://www.archlinux.org/packages/?name=lib32-libpulse) и [lib32-alsa-plugins](https://www.archlinux.org/packages/?name=lib32-alsa-plugins), если вы используете систему x86_64 и хотите, чтобы в 32-битных [multilib](/index.php/Multilib "Multilib") программах, например [Wine](/index.php/Wine "Wine") and [Steam](/index.php/Steam "Steam"), был звук.

Чтобы запретить приложениям ALSA использовать эмуляцию OSS в обход PulseAudio (тем самым не давая другим приложениям воспроизводить звук), убедитесь, что модуль `snd_pcm_oss` не загружается при загрузке системы. Если он в настоящее время загружен (`lsmod | grep oss`), отключите его, выполнив:

```
# rmmod snd_pcm_oss

```

#### Раскрытие источников, устройств вывода и микшеров PulseAudio для ALSA

[pulseaudio-alsa](https://www.archlinux.org/packages/?name=pulseaudio-alsa) также содержит необходимые конфигурационные файлы для разрешения приложениям ALSA использовать устройство PulseAudio по умолчанию. Плагин ALSA `pulse` более гибкий чем этот:

 `~/.asoundrc (or /etc/asound.conf)` 
```
# Create an alsa input/output using specific PulseAudio sources/sinks
 pcm.pulse-example1 {
     type pulse
     device "my-combined-sink" # name of a source or sink
     fallback "pulse-example2" # if combined not available
 }

 pcm.pulse-example2 {
     type pulse
     device "other-sound-card" # name of a source or sink
     # example: device "alsa_output.pci-0000_00_1b.0.analog-stereo"
 }

 # Create an alsa mixer using specific PulseAudio sources/sinks
 # these can be tested with "alsamixer -D pulse-example3"
 ctl.pulse-example3 {
     type pulse
     device "my-output" # name of source or sink to control

     # example: always control the laptop speakers:
     # device "alsa_output.pci-0000_00_1b.0.analog-stereo"
     fallback "pulse-example4" # supports fallback too
 }

 # Mixers also can control a specific source and sink, separately:
 ctl.pulse-example4 {
     type pulse
     sink "my-usb-headphones"
     source "my-internal-mic"

     # example: output to HDMI, record using internal
     sink "alsa_output.pci-0000_01_00.1.hdmi-stereo-extra1"
     source "alsa_input.pci-0000_00_1b.0.analog-stereo"
 }

 # These can override the default mixer (example: for pnmixer integration)
 ctl.!default {
     type pulse
     sink "alsa_output.pci-0000_01_00.1.hdmi-stereo-extra1"
     source "alsa_input.pci-0000_00_1b.0.analog-stereo"
 }
```

Для знакомства со всеми доступными настройками доступен [исходный код](http://git.alsa-project.org/?p=alsa-plugins.git;a=tree;f=pulse;hb=HEAD).

#### ALSA/dmix без захвата аппаратного устройства

**Примечание:** Этот раздел описывает альтернативную настройку, которая, как правило, **не** рекомендуется.

Вы, возможно, захотите использовать ALSA непосредственно в большинстве Ваших приложений, при этом, если есть необходимость, иметь возможность использовать приложения требующие PulseAudio. Следующие шаги позволяют Вам заставлять PulseAudio использовать dmix вместо того, чтобы "захватывать" устройство ALSA.

*   Удалите пакет [pulseaudio-alsa](https://www.archlinux.org/packages/?name=pulseaudio-alsa), обеспечивающий уровень совместимости между приложениями ALSA и PulseAudio. После этого Ваши приложения ALSA будут использовать ALSA напрямую, без "зацепки" Pulse.

*   Отредактируйте `/etc/pulse/default.pa`.

	Найдите и расскоментируйте строки, загружающие драйверы бэкэнда. Добавьте параметры **device** (устройства) следующим образом. Затем найдите и закомментируйте строки, загружающие модули автоматического обнаружения.

```
load-module module-alsa-sink **device=dmix**
load-module module-alsa-source **device=dsnoop**
# load-module module-udev-detect
# load-module module-detect

```

*   *Дополнительно*: если Вы используете [kdemultimedia-kmix](https://www.archlinux.org/packages/?name=kdemultimedia-kmix), Вы можете управлять громкостью ALSA, вместо громкости PulseAudio:

```
$ echo export KMIX_PULSEAUDIO_DISABLE=1 > ~/.kde4/env/kmix_disable_pulse.sh
$ chmod +x ~/.kde4/env/kmix_disable_pulse.sh

```

*   Теперь, перезагрузите свой компьютер и попытайтесь запустить одновременно приложения ALSA и PulseAudio. Они оба должны воспроизводить звук одновременно.

	При необходимости используйте [pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol) для управления звука PulseAudio.

### OSS

Есть несколько способов заставить работать OSS-программы через PulseAudio:

#### ossp

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [ossp](https://www.archlinux.org/packages/?name=ossp) и [запустите](/index.php/%D0%97%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D0%B5 "Запустите") службу `osspd.service`.

#### Оболочка padsp

Программы использующие OSS могут работать с PulseAudio путем его загрузки с padsp (включенный с PulseAudio):

```
$ padsp OSSпрограмма

```

Несколько примеров:

```
$ padsp aumix
$ padsp sox foo.wav -t ossdsp /dev/dsp

```

Вы можете также добавить пользовательский сценарий оболочки:

 `/usr/local/bin/OSSProgram` 
```
#!/bin/sh
exec padsp /usr/bin/OSSprogram "$@"

```

Убедитесь, что `/usr/local/bin`, идёт до `/usr/bin` в Вашем **PATH**.

### GStreamer

Установите [gst-plugins-good](https://www.archlinux.org/packages/?name=gst-plugins-good), или [gstreamer0.10-good-plugins](https://aur.archlinux.org/packages/gstreamer0.10-good-plugins/), если Ваша программа имеет наследие реализации [GStreamer](/index.php/GStreamer "GStreamer").

### OpenAL

Приложение OpenAL должно использовать PulseAudio по умолчанию, но может быть настроено так, чтобы использовать именно его:

 `/etc/openal/alsoft.conf`  `drivers=pulse,alsa` 

### libao

Отредактируйте файл настроек libao:

 `/etc/libao.conf`  `default_driver=pulse` 

Обязательно удалите опцию alsa драйвера `dev=default` или настройте его для определения конкретного имени устройства вывода Pulse (sink) или его числа.

**Примечание:** Вы можете держать libao стандартно на вывод драйвера *alsa* и его устройств по умолчанию, если Вы устанавливаете [pulseaudio-alsa](https://www.archlinux.org/packages/?name=pulseaudio-alsa), так как устройством вывода по умолчанию ALSA **является** PulseAudio.

## Эквалайзер

**Важно:** Модуль эквалайзера считается нестабильным и может быть удалён из PulseAudio. Больше информации об этом можно найти здесь [список рассылки (англ.)](https://lists.freedesktop.org/archives/pulseaudio-discuss/2014-March/020174.html).

PulseAudio имеет интегрированную систему эквалайзера с 10 полосами. Для использования эквалайзера, сделайте следующее:

Установите [pulseaudio-equalizer](https://www.archlinux.org/packages/?name=pulseaudio-equalizer):

### Загрузка устройства вывода эквалайзера и модуля dbus-protocol

```
$ pactl load-module module-equalizer-sink
$ pactl load-module module-dbus-protocol

```

### Графический интерфейс

выполните:

```
$ qpaeq

```

**Примечание:** Если qpaeq не произвёл никакого эффекта, установите [pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol) и измените "ALSA Playback on" на "FFT based equalizer on ...", во время работы медиапроигрывателя.

### Загрузка эквалайзера и модуля DBus при каждой загрузке системы

Отредактируйте файл `/etc/pulse/default.pa` или `~/.config/pulse/default.pa` вашим редактором, и добавьте следующие строки:

```
### Load the integrated PulseAudio equalizer and D-Bus module
load-module module-equalizer-sink
load-module module-dbus-protocol

```

**Примечание:** Устройство вывода эквалайзера должно быть загружено после того, как основное устройство вывода уже доступно.

### Альтернативные эквалайзеры

[pulseaudio-equalizer-ladspa](https://www.archlinux.org/packages/?name=pulseaudio-equalizer-ladspa) (основан на [swh-plugins](https://www.archlinux.org/packages/?name=swh-plugins)) может использоваться как альтернатива [pulseaudio-equalizer](https://www.archlinux.org/packages/?name=pulseaudio-equalizer).

[pulseeffects](https://www.archlinux.org/packages/?name=pulseeffects) применяет ограничение пиковой громкости, компрессию, реверберацию, авто уровень гроскости и 15-полосный эквалайзер к выводу приложений Pulseaudio.

## Приложения

### QEMU

Обратитесь к [QEMU (Русский)#Host](/index.php/QEMU_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Host "QEMU (Русский)") для детального описания настройки pulseaudio в [QEMU (Русский)](/index.php/QEMU_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "QEMU (Русский)").

### AlsaMixer.app

Сделайте [alsamixer.app](https://aur.archlinux.org/packages/alsamixer.app/) dockapp для использования pulseaudio [windowmaker](https://aur.archlinux.org/packages/windowmaker/), например:

```
$ AlsaMixer.app --device pulse

```

Вот два примера, где первый - для ALSA, и другой - для pulseaudio. Вы можете запустить несколько его экземпляров. Используйте опцию выбора `-w`, кнопок управления для привязки к колесику мышки.

```
# AlsaMixer.app -3 Mic -1 Master -2 PCM --card 0 -w 1
# AlsaMixer.app --device pulse -1 Capture -2 Master -w 2

```

**Примечание:** Он может использовать только те устройства вывода, которые устанавлены по умолчанию..

### XMMS2

Сделайте переключение на вывод pulseaudio

```
$ nyxmms2 server config output.plugin pulse

```

и на alsa

```
$ nyxmms2 server config output.plugin alsa

```

Для того, чтобы xmms2 использовал другое устройство вывода, например:

```
 $ nyxmms2 server config pulse.sink alsa_output.pci-0000_04_01.0.analog-stereo.monitor

```

Смотрите также официальное руководство [[3]](https://xmms2.org/wiki/Using_the_application).

### Рабочая область KDE Plasma и Qt4

PulseAudio будет автоматически использоваться приложениями KDE/Qt4\. Это поддерживается по умолчанию в микшере звука KDE. Для получения дополнительной информации посмотрите [страницу KDE, в wiki PulseAudio](https://www.freedesktop.org/wiki/Software/PulseAudio/Desktops/KDE/).

Один полезный совет с этой страницы заключён в том, что следует загружать `load-module module-device-manager`. Обычно это происходит автоматически при входе в систему с помощью скрипта `/usr/bin/start-pulseaudio-x11`, но если этого не произошло, вы можете добавить его вручную в файл `/etc/pulse/default.pa`. О возможных конфликтах с `module-switch-on-connect` смотрите [#Переключение при подключении](#Переключение_при_подключении).

Если бэкэнд phonon-gstreamer используется для Phonon, GStreamer должен также быть настроен, как описано в [#GStreamer](#GStreamer).

### Audacious

[Audacious](/index.php/Audacious_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Audacious (Русский)") изначально поддерживает PulseAudio. Для его использования установите Audacious Настройки -> Audio -> Current output plugin как 'PulseAudio Output Plugin'.

### Music Player Daemon (MPD)

[Настройте](http://mpd.wikia.com/wiki/PulseAudio) [MPD](/index.php/Music_Player_Daemon_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Music Player Daemon (Русский)") на использование PulseAudio. Смотрите также раздел [Music Player Daemon/Tips and tricks#PulseAudio](/index.php/Music_Player_Daemon/Tips_and_tricks#PulseAudio "Music Player Daemon/Tips and tricks").

### MPlayer

[MPlayer](/index.php/MPlayer "MPlayer") изначально поддерживает вывод PulseAudio с опцией `-ao pulse`. Он также может быть настроен для использования вывода PulseAudio по умолчанию, в `~/.mplayer/config` для конкретного пользователя, или для всей системы `/etc/mplayer/mplayer.conf`:

 `/etc/mplayer/mplayer.conf`  `ao=pulse` 

### guvcview

[guvcview](https://www.archlinux.org/packages/?name=guvcview) при использовании входа PulseAudio от [Веб-камеры](/index.php/Webcam_setup_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Webcam setup (Русский)"), может перевести аудиовход в "приостановленный" режим, в результате чего звук не будет записываться. Вы можете проверить это путем выполнения:

```
$ pactl list sources

```

Если источник аудиосигналов "suspended" (приостановлен), измените следующую строку в `/etc/pulse/default.pa`, изменение:

```
load-module module-suspend-on-idle

```

на

```
#load-module module-suspend-on-idle

```

И затем перезапустите PulseAudio или Ваш компьютер только займет аудиовход вместо того, чтобы находиться в "приостановленном" режиме. Теперь guvcview будет писать звук правильно.

## Сетевой звук

Проигрывание звука через аудиовыходы других компьютеров сети

### Базовая настройка с прямым подключением

##### На сервере

Отредактируйте `~/.config/pulse/default.pa` или `/etc/pulse/default.pa` (или `/etc/pulse/system.pa`, если PulseAudio запускается в системном режиме) и добавьте следующую строку:

```
 load-module module-native-protocol-tcp auth-ip-acl=127.0.0.1;172.16.0.0/16

```

Теперь только клиент с конкретным IP или диапазоном IP, определённым здесь, может получать звук.

Для разрешения общего доступа:

```
 load-module module-native-protocol-tcp auth-anonymous=true

```

**Примечание:** Если ни `auth-ip-acl`, ни `auth-anonymous` не установлены, аутентификация осуществляется посредством `~/.pulse-cookie`, который должен быть одинаковым и на клиенте и на сервере.

По умолчанию для входящих соединений PulseAudio слушает порт `tcp/4713`, поэтому вам может потребоваться открыть этот порт в [брандмауэре](/index.php/Firewall "Firewall").

##### На клиентской машине

Отредактируйте `~/.config/pulse/client.conf` или `/etc/pulse/client.conf` для установки этих настроек для одного пользователя или для всех и добавьте:

```
 default-server = *server-address*

```

*server-address* может быть простым именем домена или IPv4, больше информации можно найти в [the документации](https://www.freedesktop.org/wiki/Software/PulseAudio/Documentation/User/ServerStrings/)

Также можно установить адрес сервера в переменной окружения `$PULSE_SERVER`.

## Советы и хитрости

### Регулировка звука клавиатурой

Привяжите следующие команды к своим кнопках регулировки громкости: `XF86AudioRaiseVolume`, `XF86AudioLowerVolume`, `XF86AudioMute`. Подробнее это рассмотрено здесь [Extra keyboard keys in Xorg (Русский)](/index.php/Extra_keyboard_keys_in_Xorg_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Extra keyboard keys in Xorg (Русский)").

Во-первых, найдите устройство вывода, которое является источником звука, которым вы хотите управлять. Для отображения списка доступных источников вывода используйте команду:

```
pactl list sinks short

```

Предположим, что используется источник 0, тогда для увеличения громкости:

```
sh -c "pactl set-sink-mute 0 false ; pactl set-sink-volume 0 +5%"

```

Для понижения громкости:

```
sh -c "pactl set-sink-mute 0 false ; pactl -- set-sink-volume 0 -5%"

```

Отключить/включить звук:

```
pactl set-sink-mute 0 toggle

```

Отключить/включить микрофон:

```
pactl set-source-mute 1 toggle

```

**Совет:** Чтобы клавиатурные сокращения всегда работали с устройством вывода по умолчанию, установите `@DEFAULT_SINK@` как номер устройства вывода, например, `pactl set-sink-mute @DEFAULT_SINK@ toggle`.

### Проигрывание звука через неинтерактивную оболочку (служба systemd, cron)

Установите `XDG_RUNTIME_DIR` перед командой (замените `*user_id*` на ID пользователя, запускающего PulseAudio):

```
XDG_RUNTIME_DIR=/run/user/*user_id* paplay /usr/share/sounds/freedesktop/stereo/complete.oga

```

Или используйте `machinectl`:

```
# machinectl shell .host --uid=*user_id* /usr/bin/paplay /usr/share/sounds/freedesktop/stereo/complete.oga

```

### Сигналы событий X11

Для передачи pulseaudio управления сигналами событий X11, выполните следующие команды после запуска сеанса X11:

```
pactl upload-sample /usr/share/sounds/freedesktop/stereo/bell.oga x11-bell
pactl load-module module-x11-bell sample=x11-bell display=$DISPLAY

```

Для настройки уровня громкости сигналов X11, запустите команду:

```
xset b 100

```

100 - это уровень в процентах. Для корректной работы потребуется пакет [xorg-xset](https://www.archlinux.org/packages/?name=xorg-xset). Чтобы узнать как запускать данные команды автоматически при загрузке сессии X11, ознакомьтесь с разделом [Autostarting (Русский)](/index.php/Autostarting_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Autostarting (Русский)").

### Переключение при подключении

Это модуль, используемый для переключения выходного звукового сигнала на вновь подключенное устройство. Например, если вы подключите USB гарнитуру, то звук будет переведён на неё. Если вы её отключите, то звук вернётся на последнее используемое устройство. Данная функция могла казаться немного неотлаженной, но ей уделили много внимания в PulseAudio 8.0 и на текущий момент она должна работать стабильно.

Если вы хотите только протестировать работу модуля, то вы можете загрузить его во время выполнения, вызвав:

```
$ pactl load-module module-switch-on-connect

```

Если вы хотите сохранить данные настройки, то вам нужно добавить их в ваши локальные настройки pulseaudio или в файл /etc/pulse/default.pa (изменения будут применены во всей системе). В обоих случаях добавьте строку:

```
load-module module-switch-on-connect

```

В KDE/Plasma5, кроме того, вам следует отключить module-device-manager. Как только запускается Plasma5, она загружает (через start-pulseaudio-x11) модуль module-device-manager для pulseaudio для управления устройствами. Но этот модуль, очевидно, конфликтует с module-switch-on-connect. Таким образом, вам следует отключить этот модуль, отредактировав файл /bin/start-pulseaudio-x11 и закомментировав строки, относящиеся к KDE. Затем выполните выход и вход в систему для перезапуска сессии pulseaudio. Теперь переключение по подключению должно работать.

### Скрипт для переключения аналоговых выходов

Некоторые звуковые карты обладают несколькими аналоговыми выходами, которые можно переключать через профили Pulseaudio. Но переключение вручную может быть неудобным, и вы можете использовать для этого следующую команду:

```
$ pactl set-sink-port 'number of the card' 'port'

```

Таким образом, выбранный вами порт станет выходом по умолчанию. Пример:

```
$ pactl set-sink-port 0 "analog-output;output-speaker" 

```

Список портов можно получить, используя:

```
$ pactl list

```

Текущий выход можно отобразить командой:

```
$ pactl list sinks | grep "active profile"| cut -d ' ' -f 3-

```

Эти операции можно автоматизировать простым скриптом. Затем пользователь может назначить его на ярлык:

 `~/pa.sh (или любое другое название)` 
```
#!/bin/bash
# Этот скрипт использует уведомления kdialog для предупреждения пользователя о том, что текущий профиль изменён. Пользователь может доработать его для своих нужд или совсем изменить.

CURRENT_PROFILE=$(pactl list sinks | grep "active profile"| cut -d ' ' -f 3-)

if [ "$CURRENT_PROFILE" = "analog-output;output-speaker" ] ; then
        pactl set-sink-port 0 "analog-output;output-headphones-1"
        kdialog --title "Pulseaudio" --passivepopup "Headphone" 2 & 
else 
        pactl set-sink-port 0 "analog-output;output-speaker"      
        kdialog --title "Pulseaudio" --passivepopup  "Speaker" 2 &
fi

```

Этот скрипт предназначен для переключения между двумя профилями. Сначала он проверяет текущий профиль, а затем заменяет его. Пользователям необходимо изменить поле 'active profile' в соответствии с языком, который предоставил pactl. Пользователям, возможно, понадобится изменить номер карты и выхода для настройки под свою конкретную систему.

## Решение проблем

Смотрите [PulseAudio/Troubleshooting (Русский)](/index.php/PulseAudio/Troubleshooting_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "PulseAudio/Troubleshooting (Русский)").

## Смотрите также

*   [.asoundrc on ALSA wiki](http://www.alsa-project.org/main/index.php/Asoundrc)
*   [PulseAudio official site](http://www.pulseaudio.org/)
*   [PulseAudio FAQ](http://www.freedesktop.org/wiki/Software/PulseAudio/FAQ/)