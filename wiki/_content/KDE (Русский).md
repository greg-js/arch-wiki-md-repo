# KDE (Русский)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Ссылки по теме

*   [Среда рабочего стола](/index.php/%D0%A1%D1%80%D0%B5%D0%B4%D0%B0_%D1%80%D0%B0%D0%B1%D0%BE%D1%87%D0%B5%D0%B3%D0%BE_%D1%81%D1%82%D0%BE%D0%BB%D0%B0 "Среда рабочего стола")
*   [Экранный менеджер](/index.php/%D0%AD%D0%BA%D1%80%D0%B0%D0%BD%D0%BD%D1%8B%D0%B9_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80 "Экранный менеджер")
*   [Оконный менеджер](/index.php/%D0%9E%D0%BA%D0%BE%D0%BD%D0%BD%D1%8B%D0%B9_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80 "Оконный менеджер")
*   [Plasma](/index.php/Plasma "Plasma")
*   [Qt (Русский)](/index.php/Qt_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Qt (Русский)")
*   [KDM (Русский)](/index.php/KDM_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "KDM (Русский)")
*   [KDevelop 4](/index.php/KDevelop_4 "KDevelop 4")
*   [Uniform Look for Qt and GTK Applications (Русский)](/index.php/Uniform_Look_for_Qt_and_GTK_Applications_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Uniform Look for Qt and GTK Applications (Русский)")

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

**Эта страница нуждается в сопроводителе**

Статья не гарантирует актуальность информации. Помогите русскоязычному сообществу поддержкой подобных страниц. См. [Команда переводчиков ArchWiki](/index.php/%D0%9A%D0%BE%D0%BC%D0%B0%D0%BD%D0%B4%D0%B0_%D0%BF%D0%B5%D1%80%D0%B5%D0%B2%D0%BE%D0%B4%D1%87%D0%B8%D0%BA%D0%BE%D0%B2_ArchWiki "Команда переводчиков ArchWiki")

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

**Информация в этой статье или разделе устарела**

**Причина:** В английской версии накопилось много изменений ([Обсудить](https://wiki.archlinux.org/index.php/Talk:KDE_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)))

KDE Software Compilation — набор фреймворков, рабочих окружений и приложений, разработанных KDE для того, чтобы создать красивую, функциональную и свободную графическую среду рабочего стола для Linux и других операционных систем. Он состоит из большого количества отдельных приложений и рабочего стола в качестве оболочки для запуска этих приложений.

KDE имеет активно поддерживаемый [вики-ресурс UserBase](http://userbase.kde.org/). Здесь пользователи могут получить наиболее актуальную и подробную информацию о большинстве приложений KDE.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
    *   [1.1 Plasma 5](#Plasma_5)
    *   [1.2 Приложения KDE и языковые пакеты](#.D0.9F.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F_KDE_.D0.B8_.D1.8F.D0.B7.D1.8B.D0.BA.D0.BE.D0.B2.D1.8B.D0.B5_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D1.8B)
    *   [1.3 Обновление KDE4 до Plasma 5](#.D0.9E.D0.B1.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_KDE4_.D0.B4.D0.BE_Plasma_5)
*   [2 Запуск Plasma](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_Plasma)
*   [3 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [3.1 Персонализация](#.D0.9F.D0.B5.D1.80.D1.81.D0.BE.D0.BD.D0.B0.D0.BB.D0.B8.D0.B7.D0.B0.D1.86.D0.B8.D1.8F)
        *   [3.1.1 Plasma desktop](#Plasma_desktop)
            *   [3.1.1.1 Themes](#Themes)
                *   [3.1.1.1.1 Внешний вид Qt и GTK+](#.D0.92.D0.BD.D0.B5.D1.88.D0.BD.D0.B8.D0.B9_.D0.B2.D0.B8.D0.B4_Qt_.D0.B8_GTK.2B)
        *   [3.1.2 Рабочий стол Plasma](#.D0.A0.D0.B0.D0.B1.D0.BE.D1.87.D0.B8.D0.B9_.D1.81.D1.82.D0.BE.D0.BB_Plasma)
            *   [3.1.2.1 Темы](#.D0.A2.D0.B5.D0.BC.D1.8B)
            *   [3.1.2.2 Виджеты](#.D0.92.D0.B8.D0.B4.D0.B6.D0.B5.D1.82.D1.8B)
            *   [3.1.2.3 Значки системного трея](#.D0.97.D0.BD.D0.B0.D1.87.D0.BA.D0.B8_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D0.BD.D0.BE.D0.B3.D0.BE_.D1.82.D1.80.D0.B5.D1.8F)
            *   [3.1.2.4 Звуковой апплет в системном трее](#.D0.97.D0.B2.D1.83.D0.BA.D0.BE.D0.B2.D0.BE.D0.B9_.D0.B0.D0.BF.D0.BF.D0.BB.D0.B5.D1.82_.D0.B2_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D0.BD.D0.BE.D0.BC_.D1.82.D1.80.D0.B5.D0.B5)
            *   [3.1.2.5 Главное меню на рабочем столе](#.D0.93.D0.BB.D0.B0.D0.B2.D0.BD.D0.BE.D0.B5_.D0.BC.D0.B5.D0.BD.D1.8E_.D0.BD.D0.B0_.D1.80.D0.B0.D0.B1.D0.BE.D1.87.D0.B5.D0.BC_.D1.81.D1.82.D0.BE.D0.BB.D0.B5)
        *   [3.1.3 Декорации окон](#.D0.94.D0.B5.D0.BA.D0.BE.D1.80.D0.B0.D1.86.D0.B8.D0.B8_.D0.BE.D0.BA.D0.BE.D0.BD)
        *   [3.1.4 Темы значков](#.D0.A2.D0.B5.D0.BC.D1.8B_.D0.B7.D0.BD.D0.B0.D1.87.D0.BA.D0.BE.D0.B2)
        *   [3.1.5 Шрифты](#.D0.A8.D1.80.D0.B8.D1.84.D1.82.D1.8B)
            *   [3.1.5.1 Шрифты в KDE выглядят плохо](#.D0.A8.D1.80.D0.B8.D1.84.D1.82.D1.8B_.D0.B2_KDE_.D0.B2.D1.8B.D0.B3.D0.BB.D1.8F.D0.B4.D1.8F.D1.82_.D0.BF.D0.BB.D0.BE.D1.85.D0.BE)
            *   [3.1.5.2 Огромные или непропорциональные буквы](#.D0.9E.D0.B3.D1.80.D0.BE.D0.BC.D0.BD.D1.8B.D0.B5_.D0.B8.D0.BB.D0.B8_.D0.BD.D0.B5.D0.BF.D1.80.D0.BE.D0.BF.D0.BE.D1.80.D1.86.D0.B8.D0.BE.D0.BD.D0.B0.D0.BB.D1.8C.D0.BD.D1.8B.D0.B5_.D0.B1.D1.83.D0.BA.D0.B2.D1.8B)
        *   [3.1.6 Экономия места на экране](#.D0.AD.D0.BA.D0.BE.D0.BD.D0.BE.D0.BC.D0.B8.D1.8F_.D0.BC.D0.B5.D1.81.D1.82.D0.B0_.D0.BD.D0.B0_.D1.8D.D0.BA.D1.80.D0.B0.D0.BD.D0.B5)
    *   [3.2 Сеть](#.D0.A1.D0.B5.D1.82.D1.8C)
    *   [3.3 Печать](#.D0.9F.D0.B5.D1.87.D0.B0.D1.82.D1.8C)
    *   [3.4 Поддержка Samba/Windows](#.D0.9F.D0.BE.D0.B4.D0.B4.D0.B5.D1.80.D0.B6.D0.BA.D0.B0_Samba.2FWindows)
    *   [3.5 Комнаты KDE](#.D0.9A.D0.BE.D0.BC.D0.BD.D0.B0.D1.82.D1.8B_KDE)
    *   [3.6 Снижение энергопотребления](#.D0.A1.D0.BD.D0.B8.D0.B6.D0.B5.D0.BD.D0.B8.D0.B5_.D1.8D.D0.BD.D0.B5.D1.80.D0.B3.D0.BE.D0.BF.D0.BE.D1.82.D1.80.D0.B5.D0.B1.D0.BB.D0.B5.D0.BD.D0.B8.D1.8F)
    *   [3.7 Отслеживание изменений локальных файлов и каталогов](#.D0.9E.D1.82.D1.81.D0.BB.D0.B5.D0.B6.D0.B8.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.B8.D0.B7.D0.BC.D0.B5.D0.BD.D0.B5.D0.BD.D0.B8.D0.B9_.D0.BB.D0.BE.D0.BA.D0.B0.D0.BB.D1.8C.D0.BD.D1.8B.D1.85_.D1.84.D0.B0.D0.B9.D0.BB.D0.BE.D0.B2_.D0.B8_.D0.BA.D0.B0.D1.82.D0.B0.D0.BB.D0.BE.D0.B3.D0.BE.D0.B2)
*   [4 Системное администрирование](#.D0.A1.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D0.BD.D0.BE.D0.B5_.D0.B0.D0.B4.D0.BC.D0.B8.D0.BD.D0.B8.D1.81.D1.82.D1.80.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5)
    *   [4.1 Настройка клавиатуры](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D0.B0.D1.82.D1.83.D1.80.D1.8B)
    *   [4.2 Сочетание клавиш для остановки сервера X](#.D0.A1.D0.BE.D1.87.D0.B5.D1.82.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D1.88_.D0.B4.D0.BB.D1.8F_.D0.BE.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B8_.D1.81.D0.B5.D1.80.D0.B2.D0.B5.D1.80.D0.B0_X)
    *   [4.3 KCM](#KCM)
    *   [4.4 Автоматический вход в систему](#.D0.90.D0.B2.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8.D0.B9_.D0.B2.D1.85.D0.BE.D0.B4_.D0.B2_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.83)
*   [5 Быстрый поиск и семантический рабочий стол](#.D0.91.D1.8B.D1.81.D1.82.D1.80.D1.8B.D0.B9_.D0.BF.D0.BE.D0.B8.D1.81.D0.BA_.D0.B8_.D1.81.D0.B5.D0.BC.D0.B0.D0.BD.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8.D0.B9_.D1.80.D0.B0.D0.B1.D0.BE.D1.87.D0.B8.D0.B9_.D1.81.D1.82.D0.BE.D0.BB)
    *   [5.1 Baloo](#Baloo)
        *   [5.1.1 Настройка и использование Baloo](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D0.B8_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_Baloo)
        *   [5.1.2 Как проиндексировать съемное устройство?](#.D0.9A.D0.B0.D0.BA_.D0.BF.D1.80.D0.BE.D0.B8.D0.BD.D0.B4.D0.B5.D0.BA.D1.81.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D1.82.D1.8C_.D1.81.D1.8A.D0.B5.D0.BC.D0.BD.D0.BE.D0.B5_.D1.83.D1.81.D1.82.D1.80.D0.BE.D0.B9.D1.81.D1.82.D0.B2.D0.BE.3F)
    *   [5.2 Akonadi](#Akonadi)
        *   [5.2.1 Выключение Akonadi](#.D0.92.D1.8B.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_Akonadi)
        *   [5.2.2 Настройка базы данных](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D0.B1.D0.B0.D0.B7.D1.8B_.D0.B4.D0.B0.D0.BD.D0.BD.D1.8B.D1.85)
        *   [5.2.3 Использование KDE без Akonadi](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_KDE_.D0.B1.D0.B5.D0.B7_Akonadi)
*   [6 Phonon](#Phonon)
    *   [6.1 Какой бекэнд использовать?](#.D0.9A.D0.B0.D0.BA.D0.BE.D0.B9_.D0.B1.D0.B5.D0.BA.D1.8D.D0.BD.D0.B4_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D1.8C.3F)
*   [7 Полезные приложения](#.D0.9F.D0.BE.D0.BB.D0.B5.D0.B7.D0.BD.D1.8B.D0.B5_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F)
    *   [7.1 Yakuake](#Yakuake)
    *   [7.2 KDE Telepathy](#KDE_Telepathy)
*   [8 Советы и рекомендации](#.D0.A1.D0.BE.D0.B2.D0.B5.D1.82.D1.8B_.D0.B8_.D1.80.D0.B5.D0.BA.D0.BE.D0.BC.D0.B5.D0.BD.D0.B4.D0.B0.D1.86.D0.B8.D0.B8)
    *   [8.1 Использование альтернативного оконного менеджера с KDE](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.B0.D0.BB.D1.8C.D1.82.D0.B5.D1.80.D0.BD.D0.B0.D1.82.D0.B8.D0.B2.D0.BD.D0.BE.D0.B3.D0.BE_.D0.BE.D0.BA.D0.BE.D0.BD.D0.BD.D0.BE.D0.B3.D0.BE_.D0.BC.D0.B5.D0.BD.D0.B5.D0.B4.D0.B6.D0.B5.D1.80.D0.B0_.D1.81_KDE)
        *   [8.1.1 Сеанс KDE/Openbox](#.D0.A1.D0.B5.D0.B0.D0.BD.D1.81_KDE.2FOpenbox)
        *   [8.1.2 Compiz custom](#Compiz_custom)
        *   [8.1.3 Включение композитных эффектов](#.D0.92.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BA.D0.BE.D0.BC.D0.BF.D0.BE.D0.B7.D0.B8.D1.82.D0.BD.D1.8B.D1.85_.D1.8D.D1.84.D1.84.D0.B5.D0.BA.D1.82.D0.BE.D0.B2)
    *   [8.2 Интеграция Android в рабочий стол KDE](#.D0.98.D0.BD.D1.82.D0.B5.D0.B3.D1.80.D0.B0.D1.86.D0.B8.D1.8F_Android_.D0.B2_.D1.80.D0.B0.D0.B1.D0.BE.D1.87.D0.B8.D0.B9_.D1.81.D1.82.D0.BE.D0.BB_KDE)
    *   [8.3 Получение уведомлений о выходе обновлений ПО](#.D0.9F.D0.BE.D0.BB.D1.83.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D1.83.D0.B2.D0.B5.D0.B4.D0.BE.D0.BC.D0.BB.D0.B5.D0.BD.D0.B8.D0.B9_.D0.BE_.D0.B2.D1.8B.D1.85.D0.BE.D0.B4.D0.B5_.D0.BE.D0.B1.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B9_.D0.9F.D0.9E)
    *   [8.4 Настройка KWin для использования OpenGL ES](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_KWin_.D0.B4.D0.BB.D1.8F_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D1.8F_OpenGL_ES)
    *   [8.5 Отображение миниатюр для аудио- и видеофайлов в Konqueror/Dolphin](#.D0.9E.D1.82.D0.BE.D0.B1.D1.80.D0.B0.D0.B6.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BC.D0.B8.D0.BD.D0.B8.D0.B0.D1.82.D1.8E.D1.80_.D0.B4.D0.BB.D1.8F_.D0.B0.D1.83.D0.B4.D0.B8.D0.BE-_.D0.B8_.D0.B2.D0.B8.D0.B4.D0.B5.D0.BE.D1.84.D0.B0.D0.B9.D0.BB.D0.BE.D0.B2_.D0.B2_Konqueror.2FDolphin)
    *   [8.6 Ускорение запуска приложений](#.D0.A3.D1.81.D0.BA.D0.BE.D1.80.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA.D0.B0_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D0.B9)
    *   [8.7 Скрытие разделов](#.D0.A1.D0.BA.D1.80.D1.8B.D1.82.D0.B8.D0.B5_.D1.80.D0.B0.D0.B7.D0.B4.D0.B5.D0.BB.D0.BE.D0.B2)
    *   [8.8 Konqueror](#Konqueror)
        *   [8.8.1 Отключение Access Keys](#.D0.9E.D1.82.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_Access_Keys)
        *   [8.8.2 Использование WebKit](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_WebKit)
    *   [8.9 Интеграция Firefox в KDE](#.D0.98.D0.BD.D1.82.D0.B5.D0.B3.D1.80.D0.B0.D1.86.D0.B8.D1.8F_Firefox_.D0.B2_KDE)
    *   [8.10 Установка фона для экрана блокировки](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D1.84.D0.BE.D0.BD.D0.B0_.D0.B4.D0.BB.D1.8F_.D1.8D.D0.BA.D1.80.D0.B0.D0.BD.D0.B0_.D0.B1.D0.BB.D0.BE.D0.BA.D0.B8.D1.80.D0.BE.D0.B2.D0.BA.D0.B8)
    *   [8.11 Еще один способ установки фона для экрана блокировки](#.D0.95.D1.89.D0.B5_.D0.BE.D0.B4.D0.B8.D0.BD_.D1.81.D0.BF.D0.BE.D1.81.D0.BE.D0.B1_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B8_.D1.84.D0.BE.D0.BD.D0.B0_.D0.B4.D0.BB.D1.8F_.D1.8D.D0.BA.D1.80.D0.B0.D0.BD.D0.B0_.D0.B1.D0.BB.D0.BE.D0.BA.D0.B8.D1.80.D0.BE.D0.B2.D0.BA.D0.B8)
    *   [8.12 Изменение фона экрана приветствия при запуске (Plasma 5)](#.D0.98.D0.B7.D0.BC.D0.B5.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D1.84.D0.BE.D0.BD.D0.B0_.D1.8D.D0.BA.D1.80.D0.B0.D0.BD.D0.B0_.D0.BF.D1.80.D0.B8.D0.B2.D0.B5.D1.82.D1.81.D1.82.D0.B2.D0.B8.D1.8F_.D0.BF.D1.80.D0.B8_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA.D0.B5_.28Plasma_5.29)
*   [9 Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [9.1 Отсутствие иконок в трее (KDE5)](#.D0.9E.D1.82.D1.81.D1.83.D1.82.D1.81.D1.82.D0.B2.D0.B8.D0.B5_.D0.B8.D0.BA.D0.BE.D0.BD.D0.BE.D0.BA_.D0.B2_.D1.82.D1.80.D0.B5.D0.B5_.28KDE5.29)
    *   [9.2 Проблемы с настройками](#.D0.9F.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D1.8B_.D1.81_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0.D0.BC.D0.B8)
        *   [9.2.1 Полный сброс настроек KDE](#.D0.9F.D0.BE.D0.BB.D0.BD.D1.8B.D0.B9_.D1.81.D0.B1.D1.80.D0.BE.D1.81_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B5.D0.BA_KDE)
        *   [9.2.2 Странное поведение рабочего стола Plasma](#.D0.A1.D1.82.D1.80.D0.B0.D0.BD.D0.BD.D0.BE.D0.B5_.D0.BF.D0.BE.D0.B2.D0.B5.D0.B4.D0.B5.D0.BD.D0.B8.D0.B5_.D1.80.D0.B0.D0.B1.D0.BE.D1.87.D0.B5.D0.B3.D0.BE_.D1.81.D1.82.D0.BE.D0.BB.D0.B0_Plasma)
        *   [9.2.3 Очистка кэша для решения проблем с обновлением](#.D0.9E.D1.87.D0.B8.D1.81.D1.82.D0.BA.D0.B0_.D0.BA.D1.8D.D1.88.D0.B0_.D0.B4.D0.BB.D1.8F_.D1.80.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D1.8F_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC_.D1.81_.D0.BE.D0.B1.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5.D0.BC)
    *   [9.3 Сброс настроек Akonadi для решения проблем с KMail](#.D0.A1.D0.B1.D1.80.D0.BE.D1.81_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B5.D0.BA_Akonadi_.D0.B4.D0.BB.D1.8F_.D1.80.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D1.8F_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC_.D1.81_KMail)
    *   [9.4 Текущее состояние KWin для поддержки и отладки](#.D0.A2.D0.B5.D0.BA.D1.83.D1.89.D0.B5.D0.B5_.D1.81.D0.BE.D1.81.D1.82.D0.BE.D1.8F.D0.BD.D0.B8.D0.B5_KWin_.D0.B4.D0.BB.D1.8F_.D0.BF.D0.BE.D0.B4.D0.B4.D0.B5.D1.80.D0.B6.D0.BA.D0.B8_.D0.B8_.D0.BE.D1.82.D0.BB.D0.B0.D0.B4.D0.BA.D0.B8)
    *   [9.5 KDE4 зависает на этапе загрузки](#KDE4_.D0.B7.D0.B0.D0.B2.D0.B8.D1.81.D0.B0.D0.B5.D1.82_.D0.BD.D0.B0_.D1.8D.D1.82.D0.B0.D0.BF.D0.B5_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B8)
    *   [9.6 Программы KDE выглядят плохо в другом оконном менеджере](#.D0.9F.D1.80.D0.BE.D0.B3.D1.80.D0.B0.D0.BC.D0.BC.D1.8B_KDE_.D0.B2.D1.8B.D0.B3.D0.BB.D1.8F.D0.B4.D1.8F.D1.82_.D0.BF.D0.BB.D0.BE.D1.85.D0.BE_.D0.B2_.D0.B4.D1.80.D1.83.D0.B3.D0.BE.D0.BC_.D0.BE.D0.BA.D0.BE.D0.BD.D0.BD.D0.BE.D0.BC_.D0.BC.D0.B5.D0.BD.D0.B5.D0.B4.D0.B6.D0.B5.D1.80.D0.B5)
    *   [9.7 Проблемы с графикой](#.D0.9F.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D1.8B_.D1.81_.D0.B3.D1.80.D0.B0.D1.84.D0.B8.D0.BA.D0.BE.D0.B9)
        *   [9.7.1 Низкая производительность или артефакты изображения в режиме 2D](#.D0.9D.D0.B8.D0.B7.D0.BA.D0.B0.D1.8F_.D0.BF.D1.80.D0.BE.D0.B8.D0.B7.D0.B2.D0.BE.D0.B4.D0.B8.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D0.BE.D1.81.D1.82.D1.8C_.D0.B8.D0.BB.D0.B8_.D0.B0.D1.80.D1.82.D0.B5.D1.84.D0.B0.D0.BA.D1.82.D1.8B_.D0.B8.D0.B7.D0.BE.D0.B1.D1.80.D0.B0.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F_.D0.B2_.D1.80.D0.B5.D0.B6.D0.B8.D0.BC.D0.B5_2D)
            *   [9.7.1.1 Проблема с драйвером видеокарты](#.D0.9F.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D0.B0_.D1.81_.D0.B4.D1.80.D0.B0.D0.B9.D0.B2.D0.B5.D1.80.D0.BE.D0.BC_.D0.B2.D0.B8.D0.B4.D0.B5.D0.BE.D0.BA.D0.B0.D1.80.D1.82.D1.8B)
            *   [9.7.1.2 Использование альтернативного рендера](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.B0.D0.BB.D1.8C.D1.82.D0.B5.D1.80.D0.BD.D0.B0.D1.82.D0.B8.D0.B2.D0.BD.D0.BE.D0.B3.D0.BE_.D1.80.D0.B5.D0.BD.D0.B4.D0.B5.D1.80.D0.B0)
        *   [9.7.2 Низкая производительность в режиме 3D](#.D0.9D.D0.B8.D0.B7.D0.BA.D0.B0.D1.8F_.D0.BF.D1.80.D0.BE.D0.B8.D0.B7.D0.B2.D0.BE.D0.B4.D0.B8.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D0.BE.D1.81.D1.82.D1.8C_.D0.B2_.D1.80.D0.B5.D0.B6.D0.B8.D0.BC.D0.B5_3D)
        *   [9.7.3 Композитные эффекты не работают с современной видеокартой Nvidia](#.D0.9A.D0.BE.D0.BC.D0.BF.D0.BE.D0.B7.D0.B8.D1.82.D0.BD.D1.8B.D0.B5_.D1.8D.D1.84.D1.84.D0.B5.D0.BA.D1.82.D1.8B_.D0.BD.D0.B5_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.B0.D1.8E.D1.82_.D1.81_.D1.81.D0.BE.D0.B2.D1.80.D0.B5.D0.BC.D0.B5.D0.BD.D0.BD.D0.BE.D0.B9_.D0.B2.D0.B8.D0.B4.D0.B5.D0.BE.D0.BA.D0.B0.D1.80.D1.82.D0.BE.D0.B9_Nvidia)
        *   [9.7.4 Мерцание окон в полноэкранном режиме при включенном композитном режиме](#.D0.9C.D0.B5.D1.80.D1.86.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BE.D0.BA.D0.BE.D0.BD_.D0.B2_.D0.BF.D0.BE.D0.BB.D0.BD.D0.BE.D1.8D.D0.BA.D1.80.D0.B0.D0.BD.D0.BD.D0.BE.D0.BC_.D1.80.D0.B5.D0.B6.D0.B8.D0.BC.D0.B5_.D0.BF.D1.80.D0.B8_.D0.B2.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.BD.D0.BE.D0.BC_.D0.BA.D0.BE.D0.BC.D0.BF.D0.BE.D0.B7.D0.B8.D1.82.D0.BD.D0.BE.D0.BC_.D1.80.D0.B5.D0.B6.D0.B8.D0.BC.D0.B5)
        *   [9.7.5 Screen tearing при включенном композитном режиме](#Screen_tearing_.D0.BF.D1.80.D0.B8_.D0.B2.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.BD.D0.BE.D0.BC_.D0.BA.D0.BE.D0.BC.D0.BF.D0.BE.D0.B7.D0.B8.D1.82.D0.BD.D0.BE.D0.BC_.D1.80.D0.B5.D0.B6.D0.B8.D0.BC.D0.B5)
        *   [9.7.6 Параметры экрана сбрасываются при перезагрузке (несколько мониторов)](#.D0.9F.D0.B0.D1.80.D0.B0.D0.BC.D0.B5.D1.82.D1.80.D1.8B_.D1.8D.D0.BA.D1.80.D0.B0.D0.BD.D0.B0_.D1.81.D0.B1.D1.80.D0.B0.D1.81.D1.8B.D0.B2.D0.B0.D1.8E.D1.82.D1.81.D1.8F_.D0.BF.D1.80.D0.B8_.D0.BF.D0.B5.D1.80.D0.B5.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B5_.28.D0.BD.D0.B5.D1.81.D0.BA.D0.BE.D0.BB.D1.8C.D0.BA.D0.BE_.D0.BC.D0.BE.D0.BD.D0.B8.D1.82.D0.BE.D1.80.D0.BE.D0.B2.29)
    *   [9.8 Проблемы со звуком в KDE](#.D0.9F.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D1.8B_.D1.81.D0.BE_.D0.B7.D0.B2.D1.83.D0.BA.D0.BE.D0.BC_.D0.B2_KDE)
        *   [9.8.1 ALSA related problems](#ALSA_related_problems)
            *   [9.8.1.1 Сообщения "Falling back to default" при попытке воcпроизвести любой звук](#.D0.A1.D0.BE.D0.BE.D0.B1.D1.89.D0.B5.D0.BD.D0.B8.D1.8F_.22Falling_back_to_default.22_.D0.BF.D1.80.D0.B8_.D0.BF.D0.BE.D0.BF.D1.8B.D1.82.D0.BA.D0.B5_.D0.B2.D0.BEc.D0.BF.D1.80.D0.BE.D0.B8.D0.B7.D0.B2.D0.B5.D1.81.D1.82.D0.B8_.D0.BB.D1.8E.D0.B1.D0.BE.D0.B9_.D0.B7.D0.B2.D1.83.D0.BA)
            *   [9.8.1.2 MP3-файлы не воспроизводятся с бэкендом GStreamer](#MP3-.D1.84.D0.B0.D0.B9.D0.BB.D1.8B_.D0.BD.D0.B5_.D0.B2.D0.BE.D1.81.D0.BF.D1.80.D0.BE.D0.B8.D0.B7.D0.B2.D0.BE.D0.B4.D1.8F.D1.82.D1.81.D1.8F_.D1.81_.D0.B1.D1.8D.D0.BA.D0.B5.D0.BD.D0.B4.D0.BE.D0.BC_GStreamer)
    *   [9.9 Konsole не сохраняет историю команд](#Konsole_.D0.BD.D0.B5_.D1.81.D0.BE.D1.85.D1.80.D0.B0.D0.BD.D1.8F.D0.B5.D1.82_.D0.B8.D1.81.D1.82.D0.BE.D1.80.D0.B8.D1.8E_.D0.BA.D0.BE.D0.BC.D0.B0.D0.BD.D0.B4)
    *   [9.10 В поле ввода пароля отображается по три точки на символ](#.D0.92_.D0.BF.D0.BE.D0.BB.D0.B5_.D0.B2.D0.B2.D0.BE.D0.B4.D0.B0_.D0.BF.D0.B0.D1.80.D0.BE.D0.BB.D1.8F_.D0.BE.D1.82.D0.BE.D0.B1.D1.80.D0.B0.D0.B6.D0.B0.D0.B5.D1.82.D1.81.D1.8F_.D0.BF.D0.BE_.D1.82.D1.80.D0.B8_.D1.82.D0.BE.D1.87.D0.BA.D0.B8_.D0.BD.D0.B0_.D1.81.D0.B8.D0.BC.D0.B2.D0.BE.D0.BB)
    *   [9.11 Dolphin и File Dialogs очень долго запускаются](#Dolphin_.D0.B8_File_Dialogs_.D0.BE.D1.87.D0.B5.D0.BD.D1.8C_.D0.B4.D0.BE.D0.BB.D0.B3.D0.BE_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA.D0.B0.D1.8E.D1.82.D1.81.D1.8F)
    *   [9.12 Средство просмотра PDF по умолчанию для приложений GTK в KDE](#.D0.A1.D1.80.D0.B5.D0.B4.D1.81.D1.82.D0.B2.D0.BE_.D0.BF.D1.80.D0.BE.D1.81.D0.BC.D0.BE.D1.82.D1.80.D0.B0_PDF_.D0.BF.D0.BE_.D1.83.D0.BC.D0.BE.D0.BB.D1.87.D0.B0.D0.BD.D0.B8.D1.8E_.D0.B4.D0.BB.D1.8F_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D0.B9_GTK_.D0.B2_KDE)
*   [10 Нестабильные версии](#.D0.9D.D0.B5.D1.81.D1.82.D0.B0.D0.B1.D0.B8.D0.BB.D1.8C.D0.BD.D1.8B.D0.B5_.D0.B2.D0.B5.D1.80.D1.81.D0.B8.D0.B8)
*   [11 Другие проекты KDE](#.D0.94.D1.80.D1.83.D0.B3.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B5.D0.BA.D1.82.D1.8B_KDE)
    *   [11.1 Trinity](#Trinity)
*   [12 Ошибки в программах](#.D0.9E.D1.88.D0.B8.D0.B1.D0.BA.D0.B8_.D0.B2_.D0.BF.D1.80.D0.BE.D0.B3.D1.80.D0.B0.D0.BC.D0.BC.D0.B0.D1.85)
*   [13 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Установка

Перед тем, как устанавливать KDE, убедитесь, что в вашей системе установлен и настроен сервер [X](/index.php/Xorg_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xorg (Русский)").

### Plasma 5

**Обратите внимание:**

*   Plasma 5 нельзя установить вместе со средой KDE 4
*   KDE 4 Plasma с августа 2015 года не поддерживается [[1]](https://www.kde.org/announcements/announce-applications-15.08.0.php)

**Важно:** Перед установкой Plasma удостоверьтесь, что в вашей системе установлен и успешно запускается [Xorg](/index.php/Xorg_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xorg (Русский)")

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") мета-пакет [plasma-meta](https://www.archlinux.org/packages/?name=plasma-meta) или группу пакетов [plasma](https://www.archlinux.org/groups/x86_64/plasma/). Для получения информации о различиях между ними смотрите статью [KDE Packages (Русский)](/index.php/KDE_Packages_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "KDE Packages (Русский)").

Если вам нужна полностью голая Plasma, [установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") лишь пакет [plasma-desktop](https://www.archlinux.org/packages/?name=plasma-desktop).

### Приложения KDE и языковые пакеты

Чтобы установить все приложения KDE, установите группу пакетов [kde-applications](https://www.archlinux.org/groups/x86_64/kde-applications/) или мета пакет [kde-applications-meta](https://www.archlinux.org/packages/?name=kde-applications-meta) для установки специфичных модулей. Заметьте что вы устанавливаете только приложения KDE.

Если вам нужно установить дополнительные языковые файлы, установите пакет `kde-l10n-**ваш язык**` (например [kde-l10n-de](https://www.archlinux.org/packages/?name=kde-l10n-de) для немецкого языка). Полный список доступных языков вы можете посмотреть на странице [здесь](https://www.archlinux.org/packages/extra/any/kde-l10n/).

### Обновление KDE4 до Plasma 5

1.  Выполните команду `systemctl isolate multi-user.target` от имени суперпользователя (текущие сессии пользователей при этом закроются)
2.  Обновите (если их нет, они будут установлены) пакеты [sddm](https://www.archlinux.org/packages/?name=sddm) и [sddm-kcm](https://www.archlinux.org/packages/?name=sddm-kcm), запустив от имени суперпользователя команду `pacman -Su sddm sddm-kcm`
3.  [Выключите](/index.php/%D0%92%D1%8B%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D0%B5 "Выключите") службу `kdm`, а вместо нее [включите](/index.php/%D0%92%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D0%B5 "Включите") `sddm`
4.  [Удалите](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A3.D0.B4.D0.B0.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.BE.D0.B2 "Pacman (Русский)") пакет [kdebase-workspace](https://aur.archlinux.org/packages/kdebase-workspace/)<sup><small>AUR</small></sup>
5.  Обновите пакет [plasma-meta](https://www.archlinux.org/packages/?name=plasma-meta) при помощи команды `pacman -Su plasma-meta`, запущенной от имени суперпользователя
6.  Перезагрузите машину
7.  На экране входа в систему вместо вместо Plasma Media Center выберите Plasma

## Запуск Plasma

**Tip:**

*   [KDM (Русский)](/index.php/KDM_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "KDM (Русский)") больше недоступен для Plasma 5\. KDE upstream [рекомендует](http://blog.davidedmundson.co.uk/blog/display_managers_finale) использовать [SDDM (Русский)](/index.php/SDDM_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "SDDM (Русский)") так как он имеет интерграцию с темами Plasma 5.
*   Plasma для большей интеграции с Plasma, мы рекомендуем отредактировать файл `/etc/sddm.conf` для использования темы Breeze. Ознакомтесь с [SDDM (Русский)#Настройки темы](/index.php/SDDM_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B8_.D1.82.D0.B5.D0.BC.D1.8B "SDDM (Русский)") с инструкцией.

Для запуска Plasma 5, выберите _Plasma_ в меню вашего [display manager (Русский)](/index.php/Display_manager_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Display manager (Русский)").

Также если вы хотите запускать окружение через _startx_, добавьте `exec startkde` в ваш `.xinitrc`, который находится в основном в домашней директории. Если вы хотите чтобы Xorg при входе в систему, ознакомтесь с этим: [xinitrc#Автозапуск X при входе в систему](/index.php/Xinitrc#.D0.90.D0.B2.D1.82.D0.BE.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA_X_.D0.BF.D1.80.D0.B8_.D0.B2.D1.85.D0.BE.D0.B4.D0.B5_.D0.B2_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.83 "Xinitrc").

## Настройка

Большинство настроек KDE 4 находятся в каталоге `~/.kde4`, если это не так, то в `~/.config` is used. Вообще, большинство настроек делаются в приложении **Настройка системы**. Его можно запустить в терминале командой _systemsettings_.

Frameworks 5 могут использовать настройки от KDE 4, однако конфигурационные файлы могут находится в разных местах. Для того чтобы разрешить Frameworks 5 приложениям запускаться в KDE 4 используя нужные настройки их можно отправить в новое место и создать символьную ссылку на старое место. Например:

*   Настройки konsole из `~/.kde4/share/apps/konsole` в `~/.local/share/konsole/`
*   Настройки оформления приложений из `~/.kde4/share/config/kdeglobals` в `~/.config/kdeglobals`

### Персонализация

#### Plasma desktop

##### Themes

[Темы для Plasma](http://kde-look.org/index.php?xcontentmode=76) используются для улучшения вида панелей и плазмоидов. Для большего удобства, многие темы есть в официальных репозиториях, а также [AUR](https://aur.archlinux.org/packages.php?O=0&K=plasmatheme&do_Search=в).

Самый легкий способ установить темы, это установка в _Настройки рабочего стола_ themes is by going through the Desktop Settings control panel:

```
 Workspace Theme > Desktop Theme > Get new Themes

```

Многие дополнительные скрипты для плазмоидов можно установить на сайте [kde-look.org](http://www.kde-look.org/).

###### Внешний вид Qt и GTK+

**Tip:** Для правильной работы тем на GTK и Qt, ознакомтесь с этим: [Uniform look for Qt and GTK applications](/index.php/Uniform_look_for_Qt_and_GTK_applications "Uniform look for Qt and GTK applications").

Qt4

Для приложений на Qt4, нужно установить [breeze-kde4](https://www.archlinux.org/packages/?name=breeze-kde4) и выбрать Breeze как GUI Стиль в `qtconfig-qt4`.

GTK+

Рекомендуемая тема для приложений на GTK+ это [gtk-theme-orion](https://aur.archlinux.org/packages/gtk-theme-orion/)<sup><small>AUR</small></sup>. Также посмотрите [gnome-breeze-git](https://aur.archlinux.org/packages/gnome-breeze-git/)<sup><small>AUR</small></sup>, это GTK+ тема имитирующая дизайн Plasma 5 Breeze. После того, как вы установили тему, выберите ее _System Settings > Application Style > GNOME Application Style_. Если не хотите всдеть эти настройки, установите одну из [настройщиков GTK+](/index.php/GTK%2B#Configuration_tools "GTK+"), например [lxappearance](https://www.archlinux.org/packages/?name=lxappearance) для изменения дизайна.

#### Рабочий стол Plasma

[Plasma](/index.php/Plasma "Plasma") берет на себя роль отображения рабочего стола, виджетов и панелей.

##### Темы

[Темы Plasma](http://kde-look.org/index.php?xcontentmode=76) можно установить в окне _Desktop Settings_. Темы Plasma определяют внешний вид панелей и плазмоидов. Для простой установки на уровне целой системы, некоторые такие темы доступны с пакетами в официальных репозиториях, а также в [AUR](https://aur.archlinux.org/packages.php?O=0&K=plasmatheme&do_Search=Go).

##### Виджеты

_Плазмоиды_ представляют собой небольшие приложения, предназначенные для расширения функциональности рабочего стола. Бинарные (скомпилированные) плазмоиды вы можете найти в AUR: [https://aur.archlinux.org/packages.php?O=0&K=plasmoid&do_Search=Go&PP=25&SO=d&SB=v](https://aur.archlinux.org/packages.php?O=0&K=plasmoid&do_Search=Go&PP=25&SO=d&SB=v). Скриптовые плазмоиды можно установить гораздо проще, перейдя через контекстное меню панели в _Add Widgets > Get new Widgets > Download Widgets_. Здесь вы сможете просматривать и загружать любые виджеты, размещенные на [kde-look.org](http://www.kde-look.org/), а также устанавливать, обновлять и удалять их.

Большинство плазмоидов созданы сторонними разработчиками. Вы также можете попробовать установить виджеты Mac OS X, Microsoft Windows Vista/7, Google Widgets и даже виджеты SuperKaramba.

##### Значки системного трея

Для настройки значков системного трея вам понадобится пакет [sni-qt](https://www.archlinux.org/packages/?name=sni-qt). Саму информацию о настройке вы сможете найти на странице [http://blog.martin-graesslin.com/blog/2014/03/system-tray-in-plasma-next](http://blog.martin-graesslin.com/blog/2014/03/system-tray-in-plasma-next).

##### Звуковой апплет в системном трее

Установите Kmix ([kdemultimedia-kmix](https://www.archlinux.org/packages/?name=kdemultimedia-kmix)) из официальных репозиториев и запустите его из меню запуска. Так как KDE, по умолчанию, автоматически запускает программы из предыдущего сеанса, нет необходимости запускать их вручную во время каждого входа.

**Обратите внимание:** Чтобы настроить [шаг регулировки звука](https://bugs.kde.org/show_bug.cgi?id=313579#c28), добавьте `VolumePercentageStep=_шаг_` в раздел `[Global]` файла `~/.kde4/share/config/kmixrc`, установив желаемый шаг (целое число).

##### Главное меню на рабочем столе

Вы можете добавить на рабочий стол панель, которая будет отображать главное меню выбранного окна (наподобие панели в Mac OS X). Для этого установите пакеты [appmenu-qt](https://www.archlinux.org/packages/?name=appmenu-qt)<sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/appmenu-qt)]</sup>, [appmenu-gtk](https://aur.archlinux.org/packages/appmenu-gtk/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/appmenu-gtk)]</sup> и [appmenu-qt5](https://aur.archlinux.org/packages/appmenu-qt5/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/appmenu-qt5)]</sup>. Чтобы [Firefox](/index.php/Firefox_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Firefox (Русский)") и [LibreOffice](/index.php/LibreOffice_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "LibreOffice (Русский)") также начали использовать эту панель, установите [firefox-extension-globalmenu](https://aur.archlinux.org/packages/firefox-extension-globalmenu/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/firefox-extension-globalmenu)]</sup> и [libreoffice-extension-menubar](https://aur.archlinux.org/packages/libreoffice-extension-menubar/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/libreoffice-extension-menubar)]</sup> соответственно.

**Обратите внимание:**

*   Пакет [appmenu-gtk](https://aur.archlinux.org/packages/appmenu-gtk/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/appmenu-gtk)]</sup> является осиротевшим, и Canonical прекратила его разработку в пользу unity-gtk-module, который зависит от Unity. На октябрь 2014 нет способа экспортировать меню gtk2,3 в KDE
*   [firefox-extension-globalmenu](https://aur.archlinux.org/packages/firefox-extension-globalmenu/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/firefox-extension-globalmenu)]</sup> устарел в Firefox версии 25, и на данный момент нет рекомендованного метода добавления поддержки панели главного меню для Firefox. Однако, есть пакет [firefox-ubuntu](https://aur.archlinux.org/packages/firefox-ubuntu/)<sup><small>AUR</small></sup>, который содержит патч от Canonical, добавляющий эту поддержку, которая пока еще работает (на ноябрь 2013)

Чтобы на самом деле добавить главное меню на рабочий стол, установите пакет [kdeplasma-applets-menubar](https://aur.archlinux.org/packages/kdeplasma-applets-menubar/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/kdeplasma-applets-menubar)]</sup>. Создайте панель наверху экрана и добавьте на него апплет меню окна. Чтобы экспортировать меню программ на панель, зайдите в _Настройки системы > Внешний вид приложений > Стиль_. Перейдите на вкладку _Тонкая настройка_ и выберите _только экспорт_ из выпадающего списка _Стиль менюбара_.

#### Декорации окон

[Декорации окон](http://kde-look.org/index.php?xcontentmode=75) настраиваются в _System Settings > Workspace Appearance > Window Decorations_. Здесь вы также сможете загрузить и установить новые темы оформления, кроме того, некоторые из них доступны в [AUR](https://aur.archlinux.org/packages.php?O=0&K=kdestyle&do_Search=Go&PP=25&SO=d&SB=v).

#### Темы значков

На панели _System Settings > Application Appearance > Icons_ вы сможете выбрать тему значков, а также загрузить новые темы. Многие из них также доступны на [kde-look.org](http://www.kde-look.org/).

Официальные логотипы, значки и прочие художества Arch Linux вы можете установить с пакетом [archlinux-artwork](https://aur.archlinux.org/packages/archlinux-artwork/)<sup><small>AUR</small></sup>. Содержимое пакета устанавливается в `/usr/share/archlinux/`.

#### Шрифты

##### Шрифты в KDE выглядят плохо

Первым делом, попробуйте установить шрифты [ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu) и [ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation).

После установки перезайдите в систему. Не меняйте ничего в _System Settings > Fonts_.

Если вы вносили изменения в параметры отображения шрифтов, имейте в виду, что панель _System Settings_ может сбить ваши установки (файл `fonts.conf`).

##### Огромные или непропорциональные буквы

Попробуйте установить DPI шрифта, равный 96 в _System Settings > Application Appearance > Fonts_.

Если это не помогло, попробуйте также установить DPI напрямую в X, как указано на странице [Xorg#Setting DPI manually](/index.php/Xorg#Setting_DPI_manually "Xorg").

#### Экономия места на экране

Пользователи с маленькими экранами (например, нетбуков) могут сделать KDE несколько более экономным в плане экранного пространства. Смотрите страницу [Using with small screens (eg Netbooks)](http://userbase.kde.org/KWin#Using_with_small_screens_.28eg_Netbooks.29) для получения дополнительной информации. Также, вы можете использовать [KDE's Plasma Netbook](http://www.kde.org/workspaces/plasmanetbook/), рабочая среда которого специально сделана удобной для использования с нетбуков.

### Сеть

Вы можете использовать следующие средства для настройки и подключению к сети:

*   NetworkManager: смотрите [NetworkManager#KDE](/index.php/NetworkManager#KDE "NetworkManager").
*   Wicd: смотрите [Wicd](/index.php/Wicd "Wicd").

### Печать

**Совет:** Используйте веб-интерфейс [CUPS](/index.php/CUPS "CUPS") для более быстрой настройки. Принтеры, настроенные таким образом, могут быть использованы приложениями KDE.

Настройка принтеров в KDE осуществляется на панели _System Settings > Printer Configuration_. Для этого необходимо сначала установить [kdeutils-print-manager](https://www.archlinux.org/packages/?name=kdeutils-print-manager)<sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): replaced by [print-manager](https://www.archlinux.org/packages/?name=print-manager)]</sup> и [cups](https://www.archlinux.org/packages/?name=cups).

Демоны `avahi-daemon` и `cupsd` должны быть запущены; в противном случае, вы получите ошибку:

```
The service 'Printer Configuration' does not provide an interface 'KCModule'
with keyword 'system-config- printer-kde/system-config-printer-kde.py'
The factory does not support creating components of the specified type.

```

Если вы получаете ошибку

```
There was an error during CUPS operation: 'cups-authorization-canceled'

```

то вам необходимо дать текущему пользователю право управления принтерами. В случае CUPS, это можно сделать в файле `/etc/cups/cups-files.conf`.

Вы можете создать специальную группу `lpadmin` для пользователей, которые имеют право настройки принтеров. Добавьте группу в список `SystemGroup` в `/etc/cups/cups-files.conf`, и все пользователи в ней смогут настраивать принтеры. _Не_ добавляйте группу `lp` этот список, иначе печать работать не будет.

```
# groupadd -g107 lpadmin

```

 `/etc/cups/cups-files.conf` 

```
# Administrator user group...
SystemGroup sys root lpadmin
```

**Совет:** Подробнее о настройке CUPS вы можете прочитать на странице [CUPS (Русский)](/index.php/CUPS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "CUPS (Русский)")

### Поддержка Samba/Windows

Если вы хотите получить доступ к службам Windows, установите [Samba](/index.php/Samba "Samba") (доступна с пакетом [samba](https://www.archlinux.org/packages/?name=samba)).

Для обмена файлами Dolphin требует настроить Usershare path (общий каталог), который отсутствует в стандартном файле настроек (`smb.conf`). Инструкции по его добавлению приведены на странице [Samba#Creating usershare path](/index.php/Samba#Creating_usershare_path "Samba"). После выполнения инструкций обмен файлами в Dolphin заработает "из коробки" (после перезапуска Samba).

### Комнаты KDE

Комнаты (_Desktop Activities_) представляют собой некое развитие идеи виртуальных рабочих столов с более независимой и гибкой настройкой.

На вашем рабочем столе кликните на плазмоиде Cashew и выберите _Activities_. Панель выбора комнаты появится внизу экрана. Вы можете переключаться между ними нажимая на соответствующие значки.

### Снижение энергопотребления

В KDE имеется встроенная служба оптимизации энергопотребления — "Powerdevil Power Management", которая может регулировать профиль энергопотребления системы и/или яркость экрана (если поддерживается).

Начиная с KDE 4.6, масштабирование частоты процессора больше не контролируется KDE. Предполагается, что она должна регулироваться автоматически оборудованием и/или ядром. Начиная с ядра Linux 3.3, Arch использует `ondemand` в качестве регулятора частоты по умолчанию, поэтому в большинстве случаев дополнительной настройки не требуется. Подробнее о настройке регулятора смотрите на странице [Масштабирование частоты ЦПУ](/index.php/%D0%9C%D0%B0%D1%81%D1%88%D1%82%D0%B0%D0%B1%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5_%D1%87%D0%B0%D1%81%D1%82%D0%BE%D1%82%D1%8B_%D0%A6%D0%9F%D0%A3 "Масштабирование частоты ЦПУ").

### Отслеживание изменений локальных файлов и каталогов

С недавних пор KDE использует **inotify** напрямую из ядра с **kdirwatch** (включенного в состав [kdelibs](https://www.archlinux.org/packages/?name=kdelibs)), поэтому [Gamin](/index.php/Gamin_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Gamin (Русский)") и [FAM](/index.php/GVFS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GVFS (Русский)") больше не нужны. Вы можете установить графическую оболочку **kdirwatch** с пакетом [kdirwatch](https://aur.archlinux.org/packages/kdirwatch/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/kdirwatch)]</sup>.

## Системное администрирование

### Настройка клавиатуры

Перейдите в _System Settings > Hardware > Input Devices > Keyboard_. На первой вкладке вы можете выбрать модель клавиатуры.

На вкладке _Layouts_ вы можете добавить раскладки для клавиатуры, нажав кнопку _Add Layout_.

На вкладке _Advanced_, в подменю _Key(s) to change layout_ вы можете выбрать сочетание клавиш для смены раскладки клавиатуры.

### Сочетание клавиш для остановки сервера X

Настройте _Key Sequence to kill the X server_ в _System Settings > Input Devices > Keyboard > Advanced_.

### KCM

Модули KCM (**K**DE **C**onfig **M**odule) добавляют компоненты настройки системы на панель _System Settings_.

**Настройка внешнего вида и поведения интерфейса приложений GTK.**

*   [kde-gtk-config](https://www.archlinux.org/packages/?name=kde-gtk-config)
*   [kcm-gtk](https://aur.archlinux.org/packages/kcm-gtk/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/kcm-gtk)]</sup>
*   [kcm-qt-graphicssystem](https://aur.archlinux.org/packages/kcm-qt-graphicssystem/)<sup><small>AUR</small></sup>

**Настройка загрузчика GRUB:**

*   [grub2-editor](https://aur.archlinux.org/packages/grub2-editor/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/grub2-editor)]</sup>

**Настройка тачпадов Synaptics:**

*   [kcm-touchpad](https://www.archlinux.org/packages/?name=kcm-touchpad)<sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/kcm-touchpad)]</sup>
*   [synaptiks](https://aur.archlinux.org/packages/synaptiks/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/synaptiks)]</sup>
*   [kcm_touchpad](https://aur.archlinux.org/packages/kcm_touchpad/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/kcm_touchpad)]</sup>
*   [kcm-touchpad-git](https://aur.archlinux.org/packages/kcm-touchpad-git/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/kcm-touchpad-git)]</sup>

**Настройка UFW ([Uncomplicated Firewall](/index.php/Uncomplicated_Firewall "Uncomplicated Firewall")):**

*   [kcm-ufw](https://aur.archlinux.org/packages/kcm-ufw/)<sup><small>AUR</small></sup>

**Настройка [PolicyKit](/index.php/PolicyKit "PolicyKit"):**

*   [kcm-polkit-kde-git](https://aur.archlinux.org/packages/kcm-polkit-kde-git/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/kcm-polkit-kde-git)]</sup>

**Настройки планшетов Wacom:**

*   [kcm-wacomtablet](https://aur.archlinux.org/packages/kcm-wacomtablet/)<sup><small>AUR</small></sup>

Множество модулей KCM вы также найдете на [kde-apps.org](http://kde-apps.org/index.php?xcontentmode=273).

### Автоматический вход в систему

Перейдите в _System Settings > System Administration > Login Screen > Convenience_, установите флажок _Enable Auto-Login_ и выберите пользователя для входа.

## Быстрый поиск и семантический рабочий стол

Из [Википедии](https://en.wikipedia.org/wiki/ru:%D0%A1%D0%B5%D0%BC%D0%B0%D0%BD%D1%82%D0%B8%D1%87%D0%B5%D1%81%D0%BA%D0%B8%D0%B9_%D1%80%D0%B0%D0%B1%D0%BE%D1%87%D0%B8%D0%B9_%D1%81%D1%82%D0%BE%D0%BB "wikipedia:ru:Семантический рабочий стол"):

_"Семантический рабочий стол (в информатике) — обобщенный термин, обозначающий идеи, связанные с изменением компьютерных пользовательских интерфейсов и возможностей управления данными так, что обмен ими между различными приложениями или задачами упрощается, и невозможная ранее автоматическая обработка данных одним компьютером становится возможной. Сюда также включаются некоторые идеи о возможности автоматического обмена информацией между людьми. Эта концепция связана с семантической паутиной, но отличается тем, что основной интерес представляет персональное использование информации."_

Реализация этой концепции в KDE (начиная с KDE Applications 4.13) связана с двумя основными проектами: Akonadi и Baloo. Эти программы анализируют ваши данные и индексируют их, позволяя легко и быстро производить по ним поиск. Суть в том, что другие программы могут использовать этот индекс и связанные с ним метаданные о ваших файлах для более эффективной работы. Baloo использует Xapian для хранения данных.

### Baloo

#### Настройка и использование Baloo

Нажмите `ALT+F2` для поиска на рабочем столе при помощи Baloo. В Dophin используйте комбинацию `CTRL+F`.

По умолчанию, модуль настройки _Desktop Search_ предоставляет вам только возможность добавлять каталоги в список исключенных для индексирования, и возможность глобально включать и отключать индексирование. Более полный модуль настройки доступен с пакетом [kcm_baloo_advanced](https://aur.archlinux.org/packages/kcm_baloo_advanced/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/kcm_baloo_advanced)]</sup>.

Также вы можете вручную отредактировать настройки в файле `~/.kde4/share/config/baloofilerc`. Например, для отключения Baloo добавьте:

```
[Basic Settings]
Indexing-Enabled=false

```

После добавления каталогов в список исключения/выключения Baloo, будет запущен специальный процесс `baloo_file_cleaner`, который удалит ненужные более файлы индекса из `~/.local/share/baloo/`.

#### Как проиндексировать съемное устройство?

По умолчанию, каталоги съемных устройств автоматически исключаются из индекса. Вам необходимо лишь удалить устройство из списка исключения в панели _Desktop Search_.

### Akonadi

Akonadi представляет собой хранилище данных для всех [PIM-приложений](https://en.wikipedia.org/wiki/ru:Kdepim "wikipedia:ru:Kdepim"). Сюда входят электронная почта, контакты, календари, события, журналы, личное расписание, будильник, новости и т. п.

#### Выключение Akonadi

Смотрите раздел [Disabling the Akonadi subsystem](http://userbase.kde.org/Akonadi#Disabling_the_Akonadi_subsystem) в базе знаний KDE.

#### Настройка базы данных

Запустите _akonaditray_ (предоставляемый пакетом [kdepim-runtime](https://www.archlinux.org/packages/?name=kdepim-runtime)). В системном трее появится значок Akonadi. В контекстном меню выберите _Configure_. Во вкладке _Akonadi server configure_ вы можете:

*   Настроить Akonadi для использования СУБД MySQL/MariaDB:
    *   Если ваш домашний каталог находится в пуле ZFS, создайте файл `~/.config/akonadi/mysql-local.conf` со следующим содержимым:

```
[mysqld]
innodb_use_native_aio = 0

```

иначе вы будете получать [ошибку 22](/index.php/MySQL#OS_error_22_when_running_on_ZFS "MySQL").

*   Настроить Akonadi для использования СУБД PostgreSQL
*   Настроить Akonadi для использования СУБД SQLite:
    *   Отредактируйте файл `~/.config/akonadi/akonadiserverrc` следующим образом:

```
[General]
Driver=QSQLITE3

```

```
[QSQLITE3]
Name=/home/_username_/.local/akonadi/akonadi.db

```

#### Использование KDE без Akonadi

Вы можете установить пакет-заглушку [akonadi-fake](https://aur.archlinux.org/packages/akonadi-fake/)<sup><small>AUR</small></sup>, который заменит собой [akonadi](https://www.archlinux.org/packages/?name=akonadi).

## Phonon

Из [Википедии](https://en.wikipedia.org/wiki/ru:Phonon "wikipedia:ru:Phonon"):

_"Phonon — мультимедийный фреймворк для KDE4, который предоставляет API для разработки мультимедиа-приложений. Phonon использует набор расширяемых модулей, выполняющих реальную работу."_

**Phonon** широко используется в среде KDE, как для аудио (например, для системных уведомлений), так и для видео (например, для видео-миниатюр в Dolphin).

### Какой бекэнд использовать?

На ваш выбор предоставляются различные бекэнды: [GStreamer](/index.php/GStreamer "GStreamer") ([phonon-gstreamer](https://www.archlinux.org/packages/?name=phonon-gstreamer)<sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): replaced by [phonon-qt4-gstreamer](https://www.archlinux.org/packages/?name=phonon-qt4-gstreamer)]</sup>) и [VLC](/index.php/VLC "VLC") ([phonon-qt4-vlc](https://www.archlinux.org/packages/?name=phonon-qt4-vlc), [phonon-qt5-vlc](https://www.archlinux.org/packages/?name=phonon-qt5-vlc)), доступные в [официальных репозиториях](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)"); [MPlayer](/index.php/MPlayer_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "MPlayer (Русский)") ([phonon-qt4-mplayer-git](https://aur.archlinux.org/packages/phonon-qt4-mplayer-git/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/phonon-qt4-mplayer-git)]</sup>), QuickTime ([phonon-quicktime-git](https://aur.archlinux.org/packages/phonon-quicktime-git/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/phonon-quicktime-git)]</sup>) и [AVKode](http://martinsandsmark.wordpress.com/2012/07/07/akademy/) ([phonon-avkode-git](https://aur.archlinux.org/packages/phonon-avkode-git/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/phonon-avkode-git)]</sup>), доступные в [AUR](/index.php/AUR_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AUR (Русский)").

Большинство пользователей предпочитают VLC, который поддерживается лучше всего. GStreamer в настоящий момент поддерживается слабее. Вы можете установить несколько бекэндов и выбирать нужный в _System Settings > Multimedia > Phonon > Backend_.

**Обратите внимание:**

*   Как указано на странице [Feature Matrix](http://community.kde.org/Phonon/FeatureMatrix), бекэнд GStreamer имеет больше возможностей, чем бекэнд VLC.
*   Как указано на странице [KDE UserBase](http://userbase.kde.org/Phonon#Backend_libraries), Phonon-MPlayer в настоящий момент не поддерживается.

## Полезные приложения

Официальный набор приложений KDE доступен на странице [http://www.kde.org/applications/](http://www.kde.org/applications/).

### Yakuake

[Yakuake](/index.php/Yakuake "Yakuake") предоставляет выпадающий сверху терминал в стиле консоли из игры Quake. Доступен в официальных репозиториях с пакетом [yakuake](https://www.archlinux.org/packages/?name=yakuake).

### KDE Telepathy

[KDE Telepathy](http://community.kde.org/KTp) — проект, направленный на обеспечение лучшей интеграции обмена мгновенными сообщениями с рабочим столом KDE, пришедший на смену Kopete. Использует фреймворк Telepathy в качестве бэкенда.

Чтобы установить все протоколы Telepathy, установите группу [telepathy](https://www.archlinux.org/groups/x86_64/telepathy/). Клиент Telepathy доступен с пакетом [kde-telepathy-meta](https://www.archlinux.org/packages/?name=kde-telepathy-meta)<sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): replaced by [telepathy-kde-meta](https://www.archlinux.org/packages/?name=telepathy-kde-meta)]</sup>, который также включает в себя все из группы [kde-telepathy](https://www.archlinux.org/groups/x86_64/kde-telepathy/)<sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): package not found]</sup>.

## Советы и рекомендации

### Использование альтернативного оконного менеджера с KDE

Для использования альтернативного [оконного менеджера](/index.php/Window_manager_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Window manager (Русский)") с KDE, откройте панель _System Settings_, перейдите в _Default Applications > Window Manager > Use a different window manager_ и выберите желаемый оконный менеджер из списка.

#### Сеанс KDE/Openbox

Пакет [openbox](https://www.archlinux.org/packages/?name=openbox) предоставляет сеанс для использования KDE с [Openbox](/index.php/Openbox "Openbox"). Чтобы ее использовать, выберите _KDE/Openbox_ из меню оконного менеджера.

Если вы запускаете сеансы вручную, добавьте следующую строку в ваш файл `.xinitrc`:

```
exec openbox-kde-session

```

#### Compiz custom

Если вы хотите задать какие-нибудь опции при запуске Compiz, выберите пункт _Compiz custom_ из списка оконных менеджеров и создайте скрипт `compiz-kde-launcher`, который будет запускать Compiz с нужными опциями:

 `/usr/local/bin/compiz-kde-launcher` 

```
#!/bin/bash

LIBGL_ALWAYS_INDIRECT=1
compiz --replace &
wait

```

Не забудьте сделать его исполняемым:

```
$ chmod +x /usr/local/bin/compiz-kde-launcher

```

#### Включение композитных эффектов

Если новый оконный менеджер не предоставляет композитный буфер (например, Openbox), все композитные эффекты рабочего стола (прозрачность и т. п.) пропадут. В этом случае, запустите и установите отдельный композитный менеджер, например, [Xcompmgr](/index.php/Xcompmgr "Xcompmgr") или [Compton](/index.php/Compton_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Compton (Русский)").

### Интеграция Android в рабочий стол KDE

Установите [kdeconnect](https://www.archlinux.org/packages/?name=kdeconnect) и приложение KDE Connect из [Play Store](https://play.google.com/store/apps/details?id=org.kde.kdeconnect_tp&hl=en) (или [F-Droid](https://f-droid.org/repository/browse/?fdid=org.kde.kdeconnect_tp)) для интеграции Android в KDE.

### Получение уведомлений о выходе обновлений ПО

Установите [apper](https://aur.archlinux.org/packages/apper/)<sup><small>AUR</small></sup> для получения уведомлений об обновлениях пакетов. Также он предоставляет простой графический интерфейс для управления пакетами. Подробнее смотрите на [веб-сайте PackageKit](http://www.packagekit.org/).

### Настройка KWin для использования OpenGL ES

Начиная с KWin 4.8 вы можете использовать отдельный исполняемый файл _kwin_gles_ вместо _kwin_. Он работает точно так же, как и _kwin_ в режиме OpenGL2, с тем отличием, что вместо `glx` используется интерфейс `egl`. Для проверки просто наберите `kwin_gles --replace` в терминале. Если вы хотите постоянно использовать _kwin_gles_, создайте скрипт в `$(kde4-config --localprefix)/env/`, который будет устанавливать переменную окружения `KDEWM=kwin_gles`.

### Отображение миниатюр для аудио- и видеофайлов в Konqueror/Dolphin

Для отображения миниатюр файлов видео установите [kdemultimedia-mplayerthumbs](https://www.archlinux.org/packages/?name=kdemultimedia-mplayerthumbs) или [kdemultimedia-ffmpegthumbs](https://www.archlinux.org/packages/?name=kdemultimedia-ffmpegthumbs)<sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): replaced by [ffmpegthumbs](https://www.archlinux.org/packages/?name=ffmpegthumbs)]</sup> и включите миниатюры в _Settings > Configure Konqueror > General > Previews > Video Files_.

Для отображения миниатюр аудиофайлов в Konqueror и Dolphin установите [audiothumbs](https://aur.archlinux.org/packages/audiothumbs/)<sup><small>AUR</small></sup> из AUR.

### Ускорение запуска приложений

Вы можете ускорить запуск приложений на 50-150 мсек, создав каталог:

```
$ mkdir ~/.compose-cache/

```

Однако, это может вызывать подвисания на медленном диске. Сделайте лучше так:

```
$ ln -sfv /run/user/$UID/ /home/$USER/.compose-cache

```

Источник: [http://kdemonkey.blogspot.nl/2008/04/magic-trick.html](http://kdemonkey.blogspot.nl/2008/04/magic-trick.html).

### Скрытие разделов

В Dolphin просто вызовите контекстное меню для раздела, который вы хотите скрыть (на панели `Places`) и выберите _Hide <partition>_.

Также вы можете создать для этого правило [udev](/index.php/Udev_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.9D.D0.B0.D0.BF.D0.B8.D1.81.D0.B0.D0.BD.D0.B8.D0.B5_.D1.81.D0.B2.D0.BE.D0.B8.D1.85_.D0.BF.D1.80.D0.B0.D0.B2.D0.B8.D0.BB "Udev (Русский)"):

 `/etc/udev/rules.d/10-local.rules`  `KERNEL=="sda[0-9]", ENV{UDISKS_IGNORE}="1"` 

Или, для конкретных разделов:

```
KERNEL=="sda1", ENV{UDISKS_IGNORE}="1"
KERNEL=="sda2", ENV{UDISKS_IGNORE}="1"

```

### Konqueror

#### Отключение Access Keys

Когда вы нажимаете `Ctrl` во время просмотра веб-страниц в браузере, над каждой активной областью (ссылкой) на странице появляются небольшие подсказки с буквами, благодаря которым вы можете перейти по соответствующей ссылке без использования мыши.

Для отключения Access Keys, перейдите в _Settings > Configure Konqueror > Web Browsing_ и снимите флажок _Enable Access Key activation with Ctrl key_.

#### Использование WebKit

WebKit — веб-движок с открытым исходным кодом, разрабатываемый корпорацией Apple на основе таких библиотек, как KHTML и KJS. WebKit используется Safari, Google Chrome и rekonq.

Вы можете использовать WebKit в Konqueror вместо KHTML. Первым делом установите пакет [kwebkitpart](https://www.archlinux.org/packages/?name=kwebkitpart). Затем, после запуска Konqueror, перейдите в _Settings > Configure Konqueror > General > Default web browser engine_ и выберите `WebKit`.

### Интеграция Firefox в KDE

Смотрите [Firefox#KDE integration](/index.php/Firefox#KDE_integration "Firefox").

### Установка фона для экрана блокировки

В настоящий момент вы [не можете](https://bugs.kde.org/show_bug.cgi?id=312828) установить собственное изображение для экрана блокировки, однако, существует решение из списка рассылки OpenSUSE: [http://lists.opensuse.org/opensuse-kde/2013-02/msg00082.html](http://lists.opensuse.org/opensuse-kde/2013-02/msg00082.html)

Для этого следует отредактировать файл `/usr/share/kde4/apps/ksmserver/screenlocker/org.kde.passworddialog/contents/ui/main.qml`, заменив строку

```
source: theme.wallpaperPathForSize(parent.width, parent.height)

```

на что-нибудь вроде

```
source: "1920x1080.jpg"

```

Теперь остается просто поместить свое изображение `1920x1080.jpg` в каталог `/usr/share/kde4/apps/ksmserver/screenlocker/org.kde.passworddialog/contents/ui`.

**Обратите внимание:** Вам придется выполнять эти действия заново при каждом обновлении [kdebase-workspace](https://aur.archlinux.org/packages/kdebase-workspace/)<sup><small>AUR</small></sup>.

### Еще один способ установки фона для экрана блокировки

Возьмите за основу существующий профиль обоев, скопировав его в пользовательский каталог:

```
$ cp -r /usr/share/wallpapers/_существующий_профиль_ ~/.kde4/share/wallpapers/

```

Переименуйте его, как вам нравится — например, в `MyWallpaper`, и отдерактируйте `metadata.desktop`:

 `~/.kde4/share/wallpapers/_MyWallpaper_/metadata.desktop` 

```
[Desktop Entry]
Name=_MyWallpaper_
X-KDE-PluginInfo-Name=_MyWallpaper_
```

Удалите из каталога существующие изображения:

```
$ rm ~/.kde4/share/wallpapers/_MyWallpaper_/contents/screenshot.png
$ rm ~/.kde4/share/wallpapers/_MyWallpaper_/contents/images/*

```

Добавьте свое изображение:

```
$ cp _путь/до/изображения.jpg_ ~/.kde4/share/wallpapers/_MyWallpaper_/contents/images/_1920x1080_.jpg

```

Соответственно, вместо `1920x1080` следует указать его фактическое разрешение.

Отредактируйте файл `metadata.desktop` вашей текущей темы:

 `~/.kde4/share/apps/desktoptheme/_MyTheme_/metadata.desktop` 

```
[Wallpaper]
defaultWallpaperTheme=_MyWallpaper_
defaultFileSuffix=.jpg
defaultWidth=1920
defaultHeight=1080
```

Сохраните файл и заблокируйте экран для проверки.

**Обратите внимание:** Этот метод позволяет изменить фон экрана блокировки без внесения изменений на системном уровне. Вы также можете создать свой профиль обоев в системном каталоге `/usr/share/wallpapers` и точно так же отредактировать исходные файлы вашей темы в `/usr/share/apps/desktoptheme`.

### Изменение фона экрана приветствия при запуске (Plasma 5)

Если изменение фона экрана приветствия в _System Settings_ невозможно (не работает):

```
$ themedir=`cat ~/.config/ksplashrc | grep 'Theme=' | sed 's/Theme=//g'`
$ sudo mv /usr/share/plasma/look-and-feel/$themedir/contents/splash/images/background.png /usr/share/plasma/look-and-feel/$themedir/contents/splash/images/background.png.bkp
$ sudo cp _path/to/MyWallpaper.png_ /usr/share/plasma/look-and-feel/$themedir/contents/splash/images/background.png
$ sudo chmod -x /usr/share/plasma/look-and-feel/$themedir/contents/splash/images/background.png

```

Поменяйте `path/to/MyWallpaper.png` на путь до желаемого изображения. В идеале, оно должно иметь размер, совпадающий с разрешением вашего экрана.

**Обратите внимание:** Вам придется выполнять эти действия заново при каждом обновлении.

## Решение проблем

### Отсутствие иконок в трее (KDE5)

В KDE5 по умолчанию в трее отображаются иконки только от стандартных приложений. Другие же приложения (например Skype) в трее не отображаются. Для решения этой проблемы требуется установить следущие пакеты: [sni-qt](https://www.archlinux.org/packages/?name=sni-qt) и [lib32-sni-qt](https://www.archlinux.org/packages/?name=lib32-sni-qt). После этого перезагрузите компьютер.

### Проблемы с настройками

Множество проблем в KDE возникают из-за ошибок в файлах настроек. Одним из способов решать такие проблемы — сбрасывать настройки KDE целиком.

#### Полный сброс настроек KDE

Чтобы проверить, вызвана ли проблема ошибками в настройках, выйдите из сеанса KDE, войдите в терминал и наберите

```
$ cp -r ~/.kde4 ~/.kde4.safekeeping
$ rm ~/.kde4/{cache,socket,tmp}-$(hostname)

```

Команда _rm_ в данном случае просто удалит символические ссылки, которые потом пересоздадутся автоматически. Войдите теперь в сеанс KDE и проверьте, решилась ли проблема.

Если это так, вы теперь можете переместить группами сохраненные в `~/.kde4.safekeeping` файлы настроек обратно, постоянно проверяя, не возникли ли проблемы снова. Некоторые файлы используются только приложениями, поэтому вам даже не придется перезапускать KDE для проверки.

#### Странное поведение рабочего стола Plasma

Проблемы в Plasma обычно вызываются нестабильными плазмоидами или темами Plasma. Первым делом найдите, какие из последних плазмоидов или тем вы устанавливали и попробуйте их отключить/удалить. Если вы не помните, какие из них вы устанавливали последними, попробуйте исключать все по одному.

Если вы не смогли обнаружить проблему, попробуйте сбросить настройки Plasma:

```
$ mkdir ~/.plasma-config-backup
$ mv -r ~/.kde4/share/config/plasma* ~/.plasma-config-backup

```

и перезайдите в систему.

#### Очистка кэша для решения проблем с обновлением

После обновления устаревшие данные в кэше могут вызывать странное, мало предсказуемое и трудное в отладке поведение рабочего стола или программ KDE.

Попробуйте перестроить кэш с помощью команд:

```
$ rm ~/.config/Trolltech.conf
$ kbuildsycoca4 --noincremental

```

### Сброс настроек Akonadi для решения проблем с KMail

Первым делом убедитесь, что KMail не запущен. Сохраните настройки Akonadi:

```
$ cp ~/.local/share/akonadi ~/.local/share/akonadi-old
$ cp ~/.config/akonadi ~/.config/akonadi-old

```

Откройте _SystemSettings > Personal_ и удалите все ресурсы. Вернитесь в терминал и удалите исходные файлы настроек:

```
$ rm ~/.local/share/akonadi ~/.config/akonadi

```

Снова вернитесь к _SystemSettings_ и внимательно добавьте все необходимые ресурсы. Сохраните настройки и запустите Kontact/KMail чтобы убедиться, что теперь все работает корректно.

### Текущее состояние KWin для поддержки и отладки

Эта команда выведет полную сводку о текущем состоянии KWin включая ваши настройки, данные о композитном бэкенде и драйвере OpenGL:

```
$ qdbus org.kde.kwin /KWin supportInformation

```

Подробнее смотрите на странице [http://blog.martin-graesslin.com/blog/2012/03/on-getting-help-for-kwin-and-helping-kwin](http://blog.martin-graesslin.com/blog/2012/03/on-getting-help-for-kwin-and-helping-kwin).

### KDE4 зависает на этапе загрузки

Возможна ситуация, при которой драйвер видеокарты [NVIDIA](/index.php/NVIDIA "NVIDIA") вызывает конфликт во время запуска KDE4\. После входа в систему вы видете только экран загрузки и ничего больше не происходит.

Решение заключается в отключении композитного режима:

 `~/.kde4/share/config/kwinrc` 

```
[Compositing]
Enabled=false
```

Подробнее смотрите на странице [https://bbs.archlinux.org/viewtopic.php?pid=932598](https://bbs.archlinux.org/viewtopic.php?pid=932598).

### Программы KDE выглядят плохо в другом оконном менеджере

Если вы используете программы Qt вне сеанса KDE (то есть, вы не запускаете `startkde`), вам необходимо явно указать Qt, где находятся стили KDE (Oxygen, QtCurve и т. д.).

Для этого установите переменную окружения `QT_PLUGIN_PATH`, добавив в ваш файл инициализации командной оболочки (`~/.profile`) строку:

```
export QT_PLUGIN_PATH=$HOME/.kde4/lib/kde4/plugins/:/usr/lib/kde4/plugins/

```

Перезайдите в систему. Теперь все должно быть впорядке.

Также вы можете создать символическую ссылку на стили KDE в каталоге Qt:

```
# ln -s /usr/lib/kde4/plugins/styles/ /usr/lib/qt4/pluginlib32-libdbusmenu-glibs/styles

```

В GNOME вы также можете попробовать установить пакет [libgnomeui](https://www.archlinux.org/packages/?name=libgnomeui).

### Проблемы с графикой

#### Низкая производительность или артефакты изображения в режиме 2D

##### Проблема с драйвером видеокарты

Убедитесь, что установлен подходящий драйвер для вашей видеокарты, для того, чтобы как минимум режим 2D использовал ее ресурсы для ускорения. Подробнее смотрите на страницах [ATI](/index.php/ATI "ATI"), [NVIDIA](/index.php/NVIDIA "NVIDIA"), [Intel](/index.php/Intel "Intel").

Открытые драйверы ATI и Intel и проприетарный драйвер Nvidia должны (теоретически) обеспечить вам наилучшее ускорение как в режиме 2D, так и в 3D.

##### Использование альтернативного рендера

Если установка правильного драйвера не решила вашу проблему, вероятно, ваш драйвер не предоставляет ускорения **XRender**, который используется как рендер в Qt.

Вы можете выбрать другой рендер — например, Raster, запустив приложение Qt с опцией `-graphicssystem raster`. Вы можете установить другой рендер по умолчанию, пересобрав ваш Qt с той же опцией (`-graphicssystem raster`) _configure_.

Рендер Raster использует процессор компьютера для выполнения большей части отрисовки. В зависимости от вашей системы, это может улучшить производительность. Поэтому используйте Raster, только если у вас возникают проблемы или ваша графическая подсистема значительно менее производительна, чем центральный процессор; в ином случае, рекомендуется использовать XRender.

Начиная с Qt 4.7, пересборка Qt не обязательна. Установите переменную окружения `QT_GRAPHICSSYSTEM=raster`; также возможны значения `opengl` и `native`. Raster использует процессор CPU, OpenGL полагается на драйвер видеокарты, а Native использует отрисовку средствами X11 (смешанный подход).

Вы также можете просто установить [kcm-qt-graphicssystem](https://aur.archlinux.org/packages/kcm-qt-graphicssystem/)<sup><small>AUR</small></sup> из AUR и выбрать рендер на панели _System Settings > Qt Graphics System_.

Подробности смотрите на страницах [http://apachelog.wordpress.com/2010/09/05/qt-graphics-system-kcm](http://apachelog.wordpress.com/2010/09/05/qt-graphics-system-kcm) и [http://labs.trolltech.com/blogs/2009/12/18/qt-graphics-and-performance-the-raster-engine](http://labs.trolltech.com/blogs/2009/12/18/qt-graphics-and-performance-the-raster-engine).

#### Низкая производительность в режиме 3D

По умолчанию эффекты рабочего стола включены. Старые видеокарты могут не давать приемлемую производительность рабочего стола в режиме 3D. В таком случае, отключите эффекты рабочего стола в _System Settings > Desktop Effects_.

**Обратите внимание:** Вы можете наблюдать недостаточную производительность рабочего стола в режиме 3D даже при использовании более современной видеокарты, особенно с проприетарным драйвером Catalyst (`fglrx`). Этот драйвер известен своими проблемами с ускорением 3D. Обратитесь за помощью на страницу [ATI](/index.php/ATI "ATI").

#### Композитные эффекты не работают с современной видеокартой Nvidia

Содержимое файла настроек KWin может портиться (файл `kwinrc`), что, в свою очередь, может приводить к проблеме повторного включения композитного режима `OpenGL`. Это может происходить случайно (например, из-за падения/перезапуска сервера X), поэтому, если подобное произошло, просто удалите файл `~/.kde4/share/config/kwinrc` и перезайдите в систему. Будет создан файл со стандартными настройками и проблема должна решиться.

#### Мерцание окон в полноэкранном режиме при включенном композитном режиме

С версии KDE SC 4.6.0 на панели _Sytem Settings > Desktop Effect > Advanced_ добавлен флажок _Suspend desktop effects for fullscreen windows_. Снимите его и проблема должна решиться.

#### Screen tearing при включенном композитном режиме

[Screen tearing](https://en.wikipedia.org/wiki/Screen_tearing "wikipedia:Screen tearing") представляет собой неисправность, при которой вы видите на экране не перерисованный полностью кадр. Это проявляется в возникновении видимых горизонтальных границ между старым изображением и новым, которые мерцают по всему экрану при активной перерисовке изображения (например, во время воспроизведения анимации или видео).

**Обратите внимание:** С версии KDE 4.11, было добавлено несколько опций вертикальной синхронизации (Vsync), что может помочь в решении проблемы.

Вы можете наблюдать Screen tearing при воспроизведении композитных эффектов рабочего стола. Снимите флажок _Use Vsync_ на панели _System Settings > Desktop Effects > Advanced_.

Если вы используете проприетарный драйвер, убедитесь, что вертикальная синхронизация включена в вашем драйвере (используйте _ic|amdccle_, если у вас [Catalyst](/index.php/Catalyst "Catalyst"), и _nvidia-settings_ для [NVIDIA](/index.php/NVIDIA "NVIDIA")).

#### Параметры экрана сбрасываются при перезагрузке (несколько мониторов)

Установка [kscreen](https://www.archlinux.org/packages/?name=kscreen) может решить проблему, но если только ваши мониторы не имеют одинаковый EDID. Kscreen представляет собой улучшенный менеджер дисплеев для KDE; подробнее смотрите на странице [https://fedoraproject.org/wiki/Changes/KScreen?rd=Features/KScreen](https://fedoraproject.org/wiki/Changes/KScreen?rd=Features/KScreen).

### Проблемы со звуком в KDE

#### ALSA related problems

**Обратите внимание:** Первым делом убедитесь, что у вас установлены пакеты [alsa-lib](https://www.archlinux.org/packages/?name=alsa-lib) [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils).

##### Сообщения "Falling back to default" при попытке воcпроизвести любой звук

Если появляются сообщения наподобие:

```
The audio playback device _имя_устройства_ does not work.
Falling back to default

```

Перейдите в _System Settings > Multimedia > Phonon_ и переместите устройство `default` наверх списка.

##### MP3-файлы не воспроизводятся с бэкендом GStreamer

Эту проблему можно решить, установив плагин libav (пакет [gst-libav](https://www.archlinux.org/packages/?name=gst-libav)) для GStreamer. Если вы все еще испытываете проблемы, вы можете попробовать другой бэкенд Phonon, например [phonon-vlc](https://www.archlinux.org/packages/?name=phonon-vlc)<sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): replaced by [phonon-qt4-vlc](https://www.archlinux.org/packages/?name=phonon-qt4-vlc)]</sup>.

После установки перейдите в _System Settings > Multimedia > Phonon > Backend_ и выберите новый бэкенд.

### Konsole не сохраняет историю команд

По умолчанию, история команд сохраняется только если вы выходите, набрав `exit` в консоли. Если вы просто закрываете окно Konsole, история сохранена не будет. Чтобы включить сохранение истории после ввода каждой команды, добавьте следующие строки в файл инициализации вашей командной оболочки:

 `~/.bashrc` 

```
shopt -s histappend
[[ "${PROMPT_COMMAND}" ]] && PROMPT_COMMAND="$PROMPT_COMMAND;history -a" || PROMPT_COMMAND="history -a"

```

### В поле ввода пароля отображается по три точки на символ

Это настраивается в _System Settings > Account Details > Password & User Account_. Вы можете выбрать из следующих вариантов:

*   Показывать одну точку на каждый символ
*   Показывать три точки на каждый символ
*   Ничего не показывать

### Dolphin и File Dialogs очень долго запускаются

Это может быть вызвано службой `upower`. Если эта служба не нужна в вашей системе, отключите ее:

```
# systemctl disable upower
# systemctl mask upower

```

### Средство просмотра PDF по умолчанию для приложений GTK в KDE

В некоторых случаях, если установлен графический редактор ([Inkscape](/index.php/Inkscape "Inkscape"), [Gimp](/index.php/Gimp "Gimp") и т. д.), приложения GTK ([Firefox](/index.php/Firefox "Firefox"), например) могут перестать использовать Okular в качестве средства просмотра PDF по умолчанию (или, в общем случае, вообще перестают следовать выбору программ по умолчанию в KDE). Вы можете использовать следующую команду для того, чтобы снова заставить приложения GTK использовать Okular:

```
$ xdg-mime default kde4-okularApplication_pdf.desktop application/pdf

```

Измените команду соответствующим образом, если вы используете другое средство просмотра PDF или у вас проблемы с другим [MIME-типом](https://en.wikipedia.org/wiki/ru:MIME "wikipedia:ru:MIME").

Подробнее смотрите на странице [Default applications](/index.php/Default_applications "Default applications").

## Нестабильные версии

Когда версии KDE присваивается статус бета-релиза или RC-релиза, соответствующие "нестабильные" пакеты KDE выгружаются в репозиторий _kde-unstable_. Они находятся там, пока версия не будет признана стабильной — тогда эти пакеты переносятся в репозиторий _extra_.

Вы можете включить у себя репозиторий _kde-unstable_, добавив следующие строки в `/etc/pacman.conf`:

```
[kde-unstable]
Include = /etc/pacman.d/mirrorlist

```

перед секцией `[extra]`.

**Важно:** Если вы добавите `kde-unstable` после `extra`, это не даст никакого эффекта: pacman будет предпочитать стабильные пакеты из `extra`.

## Другие проекты KDE

### Trinity

С выходом KDE 4.x была прекращена поддержка версий KDE 3.5.x. Trinity Desktop Environment — форк KDE 3, разрабатываемый Тимоти Пирсоном ([trinitydesktop.org](http://trinitydesktop.org/)). Этот проект направлен на создание стабильного рабочего окружения с сохранением стиля KDE 3.5 (за основу взята версия KDE 3.5.10). Подробнее смотрите на странице [Trinity](/index.php/Trinity "Trinity").

**Важно:** KDE 3 больше не поддерживается. Проект "Trinity KDE" поддерживается сообществом Trinity. Используйте KDE 3 на свой страх и риск, принимая возможность столкнуться с ошибками в программах, проблемами с производительностью и безопасностью.

## Ошибки в программах

Если вы обнаружили ошибку в программе KDE, посетите [багтрекер Arch Linux](https://bugs.archlinux.org) и/или [багтрекер KDE](http://bugs.kde.org), чтобы сообщить о ней.

## Смотрите также

*   [Домашняя страница KDE](http://www.kde.org)
*   [Баг-трекер KDE](https://bugs.kde.org)
*   [Проекты KDE](https://projects.kde.org)

Retrieved from "[https://wiki.archlinux.org/index.php?title=KDE_(Русский)&oldid=413321](https://wiki.archlinux.org/index.php?title=KDE_(Русский)&oldid=413321)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [KDE (Русский)](/index.php/Category:KDE_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Category:KDE (Русский)")
*   [Русский](/index.php/Category:%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9 "Category:Русский")