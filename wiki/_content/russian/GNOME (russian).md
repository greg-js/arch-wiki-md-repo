**Состояние перевода:** На этой странице представлен перевод статьи [GNOME](/index.php/GNOME "GNOME"). Дата последней синхронизации: 2014-10-21\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=GNOME&diff=0&oldid=341064).

**GNOME** (произностися как /ɡˈnoʊm/[5] или /ˈnoʊm/[6]) - это [окружение рабочего стола](/index.php/%D0%9E%D0%BA%D1%80%D1%83%D0%B6%D0%B5%D0%BD%D0%B8%D0%B5_%D1%80%D0%B0%D0%B1%D0%BE%D1%87%D0%B5%D0%B3%D0%BE_%D1%81%D1%82%D0%BE%D0%BB%D0%B0 "Окружение рабочего стола"), которые стремится быть простым и легким в использовании. Разрабатывается в рамках [Проекта GNOME](https://en.wikipedia.org/wiki/ru:%D0%9F%D1%80%D0%BE%D0%B5%D0%BA%D1%82_GNOME "wikipedia:ru:Проект GNOME") и полностью состоит из свободного и открытого программного обеспечения. Также является частью [Проекта GNU](https://en.wikipedia.org/wiki/ru:%D0%9F%D1%80%D0%BE%D0%B5%D0%BA%D1%82_GNU "wikipedia:ru:Проект GNU").

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
    *   [1.1 Дополнительные пакеты](#.D0.94.D0.BE.D0.BF.D0.BE.D0.BB.D0.BD.D0.B8.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D1.8B.D0.B5_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D1.8B)
*   [2 Сессии GNOME](#.D0.A1.D0.B5.D1.81.D1.81.D0.B8.D0.B8_GNOME)
*   [3 Запуск GNOME](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_GNOME)
    *   [3.1 Графически](#.D0.93.D1.80.D0.B0.D1.84.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8)
    *   [3.2 Вручную](#.D0.92.D1.80.D1.83.D1.87.D0.BD.D1.83.D1.8E)
    *   [3.3 Приложения GNOME в Wayland](#.D0.9F.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F_GNOME_.D0.B2_Wayland)
*   [4 Навигация](#.D0.9D.D0.B0.D0.B2.D0.B8.D0.B3.D0.B0.D1.86.D0.B8.D1.8F)
    *   [4.1 Старые названия](#.D0.A1.D1.82.D0.B0.D1.80.D1.8B.D0.B5_.D0.BD.D0.B0.D0.B7.D0.B2.D0.B0.D0.BD.D0.B8.D1.8F)
*   [5 Конфигурация](#.D0.9A.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D1.8F)
    *   [5.1 Настройки системы](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B8_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.8B)
        *   [5.1.1 Цвет](#.D0.A6.D0.B2.D0.B5.D1.82)
        *   [5.1.2 Дата & время](#.D0.94.D0.B0.D1.82.D0.B0_.26_.D0.B2.D1.80.D0.B5.D0.BC.D1.8F)
        *   [5.1.3 Приложения по умолчанию](#.D0.9F.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F_.D0.BF.D0.BE_.D1.83.D0.BC.D0.BE.D0.BB.D1.87.D0.B0.D0.BD.D0.B8.D1.8E)
        *   [5.1.4 Мышь и тачпад](#.D0.9C.D1.8B.D1.88.D1.8C_.D0.B8_.D1.82.D0.B0.D1.87.D0.BF.D0.B0.D0.B4)
        *   [5.1.5 Сеть](#.D0.A1.D0.B5.D1.82.D1.8C)
        *   [5.1.6 Сетевые учетные записи](#.D0.A1.D0.B5.D1.82.D0.B5.D0.B2.D1.8B.D0.B5_.D1.83.D1.87.D0.B5.D1.82.D0.BD.D1.8B.D0.B5_.D0.B7.D0.B0.D0.BF.D0.B8.D1.81.D0.B8)
        *   [5.1.7 Поиск](#.D0.9F.D0.BE.D0.B8.D1.81.D0.BA)
    *   [5.2 Advanced settings](#Advanced_settings)
        *   [5.2.1 Appearance](#Appearance)
            *   [5.2.1.1 GTK+ themes and icon themes](#GTK.2B_themes_and_icon_themes)
                *   [5.2.1.1.1 Global dark theme](#Global_dark_theme)
            *   [5.2.1.2 Window manager themes](#Window_manager_themes)
                *   [5.2.1.2.1 Titlebar height](#Titlebar_height)
                *   [5.2.1.2.2 Titlebar button order](#Titlebar_button_order)
                *   [5.2.1.2.3 Hide titlebar when maximized](#Hide_titlebar_when_maximized)
            *   [5.2.1.3 GNOME Shell themes](#GNOME_Shell_themes)
            *   [5.2.1.4 Icons on menu](#Icons_on_menu)
        *   [5.2.2 Desktop](#Desktop)
            *   [5.2.2.1 Icons on the Desktop](#Icons_on_the_Desktop)
            *   [5.2.2.2 Lock screen and background](#Lock_screen_and_background)
        *   [5.2.3 Extensions](#Extensions)
        *   [5.2.4 Input methods](#Input_methods)
        *   [5.2.5 Fonts](#Fonts)
        *   [5.2.6 Startup applications](#Startup_applications)
        *   [5.2.7 Power](#Power)
            *   [5.2.7.1 Configure behaviour on lid switch close](#Configure_behaviour_on_lid_switch_close)
            *   [5.2.7.2 Change critical battery level action](#Change_critical_battery_level_action)
        *   [5.2.8 Sort applications into application (app) folders](#Sort_applications_into_application_.28app.29_folders)
*   [6 Использование оболочки](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BE.D0.B1.D0.BE.D0.BB.D0.BE.D1.87.D0.BA.D0.B8)
    *   [6.1 Шпаргалка GNOME](#.D0.A8.D0.BF.D0.B0.D1.80.D0.B3.D0.B0.D0.BB.D0.BA.D0.B0_GNOME)
    *   [6.2 Перезапуск оболочки](#.D0.9F.D0.B5.D1.80.D0.B5.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D0.BE.D0.B1.D0.BE.D0.BB.D0.BE.D1.87.D0.BA.D0.B8)
    *   [6.3 Крахи оболочки](#.D0.9A.D1.80.D0.B0.D1.85.D0.B8_.D0.BE.D0.B1.D0.BE.D0.BB.D0.BE.D1.87.D0.BA.D0.B8)
    *   [6.4 Зависания оболочки](#.D0.97.D0.B0.D0.B2.D0.B8.D1.81.D0.B0.D0.BD.D0.B8.D1.8F_.D0.BE.D0.B1.D0.BE.D0.BB.D0.BE.D1.87.D0.BA.D0.B8)
*   [7 Интеграция pacman](#.D0.98.D0.BD.D1.82.D0.B5.D0.B3.D1.80.D0.B0.D1.86.D0.B8.D1.8F_pacman)
    *   [7.1 GNOME PackageKit](#GNOME_PackageKit)
    *   [7.2 GNOME Software](#GNOME_Software)
    *   [7.3 Уведомления об обновлениях пакетов](#.D0.A3.D0.B2.D0.B5.D0.B4.D0.BE.D0.BC.D0.BB.D0.B5.D0.BD.D0.B8.D1.8F_.D0.BE.D0.B1_.D0.BE.D0.B1.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D1.8F.D1.85_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.BE.D0.B2)
*   [8 Настройка внешнего вида GNOME](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D0.B2.D0.BD.D0.B5.D1.88.D0.BD.D0.B5.D0.B3.D0.BE_.D0.B2.D0.B8.D0.B4.D0.B0_GNOME)
    *   [8.1 Темы оформления](#.D0.A2.D0.B5.D0.BC.D1.8B_.D0.BE.D1.84.D0.BE.D1.80.D0.BC.D0.BB.D0.B5.D0.BD.D0.B8.D1.8F)
    *   [8.2 gsettings и dconf](#gsettings_.D0.B8_dconf)
    *   [8.3 Верхняя панель](#.D0.92.D0.B5.D1.80.D1.85.D0.BD.D1.8F.D1.8F_.D0.BF.D0.B0.D0.BD.D0.B5.D0.BB.D1.8C)
        *   [8.3.1 Показывать дату в верхней панели](#.D0.9F.D0.BE.D0.BA.D0.B0.D0.B7.D1.8B.D0.B2.D0.B0.D1.82.D1.8C_.D0.B4.D0.B0.D1.82.D1.83_.D0.B2_.D0.B2.D0.B5.D1.80.D1.85.D0.BD.D0.B5.D0.B9_.D0.BF.D0.B0.D0.BD.D0.B5.D0.BB.D0.B8)
        *   [8.3.2 Отключить задержку при выходе из сеанса](#.D0.9E.D1.82.D0.BA.D0.BB.D1.8E.D1.87.D0.B8.D1.82.D1.8C_.D0.B7.D0.B0.D0.B4.D0.B5.D1.80.D0.B6.D0.BA.D1.83_.D0.BF.D1.80.D0.B8_.D0.B2.D1.8B.D1.85.D0.BE.D0.B4.D0.B5_.D0.B8.D0.B7_.D1.81.D0.B5.D0.B0.D0.BD.D1.81.D0.B0)
        *   [8.3.3 Показать системный монитор](#.D0.9F.D0.BE.D0.BA.D0.B0.D0.B7.D0.B0.D1.82.D1.8C_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D0.BD.D1.8B.D0.B9_.D0.BC.D0.BE.D0.BD.D0.B8.D1.82.D0.BE.D1.80)
        *   [8.3.4 Показать информацию о погоде](#.D0.9F.D0.BE.D0.BA.D0.B0.D0.B7.D0.B0.D1.82.D1.8C_.D0.B8.D0.BD.D1.84.D0.BE.D1.80.D0.BC.D0.B0.D1.86.D0.B8.D1.8E_.D0.BE_.D0.BF.D0.BE.D0.B3.D0.BE.D0.B4.D0.B5)
    *   [8.4 Обзор](#.D0.9E.D0.B1.D0.B7.D0.BE.D1.80)
        *   [8.4.1 Удаление пунктов из меню приложений](#.D0.A3.D0.B4.D0.B0.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.83.D0.BD.D0.BA.D1.82.D0.BE.D0.B2_.D0.B8.D0.B7_.D0.BC.D0.B5.D0.BD.D1.8E_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D0.B9)
        *   [8.4.2 Сортировка приложений по папкам](#.D0.A1.D0.BE.D1.80.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.BA.D0.B0_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D0.B9_.D0.BF.D0.BE_.D0.BF.D0.B0.D0.BF.D0.BA.D0.B0.D0.BC)
        *   [8.4.3 Изменение размера иконок](#.D0.98.D0.B7.D0.BC.D0.B5.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D1.80.D0.B0.D0.B7.D0.BC.D0.B5.D1.80.D0.B0_.D0.B8.D0.BA.D0.BE.D0.BD.D0.BE.D0.BA)
            *   [8.4.3.1 Для приложений в меню обзора](#.D0.94.D0.BB.D1.8F_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D0.B9_.D0.B2_.D0.BC.D0.B5.D0.BD.D1.8E_.D0.BE.D0.B1.D0.B7.D0.BE.D1.80.D0.B0)
            *   [8.4.3.2 В dash](#.D0.92_dash)
            *   [8.4.3.3 При переключении по alt-tab](#.D0.9F.D1.80.D0.B8_.D0.BF.D0.B5.D1.80.D0.B5.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B8_.D0.BF.D0.BE_alt-tab)
            *   [8.4.3.4 В системном трее](#.D0.92_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D0.BD.D0.BE.D0.BC_.D1.82.D1.80.D0.B5.D0.B5)
        *   [8.4.4 Отключение "горячего угла"](#.D0.9E.D1.82.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.22.D0.B3.D0.BE.D1.80.D1.8F.D1.87.D0.B5.D0.B3.D0.BE_.D1.83.D0.B3.D0.BB.D0.B0.22)
            *   [8.4.4.1 Меню обзора](#.D0.9C.D0.B5.D0.BD.D1.8E_.D0.BE.D0.B1.D0.B7.D0.BE.D1.80.D0.B0)
            *   [8.4.4.2 Трей сообщений](#.D0.A2.D1.80.D0.B5.D0.B9_.D1.81.D0.BE.D0.BE.D0.B1.D1.89.D0.B5.D0.BD.D0.B8.D0.B9)
    *   [8.5 Заголовок окна](#.D0.97.D0.B0.D0.B3.D0.BE.D0.BB.D0.BE.D0.B2.D0.BE.D0.BA_.D0.BE.D0.BA.D0.BD.D0.B0)
        *   [8.5.1 Уменьшение высоты заголовка окнa](#.D0.A3.D0.BC.D0.B5.D0.BD.D1.8C.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B2.D1.8B.D1.81.D0.BE.D1.82.D1.8B_.D0.B7.D0.B0.D0.B3.D0.BE.D0.BB.D0.BE.D0.B2.D0.BA.D0.B0_.D0.BE.D0.BA.D0.BDa)
        *   [8.5.2 Изменение порядка кнопок в заголовке окнa](#.D0.98.D0.B7.D0.BC.D0.B5.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D0.BE.D1.80.D1.8F.D0.B4.D0.BA.D0.B0_.D0.BA.D0.BD.D0.BE.D0.BF.D0.BE.D0.BA_.D0.B2_.D0.B7.D0.B0.D0.B3.D0.BE.D0.BB.D0.BE.D0.B2.D0.BA.D0.B5_.D0.BE.D0.BA.D0.BDa)
        *   [8.5.3 Скрытие заголовка окна при разворачивании](#.D0.A1.D0.BA.D1.80.D1.8B.D1.82.D0.B8.D0.B5_.D0.B7.D0.B0.D0.B3.D0.BE.D0.BB.D0.BE.D0.B2.D0.BA.D0.B0_.D0.BE.D0.BA.D0.BD.D0.B0_.D0.BF.D1.80.D0.B8_.D1.80.D0.B0.D0.B7.D0.B2.D0.BE.D1.80.D0.B0.D1.87.D0.B8.D0.B2.D0.B0.D0.BD.D0.B8.D0.B8)
        *   [8.5.4 Отключение анимации](#.D0.9E.D1.82.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B0.D0.BD.D0.B8.D0.BC.D0.B0.D1.86.D0.B8.D0.B8)
*   [9 Различные настройки](#.D0.A0.D0.B0.D0.B7.D0.BB.D0.B8.D1.87.D0.BD.D1.8B.D0.B5_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B8)
    *   [9.1 Управление питанием](#.D0.A3.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D0.B8.D1.82.D0.B0.D0.BD.D0.B8.D0.B5.D0.BC)
        *   [9.1.1 Выключение сна-в-ОЗУ (S3) при закрытии крышки ноутбука](#.D0.92.D1.8B.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D1.81.D0.BD.D0.B0-.D0.B2-.D0.9E.D0.97.D0.A3_.28S3.29_.D0.BF.D1.80.D0.B8_.D0.B7.D0.B0.D0.BA.D1.80.D1.8B.D1.82.D0.B8.D0.B8_.D0.BA.D1.80.D1.8B.D1.88.D0.BA.D0.B8_.D0.BD.D0.BE.D1.83.D1.82.D0.B1.D1.83.D0.BA.D0.B0)
        *   [9.1.2 Нет реакции на закрытие крышки ноутбука](#.D0.9D.D0.B5.D1.82_.D1.80.D0.B5.D0.B0.D0.BA.D1.86.D0.B8.D0.B8_.D0.BD.D0.B0_.D0.B7.D0.B0.D0.BA.D1.80.D1.8B.D1.82.D0.B8.D0.B5_.D0.BA.D1.80.D1.8B.D1.88.D0.BA.D0.B8_.D0.BD.D0.BE.D1.83.D1.82.D0.B1.D1.83.D0.BA.D0.B0)
        *   [9.1.3 Изменение действия при критическом заряде батареи (для ноутбуков)](#.D0.98.D0.B7.D0.BC.D0.B5.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B4.D0.B5.D0.B9.D1.81.D1.82.D0.B2.D0.B8.D1.8F_.D0.BF.D1.80.D0.B8_.D0.BA.D1.80.D0.B8.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.BE.D0.BC_.D0.B7.D0.B0.D1.80.D1.8F.D0.B4.D0.B5_.D0.B1.D0.B0.D1.82.D0.B0.D1.80.D0.B5.D0.B8_.28.D0.B4.D0.BB.D1.8F_.D0.BD.D0.BE.D1.83.D1.82.D0.B1.D1.83.D0.BA.D0.BE.D0.B2.29)
    *   [9.2 Возвращение назад поведения прокрутки](#.D0.92.D0.BE.D0.B7.D0.B2.D1.80.D0.B0.D1.89.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BD.D0.B0.D0.B7.D0.B0.D0.B4_.D0.BF.D0.BE.D0.B2.D0.B5.D0.B4.D0.B5.D0.BD.D0.B8.D1.8F_.D0.BF.D1.80.D0.BE.D0.BA.D1.80.D1.83.D1.82.D0.BA.D0.B8)
    *   [9.3 Автоматический запуск программ при входе в систему](#.D0.90.D0.B2.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8.D0.B9_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D0.BF.D1.80.D0.BE.D0.B3.D1.80.D0.B0.D0.BC.D0.BC_.D0.BF.D1.80.D0.B8_.D0.B2.D1.85.D0.BE.D0.B4.D0.B5_.D0.B2_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.83)
    *   [9.4 Редактирование меню приложений](#.D0.A0.D0.B5.D0.B4.D0.B0.D0.BA.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BC.D0.B5.D0.BD.D1.8E_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D0.B9)
    *   [9.5 Gnome Terminal](#Gnome_Terminal)
        *   [9.5.1 Внутренний отступ](#.D0.92.D0.BD.D1.83.D1.82.D1.80.D0.B5.D0.BD.D0.BD.D0.B8.D0.B9_.D0.BE.D1.82.D1.81.D1.82.D1.83.D0.BF)
        *   [9.5.2 Отключение мигающего курсора](#.D0.9E.D1.82.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BC.D0.B8.D0.B3.D0.B0.D1.8E.D1.89.D0.B5.D0.B3.D0.BE_.D0.BA.D1.83.D1.80.D1.81.D0.BE.D1.80.D0.B0)
        *   [9.5.3 Открытие новых вкладок в текущем каталоге (для Gnome Terminal 3.8+)](#.D0.9E.D1.82.D0.BA.D1.80.D1.8B.D1.82.D0.B8.D0.B5_.D0.BD.D0.BE.D0.B2.D1.8B.D1.85_.D0.B2.D0.BA.D0.BB.D0.B0.D0.B4.D0.BE.D0.BA_.D0.B2_.D1.82.D0.B5.D0.BA.D1.83.D1.89.D0.B5.D0.BC_.D0.BA.D0.B0.D1.82.D0.B0.D0.BB.D0.BE.D0.B3.D0.B5_.28.D0.B4.D0.BB.D1.8F_Gnome_Terminal_3.8.2B.29)
    *   [9.6 Перемещение диалоговых окон](#.D0.9F.D0.B5.D1.80.D0.B5.D0.BC.D0.B5.D1.89.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B4.D0.B8.D0.B0.D0.BB.D0.BE.D0.B3.D0.BE.D0.B2.D1.8B.D1.85_.D0.BE.D0.BA.D0.BE.D0.BD)
    *   [9.7 Расширения GNOME shell](#.D0.A0.D0.B0.D1.81.D1.88.D0.B8.D1.80.D0.B5.D0.BD.D0.B8.D1.8F_GNOME_shell)
    *   [9.8 Приложения по умолчанию](#.D0.9F.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F_.D0.BF.D0.BE_.D1.83.D0.BC.D0.BE.D0.BB.D1.87.D0.B0.D0.BD.D0.B8.D1.8E_2)
        *   [9.8.1 Файловый менеджер/замена Files](#.D0.A4.D0.B0.D0.B9.D0.BB.D0.BE.D0.B2.D1.8B.D0.B9_.D0.BC.D0.B5.D0.BD.D0.B5.D0.B4.D0.B6.D0.B5.D1.80.2F.D0.B7.D0.B0.D0.BC.D0.B5.D0.BD.D0.B0_Files)
        *   [9.8.2 Программа просмотра PDF](#.D0.9F.D1.80.D0.BE.D0.B3.D1.80.D0.B0.D0.BC.D0.BC.D0.B0_.D0.BF.D1.80.D0.BE.D1.81.D0.BC.D0.BE.D1.82.D1.80.D0.B0_PDF)
    *   [9.9 Средняя кнопка мыши](#.D0.A1.D1.80.D0.B5.D0.B4.D0.BD.D1.8F.D1.8F_.D0.BA.D0.BD.D0.BE.D0.BF.D0.BA.D0.B0_.D0.BC.D1.8B.D1.88.D0.B8)
    *   [9.10 Затемнение экрана](#.D0.97.D0.B0.D1.82.D0.B5.D0.BC.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D1.8D.D0.BA.D1.80.D0.B0.D0.BD.D0.B0)
    *   [9.11 Настройка горячих клавиш](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D0.B3.D0.BE.D1.80.D1.8F.D1.87.D0.B8.D1.85_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D1.88)
        *   [9.11.1 Files 3.4 и старше](#Files_3.4_.D0.B8_.D1.81.D1.82.D0.B0.D1.80.D1.88.D0.B5)
    *   [9.12 Запись экрана (screencast)](#.D0.97.D0.B0.D0.BF.D0.B8.D1.81.D1.8C_.D1.8D.D0.BA.D1.80.D0.B0.D0.BD.D0.B0_.28screencast.29)
    *   [9.13 Настройка клавиатуры при помощи XkbOptions](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D0.B0.D1.82.D1.83.D1.80.D1.8B_.D0.BF.D1.80.D0.B8_.D0.BF.D0.BE.D0.BC.D0.BE.D1.89.D0.B8_XkbOptions)
    *   [9.14 Включение раскладок клавиатуры](#.D0.92.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D1.80.D0.B0.D1.81.D0.BA.D0.BB.D0.B0.D0.B4.D0.BE.D0.BA_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D0.B0.D1.82.D1.83.D1.80.D1.8B)
    *   [9.15 Поддержка экранов HiDPI (Retina)](#.D0.9F.D0.BE.D0.B4.D0.B4.D0.B5.D1.80.D0.B6.D0.BA.D0.B0_.D1.8D.D0.BA.D1.80.D0.B0.D0.BD.D0.BE.D0.B2_HiDPI_.28Retina.29)
    *   [9.16 Другие советы](#.D0.94.D1.80.D1.83.D0.B3.D0.B8.D0.B5_.D1.81.D0.BE.D0.B2.D0.B5.D1.82.D1.8B)
*   [10 Tracker (программа поиска)](#Tracker_.28.D0.BF.D1.80.D0.BE.D0.B3.D1.80.D0.B0.D0.BC.D0.BC.D0.B0_.D0.BF.D0.BE.D0.B8.D1.81.D0.BA.D0.B0.29)
*   [11 Totem (видео проигрыватель)](#Totem_.28.D0.B2.D0.B8.D0.B4.D0.B5.D0.BE_.D0.BF.D1.80.D0.BE.D0.B8.D0.B3.D1.80.D1.8B.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D1.8C.29)
*   [12 Empathy (встроенная система обмена мгновенными сообщениями) и GNOME Online Accounts](#Empathy_.28.D0.B2.D1.81.D1.82.D1.80.D0.BE.D0.B5.D0.BD.D0.BD.D0.B0.D1.8F_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D0.B0_.D0.BE.D0.B1.D0.BC.D0.B5.D0.BD.D0.B0_.D0.BC.D0.B3.D0.BD.D0.BE.D0.B2.D0.B5.D0.BD.D0.BD.D1.8B.D0.BC.D0.B8_.D1.81.D0.BE.D0.BE.D0.B1.D1.89.D0.B5.D0.BD.D0.B8.D1.8F.D0.BC.D0.B8.29_.D0.B8_GNOME_Online_Accounts)
*   [13 Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [13.1 Невозможно изменить настройки в dconf-editor](#.D0.9D.D0.B5.D0.B2.D0.BE.D0.B7.D0.BC.D0.BE.D0.B6.D0.BD.D0.BE_.D0.B8.D0.B7.D0.BC.D0.B5.D0.BD.D0.B8.D1.82.D1.8C_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B8_.D0.B2_dconf-editor)
    *   [13.2 Расширения](#.D0.A0.D0.B0.D1.81.D1.88.D0.B8.D1.80.D0.B5.D0.BD.D0.B8.D1.8F)
        *   [13.2.1 Когда расширение рушит GNOME](#.D0.9A.D0.BE.D0.B3.D0.B4.D0.B0_.D1.80.D0.B0.D1.81.D1.88.D0.B8.D1.80.D0.B5.D0.BD.D0.B8.D0.B5_.D1.80.D1.83.D1.88.D0.B8.D1.82_GNOME)
        *   [13.2.2 Расширения не работают после обновления GNOME 3](#.D0.A0.D0.B0.D1.81.D1.88.D0.B8.D1.80.D0.B5.D0.BD.D0.B8.D1.8F_.D0.BD.D0.B5_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.B0.D1.8E.D1.82_.D0.BF.D0.BE.D1.81.D0.BB.D0.B5_.D0.BE.D0.B1.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D1.8F_GNOME_3)
        *   [13.2.3 Удаление расширений Gnome Shell](#.D0.A3.D0.B4.D0.B0.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D1.80.D0.B0.D1.81.D1.88.D0.B8.D1.80.D0.B5.D0.BD.D0.B8.D0.B9_Gnome_Shell)
    *   [13.3 Клавиша "Windows"](#.D0.9A.D0.BB.D0.B0.D0.B2.D0.B8.D1.88.D0.B0_.22Windows.22)
    *   [13.4 Горячие клавиши не работают, когда запущен только conky](#.D0.93.D0.BE.D1.80.D1.8F.D1.87.D0.B8.D0.B5_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D1.88.D0.B8_.D0.BD.D0.B5_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.B0.D1.8E.D1.82.2C_.D0.BA.D0.BE.D0.B3.D0.B4.D0.B0_.D0.B7.D0.B0.D0.BF.D1.83.D1.89.D0.B5.D0.BD_.D1.82.D0.BE.D0.BB.D1.8C.D0.BA.D0.BE_conky)
    *   [13.5 Окно открывается позади других окон при использовании нескольких мониторов](#.D0.9E.D0.BA.D0.BD.D0.BE_.D0.BE.D1.82.D0.BA.D1.80.D1.8B.D0.B2.D0.B0.D0.B5.D1.82.D1.81.D1.8F_.D0.BF.D0.BE.D0.B7.D0.B0.D0.B4.D0.B8_.D0.B4.D1.80.D1.83.D0.B3.D0.B8.D1.85_.D0.BE.D0.BA.D0.BE.D0.BD_.D0.BF.D1.80.D0.B8_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B8_.D0.BD.D0.B5.D1.81.D0.BA.D0.BE.D0.BB.D1.8C.D0.BA.D0.B8.D1.85_.D0.BC.D0.BE.D0.BD.D0.B8.D1.82.D0.BE.D1.80.D0.BE.D0.B2)
    *   [13.6 Несколько мониторов и расширение dock](#.D0.9D.D0.B5.D1.81.D0.BA.D0.BE.D0.BB.D1.8C.D0.BA.D0.BE_.D0.BC.D0.BE.D0.BD.D0.B8.D1.82.D0.BE.D1.80.D0.BE.D0.B2_.D0.B8_.D1.80.D0.B0.D1.81.D1.88.D0.B8.D1.80.D0.B5.D0.BD.D0.B8.D0.B5_dock)
    *   [13.7 Горячие клавиши "Показать рабочий стол" не работают](#.D0.93.D0.BE.D1.80.D1.8F.D1.87.D0.B8.D0.B5_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D1.88.D0.B8_.22.D0.9F.D0.BE.D0.BA.D0.B0.D0.B7.D0.B0.D1.82.D1.8C_.D1.80.D0.B0.D0.B1.D0.BE.D1.87.D0.B8.D0.B9_.D1.81.D1.82.D0.BE.D0.BB.22_.D0.BD.D0.B5_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.B0.D1.8E.D1.82)
    *   [13.8 Невозможно применить сохранённую конфигурация мониторов](#.D0.9D.D0.B5.D0.B2.D0.BE.D0.B7.D0.BC.D0.BE.D0.B6.D0.BD.D0.BE_.D0.BF.D1.80.D0.B8.D0.BC.D0.B5.D0.BD.D0.B8.D1.82.D1.8C_.D1.81.D0.BE.D1.85.D1.80.D0.B0.D0.BD.D1.91.D0.BD.D0.BD.D1.83.D1.8E_.D0.BA.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D1.8F_.D0.BC.D0.BE.D0.BD.D0.B8.D1.82.D0.BE.D1.80.D0.BE.D0.B2)
    *   [13.9 Кнопка блокировки не может вновь включить тачпад](#.D0.9A.D0.BD.D0.BE.D0.BF.D0.BA.D0.B0_.D0.B1.D0.BB.D0.BE.D0.BA.D0.B8.D1.80.D0.BE.D0.B2.D0.BA.D0.B8_.D0.BD.D0.B5_.D0.BC.D0.BE.D0.B6.D0.B5.D1.82_.D0.B2.D0.BD.D0.BE.D0.B2.D1.8C_.D0.B2.D0.BA.D0.BB.D1.8E.D1.87.D0.B8.D1.82.D1.8C_.D1.82.D0.B0.D1.87.D0.BF.D0.B0.D0.B4)
    *   [13.10 GNOME использует курсор Х11](#GNOME_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D1.83.D0.B5.D1.82_.D0.BA.D1.83.D1.80.D1.81.D0.BE.D1.80_.D0.A511)
    *   [13.11 Tracker и Документы не видят любые локальные файлы](#Tracker_.D0.B8_.D0.94.D0.BE.D0.BA.D1.83.D0.BC.D0.B5.D0.BD.D1.82.D1.8B_.D0.BD.D0.B5_.D0.B2.D0.B8.D0.B4.D1.8F.D1.82_.D0.BB.D1.8E.D0.B1.D1.8B.D0.B5_.D0.BB.D0.BE.D0.BA.D0.B0.D0.BB.D1.8C.D0.BD.D1.8B.D0.B5_.D1.84.D0.B0.D0.B9.D0.BB.D1.8B)
    *   [13.12 Не запоминаются пароли](#.D0.9D.D0.B5_.D0.B7.D0.B0.D0.BF.D0.BE.D0.BC.D0.B8.D0.BD.D0.B0.D1.8E.D1.82.D1.81.D1.8F_.D0.BF.D0.B0.D1.80.D0.BE.D0.BB.D0.B8)
    *   [13.13 Невозможно перетаскивать окна с помощью Alt-Key + кнопка мыши](#.D0.9D.D0.B5.D0.B2.D0.BE.D0.B7.D0.BC.D0.BE.D0.B6.D0.BD.D0.BE_.D0.BF.D0.B5.D1.80.D0.B5.D1.82.D0.B0.D1.81.D0.BA.D0.B8.D0.B2.D0.B0.D1.82.D1.8C_.D0.BE.D0.BA.D0.BD.D0.B0_.D1.81_.D0.BF.D0.BE.D0.BC.D0.BE.D1.89.D1.8C.D1.8E_Alt-Key_.2B_.D0.BA.D0.BD.D0.BE.D0.BF.D0.BA.D0.B0_.D0.BC.D1.8B.D1.88.D0.B8)
    *   [13.14 Gnome-shell 3.8.x не загружается, появляются лишь черный экран и курсор](#Gnome-shell_3.8.x_.D0.BD.D0.B5_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B6.D0.B0.D0.B5.D1.82.D1.81.D1.8F.2C_.D0.BF.D0.BE.D1.8F.D0.B2.D0.BB.D1.8F.D1.8E.D1.82.D1.81.D1.8F_.D0.BB.D0.B8.D1.88.D1.8C_.D1.87.D0.B5.D1.80.D0.BD.D1.8B.D0.B9_.D1.8D.D0.BA.D1.80.D0.B0.D0.BD_.D0.B8_.D0.BA.D1.83.D1.80.D1.81.D0.BE.D1.80)
    *   [13.15 Видео tear-free с графикой Intel HD](#.D0.92.D0.B8.D0.B4.D0.B5.D0.BE_tear-free_.D1.81_.D0.B3.D1.80.D0.B0.D1.84.D0.B8.D0.BA.D0.BE.D0.B9_Intel_HD)
    *   [13.16 Вход в систему при помощи GDM или lightdm быстро возвращает экран входа в систему без какой-либо реакции](#.D0.92.D1.85.D0.BE.D0.B4_.D0.B2_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.83_.D0.BF.D1.80.D0.B8_.D0.BF.D0.BE.D0.BC.D0.BE.D1.89.D0.B8_GDM_.D0.B8.D0.BB.D0.B8_lightdm_.D0.B1.D1.8B.D1.81.D1.82.D1.80.D0.BE_.D0.B2.D0.BE.D0.B7.D0.B2.D1.80.D0.B0.D1.89.D0.B0.D0.B5.D1.82_.D1.8D.D0.BA.D1.80.D0.B0.D0.BD_.D0.B2.D1.85.D0.BE.D0.B4.D0.B0_.D0.B2_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.83_.D0.B1.D0.B5.D0.B7_.D0.BA.D0.B0.D0.BA.D0.BE.D0.B9-.D0.BB.D0.B8.D0.B1.D0.BE_.D1.80.D0.B5.D0.B0.D0.BA.D1.86.D0.B8.D0.B8)
    *   [13.17 Системные иконки Gnome не подгружаются корректно](#.D0.A1.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D0.BD.D1.8B.D0.B5_.D0.B8.D0.BA.D0.BE.D0.BD.D0.BA.D0.B8_Gnome_.D0.BD.D0.B5_.D0.BF.D0.BE.D0.B4.D0.B3.D1.80.D1.83.D0.B6.D0.B0.D1.8E.D1.82.D1.81.D1.8F_.D0.BA.D0.BE.D1.80.D1.80.D0.B5.D0.BA.D1.82.D0.BD.D0.BE)
    *   [13.18 Искажения при разворачивании окон на весь экран](#.D0.98.D1.81.D0.BA.D0.B0.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F_.D0.BF.D1.80.D0.B8_.D1.80.D0.B0.D0.B7.D0.B2.D0.BE.D1.80.D0.B0.D1.87.D0.B8.D0.B2.D0.B0.D0.BD.D0.B8.D0.B8_.D0.BE.D0.BA.D0.BE.D0.BD_.D0.BD.D0.B0_.D0.B2.D0.B5.D1.81.D1.8C_.D1.8D.D0.BA.D1.80.D0.B0.D0.BD)
*   [14 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Установка

Доступны две группы:

*   [gnome](https://www.archlinux.org/groups/x86_64/gnome/) содержит основное рабочее окружение и набор хорошо интегрированных [приложений](https://wiki.gnome.org/Apps);
*   [gnome-extra](https://www.archlinux.org/groups/x86_64/gnome-extra/) включает в себя дополнительные приложения GNOME, такие как архиватор, диспетчер дисков, текстовый редактор и набор игр. Обратите внимание, что эта группа опирается на группу [gnome](https://www.archlinux.org/groups/x86_64/gnome/).

Базовый рабочий стол состоит из GNOME Shell, плагина для оконного менеджера Mutter. Может быть установлен отдельным пакетом [gnome-shell](https://www.archlinux.org/packages/?name=gnome-shell)

**Примечание:** *mutter* выступает в роли композитного менеджера, используя аппаратное графическое ускорение для предоставления эффектов, направленных на снижение беспорядка на экране. Менеджер сессий GNOME автоматически определяет, способен ли ваш драйвер видеокарты работать с GNOME Shell, и, если нет, возвращается к использованию программного рендеринга с использованием *llvmpipe*.

### Дополнительные пакеты

Пакеты, отсутствующие во всех вышеперечисленных группах:

*   **[Boxes](https://en.wikipedia.org/wiki/GNOME_Boxes "wikipedia:GNOME Boxes")** — Простой пользовательский интерфейс для получения доступа к виртуальным машинам [libvirt](/index.php/Libvirt "Libvirt").

	[https://wiki.gnome.org/Apps/Boxes](https://wiki.gnome.org/Apps/Boxes) || [gnome-boxes](https://www.archlinux.org/packages/?name=gnome-boxes)

*   **GNOME Initial Setup** — Простой, легкий и безопасный способ "подготовки" новой системы.

	[https://github.com/GNOME/gnome-initial-setup](https://github.com/GNOME/gnome-initial-setup) || [gnome-initial-setup](https://www.archlinux.org/packages/?name=gnome-initial-setup)

*   **GNOME PackageKit** — Коллекция графических инструментов для PackageKit, которые хорошо вписываются в окружение GNOME.

	[https://github.com/GNOME/gnome-packagekit](https://github.com/GNOME/gnome-packagekit) || [gnome-packagekit](https://www.archlinux.org/packages/?name=gnome-packagekit)

*   **[Software](https://en.wikipedia.org/wiki/GNOME_Software "wikipedia:GNOME Software")** — Позволяет вам устанавливать и обновлять приложения и системные расширения.

	[https://wiki.gnome.org/Apps/Software/](https://wiki.gnome.org/Apps/Software/) || [gnome-software](https://www.archlinux.org/packages/?name=gnome-software)

## Сессии GNOME

В GNOME 3 имеется *три* доступных режима:

*   **GNOME** - запускает GNOME Shell, используя новый протокол Wayland, а также привычные приложения X посредством Xwayland
*   **GNOME Classic** - традиционный рабочий стол, похожий на пользовательский интерфейс GNOME 2, но использующий технологии GNOME 3\. Это достигается за счет использования предустановленных расширений и настроек (смотрите [здесь](http://worldofgnome.org/welcome-to-gnome-3-8-flintstones-mode/), чтобы увидеть список). Следовательно, это более "настроенный", чем первый, режим GNOME Shell
*   **GNOME on Xorg** - запускает GNOME Shell, используя Xorg

## Запуск GNOME

GNOME может быть запущен как графически, используя [экранный менеджер](/index.php/%D0%AD%D0%BA%D1%80%D0%B0%D0%BD%D0%BD%D1%8B%D0%B9_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80 "Экранный менеджер"), так и вручную из консоли. Рекомендуется использовать [GDM](/index.php/GDM "GDM") (the GNOME Display manager) для лучшей интеграции с системой. Обратите внимание, что [включение](/index.php/%D0%92%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D1%8C "Включить") экранного менеджера (такого как GDM) означает то, что Xorg будет запускаться с правами суперпользователя.

**Примечание:** Поддержка механизмов блокировки экрана в GNOME обеспечивается GDM. Если запускать GNOME не при помощи GDM, то вам придется использовать другой блокировщик экрана. Смотрите [List of applications/Security#Screen lockers](/index.php/List_of_applications/Security#Screen_lockers "List of applications/Security").

### Графически

В меню экранного менеджера выберите *GNOME*, *GNOME Classic* или *GNOME on Xorg*.

### Вручную

*   Для запуска сессии GNOME on Xorg добавьте следующее в файл `~/.xinitrc`: `exec gnome-session`.
*   Для запуска сессии GNOME Classic добавьте следующее в файл `~/.xinitrc`:
    ```
    export XDG_CURRENT_DESKTOP=GNOME-Classic:GNOME
    export GNOME_SHELL_SESSION_MODE=classic
    exec gnome-session --session=gnome-classic
    ```

После редактирования файла `~/.xinitrc` GNOME можно запустить при помощи команды `startx` (для получения информации о других возможностях, например, сохранении сессии logind, смотрите статью [xinitrc](/index.php/Xinitrc "Xinitrc")). После настройки вашего файла `~/.xinitrc` также можете использовать инструкции из статьи [Запуск Х при входе в систему](/index.php/Start_X_at_login_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Start X at login (Русский)") с тем, чтобы вам не надо было выполнять команду `startx` вручную.

**Примечание:** Для работы GNOME on Wayland требуется пакет [xorg-server-xwayland](https://www.archlinux.org/packages/?name=xorg-server-xwayland). Эта сессия не может быть запущена посредством *startx* и `~/.xinitrc`. Вместо этого просто запустите `gnome-session`. Больше информации в статье [Wayland](/index.php/Wayland "Wayland")

### Приложения GNOME в Wayland

Когда используется сессия *GNOME*, соответствующие приложения будут запущены используя Wayland. Смотрите текущий статус Wayland для приложений GNOME [здесь](https://wiki.gnome.org/Initiatives/Wayland/Applications/).

## Навигация

Чтобы понять, как использовать GNOME эффективно, прочитайте [шпаргалку GNOME Shell](https://wiki.gnome.org/Projects/GnomeShell/CheatSheet); в ней освещаются особенности, которые включают в себя переключение между задачами, использование клавиатуры, контроль окон, панель, обзор, оболочки GNOME и горячие клавиши. Вот некоторые из них:

*   `Super` + `m`: показать трей с сообщениями
*   `Super` + `a`: показать меню приложений
*   `Alt-` + `Tab`: переключение между активными приложениями
*   `Alt-` + ``` (клавиша выше `Tab` на раскладке клавиатуры США): переключение между окнами активного приложения
*   `Alt` + `F2`, затем введите `r` или `restart`: перезапуск оболочки ввиду графических проблем (только для режима X/legacy. Недоступно для Wayland).

### Старые названия

**Примечание:** Некоторые программы GNOME претерпели изменения имен, где имя приложения в документации, диалоговых окнах изменено, а имя исполняемого файла - нет. Несколько таких приложений перечислено в таблице ниже.

**Совет:** Поиск по старому названию успешно найдет требуемое приложение. Например, если искать *nautilus*, то выдаст *Files*.

| Текущее | Старое |
| [Files](/index.php/Files "Files") | Nautilus |
| [Web](/index.php/GNOME_Web "GNOME Web") | Epiphany |
| Videos | Totem |
| Main Menu | Alacarte |
| Document Viewer | Evince |
| Disk Usage Analyser | Baobab |
| Image Viewer | EoG (Eye of GNOME) |
| [Passwords and Keys](/index.php/GNOME_Keyring "GNOME Keyring") | Seahorse |

## Конфигурация

GNOME использует для сохранения настроек системы и приложений DConf - хранилище данных. Рабочий стол поставляется с настройками по умолчанию, установленными приложениями и их собственными базами данных. Базовая конфигурация производится при помощи параметров системы GNOME (*gnome-control-center*) или настройки отдельных приложений. Можно всегда напрямую изменить базу данных DConf; это выполняется при помощи инструмента командной строки *gsettings*. В частности его можно использовать, чтобы настроить параметры, которые не доступны через пользовательский интерфейс.

Настройки GNOME применяются GNOME Settings Daemon. Обратите внимание, что демон может быть запущен вне сессии GNOME, чтобы применить настройки GNOME вне родной среды. Выполните `nohup /usr/lib/gnome-settings-daemon/gnome-settings-daemon > /dev/null &`.

Конфигурация обычно производится отдельно для каждого пользователя и остальная часть этого раздела не приводит примеры того, как создать конфигурацию для нескольких пользователей одновременно.

### Настройки системы

Заметки о настройках панели управления.

#### Цвет

Демон `colord` считывает данные EDID дисплея и извлекает соответствующий цветовой профиль. Большинство цветовых профилей являются правильными и не требуют настройки; однако для тех, которые не являются правильными или для старых дисплеев, цветовые профили могут быть помещены в `~/.local/share/icc/` и направлены туда же.

#### Дата & время

Если в системе настроен [Network Time Protocol daemon](/index.php/Network_Time_Protocol_daemon "Network Time Protocol daemon"), он будет также эффективно работать и для GNOME. Синхронизация может быть установлена на ручной контроль из меню, если требуется.

Чтобы показать дату в верхней панели, выполните:

```
$ gsettings set org.gnome.desktop.interface clock-show-date true

```

Кроме того, чтобы показывать номера недель в календаре, отрытом в верхней панели, выполните:

```
$ gsettings set org.gnome.desktop.calendar show-weekdate true

```

#### Приложения по умолчанию

После установки GNOME в первый раз, вы можете обнаружить, что неправильные приложения обрабатывают определенные протоколы. Например, *totem* открывает видео вместо ранее использованного [VLC](/index.php/VLC "VLC"). Некоторые ассоциации могут быть установлены с помощью системных настроек: *Все параметры* > *Подробности* > *Приложения по умолчанию*.

Для других протоколов и методах их конфигурации смотрите [Default applications](/index.php/Default_applications "Default applications").

#### Мышь и тачпад

Для того чтобы уменьшить неудобства, доставляемые тачпадом, вам, возможно, захочется реализовать следующее:

*   Отключение тачпада во время набора текста
*   Отключение прокрутки
*   Отключение tap-to-click

**Примечание:** Драйвер [synaptics](/index.php/Synaptics "Synaptics") не поддерживается GNOME. Вместо него вы должны использовать [libinput](/index.php/Libinput "Libinput"). Смотрите [этот отчет об ошибке](https://bugzilla.gnome.org/show_bug.cgi?id=764257#c12).

#### Сеть

[NetworkManager](/index.php/NetworkManager "NetworkManager") - родной инструмент проекта GNOME для контроля настроек сети. По умолчанию он устанавливается как зависимость пакета [tracker](https://www.archlinux.org/packages/?name=tracker), который является частью группы [gnome](https://www.archlinux.org/groups/x86_64/gnome/), и нужно просто [включить](/index.php/NetworkManager#Enable_NetworkManager "NetworkManager") его.

В отличие от других [менеджеров сети](/index.php/List_of_applications/Internet#Network_managers "List of applications/Internet"), которые могут быть также использованы, NetworkManager обеспечивает полную интеграцию через настройки сети оболочки и предоставляет апплет индикатора статуса [network-manager-applet](https://www.archlinux.org/packages/?name=network-manager-applet) (не требуется для GNOME).

#### Сетевые учетные записи

Бекенды для приложения обмена сообщениями GNOME [empathy](https://www.archlinux.org/packages/?name=empathy) и для Сетевых учетных записей GNOME, которые располагаются в Параметрах системы, находятся в отдельной группе: [telepathy](https://www.archlinux.org/groups/x86_64/telepathy/). Смотрите [не удается добавить аккаунты в Empathy и Сетевые учетные записи GNOME](/index.php/GNOME/Troubleshooting#Unable_to_add_accounts_in_Empathy_and_GNOME_Online_Accounts "GNOME/Troubleshooting"). Некоторые сетевые учетные записи, такие как [ownCloud](/index.php/OwnCloud "OwnCloud"), требуют установки [gvfs-goa](https://www.archlinux.org/packages/?name=gvfs-goa) для полной работоспособности в приложениях GNOME, таких как [GNOME Files](/index.php/GNOME_Files "GNOME Files") и GNOME Documents [[1]](https://wiki.gnome.org/ThreePointSeven/Features/Owncloud).

#### Поиск

В GNOME встроен поиск, доступ к которому можно получить используя клавишу `Super`. Пакет [tracker](https://www.archlinux.org/packages/?name=tracker) устанавливается по умолчанию как часть группы [gnome](https://www.archlinux.org/groups/x86_64/gnome/), индексирует приложения и базы метаданных. Настраивается при помощи *Поиск и индексация*; мониторинг состояния посредством *tracker-control*. Автоматически запускается *gnome-session*, когда пользователь входит в систему. Можно запустить вручную: `tracker-control -s`. Параметры поиска также могут быть настроены из панели *Все параметры*.

Отправлять запросы базе данных Tracker можно при помощи *tracker-sparql*. Смотрите страницу справочного руководства `man tracker-sparql`.

### Advanced settings

As noted above, many configuration options such as changing the [GTK+](/index.php/GTK%2B "GTK+") theme or the [window manager](/index.php/Window_manager "Window manager") theme are not exposed in the GNOME System Settings panel (*gnome-control-center*). Those users that want to configure these settings may wish to use the GNOME Tweak Tool ([gnome-tweak-tool](https://www.archlinux.org/packages/?name=gnome-tweak-tool)), a convenient graphical tool which exposes many of these settings.

GNOME settings (which are stored in the DConf database) can also be configured using the [*dconf-editor*](https://developer.gnome.org/dconf/unstable/dconf-editor.html) (a graphical DConf configuration tool) or the [*gsettings*](https://developer.gnome.org/gio/stable/GSettings.html) command line tool. The GNOME Tweak Tool does not do anything else in the background of the GUI; note though that you will not find all settings described in the following sections in it.

#### Appearance

##### GTK+ themes and icon themes

To install a new theme or icon set, add the relevant `~/.local/share/themes` or `~/.local/share/icons` respectively (add to `/usr/share/` instead of `~/.local/share/` for the themes to be available systemwide.) They and other GUI settings can also be defined in `~/.config/gtk-3.0/settings.ini`:

 `~/.config/gtk-3.0/settings.ini` 
```
[Settings]
gtk-theme-name = Adwaita
# next option is applicable only if selected theme supports it
gtk-application-prefer-dark-theme = true
# set font name and dimension
gtk-font-name = Sans 10

```

Additional theme locations:

*   [DeviantArt](http://www.deviantart.com/browse/all/customization/skins/linuxutil/desktopenv/gnome/gtk3/).
*   [gnome-look.org](http://gnome-look.org/index.php?xcontentmode=167).
*   [GTK+ 3 themes in the AUR](https://aur.archlinux.org/packages.php?O=0&K=gtk3&do_Search=Go).
*   [Cursor themes in the AUR](https://aur.archlinux.org/packages.php?O=0&K=xcursor&do_Search=Go&PP=50&SB=v&SO=d).
*   [Icon themes in the AUR](https://aur.archlinux.org/packages.php?O=0&K=icon-theme&do_Search=Go&PP=50&SB=v&SO=d).

Once installed, they can be selected using the GNOME Tweak Tool or GSettings - see below for GSettings commands:

For the GTK+ theme:

```
$ gsettings set org.gnome.desktop.interface gtk-theme *theme-name*

```

For the icon theme

```
$ gsettings set org.gnome.desktop.interface icon-theme *theme-name*

```

###### Global dark theme

GNOME will use the Adwaita light theme by default however a dark variant of this theme (called the Global Dark Theme) also exists and can be selected using the Tweak Tool or by editing the GTK+ 3 settings file - see [GTK+#Dark theme variant](/index.php/GTK%2B#Dark_theme_variant "GTK+"). Some applications such as Image Viewer (*eog*) use the dark theme by default. It should be noted that the Global Dark Theme only works with GTK+ 3 applications; some GTK+ 3 applications may only have partial support for the Global Dark theme. Qt and GTK+ 2 support for the Global Dark Theme may be added in the future.

##### Window manager themes

The window manager theme (the style of the window titlebars) can be set using the GNOME Tweak Tool or the following GSettings command:

```
$ gsettings set org.gnome.desktop.wm.preferences theme *theme-name*

```

###### Titlebar height

**Note:** Applying this configuration shrinks the titlebar of the GNOME-terminal and Chromium, but does not appear to affect the Nautilus titlebar height.
 `~/.config/gtk-3.0/gtk.css` 
```
headerbar.default-decoration {
 padding-top: 0px;
 padding-bottom: 0px;
 min-height: 0px;
 font-size: 0.6em;
}

headerbar.default-decoration button.titlebutton {
 padding: 0px;
 min-height: 0px;
}

```

See [[2]](https://ask.fedoraproject.org/en/question/10035/shrink-title-bar/?answer=86149#post-id-86149) for more information.

###### Titlebar button order

To set the order for the GNOME window manager (Mutter, Metacity):

```
$ gsettings set org.gnome.desktop.wm.preferences button-layout ':minimize,maximize,close'

```

**Tip:** The colon indicates which side of the titlebar the window buttons will appear.

###### Hide titlebar when maximized

*   [Install](/index.php/Install "Install") [gnome-shell-extension-pixel-saver-git](https://aur.archlinux.org/packages/gnome-shell-extension-pixel-saver-git/) or [gnome-shell-extension-pixel-saver](https://aur.archlinux.org/packages/gnome-shell-extension-pixel-saver/). Maximized windows get the title bar merged into the activity bar, saving precious pixels.

*   [Install](/index.php/Install "Install") [mutter-hide-legacy-decorations](https://aur.archlinux.org/packages/mutter-hide-legacy-decorations/). It changes a default setting in the window manager, so as to automatically hide the titlebar on legacy (non-headerbar) apps when they are maximized or tiled to the side.

*   [Install](/index.php/Install "Install") [maximus](https://aur.archlinux.org/packages/maximus/). To start the application, execute *maximus* from a terminal. When running, the daemon will automatically maximize windows. It will undecorate maximized windows and redecorate them when they are unmaximized. If you do not want all windows to start maximized, run `maximus -m` instead. Note that this will only work with windows decorated by the window manager; applications that use client-side decoration such as [GNOME Files](/index.php/GNOME_Files "GNOME Files") will not be undecorated when maximized.

##### GNOME Shell themes

The theme of GNOME Shell itself is configurable. To use a Shell theme, firstly ensure that you have the [gnome-shell-extensions](https://www.archlinux.org/packages/?name=gnome-shell-extensions) package installed. Then enable the *User Themes* extension, either through GNOME Tweak Tool or through the [GNOME Shell Extensions](https://extensions.gnome.org) webpage. Shell themes can then be loaded and selected using the GNOME Tweak Tool.

There are a number of GNOME Shell themes available [in the AUR](https://aur.archlinux.org/packages.php?O=0&K=gnome-shell-theme&do_Search=Go&PP=50&SB=v&SO=d).

Shell themes can also be downloaded from [gnome-look.org](http://gnome-look.org/index.php?xcontentmode=191).

##### Icons on menu

The default GNOME schema doesn't display any icon on menus. To display icons on menus, issue the following command.

```
$ gsettings set org.gnome.settings-daemon.plugins.xsettings overrides "{'Gtk/ButtonImages': <1>, 'Gtk/MenuImages': <1>}"

```

#### Desktop

Various Desktop settings can be applied.

##### Icons on the Desktop

See [GNOME/Files#Desktop Icons](/index.php/GNOME/Files#Desktop_Icons "GNOME/Files").

##### Lock screen and background

When setting the Desktop or Lock screen background, it is important to note that the Pictures tab will only display pictures located in `/home/*username*/Pictures` folder. If you wish to use a picture not located in this folder, use the commands indicated below.

For the desktop background:

```
$ gsettings set org.gnome.desktop.background picture-uri 'file:///path/to/my/picture.jpg'

```

For the lock screen background

```
$ gsettings set org.gnome.desktop.screensaver picture-uri 'file:///path/to/my/picture.jpg'

```

#### Extensions

**Note:** The GNOME Shell browser plugin which allows users to install extensions from [extensions.gnome.org](https://extensions.gnome.org) works out-of-the-box for browsers such as [Firefox](/index.php/Firefox "Firefox") or [GNOME/Web](/index.php/GNOME/Web "GNOME/Web"). For Google Chrome/Chromium, Opera and Vivaldi browsers, it is required to install [chrome-gnome-shell-git](https://aur.archlinux.org/packages/chrome-gnome-shell-git/).

GNOME Shell can be customized with extensions per user or system-wide.

The catalogue of extensions is available at [extensions.gnome.org](https://extensions.gnome.org). By a user they can be installed and activated in the browser by setting the switch in the top left of the screen to **ON** and clicking **Install** on the resulting dialog (if the extension in question is not installed). After installation it is shown in the [extensions.gnome.org/local/](https://extensions.gnome.org/local/) tab, which has to be visited as well to check for available updates. Installed extensions can also be enabled or disabled using [gnome-tweak-tool](https://www.archlinux.org/packages/?name=gnome-tweak-tool).

More information about GNOME shell extensions is available on the [GNOME Shell Extensions about page](https://extensions.gnome.org/about/).

[Installing](/index.php/Installing "Installing") extensions via a package makes them available for all users of the system and automates the update process.

The [gnome-shell-extensions](https://www.archlinux.org/packages/?name=gnome-shell-extensions) package provides a set of extensions maintained as part of the GNOME project (many of the included extensions are used by the GNOME Classic session).

Users who want a taskbar but do not wish to use the GNOME Classic session may want to enable the *Window list* extension (provided by the [gnome-shell-extensions](https://www.archlinux.org/packages/?name=gnome-shell-extensions) package).

#### Input methods

GNOME has integrated support for input methods through [IBus](/index.php/IBus "IBus"), only [ibus](https://www.archlinux.org/packages/?name=ibus) and the wanted input method engine (e.g. [ibus-libpinyin](https://www.archlinux.org/packages/?name=ibus-libpinyin) for Intelligent Pinyin) needed to be installed, after installation the input method engine can be added as a keyboard layout in GNOME's Regional & Language Settings.

#### Fonts

**Tip:** If you set the *Scaling factor* to a value above 1.00, the Accessibility menu will be automatically enabled.

Fonts can be set for Window titles, Interface (applications), Documents and Monospace. See the Fonts tab in the Tweak Tool for the relevant options.

For hinting, RGBA will likely be desired as this fits most monitors types, and if fonts appear too blocked reduce hinting to *Slight* or *None*.

#### Startup applications

To start certain applications on login, copy the relevant `.desktop` file from `/usr/share/applications/` to `~/.config/autostart/`.

The [gnome-tweak-tool](https://www.archlinux.org/packages/?name=gnome-tweak-tool) allows managing autostart-entries.

**Tip:** If the plus sign button in the Tweak Tool's Startup Applications section is unresponsive, try start the Tweak Tool from the terminal using the following command: `gnome-tweak-tool`. See the following [forum thread](https://bbs.archlinux.org/viewtopic.php?pid=1413631#p1413631).

**Note:** The deprecated *gnome-session-properties* dialog can be added by [installing](/index.php/Install "Install") the [gnome-session-properties](https://aur.archlinux.org/packages/gnome-session-properties/) package.

#### Power

The basic power settings that may want to be altered (these example settings assume the user is using a laptop - change them as desired):

```
$ gsettings set org.gnome.settings-daemon.plugins.power button-power *hibernate*
$ gsettings set org.gnome.settings-daemon.plugins.power sleep-inactive-ac-timeout *3600*
$ gsettings set org.gnome.settings-daemon.plugins.power sleep-inactive-ac-type *hibernate*
$ gsettings set org.gnome.settings-daemon.plugins.power sleep-inactive-battery-timeout *1800*
$ gsettings set org.gnome.settings-daemon.plugins.power sleep-inactive-battery-type *hibernate*
$ gsettings set org.gnome.desktop.lockdown disable-lock-screen *true*

```

To keep a monitor active on lid close:

```
$ gsettings set org.gnome.settings-daemon.plugins.xrandr default-monitors-setup do-nothing

```

##### Configure behaviour on lid switch close

The GNOME Tweak Tool can optionally *inhibit* the *systemd* setting for the lid close ACPI event.[[3]](http://ftp.gnome.org/pub/GNOME/sources/gnome-tweak-tool/3.17/gnome-tweak-tool-3.17.1.news) To *inhibit* the setting, start the Tweak Tool and, under the power tab, check the *Don't suspend on lid close* option. This means that the system will do nothing on lid close instead of suspending - the default behaviour. Checking the setting creates `~/.config/autostart/ignore-lid-switch-tweak.desktop` which will autostart the Tweak Tool's inhibitor.

If you do not want the system to suspend or do nothing on lid close, you will need to ensure that the setting described above is **not** checked and then configure *systemd* with `HandleLidSwitch=*preferred_behaviour*` as described in [Power management#ACPI events](/index.php/Power_management#ACPI_events "Power management").

##### Change critical battery level action

The settings panel does not provide an option for changing the critical battery level action. These settings have been removed from dconf as well. They are now managed by upower. Edit the upower settings in `/etc/UPower/UPower.conf`. Find these settings and adjust to your needs.

 `/etc/UPower/UPower.conf` 
```
PercentageLow=10
PercentageCritical=3
PercentageAction=2
CriticalPowerAction=HybridSleep
```

#### Sort applications into application (app) folders

**Tip:** The [gnome-catgen](https://github.com/prurigro/gnome-catgen) ([gnome-catgen-git](https://aur.archlinux.org/packages/gnome-catgen-git/)) script allows you to manage folders through the creation of files in `~/.local/share/applications-categories` named after each category and containing a list of the desktop files belonging to apps you would like to have inside. Optionally, you can have it cycle through each app without a folder and input the desired category until you ctrl-c or run out of apps.

In the **dconf-editor** navigate to `org.gnome.desktop.app-folders` and set the value of `folder-children` to an array of comma separated folder names:

```
['Utilities', 'Sundry']

```

Add applications using `gsettings`:

```
$ gsettings set org.gnome.desktop.app-folders.folder:/org/gnome/desktop/app-folders/folders/Sundry/ apps "['alacarte.desktop', 'dconf-editor.desktop']"

```

This adds the applications `alacarte.desktop` and `dconf-editor.desktop` to the Sundry folder. This will also create the folder `org.gnome.desktop.app-folders.folders.Sundry`.

To name the folder (if it has no name that appears at the top of the applications):

```
$ gsettings set org.gnome.desktop.app-folders.folder:/org/gnome/desktop/app-folders/folders/Sundry/ name "Sundry"

```

Applications can also be sorted by their category (specified in their *.desktop* file):

```
$ gsettings set org.gnome.desktop.app-folders.folder:/org/gnome/desktop/app-folders/folders/Sundry/ categories "['Office']"

```

If certain applications matching a category are not wanted in a certain folder, exclusions can be set:

```
$ gsettings set org.gnome.desktop.app-folders.folder:/org/gnome/desktop/app-folders/folders/Sundry/ excluded-apps "['libreoffice-draw.desktop']"

```

For further information, refer to the [app-folders schema](https://git.gnome.org/browse/gsettings-desktop-schemas/tree/schemas/org.gnome.desktop.app-folders.gschema.xml.in).

## Использование оболочки

### Шпаргалка GNOME

На сайте GNOME есть полезная [шпаргалка GNOME Shell](https://live.gnome.org/GnomeShell/CheatSheet), объясняющая переключение между задачами, использование клавиатуры, контроль окон, панель, обзор и другое.

### Перезапуск оболочки

После изменения внешнего вида вас обычно просят перезапустить GNOME shell. Вы можете выйти из сеанса и вновь войти, но проще и быстрее использовать сочетание клавиш. Перезапустите оболочку, нажав `Alt` + `F2`, затем введите `r` и нажмите `Enter`.

### Крахи оболочки

Некоторые улучшения и/или повторяющиеся перезапуски оболочки могут вызвать её крах. В этом случае вы будете проинформированы о крахе, и затем сеанс будет принудительно завершён. Некоторые изменения оболочки, например, переключение между ***GNOME Shell*** и ***fallback mode***, не могут быть выполнены через клавиатурный перезапуск: вы должны выйти из сеанса и вновь войти, чтобы увидеть изменения.

**Примечание:** Ценные документы должны быть сохранены (а также закрыты) перед выполнением перезапуска оболочки. Это не строго обязательно, обычно после этого открытые окна и документы остаются нетронутыми, однако есть риск потери данных, если документы не были закрыты

### Зависания оболочки

Иногда расширения оболочки вызывают зависания GNOME Shell. В этом случае возможный выход - переключение на другую виртуальную консоль при помощи `Ctrl+Alt+F1`, вход в систему и последующий перезапуск gnome-shell:

```
# pkill -HUP gnome-shell

```

После перезапуска оболочки все открытые документы будут по-прежнему доступны.

Однако, иногда простого перезапуска оболочки может быть недостаточно. В этом случае вам потребуется перезапустить X с потерей всех несохраненных данных. Вы можете сделать это, выполнив:

```
# pkill X

```

После этого GNOME Shell автоматически перезапустится.

Если это не помогает, вы можете перезапустить ваш менеджер входа. Например, если вы используете GDM, попробуйте:

```
# systemctl restart gdm.service

```

**Совет:** В tty вы также можете использовать **htop**: нажмите *t*, выберите ветку *gnome-shell*, нажмите *k* и отправьте *SIGKILL*

## Интеграция pacman

**Важно:** На данный момент (19 октября 2014 г.) интеграция *pacman* при помощи PackageKit сильно устарела. Она будет обновлена и исправлена в ближайшее время

PackageKit - это система, благодаря которой (графические) утилиты могут обращаться к пакетному менеджеру, например, *pacman*. В Arch Linux она использует бэкенд [alpm](https://www.archlinux.org/pacman/libalpm.3.html) и поддерживает следующие возможности:

*   Установка и удаление пакетов из репозиториев
*   Периодическое обновление баз данных пакетов и приглашение для обновления
*   Установка пакетов из исходников
*   Поиск пакетов по имени, описанию, категории или файлу
*   Отображение прямых и обратных зависимостей и файлов пакета
*   Игнорирование IgnorePkgs и удержание HoldPkgs
*   Уведомление о дополнительных зависимостях, файлах .pacnew и т.д.

Для GNOME доступны две графические оболочки: более консервативный GNOME PackageKit и более современный GNOME Software.

### GNOME PackageKit

GNOME PackageKit - довольно простая графическая оболочка. Для ее использования установите пакет [gnome-packagekit](https://www.archlinux.org/packages/?name=gnome-packagekit), доступный в [официальных репозиториях](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)").

Вы можете изменить опции удаления пакетов с `-Rc` на `-Rsc`, установив соответствующее значение ключа DConf в `org.gnome.packagekit.enable-autoremove`.

### GNOME Software

GNOME Software - это новая графическая оболочка для PackageKit, делающая процесс поиска и установки пакетов очень легким.

GNOME Software будет доступен в ближайшее время в пакете [gnome-software](https://www.archlinux.org/packages/?name=gnome-software) из [официальных репозиториев](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)") (на данный момент, 19 октября 2014 г., он находится в [gnome-unstable](https://www.archlinux.org/packages/gnome-unstable/x86_64/gnome-software/)).

### Уведомления об обновлениях пакетов

Если вы хотите, чтобы GNOME автоматически проверял наличие обновлений, необходимо установить пакет [gnome-settings-daemon-updates](https://aur.archlinux.org/packages/gnome-settings-daemon-updates/).

## Настройка внешнего вида GNOME

Утилита *Настройки Системы* (предоставляемая пакетом [gnome-control-center](https://www.archlinux.org/packages/?name=gnome-control-center)) является простой и удобной панелью, охватывающей большую часть общих настроек.

Более сложная графическая настройка (например, изменение шрифтов, тем, кнопок заголовка и т.п.) может быть выполнена при использовании графической *GNOME tweak tool*. Пакет [gnome-tweak-tool](https://www.archlinux.org/packages/?name=gnome-tweak-tool) доступен в [официальных репозиториях](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)"). Для получения дополнительной информации об этом смотрите раздел [#Темы оформления](#.D0.A2.D0.B5.D0.BC.D1.8B_.D0.BE.D1.84.D0.BE.D1.80.D0.BC.D0.BB.D0.B5.D0.BD.D0.B8.D1.8F) ниже.

Более существенная настройка может потребовать изменений более низкого уровня с использованием [#gsettings и dconf](#gsettings_.D0.B8_dconf).

#### Темы оформления

Для установки новых тем или наборов иконок скопируйте их в каталог `~/.local/share/themes` или `~/.local/share/icons` соответственно. После этого вы сможете активировать их в *GNOME tweak tool*, как описано выше.

Другой вариант - настроить тему GTK в `~/.config/gtk-3.0/settings.ini`. В этом файле вы можете указать тему GTK (`gtk-theme-name`), иконок (`gtk-icon-theme-name`), шрифта (`gtk-font-name`) и прочего. Например:

 `~/.config/gtk-3.0/settings.ini` 
```
[Settings]
gtk-theme-name = Adwaita
# следующая опция применима, только если выбранная тема ее поддерживает
gtk-application-prefer-dark-theme = true
# выберите название и кегль шрифта
gtk-font-name = Sans 10

```

*Adwaita,* тема по умолчанию в GNOME 3, является частью пакета [gnome-themes-standard](https://www.archlinux.org/packages/?name=gnome-themes-standard). Дополнительные темы GTK3 можно найти, например, на сайтах [DeviantArt](http://www.deviantart.com/browse/all/customization/skins/linuxutil/desktopenv/gnome/gtk3/) или [GNOME-Look.org](http://gnome-look.org/index.php?xcontentmode=167).

Необходимо перезапустить GNOME shell, чтобы изменения вступили в силу. Больше опций GTK можно найти в [документации разработчиков GNOME](http://developer.gnome.org/gtk3/3.0/GtkSettings.html#GtkSettings.properties).

#### gsettings и dconf

dconf - это хранилище данных, используемое GNOME для хранения его настроек. Их можно редактировать при помощи графического `dconf-editor` или консольной утилиты `gsettings`. Для изучения руководства по использованию gsettings смотрите страницу [Настройка GNOME Shell](http://blog.fpmurphy.com/2011/03/customizing-the-gnome-3-shell.html).

### Верхняя панель

#### Показывать дату в верхней панели

По умолчанию в верхней панели GNOME показывает только день недели и часы. Вы можете изменить это при помощи данной команды (изменения будут видны сразу):

```
$ gsettings set org.gnome.desktop.interface clock-show-date true

```

#### Отключить задержку при выходе из сеанса

Эта настройка удаляет диалог подтверждения и шестидесятисекундную задержку при выходе из сеанса.

Обычно этот диалог появляется при выходе из сеанса с помощью статус-меню. Эта настройка затрагивает диалог ***Power Off***. Это не общесистемное изменение, оно влияет только на пользователя, который введёт эту команду. Изменение вступает в силу сразу после ввода команды:

```
$ gsettings set org.gnome.SessionManager logout-prompt 'false'

```

#### Показать системный монитор

Расширение [system-monitor](https://extensions.gnome.org/extension/120/system-monitor/) включено в состав пакета [gnome-shell-extensions](https://www.archlinux.org/packages/?name=gnome-shell-extensions). Гит-версия доступна в пакете [gnome-shell-system-monitor-applet-git](https://aur.archlinux.org/packages/gnome-shell-system-monitor-applet-git/) из [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)").

#### Показать информацию о погоде

Расширение [weather](https://extensions.gnome.org/extension/613/weather/) можно установить с [официального веб-сайта расширений](https://extensions.gnome.org/extension/613/weather/). Гит-версия доступна в пакете [gnome-shell-extension-weather-git](https://aur.archlinux.org/packages/gnome-shell-extension-weather-git/) из [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)").

### Обзор

#### Удаление пунктов из меню приложений

Как и в других рабочих окружениях, для заполнения меню приложений GNOME используются файлы *.desktop*. Эти текстовые файлы находятся в `/usr/share/applications`. Их нельзя редактировать "непосредственно в папке": Files не расценивает их иконки как текстовые файлы. Для их редактирования потребуются права суперпользователя.

```
# ls /usr/share/applications
# nano /usr/share/applications/foo.desktop

```

Для общесистемных изменений редактируйте файлы в `/usr/share/applications`. Для местных изменений создайте копию `foo.desktop` в вашем домашнем каталоге.

```
$ cp /usr/share/applications/foo.desktop ~/.local/share/applications/

```

Отредактируйте файлы .desktop по своему желанию.

**Примечание:** Удаление файла .desktop не удаляет приложение, но удаляет его интеграцию с рабочим столом: MIME type'ы, ярлыки и т.д.

Чтобы скрыть иконку запуска приложения, откройте его файл .desktop в текстовом редакторе и добавьте следующую строку:

```
NoDisplay=true

```

#### Сортировка приложений по папкам

Gnome 3.12 позволяет пользователю сортировать приложения по папкам. GUI для этого предоставляет Gnome Software, но в Arch нет пакета с ним (в связи с несовместимостью с PackageKit). Однако, приложения по-прежнему можно сортировать по папкам вручную через dconf. Чтобы добавить папку, перейдите в dconf по пути `org.gnome.desktop.app-folders` и установите значение `folder-children` в массив имен папок, разделенных запятыми:

```
['Utilities', 'Sundry']

```

Чтобы добавить приложения в эти папки, используйте *gsettings*:

```
gsettings set org.gnome.desktop.app-folders.folder:/org/gnome/desktop/app-folders/folders/Sundry/ apps "['alacarte.desktop', 'dconf-editor.desktop']"

```

Эта команда добавит приложения, относящиеся к файлам `alacarte.desktop` и `dconf-editor.desktop`, в папку Sundry.

Она также создаст папку `org.gnome.desktop.app-folders.folders.Sundry`. Составляющие папки можно обновлять через *dconf-editor* или *gsettings* путем добавления приложений в список.

Чтобы дать название папке (если названия нет, она просто будет показана вверху приложений), установите значение для ключа имени через *gsettings*:

```
gsettings set org.gnome.desktop.app-folders.folder:/org/gnome/desktop/app-folders/folders/Sundry/ name "Sundry"

```

Приложения также могут быть отсортированы по их категориям (указанным в файлах *.desktop*):

```
gsettings set org.gnome.desktop.app-folders.folder:/org/gnome/desktop/app-folders/folders/Sundry/ categories "['Office']"

```

Если некоторые приложения, соответствующие категории, нежелательны в какой-либо папке, можно настроить исключения:

```
gsettings set org.gnome.desktop.app-folders.folder:/org/gnome/desktop/app-folders/folders/Sundry/ excluded-apps "['libreoffice-draw.desktop']"

```

Для получения дополнительной информации обратитесь к странице [Схема папок приложений](https://git.gnome.org/browse/gsettings-desktop-schemas/tree/schemas/org.gnome.desktop.app-folders.gschema.xml.in.in).

#### Изменение размера иконок

##### Для приложений в меню обзора

Для изменения размера иконки приложения необходимо отредактировать тему GNOME-Shell.

Редактируйте напрямую системные файлы (предварительно сделав их резервные копии) или скопируйте их в вашу локальную папку и редактируйте там:

**Примечание:** При использовании пользовательских тем редактируйте `/usr/share/themes/<Пользовательская Тема>/gnome-shell/gnome-shell.css`

Отредактируйте `gnome-shell.css` и замените необходимые значения. После этого [перезапустите GNOME shell](#.D0.9F.D0.B5.D1.80.D0.B5.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D0.BE.D0.B1.D0.BE.D0.BB.D0.BE.D1.87.D0.BA.D0.B8).

 `gnome-shell.css` 
```
 ...
 /* Application Launchers and Grid */

 .icon-grid {
     spacing: 18px;
     -shell-grid-horizontal-item-size: 82px;
     -shell-grid-vertical-item-size: 82px;
 }

 .icon-grid .overview-icon {
     icon-size: 48px;
 }
 ...

```

##### В dash

В меню обзора GNOME с левой стороны имеется dash, размер иконок в котором будет изменяться в зависимости от их количества. Вы можете настроить масштабирование или указать конкретный размер иконок. Чтобы сделать это, отредактируйте файл `/usr/share/gnome-shell/js/ui/dash.js`.

 `dash.js` 
```
 ...

        let iconSizes = [ 16, 22, 24, 32, 48, 64 ];

 ...

```

##### При переключении по alt-tab

GNOME использует встроенный переключатель задач, и размер иконок в нём будет изменяться в зависимости от их количества. Вы можете настроить масштабирование или указать конкретный размер иконок. Чтобы сделать это, отредактируйте файл `/usr/share/gnome-shell/js/ui/altTab.js`

 `altTab.js` 
```
 ...

        const iconSizes = [96, 64, 48, 32, 22];

 ...

```

##### В системном трее

GNOME использует встроенный системный трей, видимый, когда курсор мыши находится около правого нижнего угла экрана. Для иконок в нём установлено фиксированное значение 24\. Чтобы изменить его, отредактируйте файл `/usr/share/gnome-shell/js/ui/messageTray.js`

 `messageTray.js` 
```
 ...

    ICON_SIZE: 24,

 ...

```

#### Отключение "горячего угла"

##### Меню обзора

Чтобы отключить вход в меню обзора при приближении курсора мыши к "горячему углу", отредактируйте `/usr/share/gnome-shell/js/ui/layout.js` (в GNOME 3.0.x это файл *panel.js*) :

 `layout.js` 
```
 this._corner = new Clutter.Rectangle({ name: 'hot-corner',
                                       width: 1,
                                       height: 1,
                                       opacity: 0,
                                       reactive: true });icon-size: 48px;
 }

```

и установите для показателя `reactive` значение `false`. После этого GNOME Shell должен быть перезапущен.

##### Трей сообщений

Трей сообщений показывается, когда курсор мыши находится внизу экрана в течение одной секунды. Для отключения этой опции закомментируйте следующую строку в файле `/usr/share/gnome-shell/js/ui/messageTray.js`:

 `messageTray.js` 
```
        //pointerWatcher.addWatch(TRAY_DWELL_CHECK_INTERVAL, Lang.bind(this, this._checkTrayDwell));

```

После этого GNOME Shell должен быть перезапущен. Вы можете по-прежнему увидеть трей сообщений в меню обзора.

### Заголовок окна

#### Уменьшение высоты заголовка окнa

*   **Глобально** - отредактируйте `/usr/share/themes/Adwaita/metacity-1/metacity-theme-3.xml`, найдите `title_vertical_pad` и уменьшите это значение (минимальное - `0`)
*   **Для одного пользователя** - скопируйте файл `/usr/share/themes/Adwaita/metacity-1/metacity-theme-3.xml` в `/home/$USER/.local/share/themes/Adwaita/metacity-1/metacity-theme-3.xml`, найдите `title_vertical_pad` и уменьшите это значение (минимальное - `0`)

Затем [перепустите GNOME shell](#.D0.9F.D0.B5.D1.80.D0.B5.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D0.BE.D0.B1.D0.BE.D0.BB.D0.BE.D1.87.D0.BA.D0.B8).

Чтобы восстановить значения по умолчанию, [установите](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.BE.D0.BF.D1.80.D0.B5.D0.B4.D0.B5.D0.BB.D0.B5.D0.BD.D0.BD.D1.8B.D1.85_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.BE.D0.B2 "Pacman (Русский)") пакет [gnome-themes-standard](https://www.archlinux.org/packages/?name=gnome-themes-standard) из [официальных репозиториев](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)") или удалите файл `/home/$USER/.local/share/themes/Adwaita/metacity-1/metacity-theme-3.xml`.

#### Изменение порядка кнопок в заголовке окнa

В данный момент эта настройка может быть изменена при помощи *dconf-editor*.

Например, мы передвинем кнопки закрытия и сворачивания на левую сторону заголовка окна. Запустите `dconf-editor` и перейдите к ключу `org.gnome.shell.overrides.button_layout`. Измените его значение на `close,minimize:` (двоеточие указывает на свободное место между левой и правой сторонами заголовка). Установите тот порядок кнопок, который вы предпочитаете. Вы не можете использовать кнопку больше одного раза. Также помните, что некоторые кнопки устарели.

Для полноценного применения изменений необходимо изменить некоторые другие значения:

```
gsettings set org.gnome.desktop.wm.preferences button-layout 'close,minimize,maximize:'
gsettings set org.gnome.shell.overrides button-layout 'close,minimize,maximize:'
gsettings set org.gnome.settings-daemon.plugins.xsettings overrides "{'Gtk/DecorationLayout' <'close,minimize,maximize:'>}"

```

Первая команда задает порядок для *оконного менеджера Gnome*. Вторая - то же самое, но для случая использования вместе с *Gnome Shell* (для перезаписи предыдущей настройки используется этот ключ, и по умолчанию для него установлено значение ':close'). Третья команда задает порядок для [украшений на стороне клиента](/index.php/GTK%2B_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.9A.D0.BB.D0.B8.D0.B5.D0.BD.D1.82.D1.81.D0.BA.D0.B8.D0.B5_.D0.B4.D0.B5.D0.BA.D0.BE.D1.80.D0.B0.D1.86.D0.B8.D0.B8 "GTK+ (Русский)").

#### Скрытие заголовка окна при разворачивании

Чтобы заголовки окон скрывались при разворачивании на весь экран, откройте файл `/usr/share/themes/Adwaita/metacity-1/metacity-theme-3.xml`, найдите следующий тэг и измените его свойства и свойства тэгов-потомков, как показано ниже:

```
<frame_geometry name="max" has_title="false"
                           hide_buttons="true"
                           parent="normal"
                           rounded_top_left="false"
                           rounded_top_right="false">
    <distance name="left_width" value="0" />
    <distance name="right_width" value="0" />
    <distance name="left_titlebar_edge" value="0"/>
    <distance name="right_titlebar_edge" value="0"/>
    <distance name="title_vertical_pad" value="0"/>
    <border name="title_border" left="0" right="0" top="0" bottom="0"/>
    <border name="button_border" left="0" right="0" top="0" bottom="0"/>
    <distance name="bottom_height" value="0" />
</frame_geometry>

```

После сохранения файла перезапустите GNOME shell, нажав `Alt + F2` и введя `r`. Помните, что после применения данного изменения у вас могут возникнуть трудности с восстановлением размеров окон, поскольку на экране не будет заголовков с кнопками. Вы можете использовать горячие клавиши `Alt+F5`, `Alt+F10` или `Alt+Space`, чтобы исправить ситуацию.

Чтобы предотвратить перезапись файла `metacity-theme-3.xml` при каждом обновлении пакета [gnome-themes-standard](https://www.archlinux.org/packages/?name=gnome-themes-standard), добавьте его название в `/etc/pacman.conf` в секцию `NoUpgrade`:

 `/etc/pacman.conf` 
```
... previous lines ...

# Pacman won't upgrade packages listed in IgnorePkg and members of IgnoreGroup
# IgnorePkg   =
# IgnoreGroup =

NoUpgrade = usr/share/themes/Adwaita/metacity-1/metacity-theme-3.xml    # Не пишите начальный слеш в пути к файлу

... more lines ...
```

Чтобы восстановить стандартные значения темы Adwaita, установите пакет [gnome-themes-standard](https://www.archlinux.org/packages/?name=gnome-themes-standard).

#### Отключение анимации

Для отключения анимации "Показать приложения", а также "волн" при наведении курсора в верхний левый угол меню обзора, используйте *dconf-editor* и снимите галочку с настройки `org.gnome.desktop.interface enable-animations`.

## Различные настройки

### Управление питанием

#### Выключение сна-в-ОЗУ (S3) при закрытии крышки ноутбука

Эта возможность недоступна в GNOME, ее можно настроить при помощи *gnome-control-center* и *dconf*. В настоящий момент используется подход управления сном на уровне [systemd](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd (Русский)"). Отредактируйте файл `/etc/systemd/logind.conf`, раскомментировав строку `HandleLidSwitch` и установив для нее значение `ignore`:

 `/etc/systemd/logind.conf`  `HandleLidSwitch=ignore` 

Для получения дополнительной информации смотрите раздел [События ACPI](/index.php/Power_management#ACPI_events "Power management").

#### Нет реакции на закрытие крышки ноутбука

При настройке через [systemd](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A3.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D0.B8.D1.82.D0.B0.D0.BD.D0.B8.D0.B5.D0.BC "Systemd (Русский)") событий при закрытии крышки, может показаться, что изменения ни к чему не приводят. Это стандартное поведение GNOME в том случае, если у вас есть внешний монитор, подключенный к ноутбуку. Отключите монитор, и после этого изменения должны заработать, в противном случае проверьте правильность вашего файла `/etc/systemd/logind.conf`. Для изменения поведения по умолчанию откройте `dconf-editor` и поменяйте значение `org.gnome.settings-daemon.plugins.xrandr.default-monitors-setup` на `"do-nothing"`.

#### Изменение действия при критическом заряде батареи (для ноутбуков)

Панель *Системные настройки* позволяет пользователям выбирать лишь между *сном* и *гибернацией*. Для выбора другого варианта, такого как *ничего не делать*, откройте `dconf-editor` и пройдите по пути `org.gnome.settings-daemon.plugins.power`. Установите для `"critical-battery-action"` значение `"nothing"`.

### Возвращение назад поведения прокрутки

Если вам не нравится новое поведение полос прокрутки, просто вставьте строку `gtk-primary-button-warps-slider = false` в секцию `[Settings]` файла `~/.config/gtk-3.0/settings.ini`:

 `~/.config/gtk-3.0/settings.ini` 
```
[Settings]
gtk-primary-button-warps-slider = false
...

```

### Автоматический запуск программ при входе в систему

В Gnome 3.12 *gnome-session-properties* больше не используется. Укажите, какие программы должны запускаться автоматически после входа в систему, используя *gnome-tweak-tool* или вручную, как описано [здесь](http://linuxandfriends.com/how-to-add-startup-programs-in-gnome-3/).

**Совет:** Некоторые пользователи не могут добавлять приложения в автозапуск, когда запускают `gnome-tweak-tool` из режима обзора Gnome. Иногда помогает запуск из терминала. Также эту проблему можно решить, внеся изменения в соответствии с этим [сообщением](https://bbs.archlinux.org/viewtopic.php?pid=1414443#p1414443), но пользователи по-прежнему не смогут добавлять какие-либо самописные программы, такие как скрипты, в автозапуск.
[gnome-session-properties](https://aur.archlinux.org/packages/gnome-session-properties/) все еще доступен в [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)")

### Редактирование меню приложений

[alacarte](https://www.archlinux.org/packages/?name=alacarte) содержит довольно полный редактор меню для добавления/редактирования пунктов.

### Gnome Terminal

#### Внутренний отступ

Чтобы отодвинуть вывод терминала от границ окна, создайте стиль в файле `~/.config/gtk-3.0/gtk.css` со следующими настройками:

```
   TerminalScreen {
     -VteTerminal-inner-border: 10px 10px 10px 10px;
   }

```

#### Отключение мигающего курсора

Начиная с версии Gnome 3.8 и миграции на gsettings и dconf ключ, необходимый для отключения мигающего курсора в терминале, отличается незначительно, по сравнению со старым ключом gconf. Чтобы сделать это в Gnome 3.8 используйте:

```
gsettings set org.gnome.desktop.interface cursor-blink false

```

Если вместо gsettings CLI вы предпочитаете использовать dconf, откройте `dconf-editor`, перейдите по пути org -> gnome -> desktop -> interface и снимите галочку с опции **cursor-blink**.

Для отключения мигающего курсора лишь в терминале используйте (удостоверьтесь, что прописан правильный uid профиля):

```
dconf write /org/gnome/terminal/legacy/profiles:/:b1dcc9dd-5262-4d8d-a863-c897e6d979b9/cursor-blink-mode "'off'"

```

#### Открытие новых вкладок в текущем каталоге (для Gnome Terminal 3.8+)

В Gnome 3.8 изменилась технология отслеживания текущего каталога. Для восстановления прошлого поведения необходимо указать на файл `/etc/profile.d/vte.sh`, добавив следующую строку в ваш файл `~/.bashrc` (или `~/.zshrc` для пользователей zsh):

```
source /etc/profile.d/vte.sh

```

Для получения дополнительной информации обратитесь к [Gnome wiki](https://wiki.gnome.org/action/show/Apps/Terminal/FAQ?action=show&redirect=Terminal%252FFAQ#How_can_I_make_new_terminals_start_in_the_working_directory_of_the_current_terminal.3F).

### Перемещение диалоговых окон

В конфигурации по умолчанию вы не можете перемещать их, что вызывает проблемы в некоторых случаях. Для получения такой возможности используйте gconf-editor и измените следующую настройку:

```
/desktop/gnome/shell/windows/attach_modal_dialogs

```

После этого изменения вам необходимо перезапустить оболочку, чтобы увидеть результат.

### Расширения GNOME shell

GNOME Shell можно настроить при помощи расширений. Они добавляют такие функции, как dock или виджет для смены тем.

Множество расширений собрано и размещено на сайте [extensions.gnome.org](https://extensions.gnome.org/). Вы можете просматривать их и устанавливать, просто активируя в браузере. Вы можете найти больше информации о расширениях gnome shell [здесь](https://extensions.gnome.org/about/).

Для получения информации по устранению неисправностей смотрите раздел [#Когда расширение рушит GNOME](#.D0.9A.D0.BE.D0.B3.D0.B4.D0.B0_.D1.80.D0.B0.D1.81.D1.88.D0.B8.D1.80.D0.B5.D0.BD.D0.B8.D0.B5_.D1.80.D1.83.D1.88.D0.B8.D1.82_GNOME).

### Приложения по умолчанию

Когда вы нажимаете правой кнопкой мыши на любом файле и устанавливаете для него в 'Настройках' приложение по умолчанию, фактически настройки сохраняются в `$HOME/.local/share/applications/mimeapps.list` и `$HOME/.local/share/applications/mimeinfo.cache`.

**Совет:** Если вы хотите установить приложения по умолчанию общесистемно, вы можете самостоятельно создать файл `/usr/share/applications/mimeapps.list`

#### Файловый менеджер/замена Files

Вы можете указать другой файловый менеджер в файле *mimeapps.list*, как показано ниже:

**Только для пользователя**: добавьте строку `inode/directory=мойфайловыйменеджер.desktop` в `~/.local/share/applications/mimeapps.list`

**Общесистемно**: добавьте строку `inode/directory=мойфайловыйменеджер.desktop` в `/usr/share/applications/mimeapps.list`

Где мойфайловыйменеджер.desktop - правильное имя файла .desktop для выбранного файлового менеджера.

Альтернативный вариант - отредактировать линию `Exec` в файле `/usr/share/applications/nautilus.desktop`. Ищите правильный параметр в файле `.desktop` вашего файлового менеджера, например:

 `/usr/share/applications/nautilus.desktop` 
```
[...]
Exec=thunar %F
ИЛИ
Exec=pcmanfm %U
ИЛИ
Exec=nemo %U
[...]
```

#### Программа просмотра PDF

В некоторых случаях, если вы установили Inkscape или другую программу для графики, программа просмотра документов Evince больше не может быть выбрана в качестве приложения по умолчанию для PDF. Если она недоступна в диалоге **Открыть с помощью другой программы** (что является решением в GUI), вы можете использовать следующую команду:

```
xdg-mime default evince.desktop application/pdf

```

### Средняя кнопка мыши

По умолчанию GNOME 3 отключает эмуляцию средней кнопки мыши, несмотря на настройки [Xorg](/index.php/Xorg_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xorg (Русский)") (**Emulate3Buttons**). Чтобы включить эмуляцию средней кнопки мыши используйте:

```
$ gsettings set org.gnome.settings-daemon.peripherals.mouse middle-button-enabled true

```

### Затемнение экрана

По умолчанию в GNOME 3 установлен таймаут в 10 секунд простоя для затемнения экрана вне зависимости от питания (от батареи или от сети):

```
gsettings get org.gnome.settings-daemon.plugins.power idle-dim-time

```

Для установки нового значения выполните

```
gsettings set org.gnome.settings-daemon.plugins.power idle-dim-time <int>

```

где <int> - значение в секундах.

### Настройка горячих клавиш

Некоторые комбинации клавиш нельзя изменить напрямую в панели *Настройки системы*. Чтобы сделать это, используйте dconf-editor. В качестве примера следует отметить комбинацию Alt-Above_Tab. На US-клавиатурах это Alt-`, комбинация, часто используемая в редакторе [Emacs](/index.php/Emacs "Emacs"). Ее можно изменить, открыв dconf-editor и отредактировав ключ *switch-group*, расположенный по пути `org.gnome.desktop.wm.keybindings`.

Также возможно вручную менять горячие клавиши через так называемый файл accel map приложения. Его расположение зависит от приложения: например, для Thunar это ~/.config/Thunar/accels.scm, тогда как для Files - ~/.config/nautilus/accels и ~/.gnome2/accels/nautilus для старого релиза.

Файл должен содержать список доступных комбинаций, а каждая неизмененная комбинация - быть закомментирована предшествующим символом ";", который следует удалить для вступления изменений в силу. Например, чтобы изменить комбинацию, используемую Files для удаления файлов в корзину, измените строку:

```
; (gtk_accel_path "<Actions>/DirViewActions/Trash" "<Primary>Delete")

```

на такую:

```
(gtk_accel_path "<Actions>/DirViewActions/Trash" "Delete")

```

Этот файл регулярно перегенерируется, так что не оставляйте в нем комментариев. Строки останутся раскомментированными, но любой добавленный комментарий будет стерт.

#### Files 3.4 и старше

Сперва используйте **dconf-editor**, чтобы поставить галочку напротив `can-change-accels` по пути *org.gnome.desktop.interface*.

Мы заменим горячую клавишу — ярлык клавиатуры a.k.a., акселератор клавиатуры, используемый Files для перемещения файлов в корзину. По умолчанию используется неудобное `Ctrl+Delete`.

*   Откройте Files, выберите любой файл и нажмите **Изменить** на панели инструментов
*   Наведите указатель на пункт *Переместить в корзину*
*   Нажмите `Delete`. Текущий акселератор удалён
*   Нажмите клавишу, которую вы хотите использовать в качестве нового акселератора клавиатуры
*   Нажмите `Delete`, чтобы новым акселератором стала клавиша Delete

До тех пор, пока вы не выберете файл или каталог, пункт *Переместить в корзину* будет затемнён. В конце выключите `can-change-accels`, чтобы предотвратить случайные изменения горячих клавиш.

### Запись экрана (screencast)

В Gnome присутствует встроенная возможность легкого создания записей экрана. Комбинация клавиш Control+Shift+Alt+R начинает и останавливает процесс записи. При этом в нижнем правом углу экрана будет отображаться красный кружок. После окончания записи файл с именем 'Screencast from %d%u-%c.webm' будет сохранен в каталог Видео. Для использования этой возможности необходимо, чтобы были установлены плагины gst:

```
$ pacman -Qs gst

```

### Настройка клавиатуры при помощи XkbOptions

Используя **dconf-editor**, перейдите в *org.gnome.desktop.input-sources.xkb-options* и добавьте необходимые опции (например, 'caps:swapescape') в список.

Для просмотра всех XkbOptions загляните в файл /usr/share/X11/xkb/rules/xorg, а затем - в /usr/share/X11/xkb/symbols/* для соответствующих описаний.

**Примечание:** Чтобы включить комбинацию `Ctrl+Alt+Backspace` для прекращения работы Xorg, используйте [gnome-tweak-tool](https://www.archlinux.org/packages/?name=gnome-tweak-tool) из [официальных репозиториев](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)"). При помощи **Tweak Tool** пройдите по пути *Ввод > Прекращение (Typing > Terminate)* и выберите опцию `Ctrl+Alt+Backspace` из выпадающего меню

### Включение раскладок клавиатуры

С тех пор, как Gnome перестал использовать любые настройки в `/etc/X11/conf.d/*.conf`, необходимо настроить команду для переключения раскладок либо через control center при помощи опций *Переключить на предыдущий источник (Switch to previous source)* и *Переключить на следующий источник (Switch to next source)*, либо, если вы хотите использовать комбинацию Alt - Shift, запустив Gnome-Tweak-Tool и установив значение *Ввод -> Modifiers-only input sources -> выбрать Alt-shift*. Для получения дополнительной информации смотрите также [ветку](https://bbs.archlinux.org/viewtopic.php?id=152127) форума.

### Поддержка экранов HiDPI (Retina)

Поддержка HiDPI была представлена в Gnome версии 3.10\. Если ваш дисплей не предоставляет корректный размер экрана при помощи EDID, элементы интерфейса могут иметь неправильный масштаб. Для решения проблемы (установки стандартного масштабирования) вы можете открыть *dconf-editor*, найти ключ `scaling-factor` по пути `org.gnome.desktop.interface` и задать ему значение `1`.

Смотрите также статью [HiDPI](/index.php/HiDPI "HiDPI").

### Другие советы

Смотрите статью [Советы по GNOME](/index.php/GNOME_Tips_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GNOME Tips (Русский)").

## Tracker (программа поиска)

Пакет [tracker](https://www.archlinux.org/packages/?name=tracker) предоставляет программу Tracker, приложение индексации. Вы можете настроить его при помощи `tracker-preferences` и отслеживать состояние в `tracker-control`. Как только оно будет установлено, индексация должна начаться автоматически при входе в систему. Вы можете явно начать индексацию при помощи команды `tracker-control -s`. Настройки поиска можно также изменить в панели *Настройки системы*.

## Totem (видео проигрыватель)

Totem - видео проигрыватель, основанный на [GStreamer](/index.php/GStreamer "GStreamer"). Для получения информации по добавлению кодеков или включению аппаратного ускорения смотрите статью [GStreamer](/index.php/GStreamer "GStreamer").

## Empathy (встроенная система обмена мгновенными сообщениями) и GNOME Online Accounts

Empathy, движок обмена мгновенными сообщениями, GNOME Online Accounts и все остальные системные настройки, связанные с аккаунтами обмена сообщениями, не будут работать правильно, пока не будет установлена группа пакетов [telepathy](https://www.archlinux.org/groups/x86_64/telepathy/) или хотя бы один из backend'ов ([telepathy-gabble](https://www.archlinux.org/packages/?name=telepathy-gabble) или [telepathy-haze](https://www.archlinux.org/packages/?name=telepathy-haze), например).

Эти пакеты **не** включены ни в группу [gnome](https://www.archlinux.org/groups/x86_64/gnome/), ни в группу [gnome-extra](https://www.archlinux.org/groups/x86_64/gnome-extra/). Вы можете установить Telepathy и, по желанию, любые backend'ы при помощи команды:

```
# pacman -S telepathy

```

Без telepathy Empathy не откроет диалог управления аккаунтами, и даже может зависнуть в этом состоянии. Если это случится, даже после того, как вы чисто закрыли Empathy, приложение `/usr/bin/empathy-accounts` может быть по-прежнему запущено. Его работа должна быть завершена, прежде чем вы сможете добавлять новые аккаунты. Также без telepathy не будет работать кнопка 'Добавить online-аккаунт' в GNOME Online Accounts.

Смотрите описания компонентов telepathy в [Freedesktop.org Telepathy Wiki](http://telepathy.freedesktop.org/wiki/Components).

Для соединения с аккаунтом "Люди поблизости", а также для того, чтобы некоторые расширения Gnome Shell (например, [Chat Status](https://extensions.gnome.org/extension/746/chat-status/)) работали правильно, необходим демон [Avahi](/index.php/Avahi "Avahi").

## Решение проблем

### Невозможно изменить настройки в dconf-editor

Если вы не можете изменить настройки в [dconf](https://www.archlinux.org/packages/?name=dconf), возможно, они (настройки пользователя, связанные с dconf) повреждены. В этом случае лучше всего удалить dconf-файлы пользователя в `~/.config/dconf/user*`, после чего выставить нужные настройки в dconf-editor.

### Расширения

#### Когда расширение рушит GNOME

Если включение расширения оболочки вызывает крах GNOME, в первую очередь вам следует удалить расширения *user-theme* и *auto-move-windows* из их установочных каталогов.

Установочным каталогом может быть один из `~/.local/share/gnome‑shell/extensions`, `/usr/share/gnome‑shell/extensions` или `/usr/local/share/gnome‑shell/extensions`. Удаление этих двух каталогов, содержащих расширения, может исправить ситуацию. В противном случае вычислите проблемное расширение с помощью метода проб и ошибок.

Удаление или добавление каталогов, содержащих расширения, в вышеупомянутые каталоги удаляет или добавляет соответствующие расширения в вашу систему. Более подробно о расширениях GNOME Shell вы можете узнать на [веб-сайте GNOME](https://live.gnome.org/GnomeShell/Extensions).

#### Расширения не работают после обновления GNOME 3

Проверьте обновления расширений, посетив страницу [extensions.gnome.org/local](https://extensions.gnome.org/local). Если для вашей версии GNOME обновлений все еще нет, вы можете попробовать нижеописанный способ на свой страх и риск.

Найдите каталог, в котором установлены расширения. Это может быть `~/.local/share/gnome-shell/extensions` или `/usr/share/gnome-shell/extensions`.

Измените каждый файл `metadata.json`, который есть в каждом из подкаталогов, таким образом:

| Вставьте: | `"shell-version": ["3.x"]` |
| Вместо (к примеру): | `"shell-version": ["3.4"]` |

`"3.x"` заставляет расширение работать с любой версией оболочки. Если оно не работает, верните первоначальный вариант.

#### Удаление расширений Gnome Shell

Если у вас возникли трудности с удалением расширений Gnome через [https://extensions.gnome.org/local/](https://extensions.gnome.org/local/), скорее всего, они были установлены ранее с пакетом `pacman -S gnome-shell-extensions`. Чтобы удалить их, необходимо быть осторожным, так как данная команда также удалит все расширения других пользователей:

```
# pacman -R gnome-shell-extensions

```

После этого перезапустите Gnome Shell, нажав ALT+F2 и введя `restart`.

Затем вновь зайдите на [https://extensions.gnome.org/local/](https://extensions.gnome.org/local/) и проверьте список установленных у вас расширений. Он должен измениться.

Все остальные расширения должны удаляться нажатием на красную иконку X справа. Если это не так, возможно, что-то сломалось.

В качестве финального шага вы можете удалить их вручную из `~/.local/share/gnome-shell/extensions/*` и/или `/usr/share/gnome-shell/extensions`. Вновь перезапустите Gnome Shell, после чего проблема должна быть решена.

### Клавиша "Windows"

По умолчанию эта клавиша запускает меню Обзора. Вы можете изменить это назначение, чтобы освободить вашу `клавишу Windows` (также называемую `Mod4`), которая в GNOME называется `Super_L`, используя `gsettings`.

Пример: `gsettings set org.gnome.mutter overlay-key 'Foo';`. Вы можете не писать **Foo**, чтобы просто удалить любое назначение для этой клавиши.

**Примечание:** GNOME также использует `Alt+F1` для запуска меню Обзора

### Горячие клавиши не работают, когда запущен только conky

Горячие клавиши gnome-shell, такие как `Alt+F2`, `Alt+F1` и медиа-клавиши, не работают, если conky является единственной запущенной программой. Однако, если другое приложение (например, gedit) запущено, горячие клавиши работают.

Решение - отредактировать .conkyrc:

```
own_window yes
own_window_transparent yes
own_window_argb_visual yes
own_window_type dock
own_window_class Conky
own_window_hints undecorated,below,sticky,skip_taskbar,skip_pager

```

### Окно открывается позади других окон при использовании нескольких мониторов

Это ошибка в GNOME Shell, вызывающая открытие новых окон позади других. Снятие галочки `workspaces_only_on_primary` в `org/gnome/shell/overrides` в *dconf-editor* решает эту проблему.

### Несколько мониторов и расширение dock

Если вы используете несколько мониторов, настроенных с использованием Nvidia Twinview, расширение dock может разделиться на два монитора. Вы можете отредактировать код этого расширения, чтобы переместить dock туда, куда вам надо.

Отредактируйте `/usr/share/gnome-shell/extensions/dock@gnome-shell-extensions.gnome.org/extension.js` и найдите эту строку в коде:

```
this.actor.set_position(primary.width-this._item_size-this._spacing-2, (primary.height-height)/2);

```

Первый параметр - позиция X для отображения dock, вы можете поиграться с координатами X и Y, чтобы указать верное местоположение.

```
this.actor.set_position(primary.width-this._item_size-this._spacing-15, (primary.height-height)/2);

```

### Горячие клавиши "Показать рабочий стол" не работают

Разработчики GNOME считают это багом (смотрите [https://bugzilla.gnome.org/show_bug.cgi?id=643609](https://bugzilla.gnome.org/show_bug.cgi?id=643609)) в связи с тем, что сворачивание устарело. Чтобы показать рабочий стол, присвойте значение ALT+STRG+D следующей настройке:

```
Параметры системы --> Клавиатура --> Комбинации клавиш --> Навигация --> Скрыть все окна

```

### Невозможно применить сохранённую конфигурация мониторов

Если вы получаете это сообщение, попробуйте выключить xrandr gnome-settings-daemon plugin:

```
$ dconf write /org/gnome/settings-daemon/plugins/xrandr/active false

```

### Кнопка блокировки не может вновь включить тачпад

В некоторых ноутбуках есть кнопка блокировки тачпада, которая отключает его, чтобы пользователи могли набирать текст без опасений прикоснуться к тачпаду. Иногда случается, что, несмотря на то, что GNOME может блокировать тачпад при нажатии на эту кнопку, он не может потом его разблокировать. Если тачпад остаётся заблокированным, вы можете выполнить следующие действия для его разблокировки:

1.  Запустите терминал. Вы можете сделать это, нажав `Alt+F2`, набрав `gnome-terminal` и затем нажав `Enter`
2.  Введите следующую команду:

```
$ xinput --set-prop "SynPS/2 Synaptics TouchPad" "Device Enabled" 1

```

### GNOME использует курсор Х11

Вы можете обнаружить, что тема курсора, используемая в GNOME, непоследодвательна (not consistent). Например, она может меняться при перемещении курсора между различными окнами приложений. Чтобы исправить ситуацию, настройте тему курсора, создав файл `index.theme`, описывающий тему курсора согласно спецификации темы иконок XDG. Смотрите раздел [Темы курсора#Спецификация XDG](/index.php/%D0%A2%D0%B5%D0%BC%D1%8B_%D0%BA%D1%83%D1%80%D1%81%D0%BE%D1%80%D0%B0#.D0.A1.D0.BF.D0.B5.D1.86.D0.B8.D1.84.D0.B8.D0.BA.D0.B0.D1.86.D0.B8.D1.8F_XDG "Темы курсора").

### Tracker и Документы не видят любые локальные файлы

Чтобы Tracker (и, следовательно, Документы) мог видеть ваши локальные файлы, они должны находиться в каталогах, которые им известны. Если ваши документы расположены в одном из стандартных каталогов XDG (например, "Документы" или "Музыка"), вам необходимо установить пакет [xdg-user-dirs](https://www.archlinux.org/packages/?name=xdg-user-dirs) и выполнить команду:

```
 # xdg-user-dirs-update

```

Она создаст все обычные домашние каталоги XDG, если они ещё не существуют, а также конфигурационный файл, описывающий эти каталоги, необходимые для Tracker'а и Документов.

### Не запоминаются пароли

Если после каждого входа в систему вы получаете приглашение на ввод пароля и видите, что пароль не сохраняется, возможно, вам необходимо создать/настроить связку ключей по умолчанию.

Установите пакет [seahorse](https://www.archlinux.org/packages/?name=seahorse). Откройте "Пароли и ключи" в меню или выполните команду `seahorse`. Выберите Вид > По связке ключей. Если в левой колонке нет связки ключей (будет показана иконка блокировки), зайдите в Файл > Новая > Связка ключей и присвойте хорошее имя. Появится запрос на ввод пароля. Если вы его не зададите, связка будет автоматически разблокироваться при использовании автовхода, но пароли при этом будут храниться небезопасно. Наконец, нажмите правой кнопкой мыши на только что созданной связке и выберите "Установить по умолчанию".

### Невозможно перетаскивать окна с помощью Alt-Key + кнопка мыши

Измените настройку dconf "org.gnome.desktop.wm.preferences.mouse-button-modifier" с <Super> на <Alt>. Невозможно изменить её с помощью *Параметры системы* > "Клавиатура" > "Горячие клавиши", здесь вы найдёте лишь обычные сочетания клавиш. Разработчики GNOME решили изменить это в версии 3.6 из-за этого баг-репорта [https://bugzilla.gnome.org/show_bug.cgi?id=607797](https://bugzilla.gnome.org/show_bug.cgi?id=607797).

### Gnome-shell 3.8.x не загружается, появляются лишь черный экран и курсор

Если у вас включен язык с кодировкой, отличной от UTF8, Gnome 3 может не загружаться. Выключите локали не-UTF-8 и запустите locale-gen. Для получения дополнительной информации смотрите [этот баг-репорт](https://bugzilla.gnome.org/show_bug.cgi?id=698952).

Также, если включены несколько локалей разных языков, может быть необходимым отключить все локали, кроме одной (в кодировке UTF-8).

### Видео tear-free с графикой Intel HD

Включение [Xorg Intel опции TearFree](/index.php/Intel_graphics#Tear-free_video "Intel graphics") - известное рабочее решение проблемы тиринга на адаптерах Intel, однако то, как работает эта функция, делает ее излишней при использовании композитора (увеличивает потребление памяти и снижает производительность, смотрите [оригинальный последний комментарий баг-репорта](https://bugs.freedesktop.org/show_bug.cgi?id=37686#c123)).

С другой стороны, GNOME Shell в качестве композитного менеджера использует Mutter, у которого есть опция для решения проблемы тиринга (смотрите [оригинальное предложение для исправления](https://bugzilla.gnome.org/show_bug.cgi?id=657071#c1) и его упоминание в [баг-репорте Freedesktop](https://bugs.freedesktop.org/show_bug.cgi?id=37686#c59)): строка `CLUTTER_PAINT=disable-clipped-redraws:disable-culling` должна быть добавлена в `/etc/environment` с последующим перезапуском сервера Xorg. Эта настройка решает проблему тиринга.

### Вход в систему при помощи GDM или lightdm быстро возвращает экран входа в систему без какой-либо реакции

Как обнаружил некто в [этой](http://forums.debian.net/viewtopic.php?f=6&t=84115) ветке, кажется, эту проблему вызывает какой-то аспект проверки на существование и сборки скрипта bash_completion. В дополнение к настройке bash completion в пакете [bash-completion](https://www.archlinux.org/packages/?name=bash-completion), Ruby Version Manager (RVM) включает в себя вызов скрипта bash completion как части его инициализации. Стоит иметь в виду, что причины, по которым эта проблема существует, находятся за пределами области скриптов bash completion, и в /etc/profile* по-прежнему стоит поковыряться при отладке, даже если скрипт автодополнения не найден.

### Системные иконки Gnome не подгружаются корректно

Проблемы с загрузкой системных иконок, например, в заголовке Files, можно решить [(пере)установкой](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.BE.D0.BF.D1.80.D0.B5.D0.B4.D0.B5.D0.BB.D0.B5.D0.BD.D0.BD.D1.8B.D1.85_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.BE.D0.B2 "Pacman (Русский)") пакета [gdk-pixbuf2](https://www.archlinux.org/packages/?name=gdk-pixbuf2).

Также это может исправить появление экрана "oh no" и/или очень медленную загрузку и вход в систему GDM, как написано в [этой](https://bbs.archlinux.org/viewtopic.php?pid=1414157) ветке форума.

### Искажения при разворачивании окон на весь экран

В GNOME 3.12.0 разворачивание окон на весь экран может вызывать искажения [[4]](https://bbs.archlinux.org/viewtopic.php?id=183617) [[5]](https://bugzilla.gnome.org/show_bug.cgi?id=728385). Смотрите раздел [#Видео tear-free с графикой Intel HD](#.D0.92.D0.B8.D0.B4.D0.B5.D0.BE_tear-free_.D1.81_.D0.B3.D1.80.D0.B0.D1.84.D0.B8.D0.BA.D0.BE.D0.B9_Intel_HD).

## Смотрите также

*   [Официальный веб-сайт GNOME](http://www.gnome.org/)
*   [Расширения для GNOME-shell](http://extensions.gnome.org/)
*   Темы, иконки и фоновые изображения:
    *   [GNOME Art](http://art.gnome.org/)
    *   [GNOME Look](http://www.gnome-look.org/)
*   Программы GTK/GNOME:
    *   [GNOME Files](http://www.gnomefiles.org/)
    *   [GNOME Project Listing](http://www.gnome.org/projects/)