**Xorg** - свободная открытая реализация оконной системы X11\. Xorg очень популярен среди пользователей Linux, что привело к тому, что большинство приложений с графическим интерфейсом используют X11, из-за этого Xorg доступен в большинстве дистрибутивов. Более подробную информацию смотрите в [статье о Xorg в Википедии](http://en.wikipedia.org/wiki/X.Org_Server) или [на wiki X.org](http://wiki.x.org/wiki/)

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
    *   [1.1 Driver installation](#Driver_installation)
*   [2 Запуск](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA)
*   [3 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [3.1 Устройства ввода](#.D0.A3.D1.81.D1.82.D1.80.D0.BE.D0.B9.D1.81.D1.82.D0.B2.D0.B0_.D0.B2.D0.B2.D0.BE.D0.B4.D0.B0)
        *   [3.1.1 Synaptics Touchpad](#Synaptics_Touchpad)
        *   [3.1.2 Отключение горячего подключения](#.D0.9E.D1.82.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B3.D0.BE.D1.80.D1.8F.D1.87.D0.B5.D0.B3.D0.BE_.D0.BF.D0.BE.D0.B4.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D1.8F)
    *   [3.2 Настройки клавиатуры](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B8_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D0.B0.D1.82.D1.83.D1.80.D1.8B)
        *   [3.2.1 Задержка и скорость повтора](#.D0.97.D0.B0.D0.B4.D0.B5.D1.80.D0.B6.D0.BA.D0.B0_.D0.B8_.D1.81.D0.BA.D0.BE.D1.80.D0.BE.D1.81.D1.82.D1.8C_.D0.BF.D0.BE.D0.B2.D1.82.D0.BE.D1.80.D0.B0)
        *   [3.2.2 Просмотр настроек клавиатуры](#.D0.9F.D1.80.D0.BE.D1.81.D0.BC.D0.BE.D1.82.D1.80_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B5.D0.BA_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D0.B0.D1.82.D1.83.D1.80.D1.8B)
        *   [3.2.3 Переключение раскладок средствами X.org](#.D0.9F.D0.B5.D1.80.D0.B5.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D1.80.D0.B0.D1.81.D0.BA.D0.BB.D0.B0.D0.B4.D0.BE.D0.BA_.D1.81.D1.80.D0.B5.D0.B4.D1.81.D1.82.D0.B2.D0.B0.D0.BC.D0.B8_X.org)
        *   [3.2.4 Включение pointerkeys](#.D0.92.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_pointerkeys)
        *   [3.2.5 Модель клавиатуры](#.D0.9C.D0.BE.D0.B4.D0.B5.D0.BB.D1.8C_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D0.B0.D1.82.D1.83.D1.80.D1.8B)
    *   [3.3 InputClasses](#InputClasses)
*   [4 Графика](#.D0.93.D1.80.D0.B0.D1.84.D0.B8.D0.BA.D0.B0)
    *   [4.1 Установка драйвера](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.B4.D1.80.D0.B0.D0.B9.D0.B2.D0.B5.D1.80.D0.B0)
    *   [4.2 Настройка монитора](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D0.BC.D0.BE.D0.BD.D0.B8.D1.82.D0.BE.D1.80.D0.B0)
        *   [4.2.1 Начало работы](#.D0.9D.D0.B0.D1.87.D0.B0.D0.BB.D0.BE_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D1.8B)
        *   [4.2.2 Несколько мониторов](#.D0.9D.D0.B5.D1.81.D0.BA.D0.BE.D0.BB.D1.8C.D0.BA.D0.BE_.D0.BC.D0.BE.D0.BD.D0.B8.D1.82.D0.BE.D1.80.D0.BE.D0.B2)
            *   [4.2.2.1 NVIDIA](#NVIDIA)
            *   [4.2.2.2 Более одной видеокарты](#.D0.91.D0.BE.D0.BB.D0.B5.D0.B5_.D0.BE.D0.B4.D0.BD.D0.BE.D0.B9_.D0.B2.D0.B8.D0.B4.D0.B5.D0.BE.D0.BA.D0.B0.D1.80.D1.82.D1.8B)
            *   [4.2.2.3 Скрипт для переключения внутреннего/внешнего мониторов для ноутбуков](#.D0.A1.D0.BA.D1.80.D0.B8.D0.BF.D1.82_.D0.B4.D0.BB.D1.8F_.D0.BF.D0.B5.D1.80.D0.B5.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D1.8F_.D0.B2.D0.BD.D1.83.D1.82.D1.80.D0.B5.D0.BD.D0.BD.D0.B5.D0.B3.D0.BE.2F.D0.B2.D0.BD.D0.B5.D1.88.D0.BD.D0.B5.D0.B3.D0.BE_.D0.BC.D0.BE.D0.BD.D0.B8.D1.82.D0.BE.D1.80.D0.BE.D0.B2_.D0.B4.D0.BB.D1.8F_.D0.BD.D0.BE.D1.83.D1.82.D0.B1.D1.83.D0.BA.D0.BE.D0.B2)
    *   [4.3 Размер дисплея/DPI](#.D0.A0.D0.B0.D0.B7.D0.BC.D0.B5.D1.80_.D0.B4.D0.B8.D1.81.D0.BF.D0.BB.D0.B5.D1.8F.2FDPI)
    *   [4.4 DPMS](#DPMS)
    *   [4.5 Monitor](#Monitor)
        *   [4.5.1 Строчная синхронизация (horizontal sync)](#.D0.A1.D1.82.D1.80.D0.BE.D1.87.D0.BD.D0.B0.D1.8F_.D1.81.D0.B8.D0.BD.D1.85.D1.80.D0.BE.D0.BD.D0.B8.D0.B7.D0.B0.D1.86.D0.B8.D1.8F_.28horizontal_sync.29)
        *   [4.5.2 Частота обновления](#.D0.A7.D0.B0.D1.81.D1.82.D0.BE.D1.82.D0.B0_.D0.BE.D0.B1.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D1.8F)
    *   [4.6 Screen](#Screen)
        *   [4.6.1 Глубина цветовой гаммы](#.D0.93.D0.BB.D1.83.D0.B1.D0.B8.D0.BD.D0.B0_.D1.86.D0.B2.D0.B5.D1.82.D0.BE.D0.B2.D0.BE.D0.B9_.D0.B3.D0.B0.D0.BC.D0.BC.D1.8B)
        *   [4.6.2 Разрешение](#.D0.A0.D0.B0.D0.B7.D1.80.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5)
    *   [4.7 Шрифты](#.D0.A8.D1.80.D0.B8.D1.84.D1.82.D1.8B)
    *   [4.8 Примеры файлов xorg.conf](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.80.D1.8B_.D1.84.D0.B0.D0.B9.D0.BB.D0.BE.D0.B2_xorg.conf)
*   [5 Усовершенствование загрузки X](#.D0.A3.D1.81.D0.BE.D0.B2.D0.B5.D1.80.D1.88.D0.B5.D0.BD.D1.81.D1.82.D0.B2.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B8_X)
*   [6 Изменения в модульном Xorg](#.D0.98.D0.B7.D0.BC.D0.B5.D0.BD.D0.B5.D0.BD.D0.B8.D1.8F_.D0.B2_.D0.BC.D0.BE.D0.B4.D1.83.D0.BB.D1.8C.D0.BD.D0.BE.D0.BC_Xorg)
    *   [6.1 Самые распространённые пакеты](#.D0.A1.D0.B0.D0.BC.D1.8B.D0.B5_.D1.80.D0.B0.D1.81.D0.BF.D1.80.D0.BE.D1.81.D1.82.D1.80.D0.B0.D0.BD.D1.91.D0.BD.D0.BD.D1.8B.D0.B5_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D1.8B)
    *   [6.2 OpenGL 3D ускорение](#OpenGL_3D_.D1.83.D1.81.D0.BA.D0.BE.D1.80.D0.B5.D0.BD.D0.B8.D0.B5)
    *   [6.3 glxgears и glxinfo](#glxgears_.D0.B8_glxinfo)
*   [7 Tips & tricks](#Tips_.26_tricks)
    *   [7.1 Закрытие приложение по хоткею](#.D0.97.D0.B0.D0.BA.D1.80.D1.8B.D1.82.D0.B8.D0.B5_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D0.BE_.D1.85.D0.BE.D1.82.D0.BA.D0.B5.D1.8E)
*   [8 Проблемы](#.D0.9F.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D1.8B)
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
    *   [8.8 KDM/GDM не работают](#KDM.2FGDM_.D0.BD.D0.B5_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.B0.D1.8E.D1.82)
    *   [8.9 Отсутствующие библиотеки](#.D0.9E.D1.82.D1.81.D1.83.D1.82.D1.81.D1.82.D0.B2.D1.83.D1.8E.D1.89.D0.B8.D0.B5_.D0.B1.D0.B8.D0.B1.D0.BB.D0.B8.D0.BE.D1.82.D0.B5.D0.BA.D0.B8)
    *   [8.10 Некоторые пакеты не собираются, жалуясь на отсутствующие X11 includes](#.D0.9D.D0.B5.D0.BA.D0.BE.D1.82.D0.BE.D1.80.D1.8B.D0.B5_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D1.8B_.D0.BD.D0.B5_.D1.81.D0.BE.D0.B1.D0.B8.D1.80.D0.B0.D1.8E.D1.82.D1.81.D1.8F.2C_.D0.B6.D0.B0.D0.BB.D1.83.D1.8F.D1.81.D1.8C_.D0.BD.D0.B0_.D0.BE.D1.82.D1.81.D1.83.D1.82.D1.81.D1.82.D0.B2.D1.83.D1.8E.D1.89.D0.B8.D0.B5_X11_includes)
    *   [8.11 Невозможно загрузить шрифт '(null)'](#.D0.9D.D0.B5.D0.B2.D0.BE.D0.B7.D0.BC.D0.BE.D0.B6.D0.BD.D0.BE_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.B8.D1.82.D1.8C_.D1.88.D1.80.D0.B8.D1.84.D1.82_.27.28null.29.27)
    *   [8.12 Иконки KDE в панели задач и на Десктопе не работают](#.D0.98.D0.BA.D0.BE.D0.BD.D0.BA.D0.B8_KDE_.D0.B2_.D0.BF.D0.B0.D0.BD.D0.B5.D0.BB.D0.B8_.D0.B7.D0.B0.D0.B4.D0.B0.D1.87_.D0.B8_.D0.BD.D0.B0_.D0.94.D0.B5.D1.81.D0.BA.D1.82.D0.BE.D0.BF.D0.B5_.D0.BD.D0.B5_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.B0.D1.8E.D1.82)
    *   [8.13 Обновление с testing до current (отсутствующие файлы)](#.D0.9E.D0.B1.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D1.81_testing_.D0.B4.D0.BE_current_.28.D0.BE.D1.82.D1.81.D1.83.D1.82.D1.81.D1.82.D0.B2.D1.83.D1.8E.D1.89.D0.B8.D0.B5_.D1.84.D0.B0.D0.B9.D0.BB.D1.8B.29)
    *   [8.14 Проблемы с MIME типами в различных DE](#.D0.9F.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D1.8B_.D1.81_MIME_.D1.82.D0.B8.D0.BF.D0.B0.D0.BC.D0.B8_.D0.B2_.D1.80.D0.B0.D0.B7.D0.BB.D0.B8.D1.87.D0.BD.D1.8B.D1.85_DE)
    *   [8.15 DRI перестало работать с картами Matrox](#DRI_.D0.BF.D0.B5.D1.80.D0.B5.D1.81.D1.82.D0.B0.D0.BB.D0.BE_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.B0.D1.82.D1.8C_.D1.81_.D0.BA.D0.B0.D1.80.D1.82.D0.B0.D0.BC.D0.B8_Matrox)
    *   [8.16 Не выставляется нужное разрешение экрана](#.D0.9D.D0.B5_.D0.B2.D1.8B.D1.81.D1.82.D0.B0.D0.B2.D0.BB.D1.8F.D0.B5.D1.82.D1.81.D1.8F_.D0.BD.D1.83.D0.B6.D0.BD.D0.BE.D0.B5_.D1.80.D0.B0.D0.B7.D1.80.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D1.8D.D0.BA.D1.80.D0.B0.D0.BD.D0.B0)
*   [9 Полезные ссылки](#.D0.9F.D0.BE.D0.BB.D0.B5.D0.B7.D0.BD.D1.8B.D0.B5_.D1.81.D1.81.D1.8B.D0.BB.D0.BA.D0.B8)

## Установка

[Установите](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pacman (Русский)") пакет [xorg-server](https://www.archlinux.org/packages/?name=xorg-server) из [официальных репозиториев](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)").

В дополнение к нему, могут понадобиться пакеты из мета-пакета [xorg-server-utils](https://www.archlinux.org/packages/?name=xorg-server-utils) для некоторых способов настроек. О них рассказано в соответствующих разделах. Другие полезные пакеты находятся в группе [xorg-apps](https://www.archlinux.org/groups/x86_64/xorg-apps/).

**Совет:** Вам, скорее всего, понадобится установить [оконный менеджер](/index.php/%D0%9E%D0%BA%D0%BE%D0%BD%D0%BD%D1%8B%D0%B9_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80 "Оконный менеджер") или [среду рабочего стола](/index.php/Desktop_environment_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Desktop environment (Русский)") для X.

### Driver installation

The Linux kernel includes open-source video drivers and support for hardware accelerated framebuffers. However, userland support is required for OpenGL and 2D acceleration in X11.

First, identify your card:

```
$ lspci | grep -e VGA -e 3D

```

Then install an appropriate driver. You can search the package database for a complete list of open-source video drivers:

```
$ pacman -Ss xf86-video

```

The default graphics driver is [xf86-video-vesa](https://www.archlinux.org/packages/?name=xf86-video-vesa), which handles a large number of chipsets but does not include any 2D or 3D acceleration. If a better driver cannot be found or fails to load, Xorg will fall back to _vesa_.

In order for video acceleration to work, and often to expose all the modes that the GPU can set, a proper video driver is required:

**Note:** If you have a NVIDIA Optimus enabled laptop which uses an integrated video card combined with a dedicated GPU, see [Bumblebee](/index.php/Bumblebee "Bumblebee").

| Бренд | Тип | Драйвер | [Multilib](/index.php/Multilib_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Multilib (Русский)") | Документация |
| **AMD/ATI** | Свободный | [xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati) | [lib32-mesa-libgl](https://www.archlinux.org/packages/?name=lib32-mesa-libgl) | [ATI (Русский)](/index.php/ATI_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ATI (Русский)") |
| Проприетарный | [catalyst](https://aur.archlinux.org/packages/catalyst/) | [lib32-catalyst-utils](https://aur.archlinux.org/packages/lib32-catalyst-utils/) | [AMD Catalyst](/index.php/AMD_Catalyst "AMD Catalyst") |
| **Intel** | Свободный | [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) | [lib32-mesa-libgl](https://www.archlinux.org/packages/?name=lib32-mesa-libgl) | [Intel graphics (Русский)](/index.php/Intel_graphics_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Intel graphics (Русский)") |
| **Nvidia** | Свободный | [xf86-video-nouveau](https://www.archlinux.org/packages/?name=xf86-video-nouveau) | [lib32-mesa-libgl](https://www.archlinux.org/packages/?name=lib32-mesa-libgl) | [Nouveau (Русский)](/index.php/Nouveau_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Nouveau (Русский)") |
| Проприетарный | [nvidia](https://www.archlinux.org/packages/?name=nvidia) | [lib32-nvidia-libgl](https://www.archlinux.org/packages/?name=lib32-nvidia-libgl) | [NVIDIA (Русский)](/index.php/NVIDIA_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "NVIDIA (Русский)") |
| [nvidia-340xx](https://www.archlinux.org/packages/?name=nvidia-340xx) | [lib32-nvidia-340xx-libgl](https://www.archlinux.org/packages/?name=lib32-nvidia-340xx-libgl) |
| [nvidia-304xx](https://www.archlinux.org/packages/?name=nvidia-304xx) | [lib32-nvidia-304xx-libgl](https://www.archlinux.org/packages/?name=lib32-nvidia-304xx-libgl) |

Другие видео драйверы можно найти в группе [xorg-drivers](https://www.archlinux.org/groups/x86_64/xorg-drivers/).

Xorg should run smoothly without closed source drivers, which are typically needed only for advanced features such as fast 3D-accelerated rendering for games.

## Запуск

_См. также: [Запуск X при загрузке](/index.php/Start_X_at_Boot_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Start X at Boot (Русский)")_

**Совет:** Самый простой способ запустить X — воспользоваться [экранным менеджером](/index.php/Display_manager_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Display manager (Русский)"), например [GDM](/index.php/GDM "GDM"), [KDM](/index.php/KDM "KDM") или [SLiM](/index.php/SLiM "SLiM").

Если вы хотите запустить X без менеджера дисплея, установите пакет [xorg-xinit](https://www.archlinux.org/packages/?name=xorg-xinit). Можно установить [xorg-twm](https://www.archlinux.org/packages/?name=xorg-twm), [xorg-xclock](https://www.archlinux.org/packages/?name=xorg-xclock) и [xterm](https://www.archlinux.org/packages/?name=xterm), чтобы запустилась среда, установленная по умолчанию.

Команды `startx` и `xinit` запустят X-сервер и клиенты (Команда `startx` — просто интерфейс для более универсальной команды `xinit`). Для определения клиента `startx`/`xinit` читают файл `~/.xinitrc`. При его отсутствии читается `/etc/X11/xinit/xinitrc`, который запустит оконный менеджер [Twm](/index.php/Twm "Twm"), [Xclock](https://en.wikipedia.org/wiki/Xclock "wikipedia:Xclock") и [Xterm](/index.php/Xterm "Xterm").

Более подробная информация доступна в статье [xinitrc](/index.php/Xinitrc_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xinitrc (Русский)").

**Обратите внимание:**

*   Если возникают проблемы, почитайте журнал в `/var/log/Xorg.0.log`. Строчки, начинающиеся с `(EE)` сообщают об ошибках, `(WW)` — предупреждения.
*   Если файл `~/.xinitrc` _пустой_, нужно удалить или [отредактировать его](/index.php/Xinitrc_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xinitrc (Русский)"), чтобы запустить X правильно. Если этого не сделать, X покажет пустой экран без ошибок в `Xorg.0.log`. Удаление этого файла запустит среду по умолчанию.

## Настройка

Xorg можно настроить через `/etc/X11/xorg.conf`, `/etc/xorg.conf` или файлы, находящиеся в каталоге `/etc/X11/xorg.conf.d/`. Обычно никаких настроек не требуется. Вы можете создавать новые файлы конфигурации в `/etc/X11/xorg.conf.d/`, но их имена должны начинаться с `XX-`, где XX — номер, и оканчиваться на `.conf` (например, файл, начинающийся на 10, запускается раньше 20).

Кроме того, драйвер может поставляться с инструментами для настройки Xorg. Например, для NVIDIA запустите nvidia-xconfig, для ATI — aticonfig.

### Устройства ввода

#### Synaptics Touchpad

_Основная статья: [Touchpad Synaptics](/index.php/Touchpad_Synaptics_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Touchpad Synaptics (Русский)")_

Если у вас ноутбук, [установите](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.BE.D0.BF.D1.80.D0.B5.D0.B4.D0.B5.D0.BB.D0.B5.D0.BD.D0.BD.D1.8B.D1.85_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.BE.D0.B2 "Pacman (Русский)") драйвер тачпада из пакета [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics), доступного в [официальном репозитории](/index.php/Official_Repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official Repositories (Русский)").

После установки вы можете обнаружить файл `10-synaptics.conf` в `/etc/X11/xorg.conf.d`. Можете закомментировать или удалить строчки `InputClass`, связанные с тачпадом, в файле `10-evdev.conf`.

#### Отключение горячего подключения

С версии **1.8** Xorg-server использует udev для определения устройств. Эта настройка отключает его использование.

```
Section "ServerFlags"
    Option          "AutoAddDevices" "False"
EndSection

```

**Важно:** Это отключит горячее подключения для **всех** устройств ввода. Гораздо удобнее, чтобы udev сам подключал устройства. **Отключение горячего подключения не рекомендуется!**

### Настройки клавиатуры

Xorg может определить клавиатуру неправильно, что может дать проблемы с раскладкой.

Чтобы увидеть полный список поддерживаемых моделей клавиатур и раскладок, откройте `/usr/share/X11/xkb/rules/xorg.lst`.

Установка раскладки для текущего сеанса Xorg:

```
# setxkbmap dvorak

```

#### Задержка и скорость повтора

Используйте команду `xset r rate DELAY RATE` для изменения, потом запишите команду в `~/.xinitrc`, чтобы сохранить настройки.

#### Просмотр настроек клавиатуры

 `$ setxkbmap -print -verbose 10` 

```

 Setting verbose level to 10
 locale is C
 Applied rules from evdev:
 model:      evdev
 layout:     us
 options:    terminate:ctrl_alt_bksp
 Trying to build keymap using the following components:
 keycodes:   evdev+aliases(qwerty)
 types:      complete
 compat:     complete
 symbols:    pc+us+inet(evdev)+terminate(ctrl_alt_bksp)
 geometry:   pc(pc104)
 xkb_keymap {
         xkb_keycodes  { include "evdev+aliases(qwerty)" };
         xkb_types     { include "complete"      };
         xkb_compat    { include "complete"      };
         xkb_symbols   { include "pc+us+inet(evdev)+terminate(ctrl_alt_bksp)"    };
         xkb_geometry  { include "pc(pc104)"     };
 };

```

В связи с выходом X.org 1.8, HAL больше не отвечает за переключение раскладок клавиатуры.

#### Переключение раскладок средствами X.org

**Обратите внимание:** Установите [xorg-xkbevd](https://www.archlinux.org/packages/?name=xorg-xkbevd) и добавьте `xkbevd` в секцию DAEMONS файла `/etc/rc.conf`.

Для настройки переключения раскладок нужно создать новый файл в `/etc/X11/xorg.conf.d/`, например, `20-keyboard-layout.conf` со следующим содержанием:

```
Section "InputClass"
	Identifier             "keyboard-layout"
	MatchIsKeyboard        "on"
	Option "XkbLayout" "us,ru"
	Option "XkbOptions" "grp:caps_toggle,grp_led:scroll"
EndSection
```

За комбинацию клавиш переключения между двумя раскладками отвечает опция XkbOptions. Например, если вы хотите настроить переключение по Caps Lock:

```
Option "XkbOptions" "grp:caps_toggle"

```

Или переключение по Ctrl+Shift:

```
Option "XkbOptions" "grp:ctrl_shift_toggle"

```

Опция "grp_led:scroll" отвечает за включение индикатора Scroll Lock при смене на вторую раскладку (в данном случае - ru(winkeys)). Можно использовать вместо Scroll Lock и Caps Lock, и Num Lock.

Также вместо редактирования настроек можно добавить следующую команду в `~/.xinitrc`:

```
setxkbmap -layout "us,ru" -option "grp:caps_toggle,grp_led:scroll"

```

#### Включение pointerkeys

[Mouse keys](https://en.wikipedia.org/wiki/Mouse_keys "wikipedia:Mouse keys") теперь по умолчанию отключены, и их нужно включать вручную:

 `/etc/X11/xorg.conf.d/20-enable-pointerkeys.conf` 

```
Section "InputClass"
    Identifier             "Keyboard Defaults"
    MatchIsKeyboard        "yes"
    Option                 "XkbOptions" "keypad:pointerkeys"
EndSection
```

Также можно запустить:

```
$ setxkbmap -option keypad:pointerkeys

```

Both will make the `Shift+Num Lock` shortcut toggle mouse keys.

#### Модель клавиатуры

Чтобы изменить модель клавиатуры, используйте опцию XkbModel в разделе InputDevice клавиатуры. Например, если у вас клавиатура Microsoft Wireless Multimedia Keyboard:

```
Option "XkbModel" "microsoftmult"

```

### InputClasses

## Графика

### Установка драйвера

Графическим драйвером по умолчанию является vesa ([xf86-video-vesa](https://www.archlinux.org/packages/?name=xf86-video-vesa)), поддерживаемый почти всеми видеокартами, но в нем нет поддержки 2D или 3D ускорения, для включения которого вам потребуется установить драйвер специально для вашей видеокарты.

Для начала определите ее:

```
$ lspci | grep VGA

```

После этого установите соответствующий драйвер. Вы можете поискать их с помощью команды:

```
$ pacman -Ss xf86-video

```

Доступные открытые драйверы:

*   NVIDIA: [xf86-video-nouveau](https://www.archlinux.org/packages/?name=xf86-video-nouveau) (см. [Nouveau](/index.php/Nouveau "Nouveau"))
*   Intel: [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) (см. [Intel](/index.php/Intel "Intel"))
*   ATI: [xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati) (см. [ATI](/index.php/ATI "ATI"))

Проприетарные драйверы:

*   NVIDIA: [nvidia](https://www.archlinux.org/packages/?name=nvidia) (см. [NVIDIA](/index.php/NVIDIA "NVIDIA"))
*   ATI: [catalyst](https://aur.archlinux.org/packages/catalyst/) (см. [ATI Catalyst](/index.php/ATI_Catalyst "ATI Catalyst"))

Xorg должен работать гладко и без проприетарных драйверов, которые обычно нужны только для «продвинутых» функций, таких как быстрое 3D-ускорение, настройка нескольких экранов и ТВ-выход.

### Настройка монитора

#### Начало работы

**Обратите внимание:** Эти настройки необязательны, и не следует что-либо менять, если вы не знаете, что делаете.
Но нужно выполнять настройку при использовании двух мониторов и драйвера nouveau. См. [Nouveau#Configuration](/index.php/Nouveau#Configuration "Nouveau").

Создайте новый файл конфигурации, например `/etc/X11/xorg.conf.d/10-monitor.conf`. Вставьте в него следующий код:

```
Section "Monitor"
    Identifier             "Monitor0"
EndSection

Section "Device"
    Identifier             "Device0"
    Driver                 "vesa" #Choose the driver used for this monitor
EndSection

Section "Screen"
    Identifier             "Screen0"  #Collapse Monitor and Device section to Screen section
    Device                 "Device0"
    Monitor                "Monitor0"
    DefaultDepth            16 #Choose the depth (16||24)
    SubSection             "Display"
        Depth               16
        Modes              "1024x768_75.00" #Choose the resolution
    EndSubSection
EndSection

```

#### Несколько мониторов

##### NVIDIA

_См. [NVIDIA#Multiple monitors](/index.php/NVIDIA#Multiple_monitors "NVIDIA")_

##### Более одной видеокарты

Вы должны определить нужный драйвер для использования и поставить bus ID нужной видеокарты.

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

Чтобы узнать bus ID:

```
$ lspci | grep VGA
01:00.0 VGA compatible controller: nVidia Corporation G96 [GeForce 9600M GT] (rev a1)

```

bus ID здесь 1:0:0.

##### Скрипт для переключения внутреннего/внешнего мониторов для ноутбуков

```
#!/bin/bash

IN="LVDS1"
EXT="VGA1"

if (xrandr | grep "$EXT" | grep "+")
    then
    xrandr --output $EXT --off --output $IN --auto
    else
        if (xrandr | grep "$EXT" | grep " connected")
            then
            xrandr --output $IN --off --output $EXT --auto
        fi
fi

```

Узнать имена мониторов можно с помощью команды:

```
# xrandr -q

```

Если у вас нет `xrandr`, [установите](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.BE.D0.BF.D1.80.D0.B5.D0.B4.D0.B5.D0.BB.D0.B5.D0.BD.D0.BD.D1.8B.D1.85_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.BE.D0.B2 "Pacman (Русский)") пакет [xorg-xrandr](https://www.archlinux.org/packages/?name=xorg-xrandr).

### Размер дисплея/DPI

Для того чтобы выбрать правильный размер шрифтов, размер дисплея должен быть установлен для предпочитаемого DPI.

Сначала можно попробовать - настроить Xorg на автоопределение DPI и размеров экрана с помощью [DDC](http://en.wikipedia.org/wiki/Display_Data_Channel).
В `/etc/X11/xorg.conf` :

```
...
Section "Module"
# support for Data Display Channel. Allows to query the monitor capabilities via the video card
Load  "ddc"
# serial bus over which you speak the ddc protocol to get info from the monitor
Load "i2c"
...
Section Screen
...
DefaultColorDepth 24
SubSection "Display"
 Depth     24
 Modes "1280x1024" "1152x864" "1024x768" "800x600" "640x480"
EndSubSection
...

```

Не прописывайте Modeline и DisplaySize. Иногда это работает, если нет можно всё настроить вручную.

В секции `"Monitor"` пропишите размер дисплея в миллиметрах:

```
Section "Monitor"
   ...
 DisplaySize 336 252 # 96 DPI @ 1280x960
   ...
EndSection

```

Формула, рассчитывающая значение DisplaySize такова Ширина x 25.4 / DPI и Высота x 25.4 / DPI. Например, если вы запускаете Xorg с разрешением 1024x768 и хотите DPI, равное 96, используйте 1024 x 25.4 / 96 и 768 x 25.4 / 96\. Округлённые значения приведены ниже.

```
# calc: (x|y)pixels * 25.4 / dpi
# DisplaySize 168 126 # 96 DPI @ 640x480
# DisplaySize 210 157 # 96 DPI @ 800x600
# DisplaySize 269 201 # 96 DPI @ 1024x768
# DisplaySize 302 227 # 96 DPI @ 1152x864
# DisplaySize 336 252 # 96 DPI @ 1280x960
# DisplaySize 336 269 # 96 DPI @ 1280x1024 (соотношение сторон не 4:3)
# DisplaySize 420 315 # 96 DPI @ 1600x1200

```

Для nVidia драйверов вы, возможно, захотите отключить автоматическое определение DPI и поставить его вручную. Существует также более простой способ настройки DPI на этих картах. Любая или обе из следующих строк могут быть вставлены в секцию Device для вашей nVidia карты.

```
  Option   "UseEdidDpi" "false"
  Option   "DPI" "96 x 96"

```

Результат может быть проверен с помощью следующей команды, которая должна вернуть 96x96 точек на дюйм, если вы установили DPI на 96.

```
xdpyinfo | grep -B1 dot

```

### DPMS

DPMS (Display Power Management Signaling) — технология, позволяющая настроить энергосбережение монитора, когда компьютер не используется. Она позволит вам автоматически переключить монитор в режим ожидания через определенное время простоя. См. [DPMS](/index.php/DPMS "DPMS")

### Monitor

В зависимости от вашего оборудования, у Xorg может не получиться обнаружить верно возможности вашего монитора или же просто вы захотите использовать меньшее разрешение, чем то. которое поддерживает ваш монитор. Возможно, вы захотите посмотреть на следующие значения в руководстве вашего монитора перед их установкой. Следующие настройки указываются в секции Monitor:

#### Строчная синхронизация (horizontal sync)

```
HorizSync 28-64

```

#### Частота обновления

```
VertRefresh 60

```

### Screen

Следующие настройки указываются в секции Screen:

#### Глубина цветовой гаммы

```
Depth 24

```

#### Разрешение

```
Modes "1280x1024" "1024x768" "800x600"

```

### Шрифты

Некоторые советы по настройке шрифтов можно найти в [статье, посвящённой этому](/index.php/Xorg_Font_Configuration_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xorg Font Configuration (Русский)").

### Примеры файлов xorg.conf

**Работающий пример для видео карты GF-5200, монитор CTX, стандартные клавиатура и мышь**

```
Section "ServerLayout"
	Identifier     "Minimal layout"
	Screen         "Screen0" 0 0
EndSection

Section "Module"
	SubSection "extmod"
		Option	    "omit xfree86-dga"
	EndSubSection
EndSection

Section "Monitor"
	Identifier   "CTX VL500 series, MS500 series (120 Hz)|0"
	DisplaySize  280	210
	HorizSync    30.0 - 70.0
	VertRefresh  50.0 - 120.0
EndSection

Section "Device"
	Identifier  "Card0|0"
	Driver      "nvidia"
EndSection

Section "Screen"
	Identifier "Screen0"
	Device     "Card0|0"
	Monitor    "CTX VL500 series, MS500 series (120 Hz)|0"
	DefaultDepth     24
	SubSection "Display"
		Modes    "1024x768" "1024x736" "1024x600" "960x720" "848x480" "832x624" "800x600"  "720x576" "640x480"
	EndSubSection
EndSection

```

*   Shadowhand (nv и nvidia драйвера): [http://people.os-zen.net/shadowhand/configs/xorg.conf](http://people.os-zen.net/shadowhand/configs/xorg.conf)
*   Cerebral (fglrx и radeon драйвера): [http://www.student.cs.uwaterloo.ca/~tjwillar/configs/xorg.conf](http://www.student.cs.uwaterloo.ca/~tjwillar/configs/xorg.conf)
*   raskolnikov (via unichrome и synaptics драйвера): [http://athanatos.free.fr/Arch/xorg.conf](http://athanatos.free.fr/Arch/xorg.conf)
*   cheer (nvidia и synaptics драйвера, русская раскладка, dell 9400): [http://lice.wordpress.com/dell-9400-configuration/xorgconf/](http://lice.wordpress.com/dell-9400-configuration/xorgconf/)

## Усовершенствование загрузки X

для опций X смотрите

```
man Xserver

```

Следующие опции могут быть добавлены к переменной "defaultserverargs" в файле /usr/bin/startx.

запретить X прослушивание по tcp:

```
-nolisten tcp

```

избавиться от серого узора при загрузке X и заменить его чёрным фоном:

```
-br

```

включить задержку загрузки глифов для 16-битных шрифтов:

```
-deferglyphs 16

```

Если вы запускаете X с помощью kdm, то скрипт startx не выполняется. Эти опции могут быть добавлены к переменной "ServerCmd" в файле /opt/kde/share/config/kdm/kdmrc.

## Изменения в модульном Xorg

### Самые распространённые пакеты

**Обратите внимание:** Мета-пакет 'xorg' включает в себя самые распространённые нужные пакеты - когда вы делаете **pacman -Syu** для обновления с Xorg 6.8, он должен обновиться до этого пакета

Удостоверьтесь, что вы установили драйвера для мыши, клавиатуры и видеокарты. Для устройств ввода пакеты **xf86-input-keyboard** и **xf86-input-mouse** должны быть установлены. Дргие пакеты вида **xf86-input-*** доступны для других устройств ввода.

Что касается видеокарты, найдите, какой драйвер требуется и установите соответствующий пакет вида **xf86-video-***. Пользователи ATI и Nvidia могут установить проприетарные драйвера для своих видеокарт ( [NVIDIA](/index.php/NVIDIA_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "NVIDIA (Русский)"), [ATI](/index.php/ATI "ATI")).

Для установки всех драйверов сразу доступны пакеты **xorg-input-drivers** и **xorg-video-drivers**.

### OpenGL 3D ускорение

Xorg 7.1 в Arch Linux использует модульный вид для mesa, системы рендеринга OpenGL. Доступны некоторые реализации:

*   libgl-dri: свободная реализация DRI OpenGL. Возвращается к софтверному рендерингe, когда не установлен ни один из DRI драйверов.
*   некоторые другие, предоставляющие libGL (ati, nvidia)

Когда pacman устанавливает приложение, которому требуется mesa, он установит один из этих пакетов. Чтобы быть уверенным в установке нужной библиотеки для вашей системы, установите её до установки Xorg. Установка нужного пакета после также возможна, хотя это может иногда привести к некоторым ошибкам с зависимостями, которые можно преодолеть с помощью опции -d.

### glxgears и glxinfo

Эти приложения находятся в пакете mesa-demos.

## Tips & tricks

### Закрытие приложение по хоткею

Привяжите скрипт к хоткею:

```
#!/bin/bash
windowFocus=$(xdotool getwindowfocus);
pid=$(xprop -id $windowFocus | grep PID);
kill -9 $pid

```

Зависимости: [xorg-xprop](https://www.archlinux.org/packages/?name=xorg-xprop), [xdotool](https://www.archlinux.org/packages/?name=xdotool)

## Проблемы

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

Пользователи USB мышей должны прочитать [Get_All_Mouse_Buttons_Working](/index.php/Get_All_Mouse_Buttons_Working "Get All Mouse Buttons Working").

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

Проблема заключается в том, что некоторые раскладки (например, _sk_qwerty_, _uk_) перестали существовать. Следует заменить

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

### KDM/GDM не работают

KDM/GDM не может запуститься, так как ищет X в неверном месте.

*   **Исправления в конфигурационных файлах:** отредактируйте соответствующие конфигурационные файлы для KDM/GDM (наверное, лучшее решение).

Для GDM измените файл gdm.conf, заменив все встречающиеся упоминания /usr/X11R6/bin/X на /usr/bin/X

```
vim /opt/gnome/etc/gdm/gdm.conf

```

Команда замены для vi

```
:%s/\/usr\/X11R6\/bin\/X/\/usr\/bin\/X/g

```

Для KDM надо изменить файл /opt/kde/share/kdm/kdmrc.

*   **Метод символических ссылок:** вам надо запустить следующие команды для исправления ситуации:

```
mkdir -p /usr/X11R6/bin/
ln -s /usr/bin/X /usr/X11R6/bin/X

```

попробуйте снова, должно заработать.

Если вышеуказанная команда не сработала, попробуйте так:

```
 ln -s /usr/bin/ /usr/X11R6/bin

```

Возможно, потребуется перезагрузка.

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

## Полезные ссылки

*   [Добавление экранного менеджера входа в систему (KDM, GDM или XDM) в автозагрузку](/index.php/%D0%94%D0%BE%D0%B1%D0%B0%D0%B2%D0%BB%D0%B5%D0%BD%D0%B8%D0%B5_%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%BD%D0%BE%D0%B3%D0%BE_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80%D0%B0_%D0%B2%D1%85%D0%BE%D0%B4%D0%B0_%D0%B2_%D1%81%D0%B8%D1%81%D1%82%D0%B5%D0%BC%D1%83_(KDM,_GDM_%D0%B8%D0%BB%D0%B8_XDM)_%D0%B2_%D0%B0%D0%B2%D1%82%D0%BE%D0%B7%D0%B0%D0%B3%D1%80%D1%83%D0%B7%D0%BA%D1%83 "Добавление экранного менеджера входа в систему (KDM, GDM или XDM) в автозагрузку")
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

*   [X.org Wikipedia Article](http://en.wikipedia.org/wiki/X.Org_Server)
*   [X.org](http://wiki.x.org/wiki/)