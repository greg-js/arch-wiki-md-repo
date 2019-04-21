Ссылки по теме

*   [Среда рабочего стола](/index.php/%D0%A1%D1%80%D0%B5%D0%B4%D0%B0_%D1%80%D0%B0%D0%B1%D0%BE%D1%87%D0%B5%D0%B3%D0%BE_%D1%81%D1%82%D0%BE%D0%BB%D0%B0 "Среда рабочего стола")
*   [Экранный менеджер](/index.php/%D0%AD%D0%BA%D1%80%D0%B0%D0%BD%D0%BD%D1%8B%D0%B9_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80 "Экранный менеджер")
*   [Оконный менеджер](/index.php/%D0%9E%D0%BA%D0%BE%D0%BD%D0%BD%D1%8B%D0%B9_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80 "Оконный менеджер")
*   [Qt (Русский)](/index.php/Qt_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Qt (Русский)")
*   [SDDM (Русский)](/index.php/SDDM_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "SDDM (Русский)")
*   [Dolphin](/index.php/Dolphin "Dolphin")
*   [KDE Wallet](/index.php/KDE_Wallet "KDE Wallet")
*   [KDevelop](/index.php/KDevelop "KDevelop")
*   [Trinity](/index.php/Trinity "Trinity")
*   [Uniform Look for Qt and GTK Applications (Русский)](/index.php/Uniform_Look_for_Qt_and_GTK_Applications_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Uniform Look for Qt and GTK Applications (Русский)")

**Состояние перевода:** На этой странице представлен перевод статьи [KDE](/index.php/KDE "KDE"). Дата последней синхронизации: 20 апреля 2019\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=KDE&diff=0&oldid=571667).

KDE — проект, состоящий из [среды рабочего стола](/index.php/Desktop_environment_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Desktop environment (Русский)") (KDE Plasma), набора библиотек и фреймворков (KDE Frameworks), а также набора приложений (KDE Applications).

KDE активно поддерживает вики-ресурс [UserBase](https://userbase.kde.org/). Здесь пользователи могут получить наиболее актуальную и подробную информацию о большинстве приложений KDE.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Установка](#Установка)
    *   [1.1 KDE Plasma](#KDE_Plasma)
    *   [1.2 Приложения KDE](#Приложения_KDE)
    *   [1.3 Нестабильные версии](#Нестабильные_версии)
*   [2 Запуск Plasma](#Запуск_Plasma)
    *   [2.1 Используя экранный менеджер](#Используя_экранный_менеджер)
    *   [2.2 Используя консоль](#Используя_консоль)
*   [3 Настройка](#Настройка)
    *   [3.1 Персонализация](#Персонализация)
        *   [3.1.1 Рабочий стол Plasma](#Рабочий_стол_Plasma)
            *   [3.1.1.1 Темы](#Темы)
                *   [3.1.1.1.1 Внешний вид Qt и GTK+](#Внешний_вид_Qt_и_GTK+)
            *   [3.1.1.2 Аватар](#Аватар)
            *   [3.1.1.3 Виджеты](#Виджеты)
            *   [3.1.1.4 Звуковой апплет в системном трее](#Звуковой_апплет_в_системном_трее)
            *   [3.1.1.5 Отключение тени панели](#Отключение_тени_панели)
        *   [3.1.2 Декорации окон](#Декорации_окон)
        *   [3.1.3 Темы значков](#Темы_значков)
        *   [3.1.4 Экономия места на экране](#Экономия_места_на_экране)
        *   [3.1.5 Генерирование эскизов файлов](#Генерирование_эскизов_файлов)
    *   [3.2 Печать](#Печать)
    *   [3.3 Поддержка Samba/Windows](#Поддержка_Samba/Windows)
    *   [3.4 Комнаты KDE](#Комнаты_KDE)
    *   [3.5 Управление энергопотреблением](#Управление_энергопотреблением)
    *   [3.6 Автозапуск приложений](#Автозапуск_приложений)
    *   [3.7 Phonon](#Phonon)
        *   [3.7.1 Какой бекенд использовать?](#Какой_бекенд_использовать?)
*   [4 Приложения](#Приложения)
    *   [4.1 Системное администрирование](#Системное_администрирование)
        *   [4.1.1 Сочетание клавиш для остановки X-сервера](#Сочетание_клавиш_для_остановки_X-сервера)
        *   [4.1.2 KCM](#KCM)
    *   [4.2 Локальный поисковик](#Локальный_поисковик)
    *   [4.3 Веб-браузеры](#Веб-браузеры)
    *   [4.4 PIM](#PIM)
        *   [4.4.1 Akonadi](#Akonadi)
            *   [4.4.1.1 PostgreSQL](#PostgreSQL)
            *   [4.4.1.2 SQLite](#SQLite)
            *   [4.4.1.3 Отключение Akonadi](#Отключение_Akonadi)
    *   [4.5 KDE Telepathy](#KDE_Telepathy)
        *   [4.5.1 Использование Telegram с KDE Telepathy](#Использование_Telegram_с_KDE_Telepathy)
    *   [4.6 KDE Connect](#KDE_Connect)
*   [5 Советы и рекомендации](#Советы_и_рекомендации)
    *   [5.1 Использование альтернативного оконного менеджера](#Использование_альтернативного_оконного_менеджера)
        *   [5.1.1 Сеанс KDE/Openbox](#Сеанс_KDE/Openbox)
        *   [5.1.2 Включение композитных эффектов](#Включение_композитных_эффектов)
    *   [5.2 Настройка разрешения экрана / нескольких мониторов](#Настройка_разрешения_экрана_/_нескольких_мониторов)
    *   [5.3 Настройка ICC-профилей](#Настройка_ICC-профилей)
    *   [5.4 Отключение открытия Меню запуска приложений клавишей Super (Windows)](#Отключение_открытия_Меню_запуска_приложений_клавишей_Super_(Windows))
    *   [5.5 Отключение отображения закладок браузера в меню приложений](#Отключение_отображения_закладок_браузера_в_меню_приложений)
*   [6 Решение проблем](#Решение_проблем)
    *   [6.1 Шрифты](#Шрифты)
        *   [6.1.1 Шрифты в KDE Plasma выглядят плохо](#Шрифты_в_KDE_Plasma_выглядят_плохо)
        *   [6.1.2 Огромные или непропорциональные буквы](#Огромные_или_непропорциональные_буквы)
    *   [6.2 Настройки](#Настройки)
        *   [6.2.1 Странное поведение рабочего стола Plasma](#Странное_поведение_рабочего_стола_Plasma)
        *   [6.2.2 Очистка кэша для решения проблем с обновлением](#Очистка_кэша_для_решения_проблем_с_обновлением)
    *   [6.3 Графика](#Графика)
        *   [6.3.1 Получение текущего состояния KWin для поддержки и отладки](#Получение_текущего_состояния_KWin_для_поддержки_и_отладки)
        *   [6.3.2 Отключение эффектов рабочего стола вручную или автоматически для определённых приложений](#Отключение_эффектов_рабочего_стола_вручную_или_автоматически_для_определённых_приложений)
        *   [6.3.3 Включение прозрачности](#Включение_прозрачности)
        *   [6.3.4 Отключение композитного режима](#Отключение_композитного_режима)
        *   [6.3.5 Мерцание окон в полноэкранном режиме при включённом композитном режиме](#Мерцание_окон_в_полноэкранном_режиме_при_включённом_композитном_режиме)
        *   [6.3.6 Разрыв изображения с NVIDIA](#Разрыв_изображения_с_NVIDIA)
        *   [6.3.7 Курсор иногда отображается неправильно](#Курсор_иногда_отображается_неправильно)
        *   [6.3.8 Непригодное для использования множество разрешений экрана](#Непригодное_для_использования_множество_разрешений_экрана)
        *   [6.3.9 Размытые иконки в системном трее](#Размытые_иконки_в_системном_трее)
    *   [6.4 Звук](#Звук)
        *   [6.4.1 Отсутствие звука после выхода из ждущего режима](#Отсутствие_звука_после_выхода_из_ждущего_режима)
        *   [6.4.2 MP3-файлы не воспроизводятся с бекендом GStreamer в Phonon](#MP3-файлы_не_воспроизводятся_с_бекендом_GStreamer_в_Phonon)
    *   [6.5 Управление электропитанием](#Управление_электропитанием)
        *   [6.5.1 Отсутствие ждущего/спящего режима](#Отсутствие_ждущего/спящего_режима)
    *   [6.6 KMail](#KMail)
        *   [6.6.1 Сброс настроек Akonadi для решения проблем с KMail](#Сброс_настроек_Akonadi_для_решения_проблем_с_KMail)
        *   [6.6.2 Пустая папка входящих сообщений в IMAP-аккаунте KMail](#Пустая_папка_входящих_сообщений_в_IMAP-аккаунте_KMail)
        *   [6.6.3 Ошибка авторизации EWS-аккаунта в KMail](#Ошибка_авторизации_EWS-аккаунта_в_KMail)
    *   [6.7 Сеть](#Сеть)
        *   [6.7.1 Зависания при использовании автоматического монтирования NFS-раздела](#Зависания_при_использовании_автоматического_монтирования_NFS-раздела)
    *   [6.8 Слишком частое журналирование событий QXcbConnection](#Слишком_частое_журналирование_событий_QXcbConnection)
    *   [6.9 Приложения на KF5/Qt 5 не отображают значки в i3/FVWM/awesome](#Приложения_на_KF5/Qt_5_не_отображают_значки_в_i3/FVWM/awesome)
    *   [6.10 Проблемы с сохранением учётных данных и постоянно появляющимися диалогами KWallet](#Проблемы_с_сохранением_учётных_данных_и_постоянно_появляющимися_диалогами_KWallet)
    *   [6.11 Discover не отображает никакие приложения](#Discover_не_отображает_никакие_приложения)
    *   [6.12 Высокая нагрузка kscreenlocker_greet на ЦП при использовании драйверов NVIDIA](#Высокая_нагрузка_kscreenlocker_greet_на_ЦП_при_использовании_драйверов_NVIDIA)
    *   [6.13 "OS error 22" при выполнении Akonadi на ZFS](#"OS_error_22"_при_выполнении_Akonadi_на_ZFS)
    *   [6.14 Не работает прокрутка неактивных окон в некоторых программах](#Не_работает_прокрутка_неактивных_окон_в_некоторых_программах)
*   [7 Смотрите также](#Смотрите_также)

## Установка

### KDE Plasma

**Примечание:** Перед тем, как устанавливать KDE Plasma, убедитесь, что в вашей системе установлен и настроен сервер [Xorg](/index.php/Xorg_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xorg (Русский)").

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") мета-пакет [plasma-meta](https://www.archlinux.org/packages/?name=plasma-meta) или группу пакетов [plasma](https://www.archlinux.org/groups/x86_64/plasma/). Для получения информации о различиях между ними смотрите статью [Группа пакетов](/index.php/%D0%93%D1%80%D1%83%D0%BF%D0%BF%D0%B0_%D0%BF%D0%B0%D0%BA%D0%B5%D1%82%D0%BE%D0%B2 "Группа пакетов").

Если вам нужна более минималистичная Plasma (с меньшим количеством установленных пакетов и приложений), [установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [plasma-desktop](https://www.archlinux.org/packages/?name=plasma-desktop).

Для поддержки [Wayland](/index.php/Wayland_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Wayland (Русский)") также требуется установить пакет [plasma-wayland-session](https://www.archlinux.org/packages/?name=plasma-wayland-session).

### Приложения KDE

Чтобы установить все приложения KDE (KDE Applications), установите группу пакетов [kde-applications](https://www.archlinux.org/groups/x86_64/kde-applications/) или мета-пакет [kde-applications-meta](https://www.archlinux.org/packages/?name=kde-applications-meta). Обратите внимание, что установятся только Приложения KDE, а не [среда рабочего стола](/index.php/%D0%A1%D1%80%D0%B5%D0%B4%D0%B0_%D1%80%D0%B0%D0%B1%D0%BE%D1%87%D0%B5%D0%B3%D0%BE_%D1%81%D1%82%D0%BE%D0%BB%D0%B0 "Среда рабочего стола") KDE Plasma.

### Нестабильные версии

Для получения информации о нестабильных версиях KDE Plasma и KDE Applications смотрите статью [Официальные репозитории#kde-unstable](/index.php/%D0%9E%D1%84%D0%B8%D1%86%D0%B8%D0%B0%D0%BB%D1%8C%D0%BD%D1%8B%D0%B5_%D1%80%D0%B5%D0%BF%D0%BE%D0%B7%D0%B8%D1%82%D0%BE%D1%80%D0%B8%D0%B8#kde-unstable "Официальные репозитории").

## Запуск Plasma

**Примечание:** Несмотря на то, что KDE Plasma можно запустить используя [Wayland (Русский)](/index.php/Wayland_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Wayland (Русский)"), на данный момент, в Plasma 5.13, отсутствуют некоторые функции и есть известные проблемы. Для получения информации об актуальных проблемах смотрите статью [Plasma 5.13 Errata](https://community.kde.org/Plasma/5.13_Errata#Wayland) и [доску Plasma on Wayland](https://phabricator.kde.org/project/board/99/) с текущим состоянием разработки. Используйте [Xorg (Русский)](/index.php/Xorg_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xorg (Русский)") для наиболее полных возможностей и стабильной работы.

KDE Plasma можно запустить с помощью [экранного менеджера](/index.php/Display_manager_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Display manager (Русский)") или консоли.

### Используя экранный менеджер

*   Выберите *Plasma* для запуска нового сеанса в [Xorg (Русский)](/index.php/Xorg_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xorg (Русский)").
*   [Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") [plasma-wayland-session](https://www.archlinux.org/packages/?name=plasma-wayland-session) и выберите *Plasma (Wayland)* для запуска нового сеанса в [Wayland (Русский)](/index.php/Wayland_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Wayland (Русский)").

**Примечание:** Проприетарный драйвер [NVIDIA (Русский)](/index.php/NVIDIA_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "NVIDIA (Русский)") требует поддержки EGLStreams в Wayland, что будет реализовано в KDE Plasma, [начиная с версии 5.16](https://www.phoronix.com/scan.php?page=news_item&px=EGLStreams-Merged-KWin-5.16). До тех пор данная проблема решается следующими способами:

*   Использованием свободного драйвера [Nouveau (Русский)](/index.php/Nouveau_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Nouveau (Русский)").
*   Использованием сеанса Xorg.

### Используя консоль

Для запуска KDE Plasma с помощью [xinit/startx](/index.php/Xinitrc_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xinitrc (Русский)"), добавьте строку `exec startkde` в файл `.xinitrc`. Также если вы хотите автоматически запускать [Xorg (Русский)](/index.php/Xorg_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xorg (Русский)") при входе в систему, ознакомьтесь со статьёй [xinitrc (Русский)#Автозапуск X при входе в систему](/index.php/Xinitrc_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Автозапуск_X_при_входе_в_систему "Xinitrc (Русский)").

Для запуска сеанса KDE Plasma с [Wayland (Русский)](/index.php/Wayland_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Wayland (Русский)") из консоли, выполните `XDG_SESSION_TYPE=wayland dbus-run-session startplasmacompositor`.[[1]](https://community.kde.org/KWin/Wayland#Start_a_Plasma_session_on_Wayland)

## Настройка

Большинство настроек приложений KDE находятся в каталоге `~/.config/`. Однако, KDE преимущественно настраивается в приложении **Параметры системы**, которое также запускается в терминале командой `systemsettings5`.

### Персонализация

#### Рабочий стол Plasma

##### Темы

[Темы KDE Plasma](https://store.kde.org/browse/cat/104/) определяют вид панелей и плазмоидов. Для большего удобства, многие темы доступны в [официальных репозиториях](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)") и [AUR](https://aur.archlinux.org/packages.php?K=plasma+theme).

Также темы KDE Plasma устанавливаются в приложении *Параметры системы > Оформление рабочей среды > Тема рабочего стола > Загрузить новые темы*.

[KDE-Store](https://store.kde.org/) предлагает ещё больше опций персонализации KDE Plasma, например, темы для [SDDM (Русский)](/index.php/SDDM_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "SDDM (Русский)") и заставки.

###### Внешний вид Qt и GTK+

**Совет:** Для единого внешнего вида тем на GTK и Qt, ознакомтесь со статьёй [Uniform look for Qt and GTK applications (Русский)](/index.php/Uniform_look_for_Qt_and_GTK_applications_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Uniform look for Qt and GTK applications (Русский)").

	Qt4

Тема Breeze более недоступна для Qt4, так как её нельзя собрать без пакетов KDE 4, которые были удалены из репозитория *extra* в августе 2018 ([FS#59784](https://bugs.archlinux.org/task/59784)). Тем не менее, можно установить пакет [breeze-gtk](https://www.archlinux.org/packages/?name=breeze-gtk) и выбрать GTK+ как стиль графического интерфейса в `qtconfig-qt4`.

	GTK+

Рекомендуемая тема для приложений на GTK+ – это [breeze-gtk](https://www.archlinux.org/packages/?name=breeze-gtk) или [gnome-breeze-git](https://aur.archlinux.org/packages/gnome-breeze-git/). Данные темы имитируют дизайн Breeze, использующийся в KDE Plasma. Установите [kde-gtk-config](https://www.archlinux.org/packages/?name=kde-gtk-config) (часть группы пакетов [plasma](https://www.archlinux.org/groups/x86_64/plasma/)) и выберите установленную тему GTK для GTK2/GTK3 в приложении *Параметры системы > Оформление приложений > Стиль программ GNOME (GTK+)*.

В некоторых случаях, подсказки в приложениях на GTK+ имеют белый текст на белом фоне, что заметно усложняет их чтение. Чтобы изменить цвета в GTK2-приложениях, найдите раздел для подсказок ("tooltips") в файле `.gtkrc-2.0` и измените его. Для GTK3-приложений измените два файла: `gtk.css` и `settings.ini`. Также попробуйте снять флажок с *Применять указанные цвета к приложениям не на Qt* в приложении *Параметры системы* > *Цвета*.

Некоторые GTK2-приложения (например, [vuescan-bin](https://aur.archlinux.org/packages/vuescan-bin/)) всё равно плохо смотрятся из-за невидимых флажков с темой Breeze или Adwaita в KDE Plasma. Для решения этой проблемы, установите и выберите, к примеру, тему Numix-Frost-Light из пакета [numix-frost-themes](https://aur.archlinux.org/packages/numix-frost-themes/) в приложении *Параметры системы* > *Оформление приложений* > *Стиль программ GNOME (GTK+)* > *Выберите тему для GTK+ 2.x*. Numix-Frost-Light также выглядит похоже на Breeze.

##### Аватар

Аватар пользователя задаётся в разделе *Параметры системы > Учётная запись > Управление пользователями*.

Если вы не можете найти раздел *Управление пользователями*, установите пакет [user-manager](https://www.archlinux.org/packages/?name=user-manager).

##### Виджеты

Плазмоиды представляют собой небольшие приложения (бинарные или скриптовые) для KDE Plasma, предназначенные для расширения функциональности рабочего стола.

Самый лёгкий способ установить скриптовые плазмоиды – это вызвать контекстное меню панели или рабочего стола и выбрать *Добавить виджеты > Пополнить список виджетов > Получить новые виджеты Plasma*. Здесь вы сможете устанавливать, удалять и обновлять любые виджеты, размещенные на [store.kde.org](https://store.kde.org/).

Также многие бинарные плазмоиды доступны в [AUR](https://aur.archlinux.org/packages.php?K=plasmoid).

##### Звуковой апплет в системном трее

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") [plasma-pa](https://www.archlinux.org/packages/?name=plasma-pa) или [kmix](https://www.archlinux.org/packages/?name=kmix) (запустите Kmix из Меню запуска приложений). Обратите внимание, что [plasma-pa](https://www.archlinux.org/packages/?name=plasma-pa) устанавливается вместе с пакетом [plasma](https://www.archlinux.org/groups/x86_64/plasma/) и не требует настройки.

**Примечание:** Чтобы настроить [шаг регулировки звука](https://bugs.kde.org/show_bug.cgi?id=313579#c28), добавьте `VolumePercentageStep=*шаг*` в раздел `[Global]` файла `~/.config/kmixrc`, установив желаемый шаг (целое число).

##### Отключение тени панели

В связи с тем, что панель KDE Plasma находится поверх других окон, её тень всегда падает на них. [[2]](https://bbs.archlinux.org/viewtopic.php?pid=1228394#p1228394) Для отключения данной функции, без влияния на какие-либо другие тени, [установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") [xorg-xprop](https://www.archlinux.org/packages/?name=xorg-xprop) и выполните данную команду:

```
$ xprop -remove _KDE_NET_WM_SHADOW

```

затем кликните курсором мыши на панель. [[3]](https://forum.kde.org/viewtopic.php?f=285&t=121592) Для автоматизации данных действий установите [xorg-xwininfo](https://www.archlinux.org/packages/?name=xorg-xwininfo) и создайте следующий скрипт:

 `/usr/local/bin/kde-no-shadow` 
```
#!/bin/bash
for WID in $(xwininfo -root -tree | sed '/"Plasma": ("plasmashell" "plasmashell")/!d; s/^  *\([^ ]*\) .*/\1/g'); do
   xprop -id $WID -remove _KDE_NET_WM_SHADOW
done

```

Задайте права исполнения данного скрипта:

```
# chmod 755 /usr/local/bin/kde-no-shadow

```

Скрипт можно добавить в автоматический запуск при входе в систему с помощью кнопки *Добавить сценарий* в приложении *Параметры системы* > *Запуск и завершение* > *Автозапуск*:

```
$ kcmshell5 autostart

```

#### Декорации окон

[Декорации окон](https://store.kde.org/browse/cat/114/) настраиваются в приложении *Параметры системы > Оформление приложений > Оформление окон*.

Здесь вы также можете загрузить и установить новые темы оформления. Кроме того, некоторые из них доступны в [AUR](https://aur.archlinux.org/packages.php?K=kde+window+decoration).

#### Темы значков

Темы значков устанавливаются и изменяются в приложении *Параметры системы > Значки*.

**Примечание:** Все современные среды рабочего стола для Linux используют одинаковый формат значков, но в средах вроде [GNOME (Русский)](/index.php/GNOME_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GNOME (Русский)") используется меньше значков (особенно в меню и панелях инструментов). В связи с тем, что в темах для таких сред, как правило, не хватает значков, используемых в Plasma и приложениях KDE, рекомендуется устанавливать темы совместимые с Plasma.

**Совет:** В связи с тем, что некоторые темы значков не наследуют их от стандартной темы, вам может не хватать определённых значков. Чтобы наследовать их от Breeze, добавьте `breeze` в массив `Inherits=` в файле `/usr/share/icon/*theme-name*/index.theme`. Например: `Inherits=breeze,hicolor`. Данный процесс придётся повторять после каждого обновления темы значков. Как вариант, воспользуйтесь [Pacman hooks](/index.php/Pacman_hooks "Pacman hooks") для автоматизации этих действий.

#### Экономия места на экране

Рабочая среда Plasma Netbook была удалена из Plasma 5, подробности доступны на [официальном форуме](https://forum.kde.org/viewtopic.php?f=289&t=126631&p=335947&hilit=plasma+netbook#p335899). Но несмотря на это, можно добиться похоже результата отредактировав файл `~/.config/kwinrc`, добавив строку `BorderlessMaximizedWindows=true` в секции `[Windows]`.

#### Генерирование эскизов файлов

Для генерирования эскизов медиафайлов, для предпросмотра в Dolphin или на рабочем столе, [установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакеты [kdegraphics-thumbnailers](https://www.archlinux.org/packages/?name=kdegraphics-thumbnailers) и [ffmpegthumbs](https://www.archlinux.org/packages/?name=ffmpegthumbs).

Затем выберите категории эскизов для отображения на рабочем столе: кликните ПКМ на обоях и перейдите в *Настроить рабочий стол* > *Значки* > *Дополнительно*.

В *Dolphin* данная функция находится в *Настройках Dolphin* > *Главное* > *Миниатюры*.

### Печать

**Совет:** Используйте веб-интерфейс [CUPS (Русский)](/index.php/CUPS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "CUPS (Русский)") для более быстрой настройки. Принтеры, настроенные таким образом, могут быть использованы приложениями KDE.

Также принтеры можно настроить в приложении *Параметры системы > Принтеры*. Для этого [установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакеты [print-manager](https://www.archlinux.org/packages/?name=print-manager) и [cups](https://www.archlinux.org/packages/?name=cups). Подробнее о настройке CUPS вы можете прочитать на странице [CUPS (Русский)#Настройка](/index.php/CUPS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Настройка "CUPS (Русский)").

### Поддержка Samba/Windows

Если вы хотите получить доступ к службам Windows, установите [Samba](/index.php/Samba "Samba") (доступна с пакетом [samba](https://www.archlinux.org/packages/?name=samba)).

Для обмена файлами Dolphin требует пакет [kdenetwork-filesharing](https://www.archlinux.org/packages/?name=kdenetwork-filesharing) и настроить общий каталог (userhares), который отсутствует в стандартном файле настроек (`smb.conf`). Инструкции по его добавлению приведены на странице [Samba (Русский)#Создание ресурсов общего доступа от имени обычного пользователя](/index.php/Samba_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Создание_ресурсов_общего_доступа_от_имени_обычного_пользователя "Samba (Русский)"). После выполнения инструкций обмен файлами в Dolphin заработает "из коробки" (после перезапуска Samba).

**Совет:** Используйте `*` (звёздочку) в имени и пароле пользователя для доступа к общему каталогу Windows без аутентификации в диалоге Dolphin.

В отличии от файловых менеджеров основанных на [GTK+ (Русский)](/index.php/GTK%2B_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GTK+ (Русский)") и использующих GVfs также для открытия программ, открытие файлов из общего каталога Samba в Dolphin (использующего KIO) сначала копирует файл целиком в локальную систему перед его открытием в большинстве программ (исключение — [VLC](/index.php/VLC "VLC")). Для решения этой проблемы можно использовать файловые менеджеры на основе GTK, например, [thunar](https://www.archlinux.org/packages/?name=thunar) с [gvfs](https://www.archlinux.org/packages/?name=gvfs) и [gvfs-smb](https://www.archlinux.org/packages/?name=gvfs-smb) (и [gnome-keyring](https://www.archlinux.org/packages/?name=gnome-keyring) для сохранения учётных данных).

Также можно [смонтировать](/index.php/File_systems_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Монтирование_файловой_системы "File systems (Русский)") общий каталог Samba с помощью [cifs-utils](https://www.archlinux.org/packages/?name=cifs-utils). Так, для Plasma это будет казаться локальной папкой к которой можно обращаться как обычно. Для более подробной информации смотрите статьи [Samba (Русский)#Ручное монтирование](/index.php/Samba_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Ручное_монтирование "Samba (Русский)") и [Samba (Русский)#Автоматическое монтирование](/index.php/Samba_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Автоматическое_монтирование "Samba (Русский)").

Для настройки подключения к Samba из графического интерфейса можно использовать [samba-mounter-git](https://aur.archlinux.org/packages/samba-mounter-git/), который предлагает практически ту же самую функциональность, но доступную в приложении *Параметры системы* > *Network Drivers*. Тем не менее, данная функциональность может ломаться с выходом новых версий KDE Plasma.

### Комнаты KDE

[Комнаты KDE](https://userbase.kde.org/Plasma#Activities) (*Desktop Activities*) представляют собой специальные рабочие пространства, для каждого из которых можно задавать независимые настройки.

### Управление энергопотреблением

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") [powerdevil](https://www.archlinux.org/packages/?name=powerdevil) для получения встроенной службы управления энергопотреблением Plasma. Данная служба предлагает дополнительные возможности по оптимизации энергопотребления, регулировке яркости экрана (если поддерживается) и получению информации о состоянии аккумуляторов устройств.

В качестве альтернативного пакета, который не зависит от [NetworkManager (Русский)](/index.php/NetworkManager_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "NetworkManager (Русский)") и [Bluez](/index.php/Bluez "Bluez"), можно воспользоваться [powerdevil-light](https://aur.archlinux.org/packages/powerdevil-light/).

**Примечание:**

*   Powerdevil может не [переопределять](/index.php/Power_management#Power_managers "Power management") все настройки logind (например, закрытие крышки ноутбука). В таких случаях, потребуется изменить настройки самого logind — более подробная информация доступна в статье [Power management#Power management with systemd](/index.php/Power_management#Power_management_with_systemd "Power management").
*   Также поведение, описанное выше, может быть вызвано параметром *LidSwitchIgnoreInhibited* в logind, которое по умолчанию равняется *yes*. [[4]](https://bbs.archlinux.org/viewtopic.php?pid=1649022#p1649022)

### Автозапуск приложений

KDE Plasma может автоматически запускать приложения и скрипты во время включения и выключения. Для добавление приложения или скрипта в автозапуск, перейдите в *Параметры системы > Запуск и Завершение > Автозапуск*. Для приложений будет создан файл *.desktop*, для скриптов — [символическая ссылка](https://en.wikipedia.org/wiki/ru:%D0%A1%D0%B8%D0%BC%D0%B2%D0%BE%D0%BB%D0%B8%D1%87%D0%B5%D1%81%D0%BA%D0%B0%D1%8F_%D1%81%D1%81%D1%8B%D0%BB%D0%BA%D0%B0 "wikipedia:ru:Символическая ссылка").

**Примечание:**

*   Приложения могут быть автоматически запущены только во время входа в систему, тогда как скрипты могут быть также запущены во время выключения системы или даже перед запуском KDE Plasma.
*   Скрипты будут запущены только в том случае, если они являются [исполняемыми](/index.php/Help:Reading_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Сделать_исполняемым "Help:Reading (Русский)").

*   Разместите [ярлыки приложений](/index.php/%D0%AF%D1%80%D0%BB%D1%8B%D0%BA%D0%B8_%D0%BF%D1%80%D0%B8%D0%BB%D0%BE%D0%B6%D0%B5%D0%BD%D0%B8%D0%B9 "Ярлыки приложений") (например, файлы *.desktop*) в соответствующей директории [XDG Autostart](/index.php/XDG_Autostart "XDG Autostart").

*   Разместите или создайте символическую ссылку на скрипты в одной из следующих директорий:

	`~/.config/plasma-workspace/env/`

	для запуска скриптов во время входа в систему, перед запуском KDE Plasma.

	`~/.config/autostart-scripts/`

	для запуска скриптов во время входа в систему.

	`~/.config/plasma-workspace/shutdown/`

	для запуска скриптов во время выключения системы.

### Phonon

Из [Википедии](https://en.wikipedia.org/wiki/ru:Phonon "wikipedia:ru:Phonon"):

	Phonon — мультимедийный фреймворк от KDE, который предоставляет API для разработки мультимедиа-приложений. Phonon использует набор расширяемых модулей, выполняющих реальную работу.

Phonon широко используется в среде KDE, как для аудио (например, для системных уведомлений), так и для видео (например, для видео-миниатюр в [Dolphin](/index.php/Dolphin "Dolphin")).

#### Какой бекенд использовать?

На ваш выбор предоставляются бекенды основанные на [GStreamer](/index.php/GStreamer "GStreamer") и [VLC](/index.php/VLC "VLC"), каждый из которых имеет версию для приложений на Qt4 и Qt5 ([phonon-qt4-gstreamer](https://aur.archlinux.org/packages/phonon-qt4-gstreamer/), [phonon-qt5-gstreamer](https://www.archlinux.org/packages/?name=phonon-qt5-gstreamer) – [phonon-qt4-vlc](https://aur.archlinux.org/packages/phonon-qt4-vlc/), [phonon-qt5-vlc](https://www.archlinux.org/packages/?name=phonon-qt5-vlc)).

По умолчанию, бекенд на VLC имеет [более высокий приоритет](https://www.phoronix.com/scan.php?page=news_item&px=MTUwNDM), но некоторые популярные дистрибутивы Linux (например, Kubuntu и Fedora-KDE) предпочитают использовать GStreamer, в котором не используются запатентованные кодеки MPEG. Стоит отметить, что у обоих бекендов немного [отличаются возможности](https://community.kde.org/Phonon/FeatureMatrix).

Также для бекенда на Gstreamer существуют опциональные зависимости [кодеков](/index.php/Codecs_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Codecs (Русский)"):

*   [gst-libav](https://www.archlinux.org/packages/?name=gst-libav) — кодеки Libav.
*   [gst-plugins-good](https://www.archlinux.org/packages/?name=gst-plugins-good) — поддержка PulseAudio и дополнительные кодеки.
*   [gst-plugins-ugly](https://www.archlinux.org/packages/?name=gst-plugins-ugly) — дополнительные кодеки.
*   [gst-plugins-bad](https://www.archlinux.org/packages/?name=gst-plugins-bad) — дополнительные кодеки.

В прошлом были разработаны и другие бекенды, но они больше не поддерживаются и их пакеты были удалены из AUR.

**Примечание:**

*   Вы можете установить несколько бекендов и изменять их приоритет в приложении *Параметры системы > Мультимедиа > Звук и видео > Библиотеки воспроизведения*.
*   Согласно [форуму KDE](https://forum.kde.org/viewtopic.php?f=250&t=126476&p=335080), у бекенда на VLC отсутствует поддержка [ReplayGain](https://en.wikipedia.org/wiki/ru:ReplayGain "wikipedia:ru:ReplayGain").
*   Во время использования бекенда на VLC могут наблюдаться сбои в работе приложений когда Plasma хочет отправить уведомление со звуком (также и в некоторых других случаях) [[5]](https://forum.kde.org/viewtopic.php?f=289&t=135956). Данную проблему можно попробовать решить обновлением кеша плагинов VLC:

 `# /usr/lib/vlc/vlc-cache-gen /usr/lib/vlc/plugins` 

## Приложения

Проект KDE поставляет набор приложений, интегрированных в среду рабочего стола KDE Plasma, полный список которых доступен в группе пакетов [kde-applications](https://www.archlinux.org/groups/x86_64/kde-applications/). Также в категории [Category:KDE (Русский)](/index.php/Category:KDE_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Category:KDE (Русский)") доступны статьи, относящиеся к приложениям KDE.

Кроме приложений, поставляемых в KDE Applications, доступны также и многие другие, дополняющие KDE Plasma. Некоторые из них описаны ниже.

### Системное администрирование

#### Сочетание клавиш для остановки X-сервера

Перейдите в *Параметры системы > Устройства ввода > Клавиатура > Дополнительно (вкладка)* и отметьте флажок *"Комбинация клавиш для прерывания работы X-сервера"*.

#### KCM

Модули KCM (**KC**onfig **M**odule) добавляют компоненты настройки системы в приложение *Параметры системы*. Также они доступны из командой строки с помощью команды *kcmshell5*

*   **sddm-kcm** — Модуль для настройки [SDDM (Русский)](/index.php/SDDM_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "SDDM (Русский)").

	[https://cgit.kde.org/sddm-kcm.git](https://cgit.kde.org/sddm-kcm.git) || [sddm-kcm](https://www.archlinux.org/packages/?name=sddm-kcm)

*   **kde-gtk-config** — Конфигурация GTK2 и GTK3 для KDE.

	[https://cgit.kde.org/kde-gtk-config.git](https://cgit.kde.org/kde-gtk-config.git) || [kde-gtk-config](https://www.archlinux.org/packages/?name=kde-gtk-config)

*   **System policies** — Набор модулей, который позволяет администраторам изменять настройки [PolicyKit](/index.php/Polkit_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Polkit (Русский)").

	[https://cgit.kde.org/polkit-kde-kcmodules-1.git](https://cgit.kde.org/polkit-kde-kcmodules-1.git) || [kcm-polkit-kde-git](https://aur.archlinux.org/packages/kcm-polkit-kde-git/)

*   **wacom tablet** — Графический интерфейс для Wacom Linux Drivers.

	[https://www.linux-apps.com/p/1127862/](https://www.linux-apps.com/p/1127862/) || [kcm-wacomtablet](https://www.archlinux.org/packages/?name=kcm-wacomtablet)

*   **Kcmsystemd** — Модуль для настройки systemd.

	[https://github.com/rthomsen/kcmsystemd](https://github.com/rthomsen/kcmsystemd) || [systemd-kcm](https://aur.archlinux.org/packages/systemd-kcm/)

Больше модулей KCM можно найти на сайте [linux-apps.com](https://www.linux-apps.com/search?projectSearchText=KCM).

### Локальный поисковик

В KDE Plasma есть [локальный поисковик](https://en.wikipedia.org/wiki/ru:%D0%9B%D0%BE%D0%BA%D0%B0%D0%BB%D1%8C%D0%BD%D1%8B%D0%B9_%D0%BF%D0%BE%D0%B8%D1%81%D0%BA%D0%BE%D0%B2%D0%B8%D0%BA "wikipedia:ru:Локальный поисковик") — [Baloo](/index.php/Baloo "Baloo"), который позволяет индексировать и искать файлы.

### Веб-браузеры

Следующие веб-браузеры могут быть интегрированы в Plasma:

*   **[Konqueror](https://en.wikipedia.org/wiki/ru:Konqueror "wikipedia:ru:Konqueror")** — Часть проекта KDE. Поддерживает два движка — KHTML и Qt WebEngine, основанный на [Chromium (Русский)](/index.php/Chromium_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Chromium (Русский)").

	[https://konqueror.org/](https://konqueror.org/) || [konqueror](https://www.archlinux.org/packages/?name=konqueror)

*   **[Falkon](https://en.wikipedia.org/wiki/ru:Falkon "wikipedia:ru:Falkon")** — Веб-браузер основанный на Qt и включающий в себя возможности интеграции с Plasma. Falkon (ранее известный как Qupzilla) использует движок Qt WebEngine.

	[https://userbase.kde.org/Falkon/](https://userbase.kde.org/Falkon/) || [falkon](https://www.archlinux.org/packages/?name=falkon)

*   **[Chromium](/index.php/Chromium "Chromium")** — Chromium и его проприетарный вариант Google Chrome довольно ограничены в интеграции с Plasma. Они [могут использовать](/index.php/KDE_Wallet#KDE_Wallet_for_Chrome_and_Chromium "KDE Wallet") KWallet и диалоги Plasma для открытия и сохранения файлов.

	[https://www.chromium.org/](https://www.chromium.org/) || [chromium](https://www.archlinux.org/packages/?name=chromium)

*   **[Firefox](/index.php/Firefox "Firefox")** — Firefox можно настроить для большей интеграции с Plasma. Смотрите [Firefox#KDE/GNOME integration](/index.php/Firefox#KDE/GNOME_integration "Firefox") для более подробной информации.

	[https://mozilla.org/firefox](https://mozilla.org/firefox) || [firefox](https://www.archlinux.org/packages/?name=firefox)

**Совет:** Начиная с Plasma 5.13 можно интегрировать [Firefox (Русский)](/index.php/Firefox_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Firefox (Русский)") или [Chrome](/index.php/Chrome "Chrome") с Plasma для получения следующих возможностей: управление воспроизведением медиаконтентом из трея Plasma, уведомление о загрузках и нахождение открытых вкладок через KRunner. [Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") [plasma-browser-integration](https://www.archlinux.org/packages/?name=plasma-browser-integration) и соответствующее дополнение для браузера. Поддержка Chrome/Chromium уже должна быть включена, для Firefox смотрите [Firefox#KDE/GNOME integration](/index.php/Firefox#KDE/GNOME_integration "Firefox").

### PIM

KDE поставляет свой собственный набор приложений для [управления персональной информацией](https://en.wikipedia.org/wiki/Personal_information_management "wikipedia:Personal information management") (электронными письмами, контактами, календарями и так далее). Для их установки используйте мета-пакет [kdepim-meta](https://www.archlinux.org/packages/?name=kdepim-meta).

#### Akonadi

Akonadi представляет собой хранилище локального кеша для PIM-данных, которые, независимо от их происхождения, могут использоваться другими приложениями. Сюда входят: электронная почта, контакты, календари, события, журналы, будильники, заметки и так далее. Формат хранения данных зависит от самих данных (например, контакты могут храниться в формате vCard).

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [akonadi](https://www.archlinux.org/packages/?name=akonadi). Для получения дополнений, установите [kdepim-addons](https://www.archlinux.org/packages/?name=kdepim-addons).

**Примечание:** Если вы не планируете использовать [MariaDB](/index.php/MariaDB "MariaDB") в качестве базы данных, то используйте следующую команду для пропуска зависимостей [mariadb](https://www.archlinux.org/packages/?name=mariadb) при установке пакета [akonadi](https://www.archlinux.org/packages/?name=akonadi):
```
# pacman -S akonadi --assume-installed mariadb

```

Смотрите также [FS#32878](https://bugs.archlinux.org/task/32878).

##### PostgreSQL

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") [postgresql](https://www.archlinux.org/packages/?name=postgresql).

Для использования [PostgreSQL (Русский)](/index.php/PostgreSQL_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "PostgreSQL (Русский)") отредактируйте файл конфигурации Akonadi так, чтобы он содержал следующие параметры:

 `~/.config/akonadi/akonadiserverrc` 
```
[%General]
Driver=QPSQL

[QPSQL]
Host=
InitDbPath=/usr/bin/initdb
Name=akonadi
ServerPath=/usr/bin/pg_ctl
StartServer=true

```

**Примечание:** Значение переменной `Host=` будет задано Akonadi при первом запуске.

Запустите Akonadi с помощью команды `akonadictl start` и проверьте его статус: `akonadictl status`.

##### SQLite

Для использования [SQLite](/index.php/SQLite "SQLite") отредактируйте файл конфигурации Akonadi так, чтобы он содержал следующие параметры:

 `~/.config/akonadi/akonadiserverrc` 
```
[%General]
Driver=QSQLITE3

[QSQLITE3]
Name=/home/*username*/.local/share/akonadi/akonadi.db
```

##### Отключение Akonadi

Смотрите раздел [Disabling the Akonadi subsystem](https://userbase.kde.org/Akonadi#Disabling_the_Akonadi_subsystem) в KDE UserBase.

### KDE Telepathy

[KDE Telepathy](https://community.kde.org/KTp) — проект, направленный на обеспечение лучшей интеграции обмена мгновенными сообщениями с рабочим столом KDE, пришедший на смену Kopete. В качестве бекенда используется фреймворк Telepathy.

Чтобы установить все протоколы Telepathy, [установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") группу пакетов [telepathy](https://www.archlinux.org/groups/x86_64/telepathy/). Клиент Telepathy доступен с пакетом [telepathy-kde-meta](https://www.archlinux.org/packages/?name=telepathy-kde-meta), который также включает в себя все пакеты из группы [telepathy-kde](https://www.archlinux.org/groups/x86_64/telepathy-kde/).

#### Использование Telegram с KDE Telepathy

Протокол [Telegram (Русский)](/index.php/Telegram_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Telegram (Русский)") доступен с пакетом [telepathy-haze](https://www.archlinux.org/packages/?name=telepathy-haze), установкой [telegram-purple](https://aur.archlinux.org/packages/telegram-purple/) или [telegram-purple-git](https://aur.archlinux.org/packages/telegram-purple-git/) и [telepathy-morse-git](https://aur.archlinux.org/packages/telepathy-morse-git/). Имя пользователя — это номер телефона, привязанный к вашему аккаунту Telegram (учитывая национальный код страны `+*xx*`, например, `+49` для Германии).

Настройка с помощью графического интерфейса может быть сложноватой: если при добавлении нового аккаунта в KDE Telepathy номер телефона не принимается (отображается ошибка о недопустимом для создания аккаунта номере), поместите его между одинарных кавычек, после чего, вручную уберите эти кавычки из файла конфигурации (`~/.local/share/telepathy/mission-control/accounts.cfg`) после создания аккаунта (в ином случае, должна появится ошибка авторизации).

**Примечание:** Файл конфигурации должен быть отредактирован вручную когда KDE Telepathy не запущен. Например, это можно сделать в сеансе отличном от KDE Plasma. В ином случае, ваши изменения могут быть перезаписаны программным обеспечением.

### KDE Connect

[KDE Connect](https://community.kde.org/KDEConnect) предлагает ряд функций для подключения [Android](/index.php/Android "Android")-смартфона к вашему устройству с Linux:

*   Пересылайте файлы и ссылки с KDE Plasma в любое приложение (и наоборот).
*   Эмуляция тачпада: используйте экран вашего смартфона как тачпад компьютера.
*   Синхронизация уведомлений (Android 4.3+): получайте уведомления с вашего Android-смартфона в KDE Plasma.
*   Общий буфер обмена: копируйте и вставляйте с KDE Plasma в Android (и наоборот).
*   Удалённое управление медиаконтентом: используйте ваш смартфон для управления медиаплеерами в Linux.
*   Подключение по Wi-Fi: нет нужды в проводах или Bluetooth.
*   Шифрование RSA: ваши данные в безопасности.

Вам нужно будет установить KDE Connect как на компьютере (пакет [kdeconnect](https://www.archlinux.org/packages/?name=kdeconnect)), так и на Android-смартфоне (приложение из [Google Play](https://play.google.com/store/apps/details?id=org.kde.kdeconnect_tp) или [F-Droid](https://f-droid.org/packages/org.kde.kdeconnect_tp/)).

KDE Connect можно использовать и с другими средами рабочего стола. Для тех, которые используют AppIndicators (например, Unity) [установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") также пакет [indicator-kdeconnect](https://aur.archlinux.org/packages/indicator-kdeconnect/). Для пользователей GNOME, лучшей интеграции можно достичь установкой [gnome-shell-extension-gsconnect](https://aur.archlinux.org/packages/gnome-shell-extension-gsconnect/) вместо [kdeconnect](https://www.archlinux.org/packages/?name=kdeconnect).

Если вы используете [межсетевой экран](/index.php/%D0%9C%D0%B5%D0%B6%D1%81%D0%B5%D1%82%D0%B5%D0%B2%D0%BE%D0%B9_%D1%8D%D0%BA%D1%80%D0%B0%D0%BD "Межсетевой экран"), вам потребуется открыть TCP- и UDP-порты от `1714` до `1764`. Смотрите [https://community.kde.org/KDEConnect#Troubleshooting](https://community.kde.org/KDEConnect#Troubleshooting).

## Советы и рекомендации

### Использование альтернативного оконного менеджера

Plasma более не позволяет выбирать альтернативный оконный менеджер в *Параметрах системы*. [[6]](https://github.com/KDE/plasma-desktop/commit/2f83a4434a888cd17b03af1f9925cbb054256ade) Теперь для этого нужно задать значение [переменной окружения](/index.php/Environment_variables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Environment variables (Русский)") `KDEWM` перед запуском Plasma. [[7]](https://wiki.haskell.org/Xmonad/Using_xmonad_in_KDE) Сделать это можно создав скрипт `set_window_manager.sh` в `~/.config/plasma-workspace/env` и экспортируя там переменную `KDEWM`. Например, для использования оконного менеджера [i3 (Русский)](/index.php/I3_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "I3 (Русский)") скрипт будет выглядеть следующим образом:

 `~/.config/plasma-workspace/env/set_window_manager.sh`  `export KDEWM=/usr/bin/i3` 

После чего сделайте скрипт исполняемым:

 `$ chmod +x ~/.config/plasma-workspace/env/set_window_manager.sh` 

#### Сеанс KDE/Openbox

Пакет [openbox](https://www.archlinux.org/packages/?name=openbox) предоставляет сеанс для использования KDE Plasma с [Openbox (Русский)](/index.php/Openbox_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Openbox (Русский)"). Чтобы его использовать, выберите *KDE/Openbox* из меню [экранного менеджера](/index.php/Display_manager_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Display manager (Русский)").

Для запуска сеанса вручную, добавьте следующую строку в ваш файл [xinitrc (Русский)](/index.php/Xinitrc_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xinitrc (Русский)"):

 `~/.xinitrc` 
```
exec openbox-kde-session

```

#### Включение композитных эффектов

После замены Kwin на [оконный менеджер](/index.php/%D0%9E%D0%BA%D0%BE%D0%BD%D0%BD%D1%8B%D0%B9_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80 "Оконный менеджер") без [композитного менеджера](/index.php/Xorg_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Композит "Xorg (Русский)") (например, [Openbox (Русский)](/index.php/Openbox_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Openbox (Русский)")), композитные эффекты рабочего стола (прозрачность и т.п.) пропадут. В таком случае, установите и запустите отдельный композитный менеджер, например, [Xcompmgr (Русский)](/index.php/Xcompmgr_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xcompmgr (Русский)") или [Compton (Русский)](/index.php/Compton_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Compton (Русский)").

### Настройка разрешения экрана / нескольких мониторов

Для настройки разрешения экрана и нескольких мониторов в Plasma [установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [kscreen](https://www.archlinux.org/packages/?name=kscreen), после чего появятся дополнительные опции в приложении *Параметры системы > Экран*.

### Настройка ICC-профилей

Для настройки [|ICC-профилей](/index.php/ICC_profiles_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ICC profiles (Русский)") в Plasma [установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [colord-kde](https://www.archlinux.org/packages/?name=colord-kde), который добавляет дополнительные опции в *Параметры системы > Цветовая коррекция*.

ICC-профили можно импортировать с помощью функции *Добавить профиль*.

### Отключение открытия Меню запуска приложений клавишей Super (Windows)

Для отключения данной функции можно воспользоваться следующей командой:

```
$ kwriteconfig5 --file kwinrc --group ModifierOnlyShortcuts --key Meta ""

```

### Отключение отображения закладок браузера в меню приложений

KDE Plasma отображает закладки браузера в меню запуска приложений, если в системе установлена интеграция браузеров с Plasma (Plasma Browser Integration).

Для отключения этой функции, воспользуйтесь следующими командами:

```
$ mkdir ~/.local/share/kservices5
$ sed 's/EnabledByDefault=true$/EnabledByDefault=false/' /usr/share/kservices5/plasma-runner-bookmarks.desktop > ~/.local/share/kservices5/plasma-runner-bookmarks.desktop

```

## Решение проблем

### Шрифты

#### Шрифты в KDE Plasma выглядят плохо

Первым делом, попробуйте установить шрифты [ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu) и [ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation). После установки перезайдите в систему и не меняйте ничего в приложении *Параметры системы > Шрифты*. Если вы используете [qt5ct](https://www.archlinux.org/packages/?name=qt5ct), настройки Qt5 Configuration Tool могут переопределять настройки шрифтов в *Параметрах системы*.

Если вы вносили изменения в параметры [отображения шрифтов](/index.php/Fonts_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Fonts (Русский)"), имейте в виду, что приложение *Параметры системы* может на них влиять. Когда вы изменяете что-нибудь в приложении *Параметры системы > Шрифты*, скорее всего, файл конфигурации шрифтов (`fonts.conf`) будет перезаписан.

Это невозможно предотвратить, но ожидаемое поведение отображения шрифтов можно вернуть, задав такие же значения, как и в вашем файле `fonts.conf` (также понадобится перезапустить приложения или, в некоторых ситуациях, перезапустить среду рабочего стола). Обратите внимание, что у Font Preferences в среде [GNOME (Русский)](/index.php/GNOME_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GNOME (Русский)") такое же поведение.

#### Огромные или непропорциональные буквы

Попробуйте вручную задать значение DPI равное `**96**` в приложении *Параметры системы > Шрифты*.

Если это не помогло, попробуйте также вручную установить значение DPI в конфигурации сервера Xorg, как указано на странице [Xorg (Русский)#Настройка DPI вручную](/index.php/Xorg_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Настройка_DPI_вручную "Xorg (Русский)").

### Настройки

Множество проблем в KDE Plasma могут возникать из-за ошибок в файлах настроек.

#### Странное поведение рабочего стола Plasma

Проблемы в KDE Plasma обычно вызваны нестабильными *виджетами* (*плазмоидами*) или *темами Plasma*. Первым делом, найдите, какие последние плазмоиды и темы вы устанавливали и попробуйте их отключить или удалить.

Если вы наблюдаете проблемы с зависанием/закрытием Plasma, скорее всего, они вызваны ошибкой в одном из установленных виджетов. В случае если вы не помните, какие из них были установлены до появления проблемы (она может быть непостоянной), попробуйте исключать по одному до исчезновения проблемы. После этого можно удалить данный виджет и создать отчёт об ошибке на [баг-трекере KDE](https://bugs.kde.org/) **если это официальный виджет**. В ином случае, рекомендуется найти виджет на [KDE Store](https://store.kde.org/) и уведомить его автора о проблеме (указывая детали, например, как повторить ошибку).

Если вы не можете найти источник проблемы и не хотите сбрасывать *все* настройки, перейдите в каталог `~/.config` и введите следующую команду:

```
$ for j in plasma*; do mv -- "$j" "${j%}.bak"; done

```

Данная команда переименует **все** файлы конфигурации Plasma вашего пользователя в **.bak* (например, `plasmarc.bak`) и когда вы перезайдёте в Plasma, вы снова получите настройки по умолчанию. Для возвращения предыдущего состояния файлов конфигурации достаточно будет убрать расширение *.bak*. Если у вас уже есть файлы **.bak*, сначала переименуйте, переместите или удалите их. Также крайне рекомендуется регулярно создавать бекапы, смотрите статью [Synchronization and backup programs (Русский)](/index.php/Synchronization_and_backup_programs_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Synchronization and backup programs (Русский)") для получения информации о возможных решениях.

#### Очистка кэша для решения проблем с обновлением

Также [проблемы](https://bbs.archlinux.org/viewtopic.php?id=135301) могут быть вызваны старыми данными в кэше. Иногда, после обновления, они могут вызывать странное, мало предсказуемое и трудное в отладке поведение рабочего стола или программ KDE. Например, незакрываемые командные оболочки, зависания во время изменения различных настроек, невозможность Ark извлечь архив или невозможность Amarok распознать вашу коллекцию музыки. Также это может помочь решить проблему с плохим внешним видом программ KDE или Qt после обновления.

Перестроить кэш можно следующей командой:

```
$ rm ~/.config/Trolltech.conf
$ kbuildsycoca5 --noincremental

```

Дополнительно, удалите содержание директории `~/.cache`. Обратите внимание, что это также очистит и кэш других программ:

```
$ rm -rf ~/.cache/*

```

### Графика

Убедитесь, что в системе установлен подходящий драйвер для вашей видеокарты. Смотрите статью [Xorg (Русский)#Установка драйвера](/index.php/Xorg_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Установка_драйвера "Xorg (Русский)") для получения более подробной информации. В случае с более старой видеокартой может помочь [#Отключение эффектов рабочего стола вручную или автоматически для определённых приложений](#Отключение_эффектов_рабочего_стола_вручную_или_автоматически_для_определённых_приложений) или [#Отключение композитного режима](#Отключение_композитного_режима).

#### Получение текущего состояния KWin для поддержки и отладки

Следующая команда выведет полную сводку о текущем состоянии KWin включая использующиеся настройки, данные о композитном бекенде и возможностях драйвера OpenGL. Более подробная информация доступна в [данном блоге](https://blog.martin-graesslin.com/blog/2012/03/on-getting-help-for-kwin-and-helping-kwin/).

```
$ qdbus org.kde.KWin /KWin supportInformation

```

#### Отключение эффектов рабочего стола вручную или автоматически для определённых приложений

Эффекты рабочего стола Plasma активированы по умолчанию и, к примеру, не каждая игра автоматически их отключает. Вы можете выключить эффекты рабочего стола вручную в приложении *Параметры системы > Поведение рабочей среды > Эффекты* и включать/выключать их с помощью сочетания клавиш `Alt+Shift+F12`.

Также можно создать собственные правила KWin для автоматического включения/выключения композитного режима при запуске определённых программ в приложении *Параметры системы > Диспетчер окон > Особые параметры окон*.

#### Включение прозрачности

Вы увидите следующее сообщение при использовании прозрачного фона без включения композитора:

```
This color scheme uses a transparent background which does not appear to be supported on your desktop

```

Перейдите в *Параметры системы > Экран > Обеспечение эффектов*, отметьте флажок *Включать графические эффекты при входе в систему* и перезапустите Plasma.

#### Отключение композитного режима

В приложении *Параметры системы > Экран > Обеспечение эффектов* снимите флажок с опции *Включать графические эффекты при входе в систему* и перезапустите Plasma.

#### Мерцание окон в полноэкранном режиме при включённом композитном режиме

В приложении *Параметры системы > Экран > Обеспечение эффектов* снимите флажок с опции *Разрешать приложениям блокировать режим с графическими эффектами*. Это может повлиять на производительность.

#### Разрыв изображения с NVIDIA

Смотрите [NVIDIA/Troubleshooting#Avoid screen tearing in KDE (KWin)](/index.php/NVIDIA/Troubleshooting#Avoid_screen_tearing_in_KDE_(KWin) "NVIDIA/Troubleshooting").

#### Курсор иногда отображается неправильно

Создайте директорию `~/.icons/default` и файл `index.theme` внутри неё со следующим содержанием:

 `/home/*username*/.icons/default/index.theme` 
```
[Icon Theme]
Inherits=breeze_cursors
```

Также выполните данную команду:

```
$ ln -s /usr/share/icons/breeze_cursors/cursors ~/.icons/default/cursors

```

#### Непригодное для использования множество разрешений экрана

Ваши локальные настройки kscreen могут переопределять параметры `xorg.conf`. Просмотрите конфигурационные файлы kscreen в директории `~/.local/share/kscreen/` и проверьте, не задано ли режиму (mode) неподдерживаемое вашим дисплеем разрешение.

#### Размытые иконки в системном трее

Приложения часто используют библиотеку appindicator для добавления иконок в трей. Если они отображаются размытыми, проверьте установленную версию библиотеки в системе. В случае, если установлен только пакет [libappindicator-gtk2](https://www.archlinux.org/packages/?name=libappindicator-gtk2), попробуйте также установить [libappindicator-gtk3](https://www.archlinux.org/packages/?name=libappindicator-gtk3) или [libappindicator-sharp](https://www.archlinux.org/packages/?name=libappindicator-sharp).

### Звук

**Примечание:** Первым делом убедитесь, что у вас установлен пакет [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils).

#### Отсутствие звука после выхода из ждущего режима

В случае если в Plasma отсутствует звук после выхода из ждущего режима и KMix не отображает нужных аудиоустройств, может помочь перезапуск plasmashell и pulseaudio:

```
$ killall plasmashell
$ systemctl --user restart pulseaudio.service
$ plasmashell

```

Другим приложениям тоже может понадобиться перезапуск для возобновления возможности воспроизводить звук.

#### MP3-файлы не воспроизводятся с бекендом GStreamer в Phonon

Эту проблему можно решить установкой плагина libav (пакет [gst-libav](https://www.archlinux.org/packages/?name=gst-libav)) для GStreamer. Если вы все еще испытываете проблемы, вы можете попробовать другой бекенд для Phonon, например, [phonon-qt4-vlc](https://aur.archlinux.org/packages/phonon-qt4-vlc/) или [phonon-qt5-vlc](https://www.archlinux.org/packages/?name=phonon-qt5-vlc).

Также убедитесь, что выбранный вами бекенд имеет самый высокий приоритет в приложении *Параметры системы > Мультимедиа > Звук и видео > Библиотеки воспроизведения*.

### Управление электропитанием

#### Отсутствие ждущего/спящего режима

Если система может переходить в спящий или ждущий режим используя [systemd (Русский)](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd (Русский)"), но данная опция не отображается в KDE Plasma, убедитесь, что установлен пакет [powerdevil](https://www.archlinux.org/packages/?name=powerdevil).

### KMail

#### Сброс настроек Akonadi для решения проблем с KMail

Первым делом убедитесь, что KMail не запущен. После чего сохраните настройки Akonadi:

```
$ cp -a ~/.local/share/akonadi ~/.local/share/akonadi-old
$ cp -a ~/.config/akonadi ~/.config/akonadi-old

```

Откройте *System Settings > Personal* и удалите все ресурсы. Вернитесь в Dolphin и удалите исходные `~/.local/share/akonadi/` и `~/.config/akonadi/` - копии которых вы сделали ранее, чтобы иметь возможность их восстановить.

Снова вернитесь в *System Settings* и внимательно добавьте все необходимые ресурсы. Вы должны увидеть считывание ресурсов в папках с письмами. Сохраните настройки и запустите Kontact/KMail чтобы убедиться, что теперь все работает корректно.

#### Пустая папка входящих сообщений в IMAP-аккаунте KMail

Для некоторых аккаунтов KMail использующих протокол IMAP, папка входящих сообщений может отображаться в виде контейнера верхнего уровня (таким образом, делая прочтение сообщений невозможным) со всеми остальными директориями в нём.[[8]](https://bugs.kde.org/show_bug.cgi?id=284172). Для решений этой проблемы достаточно отключить подписки на стороне сервера (server-side subscriptions) в настройках аккаунта в KMail.

#### Ошибка авторизации EWS-аккаунта в KMail

При добавлении EWS-аккаунта в KMail могут возникнуть ошибки авторизации даже с корректными и работающими данными. Вероятнее всего, это вызвано нарушением связи [KWallet](/index.php/KWallet "KWallet") и KMail. Для решения проблемы задайте пароль с помощью qdbus:

```
$ qdbus org.freedesktop.Akonadi.Resource.akonadi_ews_resource_0 /Settings org.kde.Akonadi.Ews.Wallet.setPassword "XXX"

```

### Сеть

#### Зависания при использовании автоматического монтирования NFS-раздела

Использование [автоматического монтирования с systemd](/index.php/Fstab_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Автоматическое_монтирование_с_systemd "Fstab (Русский)") раздела с файловой системой [NFS (Русский)](/index.php/NFS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "NFS (Русский)") может приводить к зависаниям, для более подробной информации смотрите [отчёт об ошибке](https://bugs.kde.org/show_bug.cgi?id=354137) на баг-трекере KDE.

### Слишком частое журналирование событий QXcbConnection

Смотрите [Qt#Disable/Change Qt journal logging behaviour](/index.php/Qt#Disable/Change_Qt_journal_logging_behaviour "Qt").

### Приложения на KF5/Qt 5 не отображают значки в i3/FVWM/awesome

Смотрите [Qt#Configuration of Qt5 apps under environments other than KDE Plasma](/index.php/Qt#Configuration_of_Qt5_apps_under_environments_other_than_KDE_Plasma "Qt").

### Проблемы с сохранением учётных данных и постоянно появляющимися диалогами KWallet

[KWallet](/index.php/KWallet "KWallet"), систему сохранения паролей, не рекомендуется отключать в настройках пользователя, так как для каждого из них сохраняются некоторые зашифрованные данные, например, пароли от сетей WiFi. Однако постоянно появляющиеся диалоги KWallet могут стать причиной его отключения.

В случае если вас раздражают диалоги разблокировки KWallet когда приложения хотят получить к нему доступ, можно разрешить [экранным менеджерам](/index.php/Display_manager_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Display manager (Русский)") [SDDM (Русский)](/index.php/SDDM_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "SDDM (Русский)") и [LightDM (Русский)](/index.php/LightDM_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "LightDM (Русский)") автоматически разблокировать бумажник при входе в систему – cмотрите [KDE Wallet#Unlock KDE Wallet automatically on login](/index.php/KDE_Wallet#Unlock_KDE_Wallet_automatically_on_login "KDE Wallet"). Первый бумажник должен быть сгенерирован непосредственно KWallet (а не пользователем), чтобы использовать его при входе в систему.

В случае если вы не хотите открывать в памяти учётные данные бумажника для каждого приложения, можно ограничить доступ некоторых программ к нему с помощью [kwalletmanager](https://www.archlinux.org/packages/?name=kwalletmanager) в настройках KWallet.

Если же вы совсем не беспокоитесь насчёт шифрования учётных данных, можно просто оставить поля для ввода пароля пустыми во время создания бумажника в KWallet. В таком случае приложения смогут получать доступ к бумажнику без его предварительной разблокировки.

### Discover не отображает никакие приложения

Проблему можно решить установкой пакета [packagekit-qt5](https://www.archlinux.org/packages/?name=packagekit-qt5).

### Высокая нагрузка kscreenlocker_greet на ЦП при использовании драйверов NVIDIA

Как описано в [KDE Bug 347772](https://bugs.kde.org/show_bug.cgi?id=347772), драйвера NVIDIA OpenGL и QML могут не очень хорошо взаимодействовать друг с другом в Qt 5\. Это может привести к тому, что `kscreenlocker_greet` будет использовать довольно много ресурсов ЦП после разблокировки сессии. Для исправления данной проблемы задайте [переменной окружения](/index.php/Environment_variables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Environment variables (Русский)") `QSG_RENDERER_LOOP` значение `basic`.

После чего закройте предыдущий процесс экрана приветствия с помощью команды `killall kscreenlocker_greet`.

### "OS error 22" при выполнении Akonadi на ZFS

Если ваша домашняя директория находится в пуле [ZFS (Русский)](/index.php/ZFS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ZFS (Русский)"), создайте файл `~/.config/akonadi/mysql-local.conf` со следующим содержанием:

```
[mysqld]
innodb_use_native_aio = 0

```

Смотрите также [MariaDB#OS error 22 when running on ZFS](/index.php/MariaDB#OS_error_22_when_running_on_ZFS "MariaDB").

### Не работает прокрутка неактивных окон в некоторых программах

Проблема вызвана тем, что GTK3 проблематично обрабатывает события прокрутки мышью. Временным решением является задание [переменной окружения](/index.php/Environment_variables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Environment variables (Русский)") `GDK_CORE_DEVICE_EVENTS=1`. Однако такое решение также не позволяет использовать плавную прокрутку на тачпаде и прокрутку на сенсорном дисплее.

## Смотрите также

*   [Домашняя страница KDE](https://www.kde.org/)
*   [Баг-трекер KDE](https://bugs.kde.org/)
*   [Блог Мартина Греслина](https://blog.martin-graesslin.com/blog/kategorien/kde/)