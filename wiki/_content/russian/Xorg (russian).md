**Состояние перевода:** На этой странице представлен перевод статьи [Xorg](/index.php/Xorg "Xorg"). Дата последней синхронизации: 28 февраля 2018\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Xorg&diff=0&oldid=512264).

Ссылки по теме

*   [Автозапуск](/index.php/%D0%90%D0%B2%D1%82%D0%BE%D0%B7%D0%B0%D0%BF%D1%83%D1%81%D0%BA "Автозапуск")
*   [Экранный менеджер](/index.php/%D0%AD%D0%BA%D1%80%D0%B0%D0%BD%D0%BD%D1%8B%D0%B9_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80 "Экранный менеджер")
*   [Оконный менеджер](/index.php/%D0%9E%D0%BA%D0%BE%D0%BD%D0%BD%D1%8B%D0%B9_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80 "Оконный менеджер")
*   [Настройка шрифтов](/index.php/%D0%9D%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0_%D1%88%D1%80%D0%B8%D1%84%D1%82%D0%BE%D0%B2 "Настройка шрифтов")
*   [Темы курсора](/index.php/%D0%A2%D0%B5%D0%BC%D1%8B_%D0%BA%D1%83%D1%80%D1%81%D0%BE%D1%80%D0%B0 "Темы курсора")
*   [Среда рабочего стола](/index.php/%D0%A1%D1%80%D0%B5%D0%B4%D0%B0_%D1%80%D0%B0%D0%B1%D0%BE%D1%87%D0%B5%D0%B3%D0%BE_%D1%81%D1%82%D0%BE%D0%BB%D0%B0 "Среда рабочего стола")
*   [Wayland (Русский)](/index.php/Wayland_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Wayland (Русский)")
*   [xinitrc (Русский)](/index.php/Xinitrc_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xinitrc (Русский)")
*   [xrandr (Русский)](/index.php/Xrandr_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xrandr (Русский)")

C [http://www.x.org/wiki/](http://www.x.org/wiki/):

	Проект X.Org представляет свободную реализацию [оконной системы X](https://en.wikipedia.org/wiki/ru:X.Org_Server "w:ru:X.Org Server") с открытым исходным кодом. Разработка осуществляется X.Org Foundation, которая является образовательной некоммерческой организацией, совместно с сообществом freedesktop.org.

**Xorg** (обычно называемый просто **X**) очень популярен среди пользователей Linux, что привело к тому, что большинство приложений с графическим интерфейсом используют X11, из-за этого Xorg доступен в большинстве дистрибутивов. Для более подробной информации смотрите статью [Xorg](https://en.wikipedia.org/wiki/ru:X.Org_Server "w:ru:X.Org Server") в Википедии или посетите [веб-сайт Xorg](http://www.x.org/wiki/).

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
    *   [1.1 Установка драйвера](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.B4.D1.80.D0.B0.D0.B9.D0.B2.D0.B5.D1.80.D0.B0)
    *   [1.2 AMD](#AMD)
*   [2 Запуск](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA)
    *   [2.1 Экранный менеджер](#.D0.AD.D0.BA.D1.80.D0.B0.D0.BD.D0.BD.D1.8B.D0.B9_.D0.BC.D0.B5.D0.BD.D0.B5.D0.B4.D0.B6.D0.B5.D1.80)
    *   [2.2 Вручную](#.D0.92.D1.80.D1.83.D1.87.D0.BD.D1.83.D1.8E)
*   [3 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [3.1 Через файлы .conf](#.D0.A7.D0.B5.D1.80.D0.B5.D0.B7_.D1.84.D0.B0.D0.B9.D0.BB.D1.8B_.conf)
    *   [3.2 Через файл xorg.conf](#.D0.A7.D0.B5.D1.80.D0.B5.D0.B7_.D1.84.D0.B0.D0.B9.D0.BB_xorg.conf)
*   [4 Устройства ввода](#.D0.A3.D1.81.D1.82.D1.80.D0.BE.D0.B9.D1.81.D1.82.D0.B2.D0.B0_.D0.B2.D0.B2.D0.BE.D0.B4.D0.B0)
    *   [4.1 Ускорение мыши](#.D0.A3.D1.81.D0.BA.D0.BE.D1.80.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BC.D1.8B.D1.88.D0.B8)
    *   [4.2 Дополнительные кнопки мыши](#.D0.94.D0.BE.D0.BF.D0.BE.D0.BB.D0.BD.D0.B8.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D1.8B.D0.B5_.D0.BA.D0.BD.D0.BE.D0.BF.D0.BA.D0.B8_.D0.BC.D1.8B.D1.88.D0.B8)
    *   [4.3 Touchpad](#Touchpad)
    *   [4.4 Touchscreen](#Touchscreen)
    *   [4.5 Настройка клавиатуры](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D0.B0.D1.82.D1.83.D1.80.D1.8B)
*   [5 Настройка монитора](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D0.BC.D0.BE.D0.BD.D0.B8.D1.82.D0.BE.D1.80.D0.B0)
    *   [5.1 Начало работы](#.D0.9D.D0.B0.D1.87.D0.B0.D0.BB.D0.BE_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D1.8B)
    *   [5.2 Несколько мониторов](#.D0.9D.D0.B5.D1.81.D0.BA.D0.BE.D0.BB.D1.8C.D0.BA.D0.BE_.D0.BC.D0.BE.D0.BD.D0.B8.D1.82.D0.BE.D1.80.D0.BE.D0.B2)
        *   [5.2.1 Более одной видеокарты](#.D0.91.D0.BE.D0.BB.D0.B5.D0.B5_.D0.BE.D0.B4.D0.BD.D0.BE.D0.B9_.D0.B2.D0.B8.D0.B4.D0.B5.D0.BE.D0.BA.D0.B0.D1.80.D1.82.D1.8B)
    *   [5.3 Размер дисплея/DPI](#.D0.A0.D0.B0.D0.B7.D0.BC.D0.B5.D1.80_.D0.B4.D0.B8.D1.81.D0.BF.D0.BB.D0.B5.D1.8F.2FDPI)
        *   [5.3.1 Настройка DPI вручную](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_DPI_.D0.B2.D1.80.D1.83.D1.87.D0.BD.D1.83.D1.8E)
            *   [5.3.1.1 Проприетарный драйвер NVIDIA](#.D0.9F.D1.80.D0.BE.D0.BF.D1.80.D0.B8.D0.B5.D1.82.D0.B0.D1.80.D0.BD.D1.8B.D0.B9_.D0.B4.D1.80.D0.B0.D0.B9.D0.B2.D0.B5.D1.80_NVIDIA)
            *   [5.3.1.2 Настройка DPI вручную. Предостережение](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_DPI_.D0.B2.D1.80.D1.83.D1.87.D0.BD.D1.83.D1.8E._.D0.9F.D1.80.D0.B5.D0.B4.D0.BE.D1.81.D1.82.D0.B5.D1.80.D0.B5.D0.B6.D0.B5.D0.BD.D0.B8.D0.B5)
    *   [5.4 Управление питанием дисплея](#.D0.A3.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D0.B8.D1.82.D0.B0.D0.BD.D0.B8.D0.B5.D0.BC_.D0.B4.D0.B8.D1.81.D0.BF.D0.BB.D0.B5.D1.8F)
*   [6 Композит](#.D0.9A.D0.BE.D0.BC.D0.BF.D0.BE.D0.B7.D0.B8.D1.82)
    *   [6.1 Список композитных менеджеров](#.D0.A1.D0.BF.D0.B8.D1.81.D0.BE.D0.BA_.D0.BA.D0.BE.D0.BC.D0.BF.D0.BE.D0.B7.D0.B8.D1.82.D0.BD.D1.8B.D1.85_.D0.BC.D0.B5.D0.BD.D0.B5.D0.B4.D0.B6.D0.B5.D1.80.D0.BE.D0.B2)
*   [7 Советы и рекомендации](#.D0.A1.D0.BE.D0.B2.D0.B5.D1.82.D1.8B_.D0.B8_.D1.80.D0.B5.D0.BA.D0.BE.D0.BC.D0.B5.D0.BD.D0.B4.D0.B0.D1.86.D0.B8.D0.B8)
    *   [7.1 Закрытие приложение по хоткею](#.D0.97.D0.B0.D0.BA.D1.80.D1.8B.D1.82.D0.B8.D0.B5_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D0.BE_.D1.85.D0.BE.D1.82.D0.BA.D0.B5.D1.8E)
*   [8 Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [8.1 Если вместо всех шрифтов квадратики](#.D0.95.D1.81.D0.BB.D0.B8_.D0.B2.D0.BC.D0.B5.D1.81.D1.82.D0.BE_.D0.B2.D1.81.D0.B5.D1.85_.D1.88.D1.80.D0.B8.D1.84.D1.82.D0.BE.D0.B2_.D0.BA.D0.B2.D0.B0.D0.B4.D1.80.D0.B0.D1.82.D0.B8.D0.BA.D0.B8)
    *   [8.2 Быстрое решение конфликта с Bitstream-Vera](#.D0.91.D1.8B.D1.81.D1.82.D1.80.D0.BE.D0.B5_.D1.80.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BA.D0.BE.D0.BD.D1.84.D0.BB.D0.B8.D0.BA.D1.82.D0.B0_.D1.81_Bitstream-Vera)
    *   [8.3 Быстрое решение конфликтов файлов в /usr/include](#.D0.91.D1.8B.D1.81.D1.82.D1.80.D0.BE.D0.B5_.D1.80.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BA.D0.BE.D0.BD.D1.84.D0.BB.D0.B8.D0.BA.D1.82.D0.BE.D0.B2_.D1.84.D0.B0.D0.B9.D0.BB.D0.BE.D0.B2_.D0.B2_.2Fusr.2Finclude)
    *   [8.4 Конфликты с libgl-dri](#.D0.9A.D0.BE.D0.BD.D1.84.D0.BB.D0.B8.D0.BA.D1.82.D1.8B_.D1.81_libgl-dri)
    *   [8.5 НЕработающее колесо мыши](#.D0.9D.D0.95.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.B0.D1.8E.D1.89.D0.B5.D0.B5_.D0.BA.D0.BE.D0.BB.D0.B5.D1.81.D0.BE_.D0.BC.D1.8B.D1.88.D0.B8)
    *   [8.6 Дополнительные кнопки на мыши перестали работать](#.D0.94.D0.BE.D0.BF.D0.BE.D0.BB.D0.BD.D0.B8.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D1.8B.D0.B5_.D0.BA.D0.BD.D0.BE.D0.BF.D0.BA.D0.B8_.D0.BD.D0.B0_.D0.BC.D1.8B.D1.88.D0.B8_.D0.BF.D0.B5.D1.80.D0.B5.D1.81.D1.82.D0.B0.D0.BB.D0.B8_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.B0.D1.82.D1.8C)
    *   [8.7 Проблемы с клавиатурой](#.D0.9F.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D1.8B_.D1.81_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D0.B0.D1.82.D1.83.D1.80.D0.BE.D0.B9)
        *   [8.7.1 AltGR (Compose клавиша) не работает правильно](#AltGR_.28Compose_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D1.88.D0.B0.29_.D0.BD.D0.B5_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.B0.D0.B5.D1.82_.D0.BF.D1.80.D0.B0.D0.B2.D0.B8.D0.BB.D1.8C.D0.BD.D0.BE)
        *   [8.7.2 Невозможно установить раскладку командой setxkbmap](#.D0.9D.D0.B5.D0.B2.D0.BE.D0.B7.D0.BC.D0.BE.D0.B6.D0.BD.D0.BE_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.B8.D1.82.D1.8C_.D1.80.D0.B0.D1.81.D0.BA.D0.BB.D0.B0.D0.B4.D0.BA.D1.83_.D0.BA.D0.BE.D0.BC.D0.B0.D0.BD.D0.B4.D0.BE.D0.B9_setxkbmap)
        *   [8.7.3 Настройка франко-канадской раскладки (бывшая ca_enhanced)](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D1.84.D1.80.D0.B0.D0.BD.D0.BA.D0.BE-.D0.BA.D0.B0.D0.BD.D0.B0.D0.B4.D1.81.D0.BA.D0.BE.D0.B9_.D1.80.D0.B0.D1.81.D0.BA.D0.BB.D0.B0.D0.B4.D0.BA.D0.B8_.28.D0.B1.D1.8B.D0.B2.D1.88.D0.B0.D1.8F_ca_enhanced.29)
    *   [8.8 Отсутствующие библиотеки](#.D0.9E.D1.82.D1.81.D1.83.D1.82.D1.81.D1.82.D0.B2.D1.83.D1.8E.D1.89.D0.B8.D0.B5_.D0.B1.D0.B8.D0.B1.D0.BB.D0.B8.D0.BE.D1.82.D0.B5.D0.BA.D0.B8)
    *   [8.9 Некоторые пакеты не собираются, жалуясь на отсутствующие X11 includes](#.D0.9D.D0.B5.D0.BA.D0.BE.D1.82.D0.BE.D1.80.D1.8B.D0.B5_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D1.8B_.D0.BD.D0.B5_.D1.81.D0.BE.D0.B1.D0.B8.D1.80.D0.B0.D1.8E.D1.82.D1.81.D1.8F.2C_.D0.B6.D0.B0.D0.BB.D1.83.D1.8F.D1.81.D1.8C_.D0.BD.D0.B0_.D0.BE.D1.82.D1.81.D1.83.D1.82.D1.81.D1.82.D0.B2.D1.83.D1.8E.D1.89.D0.B8.D0.B5_X11_includes)
    *   [8.10 Невозможно загрузить шрифт '(null)'](#.D0.9D.D0.B5.D0.B2.D0.BE.D0.B7.D0.BC.D0.BE.D0.B6.D0.BD.D0.BE_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.B8.D1.82.D1.8C_.D1.88.D1.80.D0.B8.D1.84.D1.82_.27.28null.29.27)
    *   [8.11 Иконки KDE в панели задач и на Десктопе не работают](#.D0.98.D0.BA.D0.BE.D0.BD.D0.BA.D0.B8_KDE_.D0.B2_.D0.BF.D0.B0.D0.BD.D0.B5.D0.BB.D0.B8_.D0.B7.D0.B0.D0.B4.D0.B0.D1.87_.D0.B8_.D0.BD.D0.B0_.D0.94.D0.B5.D1.81.D0.BA.D1.82.D0.BE.D0.BF.D0.B5_.D0.BD.D0.B5_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.B0.D1.8E.D1.82)
    *   [8.12 Обновление с testing до current (отсутствующие файлы)](#.D0.9E.D0.B1.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D1.81_testing_.D0.B4.D0.BE_current_.28.D0.BE.D1.82.D1.81.D1.83.D1.82.D1.81.D1.82.D0.B2.D1.83.D1.8E.D1.89.D0.B8.D0.B5_.D1.84.D0.B0.D0.B9.D0.BB.D1.8B.29)
    *   [8.13 Проблемы с MIME типами в различных DE](#.D0.9F.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D1.8B_.D1.81_MIME_.D1.82.D0.B8.D0.BF.D0.B0.D0.BC.D0.B8_.D0.B2_.D1.80.D0.B0.D0.B7.D0.BB.D0.B8.D1.87.D0.BD.D1.8B.D1.85_DE)
    *   [8.14 DRI перестало работать с картами Matrox](#DRI_.D0.BF.D0.B5.D1.80.D0.B5.D1.81.D1.82.D0.B0.D0.BB.D0.BE_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.B0.D1.82.D1.8C_.D1.81_.D0.BA.D0.B0.D1.80.D1.82.D0.B0.D0.BC.D0.B8_Matrox)
    *   [8.15 Не выставляется нужное разрешение экрана](#.D0.9D.D0.B5_.D0.B2.D1.8B.D1.81.D1.82.D0.B0.D0.B2.D0.BB.D1.8F.D0.B5.D1.82.D1.81.D1.8F_.D0.BD.D1.83.D0.B6.D0.BD.D0.BE.D0.B5_.D1.80.D0.B0.D0.B7.D1.80.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D1.8D.D0.BA.D1.80.D0.B0.D0.BD.D0.B0)
*   [9 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [xorg-server](https://www.archlinux.org/packages/?name=xorg-server).

В дополнение к нему, могут понадобиться пакеты из группы [xorg-apps](https://www.archlinux.org/groups/x86_64/xorg-apps/) для некоторых способов настроек. О них рассказано в соответствующих разделах.

К тому же имеется группа [xorg](https://www.archlinux.org/groups/x86_64/xorg/), которая включает пакеты оконной системы Xorg и пакеты из группы [xorg-apps](https://www.archlinux.org/groups/x86_64/xorg-apps/), а также шрифты.

**Совет:** Вам, скорее всего, понадобится [оконный менеджер](/index.php/%D0%9E%D0%BA%D0%BE%D0%BD%D0%BD%D1%8B%D0%B9_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80 "Оконный менеджер") или [среда рабочего стола](/index.php/%D0%A1%D1%80%D0%B5%D0%B4%D0%B0_%D1%80%D0%B0%D0%B1%D0%BE%D1%87%D0%B5%D0%B3%D0%BE_%D1%81%D1%82%D0%BE%D0%BB%D0%B0 "Среда рабочего стола") в дополнение к X.

### Установка драйвера

Ядро Linux включает в себя видеодрайверы с открытым исходным кодом и поддержку аппаратного ускорения буфера кадров. Однако, для работы OpenGL и двухмерного ускорения в X11 требуется поддержка пользовательского ПО.

Сперва определите вашу видеокарту:

```
$ lspci | grep -e VGA -e 3D

```

Затем установите соответствующий драйвер. Вы можете поискать в базе данных пакетов полный список видеодрайверов с открытым исходным кодом:

```
$ pacman -Ss xf86-video

```

Xorg автоматически ищет установленные драйверы:

*   Если он не может найти установленным необходимый драйвер для оборудования (перечислены ниже), тогда он сначала ищет драйвер *fbdev* ([xf86-video-fbdev](https://www.archlinux.org/packages/?name=xf86-video-fbdev)).
*   Если и он не найден, тогда Xorg ищет общий драйвер *vesa* ([xf86-video-vesa](https://www.archlinux.org/packages/?name=xf86-video-vesa)), который поддерживает большое количество чипсетов, но не включает 2D или 3D ускорение.
*   А если и *vesa* не найден, тогда X обратится к режиму [KMS](/index.php/Kernel_mode_setting_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Kernel mode setting (Русский)"), который включает ускорение GLAMOR (смотрите [modesetting(4)](https://jlk.fjfi.cvut.cz/arch/manpages/man/modesetting.4)).

Для того, чтобы ускорение видео работало, и часто для того, чтобы разблокировать все режимы, в которых может работать GPU, требуется правильный видеодрайвер:

| Бренд | Тип | Драйвер | OpenGL | OpenGL ([Multilib](/index.php/Multilib_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Multilib (Русский)")) | Документация |
| **AMD/
ATI** | Свободный | [xf86-video-amdgpu](https://www.archlinux.org/packages/?name=xf86-video-amdgpu) | [mesa](https://www.archlinux.org/packages/?name=mesa) | [lib32-mesa](https://www.archlinux.org/packages/?name=lib32-mesa) | [AMDGPU (Русский)](/index.php/AMDGPU_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AMDGPU (Русский)") |
| [xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati) | [ATI (Русский)](/index.php/ATI_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ATI (Русский)") |
| Проприетарный | [catalyst](https://aur.archlinux.org/packages/catalyst/) | [catalyst-libgl](https://aur.archlinux.org/packages/catalyst-libgl/) | [lib32-catalyst-libgl](https://aur.archlinux.org/packages/lib32-catalyst-libgl/) | [AMD Catalyst (Русский)](/index.php/AMD_Catalyst_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AMD Catalyst (Русский)") |
| **Intel** | Свободный | [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) | [mesa](https://www.archlinux.org/packages/?name=mesa) | [lib32-mesa](https://www.archlinux.org/packages/?name=lib32-mesa) | [Intel graphics (Русский)](/index.php/Intel_graphics_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Intel graphics (Русский)") |
| **Nvidia** | Свободный | [xf86-video-nouveau](https://www.archlinux.org/packages/?name=xf86-video-nouveau) | [mesa](https://www.archlinux.org/packages/?name=mesa) | [lib32-mesa](https://www.archlinux.org/packages/?name=lib32-mesa) | [Nouveau (Русский)](/index.php/Nouveau_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Nouveau (Русский)") |
| Проприетарный | [nvidia](https://www.archlinux.org/packages/?name=nvidia) | [nvidia-utils](https://www.archlinux.org/packages/?name=nvidia-utils) | [lib32-nvidia-utils](https://www.archlinux.org/packages/?name=lib32-nvidia-utils) | [NVIDIA (Русский)](/index.php/NVIDIA_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "NVIDIA (Русский)") |
| [nvidia-340xx](https://www.archlinux.org/packages/?name=nvidia-340xx) | [nvidia-340xx-utils](https://www.archlinux.org/packages/?name=nvidia-340xx-utils) | [lib32-nvidia-340xx-utils](https://www.archlinux.org/packages/?name=lib32-nvidia-340xx-utils) |

**Примечание:** Если Вы пользуетесь ноутбуком с поддержкой NVIDIA Optimus, который использует интегрированную видеокарту вместе с дискретной видеокартой, обратитесь к статье [NVIDIA Optimus (Русский)](/index.php/NVIDIA_Optimus_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "NVIDIA Optimus (Русский)") или [Bumblebee (Русский)](/index.php/Bumblebee_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Bumblebee (Русский)").

Другие видео драйверы можно найти в группе [xorg-drivers](https://www.archlinux.org/groups/x86_64/xorg-drivers/).

Во избежание проблем X следует запускать без драйверов с закрытым исходным кодом, которые обычно требуются только для расширенных возможностей, таких, как быстрый 3D рендеринг в играх.

### AMD

| Архитектура GPU | Карты Radeon | Драйвер с открытым исходным кодом | Проприетарный драйвер |
| GCN 4
и новее | [варианты](https://en.wikipedia.org/wiki/ru:%D0%A1%D0%BF%D0%B8%D1%81%D0%BE%D0%BA_%D0%B3%D1%80%D0%B0%D1%84%D0%B8%D1%87%D0%B5%D1%81%D0%BA%D0%B8%D1%85_%D0%BF%D1%80%D0%BE%D1%86%D0%B5%D1%81%D1%81%D0%BE%D1%80%D0%BE%D0%B2_AMD "w:ru:Список графических процессоров AMD") | [AMDGPU (Русский)](/index.php/AMDGPU_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AMDGPU (Русский)") | [AMDGPU PRO (Русский)](/index.php/AMDGPU_PRO_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AMDGPU PRO (Русский)") |
| GCN 3 | [AMDGPU (Русский)](/index.php/AMDGPU_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AMDGPU (Русский)") | [Catalyst (Русский)](/index.php/Catalyst_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Catalyst (Русский)") /
[AMDGPU PRO (Русский)](/index.php/AMDGPU_PRO_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AMDGPU PRO (Русский)") |
| GCN 2 | [AMDGPU (Русский)](/index.php/AMDGPU_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AMDGPU (Русский)")* / [ATI (Русский)](/index.php/ATI_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ATI (Русский)") | [Catalyst (Русский)](/index.php/Catalyst_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Catalyst (Русский)") |
| GCN 1 | [AMDGPU (Русский)](/index.php/AMDGPU_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AMDGPU (Русский)")* / [ATI (Русский)](/index.php/ATI_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ATI (Русский)") | [Catalyst (Русский)](/index.php/Catalyst_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Catalyst (Русский)") |
| TeraScale 2&3 | HD 5000 - HD 6000 | [ATI (Русский)](/index.php/ATI_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ATI (Русский)") | [Catalyst (Русский)](/index.php/Catalyst_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Catalyst (Русский)") |
| TeraScale 1 | HD 2000 - HD 4000 | устаревший [Catalyst (Русский)](/index.php/Catalyst_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Catalyst (Русский)") |
| Старые | X1000 и старше | *недоступен* |

	*: Экспериментальный

## Запуск

### Экранный менеджер

Использование [экранного менеджера](/index.php/%D0%AD%D0%BA%D1%80%D0%B0%D0%BD%D0%BD%D1%8B%D0%B9_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80 "Экранный менеджер") для запуска X удобно, но для этого требуется дополнительное приложение и некоторые зависимости для него.

### Вручную

Чтобы запустить X без экранного менеджера, смотрите статью [xinitrc (Русский)](/index.php/Xinitrc_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xinitrc (Русский)").

## Настройка

**Примечание:** Arch предоставляет файлы конфигурации по умолчанию в `/usr/share/X11/xorg.conf.d`. Большинству пользователей никакая дополнительная настройка не нужна.

Xorg можно настроить через `xorg.conf` и через файлы, заканчивающие на `.conf`: полный список каталог, где можно найти эти файлы есть в [xorg.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xorg.conf.5) вместе с подробным объяснением всех доступных опций.

### Через файлы .conf

Каталог `/etc/X11/xorg.conf.d/` хранит конфигурацию, специфичную для хоста (вашего компьютера). Вы можете свободно добавлять конфигурационные файлы сюда, но они обязательно должны оканчиваться на `.conf`: файлы читаются в кодировке ASCII и по соглашению их имена должны начинаться с `*XX*-` (две цифры и дефис, так, например, файл, начинающийся на 10, читается раньше 20). Эти файлы анализируются x-сервером при запуске и рассматриваются как часть традиционного конфигурационного файла `xorg.conf`. Обратите внимание, что при конфликтующей настройки *последний* прочитанный файл будет обработан. Поэтому наиболее общие файлы конфигурации должны быть упорядочены по имени. Конфигурационные записи в `xorg.conf` обрабатываются в конце.

Смотрите примеры настройки на [вики fedora](http://fedoraproject.org/wiki/Input_device_configuration#xorg.conf.d).

### Через файл xorg.conf

Xorg также можно настраивать через `/etc/X11/xorg.conf` или `/etc/xorg.conf`. Чтобы сгенерировать основу файла `xorg.conf`:

```
# Xorg :0 -configure

```

Это создает файл `xorg.conf.new` в `/root/`, который можно скопировать в `/etc/X11/xorg.conf`.

**Совет:** Если вы уже запустили X, тогда используйте другой дисплей, например `Xorg :2 -configure`.

Кроме того, ваш проприетарный видеодрайвер может поставляться с инструментом для автоматической настройки Xorg: смотрите статьи [NVIDIA (Русский)](/index.php/NVIDIA_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "NVIDIA (Русский)") или [AMD Catalyst (Русский)](/index.php/AMD_Catalyst_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AMD Catalyst (Русский)") для подробностей.

**Примечание:** Ключевые слова файла конфигурации не учитывают регистр, а символы "_" игнорируются. Большинство строк (включая имена опций) также нечувствительны к регистру и к пробелам, да к символам "_".

## Устройства ввода

Для устройств ввода в X по умолчанию используют драйвер libinput ([xf86-input-libinput](https://www.archlinux.org/packages/?name=xf86-input-libinput)), но также можно использовать драйвер [xf86-input-evdev](https://www.archlinux.org/packages/?name=xf86-input-evdev) и другие соответствующие драйверы.[[1]](https://www.archlinux.org/news/xorg-server-1191-is-now-in-extra/)

[Udev](/index.php/Udev_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Udev (Русский)"), являющий зависимостью systemd, обнаруживает аппаратное обеспечение, и поэтому оба драйвера будут работать в режиме горячего подключения устройств ввода практически для всех устройств, как определенно в стандарных конфигурационных файлах `10-quirks.conf` и `40-libinput.conf` в каталоге `/usr/share/X11/xorg.conf.d/`.

После запуска оконной системы X, в лог-файле будет записываться информация об используемом драйвере для каждого подключенного устройства (обратите внимание, что имя последнего лог-файла может отличаться):

```
$ grep -e "Using input driver " Xorg.0.log

```

Если оба драйвера не поддерживают конкретное устройство, установите необходимый драйвер из группы [xorg-drivers](https://www.archlinux.org/groups/x86_64/xorg-drivers/). То же самое относится, если вы желаете использовать другой драйвер.

Чтобы изменить поведение горячего подключения (hotplugging), смотрите статью [#Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0).

Для получения конкретных инструкций, смотрите статью [libinput](/index.php/Libinput "Libinput"), следующие страницы ниже, или записи в [википедии Fedora](https://fedoraproject.org/wiki/Input_device_configuration).

### Ускорение мыши

Смотрите [Mouse acceleration](/index.php/Mouse_acceleration "Mouse acceleration").

### Дополнительные кнопки мыши

Смотрите [кнопки мыши](/index.php/%D0%9A%D0%BD%D0%BE%D0%BF%D0%BA%D0%B8_%D0%BC%D1%8B%D1%88%D0%B8 "Кнопки мыши").

### Touchpad

Смотрите [libinput](/index.php/Libinput "Libinput") или [Touchpad Synaptics (Русский)](/index.php/Touchpad_Synaptics_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Touchpad Synaptics (Русский)").

### Touchscreen

Смотрите [Touchscreen](/index.php/Touchscreen "Touchscreen").

### Настройка клавиатуры

Смотрите [конфигурация клавиатуры в Xorg](/index.php/%D0%9A%D0%BE%D0%BD%D1%84%D0%B8%D0%B3%D1%83%D1%80%D0%B0%D1%86%D0%B8%D1%8F_%D0%BA%D0%BB%D0%B0%D0%B2%D0%B8%D0%B0%D1%82%D1%83%D1%80%D1%8B_%D0%B2_Xorg "Конфигурация клавиатуры в Xorg").

## Настройка монитора

#### Начало работы

**Примечание:** Новые версии Xorg автоматически все настраивают, поэтому вам не следует что-либо менять тем более, если вы не знаете, что делаете.

Создайте новый файл конфигурации, например `/etc/X11/xorg.conf.d/10-monitor.conf`.

 `/etc/X11/xorg.conf.d/10-monitor.conf` 
```
Section "Monitor"
    Identifier             "Monitor0"
EndSection

Section "Device"
    Identifier             "Device0"
    Driver                 "vesa" #Выберите драйвер для этого монитора
EndSection

Section "Screen"
    Identifier             "Screen0"  #Collapse Monitor and Device section to Screen section
    Device                 "Device0"
    Monitor                "Monitor0"
    DefaultDepth           16 #Выберите глубину (16||24)
    SubSection             "Display"
        Depth              16
        Modes              "1024x768_75.00" #Выберите разрешение
    EndSubSection
EndSection

```

**Примечание:** По умолчанию Xorg должен иметь возможность обнаружить монитор, иначе он не запустится вовсе. Обходной путь заключается в создании файла конфигурации, такого как указано выше, и, таким образом, мы избежим автоматическую настройку. Часто это необходимо, когда Х запускаются автоматически и система используется без монитора, либо, если [вход в систему](/index.php/%D0%90%D0%B2%D1%82%D0%BE%D0%B7%D0%B0%D0%BF%D1%83%D1%81%D0%BA_X_%D0%BF%D1%80%D0%B8_%D0%B2%D1%85%D0%BE%D0%B4%D0%B5_%D0%B2_%D1%81%D0%B8%D1%81%D1%82%D0%B5%D0%BC%D1%83 "Автозапуск X при входе в систему") осуществляется через [виртуальную консоль](/index.php/Automatic_login_to_virtual_console "Automatic login to virtual console"), или из [экранного менеджера](/index.php/%D0%AD%D0%BA%D1%80%D0%B0%D0%BD%D0%BD%D1%8B%D0%B9_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80 "Экранный менеджер").

### Несколько мониторов

Смотрите главную статью [Multihead](/index.php/Multihead "Multihead") для получения общей информации.

Также смотрите специфичные инструкции для GPU:

*   [NVIDIA (Русский)#Несколько мониторов](/index.php/NVIDIA_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.9D.D0.B5.D1.81.D0.BA.D0.BE.D0.BB.D1.8C.D0.BA.D0.BE_.D0.BC.D0.BE.D0.BD.D0.B8.D1.82.D0.BE.D1.80.D0.BE.D0.B2 "NVIDIA (Русский)")
*   [Nouveau (Русский)#DualHead](/index.php/Nouveau_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#DualHead "Nouveau (Русский)")
*   [AMD Catalyst (Русский)#Два экрана (Dual Head / Dual Screen / Xinerama)](/index.php/AMD_Catalyst_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.94.D0.B2.D0.B0_.D1.8D.D0.BA.D1.80.D0.B0.D0.BD.D0.B0_.28Dual_Head_.2F_Dual_Screen_.2F_Xinerama.29 "AMD Catalyst (Русский)")
*   [ATI#Multihead setup](/index.php/ATI#Multihead_setup "ATI")

#### Более одной видеокарты

Вы должны определить нужный драйвер для использования и ввести ID шины (BusID) нужной видеокарты.

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

Чтобы узнать ID шины:

 `$ lspci | grep VGA` 
```
01:00.0 VGA compatible controller: nVidia Corporation G96 [GeForce 9600M GT] (rev a1)

```

ID шины здесь 1:0:0.

### Размер дисплея/DPI

DPI оконной системы X устанавливается следующими способами:

1.  Параметр командной строки -dpi имеет наивысший приоритет.
2.  Если он не используется, параметр DisplaySize в файле конфигурации X используется для получения DPI, учитывая разрешение экрана.
3.  Если параметр DisplaySize не задан, значения размера монитора используются из [DDC](https://en.wikipedia.org/wiki/ru:Display_Data_Channel "w:ru:Display Data Channel") для получения DPI с учетом разрешения экрана.
4.  Если DDC не определяет размер, по умолчанию используется 75 DPI.

Чтобы получить правильные точки на дюйм (DPI), разрешение дисплея должно быть распознано или установлено. Наличие правильного DPI особенно необходимо, когда требуются точные детали (например, рендеринг шрифтов). Ранее производители пытались создать стандарт для 96 DPI (монитор с диагональю размером 10,3 дюйма был бы 800x600, 13,2-дюймовый монитор - 1024x768). Сейчас DPI экраном отличаются и могут быть не равными по горизонтали и по вертикали. Например, 19-дюймовый широкоэкранный ЖК-дисплей с разрешением 1440x900 может иметь DPI 89х87\. Чтобы установить DPI, сервер Xorg пытается автоматически определить физическое разрешение вашего монитора с помощью видеокарты с DDC. ~~Когда Xorg знает физическое разрешение экрана, он сможет установить правильный DPI в зависимости от размера этого разрешения.~~

Чтобы убедиться, что разрешение вашего дисплея и DPI обнаружены/правильно рассчитаны:

```
$ xdpyinfo | grep -B2 resolution

```

Убедитесь, что выведенное разрешение соответствует настоящему разрешению вашего монитора. Если Xorg не может правильно рассчитать разрешение экрана, он по умолчанию установит значение 75x75 DPI. Поэтому вам придется самому рассчитать его.

Если у вас есть в спецификации физическое разрешение экрана, его можно ввести в конфигурационный файл Xorg так, чтобы был рассчитан правильный DPI:

```
Section "Monitor"
    Identifier             "Monitor0"
    DisplaySize             286 179    # В миллиметрах
EndSection

```

Если вы только хотите ввести спецификацию вашего монитора **без** создания полного xorg.conf, тогда создайте новый конфигурационный файл. Например, (`/etc/X11/xorg.conf.d/90-monitor.conf`):

```
Section "Monitor"
    Identifier             "<default monitor>"
    DisplaySize            286 179    # В миллиметрах
EndSection

```

Если у вас нет в спецификации ширины и высоты монитора (сейчас в большинстве спецификаций указывается только размер диагонали), вы можете использовать родное разрешение монитора (или соотношение сторон) и размер диагонали для вычисления горизонтальных и вертикальных размеров. Используя теорему Пифагора для монитора с диагональю 13,3" и с родным разрешением 1280x800 (или соотношением сторон 16:10):

```
$ echo 'scale=5;sqrt(1280^2+800^2)' | bc  # 1509.43698

```

Вы получите размер диагонали в пикселях. С помощью него можно узнать ширину и высоту монитора в дюймах (а затем перевести их в миллиметры):

```
$ echo 'scale=5;(13.3/1509)*1280*25.4' | bc  # 286.43072
$ echo 'scale=5;(13.3/1509)*800*25.4'  | bc  # 179.01920

```

**Примечание:** Эти вычисления работают для мониторов с квадратными пикселями; однако, иногда встречаются мониторы, сжимающие соотношение сторон (например, разрешение изображения на мониторе с 16:10 до 16:9). В этом случае, придется измерить разрешение монитора вручную.

#### Настройка DPI вручную

**Примечание:** Сейчас вы можете установить любой dpi, который вам нравится, и тогда приложения, использующие Qt и GTK, будут масштабироваться соответственно. Рекомендуется установить dpi в 96, 120 (на 25% больше), 144 (на 50% больше), 168 (на 75% болше), 192 (на 100% больше) и т.д. для уменьшения масштабирования артефактов в приложениях с GUI, использующие растровые изображения. Уменьшение точек на дюйм (dpi) ниже 96 может не снижать размер графический элементов GUI. Обычно, наименьшее количество dpi, на которое сделаны значки, равно 96.

Для RandR-совместимых драйверов (например, драйвер ATI с открытым исходным кодом) вы можете установить dpi так:

```
$ xrandr --dpi 144

```

**Примечание:** Для уже запущенных приложений настройка не применяется сразу, поэтому вы должны перезапустить их.

Чтобы сделать его постоянным, посмотрите [запуск команд после запуска X](/index.php/%D0%97%D0%B0%D0%BF%D1%83%D1%81%D0%BA_%D0%BA%D0%BE%D0%BC%D0%B0%D0%BD%D0%B4_%D0%BF%D0%BE%D1%81%D0%BB%D0%B5_%D0%B7%D0%B0%D0%BF%D1%83%D1%81%D0%BA%D0%B0_X "Запуск команд после запуска X").

##### Проприетарный драйвер NVIDIA

DPI можно установить вручную, если вы планируете использовать только одно разрешение экрана ([калькулятор DPI](http://pxcalc.com/)):

```
Section "Monitor"
    Identifier             "Monitor0"
    Option                 "DPI" "96 x 96"
EndSection

```

Вы можете установить DPI вручную, добавив параметры ниже в `/etc/X11/xorg.conf.d/20-nvidia.conf` (внутри раздела **Device**):

```
Option              "UseEdidDpi" "False"
Option              "DPI" "96 x 96"

```

##### Настройка DPI вручную. Предостережение

GTK очень часто переопределяет DPI сервера через опциональный файл Xresource `Xft.dpi`. Чтобы выяснить происходит ли это у вас, введите:

```
$ xrdb -query | grep dpi

```

Начиная с версии GTK 3.16, если эта переменная явно не задана, GTK устанавливает ее в 96\. Чтобы приложения GTK работали с DPI сервера, вам может потребоваться явно установить Xft.dpi на то же значение, что и сервер. С помощью файла ресурсов Xft.dpi некоторые среды рабочего стола опционально приводят DPI к определенному значению в личных настройках. Среди них KDE и TDE.

### Управление питанием дисплея

[DPMS](/index.php/DPMS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "DPMS (Русский)") (Display Power Management Signaling (англ), сигналы управления энергопотреблением дисплеев) — технология, позволяющая настроить энергосбережение монитора, когда компьютер не используется. Она позволит вам автоматически переключить монитор в режим ожидания через определенное время простоя.

## Композит

Композитное расширение для X приводит к вынесению всего поддерева иерархии окон в буфер вне экрана. Затем приложения могут загружать содержимое этого буфера и делать все, что им нравится. Закадровый буфер может автоматически объединяться в родительское окно или объединяться внешними программами, называемыми композитными менеджерами. Для получения дополнительной информации смотрите следующую статью: [w:ru:Композитный менеджер окон](https://en.wikipedia.org/wiki/ru:%D0%9A%D0%BE%D0%BC%D0%BF%D0%BE%D0%B7%D0%B8%D1%82%D0%BD%D1%8B%D0%B9_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80_%D0%BE%D0%BA%D0%BE%D0%BD "w:ru:Композитный менеджер окон")

Некоторые оконные менеджеры (например, [Compiz](/index.php/Compiz_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Compiz (Русский)"), [Enlightenment](/index.php/Enlightenment_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Enlightenment (Русский)"), KWin, Marco, Metacity, Muffin, Mutter, [Xfwm](/index.php/Xfce_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xfce (Русский)")) имеют встроенный композит. Для других оконных менеджеров можно использовать отдельные композитные менеджеры.

### Список композитных менеджеров

*   **[Compton](/index.php/Compton_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Compton (Русский)")** — Композитный оконный менеджер (форк xcompmgr-dana)

	[https://github.com/chjj/compton](https://github.com/chjj/compton) || [compton](https://www.archlinux.org/packages/?name=compton)

*   **[Xcompmgr](/index.php/Xcompmgr_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xcompmgr (Русский)")** — Композитный оконный менеджер

	[http://cgit.freedesktop.org/xorg/app/xcompmgr/](http://cgit.freedesktop.org/xorg/app/xcompmgr/) || [xcompmgr](https://www.archlinux.org/packages/?name=xcompmgr)

*   **Unagi** — Модульный композитный менеджер, написанный на Си и основанный на XCB

	[http://projects.mini-dweeb.org/projects/unagi](http://projects.mini-dweeb.org/projects/unagi) || [unagi](https://aur.archlinux.org/packages/unagi/)

## Советы и рекомендации

### Закрытие приложение по хоткею

Привяжите скрипт к хоткею:

```
#!/bin/bash
windowFocus=$(xdotool getwindowfocus);
pid=$(xprop -id $windowFocus | grep PID);
kill -9 $pid

```

Зависимости: [xorg-xprop](https://www.archlinux.org/packages/?name=xorg-xprop), [xdotool](https://www.archlinux.org/packages/?name=xdotool)

## Решение проблем

### Если вместо всех шрифтов квадратики

1.  pango-querymodules > /etc/pango/pango.modules

### Быстрое решение конфликта с Bitstream-Vera

Если вы видите сообщение о конфликте ttf-bitstream-vera conflicts и xorg:

1.  Выйдите из pacman'а, ответив no.
2.  Run `pacman -Rd xorg`
3.  Run `pacman -Syu`
4.  Run `pacman -S xorg`
5.  Обновите пути в файле /etc/X11/xorg.conf

### Быстрое решение конфликтов файлов в /usr/include

Если вы видите сообщения о конфликтах файлов в /usr/include/X11 и /usr/include/GL:

1.  выполните `rm /usr/include/{GL,X11}`
2.  выполните `pacman -Su`

Каталоги, на которые были созданы символические ссылки будут удаленыи заменены реальными каталогами в новом пакете xorg, который и вызвал конфликт у файлов.

### Конфликты с libgl-dri

Если вы видите сообщение типа:

```
:: libgl-dri conflicts with nvidia-legacy. Remove nvidia-legacy? [Y/n]

```

это проиходит из-за нескольких реализаций OpenGL, объяснённых в разделе OpenGL выше - pacman пытается установить libgl-dri для удовлетворения зависимостей, но ещё и хочет обновить ваш видеодрайвер, а они конфликтуют. Для разрешения проблемы попробуйте:

*   обновить видеодрайвер перед полным обновлением системы:

```
pacman -S nvidia-legacy
pacman -Syu

```

или, если это не работает:

*   Удалить существующий видеодрайвер, обновиться, потом переустановить драйвер:

```
$ pacman -Rd nvidia-legacy
$ pacman -Syu
$ pacman -S nvidia-legacy
:: nvidia-legacy conflicts with libgl-dri. Remove libgl-dri? [Y/n] **Y**

```

### НЕработающее колесо мыши

Протокол "Auto" не работает правильно в Xorg 7\. В секции InputDevice для мыши, измените:

```
Option         "Protocol" "auto"

```

на

```
Option         "Protocol" "IMPS/2"

```

или

```
Option         "Protocol" "ExplorerPS/2"

```

### Дополнительные кнопки на мыши перестали работать

Пользователи USB мышей должны прочитать [Get All Mouse Buttons Working](/index.php/Get_All_Mouse_Buttons_Working "Get All Mouse Buttons Working").

Пользователи Intellimouse (ExplorerPS/2) могут столкнуться с неработающим скроллом и боковыми кнопками. Раньше была запись в xorg.conf:

```
Option      "Buttons" "7"
Option      "ZAxisMapping" "6 7"

```

и пользователи также запускали xmodmap, чтобы боковые кнопки работали, командой типа:

```
xmodmap -e "pointer = 1 2 3 6 7 4 5"

```

Теперь xmodmap не нужен. Вместо этого исправьте xorg.conf так:

```
Option      "Buttons" "5"
Option      "ZAxisMapping" "4 5"
Option      "ButtonMapping" "1 2 3 6 7"

```

и боковые кнопки 7-кнопочной Intellimouse будут работать, как и прежде, без запуска xmodmap.

### Проблемы с клавиатурой

Некоторые раскладки клавиатуры изменились. Стало невозможным:

*   использовать Ctrl+Alt+Fx для переключения между консолями
*   переключаться по раскладкам
*   использовать знак £ для локали gb

Проблема заключается в том, что некоторые раскладки (например, *sk_qwerty*, *uk*) перестали существовать. Следует заменить

```
Option         "XkbLayout" "us,sk_qwerty"

```

на

```
Option         "XkbLayout" "us,sk"
Option         "XkbVariant" ",qwerty"

```

Также обратите внимание на следующие строки:

```
Option "XkbRules"   "xfree86"    #должно быть "xorg"
Option "XkbVariant" "nodeadkeys" #эта строчка может вызывать описанные выше проблемы, попробуйте её закомментировать.

```

#### AltGR (Compose клавиша) не работает правильно

Если после обновления вы не можете использовать клавишу altGr, как раньше её использовали, попробуйте добавить эту строку в раздел клавиатуры:

```
Option      "XkbOptions" "compose:ralt"

```

Это не совсем правильный вариант активирования клавиши AltGr на немецкой клавиатуре (например, чтобы использовать знаки '|' и '@'). Просто выберите верный keyboard variant, чтобы клавиша снова заработала, например (для немецкой клавиатуры):

```
Option      "XkbLayout" "de"
Option      "XkbVariant" "nodeadkeys"

```

Вышеуказанные решения не работают, если у вас итальянская клавиатура. Для того чтобы активировать клавишу AltGr на итальянской клавиатуре, проверьте правильность следующих строк:

```
 Driver          "kbd"
 Option          "XkbRules"      "xorg"
 Option          "XkbVariant"    ""

```

#### Невозможно установить раскладку командой setxkbmap

После обновления некоторые qwerty раскладки были удалены, например sk_qwerty. Если вы хотите переключить имеющуюся раскладку на другую qwerty, используйте следующую команду:

```
setxkbmap NAME_OF_THE_LAYOUT qwerty

```

например, для sk_qwerty вводите:

```
setxkbmap sk qwerty

```

Может так получиться, что после обновления и вышеприведённой команды будет сообщение: "Error loading new keyboard description". Оказывается, xserver не имеет прав записи, исполнения и чтения в /var/tmp Просто дайте права на эту директорию и перезапустите xserver!

#### Настройка франко-канадской раскладки (бывшая ca_enhanced)

В Xorg7 "ca_enhanced" более не существует. Для получения той раскладки, которая была, придётся использовать маленький трюк. Измените

```
       Option          "XkbLayout"     "ca_enhanced"

```

на

```
       Option          "XkbLayout"     "ca"
       Option          "XkbVariant"    "fr"

```

То же самое, видимо, и с другими подобными раскладками. Вы можете обратиться к Gentoo HowTo по этому вопросу: [http://www.gentoo.org/proj/en/desktop/x/x11/modular-x-howto.xml](http://www.gentoo.org/proj/en/desktop/x/x11/modular-x-howto.xml)

### Отсутствующие библиотеки

*   **Помогите! Постоянно вываливается окно с сообщением об ошибке запуска моей любимой программы: "libXчто-то" не существует!**

В большинстве случаев всё, что вам нужно сделать, - это взять имя библиотеки (например,libXau.so.1), перевести название в нижний регистр и установить её:

```
pacman -S libxau

```

### Некоторые пакеты не собираются, жалуясь на отсутствующие X11 includes

Просто переустановите пакеты xproto и libx11, даже если они уже установлены.

### Невозможно загрузить шрифт '(null)'

*   **Некоторые программы не работают и говорят, что не могут загрузить шрифт `(null)'.**

Эти пакеты хотят каких-то дополнительных шрифтов. Некоторые программы работают только с bitmap шрифтами. Доступны два больших пакета, содержащих bitmap шрифты, xorg-fonts-75dpi и xorg-fonts-100dpi. Вам не нужны оба, достаточно и одного. Чтобы найти, какой вам подходит больше, попробуйте команду:

```
xdpyinfo | grep resolution

```

и выберите, что ближе (75 или 100 вместо XX)

```
pacman -S xorg-fonts-XXdpi

```

### Иконки KDE в панели задач и на Десктопе не работают

*   **Панель задач KDEне работает и исчезли иконки на рабочем столе**

Установите пакеты libxcomposite и libxss:

```
pacman -S libxcomposite libxss

```

### Обновление с testing до current (отсутствующие файлы)

Если вы обновились с Xorg 7 из testing до Xorg 7 из current и обнаружили, что много файлов отсутствуют (включая startx, /usr/share/X11/rgb.txt и другие), потеря могла произойти из-за того, что пакет xorg-clients был разбит на много мелких пакетов.

Вам необходимо переустановить пакеты, которые являются зависимостями xorg-clients:

```
pacman -S xorg-apps xorg-font-utils xorg-res-utils xorg-server-utils \
          xorg-twm xorg-utils xorg-xauth xorg-xdm xorg-xfs xorg-xfwp \
          xorg-xinit xorg-xkb-utils xorg-xsm

```

Это должно разрешить проблему.

### Проблемы с MIME типами в различных DE

Если вы заметили недостающие иконки и вы не можете открывать файлы по щелчку мыши в вашем DE, добавьте следующие строчки в /etc/profile или предпочитаемый скрипт загрузки и перезагрузитесь.

```
XDG_DATA_DIRS=$XDG_DATA_DIRS:/usr/share
export XDG_DATA_DIRS

```

### DRI перестало работать с картами Matrox

Если вы используете карту Matrox и DRI не работает после обновления до xorg7, попробуйте добавить строку

```
Option "OldDmaInit" "On"

```

в секцию Device, описывающую видеокарту в xorg.conf.

### Не выставляется нужное разрешение экрана

Если Xorg запускается разрешением экрана, не соответствующим максимально возможному для вашего монитора - попробуйте расширить диапазон частот **VertRefresh** в секции **Monitor**. Некоторые мониторы не могут воспроизводить картинку своего максимального разрешения на максимальной частоте.

## Смотрите также

*   [Добавление экранного менеджера входа в систему (GDM или XDM) в автозагрузку](/index.php?title=%D0%94%D0%BE%D0%B1%D0%B0%D0%B2%D0%BB%D0%B5%D0%BD%D0%B8%D0%B5_%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%BD%D0%BE%D0%B3%D0%BE_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80%D0%B0_%D0%B2%D1%85%D0%BE%D0%B4%D0%B0_%D0%B2_%D1%81%D0%B8%D1%81%D1%82%D0%B5%D0%BC%D1%83_(GDM_%D0%B8%D0%BB%D0%B8_XDM)_%D0%B2_%D0%B0%D0%B2%D1%82%D0%BE%D0%B7%D0%B0%D0%B3%D1%80%D1%83%D0%B7%D0%BA%D1%83&action=edit&redlink=1 "Добавление экранного менеджера входа в систему (GDM или XDM) в автозагрузку (page does not exist)")
*   [Запуск X при загрузке](/index.php/%D0%97%D0%B0%D0%BF%D1%83%D1%81%D0%BA_X_%D0%BF%D1%80%D0%B8_%D0%B7%D0%B0%D0%B3%D1%80%D1%83%D0%B7%D0%BA%D0%B5 "Запуск X при загрузке")
*   [Xorg Font Configuration (Русский)](/index.php/Xorg_Font_Configuration_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xorg Font Configuration (Русский)")
*   Проприетарные видеодрайверы
    *   [ATI wiki](/index.php/ATI "ATI")
    *   [NVIDIA (Русский)](/index.php/NVIDIA_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "NVIDIA (Русский)")
*   [Среды рабочего стола](/index.php/Desktop_environment_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Desktop environment (Русский)")
    *   [KDE](/index.php/KDE "KDE")
    *   [GNOME (Русский)](/index.php/GNOME_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GNOME (Русский)")
    *   [MATE](/index.php/MATE "MATE")
    *   [Xfce](/index.php/Xfce "Xfce")
    *   [Enlightenment](/index.php/Enlightenment "Enlightenment")
    *   [Fluxbox](/index.php/Fluxbox "Fluxbox")
*   [Compiz](/index.php/Compiz "Compiz")

Внешние ссылки:

*   [X.org Wikipedia Article](https://en.wikipedia.org/wiki/X.Org_Server "wikipedia:X.Org Server")
*   [X.org](http://wiki.x.org/wiki/)