# Xfce (Русский)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Ссылки по теме

*   [Среда рабочего стола](/index.php/%D0%A1%D1%80%D0%B5%D0%B4%D0%B0_%D1%80%D0%B0%D0%B1%D0%BE%D1%87%D0%B5%D0%B3%D0%BE_%D1%81%D1%82%D0%BE%D0%BB%D0%B0 "Среда рабочего стола")
*   [Оконный менеджер](/index.php/%D0%9E%D0%BA%D0%BE%D0%BD%D0%BD%D1%8B%D0%B9_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80 "Оконный менеджер")
*   [Xfwm](/index.php/Xfwm "Xfwm")
*   [Thunar (Русский)](/index.php/Thunar_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Thunar (Русский)")
*   [LXDE (Русский)](/index.php/LXDE_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "LXDE (Русский)")
*   [GNOME (Русский)](/index.php/GNOME_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GNOME (Русский)")

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

**Эта страница нуждается в сопроводителе**

Статья не гарантирует актуальность информации. Помогите русскоязычному сообществу поддержкой подобных страниц. См. [Команда переводчиков ArchWiki](/index.php/%D0%9A%D0%BE%D0%BC%D0%B0%D0%BD%D0%B4%D0%B0_%D0%BF%D0%B5%D1%80%D0%B5%D0%B2%D0%BE%D0%B4%D1%87%D0%B8%D0%BA%D0%BE%D0%B2_ArchWiki "Команда переводчиков ArchWiki")

[Xfce](http://www.xfce.org) — легковесная модульная [среда рабочего стола](/index.php/%D0%A1%D1%80%D0%B5%D0%B4%D0%B0_%D1%80%D0%B0%D0%B1%D0%BE%D1%87%D0%B5%D0%B3%D0%BE_%D1%81%D1%82%D0%BE%D0%BB%D0%B0 "Среда рабочего стола"), на данный момент работающая на основе на GTK+ 2\. Она включает в себя оконный менеджер, файловый менеджер, рабочий стол и основную панель.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Запуск Xfce](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_Xfce)
    *   [2.1 Вход через интерфейс](#.D0.92.D1.85.D0.BE.D0.B4_.D1.87.D0.B5.D1.80.D0.B5.D0.B7_.D0.B8.D0.BD.D1.82.D0.B5.D1.80.D1.84.D0.B5.D0.B9.D1.81)
    *   [2.2 Виртуальная консоль](#.D0.92.D0.B8.D1.80.D1.82.D1.83.D0.B0.D0.BB.D1.8C.D0.BD.D0.B0.D1.8F_.D0.BA.D0.BE.D0.BD.D1.81.D0.BE.D0.BB.D1.8C)
*   [3 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [3.1 Меню](#.D0.9C.D0.B5.D0.BD.D1.8E)
        *   [3.1.1 Whisker Menu](#Whisker_Menu)
        *   [3.1.2 Редактирование записей](#.D0.A0.D0.B5.D0.B4.D0.B0.D0.BA.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.B7.D0.B0.D0.BF.D0.B8.D1.81.D0.B5.D0.B9)
    *   [3.2 Рабочий стол](#.D0.A0.D0.B0.D0.B1.D0.BE.D1.87.D0.B8.D0.B9_.D1.81.D1.82.D0.BE.D0.BB)
        *   [3.2.1 Прозрачный фон для подписей значков](#.D0.9F.D1.80.D0.BE.D0.B7.D1.80.D0.B0.D1.87.D0.BD.D1.8B.D0.B9_.D1.84.D0.BE.D0.BD_.D0.B4.D0.BB.D1.8F_.D0.BF.D0.BE.D0.B4.D0.BF.D0.B8.D1.81.D0.B5.D0.B9_.D0.B7.D0.BD.D0.B0.D1.87.D0.BA.D0.BE.D0.B2)
        *   [3.2.2 Скрытие разделов](#.D0.A1.D0.BA.D1.80.D1.8B.D1.82.D0.B8.D0.B5_.D1.80.D0.B0.D0.B7.D0.B4.D0.B5.D0.BB.D0.BE.D0.B2)
        *   [3.2.3 Убрать пункты Thunar из контекстного меню](#.D0.A3.D0.B1.D1.80.D0.B0.D1.82.D1.8C_.D0.BF.D1.83.D0.BD.D0.BA.D1.82.D1.8B_Thunar_.D0.B8.D0.B7_.D0.BA.D0.BE.D0.BD.D1.82.D0.B5.D0.BA.D1.81.D1.82.D0.BD.D0.BE.D0.B3.D0.BE_.D0.BC.D0.B5.D0.BD.D1.8E)
        *   [3.2.4 Комбинация клавиш для закрытия окон](#.D0.9A.D0.BE.D0.BC.D0.B1.D0.B8.D0.BD.D0.B0.D1.86.D0.B8.D1.8F_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D1.88_.D0.B4.D0.BB.D1.8F_.D0.B7.D0.B0.D0.BA.D1.80.D1.8B.D1.82.D0.B8.D1.8F_.D0.BE.D0.BA.D0.BE.D0.BD)
    *   [3.3 Сеанс Xfce](#.D0.A1.D0.B5.D0.B0.D0.BD.D1.81_Xfce)
        *   [3.3.1 Автозапуск приложений](#.D0.90.D0.B2.D1.82.D0.BE.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D0.B9)
        *   [3.3.2 Блокировка экрана](#.D0.91.D0.BB.D0.BE.D0.BA.D0.B8.D1.80.D0.BE.D0.B2.D0.BA.D0.B0_.D1.8D.D0.BA.D1.80.D0.B0.D0.BD.D0.B0)
        *   [3.3.3 Переключение пользователей](#.D0.9F.D0.B5.D1.80.D0.B5.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D0.B5.D0.B9)
        *   [3.3.4 Отключение сохранения сеансов](#.D0.9E.D1.82.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D1.81.D0.BE.D1.85.D1.80.D0.B0.D0.BD.D0.B5.D0.BD.D0.B8.D1.8F_.D1.81.D0.B5.D0.B0.D0.BD.D1.81.D0.BE.D0.B2)
        *   [3.3.5 Оконный менеджер по умолчанию](#.D0.9E.D0.BA.D0.BE.D0.BD.D0.BD.D1.8B.D0.B9_.D0.BC.D0.B5.D0.BD.D0.B5.D0.B4.D0.B6.D0.B5.D1.80_.D0.BF.D0.BE_.D1.83.D0.BC.D0.BE.D0.BB.D1.87.D0.B0.D0.BD.D0.B8.D1.8E)
    *   [3.4 Темы](#.D0.A2.D0.B5.D0.BC.D1.8B)
        *   [3.4.1 Согласованность компонентов](#.D0.A1.D0.BE.D0.B3.D0.BB.D0.B0.D1.81.D0.BE.D0.B2.D0.B0.D0.BD.D0.BD.D0.BE.D1.81.D1.82.D1.8C_.D0.BA.D0.BE.D0.BC.D0.BF.D0.BE.D0.BD.D0.B5.D0.BD.D1.82.D0.BE.D0.B2)
        *   [3.4.2 Курсоры мыши](#.D0.9A.D1.83.D1.80.D1.81.D0.BE.D1.80.D1.8B_.D0.BC.D1.8B.D1.88.D0.B8)
        *   [3.4.3 Значки](#.D0.97.D0.BD.D0.B0.D1.87.D0.BA.D0.B8)
        *   [3.4.4 Шрифты](#.D0.A8.D1.80.D0.B8.D1.84.D1.82.D1.8B)
    *   [3.5 Звук](#.D0.97.D0.B2.D1.83.D0.BA)
        *   [3.5.1 Настройка xfce4-mixer](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_xfce4-mixer)
        *   [3.5.2 Xfce4-mixer и OSS4](#Xfce4-mixer_.D0.B8_OSS4)
        *   [3.5.3 Xfce4-mixer и pulseaudio](#Xfce4-mixer_.D0.B8_pulseaudio)
        *   [3.5.4 Звуковые мультимедиа-клавиши](#.D0.97.D0.B2.D1.83.D0.BA.D0.BE.D0.B2.D1.8B.D0.B5_.D0.BC.D1.83.D0.BB.D1.8C.D1.82.D0.B8.D0.BC.D0.B5.D0.B4.D0.B8.D0.B0-.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D1.88.D0.B8)
            *   [3.5.4.1 ALSA](#ALSA)
            *   [3.5.4.2 PulseAudio](#PulseAudio)
            *   [3.5.4.3 OSS](#OSS)
            *   [3.5.4.4 Xfce4-volumed](#Xfce4-volumed)
            *   [3.5.4.5 Volumeicon](#Volumeicon)
            *   [3.5.4.6 Специальные клавиши](#.D0.A1.D0.BF.D0.B5.D1.86.D0.B8.D0.B0.D0.BB.D1.8C.D0.BD.D1.8B.D0.B5_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D1.88.D0.B8)
        *   [3.5.5 Добавление звука запуска системы](#.D0.94.D0.BE.D0.B1.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B7.D0.B2.D1.83.D0.BA.D0.B0_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA.D0.B0_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.8B)
    *   [3.6 Сочетания клавиш](#.D0.A1.D0.BE.D1.87.D0.B5.D1.82.D0.B0.D0.BD.D0.B8.D1.8F_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D1.88)
        *   [3.6.1 Сложные сочетания](#.D0.A1.D0.BB.D0.BE.D0.B6.D0.BD.D1.8B.D0.B5_.D1.81.D0.BE.D1.87.D0.B5.D1.82.D0.B0.D0.BD.D0.B8.D1.8F)
    *   [3.7 Агент аутентификаци Polkit](#.D0.90.D0.B3.D0.B5.D0.BD.D1.82_.D0.B0.D1.83.D1.82.D0.B5.D0.BD.D1.82.D0.B8.D1.84.D0.B8.D0.BA.D0.B0.D1.86.D0.B8_Polkit)
*   [4 Советы и рекомендации](#.D0.A1.D0.BE.D0.B2.D0.B5.D1.82.D1.8B_.D0.B8_.D1.80.D0.B5.D0.BA.D0.BE.D0.BC.D0.B5.D0.BD.D0.B4.D0.B0.D1.86.D0.B8.D0.B8)
    *   [4.1 Интеграция с xdg-open (предпочтительные приложения)](#.D0.98.D0.BD.D1.82.D0.B5.D0.B3.D1.80.D0.B0.D1.86.D0.B8.D1.8F_.D1.81_xdg-open_.28.D0.BF.D1.80.D0.B5.D0.B4.D0.BF.D0.BE.D1.87.D1.82.D0.B8.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D1.8B.D0.B5_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F.29)
    *   [4.2 Скриншоты](#.D0.A1.D0.BA.D1.80.D0.B8.D0.BD.D1.88.D0.BE.D1.82.D1.8B)
        *   [4.2.1 Клавиша Print Screen](#.D0.9A.D0.BB.D0.B0.D0.B2.D0.B8.D1.88.D0.B0_Print_Screen)
    *   [4.3 Блокировка клавиш F1 и F11 в терминале](#.D0.91.D0.BB.D0.BE.D0.BA.D0.B8.D1.80.D0.BE.D0.B2.D0.BA.D0.B0_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D1.88_F1_.D0.B8_F11_.D0.B2_.D1.82.D0.B5.D1.80.D0.BC.D0.B8.D0.BD.D0.B0.D0.BB.D0.B5)
    *   [4.4 Цветовые схемы терминала](#.D0.A6.D0.B2.D0.B5.D1.82.D0.BE.D0.B2.D1.8B.D0.B5_.D1.81.D1.85.D0.B5.D0.BC.D1.8B_.D1.82.D0.B5.D1.80.D0.BC.D0.B8.D0.BD.D0.B0.D0.BB.D0.B0)
        *   [4.4.1 Изменение стандартной цветовой схемы](#.D0.98.D0.B7.D0.BC.D0.B5.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D1.81.D1.82.D0.B0.D0.BD.D0.B4.D0.B0.D1.80.D1.82.D0.BD.D0.BE.D0.B9_.D1.86.D0.B2.D0.B5.D1.82.D0.BE.D0.B2.D0.BE.D0.B9_.D1.81.D1.85.D0.B5.D0.BC.D1.8B)
        *   [4.4.2 Цветовая схема tango](#.D0.A6.D0.B2.D0.B5.D1.82.D0.BE.D0.B2.D0.B0.D1.8F_.D1.81.D1.85.D0.B5.D0.BC.D0.B0_tango)
    *   [4.5 Цветовые профили](#.D0.A6.D0.B2.D0.B5.D1.82.D0.BE.D0.B2.D1.8B.D0.B5_.D0.BF.D1.80.D0.BE.D1.84.D0.B8.D0.BB.D0.B8)
        *   [4.5.1 Загрузка профиля](#.D0.97.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B0_.D0.BF.D1.80.D0.BE.D1.84.D0.B8.D0.BB.D1.8F)
        *   [4.5.2 Создание профиля](#.D0.A1.D0.BE.D0.B7.D0.B4.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D1.84.D0.B8.D0.BB.D1.8F)
    *   [4.6 Несколько мониторов](#.D0.9D.D0.B5.D1.81.D0.BA.D0.BE.D0.BB.D1.8C.D0.BA.D0.BE_.D0.BC.D0.BE.D0.BD.D0.B8.D1.82.D0.BE.D1.80.D0.BE.D0.B2)
    *   [4.7 Пользовательские каталоги XDG](#.D0.9F.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D1.8C.D1.81.D0.BA.D0.B8.D0.B5_.D0.BA.D0.B0.D1.82.D0.B0.D0.BB.D0.BE.D0.B3.D0.B8_XDG)
    *   [4.8 SSH Agents](#SSH_Agents)
    *   [4.9 Bluetooth](#Bluetooth)
    *   [4.10 Прокрутка в фоновом окне без фокусировки на нем](#.D0.9F.D1.80.D0.BE.D0.BA.D1.80.D1.83.D1.82.D0.BA.D0.B0_.D0.B2_.D1.84.D0.BE.D0.BD.D0.BE.D0.B2.D0.BE.D0.BC_.D0.BE.D0.BA.D0.BD.D0.B5_.D0.B1.D0.B5.D0.B7_.D1.84.D0.BE.D0.BA.D1.83.D1.81.D0.B8.D1.80.D0.BE.D0.B2.D0.BA.D0.B8_.D0.BD.D0.B0_.D0.BD.D0.B5.D0.BC)
    *   [4.11 Прозрачность активного окна](#.D0.9F.D1.80.D0.BE.D0.B7.D1.80.D0.B0.D1.87.D0.BD.D0.BE.D1.81.D1.82.D1.8C_.D0.B0.D0.BA.D1.82.D0.B8.D0.B2.D0.BD.D0.BE.D0.B3.D0.BE_.D0.BE.D0.BA.D0.BD.D0.B0)
*   [5 Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [5.1 Отсутствующие значки на кнопках действий](#.D0.9E.D1.82.D1.81.D1.83.D1.82.D1.81.D1.82.D0.B2.D1.83.D1.8E.D1.89.D0.B8.D0.B5_.D0.B7.D0.BD.D0.B0.D1.87.D0.BA.D0.B8_.D0.BD.D0.B0_.D0.BA.D0.BD.D0.BE.D0.BF.D0.BA.D0.B0.D1.85_.D0.B4.D0.B5.D0.B9.D1.81.D1.82.D0.B2.D0.B8.D0.B9)
    *   [5.2 Сбиваются позиции ярлыков рабочего стола](#.D0.A1.D0.B1.D0.B8.D0.B2.D0.B0.D1.8E.D1.82.D1.81.D1.8F_.D0.BF.D0.BE.D0.B7.D0.B8.D1.86.D0.B8.D0.B8_.D1.8F.D1.80.D0.BB.D1.8B.D0.BA.D0.BE.D0.B2_.D1.80.D0.B0.D0.B1.D0.BE.D1.87.D0.B5.D0.B3.D0.BE_.D1.81.D1.82.D0.BE.D0.BB.D0.B0)
    *   [5.3 Темы GTK не работают с несколькими мониторами](#.D0.A2.D0.B5.D0.BC.D1.8B_GTK_.D0.BD.D0.B5_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.B0.D1.8E.D1.82_.D1.81_.D0.BD.D0.B5.D1.81.D0.BA.D0.BE.D0.BB.D1.8C.D0.BA.D0.B8.D0.BC.D0.B8_.D0.BC.D0.BE.D0.BD.D0.B8.D1.82.D0.BE.D1.80.D0.B0.D0.BC.D0.B8)
    *   [5.4 HTML-файлы не открываются корректно в Firefox](#HTML-.D1.84.D0.B0.D0.B9.D0.BB.D1.8B_.D0.BD.D0.B5_.D0.BE.D1.82.D0.BA.D1.80.D1.8B.D0.B2.D0.B0.D1.8E.D1.82.D1.81.D1.8F_.D0.BA.D0.BE.D1.80.D1.80.D0.B5.D0.BA.D1.82.D0.BD.D0.BE_.D0.B2_Firefox)
    *   [5.5 Значки не появляются в контекстных меню](#.D0.97.D0.BD.D0.B0.D1.87.D0.BA.D0.B8_.D0.BD.D0.B5_.D0.BF.D0.BE.D1.8F.D0.B2.D0.BB.D1.8F.D1.8E.D1.82.D1.81.D1.8F_.D0.B2_.D0.BA.D0.BE.D0.BD.D1.82.D0.B5.D0.BA.D1.81.D1.82.D0.BD.D1.8B.D1.85_.D0.BC.D0.B5.D0.BD.D1.8E)
    *   [5.6 Настройки клавиатуры не сохраняются в xkb-plugin](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B8_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D0.B0.D1.82.D1.83.D1.80.D1.8B_.D0.BD.D0.B5_.D1.81.D0.BE.D1.85.D1.80.D0.B0.D0.BD.D1.8F.D1.8E.D1.82.D1.81.D1.8F_.D0.B2_xkb-plugin)
    *   [5.7 GDM игнорирует локали](#GDM_.D0.B8.D0.B3.D0.BD.D0.BE.D1.80.D0.B8.D1.80.D1.83.D0.B5.D1.82_.D0.BB.D0.BE.D0.BA.D0.B0.D0.BB.D0.B8)
    *   [5.8 В меню отсутствуют приложения Wine](#.D0.92_.D0.BC.D0.B5.D0.BD.D1.8E_.D0.BE.D1.82.D1.81.D1.83.D1.82.D1.81.D1.82.D0.B2.D1.83.D1.8E.D1.82_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F_Wine)
    *   [5.9 Повторный вход в спящий режим](#.D0.9F.D0.BE.D0.B2.D1.82.D0.BE.D1.80.D0.BD.D1.8B.D0.B9_.D0.B2.D1.85.D0.BE.D0.B4_.D0.B2_.D1.81.D0.BF.D1.8F.D1.89.D0.B8.D0.B9_.D1.80.D0.B5.D0.B6.D0.B8.D0.BC)
    *   [5.10 Некорректное отображение символов при монтировании USB-накопителей](#.D0.9D.D0.B5.D0.BA.D0.BE.D1.80.D1.80.D0.B5.D0.BA.D1.82.D0.BD.D0.BE.D0.B5_.D0.BE.D1.82.D0.BE.D0.B1.D1.80.D0.B0.D0.B6.D0.B5.D0.BD.D0.B8.D0.B5_.D1.81.D0.B8.D0.BC.D0.B2.D0.BE.D0.BB.D0.BE.D0.B2_.D0.BF.D1.80.D0.B8_.D0.BC.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B8_USB-.D0.BD.D0.B0.D0.BA.D0.BE.D0.BF.D0.B8.D1.82.D0.B5.D0.BB.D0.B5.D0.B9)
    *   [5.11 NVIDIA и xfce4-sensors-plugin](#NVIDIA_.D0.B8_xfce4-sensors-plugin)
    *   [5.12 Отключение экрана](#.D0.9E.D1.82.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D1.8D.D0.BA.D1.80.D0.B0.D0.BD.D0.B0)
    *   [5.13 Настройки предпочтений не работают](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B8_.D0.BF.D1.80.D0.B5.D0.B4.D0.BF.D0.BE.D1.87.D1.82.D0.B5.D0.BD.D0.B8.D0.B9_.D0.BD.D0.B5_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.B0.D1.8E.D1.82)
    *   [5.14 Лишний пункт в контекстном меню рабочего стола](#.D0.9B.D0.B8.D1.88.D0.BD.D0.B8.D0.B9_.D0.BF.D1.83.D0.BD.D0.BA.D1.82_.D0.B2_.D0.BA.D0.BE.D0.BD.D1.82.D0.B5.D0.BA.D1.81.D1.82.D0.BD.D0.BE.D0.BC_.D0.BC.D0.B5.D0.BD.D1.8E_.D1.80.D0.B0.D0.B1.D0.BE.D1.87.D0.B5.D0.B3.D0.BE_.D1.81.D1.82.D0.BE.D0.BB.D0.B0)
    *   [5.15 Восстановление стандартных настроек](#.D0.92.D0.BE.D1.81.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D1.81.D1.82.D0.B0.D0.BD.D0.B4.D0.B0.D1.80.D1.82.D0.BD.D1.8B.D1.85_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B5.D0.BA)
    *   [5.16 Отказ сеанса](#.D0.9E.D1.82.D0.BA.D0.B0.D0.B7_.D1.81.D0.B5.D0.B0.D0.BD.D1.81.D0.B0)
*   [6 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") Xfce с группой [xfce4](https://www.archlinux.org/groups/x86_64/xfce4/), доступной в [официальных репозиториях](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)"). Вам также может понадобиться установить группу [xfce4-goodies](https://www.archlinux.org/groups/x86_64/xfce4-goodies/), которая включает дополнительные плагины и полезные утилиты, таких как редактор [mousepad](https://www.archlinux.org/packages/?name=mousepad). В качестве оконного менеджера по умолчанию используется [Xfwm](/index.php/Xfwm "Xfwm").

## Запуск Xfce

### Вход через интерфейс

В меню [экранного менеджера](/index.php/Display_manager_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Display manager (Русский)") выберите _Xfce Session_.

### Виртуальная консоль

Добавьте `exec startxfce4` в [~/.xinitrc](/index.php/~/.xinitrc "~/.xinitrc").

**Обратите внимание:** Не используйтe скрипт `xfce4-session`; `startxfce4` действительно та самая команда, которая вам нужна и которая в свою очередь вызовет этот скрипт когда надо.

## Настройка

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**Эта статья или раздел нуждается в улучшении грамматики, форматирования или стиля.**

**Причина:** Повторы, излишняя сложность, плохой стиль. (обсуждение: [Talk:Xfce (Русский)#](https://wiki.archlinux.org/index.php/Talk:Xfce_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)))

Xfce хранит настройки в [Xfconf](http://docs.xfce.org/xfce/xfconf/start). Есть несколько способов их отредактировать:

*   В главном меню, выберите [Settings](http://docs.xfce.org/xfce/xfce4-settings/start) и ту категорию, которую вы хотите настроить. Категории — это программы, обычно располагающиеся в `/usr/bin/xfce4-*` или `/usr/bin/xfdesktop-settings`.
*   Утилита `xfce4-settings-editor` дает возможность просмотреть и настроить все опции. Отредактированные параметры сразу вступают в силу. Используйте `xfconf-query`, чтобы изменять настройки через командную строку; подробнее см. в [документации](http://docs.xfce.org/xfce/xfconf/xfconf-query).
*   Настройки хранятся в xml-файлах в `~/.config/xfce4/xfconf/xfce-perchannel-xml/`, которые могут быть отредактированы вручную. Однако, изменения здесь не вступают в силу сразу после сохранения.

### Меню

#### Whisker Menu

[xfce4-whiskermenu-plugin](https://www.archlinux.org/packages/?name=xfce4-whiskermenu-plugin), доступный в [официальных репозиториях](/index.php/%D0%9E%D1%84%D0%B8%D1%86%D0%B8%D0%B0%D0%BB%D1%8C%D0%BD%D1%8B%D1%85_%D1%80%D0%B5%D0%BF%D0%BE%D0%B7%D0%B8%D1%82%D0%BE%D1%80%D0%B8%D1%8F%D1%85 "Официальных репозиториях") представляет собой полноценное альтернативное стартовое меню для запуска приложений. Оно умеет отображать список избранных программ, а также списки всех установленных программ по категориям.

#### Редактирование записей

Чтобы скрыть пункт меню, добавьте `NoDisplay=true` в соответствующую секцию [desktop entries](/index.php/Desktop_entries "Desktop entries"). Вы можете скопировать запись из `/usr/share/applications` в `.local/share/applications`, чтобы создать настройки для конкретного пользователя, и избежать перезаписи своих изменений в общем файле при установке обновлений для программ.

Вы также можете изменить категорию приложения, изменяя значение параметра `Categories=` в файлах _.desktop_.

Альтернативным способом является создание файла конфигурации `~/.config/menus/xfce-applications.menu`:

```
<!DOCTYPE Menu PUBLIC "-//freedesktop//DTD Menu 1.0//EN"
  "http://www.freedesktop.org/standards/menu-spec/1.0/menu.dtd">

<Menu>
    <Name>Xfce</Name>
    <MergeFile type="parent">/etc/xdg/menus/xfce-applications.menu</MergeFile>

    <Exclude>
        <Filename>xfce4-run.desktop</Filename>
        <Filename>exo-terminal-emulator.desktop</Filename>
        <Filename>exo-file-manager.desktop</Filename>
        <Filename>exo-mail-reader.desktop</Filename>
        <Filename>exo-web-browser.desktop</Filename>
        <Filename>xfce4-about.desktop</Filename>
        <Filename>xfhelp4.desktop</Filename>
    </Exclude>

    <Layout>
        <Merge type="all"/>
        <Separator/>
        <Menuname>Settings</Menuname>
        <Separator/>
        <Filename>xfce4-session-logout.desktop</Filename>
    </Layout>
</Menu>

```

Тег `<MergeFile>` включает конфигурацию стандартного меню Xfce в наш файл.

Тег `<Exclude>` содержит список исключения для тех приложений, которые вы не хотите видеть в меню. Здесь мы исключили некоторые стандартные ярлыки Xfce, но вы также можете исключить любое другое приложение, например `firefox.desktop`.

Тег `<Layout>` определяет внешний вид меню: состав и расположение элементов. Приложения можно сгруппировать в папки или любым другим образом. Подробнее см. на странице [Xfce wiki](http://wiki.xfce.org/howto/customize-menu).

Отдельные инструменты также доступны для настройки меню:

*   **XAME** — инструмент с графическим интерфейсом, написанный на языке [Gambas](/index.php/Gambas "Gambas") и разработанный специально для настройки меню в Xfce. В других средах рабочего стола работать не будет.

[http://www.redsquirrel87.com/XAME.html](http://www.redsquirrel87.com/XAME.html) || [xame](https://aur.archlinux.org/packages/xame/)<sup><small>AUR</small></sup>

*   **menulibre** — расширенный редактор меню, предоставляющий современные возможности в простом и легком для использования интерфейсе.

[https://launchpad.net/menulibre](https://launchpad.net/menulibre) || [menulibre](https://aur.archlinux.org/packages/menulibre/)<sup><small>AUR</small></sup>

*   **alacarte** — pедактор меню для GNOME

[http://www.gnome.org/](http://www.gnome.org/) || [alacarte](https://www.archlinux.org/packages/?name=alacarte)

**Обратите внимание:** Если запись содержит `OnlyShowIn=Xfce;`, она не появится в _alacarte_. Аналогично, записи с `OnlyShowIn=GNOME;` не будут отображены в меню Xfce. Пакеты [alacarte-xfce](https://aur.archlinux.org/packages/alacarte-xfce/)<sup><small>AUR</small></sup> и [alacarte-lxde](https://aur.archlinux.org/packages/alacarte-lxde/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/alacarte-lxde)]</sup> созданы для решения этой проблемы; последний будет работать внутри и вне [LXDE](/index.php/LXDE_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "LXDE (Русский)")

### Рабочий стол

#### Прозрачный фон для подписей значков

Чтобы изменить стандартный белый фон текстовых подписей значков рабочего стола на что-нибудь более подходящее, добавьте в файл `~/.gtkrc-2.0` следюущие строки:

```
style "xfdesktop-icon-view" {
    XfdesktopIconView::label-alpha = 10
    base[NORMAL] = "#000000"
    base[SELECTED] = "#71B9FF"
    base[ACTIVE] = "#71B9FF"
    fg[NORMAL] = "#fcfcfc"
    fg[SELECTED] = "#ffffff"
    fg[ACTIVE] = "#ffffff"
}
widget_class "*XfdesktopIconView*" style "xfdesktop-icon-view"

```

#### Скрытие разделов

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**Эта статья или раздел является кандидатом на объединение с [udev (Русский)](/index.php/Udev_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Udev (Русский)").**

**Причина:** пожалуйста, используйте второй аргумент шаблона для указания причины. (обсуждение: [Talk:Xfce (Русский)#](https://wiki.archlinux.org/index.php/Talk:Xfce_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)))

Если вы не хотите, чтобы конкретные разделы или дисковые устройства появлялись на рабочем столе, вы можете создать следующее правило [udev](/index.php/Udev_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Udev (Русский)"), например `/etc/udev/rules.d/10-local.rules`:

```
KERNEL=="sda1", ENV{UDISKS_PRESENTATION_HIDE}="1"
KERNEL=="sda2", ENV{UDISKS_PRESENTATION_HIDE}="1"

```

Разделы `sda1` и `sda2` теперь будут убраны с рабочего стола. Обратите внимание, что если вы используете [udisks2](https://www.archlinux.org/packages/?name=udisks2), этот способ не сработает, так как `UDISKS_PRESENTATION_HIDE` больше не поддерживается. Вместо этого, используйте `UDISKS_IGNORE`:

```
KERNEL=="sda1", ENV{UDISKS_IGNORE}="1"
KERNEL=="sda2", ENV{UDISKS_IGNORE}="1"

```

#### Убрать пункты Thunar из контекстного меню

Для того, чтобы убрать пункты Thunar из меню, вызываемого кликом правой кнопкой мыши, выполните команду:

```
$ xfconf-query -c xfce4-desktop -v --create -p /desktop-icons/style -t int -s 0

```

#### Комбинация клавиш для закрытия окон

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

**Правильность информации, представленной в этой статье или разделе, оспаривается**

**Причина:** Нет пояснения, что команда делает кроме простого вызова `xkill`. (обсуждение: [Talk:Xfce (Русский)#](https://wiki.archlinux.org/index.php/Talk:Xfce_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)))

Xfce не поддерживает напрямую горячей клавиши для закрытия окна программы, но вы можете добавить его простым скриптом. Убедитесь, что пакет [xorg-xkill](https://www.archlinux.org/packages/?name=xorg-xkill) установлен.

Создайте скрипт в `~/.config/xfce4/killwindow.sh` со следующим содержимым и дайте ему права на выполнение:

```
xkill -id "`xprop -root -notype | sed -n '/^_NET_ACTIVE_WINDOW/ s/^.*# *\|\,.*$//g p'`"

```

И назначьте запуск скрипта по нажатию комбинации клавиш в меню _Settings > Keyboard_.

### Сеанс Xfce

#### Автозапуск приложений

Чтобы приложения запускались во время загрузки Xfce, зайдите в _Applications Menu > Settings > Settings Manager_, выберите _Session and Startup_ и откройте вкладку _Application Autostart_. Вы увидите список программ, которые запускаются при загрузке. Чтобы добавить новую программу, нажмите _Add_, заполните поля в появившемся окне, указав путь до исполняемого файла, который вы хотите запустить.

Также вы можете использовать скрипт для автозапуска. Он включает в себя инициализацию необходимых переменных среды.

*   Скопируйте файл `/etc/xdg/xfce4/xinitrc` в `~/.config/xfce4/`
*   Отредактируйте файл. Добавьте в него нужные вам команды, например:

```
source $HOME/.bashrc
# start rxvt-unicode server
urxvtd -q -o -f

```

#### Блокировка экрана

Чтобы заблокировать сеанс Xfce4 (с помощью `xflock4`), установите один из следующих пакетов: [xscreensaver](https://www.archlinux.org/packages/?name=xscreensaver), [gnome-screensaver](https://www.archlinux.org/packages/?name=gnome-screensaver), [slock](https://www.archlinux.org/packages/?name=slock) или [xlockmore](https://www.archlinux.org/packages/?name=xlockmore). Мы рекомендуем использовать [XScreenSaver](/index.php/XScreenSaver "XScreenSaver").

Также вы можете сделать локальную копию _xflock4_, например в `/usr/local/bin/xflock4`.

Чтобы изменить скринсейвер, или поменять его для приложений вроде Whisker Menu перейдите в _Properties > Behavior > Lock Screen_. Полный список доступных вариантов смотрите на странице [List of applications/Security#Screen lockers](/index.php/List_of_applications/Security#Screen_lockers "List of applications/Security").

#### Переключение пользователей

Xfce4 поддерживает переключение пользователей когда используется вместе с [экранным менеджером](/index.php/Display_manager_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Display manager (Русский)"), который имеет такую функциональность — например, [LightDM](/index.php/LightDM "LightDM") и [GDM](/index.php/GDM "GDM"). Подробную информацию о них смотрите на wiki-страницах. Когда вы установите и правильно настроите экранный менеджер, вы сможете переключаться между пользователями в системе с помощью пункта меню 'action buttons' на панели.

#### Отключение сохранения сеансов

Xfce имеет специальный режим kiosk (_kiosk mode_), в котором вы можете легко заблокировать сохранение сеансов при выходе из системы. Создайте при необходимости и отредактируйте файл `/etc/xdg/xfce4/kiosk/kioskrc`, добавив в него следующее:

```
[xfce4-session]
SaveSession=NONE

```

Если режим kiosk не работает, вы также можете попробовать ограничить права на запись в каталог сессий:

```
$ rm ~/.cache/sessions/* && chmod 500 ~/.cache/sessions

```

Таким образом, при выходе Xfce просто не сможет сохранить в этот каталог параметры текущего сеанса.

#### Оконный менеджер по умолчанию

Оконный менеджер по умолчанию для всей системы устанавливается в файле `/etc/xdg/xfce4/xfconf/xfce-perchannel-xml/xfce4-session.xml`. Файл настроек конкретного пользователя может быть создан копированием системного файла:

```
$ cp /etc/xdg/xfce4/xfconf/xfce-perchannel-xml/xfce4-session.xml ~/.config/xfce4/xfconf/xfce-perchannel-xml/xfce4-session.xml

```

Внутри этих файлов оконный менеджер указан в параметре `Client0_Command`. Найдите строку, содержащую имя параметра; сразу после нее вы увидите значение этого параметра типа string:

```
<value type="string" value="'''xfwm4'''"/>

```

Измените значение атрибута `value` с _xfwm4_ на имя исполняемого файла оконного менеджера, который будет использоваться по умолчанию:

```
<value type="string" value="''имя_исполняемого_файла''"/>

```

**Обратите внимание:** Чтобы изменения вступили в силу, вам необходимо отключить сохранение сеансов перед тем, как выйти из системы. После того, как желаемый оконный менеджер будет запущен, вы можете снова включить сохранение сеансов.

Также, вы можете заменить [xfwm](/index.php/Xfwm "Xfwm") другим [оконным менеджером](/index.php/Window_manager_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Window manager (Русский)"), с помощью команды `_название_оконного_менеджера_ --replace`, указав вместо _название_оконного_менеджера_ название того менеджера окон, который вы хотите использовать — например, `metacity`

Если включено сохранение сеансов, выход из системы во время работы альтернативного менеджера окон приведет к тому, что этот же менеджер будет автоматически запущен при новом входе в систему.

Если вы не используете сохранение сеансов, вы можете добавить альтернативный менеджер окон в список автозагрузки Xfce. Чтобы это сделать, из главного меню перейдите в _Settings Manager > Session and Startup > Application Autostart_ и нажмите _Add_. Укажите команду для запуска желаемого оконного менеджера в поле _Command_, также задайте имя и описание. Нажмите _Ok_ для сохранения изменений, и перезайдите в систему чтобы увидеть результат.

**Обратите внимание:** Если вы используете список автозапуска программ для запуска альтернативного оконного менеджера, рекомендуется отключить сохранение сеансов. В противном случае, при входе в систему выбранный оконный менеджер может быть запущен дважды.

### Темы

Темы для Xfce доступны на сайте [[1]](http://www.xfce-look.org). Темы _Xfwm_ находятся в `/usr/share/themes/xfce4` и устанавливаются в меню _Settings > Window Manager_. Темы [GTK+](/index.php/GTK%2B_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GTK+ (Русский)") устанавливаются через меню _Settings > Appearance_.

#### Согласованность компонентов

Чтобы у приложений был единый схожий внешний вид рекомендуется использовать последние версии тем GTK+ 3, таких как, например, _Adwaita_, так как темы GTK+ 3 совместимы с приложениями GTK+ 2.

Подробнее см. в разделе [GTK+ 3.x](/index.php/GTK%2B_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A0.D0.B0.D0.B7.D0.BB.D0.B8.D1.87.D0.BD.D1.8B.D0.B5_.D1.82.D0.B5.D0.BC.D1.8B_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D0.B9_.D0.BC.D0.B5.D0.B6.D0.B4.D1.83_GTK.2B_2_.D0.B8_GTK.2B_3 "GTK+ (Русский)") для GTK+ 3 и [Uniform Look for Qt and GTK Applications](/index.php/Uniform_Look_for_Qt_and_GTK_Applications "Uniform Look for Qt and GTK Applications") для Qt.

#### Курсоры мыши

Смотрите на странице [Cursor themes](/index.php/Cursor_themes "Cursor themes"). Установить тему можно в меню _Settings > Mouse_.

#### Значки

Смотрите [значки](/index.php/Icons "Icons").

#### Шрифты

Смотрите [настройка шрифтов](/index.php/Font_configuration_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Font configuration (Русский)"). Установить шрифты в Xfce можно через меню _Settings > Appearance_.

### Звук

#### Настройка xfce4-mixer

[xfce4-mixer](https://www.archlinux.org/packages/?name=xfce4-mixer) — графический микшер и плагин для панели, разработанный командой Xfce. Является частью группы пакетов [xfce4](https://www.archlinux.org/groups/x86_64/xfce4/), поэтому, вероятно, уже установлен у вас. Xfce 4.6 использует [gstreamer](https://www.archlinux.org/packages/?name=gstreamer) как бэкэнд для управления уровнем звука, поэтому, сначала необходимо настроить совместную работу gstreamer и xfce4-mixer. Некоторые пакеты плагинов, перечисленные как опциональные для gstreamer, должны быть установлены. Без них, вы можете получать ошибку при клике на значок микшера на панели:

```
 GStreamer was unable to detect any sound devices. Some sound system specific GStreamer packages may be missing.

```

Какие именно плагины вам нужны, зависит от аппаратной части вашего компьютера. Большинству пользователей подойдет пакет [gstreamer0.10-base-plugins](https://www.archlinux.org/packages/?name=gstreamer0.10-base-plugins), который может быть [установлен](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.BE.D0.BF.D1.80.D0.B5.D0.B4.D0.B5.D0.BB.D0.B5.D0.BD.D0.BD.D1.8B.D1.85_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.BE.D0.B2 "Pacman (Русский)") из [официальных репозиториев](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)").

Если xfce4-mixer уже был запущен перед установкой одного из дополнительных пакетов, перезайдите в систему чтобы увидеть изменения, или просто удалите значок микшера с панели и добавьте его снова. Если установка плагина для gstreamer не помогла, возможно, вам нужны еще какие-нибудь плагины. Попробуйте [установить](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.BE.D0.BF.D1.80.D0.B5.D0.B4.D0.B5.D0.BB.D0.B5.D0.BD.D0.BD.D1.8B.D1.85_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.BE.D0.B2 "Pacman (Русский)") пакеты [gstreamer0.10-good-plugins](https://www.archlinux.org/packages/?name=gstreamer0.10-good-plugins) или [gstreamer0.10-bad-plugins](https://www.archlinux.org/packages/?name=gstreamer0.10-bad-plugins).

Если вам нужно поменять звуковую карту в микшере, перезайдите в систему, чтобы звук вновь появился.

Дополнительную информацию, например о том, как установить звуковую карту по умолчанию, смотрите в [Advanced Linux Sound Architecture](/index.php/Advanced_Linux_Sound_Architecture_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Advanced Linux Sound Architecture (Русский)"). Также вы можете использовать [PulseAudio](/index.php/PulseAudio_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "PulseAudio (Русский)") вместе с [pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol).

#### Xfce4-mixer и OSS4

Если прочтение предыдущего раздела не помогло вам настроить звук в xfce4-mixer, вероятно, вам нужно скомпилировать самостоятельно пакет [gstreamer0.10-good-plugins](https://www.archlinux.org/packages/?name=gstreamer0.10-good-plugins). Загрузите PKGBUILD и прочие необходимые файлы из [ABS](/index.php/Arch_Build_System_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch Build System (Русский)") или [отсюда](https://projects.archlinux.org/svntogit/packages.git/tree/gstreamer0.10-good/repos) и отредактируйте PKGBUILD, добавив опцию `--enable-oss`.

```
 ./configure --prefix=/usr --sysconfdir=/etc --localstatedir=/var \
   **--enable-oss \**
   --disable-static --enable-experimental \
   --disable-schemas-install \
   --disable-hal \
   --with-package-name="GStreamer Good Plugins (Archlinux)" \
   --with-package-origin="[https://www.archlinux.org/](https://www.archlinux.org/)"

```

теперь запустите

```
$ makepkg -i

```

Смотрите также [форум OSS](http://www.4front-tech.com/forum/).

#### Xfce4-mixer и pulseaudio

Откройте `xfce4-settings-editor`, перейдите в _xfce4-mixer_. Вероятно, вам захочется изменить значение _active-card_. Проверьте ниже _sound-cards_: вероятно, вы увидите несколько строк после нее, и одна из них должна быть похожа на нечто вроде **PlaybackInternalAudioAnalogStereoPulseAudioMixer**. Это и есть pulseaudio, распознанный Xfce. Так что все, что нужно сделать - выбрать его по умолчанию. Скопируйте строку и замените значения _active-card_ и _sound-card_. Может потребоваться перезагрузка или перезапуск xfce4-mixer.

#### Звуковые мультимедиа-клавиши

Зайдите в _Settings > Keyboard_, откройте вкладку _Application Shortcuts_, и добавьте новое сочетание клавиш нажатием _Add_. В подразделах приведены примеры команд, которые вы можете использовать для сочетания клавиш. В следующем окне нажмите соответствующую клавишу на клавиатуре для того, чтобы назначить ее для команды и нажмите _Ok_.

##### ALSA

Клавиша "Увеличить громкость":

```
amixer set Master 5%+

```

Клавиша "Уменьшить громкость":

```
amixer set Master 5%-

```

Клавиша "Приглушить звук":

```
amixer set Master toggle

```

Вы также можете запустить эти команды, чтобы назначить стандартные клавиши XF86Audio для управления звуком:

```
xfconf-query -c xfce4-keyboard-shortcuts -p /commands/custom/XF86AudioRaiseVolume -n -t string -s "amixer set Master 5%+ unmute"
xfconf-query -c xfce4-keyboard-shortcuts -p /commands/custom/XF86AudioLowerVolume -n -t string -s "amixer set Master 5%- unmute"
xfconf-query -c xfce4-keyboard-shortcuts -p /commands/custom/XF86AudioMute -n -t string -s "amixer set Master toggle"

```

Если `amixer set Master toggle` не работает, попробуйте вместо Master переключать канал PCM: (`amixer set PCM toggle`).

Звуковой канал должен иметь опцию приглушения звука (_mute_), чтобы команда toggle работала. Чтобы проверить, поддерживает ли ваш основной канал (Master) приглушение звука, запустите `alsamixer` в консоли и поищите буквы **MM** под основным каналом. Если таких букв нет, значит канал не поддерживает приглушение звука.

##### PulseAudio

Клавиша "Увеличить громкость":

```
sh -c "pactl set-sink-mute 0 false ; pactl set-sink-volume 0 +5%"

```

Клавиша "Уменьшить громкость":

```
sh -c "pactl set-sink-mute 0 false ; pactl -- set-sink-volume 0 -5%"

```

Клавиша "Приглушить звук":

```
pactl set-sink-mute 0 toggle

```

Эти настройки предполагают, что контролируемое устройство имеет индекс 0\. Используйте команду `pactl list sinks short` для отображения звуковых выходов и их индексов.

##### OSS

Смотрите [OSS#Using multimedia keys with OSS](/index.php/OSS#Using_multimedia_keys_with_OSS "OSS").

##### Xfce4-volumed

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**Эта статья или раздел является кандидатом на объединение с [Xfce (Русский)#Xfce4-mixer и pulseaudio](/index.php/Xfce_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Xfce4-mixer_.D0.B8_pulseaudio "Xfce (Русский)").**

**Причина:** пожалуйста, используйте второй аргумент шаблона для указания причины. (обсуждение: [Talk:Xfce (Русский)#](https://wiki.archlinux.org/index.php/Talk:Xfce_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)))

Демон [xfce4-volumed](https://aur.archlinux.org/packages/xfce4-volumed/)<sup><small>AUR</small></sup> из [AUR](/index.php/AUR_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AUR (Русский)") автоматически назначает звуковые клавиши вашей клавиатуры на Xfce-mixer. Дополнительно, вы можете настроить отображение всплывающего информационного окна во время регулировки звука с помощью Xfce4-notifyd. Xfce4-volumed не требует настройки и запускается автоматически вместе с Xfce.

Если вы используете PulseAudio и звук не восстанавливается после приглушения при повторном нажатии клавиши, используйте команду из раздела [#PulseAudio](#PulseAudio).

**Совет:** Пользователи PulseAudio также могут установить форк программы с пакетом [xfce4-volumed-pulse](https://aur.archlinux.org/packages/xfce4-volumed-pulse/)<sup><small>AUR</small></sup>.

Также вам может понадобиться сменить звуковое устройство по умолчанию на PluseAudio — смотрите [#Xfce4-mixer и pulseaudio](#Xfce4-mixer_.D0.B8_pulseaudio).

##### Volumeicon

[volumeicon](https://www.archlinux.org/packages/?name=volumeicon) является альтернативой xfce4-volumed и также обрабатывает назначения клавиш и уведомления через [xfce4-notifyd](https://www.archlinux.org/packages/?name=xfce4-notifyd).

**Обратите внимание:** Volumeicon может обрабатывать только мультимедиа-клавиши для ALSA. Если вы используете Pulseaudio вместе с Volumeicon, вы можете столкнуться с проблемами, например невозможностью восстановить звук после его приглушения с помощью мультимедиа-клавиш.

##### Специальные клавиши

Если вы переходите с другого дистрибутива, вы можете быть заинтересованы в настройке дополнительных клавиш на клавиатуре. Как это сделать, см. на странице [особые клавиши](/index.php/Extra_keyboard_keys_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Extra keyboard keys (Русский)").

#### Добавление звука запуска системы

Arch Linux не имеет встроенного средства настройки запуска звука. Тем не менее, вы можете добавить команду для проигрывания звука в список автозапуска Xfce:

```
aplay /boot/startupsound.wav

```

Расположение и имя файла могут быть какими угодно.

### Сочетания клавиш

Сочетания клавиш могут быть установлены в двух местах: _Settings > Window Manager > Keyboard_ и _Settings > Keyboard > Shortcuts_.

#### Сложные сочетания

Стандартная версия Xfce4 не сможет использовать некоторые сочетания, например `Super+Shift+j`, даже если вы добавите их в `keyboard.xml` самостоятельно. Чтобы установить такое сочетание, вам придется либо использовать другую программу, например [xbindkeys](/index.php/Xbindkeys "Xbindkeys"), либо установить пакет [libxfce4ui-devel](https://aur.archlinux.org/packages/libxfce4ui-devel/)<sup><small>AUR</small></sup> из AUR.

### Агент аутентификаци Polkit

В состав Xfce не включен агент аутентификации [Polkit](/index.php/Polkit "Polkit"). Смотрите подробнее на странице [Polkit#Authentication agents](/index.php/Polkit#Authentication_agents "Polkit").

## Советы и рекомендации

### Интеграция с xdg-open (предпочтительные приложения)

Большинство графических приложений полагаются на [xdg-open](/index.php/Xdg-open "Xdg-open"), который используется для открытия файлов и URL предпочтительным приложением.

Для правильной интеграции xdg-open и xdg-settings со средой рабочего стола Xfce, вам нужно [установить](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.BE.D0.BF.D1.80.D0.B5.D0.B4.D0.B5.D0.BB.D0.B5.D0.BD.D0.BD.D1.8B.D1.85_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.BE.D0.B2 "Pacman (Русский)") пакет [xorg-xprop](https://www.archlinux.org/packages/?name=xorg-xprop).

Если вы не хотите этого делать, ваши предпочтения приложений не будут соблюдаться. Установка пакета и настройка _xdg-open_ на работу в среде Xfce позволяет перенаправлять все вызовы на _exo-open_, который корректно обрабатывает ваши предпочтения.

Чтобы убедиться, что _xdg-open_ работает нормально, вызовите _xdg-settings_ для какого-нибудь типа предпочтения, например:

```
# xdg-settings get default-web-browser

```

Если программа отобразит

```
xdg-settings: unknown desktop environment

```

это значит, что _xdg-open_ не смог определить Xfce как вашу среду по умолчанию, что, вероятно, случилось из-за того, что не установлен пакет [xorg-xprop](https://www.archlinux.org/packages/?name=xorg-xprop).

### Скриншоты

В состав Xfce входит собственное средство для создания снимков экрана, [xfce4-screenshooter](https://www.archlinux.org/packages/?name=xfce4-screenshooter). Пакет входит в группу [xfce4-goodies](https://www.archlinux.org/groups/x86_64/xfce4-goodies/).

#### Клавиша Print Screen

Перейдите в _Settings > Keyboard > Application Shortcuts_.

Назначьте команду `xfce4-screenshooter -f` на клавишу Print Screen, которая будет делать скриншоты всего экрана. Подробнее о команде `xfce4-screenshooter` и ее опциях вы можете узнать на ее [man-страницах](/index.php/Man_page_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Man page (Русский)").

Также вы можете использовать стороннюю программу для создания скриншотов, например, [scrot](/index.php/Taking_a_screenshot#scrot "Taking a screenshot").

### Блокировка клавиш F1 и F11 в терминале

Терминал Xfce назначает клавиши F1 и F11 на вызов помощи и переход в полноэкранный режим, соответственно, что затрудняет использование некоторых программ вроде _htop_. Чтобы заблокировать эти клавиши, создайте при необходимости и отредактируйте файл настроек, и перезайдите в систему:

 `~/.config/xfce4/terminal/accels.scm` 

```
(gtk_accel_path "<Actions>/terminal-window/fullscreen" "")
(gtk_accel_path "<Actions>/terminal-window/contents" "")

```

Клавиша F10 может быть заблокирована в меню Preferences.

### Цветовые схемы терминала

Цветовые схемы терминала (цветовые палитры) могут быть настроены во вкладке Appearance в окне Preferences. Это цвета, доступные для многих консольных приложений, например [Emacs](/index.php/Emacs "Emacs"), [Vi](/index.php/Vi "Vi") и т.п. Их параметры хранятся для каждого пользователя отдельно в файле `~/.config/xfce4/terminal/terminalrc`. Существуют также многие другие готовые темы на ваш выбор. В ветке [Terminal Colour Scheme Screenshots](https://bbs.archlinux.org/viewtopic.php?id=51818) на форуме вы найдете сотни новых тем на любой вкус.

#### Изменение стандартной цветовой схемы

Пакет `extra/terminal` поставляется с цветовой схемой в темных тонах. Если вы хотите немного более светлые цвета для текста, которые легче воспринимать на темном фоне терминала, добавьте следующие строки в ваш файл `terminalrc`:

 `~/.config/xfce4/terminal/terminalrc` 

```
ColorPalette5=#38d0fcaaf3a9
ColorPalette4=#e013a0a1612f
ColorPalette2=#d456a81b7b42
ColorPalette6=#ffff7062ffff
ColorPalette3=#7ffff7bd7fff
ColorPalette13=#82108210ffff

```

#### Цветовая схема tango

Цветовая схема tango может быть установлена добавлением следующих строк в terminalrc:

 `~/.config/xfce4/terminal/terminalrc` 

```
ColorForeground=White
ColorBackground=#323232323232
ColorPalette1=#2e2e34343636
ColorPalette2=#cccc00000000
ColorPalette3=#4e4e9a9a0606
ColorPalette4=#c4c4a0a00000
ColorPalette5=#34346565a4a4
ColorPalette6=#757550507b7b
ColorPalette7=#060698989a9a
ColorPalette8=#d3d3d7d7cfcf
ColorPalette9=#555557575353
ColorPalette10=#efef29292929
ColorPalette11=#8a8ae2e23434
ColorPalette12=#fcfce9e94f4f
ColorPalette13=#72729f9fcfcf
ColorPalette14=#adad7f7fa8a8
ColorPalette15=#3434e2e2e2e2
ColorPalette16=#eeeeeeeeecec

```

### Цветовые профили

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**Эта статья или раздел является кандидатом на объединение с [Color management](/index.php?title=Color_management&action=edit&redlink=1 "Color management (страница не существует)").**

**Причина:** пожалуйста, используйте второй аргумент шаблона для указания причины. (обсуждение: [Talk:Xfce (Русский)#](https://wiki.archlinux.org/index.php/Talk:Xfce_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)))

_xfce4-settings-manager_ не предоставляет возможности задать настройки цветовых профилей/калибровки экрана, также нет никакой специальной для Xfce программы для настройки монитора.

Есть одна хорошая [статья](https://encrypted.pcode.nl/blog/2013/11/24/display-color-profiling-on-linux), описывающая процедуру настройки цветового профиля в Xfce. В подразделах приведены некоторые основы для настройки.

#### Загрузка профиля

Если вы хотите **загрузить** профиль icc (который вы создали или получили из сети) для калибровки монитора в момент запуска системы, вы можете установить пакет [xcalib](https://aur.archlinux.org/packages/xcalib/)<sup><small>AUR</small></sup> из [AUR](/index.php/AUR_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AUR (Русский)"), затем открыть _Settings Manager_, зайти в _Session and Startup_ и на вкладке _Autostart_ добавить такую команду в список автозапуска:

`/usr/bin/xcalib _/путь/до/profile.icc_`

Но вам все равно нужно явно указать программам, какой профиль следует использовать, чтобы видеть их изображения в правильных цветах.

Альтернативный вариант — dispwin. Dispwin не только калибрует монитор, но также устанавливает атом _ICC_PROFILE в [X](/index.php/Xorg_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xorg (Русский)"), таким образом, некоторые приложения смогут использовать "системный" цветовой профиль вместо того, чтобы требовать его явную установку от пользователя (в числе таких программ GIMP, Inkscape, darktable, UFRaw и многие другие).

Для получения дополнительной информации, смотрите [загрузка профилей ICC](/index.php/ICC_profiles#Loading_ICC_Profiles "ICC profiles").

#### Создание профиля

Если вы хотите **создать** профиль icc для своего монитора (выполнив калибровку, используя какое-нибудь специальное оборудование или "на глаз"), простейшим вариантом будет установка [dispcalgui](https://www.archlinux.org/packages/?name=dispcalgui) из [AUR](/index.php/AUR_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AUR (Русский)").

Также вы можете установить [gnome-settings-daemon](https://www.archlinux.org/packages/?name=gnome-settings-daemon) и [gnome-color-manager](https://www.archlinux.org/packages/?name=gnome-color-manager) (доступны в extra). Чтобы начать калибровку из командной строки, вызовите `/usr/lib/gnome-settings-daemon/gnome-settings-daemon &` (обратите внимание, что это может изменить раскладку клавиатуры и чего угодно еще, поэтому, возможно стоит сделать это в отдельном аккаунте). Затем выполните `colormgr get-devices` и посмотрите значение "Device ID". Если это, например, "xrandr-Lenovo Group Limited", начните калибровку командой `gcm-calibrate --device "xrandr-Lenovo Group Limited"`.

**Обратите внимание:** Причина, по которой вам нужен gnome-settings-daemon в том, что Xfce сам по себе не поддерживает colord (см. [[2]](https://bugzilla.xfce.org/show_bug.cgi?id=8559)). Вместо него, вы можете использовать демон [xiccd](https://github.com/agalakhov/xiccd).

Для получения дополнительной информации, смотрите [ICC profiles](/index.php/ICC_profiles "ICC profiles").

### Несколько мониторов

Если вы настроили X.org так, что он использует несколько мониторов, то при логине в Xfce вы скорее всего увидите, что изображение на всех мониторах одинаковое. Вы можете использовать **xrandr**, чтобы это исправить, однако, если он не будет вызван в нужное время при старте системы, некоторая функциональность может быть потеряна и какие-то части вашего экрана будут недоступны для указателя мыши.

Более правильный способ состоит в настройке Xfce для конкретного расположения ваших мониторов. Однако, на данный момент, нет никакого средства для настройки мониторов напрямую.

*   Окно _Settings > Display_ позволяет настроить разрешение экрана, поворот и включение/выключение отдельных мониторов. Будьте внимательны, изменения в этом окне могут повлечь потерю настроек, выполненных вручную, которые нельзя отрегулировать в самом окне (подробности ниже).
*   Окно _Settings > Settings Editor_ позволяет менять все возможные параметры, в частности настройки экранов (_displays_), которые сохраняются в файле **displays.xml**.

```
~/.config/xfce4/xfconf/xfce-perchannel-xml

```

*   Вы можете вручную отредактировать содержимое файла _displays.xml_.

Основной задачей конфигурации с несколькими мониторами является приведение их логического расположение к физическому. Это можно настроить в параметрах **Position** (**X** и **Y**); позиция _0,0_ соответствует левому верхнему пикселю левой верхней позиции в сетке расположения ваших мониторов. Это позиция по умолчанию для всех мониторов, и если несколько мониторов задействованы, на них будет изначально отображаться одно и то же изображение.

Чтобы правильно увеличить зону отображения для двух мониторов:

*   если мониторы расположены горизонтально, установите координату **X** правого монитора равной ширине (в пикселях) левого монитора
*   если мониторы расположены один под другим, установите координату **Y** нижнего монитора равной высоте (в пикселях) верхнего
*   для более сложных конфигураций, устанавливайте координаты по похожему принципу в соответствии с расположением мониторов

Учтите, что координаты необходимо задавать в пикселях, учитывая поворот экранов. Пример: два монитора с одинаковыми разрешениями _1920x1080_, повернутые на 90 градусов и расположенные бок-о-бок друг к другу, могут быть сконфигурированы следующим образом:

```
<channel name="displays" version="1.0">
 <property name="Default" type="empty">
   <property name="VGA-1" type="string" value="Idek Iiyama 23"">
     <property name="Active" type="bool" value="true"/>
     <property name="Resolution" type="string" value="1920x1080"/>
     <property name="RefreshRate" type="double" value="60.000000"/>
     <property name="Rotation" type="int" value="90"/>
     <property name="Reflection" type="string" value="0"/>
     <property name="Primary" type="bool" value="false"/>
     <property name="Position" type="empty">
       **<property name="X" type="int" value="0"/>**
       <property name="Y" type="int" value="0"/>
     </property>
   </property>
   <property name="DVI-0" type="string" value="Digital display">
     <property name="Active" type="bool" value="true"/>
     <property name="Resolution" type="string" value="1920x1080"/>
     <property name="RefreshRate" type="double" value="60.000000"/>
     <property name="Rotation" type="int" value="90"/>
     <property name="Reflection" type="string" value="0"/>
     <property name="Primary" type="bool" value="false"/>
     <property name="Position" type="empty">
       **<property name="X" type="int" value="1080"/>**
       <property name="Y" type="int" value="0"/>
     </property>
   </property>
 </property>
</channel>

```

После завершения редактирования файла вам потребуется перезайти в систему, чтобы увидеть изменения.

В ожидаемом релизе xfce-settings 4.12 станет доступен новый метод установки нескольких мониторов.

### Пользовательские каталоги XDG

freedesktop.org определяет стандартные каталоги для пользователей, вроде desktop или music. Дополнительную информацию см. в [Xdg user directories](/index.php/Xdg_user_directories "Xdg user directories").

### SSH Agents

По умолчанию, Xfce версии 4.10 попытается загрузить gpg-agent или ssh-agent во время начальной инициализации сеанса. Чтобы отключить это, создайте ключ xfconf используя команду:

```
xfconf-query -c xfce4-session -p /startup/ssh-agent/enabled -n -t bool -s false

```

Чтобы заставить Xfce использовать ssh-agent, даже если gpg-agent установлен, выполните эту команду вместо предыдущей:

```
xfconf-query -c xfce4-session -p /startup/ssh-agent/type -n -t string -s ssh-agent

```

Чтобы использовать [GNOME Keyring](/index.php/GNOME_Keyring "GNOME Keyring"), установите флажок _Launch GNOME services on startup_ во вкладке _Advanced_ окна _Session Manager_ в настройках. Это также заблокирует gpg-agent и ssh-agent.

Смотрите также [[3]](http://docs.xfce.org/xfce/xfce4-session/advanced).

### Bluetooth

У вас есть 3 способа использовать Blueetooth в Xfce:

*   [Blueman](/index.php/Blueman "Blueman").

*   [GNOME Bluetooth](/index.php/Bluetooth_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#GNOME_Bluetooth "Bluetooth (Русский)").

*   Инструменты командной строки. [Obex](/index.php/Bluetooth_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_Obex_.D0.B4.D0.BB.D1.8F_.D0.BE.D1.82.D1.81.D1.8B.D0.BB.D0.BA.D0.B8_.D0.B8_.D0.BF.D0.BE.D0.BB.D1.83.D1.87.D0.B5.D0.BD.D0.B8.D1.8F_.D1.84.D0.B0.D0.B9.D0.BB.D0.BE.D0.B2 "Bluetooth (Русский)") может быть использован для отправки и получения файлов, а [bluetoothctl](/index.php/Bluetooth_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Bluetoothctl "Bluetooth (Русский)") — для сопряжения устройств. Смотрите также [Bluetooth](/index.php/Bluetooth_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Bluetooth (Русский)") для получения дополнительной информации.

### Прокрутка в фоновом окне без фокусировки на нем

Перейдите в _Settings > Window Manager Tweaks_ > вкладка _Accessibility_, и снимите флажок _Raise windows when any mouse button is pressed_.

### Прозрачность активного окна

Можно настроить прозрачность активного окна путём горизонтального скролла (или Atl + колёсико мыши) на заголовке оного. Настройка не сохранится при переоткрытии окна, возможно, это можно исправить.

## Решение проблем

### Отсутствующие значки на кнопках действий

Так происходит, если значки для каких-нибудь действий (Suspend, Hibernate) отсутствуют в теме значков, или имеют нестандартные имена. Первым делом, посмотрите, какая тема используется в данный момент в окне Settings Manager (_Appearance > Icons_). Теперь по названию найдите, в каком подкаталоге она расположена в `/usr/share/icons`. Например, если выбрана тема GNOME, вы можете найти каталог `/usr/share/icons/gnome` с файлами темы.

```
icontheme=/usr/share/icons/gnome

```

Установите какую-нибудь тему, в которой имеются отсутствующие значки. Смотрите [Icons](/index.php/Icons "Icons").

Пакет [xfce4-power-manager](https://www.archlinux.org/packages/?name=xfce4-power-manager) также содержит необходимые значки. Создайте символические ссылки в каталоге текущей темы к файлам из каталога `hicolor`.

```
ln -s /usr/share/icons/hicolor/16x16/actions/xfpm-suspend.png   ${icontheme}/16x16/actions/system-suspend.png
ln -s /usr/share/icons/hicolor/16x16/actions/xfpm-hibernate.png ${icontheme}/16x16/actions/system-hibernate.png
ln -s /usr/share/icons/hicolor/22x22/actions/xfpm-suspend.png   ${icontheme}/22x22/actions/system-suspend.png
ln -s /usr/share/icons/hicolor/22x22/actions/xfpm-hibernate.png ${icontheme}/22x22/actions/system-hibernate.png
ln -s /usr/share/icons/hicolor/24x24/actions/xfpm-suspend.png   ${icontheme}/24x24/actions/system-suspend.png
ln -s /usr/share/icons/hicolor/24x24/actions/xfpm-hibernate.png ${icontheme}/24x24/actions/system-hibernate.png
ln -s /usr/share/icons/hicolor/48x48/actions/xfpm-suspend.png   ${icontheme}/48x48/actions/system-suspend.png
ln -s /usr/share/icons/hicolor/48x48/actions/xfpm-hibernate.png ${icontheme}/48x48/actions/system-hibernate.png

```

Перезайдите в систему, чтобы увидеть изменения.

### Сбиваются позиции ярлыков рабочего стола

В определенные моменты (например, при открытии диалогового окна настроек панели), расположение ярлыков на рабочем столе может быть сбито. Это происходит оттого, что расположения ярлыков хранятся в файлах в каталоге `~/.config/xfce4/desktop/`. Каждый раз, когда вы вносите изменения на рабочем столе, (добавляете/удаляете значки), в этом каталоге генерируется новый файл и он конфликтует с уже существующими.

Чтобы это исправить, зайдите в этот каталог и удалите все файлы кроме того, который содержит правильные позиции ярлыков. Вы можете найти этот файл по содержимому, посмотрев координаты расположения ярлыков в сетке. Верхняя строка определяется как `row=0`, левая колонка — `col=0`. Таким образом, запись:

```
[Firefox]
row=3
col=0

```

означает, что ярлык Firefox расположен на четвертой строке первой колонки (то есть, у левого края).

### Темы GTK не работают с несколькими мониторами

Некоторые средства конфигурации могут поломать displays.xml, в результате чего темы GTK в _Settings > Appearance_ прекратят работать. Чтобы это исправить, удалите `~/.config/xfce4/xfconf/xfce-perchannel-xml/displays.xml` и заново настройте мониторы.

### HTML-файлы не открываются корректно в Firefox

Проблема возникает, если Firefox установлен как браузер по умолчанию в `exo-preferred-applications`. При открытии файлов HTML, в имени которых есть пробелы, каждая часть имени, разделенная пробелом, может быть открыта как отдельный URL в отдельной вкладке ([[4]](https://bugzilla.xfce.org/show_bug.cgi?id=10731)). Вы можете открывать такие файлы, указывая явно `firefox.desktop` (_Firefox_) вместо `exo-web-browser.desktop` (_Web Browser_), или в файле `/usr/share/xfce4/helpers/firefox.desktop` измените:

```
X-XFCE-CommandsWithParameter=%B -remote "openURL(%s)";%B %s;

```

на (добавив кавычки вокруг `%s`)

```
X-XFCE-CommandsWithParameter=%B -remote "openURL(%s)";%B **"%s"**;

```

Также вы можете установить пакет [exo-helpers-patch](https://aur.archlinux.org/packages/exo-helpers-patch/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/exo-helpers-patch)]</sup>.

### Значки не появляются в контекстных меню

Вы можете обнаружить, что значки не появляются при нажатии правой кнопкой мыши в некоторых приложениях, включая те, что используют [Qt](/index.php/Qt_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Qt (Русский)"). Эта проблема появляется только в Xfce. Выполните следующие команды:

```
$ gconftool-2 --type boolean --set /desktop/gnome/interface/buttons_have_icons true
$ gconftool-2 --type boolean --set /desktop/gnome/interface/menus_have_icons true

```

### Настройки клавиатуры не сохраняются в xkb-plugin

Это ошибка в [xfce4-xkb-plugin](https://www.archlinux.org/packages/?name=xfce4-xkb-plugin) версии _0.5.4.1-1_, который вызывает потерю настроек клавиатуры, раскладок и клавиши compose. Решением проблемы является сбросить настройки (_Use system defaults_) в `xfce4-keyboard-settings`, и выполнить настройку _xfce4-xkb-plugin_ заново.

### GDM игнорирует локали

Добавьте вашу [локаль](/index.php/Locale_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Locale (Русский)") в `/var/lib/AccountsService/users/$USER`:

```
[User]
Language=_your_locale_
XSession=xfce

```

Перезагрузите GDM, чтобы увидеть изменения.

### В меню отсутствуют приложения Wine

Приложения [Wine](/index.php/Wine_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Wine (Русский)") могут отсутствовать в `/usr/share/applications`. См. категорию "Other" в `~/.local/share/applications/wine/`.

### Повторный вход в спящий режим

Если для обработки событий ACPI используется [xfce4-power-manager](https://www.archlinux.org/packages/?name=xfce4-power-manager), а не [systemd](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd (Русский)"), поправьте `/etc/systemd/logind.conf`:

```
HandlePowerKey=ignore
HandleSuspendKey=ignore
HandleHibernateKey=ignore
HandleLidSwitch=ignore

```

### Некорректное отображение символов при монтировании USB-накопителей

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**Эта статья или раздел является кандидатом на объединение с [Mount (Русский)](/index.php/Mount_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Mount (Русский)").**

**Причина:** пожалуйста, используйте второй аргумент шаблона для указания причины. (обсуждение: [Talk:Xfce (Русский)#](https://wiki.archlinux.org/index.php/Talk:Xfce_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)))

Известная проблема с автоматическим монтированием USB-накопителей, отформатированных в FAT, когда не отображаются корректно символы с умляутами, вроде ñ, ß, и т.п. Это может быть решено изменением кодировки по умолчанию на UTF-8, что легко сделать, добавив строку в `/etc/xdg/xfce4/mount.rc`:

```
[vfat]
uid=<auto>
shortname=winnt
**utf8=true**
# FreeBSD specific option
longnames=true
flush=true

```

Обратите внимание, что когда используется UTF-8, система станет различать регистр символов, возможно портя ваши файлы. Будьте осторожны.

Возможно монтировать устройства VFAT с опцией _flush_, так, что при копировании на USB-накопители данные будут сбрасываться из буфера в память устройства чаще, таким образом, индикатор выполнения tunar будет оставаться до фактического завершения передачи данных. Опция _async_ наоборот, будет ускорять операции записи, но не забывайте в таком случае размонтировать (_Eject_) устройство перед удалением. Вы можете указать опции монтирования устройств хранения данных, подключенных во время запуска системы, в файле [fstab](/index.php/Fstab_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Fstab (Русский)"), а для прочих устройств — создавая правила [udev](/index.php/Udev_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Udev (Русский)").

### NVIDIA и xfce4-sensors-plugin

Чтобы определить и использовать датчики на GPU NVidia, вам необходимо установить [libxnvctrl](https://www.archlinux.org/packages/?name=libxnvctrl) и пересобрать [xfce4-sensors-plugin](https://www.archlinux.org/packages/?name=xfce4-sensors-plugin), используя [ABS](/index.php/Arch_Build_System_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch Build System (Русский)").

### Отключение экрана

Xfce4, по крайней мере, версии 4.12, не учитывает режимы электропитания монитора в `xfce4-power-manager`. Вместо этого, он пытается запустить скринсейвер каждые 10 минут. Это может быть проверено командой `$ xset q`. Запустите `$ xset s noblank`, чтобы предотвратить это поведение; смотрите также [DPMS](/index.php/DPMS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "DPMS (Русский)").

Также вы можете добавить следующее в `/etc/X11/xorg.conf.d/`:

 `20-blank.conf` 

```
Section "ServerFlags"
 Option "BlankTime" "0"
EndSection

```

### Настройки предпочтений не работают

Если вы задали предпочтительные приложения с _exo-preferred-applications_, но они не работают, посмотрите подраздел [#Интеграция с xdg-open (предпочтительные приложения)](#.D0.98.D0.BD.D1.82.D0.B5.D0.B3.D1.80.D0.B0.D1.86.D0.B8.D1.8F_.D1.81_xdg-open_.28.D0.BF.D1.80.D0.B5.D0.B4.D0.BF.D0.BE.D1.87.D1.82.D0.B8.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D1.8B.D0.B5_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F.29).

### Лишний пункт в контекстном меню рабочего стола

**Обратите внимание:** По крайней мере, в Xfce 4.10 (совместно с Thunar 1.63, xfdesktop 4.10.2) имеется такая неисправность. Не уверен, что это имеет отношение к xfdesktop.

При создании нового пустого (текстового) файла на рабочем столе, правый клик по нему покажет лишний пункт _Set as wallpaper_. Чтобы это отключить, [пересоберите](/index.php/Arch_Build_System_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch Build System (Русский)") Thunar с опцией `--disable-wallpaper-plugin`.

### Восстановление стандартных настроек

Если по какой-то причине вы захотели начать с чистого листа, просто переименуйте каталоги `~/.config/xfce4-session/` и `~/.config/xfce4/`:

```
$ mv ~/.config/xfce4-session/ ~/.config/xfce4-session-bak
$ mv ~/.config/xfce4/ ~/.config/xfce4-bak

```

И перезайдите в систему. Если вы получили "Unable to load a failsafe session" во время входа, посмотрите [#Отказ сеанса](#.D0.9E.D1.82.D0.BA.D0.B0.D0.B7_.D1.81.D0.B5.D0.B0.D0.BD.D1.81.D0.B0).

### Отказ сеанса

Симптомы:

*   указатель мыши как в [X](/index.php/Xorg_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xorg (Русский)") или вообще отсутствует;
*   декорации окон пропали и окна не закрываются;
*   (`xfwm4-settings`) не запускается, сообщая `These settings cannot work with your current window manager (unknown)`;
*   [экранный менеджер](/index.php/%D0%AD%D0%BA%D1%80%D0%B0%D0%BD%D0%BD%D1%8B%D0%B9_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80 "Экранный менеджер") сообщает об ошибках, таких как `No window manager registered on screen 0`.

Полная перезагрузка может решить проблему, однако, ее причиной может быть поврежденный сохраненный сеанс. Удалите каталог сохраненного сеанса:

```
$ rm -r ~/.cache/sessions/

```

## Смотрите также

*   [Xfce — About](http://www.xfce.org/about/).
*   [[5]](http://docs.xfce.org/) — полная документация.
*   [Xfce-Look](http://www.xfce-look.org/) — темы, обои и многое другое.
*   [[6]](http://xfce.wikia.com/wiki/Frequently_Asked_Questions) — FAQ по Xfce.
*   [Xfce Wiki](http://wiki.xfce.org).

Retrieved from "[https://wiki.archlinux.org/index.php?title=Xfce_(Русский)&oldid=414880](https://wiki.archlinux.org/index.php?title=Xfce_(Русский)&oldid=414880)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Desktop environments (Русский)](/index.php/Category:Desktop_environments_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Category:Desktop environments (Русский)")
*   [Русский](/index.php/Category:%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9 "Category:Русский")