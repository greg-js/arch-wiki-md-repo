**Состояние перевода:** На этой странице представлен перевод статьи [PulseAudio](/index.php/PulseAudio "PulseAudio"). Дата последней синхронизации: 10 октября 2015‎. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=PulseAudio&diff=0&oldid=403994).

[PulseAudio](https://en.wikipedia.org/wiki/ru:PulseAudio или [KDE](/index.php/KDE_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "KDE (Русский)"). Он служит в качестве прокси для звуковых приложений, используя существующие звуковые компоненты, такие как ядро [ALSA](/index.php/ALSA_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ALSA (Русский)") или [OSS](/index.php/OSS "OSS"). ALSA включена в Arch Linux по умолчанию, использование PulseAudio вместе с ALSA является наиболее распространённым сценарием.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
    *   [1.1 Модули PulseAudio](#.D0.9C.D0.BE.D0.B4.D1.83.D0.BB.D0.B8_PulseAudio)
*   [2 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [2.1 Файлы настроек](#.D0.A4.D0.B0.D0.B9.D0.BB.D1.8B_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B5.D0.BA)
        *   [2.1.1 daemon.conf](#daemon.conf)
        *   [2.1.2 default.pa](#default.pa)
        *   [2.1.3 client.conf](#client.conf)
    *   [2.2 Команда настроек](#.D0.9A.D0.BE.D0.BC.D0.B0.D0.BD.D0.B4.D0.B0_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B5.D0.BA)
*   [3 Выполнение](#.D0.92.D1.8B.D0.BF.D0.BE.D0.BB.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5)
    *   [3.1 Запуск вручную](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D0.B2.D1.80.D1.83.D1.87.D0.BD.D1.83.D1.8E)
*   [4 Настройка бакэндов](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D0.B1.D0.B0.D0.BA.D1.8D.D0.BD.D0.B4.D0.BE.D0.B2)
    *   [4.1 ALSA](#ALSA)
        *   [4.1.1 ALSA/dmix без захвата аппаратного устройства](#ALSA.2Fdmix_.D0.B1.D0.B5.D0.B7_.D0.B7.D0.B0.D1.85.D0.B2.D0.B0.D1.82.D0.B0_.D0.B0.D0.BF.D0.BF.D0.B0.D1.80.D0.B0.D1.82.D0.BD.D0.BE.D0.B3.D0.BE_.D1.83.D1.81.D1.82.D1.80.D0.BE.D0.B9.D1.81.D1.82.D0.B2.D0.B0)
    *   [4.2 OSS](#OSS)
        *   [4.2.1 ossp](#ossp)
        *   [4.2.2 Оболочка padsp](#.D0.9E.D0.B1.D0.BE.D0.BB.D0.BE.D1.87.D0.BA.D0.B0_padsp)
    *   [4.3 GStreamer](#GStreamer)
    *   [4.4 OpenAL](#OpenAL)
    *   [4.5 libao](#libao)
*   [5 Эквалайзер](#.D0.AD.D0.BA.D0.B2.D0.B0.D0.BB.D0.B0.D0.B9.D0.B7.D0.B5.D1.80)
    *   [5.1 Загрузка модуля эквалайзера и протокола dbus](#.D0.97.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B0_.D0.BC.D0.BE.D0.B4.D1.83.D0.BB.D1.8F_.D1.8D.D0.BA.D0.B2.D0.B0.D0.BB.D0.B0.D0.B9.D0.B7.D0.B5.D1.80.D0.B0_.D0.B8_.D0.BF.D1.80.D0.BE.D1.82.D0.BE.D0.BA.D0.BE.D0.BB.D0.B0_dbus)
    *   [5.2 Графический интерфейс](#.D0.93.D1.80.D0.B0.D1.84.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8.D0.B9_.D0.B8.D0.BD.D1.82.D0.B5.D1.80.D1.84.D0.B5.D0.B9.D1.81)
    *   [5.3 Загрузка эквалайзера и модуля DBus при каждой загрузке](#.D0.97.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B0_.D1.8D.D0.BA.D0.B2.D0.B0.D0.BB.D0.B0.D0.B9.D0.B7.D0.B5.D1.80.D0.B0_.D0.B8_.D0.BC.D0.BE.D0.B4.D1.83.D0.BB.D1.8F_DBus_.D0.BF.D1.80.D0.B8_.D0.BA.D0.B0.D0.B6.D0.B4.D0.BE.D0.B9_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B5)
*   [6 Приложения](#.D0.9F.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F)
    *   [6.1 QEMU](#QEMU)
    *   [6.2 AlsaMixer.app](#AlsaMixer.app)
    *   [6.3 XMMS2](#XMMS2)
    *   [6.4 Рабочая область KDE и Qt4](#.D0.A0.D0.B0.D0.B1.D0.BE.D1.87.D0.B0.D1.8F_.D0.BE.D0.B1.D0.BB.D0.B0.D1.81.D1.82.D1.8C_KDE_.D0.B8_Qt4)
    *   [6.5 Audacious](#Audacious)
    *   [6.6 Java/OpenJDK 6](#Java.2FOpenJDK_6)
    *   [6.7 Music Player Daemon (MPD)](#Music_Player_Daemon_.28MPD.29)
    *   [6.8 MPlayer](#MPlayer)
    *   [6.9 guvcview](#guvcview)
*   [7 Советы и хитрости](#.D0.A1.D0.BE.D0.B2.D0.B5.D1.82.D1.8B_.D0.B8_.D1.85.D0.B8.D1.82.D1.80.D0.BE.D1.81.D1.82.D0.B8)
    *   [7.1 Регулировка звука клавиатурой](#.D0.A0.D0.B5.D0.B3.D1.83.D0.BB.D0.B8.D1.80.D0.BE.D0.B2.D0.BA.D0.B0_.D0.B7.D0.B2.D1.83.D0.BA.D0.B0_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D0.B0.D1.82.D1.83.D1.80.D0.BE.D0.B9)
*   [8 Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
*   [9 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Установка

*   Требуется пакет: [pulseaudio](https://www.archlinux.org/packages/?name=pulseaudio)
*   Дополнительно: графические интерефейсы GTK: [paprefs](https://www.archlinux.org/packages/?name=paprefs) и [pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol)
*   Дополнительно: регулировка звука с помощью мультимедиа клавиш на клавиатуре: [pulseaudio-ctl](https://aur.archlinux.org/packages/pulseaudio-ctl/)
*   Дополнительно: консольные (CLI) микшеры: [ponymix](https://www.archlinux.org/packages/?name=ponymix) и [pamixer-git](https://aur.archlinux.org/packages/pamixer-git/)
*   Дополнительно: консольный (с поддержкой курсора) микшер: [pulsemixer-git](https://aur.archlinux.org/packages/pulsemixer-git/)
*   Дополнительно: web-интерфейс для регулировка звука: [PaWebControl](https://github.com/Siot/PaWebControl)
*   Дополнительно: иконка в системном трее: [pasystray-git](https://aur.archlinux.org/packages/pasystray-git/)
*   Дополнительно: апплет KDE4 плазма: [kdemultimedia-kmix](https://www.archlinux.org/packages/?name=kdemultimedia-kmix) и [kdeplasma-applets-veromix](https://aur.archlinux.org/packages/kdeplasma-applets-veromix/) (Если KMix/Veromix не удается подключиться к PulseAudio при загрузке, вы можете отредактировать `/etc/pulse/client.conf` включив `autospawn = yes` вместо `autospawn = no`.)
*   Дополнительно: KF5 плазма аплет: [kmix](https://www.archlinux.org/packages/?name=kmix) и [plasma-pa](https://www.archlinux.org/packages/?name=plasma-pa)
*   Если вы хотите использовать Гарнитуру Bluetooth или другое Bluetooth Аудио Устройство вместе с PulseAudio смотрите статью [Bluetooth headset](/index.php/Bluetooth_headset "Bluetooth headset").

**Примечание:** Some confusion can be made between [ALSA](/index.php/ALSA "ALSA") and PulseAudio. ALSA both includes a Linux kernel component with sound card drivers, and a userspace component, `libalsa`. [[1]](http://www.alsa-project.org/main/index.php/Download) PulseAudio only builds on the kernel component, but offers compability with `libalsa` through [pulseaudio-alsa](https://www.archlinux.org/packages/?name=pulseaudio-alsa). [[2]](http://www.freedesktop.org/wiki/Software/PulseAudio/FAQ/#index14h3)

### Модули PulseAudio

Некоторые модули PulseAudio были [убраны](https://www.archlinux.org/news/pulseaudio-split/) из основного пакета и должны быть установлены отдельно, если это необходимо.

## Настройка

### Файлы настроек

По умолчанию PulseAudio настроен на управление и автоматическое обнаружение всех звуковых карт. Он берёт под свой контроль все обнаруженные устройства ALSA, и перенаправляет все аудиопотоки на себя, делая демон PulseAudio центральной точкой настроек. Демон, в основном, должен работать "из коробки", требуя только нескольких незначительных изменений настроек.

PulseAudio будет сначала смотреть файлы настроек в домашнем каталоге `~/.config/pulse`, а затем в общесистемном `/etc/pulse`.

PulseAudio работает как демон сервера, который может работать или общесистемно или для каждого пользователя, с помощью архитектуры клиент/сервер. Без своих модулей демон сам по себе ничего не делает, кроме обеспечения API и размещения динамически загружаемых модулей. Вся маршрутизация аудио и обработка задач обрабатывается различными модулями. Вы можете найти подробный список всех доступных модулей в [Загружаемые Модули Pulseaudio (Англ.)](http://www.freedesktop.org/wiki/Software/PulseAudio/Documentation/User/Modules/). Чтобы включить их, Вы можете добавить строку `load-module <имя модуля из списка>` в `~/.config/pulse/default.pa`.

**Совет:**

*   Настоятельно советуем не редактировать общесистемные файлы настроек, вместо них редактируйте пользовательские. Создайте каталог `~/.config/pulse`, затем скопируйте (`cp /etc/pulse/ ~/.config/pulse`) файлы настроек системы в него, и редактируйте согласно Вашим требованиям.
*   Убедитесь, что Вы держите пользовательские настройки в синхронизации с изменениями в пакетных файлах `/etc/pulse/`. Иначе, PulseAudio может отказаться запускаться из-за ошибки в настройках.
*   Нет необходимости добавлять Вашего пользователя к группе audio, поскольку он использует [udev](/index.php/Udev_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Udev (Русский)") и *logind* для динамичного предоставления доступа к "в настоящее время активному" пользователю

#### daemon.conf

Определяет основные настройки, такие как: частоты дискретизации по умолчанию, используемые модулями, методы повторной выборки, планирование в реальном времени, и другие различные настройки, связанные с серверным процессом. Они не могут быть изменены во время выполнения, без перезапуска демона PulseAudio. Значения по умолчанию разумны для большинства пользователей.

<caption>Известные параметры настроек</caption>
| опция | описание |<caption></caption>
| system-instance (системный экземпляр) | Запустит демон как общесистемный экзеппляр. Крайне нежелательно, поскольку это может привести к проблемам безопасности. Полезно в (headless) системах, не имеющих никаких настоящих локальных пользователей. Значение по умолчанию `no`. |<caption></caption>
| resample-method (метод частоты дискретизации) | Какой метод частоты дискретизации (resampler) использовать, когда звук с несовместимыми частотами дискретизации должен быть передан между модулями (например, воспроизведение звука на 96 кГц на аппаратном обеспечении, поддерживающим только 48 кГц). Доступные resampler'ы могут быть перечислены с помощью `$ pulseaudio --dump-resample-methods`. Выберите и используйте лучший компромисс между загрузкой процессора и качеством звука.
**Совет:** В некоторых случаях PulseAudio будет генерировать высокую нагрузку на процессор. Это может произойти, когда несколько потоков передискретизируются (индивидуально). Если это используется в выбранном общем рабочем процессе, его следует продумать, чтобы создать дополнительное устройство вывода (sink) с соответствующей частотой дискретизации, которое может передавать в основное устройство вывода (main sink), передискретизируя только один раз.
 |<caption></caption>
| flat-volumes | `flat-volumes` масштабирует громкость устройства с громкостью "самого громкого" приложения. Например, повышение громкости вызова VoIP повысит аппаратную громкость и скорректирует звук аудиоплеера, таким образом, что понижать громкость аудиоплеера вручную нет необходимости. Значение по умолчанию `yes`.
**Важно:** Поведение значения по умолчанию, иногда, может сбивать с толку, и некоторые приложения не зная об этой функции, могут регулировать свою громкость к 100% при запуске, потенциально создавая неожиданно громкий звук. Для восстановления классического поведения (ALSA), установите это значение в `no`.
 |<caption></caption>
| default-fragments (фрагменты по умолчанию) | Аудиосэмплы разделяются на многократные фрагменты `default-fragment-size-msec`. Чем больше буфер, тем менее вероятен пропуск звука, когда система будет перегружена. С другой стороны это увеличит общую величину задержки. Увеличьте это значение, если у Вас есть проблемы. |

#### default.pa

Этот файл является сценарием запуска и используется для настройки модулей. Он анализируется и читается после завершения инициализации демона. Дополнительные команды могут быть отправлены во время выполнения с помощью `$ pactl` или `$ pacmd`. Сценарий запуска также может быть указан в командной строке, путем запуска PulseAudio в терминале, с помощью `$ pulseaudio -nC`. Это заставит демона загрузить модуль CLI и принимать настройки непосредственно из командной строки, выдавать получающуюся информацию или сообщения об ошибках на том же терминале. Это может быть полезно при отладке демона или тестирования различных модулей, перед постоянной установкой их на диск. Обратитесь к странице руководства `man pulse-cli-syntax`, для пояснений элементов синтаксиса

**Совет:**

*   Для перечисления доступных устройств вывода, выполните `$ pacmd list-sinks|egrep -i 'index:|name:'`. Задействованное в настоящее время устройство вывода по умолчанию, отмечено звёздочкой (*).
*   Редактируйте `~/.config/pulse/default.pa` для вставки/изменения команды установленного_по_умолчанию_устройства_вывода, использующей имя устройства вывода, поскольку повторная нумерация не может быть гарантирована.

#### `client.conf`

Это файл настроек, читающийся каждым клиентским приложением PulseAudio. Он используется для настройки опций во время выполнения для отдельных клиентов. Может использоваться чтобы устанавливать и настраивать устройство вывода по умолчанию и для статического запуска, а также позволять (или запрещать) клиентам автоматический запуск сервера, если он в настоящее время не работает.

### Команда настроек

Основная команда для настройки сервера во время выполнения является `$ pacmd`. Для списка опций выполните `$ pacmd --help`, или для входа в интерактивный режим оболочки выполните `$ pacmd` и `Ctrl+d` для выхода. Все модификации будут сразу применены.

После того, как новые настройки были проверены и удовлетворили Ваши потребности, соответственно отредактируйте `default.pa` чтобы изменения стали постоянными. Для некоторых основных настроек, смотрите [PulseAudio/Examples](/index.php/PulseAudio/Examples "PulseAudio/Examples").

**Совет:** Оставьте строку `load-module module-default-device-restore` в нетронутом файле `default.pa`. Это позволит вам перезапустить сервер в состояние по умолчанию, таким образом избегая любых неправильных установок.

Важно понять, что "sources" (источники) (процессы, устройства захвата) и доступные "sinks" (устройства вывода/приемники) (звуковые карты, серверы, другие процессы) можно выбрать через PulseAudio, это зависит от текущих аппаратных средств выбранного "Profile" (профиля). Эти "Профили" являются теми ALSA "pcms" перечисленные командой `aplay -L`, и более конкретно командой `pacmd list-cards`, которая будет включать строку "index:" (индекс), список начинающих "profiles:" (профилей) и строку "active profile: <...>" (активный профиль) на выводе, среди других вещей.

"active profile" (Активный профиль) может быть установлен командой `pacmd set-card-profile INDEX PROFILE` без запятой ( `,` ) разделяющей INDEX и PROFILE, где INDEX является просто числом на строке "index:" и имя PROFILE является всем показанным с начала любой строки под "профилем": *до* двоеточия и начала места, как показано командой `pacmd list-cards`. Например, `pacmd set-card-profile 0 output:analog-stereo+input:analog-stereo`.

"Профиль" проще выбрать с графическим инструментом как `pavucontrol`, под вкладкой "Configuration" (Настройка) или Параметрами настройки системы KDE, "Мультимедийные/Аудио и Параметры видео", под вкладкой "Audio Hardware Setup". Каждая аудио "Карта", которая являются теми устройствами, перечисленными командой `aplay -l`, или снова командой `pacmd list-cards`, будет иметь свой собственный выбор "Профиля". Когда "Профиль" был выбран, то доступные "источники" и "приемники" можно увидеть при помощи команд `pacmd list-sources` и `pacmd list-sinks`. Обратите внимание на то, что "индекс" доступных источников и приемников изменятся каждый раз, когда изменяется профиль карты.

Выбранный "Профиль" может быть проблемой для некоторых приложений, особенно Adobe Flash Player, обычно `/usr/lib/mozilla/plugins/libflashplayer.so` и `/usr/lib/PepperFlash/libpepflashplayer.so`. Часто, эти флэш-плееры будут работать только тогда, когда выбран один из профилей Стерео, иначе видео будет проигрываться без звука или просто "откажется" воспроизводиться. Когда все остальное перестало работать, Вы можете попробовать выбрать различные профили.

Конечно, при настройке некоторых вариаций Surround Sound (Объёмного Звука) в PulseAudio, должен быть выбран соответствующий профиль Surround. Прежде чем объёмный звук будет работать, сделайте такие вещи, как переназначение каналов динамиков (speaker channels).

## Выполнение

Начиная с [версии 7.0](http://www.freedesktop.org/wiki/Software/PulseAudio/Notes/7.0/) PulseAudio на Arch использует активацию сокета. [По умолчанию](https://projects.archlinux.org/svntogit/packages.git/commit/trunk?h=packages/pulseaudio&id=419bd740dc8), `pulseaudio.socket` включен для экземпляра [systemd/Пользователь](/index.php/Systemd/%D0%9F%D0%BE%D0%BB%D1%8C%D0%B7%D0%BE%D0%B2%D0%B0%D1%82%D0%B5%D0%BB%D1%8C "Systemd/Пользователь").

**Примечание:**

*   Для отключения `pulseaudio.socket` удостоверьтесь, что `$XDG_CONFIG_HOME/systemd/user` существует, и выполните `systemctl --user mask pulseaudio.socket`
*   Многие [окружения рабочих столов](/index.php/Desktop_environment_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Desktop environment (Русский)") автоматически запускают программы на основе [файлов desktop](/index.php/Desktop_entries#Autostart "Desktop entries") из каталога `/etc/xdg/autostart/`. В этом случае PulseAudio будет запущен автоматически независимо от состояния активации сокета

Для получения дополнительной информации посмотрите [PulseAudio: Выполнение](http://www.freedesktop.org/wiki/Software/PulseAudio/Documentation/User/Running/).

### Запуск вручную

PulseAudio может быть запущен вручную:

```
$ pulseaudio --start

```

И остановлен:

```
$ pulseaudio --kill

```

## Настройка бакэндов

### ALSA

Установите [pulseaudio-alsa](https://www.archlinux.org/packages/?name=pulseaudio-alsa) из [официальных репозиториев](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)"). Этот пакет содержит `/etc/asound.conf` необходимый для настройки ALSA с использованием PulseAudio.

Если вы используете систему x86_64, установите [lib32-libpulse](https://www.archlinux.org/packages/?name=lib32-libpulse) и [lib32-alsa-plugins](https://www.archlinux.org/packages/?name=lib32-alsa-plugins) если хотите получить звук в 32-битных [multilib](/index.php/Multilib "Multilib") программах, таких как: Wine, Skype и Steam.

Чтобы не допустить приложениям ALSA использовать эмуляцию OSS в обход PulseAudio (тем самым не давая другим приложениям воспроизводить звук), убедитесь, что модуль `snd_pcm_oss` не загружается при загрузке. Если в настоящее время загружен (`lsmod | grep oss`), отключите его, выполнив:

```
# rmmod snd_pcm_oss

```

#### ALSA/dmix без захвата аппаратного устройства

**Примечание:** Этот раздел описывает альтернативную настройку, которая, как правило, **не** рекомендуется .

Вы возможно захотите использовать ALSA непосредственно в большинстве Ваших приложений, при этом елси есть необходимость использовать приложения требующие PulseAudio. Следующие шаги позволяют Вам заставлять PulseAudio использовать dmix вместо того, чтобы "захватывать" устройство ALSA.

*   Удалите пакет [pulseaudio-alsa](https://www.archlinux.org/packages/?name=pulseaudio-alsa), обеспечивающий уровень совместимости между приложениями ALSA и PulseAudio. После этого Ваши приложения ALSA будут использовать ALSA напрямую, без "зацепки" Pulse.

*   Отредактируйте `/etc/pulse/default.pa`.

	Найдите и расскоментируйте строки, загружающие драйверы бэкэнда. Добавьте параметры **device** (устройство) следующим образом. Затем найдите и закомментируйте строки, загружающие модули автоматического обнаружения.

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

$ padsp OSSпрограмма

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

Установите [gst-plugins-good](https://www.archlinux.org/packages/?name=gst-plugins-good), или [gstreamer0.10-good-plugins](https://www.archlinux.org/packages/?name=gstreamer0.10-good-plugins), если Ваша программа имеет наследие реализации [GStreamer](/index.php/GStreamer "GStreamer").

### OpenAL

Приложение OpenAL должно использовать PulseAudio по умолчанию, но может быть настроено так, чтобы использовать именно его: `/etc/openal/alsoft.conf`  `drivers=pulse, alsa` 

### libao

Отредактируйте файл настроек libao:

 `/etc/libao.conf`  `default_driver=pulse` 

Обязательно удалите опцию alsa драйвера `dev=default` или настройте его для определения определенного имени устройства вывода Pulse (sink) или его числа.

**Примечание:** Вы можете держать libao стандартно на вывод драйвера *alsa* и его устройств по умолчанию, если Вы устанавливаете [pulseaudio-alsa](https://www.archlinux.org/packages/?name=pulseaudio-alsa), так как устройством вывода по умолчанию ALSA **является** PulseAudio.

## Эквалайзер

PulseAudio имеет интегрированную систему эквалайзера с 10 полосами. Для использования эквалайзера, сделайте следующее:

Установите [pulseaudio-equalizer](https://www.archlinux.org/packages/?name=pulseaudio-equalizer):

### Загрузка модуля эквалайзера и протокола dbus

```
$ pactl load-module module-equalizer-sink
$ pactl load-module module-dbus-protocol

```

### Графический интерфейс

выполните:

$ qpaeq

**Примечание:** Если qpaeq не произвёл никакого эффекта, установите [pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol) и измените "ALSA Playback on" на "FFT based equalizer on ...", во время работы медиапроигрывателя.

### Загрузка эквалайзера и модуля DBus при каждой загрузке

Отредактируйте файл `/etc/pulse/default.pa` или `~/.config/pulse/default.pa` вашим редактором, и добавьте следующие строки:

```
### Load the integrated PulseAudio equalizer and D-Bus module
load-module module-equalizer-sink
load-module module-dbus-protocol

```

**Примечание:** Устройство вывода эквалайзера должно быть загружено после того, как основное устройство вывода уже доступно.

## Приложения

### QEMU

Аудио драйвер, используемый QEMU, установлен с переменной окружения `QEMU_AUDIO_DRV`:

```
$ export QEMU_AUDIO_DRV=pa

```

Выполните следующую команду для связывания параметров настроек QEMU с PulseAudio:

```
$ qemu-system-x86_64 -audio-help | awk '/Name: pa/' RS=

```

Перечисленные опции могут быть экспортированы как переменные окружения, например:

```
$ export QEMU_PA_SINK=alsa_output.pci-0000_04_01.0.analog-stereo.monitor
$ export QEMU_PA_SOURCE=input
```

Чтобы получить список поддерживаемых драйверов эмуляции аудио:

```
$ qemu-system-x86_64 -soundhw help

```

Для гостевого использования, например, драйвера `ac97`, команда с QEMU `-soundhw ac97`.

**Примечание:** Эмулирование драйвера видеокарты для гостевой машины может также вызвать проблему с качеством звука. Тестируйте один за другим, чтобы заставить его работать. Вы можете перечислить возможные варианты с поомщью `qemu-system-x86_64 -h | grep vga`.

### AlsaMixer.app

Сделайте [alsamixer.app](https://aur.archlinux.org/packages/alsamixer.app/) dockapp для использования pulseaudio [windowmaker](https://www.archlinux.org/packages/?name=windowmaker), например:

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

### Рабочая область KDE и Qt4

PulseAudio будет автоматически использоваться приложениями KDE/Qt4\. Это поддерживается по умолчанию в микшере звука KDE. Для получения дополнительной информации посмотрите [страницу KDE, в wiki PulseAudio](http://www.pulseaudio.org/wiki/KDE). Один полезный совет с той страници: добавить `load-module module-device-manager` в `/etc/pulse/default.pa`.

Если бэкэнд phonon-gstreamer используется для Phonon, GStreamer должен также быть настроен, как описано в [#GStreamer](#GStreamer).

### Audacious

[Audacious](/index.php/Audacious_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Audacious (Русский)") изначально поддерживает PulseAudio. Для его использования установите Audacious Настройки -> Audio -> Current output plugin to 'PulseAudio Output Plugin'.

### Java/OpenJDK 6

Создайте "обертку" для исполняемой программы Java, использующей padsp, как замечено на странице [Java sound with PulseAudio](/index.php/Java#Java_sound_with_PulseAudio "Java").

### Music Player Daemon (MPD)

[Настройте](http://mpd.wikia.com/wiki/PulseAudio) [MPD](/index.php/Music_Player_Daemon_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Music Player Daemon (Русский)") на использование PulseAudio. Смотрите также раздел [Music Player Daemon/Tips and tricks#PulseAudio](/index.php/Music_Player_Daemon/Tips_and_tricks#PulseAudio "Music Player Daemon/Tips and tricks").

### MPlayer

[MPlayer](/index.php/MPlayer "MPlayer") изначально поддерживает вывод PulseAudio с опцией `-ao pulse`. Это также может быть настроено для установки по умолчанию на вывод PulseAudio, в `~/.mplayer/config` для конкретного пользователя, или для всей системы `/etc/mplayer/mplayer.conf`:

 `/etc/mplayer/mplayer.conf`  `ao=pulse` 

### guvcview

[guvcview](https://www.archlinux.org/packages/?name=guvcview) при использовании входа PulseAudio от [Веб-камеры](/index.php/Webcam_setup_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Webcam setup (Русский)"), аудиовход может быть в "приостановленном" режиме, в результате чего звук не будет записываться. Вы можете проверить это путем выполнения:

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

И затем перезапустите PulseAudio или Ваш компьютер. Теперь аудиовход будет "бездействовать", вметсо того, чтобы находиться в "приостановленном" режиме. Теперь guvcview будет писать звук правильно.

## Советы и хитрости

### Регулировка звука клавиатурой

Обозначьте следующие команды на своих кнопках регулировки громкости: `XF86AudioRaiseVolume`, `XF86AudioLowerVolume`, `XF86AudioMute`

Повысить громкость:

```
sh -c "pactl set-sink-mute 0 false ; pactl set-sink-volume 0 +5%"

```

Понизить громкость:

```
sh -c "pactl set-sink-mute 0 false ; pactl -- set-sink-volume 0 -5%"

```

Отключить/Включить звук:

```
pactl set-sink-mute 0 toggle

```

## Решение проблем

Смотрите [PulseAudio/Troubleshooting](/index.php/PulseAudio/Troubleshooting "PulseAudio/Troubleshooting").

## Смотрите также

*   [.asoundrc on ALSA wiki](http://www.alsa-project.org/main/index.php/Asoundrc)
*   [PulseAudio official site](http://www.pulseaudio.org/)
*   [PulseAudio FAQ](http://www.freedesktop.org/wiki/Software/PulseAudio/FAQ/)