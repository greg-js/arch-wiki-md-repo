## Contents

*   [1 Уловки конфигурации](#.D0.A3.D0.BB.D0.BE.D0.B2.D0.BA.D0.B8_.D0.BA.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D0.B8)
    *   [1.1 Добавление/Редактирование GDM сессий](#.D0.94.D0.BE.D0.B1.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5.2F.D0.A0.D0.B5.D0.B4.D0.B0.D0.BA.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_GDM_.D1.81.D0.B5.D1.81.D1.81.D0.B8.D0.B9)
    *   [1.2 Внешний вид GDM](#.D0.92.D0.BD.D0.B5.D1.88.D0.BD.D0.B8.D0.B9_.D0.B2.D0.B8.D0.B4_GDM)
    *   [1.3 Доводка](#.D0.94.D0.BE.D0.B2.D0.BE.D0.B4.D0.BA.D0.B0)
    *   [1.4 Низкая производительность](#.D0.9D.D0.B8.D0.B7.D0.BA.D0.B0.D1.8F_.D0.BF.D1.80.D0.BE.D0.B8.D0.B7.D0.B2.D0.BE.D0.B4.D0.B8.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D0.BE.D1.81.D1.82.D1.8C)
    *   [1.5 Приложения по умолчанию](#.D0.9F.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F_.D0.BF.D0.BE_.D1.83.D0.BC.D0.BE.D0.BB.D1.87.D0.B0.D0.BD.D0.B8.D1.8E)
    *   [1.6 Улучшение производительности видео](#.D0.A3.D0.BB.D1.83.D1.87.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B8.D0.B7.D0.B2.D0.BE.D0.B4.D0.B8.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D0.BE.D1.81.D1.82.D0.B8_.D0.B2.D0.B8.D0.B4.D0.B5.D0.BE)
    *   [1.7 Шрифты кажутся перекошенным](#.D0.A8.D1.80.D0.B8.D1.84.D1.82.D1.8B_.D0.BA.D0.B0.D0.B6.D1.83.D1.82.D1.81.D1.8F_.D0.BF.D0.B5.D1.80.D0.B5.D0.BA.D0.BE.D1.88.D0.B5.D0.BD.D0.BD.D1.8B.D0.BC)
    *   [1.8 Изменение фона рабочего стола по умолчанию](#.D0.98.D0.B7.D0.BC.D0.B5.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D1.84.D0.BE.D0.BD.D0.B0_.D1.80.D0.B0.D0.B1.D0.BE.D1.87.D0.B5.D0.B3.D0.BE_.D1.81.D1.82.D0.BE.D0.BB.D0.B0_.D0.BF.D0.BE_.D1.83.D0.BC.D0.BE.D0.BB.D1.87.D0.B0.D0.BD.D0.B8.D1.8E)
    *   [1.9 Увеличении размера окна терминала](#.D0.A3.D0.B2.D0.B5.D0.BB.D0.B8.D1.87.D0.B5.D0.BD.D0.B8.D0.B8_.D1.80.D0.B0.D0.B7.D0.BC.D0.B5.D1.80.D0.B0_.D0.BE.D0.BA.D0.BD.D0.B0_.D1.82.D0.B5.D1.80.D0.BC.D0.B8.D0.BD.D0.B0.D0.BB.D0.B0)
*   [2 Различные уловки](#.D0.A0.D0.B0.D0.B7.D0.BB.D0.B8.D1.87.D0.BD.D1.8B.D0.B5_.D1.83.D0.BB.D0.BE.D0.B2.D0.BA.D0.B8)
    *   [2.1 Блокировка экрана](#.D0.91.D0.BB.D0.BE.D0.BA.D0.B8.D1.80.D0.BE.D0.B2.D0.BA.D0.B0_.D1.8D.D0.BA.D1.80.D0.B0.D0.BD.D0.B0)
    *   [2.2 Разблокировка GNOME-keyring при входе в систему](#.D0.A0.D0.B0.D0.B7.D0.B1.D0.BB.D0.BE.D0.BA.D0.B8.D1.80.D0.BE.D0.B2.D0.BA.D0.B0_GNOME-keyring_.D0.BF.D1.80.D0.B8_.D0.B2.D1.85.D0.BE.D0.B4.D0.B5_.D0.B2_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.83)
    *   [2.3 Nautilus уловки](#Nautilus_.D1.83.D0.BB.D0.BE.D0.B2.D0.BA.D0.B8)
        *   [2.3.1 Изменение режима файлового менеджера (Вид обозревателя)](#.D0.98.D0.B7.D0.BC.D0.B5.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D1.80.D0.B5.D0.B6.D0.B8.D0.BC.D0.B0_.D1.84.D0.B0.D0.B9.D0.BB.D0.BE.D0.B2.D0.BE.D0.B3.D0.BE_.D0.BC.D0.B5.D0.BD.D0.B5.D0.B4.D0.B6.D0.B5.D1.80.D0.B0_.28.D0.92.D0.B8.D0.B4_.D0.BE.D0.B1.D0.BE.D0.B7.D1.80.D0.B5.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D1.8F.29)
        *   [2.3.2 Музыкальные информационные колонки в окне файлового менеджера (битрейт и т.д.)](#.D0.9C.D1.83.D0.B7.D1.8B.D0.BA.D0.B0.D0.BB.D1.8C.D0.BD.D1.8B.D0.B5_.D0.B8.D0.BD.D1.84.D0.BE.D1.80.D0.BC.D0.B0.D1.86.D0.B8.D0.BE.D0.BD.D0.BD.D1.8B.D0.B5_.D0.BA.D0.BE.D0.BB.D0.BE.D0.BD.D0.BA.D0.B8_.D0.B2_.D0.BE.D0.BA.D0.BD.D0.B5_.D1.84.D0.B0.D0.B9.D0.BB.D0.BE.D0.B2.D0.BE.D0.B3.D0.BE_.D0.BC.D0.B5.D0.BD.D0.B5.D0.B4.D0.B6.D0.B5.D1.80.D0.B0_.28.D0.B1.D0.B8.D1.82.D1.80.D0.B5.D0.B9.D1.82_.D0.B8_.D1.82..D0.B4..29)
    *   [2.4 Увеличение скорости авто-скрытия панели](#.D0.A3.D0.B2.D0.B5.D0.BB.D0.B8.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D1.81.D0.BA.D0.BE.D1.80.D0.BE.D1.81.D1.82.D0.B8_.D0.B0.D0.B2.D1.82.D0.BE-.D1.81.D0.BA.D1.80.D1.8B.D1.82.D0.B8.D1.8F_.D0.BF.D0.B0.D0.BD.D0.B5.D0.BB.D0.B8)
    *   [2.5 Уловки меню GNOME](#.D0.A3.D0.BB.D0.BE.D0.B2.D0.BA.D0.B8_.D0.BC.D0.B5.D0.BD.D1.8E_GNOME)
        *   [2.5.1 Доводка скорости](#.D0.94.D0.BE.D0.B2.D0.BE.D0.B4.D0.BA.D0.B0_.D1.81.D0.BA.D0.BE.D1.80.D0.BE.D1.81.D1.82.D0.B8)
        *   [2.5.2 Редактирование меню](#.D0.A0.D0.B5.D0.B4.D0.B0.D0.BA.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BC.D0.B5.D0.BD.D1.8E)
            *   [2.5.2.1 Пользовательское меню](#.D0.9F.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D1.8C.D1.81.D0.BA.D0.BE.D0.B5_.D0.BC.D0.B5.D0.BD.D1.8E)
            *   [2.5.2.2 Группы меню, системное меню](#.D0.93.D1.80.D1.83.D0.BF.D0.BF.D1.8B_.D0.BC.D0.B5.D0.BD.D1.8E.2C_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D0.BD.D0.BE.D0.B5_.D0.BC.D0.B5.D0.BD.D1.8E)
        *   [2.5.3 Изменение логотипа Gnome на Arch](#.D0.98.D0.B7.D0.BC.D0.B5.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BB.D0.BE.D0.B3.D0.BE.D1.82.D0.B8.D0.BF.D0.B0_Gnome_.D0.BD.D0.B0_Arch)
        *   [2.5.4 Другой способ изменить логотип](#.D0.94.D1.80.D1.83.D0.B3.D0.BE.D0.B9_.D1.81.D0.BF.D0.BE.D1.81.D0.BE.D0.B1_.D0.B8.D0.B7.D0.BC.D0.B5.D0.BD.D0.B8.D1.82.D1.8C_.D0.BB.D0.BE.D0.B3.D0.BE.D1.82.D0.B8.D0.BF)
        *   [2.5.5 Удаление стандартных иконок с рабочего стола](#.D0.A3.D0.B4.D0.B0.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D1.81.D1.82.D0.B0.D0.BD.D0.B4.D0.B0.D1.80.D1.82.D0.BD.D1.8B.D1.85_.D0.B8.D0.BA.D0.BE.D0.BD.D0.BE.D0.BA_.D1.81_.D1.80.D0.B0.D0.B1.D0.BE.D1.87.D0.B5.D0.B3.D0.BE_.D1.81.D1.82.D0.BE.D0.BB.D0.B0)
        *   [2.5.6 Автоматическая смена обоев рабочего стола](#.D0.90.D0.B2.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B0.D1.8F_.D1.81.D0.BC.D0.B5.D0.BD.D0.B0_.D0.BE.D0.B1.D0.BE.D0.B5.D0.B2_.D1.80.D0.B0.D0.B1.D0.BE.D1.87.D0.B5.D0.B3.D0.BE_.D1.81.D1.82.D0.BE.D0.BB.D0.B0)
    *   [2.6 Отключение прокрутки в панели задач](#.D0.9E.D1.82.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.BA.D1.80.D1.83.D1.82.D0.BA.D0.B8_.D0.B2_.D0.BF.D0.B0.D0.BD.D0.B5.D0.BB.D0.B8_.D0.B7.D0.B0.D0.B4.D0.B0.D1.87)
*   [3 Полезные дополнения](#.D0.9F.D0.BE.D0.BB.D0.B5.D0.B7.D0.BD.D1.8B.D0.B5_.D0.B4.D0.BE.D0.BF.D0.BE.D0.BB.D0.BD.D0.B5.D0.BD.D0.B8.D1.8F)
    *   [3.1 FAM](#FAM)
    *   [3.2 Системный монитор Gnome](#.D0.A1.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D0.BD.D1.8B.D0.B9_.D0.BC.D0.BE.D0.BD.D0.B8.D1.82.D0.BE.D1.80_Gnome)
    *   [3.3 Запись дисков CDs из файлового менеджера](#.D0.97.D0.B0.D0.BF.D0.B8.D1.81.D1.8C_.D0.B4.D0.B8.D1.81.D0.BA.D0.BE.D0.B2_CDs_.D0.B8.D0.B7_.D1.84.D0.B0.D0.B9.D0.BB.D0.BE.D0.B2.D0.BE.D0.B3.D0.BE_.D0.BC.D0.B5.D0.BD.D0.B5.D0.B4.D0.B6.D0.B5.D1.80.D0.B0)
    *   [3.4 Сервисные приложения GNOME](#.D0.A1.D0.B5.D1.80.D0.B2.D0.B8.D1.81.D0.BD.D1.8B.D0.B5_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F_GNOME)
    *   [3.5 Gdesklets: плюшки на рабочем столе](#Gdesklets:_.D0.BF.D0.BB.D1.8E.D1.88.D0.BA.D0.B8_.D0.BD.D0.B0_.D1.80.D0.B0.D0.B1.D0.BE.D1.87.D0.B5.D0.BC_.D1.81.D1.82.D0.BE.D0.BB.D0.B5)
*   [4 Другие приложения](#.D0.94.D1.80.D1.83.D0.B3.D0.B8.D0.B5_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F)
    *   [4.1 gnome-terminal](#gnome-terminal)
        *   [4.1.1 Выпадающие консоли](#.D0.92.D1.8B.D0.BF.D0.B0.D0.B4.D0.B0.D1.8E.D1.89.D0.B8.D0.B5_.D0.BA.D0.BE.D0.BD.D1.81.D0.BE.D0.BB.D0.B8)
            *   [4.1.1.1 Guake](#Guake)
            *   [4.1.1.2 Tilda](#Tilda)
    *   [4.2 gedit](#gedit)
    *   [4.3 eog](#eog)
    *   [4.4 file-roller](#file-roller)
    *   [4.5 gcalctool](#gcalctool)
    *   [4.6 rhythmbox](#rhythmbox)
    *   [4.7 sound-juicer](#sound-juicer)
    *   [4.8 totem](#totem)
    *   [4.9 gimp](#gimp)
    *   [4.10 gftp](#gftp)
    *   [4.11 abiword](#abiword)
    *   [4.12 gnumeric](#gnumeric)
    *   [4.13 Возможность оставлять сообщения в хранителе экрана](#.D0.92.D0.BE.D0.B7.D0.BC.D0.BE.D0.B6.D0.BD.D0.BE.D1.81.D1.82.D1.8C_.D0.BE.D1.81.D1.82.D0.B0.D0.B2.D0.BB.D1.8F.D1.82.D1.8C_.D1.81.D0.BE.D0.BE.D0.B1.D1.89.D0.B5.D0.BD.D0.B8.D1.8F_.D0.B2_.D1.85.D1.80.D0.B0.D0.BD.D0.B8.D1.82.D0.B5.D0.BB.D0.B5_.D1.8D.D0.BA.D1.80.D0.B0.D0.BD.D0.B0)
    *   [4.14 DevilsPie](#DevilsPie)
*   [5 См. также](#.D0.A1.D0.BC._.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Уловки конфигурации

### Добавление/Редактирование GDM сессий

Для добавления или редактирования сессий [GDM](/index.php/GDM "GDM") используется конфигурационный файл `gdm.conf`, который располагается в `/opt/gnome/etc/gdm/` или `/etc/gdm` директориях. По умолчанию конфигурационный файл указывает, что в директории `/etc/X11/sessions` находятся файлы сессий оконных менеджеров. Файлы сессий используются в формате `.desktop`.

**Для добавления новой сессии:**

1\. Скопируйте существующий файл `.desktop` для использования в качестве шаблона:

```
# cd /etc/X11/sessions
$ cp enlightenment.desktop waimea.desktop

```

2\. Измените файл шаблона `.desktop` в соответствии с тем менеджером окон, который хотите использовать:

```
# nano waimea.desktop

```

В качестве альтернативы вы можете открыть новую сессию в [KDM](/index.php/KDM_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "KDM (Русский)"). Это создаст файл *.desktop*. Затем, когда вернетесь к использованию GDM, новая сессия будет доступна.

### Внешний вид GDM

Вы можете изменить фоновое изображение, тему [GTK+ (Русский)](/index.php/GTK%2B_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GTK+ (Русский)") и иконок вручную или можете воспользоваться утилитой [gdm2setup](https://aur.archlinux.org/packages/gdm2setup/).

### Доводка

Если приложения gnome кажутся медленными или он подвисает во время загрузки, после вылета предыдущей сессии, то скорее всего неправильно настроен файл `/etc/hosts` и содержит:

```
127.0.0.1       localhost.localdomain     localhost      ВАШЕ_ИМЯ_УЗЛА

```

Затем запустите `/bin/hostname ВАШЕ_ИМЯ_УЗЛА` и `/sbin/ifconfig lo up` от имени суперпользователя.

Смотрите также статью [Настройка сети](/index.php/%D0%9D%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0_%D1%81%D0%B5%D1%82%D0%B8 "Настройка сети").

### Низкая производительность

В результате того, что отрисовывающая библиотека GNOME сделана не должным образом, некоторые действия в среде GNOME могут привести к замедлению системы. Если иконки темы хранятся в формате SVG, то это может замедлить систему. Лучше использовать иконки в формате PNG или преобразовать имеющиеся в формат PNG.

### Приложения по умолчанию

Возможно вы хотите настроить приложения по умолчанию и ассоциации расширений файлов для всей системы. Это особенно необходимо, когда у вас установлены некоторые KDE приложения, но вы хотите чтобы по умолчанию использовались приложения GNOME.

Чтобы сделать это, вы можете установить [gnome-defaults-list](https://aur.archlinux.org/packages/gnome-defaults-list/) из AUR. Это заменит ваш файл настройки в `/etc/gnome/defaults.list`.

Если хотите произвести изменения вручную, то создайте файл `/usr/share/applications/defaults.list` с соответствующим форматом:

```
[Default Applications]
application/pdf=evince.desktop
image/jpeg=eog.desktop
...

```

### Улучшение производительности видео

Некоторые пользователи замечали, что если они двигают окно проигрывателя, пока воспроизводится видео файл, появляется синяя рамка вокруг видео. Если у вас похожая ситуация, зайдите в терминал и запустите команду gstreamer-properties. В появившемся окне в "Видео->Выход по умолчанию" измените на "Система X Window(без расширения Xv)". После того, как кликните на кнопку "Проверить", синяя рамка должна исчезнуть и видео должно лучше воспроизводиться.

**Примечание:** Это больше не появляется с версией Gnome 2.20 и выше ([Evanlec](/index.php/User:Evanlec "User:Evanlec"))

### Шрифты кажутся перекошенным

Вы можете изменять [DPI](http://ru.wikipedia.org/wiki/Dpi) ваших шрифтов в GNOME c помощью [ПКМ](http://ru.wikipedia.org/wiki/%D0%9F%D0%9A%D0%9C) щелкните на Рабочем столе->Изменить фон рабочего стола->Шрифты->Подробнее...->Разрешение

```
Разрешение: [96] точек на дюм

```

На моей x86_64 система по некоторой причине, по умолчанию установлено 89 точек на дюм. Я увеличел их до 96 и все стало выглядеть опять "нормально".

### Изменение фона рабочего стола по умолчанию

По умолчанию на фоне рабочего стола размещен увеличенный зеленый листочек. Это также появляется для ново созданных пользователей, но что более важно, это изображение появляется когда экран заблокирован. С 25-Апреля-2009, вы можете найти файл этого изображения здесь

```
/usr/share/pixmaps/backgrounds/gnome/background-default.jpg

```

Чтобы изменить его, достаточно под суперпользователем скопировать понравившееся изображение на место background-default.jpg.

### Увеличении размера окна терминала

После того, как вы добавили кнопку запуска для вашего gnome-terminal, вы можете захотеть изменить размер больше стандартного. ПКМ щелкните на кнопке запуска->свойства, в поле "Команда", добавьте следующее:

```
Команда: gnome-terminal --geometry 105x25+100+20

```

## Различные уловки

### Блокировка экрана

1.  Убедитесь, что dbus запущен(возможно его стоить добавить в список демонов в `/etc/rc.conf`)
2.  Установите xscreensaver: [xscreensaver](https://www.archlinux.org/packages/?name=xscreensaver)
3.  Зайдите в Систему -> Параметры -> Хранитель экрана
4.  Выберете один или более скринсейверов
5.  Теперь блокировка экрана запустит ваш скринсейвер и потребует ввода пароля для выхода из блокировки.

**или** вы можете установить [gnome-screensaver](https://www.archlinux.org/packages/?name=gnome-screensaver):

Также вы можете посмотреть как заменить gnome-screensaver на xscreensaver [тут](http://ubuntuforums.org/showthread.php?t=195557)

### Разблокировка GNOME-keyring при входе в систему

В `/etc/pam.d/gdm`, добавьте похожие строчки в конец файла:

```
auth            optional        pam_gnome_keyring.so
session         optional        pam_gnome_keyring.so  auto_start

```

В `/etc/pam.d/gnome-screensaver`, добавьте:

```
auth        optional     pam_gnome_keyring.so

```

В `/etc/pam.d/passwd`, добавьте:

```
password        optional        pam_gnome_keyring.so

```

[http://live.gnome.org/GnomeKeyring/Pam](http://live.gnome.org/GnomeKeyring/Pam)

**Способ проще:** Установите SEAHORSE с помощью [seahorse](https://www.archlinux.org/packages/?name=seahorse). Теперь у вас появиться в "Приложения -> Стандартные -> Пароли и ключи шифрования" неплохое графическое приложение, где вы можете установить нужные вам опции.

### Nautilus уловки

Если хотите окно ввода адреса пути, просто нажмите:

```
Control + L

```

#### Изменение режима файлового менеджера (Вид обозревателя)

1.  Запустите gconf-editor
2.  Перейдите в apps/nautilus/preferences
3.  Измените занчаение "always_use_browser" на "true"

Или через свойства файлового менеждера:

1.  В окне Nautilus зайдите в Правка -> Настройки
2.  Перейдите на вкладку Поведения
3.  Отметьте (или снимите отметку) "Всегда открывать в окне обозревателя"

#### Музыкальные информационные колонки в окне файлового менеджера (битрейт и т.д.)

В файловом менеджере отсутствует возможность отображать метаданные музыкальных файлов, поэтому был написан скрипт на python, который позволяет добавить колонки в режиме списка:

*   Artist
*   Album
*   Track Title
*   Bit Rate

С начало, установите зависимости: [mutagen](https://www.archlinux.org/packages/?name=mutagen)

Затем, из [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)"), [python-nautilus](https://aur.archlinux.org/packages/python-nautilus/)

Теперь, создайте директорию под названием *python-extensions* в `~/.nautilus`. Положите следующий скрипт, с названием `bsc.py`, в только что созданную папку. Вы можете скачать скрипт тут: [[bsc.py](http://stefanwilkens.eu/bsc.py)] (пожалуйста, бросьте пару строк --[stefanwilkens](/index.php/User:Stefanwilkens "User:Stefanwilkens") если файл будет не доступен)

Перезапустите файловый менеджер, теперь вы сможете настроить отображение метаданных в Правка -> Параметры -> List Columns

### Увеличение скорости авто-скрытия панели

Если вам кажется, что при использовании функции авто-скрытия панели, панель слишком долго появляется или исчезает, попробуйте данное решение:

1.  Запустите gconf-editor
2.  Перейдите в /apps/panel/global
3.  Установите panel_hide_delay и panel_show_delay в более уместные значения(integer). Эти значения представляют собой миллисекунды.

### Уловки меню GNOME

#### Доводка скорости

Вы можете убрать задержку в меню GNOME, запустив данную комманду:

```
echo "gtk-menu-popup-delay = 0" >> ~/.gtkrc-2.0

```

Или просто добавьте "`gtk-menu-popup-delay = 0`" в .gtkrc-2.0

Тем не менее, по некоторым сообщениям, данные настройки могут привести к аварийному завершению banshee и других приложений.

#### Редактирование меню

Большинство пользователей Gnome жалуются по поводу меню. Т.к. изменение записей меню в масштабе всей системы или одного и более пользователей слабо документировано.

##### Пользовательское меню

В недавних версиях Gnome (например, v2.22) имеется редактор меню, в котором вы можете отметить отображение записей меню, но нет возможности добавить новых записей. Щелкните ПКМ на панели меню и выберите Изменить меню. Вы можете снять галочку с поля "Отображать", если хотите что бы данная запись меню не отображалась при выборе.

Для добавления новой записи, создайте файл .desktop в директории $XDG_DATA_HOME/applications (более вероятно, что в `~/.local/share`). Пример файла .desktop можете посмотреть ниже или здесь [GNOME documentation](http://library.gnome.org/admin/system-admin-guide/2.22/menustructure-desktopentry.html.en%7Cthe).

Или установите Alacarte, что позволит вам легко создать, изменить или убрать записи меню с помощью графического интерфейса. Используйте для этого команду:

```
# pacman -S alacarte

```

##### Группы меню, системное меню

Вы можете найти записи меню как "названиеприложения.desktop" файлов в одной из $XDG_DATA_DIRS/applications директорий(или скорее всего в `/usr/share/applications`). Чтобы добавить новый элемент в меню для всех пользователей, необходимо создать "названиеприложения.desktop" файл в одной из директорий.

*   Вы можете создать новый файл, в последствии используемого для запуска нового приложения. Или измените существующий.
*   Сохраните его как запись меню для всех пользователей
    В большинстве случаев, необходимо установить доступ к файлу равный 644 (root: rw group: r others: r), что бы смогли видеть все пользовтели.
*   Сохраните его как запись меню для группы или единичного пользователя
    Вы также можете иметь различные уровни доступа:как пример, некоторые записи меню будут доступны только определенной группе или только для одного пользователя.

Здесь пример, того как запись меню для Scite может выглядеть:

```
[Desktop Entry]
Encoding=UTF-8
Name=SciTE
Comment=SciTE editor
Type=Application
Exec=/usr/bin/scite
Icon=/usr/share/pixmaps/scite_48x48.png
Terminal=false
Categories=GNOME;Application;Development;
StartupNotify=true

```

#### Изменение логотипа Gnome на Arch

**Примечание:** Благодарность arkham, кто запостил данный способ в [[этот форум](https://bbs.archlinux.org/viewtopic.php?id=74881)]

*   Скачайте [[this Arch icon](http://img23.imageshack.us/img23/9679/starthere.png)] (имя файла `starthere.png`)
*   Или можете установить пакет artwork используя команду "pacman -S archlinux-artwork", что добавит новые файлы в каталог/usr/share/archlinux , и измените размер выбранного вами логотипа к 24х24px
*   Создайте в папке .icons домашней директории папку gnome

```
$ mkdir ~/.icons/gnome

```

*   Затем в ней папку 24x24

```
$ mkdir ~/.icons/gnome/24x24

```

*   В папке 24х24 создайте папку places и поместите туда файл иконки под именем start-here.png *формат должен быть .png, тире в середине обязятельно!*

```
$ mkdir ~/.icons/gnome/24x24/places
$ cp starthere.png ~/.icons/gnome/24x24/places/start-here.png

```

*   Перезапустите gnome-panels и наблюдайте логотип Arch, на месте прошлого

```
$ pkill gnome-panel

```

#### Другой способ изменить логотип

**Примечание:** У мене не заработал данный метод на Gnome 2.26.2, но убирать его не хочу.

Это быстрый способ сменить иконку ноги gnome с главного меню на любую на ваше усмотрение.

1.  Откройте редактор настроек в gnome (он находится в Системных приложения в главном меню) или лучше запустите `gconf-editor`
2.  В редакторе конфигураций перейдите в apps > panel > objects > найдите объект для вашего меню (простой способ найти его, это посмотреть секцию tooltip на наличие "Main Menu").
3.  Добавьте путь к вашей иконке в поле "Custom_Icon".
4.  Проверьте установлен ли "Use_Custom_Icon".
5.  Что бы изменения вступили в силу без перезагрузки Х-ов, откройте терминал и введите комманду:

```
$ killall gnome-panel

```

#### Удаление стандартных иконок с рабочего стола

Я люблю содержать мой рабочий стол в чистоте и наверно, я такой не один. Ниже описано как убрать иконки домашней папки, компьютера и корзины с рабочего стола:

1.  Откройте терминал
2.  Наберите: gconf-editor
3.  Редактор конфигурации откроется. Перейдите в: apps --> nautilus --> desktop
4.  Снимите галочки со всех иконок, от которых хотите избавиться
5.  Всё, теперь иконки должны моментально исчезнуть

#### Автоматическая смена обоев рабочего стола

Достаточно выполнить команду:

```
$ cp `ls -1 ~/Изображения/Обои/*.jpg | shuf -n1` ~/Изображения/Обои/.RandomWallpaper.jpg

```

где "~/Изображения/Обои/" - каталог с обоями, а ".RandomWallpaper.jpg" - текущие обои рабочего стола. При каждом выполнении данной команды содержимое файла .RandomWallpaper.jpg будет заменятся на случайное изображение из каталога ~/Изображения/Обои/ Команду можно добавить в Система -> Параметры -> Запускаемые приложения для смены обоев при входе в систему.

### Отключение прокрутки в панели задач

Довольно долго существует "баг" в панели задач Gnome: колесико мышки прокручивает окна. Раздражает, если у вас неплохая мышка и превращается в головную боль если вы пользуетесь тачпадом. Невозможно аккуратно перемещаться, если пользуешься тачпадом, поэтому если вы случайно прикоснулись к нему, в то время когда мышка находилась на панели задач, тогда все окна начинают быстро переключаться или мелькать. Никаких параметров, которые могут отключить данную особенность в gconf/preferences, нету. Это также справедливо и для KDE 3, на счет KDE 4 не знаю. Решение нашлось - установить xfce4-panel, которая лишена данной проблемы и выглядит как стандартная панель задач gnome. Эта ошибка хорошо описана здесь [[1]](https://bugs.launchpad.net/ubuntu/+source/gnome-panel/+bug/39328).

Возможно, эта ошибка никогда не была бы исправлена, но используя систему ABS, мы можем собрать соответствующие нашим запросам программу. Установите [ABS](/index.php/ABS "ABS") (+70Mb), затем

```
cp -r /var/abs/extra/libwnck /home/{your name}/Desktop/somewhere

```

Перейдите в данную директорию, затем выполните

```
makepkg --nobuild

```

Это скачает и распакует исходники. Перейдите в src/libwnck-{version}/libwnck. Подправьте tasklist.c, найдите строчку "scroll-event". Вы встретите, что-то на подобие этого:

```
g_signal_connect(obj, "scroll-event", G_CALLBACK(wnck_tasklist_scroll_cb), NULL);

```

Эта строчка кода устанавливает обработчик событий для прокрутки(scroll-event), закомментируйте данную строчку(достаточно вставить /* и */, перед и после данной строчки). Или можете просто удалить эту строчку. Теперь перейдите обратно в /home/{username}/Desktop/somewhere и

```
makepkg --noextract --syncdeps

```

Вы должны иметь [sudo](/index.php/Sudo_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Sudo (Русский)"), что бы установить недостающие зависимости (intltool), но вы всегда можете использовать 'pacman -S' по отдельности, если не желаете --syncdeps автоматически. Опция --noextract сообщает makepkg не распаковывать исходники и использовать существующие в src/

```
pacman -U libwnck-{version}.pkg.tar.gz

```

Затем разлогиньтесь/залогиньтесь и наслаждайтесь. Удалите папку с исходниками с вашего рабочего стола, если желаете, можете удалить abs. Следующим шагом будет, добавление опции в gconf, но я это оставлю для гуру Gnome. Мне просто незачем данная "фитча", даже если использую мышь. (alt+tab все равно лучшеу)anyway).

## Полезные дополнения

### FAM

FAM автоматически обновляет содержимое меню, когда устанавливается новое приложение, и обновляет содержимое директории в файловом менеджере, когда происходят изменения.

Здесь находятся [FAM Wiki](/index.php/FAM "FAM") инструкции по установке.

### Системный монитор Gnome

Это приложение появляется когда кликните на апплете "Системный монитор". Оно отображает использование процессора/памяти запущенными приложениями. Но это приложение не устанавливается по умолчанию вместе с групоой GNOME, поэтому вам придется установить его отдельно:

```
# pacman -S gnome-system-monitor

```

### Запись дисков CDs из файлового менеджера

```
# pacman -S nautilus-cd-burner

```

### Сервисные приложения GNOME

Это добавит несколько элементов в меню под Система->Администрирование, в особенности "пользователи и группы", "дата и время", "сеть", "службы" и "опубликованные папки" через samba или NFS. См. [GNOME documentation](http://projects.gnome.org/gst/).

```
# pacman -S [gnome-system-tools](https://aur.archlinux.org/packages/gnome-system-tools/)

```

**Обращайте внимание на сообщения pacman-a после установки.**

### Gdesklets: плюшки на рабочем столе

Добавьте часы, календарь, состояние погоды, и много другого на ваш рабочий стол

```
# pacman -S gdesklets

```

Вы можете найти больше desklet-ов на [gdesklets.org](http://www.gdesklets.de/?q=desklet/browse). Для установки их, скачайте файлы. Затем, в меню, откройте Приложения->Стандартные->gDesklets. Появится оболочка gDesklet-а, перетащите с помощью мышки файл нового gdesklet-a на оболочку. Если вы желаете, что бы во время загрузки, также загружались необходимые вам gdesklet-ы, выберите в меню Система->Параметры->Запускаемые приложения. Во вкладке "Автоматически запускаемые приложения" кликните по "добавить" и впишите в поле "команда" /usr/bin/gdesklets. Не забудьте проверить, действительно ли по данному пути находится gdesklets, с помощью команды "whereis gdesklets".

## Другие приложения

Здесь собраны хорошие приложения и утилиты для gnome, большинство которых можно установить за раз используя команду:

```
# pacman -S gnome-extra

```

Т.к. это группа, достаточно просто выбрать что загружать и не загружать некоторые пакеты, например, такие как документация.

### gnome-terminal

Если вы решите отказаться от использования xterm, установите данное приложение.

#### Выпадающие консоли

У gnom-а есть несколько выпадающих консолей, на создание которых вдохновили консоли используемые в играх на подобие Quake и Half-lif(при нажатие клавиши ~). Так же имеется, что-то похожее(Yakuake) под KDE, ниже представлены для Gnome.

##### Guake

Guake устанавливается следующей командой, но ему необходим Python. F12 используется по умолчанию для активации консоли. Дополнительная особенность Guake - множественные вкладки, по умолчанию используется комбинация Ctrl+PgUp и Ctrl+PgDown для переключение между этими терминалами.

```
# pacman -S guake

```

Так же вы можете установить прозрачность и другие настройки, сначала активировав консоль с помощью F12, затем правой кнопкой кликните на терминале и выберите Настройки.

Guake может запускаться автоматически при старте, добавьте следующее в меню Система->Параметры->Запускаемые приложения Выберите "добавить" и используйте наподобие этих параметров:

*   **Имя:** Guake
*   **Команда:** guake &
*   **Коментарий:** Guake Dropdown Terminal.

##### Tilda

Tilda еще один выпадающий терминал для Gnome. Если не возражаете, так же будет находится в данной секции.

```
# pacman -S tilda

```

### gedit

Текстовый редактор с подсветкой синтаксиса.

### eog

Eye-of-Gnome(глаз гнома), удобный, быстрый, легкий просмотрщик, который может изменять размер и поворачивать изображения.

### file-roller

Менеджер архивов, способный воспринимать множество различных форматов. (Установите unrar, unzip, ... для поддержки соответствующих форматов)

### gcalctool

Калькулятор, что еще нужно для счастья?

### rhythmbox

Аудио библиотека и плеер наподобие iTunes.

### sound-juicer

CD-рипер, интегрированный в rhythmbox.

*Включение mp3 профилей по умолчанию в меню настройки:*

```
# pacman -S gstreamer0.10-lame gstreamer0.10-taglib

```

**Примечание:** Уже не требуется проделывать это, с тех пор как эти пакеты стали включать в gstreamer0.10-ugly-plugins и gstreamer0.10-good-plugins

*Если у вас есть проблемы с SoundJuicer, обращайтесь [here](/index.php/User:Munk3h "User:Munk3h")*

### totem

Видео плеер, использует gstreamer для декодирования потока.

### gimp

Свободная альтернатива Photoshop для Линукса. Обязательный к применению, если вы как-то связаны с графикой.

### gftp

Хороший, маленький FTP клиент для gnome.

### abiword

Маленький, быстрый, .doc совместимый текстовый редактор.

### gnumeric

Хороший редактор электронных таблиц, наподобие excel.

### Возможность оставлять сообщения в хранителе экрана

Классная возможность появилась с версией gnome-screensaver 2.20, теперь каждый может оставить сообщение для вас, если вы не на месте.

**Примечание:** Пожалуйста, установите notification-daemon для работы приложения

### DevilsPie

Полезное приложение, которое может быть запущено как демон внутри gnome. Оно манипулирует созданием окон, позволяя вам выбрать на каком рабочем столе, с каким размером запускать выбранное вами приложение, а также другие характеристики. DevilsPie предоставляет целый новый уровень контроля внутри движка metacity. Здесь неплохой HOWTO [homepage](http://live.gnome.org/DevilsPie),

## См. также

*   [GNOME_(Русский)](/index.php/GNOME_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GNOME (Русский)")