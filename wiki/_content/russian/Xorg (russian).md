**Состояние перевода:** На этой странице представлен перевод статьи [Xorg](/index.php/Xorg "Xorg"). Дата последней синхронизации: 5 сентября 2018\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Xorg&diff=0&oldid=539938).

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
    *   [4.1 Идентификация ввода](#.D0.98.D0.B4.D0.B5.D0.BD.D1.82.D0.B8.D1.84.D0.B8.D0.BA.D0.B0.D1.86.D0.B8.D1.8F_.D0.B2.D0.B2.D0.BE.D0.B4.D0.B0)
    *   [4.2 Ускорение мыши](#.D0.A3.D1.81.D0.BA.D0.BE.D1.80.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BC.D1.8B.D1.88.D0.B8)
    *   [4.3 Дополнительные кнопки мыши](#.D0.94.D0.BE.D0.BF.D0.BE.D0.BB.D0.BD.D0.B8.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D1.8B.D0.B5_.D0.BA.D0.BD.D0.BE.D0.BF.D0.BA.D0.B8_.D0.BC.D1.8B.D1.88.D0.B8)
    *   [4.4 Тачпад](#.D0.A2.D0.B0.D1.87.D0.BF.D0.B0.D0.B4)
    *   [4.5 Тачскрин](#.D0.A2.D0.B0.D1.87.D1.81.D0.BA.D1.80.D0.B8.D0.BD)
    *   [4.6 Настройка клавиатуры](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D0.B0.D1.82.D1.83.D1.80.D1.8B)
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
    *   [7.1 Автоматизация](#.D0.90.D0.B2.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D0.B8.D0.B7.D0.B0.D1.86.D0.B8.D1.8F)
    *   [7.2 Вложенная X-сессия](#.D0.92.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.BD.D0.B0.D1.8F_X-.D1.81.D0.B5.D1.81.D1.81.D0.B8.D1.8F)
    *   [7.3 Запуск программ с GUI удаленно](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D0.BF.D1.80.D0.BE.D0.B3.D1.80.D0.B0.D0.BC.D0.BC_.D1.81_GUI_.D1.83.D0.B4.D0.B0.D0.BB.D0.B5.D0.BD.D0.BD.D0.BE)
    *   [7.4 Отключение и включение при необходимости устройств ввода](#.D0.9E.D1.82.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B8_.D0.B2.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.B8_.D0.BD.D0.B5.D0.BE.D0.B1.D1.85.D0.BE.D0.B4.D0.B8.D0.BC.D0.BE.D1.81.D1.82.D0.B8_.D1.83.D1.81.D1.82.D1.80.D0.BE.D0.B9.D1.81.D1.82.D0.B2_.D0.B2.D0.B2.D0.BE.D0.B4.D0.B0)
    *   [7.5 Закрытие приложения с помощью горячей клавиши](#.D0.97.D0.B0.D0.BA.D1.80.D1.8B.D1.82.D0.B8.D0.B5_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F_.D1.81_.D0.BF.D0.BE.D0.BC.D0.BE.D1.89.D1.8C.D1.8E_.D0.B3.D0.BE.D1.80.D1.8F.D1.87.D0.B5.D0.B9_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D1.88.D0.B8)
    *   [7.6 Блокирование доступа к TTY](#.D0.91.D0.BB.D0.BE.D0.BA.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.B4.D0.BE.D1.81.D1.82.D1.83.D0.BF.D0.B0_.D0.BA_TTY)
    *   [7.7 Запрет пользователю закрывать, перезапускать X](#.D0.97.D0.B0.D0.BF.D1.80.D0.B5.D1.82_.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D1.8E_.D0.B7.D0.B0.D0.BA.D1.80.D1.8B.D0.B2.D0.B0.D1.82.D1.8C.2C_.D0.BF.D0.B5.D1.80.D0.B5.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA.D0.B0.D1.82.D1.8C_X)
*   [8 Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [8.1 Общее](#.D0.9E.D0.B1.D1.89.D0.B5.D0.B5)
    *   [8.2 Черный экран, протокол не указан.., Ресурс временно недоступен для всех или некоторых пользователей](#.D0.A7.D0.B5.D1.80.D0.BD.D1.8B.D0.B9_.D1.8D.D0.BA.D1.80.D0.B0.D0.BD.2C_.D0.BF.D1.80.D0.BE.D1.82.D0.BE.D0.BA.D0.BE.D0.BB_.D0.BD.D0.B5_.D1.83.D0.BA.D0.B0.D0.B7.D0.B0.D0.BD...2C_.D0.A0.D0.B5.D1.81.D1.83.D1.80.D1.81_.D0.B2.D1.80.D0.B5.D0.BC.D0.B5.D0.BD.D0.BD.D0.BE_.D0.BD.D0.B5.D0.B4.D0.BE.D1.81.D1.82.D1.83.D0.BF.D0.B5.D0.BD_.D0.B4.D0.BB.D1.8F_.D0.B2.D1.81.D0.B5.D1.85_.D0.B8.D0.BB.D0.B8_.D0.BD.D0.B5.D0.BA.D0.BE.D1.82.D0.BE.D1.80.D1.8B.D1.85_.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D0.B5.D0.B9)
    *   [8.3 DRI с картами Matrox перестает работать](#DRI_.D1.81_.D0.BA.D0.B0.D1.80.D1.82.D0.B0.D0.BC.D0.B8_Matrox_.D0.BF.D0.B5.D1.80.D0.B5.D1.81.D1.82.D0.B0.D0.B5.D1.82_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.B0.D1.82.D1.8C)
    *   [8.4 Проблемы с режимом Фреймбуфер](#.D0.9F.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D1.8B_.D1.81_.D1.80.D0.B5.D0.B6.D0.B8.D0.BC.D0.BE.D0.BC_.D0.A4.D1.80.D0.B5.D0.B9.D0.BC.D0.B1.D1.83.D1.84.D0.B5.D1.80)
    *   [8.5 Программа требует "шрифт '(null)'"](#.D0.9F.D1.80.D0.BE.D0.B3.D1.80.D0.B0.D0.BC.D0.BC.D0.B0_.D1.82.D1.80.D0.B5.D0.B1.D1.83.D0.B5.D1.82_.22.D1.88.D1.80.D0.B8.D1.84.D1.82_.27.28null.29.27.22)
    *   [8.6 Восстановление: отключение Xorg перед входом в GUI](#.D0.92.D0.BE.D1.81.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5:_.D0.BE.D1.82.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_Xorg_.D0.BF.D0.B5.D1.80.D0.B5.D0.B4_.D0.B2.D1.85.D0.BE.D0.B4.D0.BE.D0.BC_.D0.B2_GUI)
    *   [8.7 Клиент X запускается с ошибкой "su"](#.D0.9A.D0.BB.D0.B8.D0.B5.D0.BD.D1.82_X_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA.D0.B0.D0.B5.D1.82.D1.81.D1.8F_.D1.81_.D0.BE.D1.88.D0.B8.D0.B1.D0.BA.D0.BE.D0.B9_.22su.22)
    *   [8.8 Не удалось запустить X: Ошибка инициализация клавиатуры](#.D0.9D.D0.B5_.D1.83.D0.B4.D0.B0.D0.BB.D0.BE.D1.81.D1.8C_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D1.82.D0.B8.D1.82.D1.8C_X:_.D0.9E.D1.88.D0.B8.D0.B1.D0.BA.D0.B0_.D0.B8.D0.BD.D0.B8.D1.86.D0.B8.D0.B0.D0.BB.D0.B8.D0.B7.D0.B0.D1.86.D0.B8.D1.8F_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D0.B0.D1.82.D1.83.D1.80.D1.8B)
    *   [8.9 Использование Xorg без прав суперпользователя](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_Xorg_.D0.B1.D0.B5.D0.B7_.D0.BF.D1.80.D0.B0.D0.B2_.D1.81.D1.83.D0.BF.D0.B5.D1.80.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D1.8F)
        *   [8.9.1 Неработающее перенаправление](#.D0.9D.D0.B5.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.B0.D1.8E.D1.89.D0.B5.D0.B5_.D0.BF.D0.B5.D1.80.D0.B5.D0.BD.D0.B0.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5)
    *   [8.10 Зеленый экран при попытке просмотра видео](#.D0.97.D0.B5.D0.BB.D0.B5.D0.BD.D1.8B.D0.B9_.D1.8D.D0.BA.D1.80.D0.B0.D0.BD_.D0.BF.D1.80.D0.B8_.D0.BF.D0.BE.D0.BF.D1.8B.D1.82.D0.BA.D0.B5_.D0.BF.D1.80.D0.BE.D1.81.D0.BC.D0.BE.D1.82.D1.80.D0.B0_.D0.B2.D0.B8.D0.B4.D0.B5.D0.BE)
    *   [8.11 Ошибка SocketCreateListener](#.D0.9E.D1.88.D0.B8.D0.B1.D0.BA.D0.B0_SocketCreateListener)
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

| Бренд | Тип | Драйвер | OpenGL | OpenGL ([multilib](/index.php/Multilib_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Multilib (Русский)")) | Документация |
| AMD/ATI | Свободный | [xf86-video-amdgpu](https://www.archlinux.org/packages/?name=xf86-video-amdgpu) | [mesa](https://www.archlinux.org/packages/?name=mesa) | [lib32-mesa](https://www.archlinux.org/packages/?name=lib32-mesa) | [AMDGPU (Русский)](/index.php/AMDGPU_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AMDGPU (Русский)") |
| [xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati) | [ATI (Русский)](/index.php/ATI_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ATI (Русский)") |
| Проприетарный | [catalyst](https://aur.archlinux.org/packages/catalyst/) | [catalyst-libgl](https://aur.archlinux.org/packages/catalyst-libgl/) | [lib32-catalyst-libgl](https://aur.archlinux.org/packages/lib32-catalyst-libgl/) | [AMD Catalyst (Русский)](/index.php/AMD_Catalyst_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AMD Catalyst (Русский)") |
| Intel | Свободный | [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) | [mesa](https://www.archlinux.org/packages/?name=mesa) | [lib32-mesa](https://www.archlinux.org/packages/?name=lib32-mesa) | [Intel graphics (Русский)](/index.php/Intel_graphics_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Intel graphics (Русский)") |
| Nvidia | Свободный | [xf86-video-nouveau](https://www.archlinux.org/packages/?name=xf86-video-nouveau) | [mesa](https://www.archlinux.org/packages/?name=mesa) | [lib32-mesa](https://www.archlinux.org/packages/?name=lib32-mesa) | [Nouveau (Русский)](/index.php/Nouveau_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Nouveau (Русский)") |
| Проприетарный | [nvidia](https://www.archlinux.org/packages/?name=nvidia) | [nvidia-utils](https://www.archlinux.org/packages/?name=nvidia-utils) | [lib32-nvidia-utils](https://www.archlinux.org/packages/?name=lib32-nvidia-utils) | [NVIDIA (Русский)](/index.php/NVIDIA_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "NVIDIA (Русский)") |
| [nvidia-390xx](https://www.archlinux.org/packages/?name=nvidia-390xx) | [nvidia-390xx-utils](https://www.archlinux.org/packages/?name=nvidia-390xx-utils) | [lib32-nvidia-390xx-utils](https://www.archlinux.org/packages/?name=lib32-nvidia-390xx-utils) |
| [nvidia-340xx](https://www.archlinux.org/packages/?name=nvidia-340xx) | [nvidia-340xx-utils](https://www.archlinux.org/packages/?name=nvidia-340xx-utils) | [lib32-nvidia-340xx-utils](https://www.archlinux.org/packages/?name=lib32-nvidia-340xx-utils) |

**Примечание:**

*   Если Вы пользуетесь ноутбуком с поддержкой NVIDIA Optimus, который использует интегрированную видеокарту вместе с дискретной видеокартой, обратитесь к статье [NVIDIA Optimus (Русский)](/index.php/NVIDIA_Optimus_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "NVIDIA Optimus (Русский)") или [Bumblebee (Русский)](/index.php/Bumblebee_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Bumblebee (Русский)").
*   Чтобы узнать доступные драйверы для графики Intel 4-го поколения и выше, смотрите статью [Intel graphics (Русский)#Установка](/index.php/Intel_graphics_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0 "Intel graphics (Русский)").

Другие видео драйверы можно найти в группе [xorg-drivers](https://www.archlinux.org/groups/x86_64/xorg-drivers/).

Во избежание проблем X следует запускать без драйверов с закрытым исходным кодом, которые обычно требуются только для расширенных возможностей, таких, как быстрый 3D рендеринг в играх. Исключением из этого правила являются недавние графические процессоры (особенно видеокарты NVIDIA), которые не поддерживаются драйверами с открытым исходным кодом.

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

**Примечание:** Arch предоставляет файлы конфигурации по умолчанию в `/usr/share/X11/xorg.conf.d/`. Большинству пользователей никакая дополнительная настройка не нужна.

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

### Идентификация ввода

Для получения дополнительной информации смотрите [Extra keyboard keys#In Xorg](/index.php/Extra_keyboard_keys#In_Xorg "Extra keyboard keys").

### Ускорение мыши

Смотрите [Mouse acceleration](/index.php/Mouse_acceleration "Mouse acceleration").

### Дополнительные кнопки мыши

Смотрите [кнопки мыши](/index.php/%D0%9A%D0%BD%D0%BE%D0%BF%D0%BA%D0%B8_%D0%BC%D1%8B%D1%88%D0%B8 "Кнопки мыши").

### Тачпад

Смотрите [libinput](/index.php/Libinput "Libinput") или [Touchpad Synaptics (Русский)](/index.php/Touchpad_Synaptics_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Touchpad Synaptics (Русский)").

### Тачскрин

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

Если у вас есть в спецификации физическое разрешение экрана, его можно ввести в конфигурационный файл Xorg так, чтобы был рассчитан правильный DPI (регулируете идентификатор для вашего вывода xrandr):

```
Section "Monitor"
    Identifier              "DVI-D-0"
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

### Автоматизация

В этом разделе перечислены утилиты для автоматизации операций с окнами (например, перемещение, изменение размера или фокусировка), ввода/вывода клавиатуры и мыши.

| Утилита | Пакет | Документация | эмуляция
клавиш | операции
с окнами | Примечание |
| xte | [xautomation](https://www.archlinux.org/packages/?name=xautomation) | [xte(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xte.1) | Да | Нет | Также содержит инструменты для очистки экрана. Не может эмулировать F13+. |
| xdo | [xdo-git](https://aur.archlinux.org/packages/xdo-git/) | [xdo(1)](https://github.com/baskerville/xdo/blob/master/doc/xdo.1.txt) | Нет | Да | Небольшая утилита X для выполнения элементарных действий над окнами. |
| xdotool | [xdotool](https://www.archlinux.org/packages/?name=xdotool) | [xdotool(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xdotool.1) | Да | Да | [Очень забагованный](https://github.com/jordansissel/xdotool/issues) и находится в неактивной разработке, например: имеет сломанный CLI parsing.[[2]](https://github.com/jordansissel/xdotool/issues/14#issuecomment-327968132)[[3]](https://github.com/jordansissel/xdotool/issues/71) |
| xvkbd | [xvkbd](https://aur.archlinux.org/packages/xvkbd/) | [xvkbd(1)](http://t-sato.in.coocan.jp/xvkbd/#option) | Да | Нет | Виртуальная клавиатура для Xorg, также имеет параметр `-text` для отправки символов. |

Также посмотрите [Clipboard#Tools](/index.php/Clipboard#Tools "Clipboard").

### Вложенная X-сессия

Для запуска вложенного сеанса другой среды рабочего стола:

```
$ /usr/bin/Xnest :1 -geometry 1024x768+0+0 -ac -name Windowmaker & wmaker -display :1

```

Это запустит сеанс Window Maker в окне 1024 на 768 в рамках текущей X-сессии.

Для этого необходим установленный пакет [xorg-server-xnest](https://www.archlinux.org/packages/?name=xorg-server-xnest).

### Запуск программ с GUI удаленно

Смотрите основную статью: [Secure Shell (Русский)#Проброс X11](/index.php/Secure_Shell_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.9F.D1.80.D0.BE.D0.B1.D1.80.D0.BE.D1.81_X11 "Secure Shell (Русский)").

### Отключение и включение при необходимости устройств ввода

С помощью *xinput* вы можете временно отключить или включить устройства ввода. Это полезно, например, на системах, имеющих несколько мышек, таких как ThinkPads и, если вам хотелось бы использовать только одну, чтобы избежать нежелательные нажатия.

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [xorg-xinput](https://www.archlinux.org/packages/?name=xorg-xinput).

Найдите имя или ID устройства, которое вы хотите отключить:

```
$ xinput

```

Например для ноутбука Lenovo ThinkPad T500 вывод выглядит следующим образом:

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

Отключить устройство можно командой `xinput --disable *устройство*`, где *устройство* это ID устройства или имя устройства, которое вы хотите отключить. В следующем примере мы отключим тачпад Synaptics с ID 10:

```
$ xinput --disable 10

```

Чтобы снова включить устройство, просто выполните противоположную команду:

```
$ xinput --enable 10

```

Так выглядит команда для выключения устройства (здесь тачпада) через его имя:

```
$ xinput --disable "SynPS/2 Synaptics TouchPad"

```

### Закрытие приложения с помощью горячей клавиши

Привяжите скрипт к горячей клавише:

```
#!/bin/bash
windowFocus=$(xdotool getwindowfocus);
pid=$(xprop -id $windowFocus | grep PID);
kill -9 $pid

```

Зависимости: [xorg-xprop](https://www.archlinux.org/packages/?name=xorg-xprop), [xdotool](https://www.archlinux.org/packages/?name=xdotool)

### Блокирование доступа к TTY

Чтобы запретить доступ к tty в X, добавьте следующее в файл [xorg.conf](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0):

```
Section "ServerFlags"
    Option "DontVTSwitch" "True"
EndSection
```

### Запрет пользователю закрывать, перезапускать X

Чтобы запретить пользователю закрывать, перезапускать запущенный Xorg, добавьте следующее в файл [xorg.conf](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0):

```
Section "ServerFlags"
    Option "DontZap"      "True"
EndSection
```

## Решение проблем

### Общее

Если произошла какая-то проблема с X, посмотрите лог (журнал), хранящийся в `/var/log/` или для пользователей без рут-доступа в `~/.local/share/xorg/` (по умолчанию с версии 1.16). Пользователям [GDM](/index.php/GDM "GDM") следует проверить журнал [systemd](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd (Русский)"). [[4]](https://bbs.archlinux.org/viewtopic.php?id=184639)

Файлы журналов имеют следующий вид `Xorg.n.log`, где `n` - номер монитора. Для одного пользовательского компьютера с настройками по умолчанию имя нужного журнала обычно `Xorg.0.log`, но для остальных оно может отличаться. Чтобы убедиться, что выбранный вами файл правильный, посмотрите временную отметку запуска сеанса X сервера и из какой консоли он был запущен. Например:

 `$ grep -e Log -e tty Xorg.0.log` 
```
[    40.623] (==) Log file: "/home/archuser/.local/share/xorg/Xorg.0.log", Time: Thu Aug 28 12:36:44 2014
[    40.704] (--) controlling tty is VT number 1, auto-enabling KeepTty
```

*   При посмотре журнала будьте внимательны к строкам начинающим с `(EE)`, которые обозначают ошибки, и к строкам - `(WW)`, которые предупреждают об возможных других проблемах.

*   Если файл `.xinitrc` *пустой* в `$HOME`, то его необходимо или удалить, или изменить для правильной загрузки X. Не сделав этого, вы получите пустой экран, а в журнале возможно `Xorg.0.log` не будет ошибок. Просто удалив его, у вас будет запускаться стандартное окружение X.
*   Если экран становиться черным, вы все еще можете попытаться переключиться на другую виртуальную консоль (например, `Ctrl+Alt+F2`), и слепо войти в систему как root. Чтобы сделать это, введите `root` (нажмите `Enter` после ввода), а потом введите пароль суперпользователя (root) (снова нажмите `Enter` после ввода).

	Вы можете попытаться завершить X сервер через:

	 `# pkill -x X` 

	Если это не сработало, просто перезагрузитесь:

	 `# reboot` 

*   Если у вас проблемы с устройствами ввода (клавиатурой, мышкой, тачпадом, и т.д.), смотрите страницы в [Category:Input devices (Русский)](/index.php/Category:Input_devices_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Category:Input devices (Русский)").
*   Смотрите также решение проблем в статьях [ATI (Русский)](/index.php/ATI_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ATI (Русский)"), [Intel graphics (Русский)](/index.php/Intel_graphics_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Intel graphics (Русский)") и [NVIDIA (Русский)](/index.php/NVIDIA_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "NVIDIA (Русский)").

### Черный экран, протокол не указан.., Ресурс временно недоступен для всех или некоторых пользователей

X создает конфигурационные и временные файлы в текущем домашнем каталоге пользователя. Убедитесь в наличии свободного места на разделе, в котором находится домашний каталог. К сожаления, X сервер в этом случае не представляет очевидную информацию о недостатке места.

### DRI с картами Matrox перестает работать

Если вы используете карту Matrox и DRI перестал работать после обновления Xorg, попробуйте добавить строку:

```
Option "OldDmaInit" "On"

```

в раздел Device, который ссылается на видео карту в `xorg.conf`.

### Проблемы с режимом Фреймбуфер

Если X не запускается со следующим сообщением в журнале,

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

[Удалите](/index.php/%D0%A3%D0%B4%D0%B0%D0%BB%D0%B8%D1%82%D0%B5 "Удалите") пакет [xf86-video-fbdev](https://www.archlinux.org/packages/?name=xf86-video-fbdev).

### Программа требует "шрифт '(null)'"

*   Сообщение об ошибке: "*unable to load font `(null)'.*"

Некоторые программы работают только с растровыми шрифтами. Имеется два крупных пакета с растровыми шрифтами [xorg-fonts-75dpi](https://www.archlinux.org/packages/?name=xorg-fonts-75dpi) и [xorg-fonts-100dpi](https://www.archlinux.org/packages/?name=xorg-fonts-100dpi). Вам не нужны оба; одного будет достаточно. Чтобы выяснить какой будет лучше в вашем случае, попробуйте утилиту `xdpyinfo` из пакета [xorg-xdpyinfo](https://www.archlinux.org/packages/?name=xorg-xdpyinfo) таким образом:

```
$ xdpyinfo | grep resolution

```

и используйте шрифт тот, у которого dpi ближе к показанному значению.

### Восстановление: отключение Xorg перед входом в GUI

Если Xorg настроен на автозапуск и по какой-то причине вам нужно предотвратить его запуск до менеджера входа/экранного менеджера (например, если ваша система неправильно настроена и Xorg не распознает ввод с помощью мыши или клавиатуры), вы можете решить эту задачу двумя способами.

*   Изменить цель по умолчанию на rescue.target. Для получения дополнительной информации смотрите [systemd (Русский)#Изменение цели загрузки по умолчанию](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.98.D0.B7.D0.BC.D0.B5.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D1.86.D0.B5.D0.BB.D0.B8_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B8_.D0.BF.D0.BE_.D1.83.D0.BC.D0.BE.D0.BB.D1.87.D0.B0.D0.BD.D0.B8.D1.8E "Systemd (Русский)").
*   Если у вас не только не исправная система, которая делает Xorg непригодным для использования, но также задержка меню GRUB установлено в ноль, или не как иначе нельзя использовать GRUB для предотвращения загрузки Xorg, вы можете использовать live CD Arch Linux. Следуйте [руководство по установке](/index.php/Installation_guide_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A4.D0.BE.D1.80.D0.BC.D0.B0.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.80.D0.B0.D0.B7.D0.B4.D0.B5.D0.BB.D0.BE.D0.B2 "Installation guide (Русский)"), где монтируется система и используется chroot в установленный Arch Linux. Кроме того, попытайтесь переключиться на другую [tty](/index.php/Tty "Tty") с помощью сочетания клавиш `Ctrl+Alt` + функциональная клавиша (обычно от `F1` до `F7` в зависимости от того, какая не используется X), войдите как root и следуйте шагам ниже.

В зависимости от настройки, вам необходимо выполнить один или более шагов:

*   [Отключите](/index.php/%D0%9E%D1%82%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D0%B5 "Отключите") [экранный менеджер](/index.php/%D0%AD%D0%BA%D1%80%D0%B0%D0%BD%D0%BD%D1%8B%D0%B9_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80 "Экранный менеджер").
*   Отключите [автозапуск X при входе в систему](/index.php/%D0%90%D0%B2%D1%82%D0%BE%D0%B7%D0%B0%D0%BF%D1%83%D1%81%D0%BA_X_%D0%BF%D1%80%D0%B8_%D0%B2%D1%85%D0%BE%D0%B4%D0%B5_%D0%B2_%D1%81%D0%B8%D1%81%D1%82%D0%B5%D0%BC%D1%83 "Автозапуск X при входе в систему").
*   Переименуйте файл `~/.xinitrc` или закомментируйте линии с `exec` в нем.

### Клиент X запускается с ошибкой "su"

Если вы получаете сообщение "Client is not authorized to connect to server" (Клиент не авторизован для подключения к серверу), попробуйте добавить строку:

```
session        optional        pam_xauth.so

```

в `/etc/pam.d/su` и `/etc/pam.d/su-l`. Затем `pam_xauth` правильно установит переменные среды и обработает ключи `xauth`.

### Не удалось запустить X: Ошибка инициализация клавиатуры

Если файловая система (в частности `/tmp`) заполнена, `startx` не запустится. В конце журнала `/var/log/Xorg.0.log` будет:

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

Освободите место на соответствующей файловой системе, и X сервер запустится.

### Использование Xorg без прав суперпользователя

Xorg может запускаться со стандартными привилегиями пользователя через [systemd-logind(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-logind.8), для получения дополнительной информации смотрите [[5]](https://fedoraproject.org/wiki/Changes/XorgWithoutRootRights) и [FS#41257](https://bugs.archlinux.org/task/41257). Для этого необходимо:

*   Запустить X через [xinit](/index.php/Xinitrc_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xinitrc (Русский)"); экранный менеджер не поддерживается
*   [KMS](/index.php/Kernel_mode_setting_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Kernel mode setting (Русский)"); реализации в проприетарных драйверах монитора не допускает [автообнаружение](http://cgit.freedesktop.org/xorg/xserver/tree/hw/xfree86/xorg-wrapper.c#n222), поэтому необходимо вручную настроить `needs_root_rights = no` в `/etc/X11/Xwrapper.config`.

Если вам не удовлетворяют эти требования, повторно включите права суперпользователя в `/etc/X11/Xwrapper.config`:

 `/etc/X11/Xwrapper.config`  `needs_root_rights = *yes*` 

Для получения дополнительной информации смотрите [Xorg.wrap(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/Xorg.wrap.1) и [systemd/User (Русский)#Xorg как служба systemd пользователь](/index.php/Systemd/User_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Xorg_.D0.BA.D0.B0.D0.BA_.D1.81.D0.BB.D1.83.D0.B6.D0.B1.D0.B0_systemd_.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D1.8C "Systemd/User (Русский)").

Также [GDM](/index.php/GDM "GDM") запускает Xorg без привилегий суперпользователя по умолчанию, когда используется [KMS](/index.php/Kernel_mode_setting_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Kernel mode setting (Русский)").

#### Неработающее перенаправление

Пока журналы пользователя Xorg хранятся в `~/.local/share/xorg/Xorg.log`, они не включают вывод X-сессии. Чтобы повторно включить перенаправление, запустите X с флагом `-keeptty`:

```
exec startx -- -keeptty > ~/.xorg.log 2>&1

```

Или скопируйте `/etc/X11/xinit/xserverrc` в `~/.xserverrc` и добавьте `-keeptty`. Для получения дополнительной информации смотрите [[6]](https://bbs.archlinux.org/viewtopic.php?pid=1446402#p1446402).

### Зеленый экран при попытке просмотра видео

У вас неправильно установлена цветовая глубина. Например, требуется 24 вместо 16.

### Ошибка SocketCreateListener

Если X завершаются с сообщением об ошибке "SocketCreateListener() failed", вам необходимо удалить файлы сокета в `/tmp/.X11-unix`. Это может происходить после того, как вы ранее запускали Xorg с правами суперпользователя (например, для создания `xorg.conf`).

## Смотрите также

*   [Xplain](https://magcius.github.io/xplain/article/) - Подробное объяснение системы X Window