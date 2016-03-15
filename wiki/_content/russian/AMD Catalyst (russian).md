Владельцы видеокарт ATI/AMD имеют выбор между проприетарным ([catalyst](https://aur.archlinux.org/packages/catalyst/)) и [открытым драйвером](/index.php/ATI_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ATI (Русский)") ([xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati)). Эта статья описывает проприетарный драйвер.

Пакет с драйвером AMD для Linux, *catalyst*, раньше назывался *fglrx* (**F**ire**GL** и **R**adeon **X**). Было изменено только имя пакета, в то время как модуль ядра сохраняет исходное имя *fglrx.ko*. Таким образом, любое упоминание о fglrx ниже, является отсылкой к *модулю ядра*, а **не к пакету**.

**Пакет Catalyst больше не размещается в официальных репозиториях.** В прошлом, поддержка Catalyst была [прекращена](https://www.archlinux.org/news/ati-catalyst-support-dropped/), в связи с неудовлетвореностью качеством и скоростью разработки. После короткого возвращения, поддержка снова была прекращена в апреле 2013 и ее не вернули до сих пор.

В сравнении с открытым драйвером, Catalyst лучше выполняет визуализацию 2D и 3D, а также имеет лучшее управление энергопотреблением, но он неэфективен в поддержке нескольких экранов. Поддерживаемые устройства [ATI/AMD Radeon](https://en.wikipedia.org/wiki/ru:Radeon "wikipedia:ru:Radeon") - это видео карты с чипсетом R600 и новее (Radeon HD 2xxx и новее). Смотрите [кольцо декодирования Xorg](http://www.x.org/wiki/RadeonFeature/#index5h2) или [эту таблицу](https://en.wikipedia.org/wiki/Comparison_of_AMD_graphics_processing_units "wikipedia:Comparison of AMD graphics processing units"), переводите имя *модели* (X1900, HD4850) в/из имя *чипа* (R580, RV770 соответственно).

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
    *   [1.1 Установка драйвера](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.B4.D1.80.D0.B0.D0.B9.D0.B2.D0.B5.D1.80.D0.B0)
        *   [1.1.1 Установка из неофициального репозитория](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.B8.D0.B7_.D0.BD.D0.B5.D0.BE.D1.84.D0.B8.D1.86.D0.B8.D0.B0.D0.BB.D1.8C.D0.BD.D0.BE.D0.B3.D0.BE_.D1.80.D0.B5.D0.BF.D0.BE.D0.B7.D0.B8.D1.82.D0.BE.D1.80.D0.B8.D1.8F)
        *   [1.1.2 Установка из AUR](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.B8.D0.B7_AUR)
    *   [1.2 Конфигурация драйвера](#.D0.9A.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D1.8F_.D0.B4.D1.80.D0.B0.D0.B9.D0.B2.D0.B5.D1.80.D0.B0)
        *   [1.2.1 Конфигурация X](#.D0.9A.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D1.8F_X)
        *   [1.2.2 Загрузка модуля при загрузе](#.D0.97.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B0_.D0.BC.D0.BE.D0.B4.D1.83.D0.BB.D1.8F_.D0.BF.D1.80.D0.B8_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.B5)
        *   [1.2.3 Отключение kernel mode setting](#.D0.9E.D1.82.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_kernel_mode_setting)
        *   [1.2.4 Проверка работоспособности](#.D0.9F.D1.80.D0.BE.D0.B2.D0.B5.D1.80.D0.BA.D0.B0_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.BE.D1.81.D0.BF.D0.BE.D1.81.D0.BE.D0.B1.D0.BD.D0.BE.D1.81.D1.82.D0.B8)
    *   [1.3 Пользовательские ядра](#.D0.9F.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D1.8C.D1.81.D0.BA.D0.B8.D0.B5_.D1.8F.D0.B4.D1.80.D0.B0)
    *   [1.4 Поддержка PowerXpress](#.D0.9F.D0.BE.D0.B4.D0.B4.D0.B5.D1.80.D0.B6.D0.BA.D0.B0_PowerXpress)
        *   [1.4.1 Запуск двух X серверов (один использующий драйвер Intel, другой fglrx) одновременно](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D0.B4.D0.B2.D1.83.D1.85_X_.D1.81.D0.B5.D1.80.D0.B2.D0.B5.D1.80.D0.BE.D0.B2_.28.D0.BE.D0.B4.D0.B8.D0.BD_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D1.83.D1.8E.D1.89.D0.B8.D0.B9_.D0.B4.D1.80.D0.B0.D0.B9.D0.B2.D0.B5.D1.80_Intel.2C_.D0.B4.D1.80.D1.83.D0.B3.D0.BE.D0.B9_fglrx.29_.D0.BE.D0.B4.D0.BD.D0.BE.D0.B2.D1.80.D0.B5.D0.BC.D0.B5.D0.BD.D0.BD.D0.BE)
        *   [1.4.2 Проблемы с PowerXpress на ноутбуке запущенный в режиме AMD (pxp_switch_catalyst amd) с внешним / вторым монитором](#.D0.9F.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D1.8B_.D1.81_PowerXpress_.D0.BD.D0.B0_.D0.BD.D0.BE.D1.83.D1.82.D0.B1.D1.83.D0.BA.D0.B5_.D0.B7.D0.B0.D0.BF.D1.83.D1.89.D0.B5.D0.BD.D0.BD.D1.8B.D0.B9_.D0.B2_.D1.80.D0.B5.D0.B6.D0.B8.D0.BC.D0.B5_AMD_.28pxp_switch_catalyst_amd.29_.D1.81_.D0.B2.D0.BD.D0.B5.D1.88.D0.BD.D0.B8.D0.BC_.2F_.D0.B2.D1.82.D0.BE.D1.80.D1.8B.D0.BC_.D0.BC.D0.BE.D0.BD.D0.B8.D1.82.D0.BE.D1.80.D0.BE.D0.BC)
*   [2 Репозитории Xorg](#.D0.A0.D0.B5.D0.BF.D0.BE.D0.B7.D0.B8.D1.82.D0.BE.D1.80.D0.B8.D0.B8_Xorg)
    *   [2.1 xorg117](#xorg117)
    *   [2.2 xorg116](#xorg116)
    *   [2.3 xorg115](#xorg115)
    *   [2.4 xorg114](#xorg114)
    *   [2.5 xorg113](#xorg113)
    *   [2.6 xorg112](#xorg112)
*   [3 Инструменты](#.D0.98.D0.BD.D1.81.D1.82.D1.80.D1.83.D0.BC.D0.B5.D0.BD.D1.82.D1.8B)
    *   [3.1 Catalyst-hook](#Catalyst-hook)
    *   [3.2 Catalyst-generator](#Catalyst-generator)
    *   [3.3 Разработка OpenCL и OpenGL](#.D0.A0.D0.B0.D0.B7.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.BA.D0.B0_OpenCL_.D0.B8_OpenGL)
        *   [3.3.1 amdapp-aparapi](#amdapp-aparapi)
        *   [3.3.2 amdapp-sdk (ранее известный как amdstream)](#amdapp-sdk_.28.D1.80.D0.B0.D0.BD.D0.B5.D0.B5_.D0.B8.D0.B7.D0.B2.D0.B5.D1.81.D1.82.D0.BD.D1.8B.D0.B9_.D0.BA.D0.B0.D0.BA_amdstream.29)
        *   [3.3.3 amdapp-codexl](#amdapp-codexl)
*   [4 Преимущества](#.D0.9F.D1.80.D0.B5.D0.B8.D0.BC.D1.83.D1.89.D0.B5.D1.81.D1.82.D0.B2.D0.B0)
    *   [4.1 Tear Free Rendering](#Tear_Free_Rendering)
    *   [4.2 Аппаратное ускорение](#.D0.90.D0.BF.D0.BF.D0.B0.D1.80.D0.B0.D1.82.D0.BD.D0.BE.D0.B5_.D1.83.D1.81.D0.BA.D0.BE.D1.80.D0.B5.D0.BD.D0.B8.D0.B5)
    *   [4.3 Частота, температура, скорость вентилятора, утилиты для разгона GPU/Памяти](#.D0.A7.D0.B0.D1.81.D1.82.D0.BE.D1.82.D0.B0.2C_.D1.82.D0.B5.D0.BC.D0.BF.D0.B5.D1.80.D0.B0.D1.82.D1.83.D1.80.D0.B0.2C_.D1.81.D0.BA.D0.BE.D1.80.D0.BE.D1.81.D1.82.D1.8C_.D0.B2.D0.B5.D0.BD.D1.82.D0.B8.D0.BB.D1.8F.D1.82.D0.BE.D1.80.D0.B0.2C_.D1.83.D1.82.D0.B8.D0.BB.D0.B8.D1.82.D1.8B_.D0.B4.D0.BB.D1.8F_.D1.80.D0.B0.D0.B7.D0.B3.D0.BE.D0.BD.D0.B0_GPU.2F.D0.9F.D0.B0.D0.BC.D1.8F.D1.82.D0.B8)
    *   [4.4 Два экрана (Dual Head / Dual Screen / Xinerama)](#.D0.94.D0.B2.D0.B0_.D1.8D.D0.BA.D1.80.D0.B0.D0.BD.D0.B0_.28Dual_Head_.2F_Dual_Screen_.2F_Xinerama.29)
        *   [4.4.1 Введение](#.D0.92.D0.B2.D0.B5.D0.B4.D0.B5.D0.BD.D0.B8.D0.B5)
        *   [4.4.2 ATI Catalyst Control Center](#ATI_Catalyst_Control_Center)
        *   [4.4.3 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_2)
        *   [4.4.4 Конфигурация](#.D0.9A.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D1.8F)
*   [5 Удаление](#.D0.A3.D0.B4.D0.B0.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5)
*   [6 Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [6.1 Не удалось запустить atieventsd.service](#.D0.9D.D0.B5_.D1.83.D0.B4.D0.B0.D0.BB.D0.BE.D1.81.D1.8C_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D1.82.D0.B8.D1.82.D1.8C_atieventsd.service)
    *   [6.2 Не удалось открыть fglrx_dri.so](#.D0.9D.D0.B5_.D1.83.D0.B4.D0.B0.D0.BB.D0.BE.D1.81.D1.8C_.D0.BE.D1.82.D0.BA.D1.80.D1.8B.D1.82.D1.8C_fglrx_dri.so)
    *   [6.3 Не запускается GDM](#.D0.9D.D0.B5_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA.D0.B0.D0.B5.D1.82.D1.81.D1.8F_GDM)
    *   [6.4 Притормаживают 3D приложения в Wine](#.D0.9F.D1.80.D0.B8.D1.82.D0.BE.D1.80.D0.BC.D0.B0.D0.B6.D0.B8.D0.B2.D0.B0.D1.8E.D1.82_3D_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F_.D0.B2_Wine)
    *   [6.5 Проблема с цветами в видео](#.D0.9F.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D0.B0_.D1.81_.D1.86.D0.B2.D0.B5.D1.82.D0.B0.D0.BC.D0.B8_.D0.B2_.D0.B2.D0.B8.D0.B4.D0.B5.D0.BE)
    *   [6.6 KWin и композит](#KWin_.D0.B8_.D0.BA.D0.BE.D0.BC.D0.BF.D0.BE.D0.B7.D0.B8.D1.82)
    *   [6.7 Черный экран с полным зависанием и/или притормаживания после перезагрузки или startx](#.D0.A7.D0.B5.D1.80.D0.BD.D1.8B.D0.B9_.D1.8D.D0.BA.D1.80.D0.B0.D0.BD_.D1.81_.D0.BF.D0.BE.D0.BB.D0.BD.D1.8B.D0.BC_.D0.B7.D0.B0.D0.B2.D0.B8.D1.81.D0.B0.D0.BD.D0.B8.D0.B5.D0.BC_.D0.B8.2F.D0.B8.D0.BB.D0.B8_.D0.BF.D1.80.D0.B8.D1.82.D0.BE.D1.80.D0.BC.D0.B0.D0.B6.D0.B8.D0.B2.D0.B0.D0.BD.D0.B8.D1.8F_.D0.BF.D0.BE.D1.81.D0.BB.D0.B5_.D0.BF.D0.B5.D1.80.D0.B5.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B8_.D0.B8.D0.BB.D0.B8_startx)
        *   [6.7.1 Неисправные вызовы ACPI](#.D0.9D.D0.B5.D0.B8.D1.81.D0.BF.D1.80.D0.B0.D0.B2.D0.BD.D1.8B.D0.B5_.D0.B2.D1.8B.D0.B7.D0.BE.D0.B2.D1.8B_ACPI)
        *   [6.7.2 Неподдерживаемые версии ядра Linux](#.D0.9D.D0.B5.D0.BF.D0.BE.D0.B4.D0.B4.D0.B5.D1.80.D0.B6.D0.B8.D0.B2.D0.B0.D0.B5.D0.BC.D1.8B.D0.B5_.D0.B2.D0.B5.D1.80.D1.81.D0.B8.D0.B8_.D1.8F.D0.B4.D1.80.D0.B0_Linux)
    *   [6.8 KDM исчезает после выхода из системы](#KDM_.D0.B8.D1.81.D1.87.D0.B5.D0.B7.D0.B0.D0.B5.D1.82_.D0.BF.D0.BE.D1.81.D0.BB.D0.B5_.D0.B2.D1.8B.D1.85.D0.BE.D0.B4.D0.B0_.D0.B8.D0.B7_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.8B)
    *   [6.9 Не работает Direct Rendering](#.D0.9D.D0.B5_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.B0.D0.B5.D1.82_Direct_Rendering)
    *   [6.10 Проблемы с гибернацией/сном](#.D0.9F.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D1.8B_.D1.81_.D0.B3.D0.B8.D0.B1.D0.B5.D1.80.D0.BD.D0.B0.D1.86.D0.B8.D0.B5.D0.B9.2F.D1.81.D0.BD.D0.BE.D0.BC)
        *   [6.10.1 Видео не возобновляется из suspend2ram](#.D0.92.D0.B8.D0.B4.D0.B5.D0.BE_.D0.BD.D0.B5_.D0.B2.D0.BE.D0.B7.D0.BE.D0.B1.D0.BD.D0.BE.D0.B2.D0.BB.D1.8F.D0.B5.D1.82.D1.81.D1.8F_.D0.B8.D0.B7_suspend2ram)
    *   [6.11 Система Притормаживает/Сильно зависает](#.D0.A1.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D0.B0_.D0.9F.D1.80.D0.B8.D1.82.D0.BE.D1.80.D0.BC.D0.B0.D0.B6.D0.B8.D0.B2.D0.B0.D0.B5.D1.82.2F.D0.A1.D0.B8.D0.BB.D1.8C.D0.BD.D0.BE_.D0.B7.D0.B0.D0.B2.D0.B8.D1.81.D0.B0.D0.B5.D1.82)
    *   [6.12 Конфликты оборудования](#.D0.9A.D0.BE.D0.BD.D1.84.D0.BB.D0.B8.D0.BA.D1.82.D1.8B_.D0.BE.D0.B1.D0.BE.D1.80.D1.83.D0.B4.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D1.8F)
    *   [6.13 Временные зависания при воспроизведении видео](#.D0.92.D1.80.D0.B5.D0.BC.D0.B5.D0.BD.D0.BD.D1.8B.D0.B5_.D0.B7.D0.B0.D0.B2.D0.B8.D1.81.D0.B0.D0.BD.D0.B8.D1.8F_.D0.BF.D1.80.D0.B8_.D0.B2.D0.BE.D1.81.D0.BF.D1.80.D0.BE.D0.B8.D0.B7.D0.B2.D0.B5.D0.B4.D0.B5.D0.BD.D0.B8.D0.B8_.D0.B2.D0.B8.D0.B4.D0.B5.D0.BE)
    *   [6.14 "aticonfig: No supported adapters detected"](#.22aticonfig:_No_supported_adapters_detected.22)
    *   [6.15 Поддержка WebGL в chromium](#.D0.9F.D0.BE.D0.B4.D0.B4.D0.B5.D1.80.D0.B6.D0.BA.D0.B0_WebGL_.D0.B2_chromium)
    *   [6.16 Задержки/подтормаживания просматривая flash видео через Adobe's flashplugin](#.D0.97.D0.B0.D0.B4.D0.B5.D1.80.D0.B6.D0.BA.D0.B8.2F.D0.BF.D0.BE.D0.B4.D1.82.D0.BE.D1.80.D0.BC.D0.B0.D0.B6.D0.B8.D0.B2.D0.B0.D0.BD.D0.B8.D1.8F_.D0.BF.D1.80.D0.BE.D1.81.D0.BC.D0.B0.D1.82.D1.80.D0.B8.D0.B2.D0.B0.D1.8F_flash_.D0.B2.D0.B8.D0.B4.D0.B5.D0.BE_.D1.87.D0.B5.D1.80.D0.B5.D0.B7_Adobe.27s_flashplugin)
    *   [6.17 Задержки/медленные перемещения окон в GNOME3](#.D0.97.D0.B0.D0.B4.D0.B5.D1.80.D0.B6.D0.BA.D0.B8.2F.D0.BC.D0.B5.D0.B4.D0.BB.D0.B5.D0.BD.D0.BD.D1.8B.D0.B5_.D0.BF.D0.B5.D1.80.D0.B5.D0.BC.D0.B5.D1.89.D0.B5.D0.BD.D0.B8.D1.8F_.D0.BE.D0.BA.D0.BE.D0.BD_.D0.B2_GNOME3)
    *   [6.18 Not using full screen resolution at 1920x1080 (underscanning, black borders around the screen)](#Not_using_full_screen_resolution_at_1920x1080_.28underscanning.2C_black_borders_around_the_screen.29)
    *   [6.19 Dual Screen Setup: general problems with acceleration, OpenGL, compositing, performance](#Dual_Screen_Setup:_general_problems_with_acceleration.2C_OpenGL.2C_compositing.2C_performance)
    *   [6.20 Disabling VariBright feature](#Disabling_VariBright_feature)
    *   [6.21 Hybrid/PowerXpress: turning off discrete GPU](#Hybrid.2FPowerXpress:_turning_off_discrete_GPU)
    *   [6.22 Switching from X session to TTYs gives a blank screen/low resolution TTY](#Switching_from_X_session_to_TTYs_gives_a_blank_screen.2Flow_resolution_TTY)
    *   [6.23 Switching from X session to TTYs gives a black screen with the monitor backlight on](#Switching_from_X_session_to_TTYs_gives_a_black_screen_with_the_monitor_backlight_on)
    *   [6.24 Switching to TTYs then back to X session gives a black screen with a mouse cursor](#Switching_to_TTYs_then_back_to_X_session_gives_a_black_screen_with_a_mouse_cursor)
    *   [6.25 30 FPS / Tear-Free / V-Sync bug](#30_FPS_.2F_Tear-Free_.2F_V-Sync_bug)
    *   [6.26 Backlight adjustment does not work](#Backlight_adjustment_does_not_work)
*   [7 See also](#See_also)

## Установка

Существует три способа установки Catalyst. Первый - использование репозитория [Vi0L0](https://aur.archlinux.org/account/Vi0l0/) (неофицального мейнтейнера Catalyst в Arch). Этот репозиторий содержит все необходимые пакеты. Второй - использование AUR; PKGBUILD'ы, которые сделал Vi0L0 идентичны тем, которые используются в его репозитории. Третий - скачивание драйвера с сайта AMD.

Прежде чем выбрать понравившийся способ, нужно узнать какой драйвер вам нужен. Начиная с Catalyst 12.4, AMD отделила разработку драйвера для видеокарт Radeon HD 2xxx, 3xxx и 4xxx версий в отдельный драйвер, который называется Catalyst **legacy**. Для видеокарт Radeon HD 5xxx и новее, подойдет обычный драйвер Catalyst. В независимости от выбранного драйвера, вам нужно установить утилиты Catalyst.

**Примечание:** После установки драйвера выбранным способом, вы найдете общие указания, которые должен выполнить **каждый**, в независимости от выбранного способа.

### Установка драйвера

#### Установка из неофициального репозитория

Если вам не по душе собирать пакеты из [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)"), то этот способ для вас. Репозиторий сопровождается неофициальным мейнтейнером Catalyst, [Vi0l0](/index.php/User:Vi0L0 "User:Vi0L0"). Все пакеты подписаны и считаются безопасными для использования. Как вы позже увидите в этой статье, Vi0L0 ответственен за многие другие пакеты, которые помогают вашей системе работать с видеокартой ATI.

У Vi0L0 есть три репозитория Catalyst, каждый из которых содержит уникальный драйвер:

*   [catalyst](/index.php/Unofficial_user_repositories#catalyst "Unofficial user repositories") - репозиторий с последними (стабильными и бета) выпусками Catalyst для видеокарт Radeon HD 5xxx и выше.
*   *catalyst-stable* - репозиторий со стабильными выпусками Catalyst для видеокарт Radeon HD 5xxx и выше.
*   [catalyst-hd234k](/index.php/Unofficial_user_repositories#catalyst-hd234k "Unofficial user repositories") - репозиторий с драйвером Catalyst legacy для видеокарт Radeon HD 2xxx, 3xxx и 4xxx.

Чтобы добавить один из репозиториев следуйте инструкциям в этой [статье](/index.php/Unofficial_user_repositories "Unofficial user repositories"). Добавьте выбранный репозиторий **выше всех других репозиториев** в `pacman.conf`.

**Примечание:** Репозитории *catalyst* и *catalyst-stable* предоставляют один и тот же URL. Чтобы включить *catalyst-stable*, следуйте тем же инструкциям, что и для *catalyst*, но замените `[catalyst]` на `[catalyst-stable]` в `pacman.conf`. Если вам нужно придерживаться старой версии, есть несколько репозиториев, которые используют один и тот же URL (например, *catalyst-stable-13.4*).

**Важно:**

*   Драйвер Catalyst legacy не поддерживает Xorg 1.17\. Если вы хотите использовать этот драйвер, смотрите [#Репозитории Xorg](#.D0.A0.D0.B5.D0.BF.D0.BE.D0.B7.D0.B8.D1.82.D0.BE.D1.80.D0.B8.D0.B8_Xorg) для получения инструкций о том, как сделать откат Xorg на версию 1.16.

**Совет:** Так как catalyst.wirephire.com будет выключаться при превышении определенного предела пропускной способности (это случалось в прошлом) или может быть слишком медленным для вашего местоположения, зеркало для этого репозитория сделал rtsinformatique и оно находится по ссылке [[1]](http://mirror.rts-informatique.fr/archlinux-catalyst/) (Франция), так же другое зеркало [[2]](http://mirror.hactar.bz/Vi0L0/) (Германия). Эти зеркала предоставляются без гарантий. Раскомментируйте строку с зеркалом, которое ближе всего к вам. Хорошая идея - держать альтернативу в случае отказа одного зеркала.

Использование зеркала для репозитория можно легко добиться с помощью `rsync://mirror.rts-informatique.fr::archlinux-catalyst`.

После добавления репозитория Catalyst, обновите базу данных pacman и [установите](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pacman (Русский)") эти пакеты (смотрите [#Инструменты](#.D0.98.D0.BD.D1.81.D1.82.D1.80.D1.83.D0.BC.D0.B5.D0.BD.D1.82.D1.8B) для большей информации):

*   *catalyst-hook*
*   *catalyst-utils*
*   *catalyst-libgl*
*   *opencl-catalyst* - необязательный, нужен для поддержки OpenCL
*   *lib32-catalyst-utils* - необязательный, нужен для поддержки 32-битного OpenGL на 64-битных системах
*   *lib32-catalyst-libgl* - необязательный, нужен для поддержки 32-битного OpenGL на 64-битных системах
*   *lib32-opencl-catalyst* - необязательный, нужен для поддержки 32-битного OpenCL на 64-битных системах

Если вы используете ноутбук с гибридной графикой Intel/AMD, набор пакетов будет немного отличаться:

*   *catalyst-hook*
*   *catalyst-utils-pxp*
*   *lib32-catalyst-utils-pxp* - необязательный, нужен для поддержки 32-битного OpenGL на 64-битных системах

**Примечание:** Если pacman спросит вас про удаление **libgl**, вы можете смело соглашаться.

**Важно:** Пакет catalyst был удален из репозитория Vi0L0, его место занял catalyst-hook.

#### Установка из AUR

Второй способ заключается в установке Catalyst из [AUR](/index.php/Arch_User_Repository "Arch User Repository"). Если вы хотите собрать пакеты конкретно для вашего компьютера, то этот способ для вас. Обратите внимание, что это также и самый утомительный способ установки Catalyst; он требует больше всего работы, а также требует обновления вручную при каждом обновлении ядра.

**Важно:** Если вы установили пакет Catalyst из AUR, вам нужно будет пересобирать Catalyst после каждого обновления ядра. Иначе, X сервер **не** запустится.

Все пакеты, которые сопровождает Vi0L0 в неофициальном репозитории доступны в [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)"):

*   [catalyst](https://aur.archlinux.org/packages/catalyst/)
*   [catalyst-generator](https://aur.archlinux.org/packages/catalyst-generator/)
*   [catalyst-hook](https://aur.archlinux.org/packages/catalyst-hook/)
*   [catalyst-utils](https://aur.archlinux.org/packages/catalyst-utils/)
*   [lib32-catalyst-utils](https://aur.archlinux.org/packages/lib32-catalyst-utils/)

Также, AUR содержит пакеты, которых **нет** в других репозиториях. Эти пакеты содержат так называемые *Catalyst-total* пакеты и бета версии:

*   [catalyst-total](https://aur.archlinux.org/packages/catalyst-total/)
*   [catalyst-total-pxp](https://aur.archlinux.org/packages/catalyst-total-pxp/)
*   [catalyst-total-hd234k](https://aur.archlinux.org/packages/catalyst-total-hd234k/)
*   [catalyst-test](https://aur.archlinux.org/packages/catalyst-test/)

Пакеты [catalyst-total](https://aur.archlinux.org/packages/catalyst-total/) создаются чтобы облегчить жизнь пользователям AUR. Они обеспечивают построение драйвера, утилит и 32-битных утилит. Также они собирают пакет [catalyst-hook](https://aur.archlinux.org/packages/catalyst-hook/), который описан в разделе [#Инструменты](#.D0.98.D0.BD.D1.81.D1.82.D1.80.D1.83.D0.BC.D0.B5.D0.BD.D1.82.D1.8B).

[catalyst-total-pxp](https://aur.archlinux.org/packages/catalyst-total-pxp/) собирает Catalyst с экспериментальной поддержкой powerXpress.

### Конфигурация драйвера

После того, как вы установили драйвер выбранным способом, вам нужно настроить X для работы с Catalyst. Также, вам придется убедиться, что модуль загружается при запуске. И еще, вы должны выключить [kernel mode setting](/index.php/KMS "KMS").

#### Конфигурация X

Чтобы настроить X, вам нужно создать файл `xorg.conf`. Catalyst предоставляет свой собственный инструмент `aticonfig` для создания и/или изменения этого файла.

Он также может настроить практически каждый аспект видеокарты, он также получает доступ к файлу `/etc/ati/amdpcsdb`. Для получения полного списка параметров `aticonfig`, запустите:

```
# aticonfig --help | less

```

**Важно:** Используйте параметр `--output` прежде чем совершать изменения в `/etc/X11/`, также как и в файле `xorg.conf`, инструмент перезапишет все в `/etc/X11/xorg.conf.d/`

**Примечание:** Чтобы использовать новое местоположение файла конфигурации используйте `# aticonfig [...] --output`, чтобы адаптировать раздел `Device` в `/etc/X11/xorg.conf.d/20-radeon.conf`. Недостатком является то, что многие опции `aticonfig` зависят от `xorg.conf` и будут недоступны.

Теперь, настроим Catalyst. Если у вас только один монитор, запустите:

```
# aticonfig --initial

```

**Примечание:** Если у вас проблемы с PowerXpress, вам, вероятно, нужно установить [catalyst-total-pxp](https://aur.archlinux.org/packages/catalyst-total-pxp/).

Если у вас два монитора и вы хотите использовать их оба, вы можете запустить команду ниже. Обратите внимание на то, что инструмент сгенерирует файл конфигурации, где второй экран выше первого экрана.

```
# aticonfig --initial=dual-head --screen-layout=above

```

**Примечание:** Смотрите [#Два экрана (Dual Head / Dual Screen / Xinerama)](#.D0.94.D0.B2.D0.B0_.D1.8D.D0.BA.D1.80.D0.B0.D0.BD.D0.B0_.28Dual_Head_.2F_Dual_Screen_.2F_Xinerama.29) для получения дополнительной информации по настройке двух экранов.

Вы можете сравнить сгенерированный файл с [примером xorg.conf](/index.php/Xorg_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.80.D1.8B_.D1.84.D0.B0.D0.B9.D0.BB.D0.BE.D0.B2_xorg.conf "Xorg (Русский)").

Хотя текущие версии Xorg автоматически обнаруживают большинство параметров при запуске, вы можете указать некоторые параметры по умолчанию в случае изменения между версиями.

Вот пример (с заметками) *'для справки'* . Записи с `#` должны присутствовать в файле, записи с `##` добавляйте по необходимости:

 `/etc/X11/xorg.conf` 
```
Section "ServerLayout"
        Identifier     "Arch"
        Screen      0  "Screen0" 0 0          # 0 обязателен.
EndSection
Section "Module"
        Load [...]
        [...]
EndSection
Section "Monitor"
        Identifier   "Monitor0"
        [...]
EndSection
Section "Device"
        Identifier  "Card0"
        Driver      "fglrx"                         # Необходимо.
        BusID       "PCI:1:0:0"                     # Рекомендуется, если не получается автоопределить.
        Option      "OpenGLOverlay" "0"             ##
        Option      "XAANoOffscreenPixmaps" "false" ##
EndSection
Section "Screen"
        Identifier "Screen0"
        Device     "Card0"
        Monitor    "Monitor0"
        DefaultDepth    24
        SubSection "Display"
                Viewport   0 0
                Depth     24                        # Не должно быть отличным от '24'
                Modes "1280x1024" "2048x1536"       ## Первое значение=разрешение по умолчанию, второе=максимальное.
                Virtual 1664 1200                   ## (x+64, y) для обхода прямоугольников OGL. артефакты/
        EndSubSection                               ## исправлено в Catalyst 9.8
EndSection
Section "DRI"
        Mode 0666                                   # Может помочь включить direct rendering.
EndSection
```

**Примечание:** C **каждым** обновлением Catalyst этим способом вы должны удалять файл `amdpcsdb`: убейте X, удалите `/etc/ati/amdpcsdb`, запустите X и запустите`amdcccle` - иначе, версия Catalyst может не правильно отображаться в`amdcccle`.

*Если вам нужна дополнительная информация о Catalyst, посетите [эту тему](https://bbs.archlinux.org/viewtopic.php?id=57084).*

#### Загрузка модуля при загрузе

Мы должны запретить загрузку модуля `radeon`. Для этого, добавьте *radeon* в `/etc/modprobe.d/modprobe.conf`. Также, убедитесь, что он не загружается каким - либо файлом в `/etc/modules-load.d/`. Для большей информации, смотрите [kernel modules#Запрет загрузки](/index.php/Kernel_modules_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.97.D0.B0.D0.BF.D1.80.D0.B5.D1.82_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B8 "Kernel modules (Русский)").

Далее, мы должны убедиться, что модуль `fglrx` автоматически загружается. Также добавьте `fglrx` в существующий файл модуля в `/etc/modules-load.d/` или создайте новый файл и добавьте туда `fglrx`.

#### Отключение kernel mode setting

**Примечание:** Не отключайте kernel mode setting если вы используете `catalyst-utils-pxp` или `catalyst-total-pxp`, так как драйвер intel использует это.

Важно отключить kernel mode setting, так как драйвер не использует преимущества [KMS](/index.php/KMS "KMS"). Если вы не отключите KMS, ваша система может зависнуть при попытке переключиться в TTY или даже при выключении через среду рабочего стола.

Чтобы выключить kernel mode setting, добавьте `nomodeset` в [параметры ядра](/index.php/Kernel_parameters_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Kernel parameters (Русский)").

#### Проверка работоспособности

Предполагая, что перезагрузка и вход в систему прошли успешно, вы можете проверить, что fglrx работает правильно:

```
$ lsmod | grep fglrx
$ fglrxinfo

```

Если вы получаете сообщения, он работает. Наконец, запустим X при помощи `startx` или используя GDM/KDM и проверим, что direct rendering включен:

```
$ glxinfo | grep "direct rendering"

```

Если ответ `"direct rendering: yes"`, то это хорошо! Если команда `$ glxinfo` не найдена, установите пакет [mesa-demos](https://www.archlinux.org/packages/?name=mesa-demos).

**Примечание:** Вы также можете использовать:
```
$ fgl_glxgears

```

как альтернативу `glxgears`.

**Важно:** В последних версиях Xorg, пути к библиотекам поменялись. Поэтому, иногда `libGL.so` не может быть правильно загружена, даже если она установлена. Проверьте это, если GL не работает. Читайте подробности в разделе [#Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC).

### Пользовательские ядра

**Примечание:** Если вам неудобно или вы не умеете собирать пакеты, прочитайте статью [ABS](/index.php/Arch_Build_System_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch Build System (Русский)").

Чтобы установить catalyst с пользовательским ядром, вам нужно собрать свой собственный пакет `catalyst-$kernel`:

1.  Возьмите файлы `PKGBUILD` и `catalyst.install` из [Catalyst](/index.php/AUR "AUR").
2.  Отредактируйте PKGBUILD. Нужно сделать два изменения:
    1.  Измените `pkgname=catalyst` на `pkgname=catalyst-$название_ядра`, где `$название_ядра` это то, что вы хотите (например, пользовательское, мм, самоекрутоеядро).
    2.  Измените зависимости `linux` на `$название_ядра`.
3.  Соберите и установите этот пакет; запустите `makepkg -i` или `makepkg`, затем `# pacman -U имяпакета.pkg.tar.gz`

**Примечание:**

*   Если вы запускаете несколько ядер, вам нужно установить пакет [catalyst-utils](https://aur.archlinux.org/packages/catalyst-utils/) для всех ядер. Они не конфликтуют друг с другом.
*   Утилита [catalyst-generator](https://aur.archlinux.org/packages/catalyst-generator/) в состоянии собрать пакеты `catalyst-{версия_ядра}` для вас и вам ненужно проделывать все самостоятельно. Для большей информации, смотрите [раздел инструменты](#.D0.98.D0.BD.D1.81.D1.82.D1.80.D1.83.D0.BC.D0.B5.D0.BD.D1.82.D1.8B).

### Поддержка PowerXpress

Технология PowerXpress позволяет ноутбуку с двумя видеокартами переключаться из интегрированной графики (ИГП) на дискретную и обратно, для того чтобы достигнуть долгой автономной работы или более лучшей 3D визуализации.

Чтобы использовать эту технологию в Arch, вам придется:

*   Скачать и собрать пакет [catalyst-total](https://aur.archlinux.org/packages/catalyst-total/) / [catalyst-test](https://aur.archlinux.org/packages/catalyst-test/) из [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)") или
*   Установить пакеты **catalyst-libgl** и **catalyst-utils** из репозитория [catalyst] (если требуется, установите lib32-catalyst-utils-pxp).

Чтобы переключиться на ИГП Intel, вам нужно установить пакет [mesa](https://www.archlinux.org/packages/?name=mesa) и драйвер Intel: [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel).

**Примечание:** Иногда у catalyst появляются проблемы с новейшими драйверами intel. Если это происходит, понизьте версию пакета [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) на предыдущую версию найденную в [архиве Arch Linux](/index.php/Arch_Linux_Archive "Arch Linux Archive") или даже в архиве [репозиториев Xorg](#.D0.A0.D0.B5.D0.BF.D0.BE.D0.B7.D0.B8.D1.82.D0.BE.D1.80.D0.B8.D0.B8_Xorg) вместе с пакетом (пакетами) xorg-server.

Вы можете переключаться между встроенным графическим процессором и дискретным, используя следующие команды:

```
# aticonfig --px-igpu    #для встроенного графического процессора
# aticonfig --px-dgpu    #для дискретного графического процессора
```

Просто запомните, что fglrx требует сконфигурированный `/etc/X11/xorg.conf` для видеокарты AMD c fglrx.

Вы можете использовать скрипт `pxp_switch_catalyst`, который позволит выполнять некоторые полезные операции:

*   Переключение - переименовывает `xorg.conf` в `xorg.conf.cat` (если fglrx внутри) или `xorg.conf.oth` (если intel внутри) и тогда создает символическую ссылку на `xorg.conf`, в зависимости от вашего выбора.
*   Запуск `aticonfig --px-Xgpu`.
*   Запуск `switchlibGL`.
*   Добавление/удаление `fglrx` в/из `/etc/modules-load.d/catalyst.conf`.

Использование:

```
# pxp_switch_catalyst amd
# pxp_switch_catalyst intel
```

Если у вас проблемы при запуске X на драйвере Intel, вы можете попробовать принудительно использовать ускорение "UXA". Просто убедитесь, что у вас есть строка `Option "AccelMethod" "uxa"` в `xorg.conf`:

 `/etc/X11/xorg.conf` 
```
Section "Device"
        Identifier  "Intel Graphics"
        Driver      "intel"
        #Option      "AccelMethod"  "sna"
        **Option      "AccelMethod"  "uxa"**
        #Option      "AccelMethod"  "xaa"
EndSection
```

#### Запуск двух X серверов (один использующий драйвер Intel, другой fglrx) одновременно

Так как fglrx склонен к падениям (относительно PowerXpress), это может быть хорошей идеей, использовать драйвер Intel на основном сервере X, а fglrx на дополнительном, когда понадобится 3D-ускорение. Однако, простое переключение на дискретный графический процессор с встроенного графического процессора используя `aticonfig` или `amdcccle` вызовет ошибки разного рода при запуске второго X.

Чтобы запустить два X сервера в одно время (каждый с разным драйвером), вы должны настроить полностью рабочий X с Catalyst и затем переместить {[ic|xorg.conf}} во временное место (например, `/etc/X11/xorg.conf.fglrx`). В следующий раз, когда X запустится, он будет по умолчанию использовать драйвер Intel вместо fglrx.

Чтобы запустить второй X сервер использующий fglrx, просто переместите `xorg.conf` назад в правильное место (`/etc/X11/xorg.conf`) перед запуском X. Этот метод позволяет вам переключаться между запущенными сессиями X. Когда вы закончили использовать fglrx, снова переместите `xorg.conf` в другое место.

Единственный недостаток этого метода в том, что у вас не будет 3D-ускорения используя драйвер Intel. 2D-ускорение полностью функционирует. Кроме того, это обеспечит нас полностью стабильным рабочим столом.

#### Проблемы с PowerXpress на ноутбуке запущенный в режиме AMD (pxp_switch_catalyst amd) с внешним / вторым монитором

Используя PowerXpress на ноутбуке в режиме AMD-только (т.е., дискретная видеокарта все визуализирует), иногда, вы можете столкнуться с артефактами/дублированием между дисплеями. Это известная проблема, и, кажется, она характера для видеокарт 7xxxM серии.

Артефакты исчезнут когда вы преобразуете один из мониторов при помощи поворота или масштабирования. Вы можете использовать xrand:

 `xrandr --output HDMI1 --left-of LVDS1 --primary --scale 1x1 --output LVDS1 --scale 1.0001x1.0001` 

## Репозитории Xorg

Catalyst славится своим медленным обновлением. Поэтому новые версии Xorg несовместимы с Catalyst. Это значит, что вам нужно собрать свои пакеты Xorg или использовать репозиторий. Vi0L0 занялся этой задачей и сделал несколько репозиториев.

Чтобы включить один из репозиториев, следуйте инструкциям в [Unofficial user repositories](/index.php/Unofficial_user_repositories "Unofficial user repositories") (используйте тот же PGP ключ для репозитория [catalyst](/index.php/Unofficial_user_repositories#catalyst "Unofficial user repositories")). Не забудьте добавит выбранный репозиторий **выше других репозиториев** в `pacman.conf`, даже выше репозитория *catalyst*.

### xorg117

Catalyst не поддерживает xorg-server 1.18

```
[xorg117]
Server = http://catalyst.wirephire.com/repo/xorg117/$arch
## Зеркала, если основной сервер не работает или работает, но слишком медленно:
#Server = http://mirror.rts-informatique.fr/archlinux-catalyst/repo/xorg117/$arch
#Server = http://mirror.hactar.bz/Vi0L0/xorg117/$arch

```

### xorg116

Catalyst < 15.7 не поддерживает xorg-server 1.17

```
[xorg116]
Server = http://catalyst.wirephire.com/repo/xorg116/$arch
## Зеркала, если основной сервер не работает или работает, но слишком медленно:
#Server = http://mirror.rts-informatique.fr/archlinux-catalyst/repo/xorg116/$arch
#Server = http://mirror.hactar.bz/Vi0L0/xorg116/$arch

```

### xorg115

Catalyst < 14.9 не поддерживает xorg-server 1.16

```
[xorg115]
Server = http://catalyst.wirephire.com/repo/xorg115/$arch
## Зеркала, если основной сервер не работает или работает, но слишком медленно:
#Server = http://mirror.rts-informatique.fr/archlinux-catalyst/repo/xorg115/$arch
#Server = http://mirror.hactar.bz/Vi0L0/xorg115/$arch

```

### xorg114

Catalyst < 14.1 doesn't support xorg-server 1.15.

```
[xorg114]
Server = http://catalyst.wirephire.com/repo/xorg114/$arch
## Mirrors, if the primary server does not work or is too slow:
#Server = http://mirror.rts-informatique.fr/archlinux-catalyst/repo/xorg114/$arch
#Server = http://mirror.hactar.bz/Vi0L0/xorg114/$arch

```

### xorg113

Catalyst < 13.6 не поддерживает xorg-server 1.14.

```
[xorg113]
Server = http://catalyst.wirephire.com/repo/xorg113/$arch
## Зеркала, если основной сервер не работает или работает, но слишком медленно:
#Server = http://mirror.rts-informatique.fr/archlinux-catalyst/repo/xorg113/$arch
#Server = http://mirror.hactar.bz/Vi0L0/xorg113/$arch

```

### xorg112

Catalyst < 12.10 и Catalyst Legacy не поддерживают xorg-server 1.13.

```
[xorg112]
Server = http://catalyst.wirephire.com/repo/xorg112/$arch
## Зеркала, если основной сервер не работает или работает, но слишком медленно:
#Server = http://mirror.rts-informatique.fr/archlinux-catalyst/repo/xorg112/$arch
#Server = http://mirror.hactar.bz/Vi0L0/xorg112/$arch

```

## Инструменты

### Catalyst-hook

[Catalyst-hook](https://aur.archlinux.org/packages/Catalyst-hook/) - это сервис [systemd](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd (Русский)"), который автоматически собирает модуль `fglrx` пока система выключается или перезагружается, но только когда это нужно (например, после обновления).

Перед использованием убедитесь, что группа [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) и пакет [linux-headers](https://www.archlinux.org/packages/?name=linux-headers) установлены.

Чтобы включить автоматическое обновление, включите `catalyst-hook.service`:

```
# systemctl enable catalyst-hook
# systemctl start catalyst-hook

```

Также, вы можете использовать этот пакет чтобы собственноручно собирать модуль `fglrx`. Просто запустите скрипт `catalyst_build_module` после обновления ядра:

```
# catalyst_build_module all

```

**Несколько технических деталей:**

`catalyst-hook.service` останавливает "поток" systemd и заставляет systemd ждать пока catalyst-hook завершит свою работу.

`catalyst-hook.service` вызывает функцию `catalyst_build_module check`, которая проверяет, что пересборка fglrx действительно нужна.

Функция `check` проверяет, что модуль `fglrx` существует, если он:

*   не существует, то он будет собран;

*   существует, он будет сравнен с двумя значениями, чтобы удостовериться, что пересборка модуля действительно нужна.

Этими значениями являются md5sum файла `/usr/lib/modules/<kernel_version>/build/Module.symvers` (потому что я, Vi0L0, заметил, что этот файл уникален и отличается для каждой версии ядра). Первое значение - это md5sum существующего файла `Module.symvers`. Второе значение - это md5sum файла `Module.symvers`, который существует на момент сборки модуля `fglrx`. Это значение было встроено при компиляции в модуль `fglrx` скриптом `catalyst_build_module`.

Если значения отличаются, то будет скомпилирован новый модуль `fglrx`.

Функция проверки проверяет всю директорию `/usr/lib/modules` и собирает модули для всех установленных ядер если это нужно. Если сборка или пересборка не нужна, то процесс длится всего несколько миллисекунд перед тем как он будет завершен systemd.

### Catalyst-generator

[catalyst-generator](https://aur.archlinux.org/packages/catalyst-generator/) - это пакет, который в состоянии собрать и установить модуль `fglrx` запакованный в совместимый с pacman пакет `catalyst-${kernver}`. Основное отличие от [#Catalyst-hook](#Catalyst-hook), это то, что вам не нужно запускать скрипты собственноручно, Catalyst-hook будет делать это все автоматически при загрузке когда новое ядро установлено.

Он создает пакет `catalyst-${kernver}` используя [makepkg](/index.php/Makepkg_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Makepkg (Русский)") и устанавливает их с помощью [pacman](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pacman (Русский)"). `${kernver}` - это версия ядра для которой собирается пакет (например, пакет catalyst-2.6.35-ARCH который будет собран для ядра 2.6.35-ARCH).

Чтобы собрать и установить пакет `catalyst-${kernver}` для текущего ядра как пользователь без привилегий (пользователь не являющийся root; безопаснейший путь), используйте `catalyst_build_module`. Вас спросят пароль root для продолжения установки пакета.

Небольшой обзор об использовании этого пакета:

1.  Как root: `catalyst_build_module remove`. Эта команда удалит неиспользуемые пакеты `catalyst-{kernver}`.
2.  Как пользователь без привилегий: `catalyst_build_module ${kernver}`, где `${kernver}` это версия ядра, которую только что обновили. Например: `catalyst_build_module 2.6.36-ARCH`. Вы также можете собрать `catalyst-{kernver}` для всех установленных ядер используя `catalyst_build_module all`.
3.  Если вы хотите удалить `catalyst-generator`, лучше всего запустить эту команду как root перед удалением catalyst-generator: `catalyst_build_module remove_all`. **Эта команда удалит все пакеты `catalyst-{kernver}` из системы.**

`Catalyst-generator` не в состоянии удалить все пакеты `catalyst-{kernver}` автоматически, потому что pacman может быть запущен только в одном экземпляре. Если вы забыли запустить `# catalyst_build_module remove_all` перед использованием `# pacman -R catalyst-generator`, catalyst-generator сообщит вам о том, какие пакеты `catalyst-{kernver}` вы должны удалить вручную после удаления его самого.

Catalyst-generator - это самое безопасное и просто решение потому что:

1.  вы можете использовать пользователя без привилегий чтобы собрать этот пакет;
2.  он собирает модули в среде fakeroot;
3.  он не бросает файлы туда-сюда, [pacman](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pacman (Русский)") всегда знает где они есть;
4.  все что вам нужно запомнить, это не забыть использовать catalyst-generator

**Примечание:** Если вы видите эти предупреждения:
```
**WARNING:** Package contains reference to $srcdir

```

```
**WARNING:** '.pkg' is not a valid archive extension.

```
во время сборки пакета `catalyst-{kernver}`, не беспокойтесь, это нормально.

### Разработка OpenCL и OpenGL

Уже много лет AMD работает над инструментами для разработки на OpenCL и OpenGL.

В настоящее время под заголовком **"Heterogeneous Computing"** AMD обеспечивает еще больше, к счастью, большинство из вычислительных инструментов доступны также и для Linux.

В AUR и репозиториях [catalyst] вы найдете пакеты, которые представляют наиболее важную работу AMD, а именно:

*   [amdapp-aparapi](https://aur.archlinux.org/packages/amdapp-aparapi/)
*   [amdapp-sdk](https://aur.archlinux.org/packages/amdapp-sdk/)
*   [amdapp-codexl](https://aur.archlinux.org/packages/amdapp-codexl/)

Ярлык APP выступает за Ускорение Параллельной Обработки.

#### amdapp-aparapi

AMD Aparapi - это API языка программирования Java для написания и выполнения OpenCL - ядер на графических акселераторах компании AMD. Если целевая платформа поддерживает OpenCL, то байткод будет проанализирован "на лету" и в случае отсутствия неконвертируемого в OpenCL кода, он транслируется в OpenCL, компилируется и запускается на GPU (если подходящий GPU присутствует). В противном случае, код будет запущен как обычный байткод на CPU.

Больше информации о Aparapi вы найдете [здесь](http://developer.amd.com/tools/heterogeneous-computing/aparapi/)

#### amdapp-sdk (ранее известный как amdstream)

Коплект Средств Разработки (КСР) AMD APP - это полная платформа разработки от AMD, которая позволяет быстро и легко разрабатывать приложения, аппаратно ускоренные с помощью технологии AMD APP. КСР предоставляет примеры, документацию и другие материалы, которые помогают быстрее начать разрабатывать приложения использующие OpenCL, Bolt или C++ AMP в вашем приложении C/C++.

Начиная с версии 2.8 amdapp-sdk предоставляет aparapiUtil, а также примеры aparapi. Пакет доступен в репозитории [catalyst]; он зависит от пакета [amdapp-aparapi](https://aur.archlinux.org/packages/amdapp-aparapi/). Пакет из AUR позволяет вам решать, хотите ли вы дополнения к aparapi или нет.

Версия 2.8 не предоставляет функциональность Профайлера, он был перемещен в CodeXL.

Больше информации о AMD APP SDK [здесь](http://developer.amd.com/tools/heterogeneous-computing/amd-accelerated-parallel-processing-app-sdk/).

#### amdapp-codexl

CodeXL - это Отладчик и Профилировщик для OpenCL и OpenGL со статическим анализом ядра OpenCL. Это приложение с графическим интерфейсом написано поверх известного [gdebugger](https://aur.archlinux.org/packages/gdebugger/) и доступно только для систем x86_64.

Больше информации о CodeXL вы найдете [здесь](http://developer.amd.com/tools/heterogeneous-computing/codexl/).

## Преимущества

### Tear Free Rendering

Технология, представленная в **Catalyst 11.1**, называемая *Tear Free Desktop*, которая уменьшает разрывы между изображениями на экране, в 2D, 3D и видео приложениях. Скорее всего, она добавляет тройную буферизацию и вертикальную синхронизацию. Обратите внимание, включение данной технологии создает дополнительную нагрузку на видеокарту.

Чтобы включить 'Tear Free Desktop' запустите `amdcccle` и перейдите в: `Display Options` → `Tear Free`.

Или выполните:

```
# aticonfig --set-pcs-u32=DDX,EnableTearFreeDesktop,1

```

Чтобы выключить, используйте `amdcccle` или выполните:

```
# aticonfig --del-pcs-key=DDX,EnableTearFreeDesktop

```

### Аппаратное ускорение

**[Video Acceleration API](https://en.wikipedia.org/wiki/Video_Acceleration_API "wikipedia:Video Acceleration API") (VA API)** - это библиотека с открытым исходным кодом (libVA) и API, который обеспечивает ускорение GPU для обработки видео в операционных системах Linux/UNIX. Процесс работает включая аппаратного ускорения обработки видео на разных входных точках (VLD, IDCT, Motion Compensation, deblocking) для распространенных стандартов кодирования (MPEG-2, MPEG-4 ASP/H.263, MPEG-4 AVC/H.264, and VC-1/WMV3).

У VA-API есть проприетарный бекэнд (появился в ноябре 2009) называемый [xvba-video](https://aur.archlinux.org/packages/xvba-video/), который позволяет приложениям VA-API использовать преимущества чипсетов AMD Radeons UVD2 через библиотеку [XvBA (X-Video Bitstream Acceleration API designed by AMD)](https://en.wikipedia.org/wiki/XvBA "wikipedia:XvBA").

**Примечание:** Нет необходимости устанавливать пакет [xvba-video](https://aur.archlinux.org/packages/xvba-video/), если вы используете `catalyst-test` или `catalyst-total`, потому что в этом случае работает символическая ссылка

Поддержка XvBA и xvba-video находится еще в стадии разработки, однако они **работают хорошо в большинстве случаев**. Соберите (или установите из репозитория Vi0L0) проприетарный пакет [xvba-video](https://aur.archlinux.org/packages/xvba-video/), если у вас имеются проблемы с этой версией установите [libva-xvba-driver](https://aur.archlinux.org/packages/libva-xvba-driver/), а также установите [mplayer-vaapi](https://aur.archlinux.org/packages/mplayer-vaapi/) и [libva](https://www.archlinux.org/packages/?name=libva). Затем просто скажите вашему видео проигрывателю, чтобы он использовал vaapi:gl как видеовыход:

```
$ mplayer -vo vaapi:gl movie.avi

```

Эти параметры могут быть добавлены в конфигурационный файл mplayer, смотрите [MPlayer](/index.php/MPlayer_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "MPlayer (Русский)").

Для **smplayer**:

```
Настройки → Настройки → Основные → Видео (вкладка) → Устройство вывода: Определено пользователем : vaapi:gl
Настройки → Настройки → Основные → Видео (вкладка) → Двойная буферизация **включить**
Настройки → Настройки → Основные → Основные → Снимки экрана → Включить снимки экрана **выключить**
Настройки → Настройки → Быстродействие → Потоков декодирование: **1** (чтобы выключить параметр -lavdopts)

```

**Примечание:** Если технология Tear Free Desktop включена, лучше использовать:
```
Настройки → Настройки → Основные → Видео (вкладка) → Устройство вывода: vaapi

```

Если Видео Выход **vaapi:gl** не работает - проверьте:

```
**vaapi**, **vaapi:gl2** или просто **xv(0 - AMD Radeon [AVIVO Video](https://en.wikipedia.org/wiki/Avivo "wikipedia:Avivo"))**.

```

Для **VLC**:

```
Инструменты → Настройки → Ввод & кодеки → Декодирование с аппаратным ускорением

```

Может помочь включение вертикальной синхронизации в **amdcccle**:

```
3D → More Settings → Wait for vertical refresh = Always On

```

**Примечание:** Если вы используете **Compiz/KWin**, то единственный способ **избежать мерцания видео** - это смотреть видео в **полноэкранном режиме** и только когда **Unredirect Fullscreen выключен**. В **compiz** вам нужно включить **Redirected Direct Rendering** в настройках ccsm. Если видео по прежнему мерцает, попробуйте выключить эту опцию в CCSM. Redirected Direct Rendering по умолчанию выключен в **KWin**, но если вы видите мерцания, попробуйте включить "Suspend desktop effects for fullscreen windows" или выключить в `System Settings` → `Desktop Effects` → `Advanced`.

### Частота, температура, скорость вентилятора, утилиты для разгона GPU/Памяти

Чтобы узнать частоту GPU/Памяти: `$ aticonfig --od-getclocks`.

Чтобы узнать скорость вентилятора: `$ aticonfig --pplib-cmd "get fanspeed 0"`

Чтобы узнать температуру: `$ aticonfig --odgt`

Чтобы установить скорость вращения вентилятора: `$ aticonfig --pplib-cmd "set fanspeed 0 50"`, где Query Index: 50, Скорость в процентах.

Для разгона и/или уменьшение частоты оборудования проще использовать программу с графическим интерфейсом, например **ATi Overclocking Utility**, которая очень простая и требует qt для работы. Она может быть устаревшей, но вы можете скачать ее [здесь](http://kde-apps.org/content/show.php/ATI+Overclock?content=47796).

Другая, более сложная утилита для выполнения таких операций - **AMDOverdriveCtrl**. Ее домашняя страница [здесь](http://sourceforge.net/projects/amdovdrvctrl) или вы можете собрать [amdoverdrivectrl](https://aur.archlinux.org/packages/amdoverdrivectrl/) из AUR или из неофициального репозитория Vi0L0.

### Два экрана (Dual Head / Dual Screen / Xinerama)

#### Введение

**Важно:** Вам следует запомнить, что тут нет единого решения, каждая установка и настройка нуждается в конфигурации. Поэтому вы должны адаптировать инструкции ниже под себя. Вполне возможно, что вам придется попробовать несколько раз. Поэтому вы должны сохранить ваш `/etc/X11/xorg.conf` **перед** началом изменений чтобы у вас была возможность восстановить рабочее состояние из командной строки.

*   В этой главе мы опишем установку двух экранов разных размеров с использование одной видеокарты, которая использует разные порты для вывода (DVI + HDMI) используя конфигурацию "Большой рабочий стол"

*   Решение в котором используется Xinerama имеет некоторые неудобства, особенно потому что она не совместима с XrandR. Именно по этой причине вы не должны использовать ее, т.к. XrandR понадобится нам для последующей конфигурации.

*   Решение в котором используется Dual Head позволит вам иметь 2 различные сессии (по одной на каждый экран). Это может быть то, что вы хотите, но вы не сможете перемещать окна с одного экрана на другой. Если у вас только один экран, вам придется определять мышь в вашей сессии Xorg для каждой из двух сессий внутри раздела Server Layout.

[Документация ATI](http://support.amd.com/us/kbarticles/Pages/1105-HowCanIConfigureMultip.aspx)

#### ATI Catalyst Control Center

Инструмент с графическим интерфейсом предоставляемый ATI очень полезен и мы постараемся использовать все его возможности. Чтобы запустить его, откройте терминал и выполните следующую команду:

```
$ {kdesu/gksu} amdcccle

```

**Важно:** Использовать sudo напрямую в графическом интерфейсе **не стоит**. Sudo дает административные привилегия вместе с информацией об учетной записи пользователя. Вместо него используйте *gksu* (GNOME) или *kdesu* (KDE).

#### Установка

Прежде чем мы начнем, убедитесь, что ваше оборудование правильно подключено и вы знаете ваши аппаратные характеристики (размеры экрана, диагональ, частота обновления и т.д.). Обычно оба экрана распознаются во время загрузки, но не обязательно правильно, особенно если вы не используете никакой конфигурационный файл Xorg (`/etc/X11/xorg.conf`), но надеетесь, что ваши устройства распознаются при запуске.

Сначала нужно убедится, что ваши экраны распознаются вашим DE и X. Для этого, вам нужно с генерировать базовый конфигурационный файл Xorg для двух экранов:

```
# aticonfig --initial --desktop-setup=horizontal --overlay-on=1

```

или

```
# aticonfig --initial=dual-head --screen-layout=left

```

**Примечание:** Аргумент `overlay` важен, поскольку он позволяет вам иметь 1 пиксель (или больше) разделенный между 2 экранами.

**Совет:** Для других возможных и доступных опций, напечатайте `aticonfig --help` внутри терминала чтобы отобразить все доступные аргументы командой строки.

Теперь у вас должен быть базовый файл конфигурации Xorg, который вы можете отредактировать чтобы добавить свое разрешение экрана. Важно использовать точное разрешение экрана, особенно если у вас мониторы разных размеров. Разрешения экрана должны быть добавлены в секцию "Screen":

```
SubSection "Display"
    Depth     24
    Modes     "X-resolution screen 1xY-resolution screen 1" "Xresolution screen 2xY-resolution screen 2"
EndSubSection

```

Теперь, вместо редактирования файла `xorg.conf` вручную, можно использовать инструмент с графическим интерфейсом от ATI. Перезапустите X чтобы убедится, что ваши два экрана поддерживаются должным образом и ваше разрешение экрана правильно распознавалось (Экраны должны быть независимыми, не должно быть отражения).

From now on, instead of editing the `xorg.conf` file manually, let us use the ATI GUI tool. Restart X to be sure that your two screens are properly supported and that the resolutions are properly recognized (Screens must be independent, not mirrored).

#### Конфигурация

Теперь вас остается только запустить панель управления ATI с привилегиями root, перейдите в меню дисплей и выберите как вы бы хотели установить вашу конфигурацию (маленькая стрелка выпадающего меню). Перезапустите X и все должно быть готово!

Перед перезагрузкой X перепроверьте ваш новый `xorg.conf`. Внутри подраздела "Display", который находится внутри "Screen" вы должны увидеть "виртуальную" командную строку, которая определяет какое разрешение экрана в сумме должно быть у обоих экранов. Раздел "Server Layout" описывает все остальное.

## Удаление

Если по какой-либо причине драйвер не работает или вы просто хотите попробовать открытый драйвер, удалите пакеты `catalyst` и `catalyst-utils`. Также вы должны удалить пакеты [catalyst-generator](https://aur.archlinux.org/packages/catalyst-generator/), [catalyst-hook](https://aur.archlinux.org/packages/catalyst-hook/) и [lib32-catalyst-utils](https://aur.archlinux.org/packages/lib32-catalyst-utils/) если они установлены в вашей системе.

**Важно:**

*   Вам, возможно, придется использовать `# pacman -Rdd` чтобы удалить [catalyst-utils](https://aur.archlinux.org/packages/catalyst-utils/) (и/или [lib32-catalyst-utils](https://aur.archlinux.org/packages/lib32-catalyst-utils/)), потому что этот пакет содержит связанные файлы *gl* и много ваших пакетов зависят от них. Эти зависимости снова удовлетворятся когда вы установите [xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati).
*   Вам, возможно, придется удалить `/etc/profile.d/ati-flgrx.sh` и `/etc/profile.d/lib32-catalyst` (если они существуют в вашей системе), в противном случае `r600_dri.so` не сможет загрузится и у вас скорее всего не будет 3D поддержки.

**Примечание:** Вам следует удалить неофициальный репозиторий из вашего `/etc/pacman.conf` и запустить `# pacman -Syu`, потому что они содержат пакеты с устаревшими версиями Xorg, которые позволяют использовать `catalyst`, а пакету [xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati) нужна самая свежая версия пакета Xorg из [Официальных репозиториев](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)").

Также выполните следующие действие:

*   Если у вас есть файл `/etc/modprobe.d/blacklist-radeon.conf`, удалите его или закомментируйте строку `blacklist radeon` в этом файле
*   Если у вас есть файл в `/etc/modules-load.d`, который загружает модуль `fglrx` при загрузке, удалите его или закомментируйте линию, которая содержит `fglrx`.
*   Убедитесь в том, что вы удалили или сделали резервную копию файла `/etc/X11/xorg.conf`.
*   Если у вас установлен пакет [catalyst-hook](https://aur.archlinux.org/packages/catalyst-hook/), убедитесь в том, что вы [отключили](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.8E.D0.BD.D0.B8.D1.82.D0.BE.D0.B2 "Systemd (Русский)") службу.
*   Если вы использовали параметр `nomodeset` в [параметрах ядра](/index.php/Kernel_parameters_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Kernel parameters (Русский)") и планируете использовать KMS, удалите его.
*   **Перезагрузитесь** перед установкой другого драйвера.

## Решение проблем

Если вы все еще загружаетесь в командную строку, то проблема скорее всего заключается в `/etc/X11/xorg.conf`

Вы можете проанализировать весь `/var/log/Xorg.0.log`:

```
$ grep '(EE)' /var/log/Xorg.0.log
$ grep '(WW)' /var/log/Xorg.0.log

```

Если вы до сих пор не понимаете в чем проблема, сначала попробуйте поискать на форумах. Затем опубликуйте сообщение в тему [специфичную для ATI/AMD](https://bbs.archlinux.org/viewtopic.php?pid=1166052#p1166052/). В сообщение вложите файл `xorg.conf` и вывод двух команд сверху.

### Не удалось запустить atieventsd.service

Установите [acpid](https://www.archlinux.org/packages/?name=acpid) из [официальных репозиториев](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)"). [Запустите](/index.php/%D0%97%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D0%B5 "Запустите") и включите [службу](/index.php/Daemon "Daemon") acpid.

Если служба не смогла запуститься, отредактируйте файл `/usr/lib/systemd/system/atieventsd.service` и замените `acpid.socket` на `acpid.service`.

### Не удалось открыть fglrx_dri.so

Создайте символическую ссылку из файла `/usr/lib/xorg/modules/dri/fglrx_dri.so` на файл `/usr/X11R6/lib64/modules/dri/fglrx_dri.so` (или другой требуемый путь):

```
# mkdir -p /usr/X11R6/lib64/modules/dri
# ln -s /usr/lib/xorg/modules/dri/fglrx_dri.so /usr/X11R6/lib64/modules/dri/fglrx_dri.so

```

### Не запускается GDM

Понизьте версию пакета [xorg-server](https://www.archlinux.org/packages/?name=xorg-server) или попытайтесь использовать другой [экранный менеджер](/index.php/Display_manager_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Display manager (Русский)"), например, [LightDM](/index.php/LightDM "LightDM").

### Притормаживают 3D приложения в Wine

Если вы используете 3D приложения в Wine и они притормаживают, вам нужно выключить TLS. Чтобы это сделать, вы можете использовать `aticonfig` или отредактировать файл `/etc/X11/xorg.conf`. Используя `aticonfig`:

```
# aticonfig --tls=off

```

Или, отредактировать файл `/etc/X11/xorg.conf`; сначала, откройте файл в редакторе с привилегиями root, а затем добавьте `Option "UseFastTLS" "off"` в раздел *Device* этого файла.

После выполнения любого из решений, перезапустите X для того, чтобы изменения вступили в силу.

### Проблема с цветами в видео

Вы по-прежнему можете использовать `vaapi:gl` чтобы избежать мерцания в видео, но без графического ускорения:

*   Запустите **mplayer** без `-vo vaapi`.
*   Запустите **smplayer** и удалите `-vo vaapi` из Настройки → Настройки → Дополнительно → Параметры MPlayer → Настройки: -vo vaapi

Теперь мы можете безопасно включить скриншоты в **smplayer**.

### KWin и композит

Вы можете использовать XRender если визуализация при помощи OpenGL очень медленная. Однако, XRender может быть медленнее чем OpenGL в зависимости от вашей карты. XRender также решает артефакты в некоторых случаях, например, при изменении размера Konsole.

### Черный экран с полным зависанием и/или притормаживания после перезагрузки или startx

Убедитесь в том, что вы добавили параметр `nomodeset` в параметры ядра в вашем загрузчике (смотрите [#Отключение kernel mode setting](#.D0.9E.D1.82.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_kernel_mode_setting)).

Если вы используете legacy драйвер (`catalyst-hd234k`) и получаете черный экран, попробуйте понизить версию xorg-server до 1.12 используя репозиторий [#xorg112](#xorg112).

#### Неисправные вызовы ACPI

Вполне возможно, что fglrx может плохо кооперировать с системным ACPI при помощи аппаратных вызовов, поэтому он автоматически отключается и из-за этого нет вывода на экран.

Если это так, попробуйте запустить:

```
$ aticonfig --acpi-services=off

```

#### Неподдерживаемые версии ядра Linux

Catalyst не поддерживает ядро Linux 4.2 и выше.

Пожалуйста, настройте загрузчик так, чтобы использовалось правильное ядро при загрузке, как linux-lts например.

### KDM исчезает после выхода из системы

Если вы используете проприетарный драйвер Catalyst и вы получаете консоль (tty1) вместо ожидаемого приветсвия KDM после выхода, вы должны дать указания KDM чтобы он перезапускал сервер X после каждого выхода. Раскоментируйте линию в разделе `[X-:*-Core]`

 `/usr/share/config/kdm/kdmrc`  `TerminateServer=True` 

Теперь KDM будет появляться после выхода из KDE.

### Не работает Direct Rendering

Проблема может возникнуть при использование проприетарного драйвера **Catalyst**.

**Важно:** Эта ошибка также появляется, если вы не **перезапустили** систему после установки или обновления catalyst. Система должна правильно загрузить модуль fglrx.ko, чтобы драйвер работал.

Если у вас проблемы с direct rendering, запустите:

```
$ LIBGL_DEBUG=verbose glxinfo > /dev/null

```

в командной строке. В самом начале вывода, как правило, показываются сообщения об ошибке, которые говорят вам о том, что у вас отсутствует direct rendering.

Распространенные ошибки и способы их устранения:

```
libGL error: XF86DRIQueryDirectRenderingCapable returned false

```

*   Убедитесь в том, что вы правильно загрузили модуль для вашего чипсета AGP перед модулем ядра `fglrx`. Чтобы узнать, какой именно модуль AGP требуется, запустите `# hwdetect --show-agp`. Затем, откройте файл `/etc/modules-load.d/fglrx.conf` и добавьте модуль AGP **перед** линией, которая содержит `fglrx`.

```
libGL error: failed to open DRM: Operation not permitted
libGL error: reverting to (slow) indirect rendering

```

```
libGL: OpenDriver: trying /usr/lib/xorg/modules/dri//fglrx_dri.so
libGL error: dlopen /usr/lib/xorg/modules/dri//fglrx_dri.so failed
(/usr/lib/xorg/modules/dri//fglrx_dri.so: cannot open shared object file: No such file or directory)
libGL error: unable to find driver: fglrx_dri.so

```

*   Что-то не было правильно инициализировано. Если путь в ошибке - `/usr/X11R6/lib/modules/dri/fglrx_dri.so`, то, убедитесь в том, что вы полностью вышли из системы, затем, зайдите снова. Если вы используете графический экранный менеджер (gdm, kdm, xdm), убедитесь в том, что `/etc/profile` выполняется при каждом входе. Обычно это делается путем добавления `source /etc/profile` в `~/.xsession` или `~/.xinitrc`, но это может варьироваться в зависимости от используемого экранного менеджера.

*   Если путь в ошибке - `/usr/lib/xorg/modules/dri/fglrx_dri.so`, значит, что-то не было правильно установлено. Попробуйте переустановить пакет [catalyst](https://aur.archlinux.org/packages/catalyst/).

Такие ошибки как:

```
fglrx: libGL version undetermined - OpenGL module is using glapi fallback

```

вызваны тем, что у вас в системе несколько версий `libGL.so`. Команда ниже должна вернуть следующее:

 `$ locate libGL.s` 
```
/usr/lib/libGL.so
/usr/lib/libGL.so.1
/usr/lib/libGL.so.1.2
```

В вашей системе должно быть только три файла libGL.so. Если у вас больше (например, `/usr/X11R6/lib/libGL.so.1.2`), удалите их. Это должно исправить ошибку.

Вы можете не получать никакого сообщения об ошибке. Если вы используете X11R7, убедитесь в том, что у вас **нет** следующих файлов в системе:

```
/usr/X11R6/lib/libGL.so.1.2
/usr/X11R6/lib/libGL.so.1

```

### Проблемы с гибернацией/сном

#### Видео не возобновляется из suspend2ram

Проприетарный драйвер Catalyst не сможет выйти из ждущего режима пока фреймбуфер включен. Чтобы отключить фреймбуфер, добавьте `vga=0` в [параметры ядра](/index.php/Kernel_parameters_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Kernel parameters (Русский)").

Чтобы увидеть, где нужно добавить эти параметры для других загрузчиков, смотрите [#Отключение kernel mode setting](#.D0.9E.D1.82.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_kernel_mode_setting)

### Система Притормаживает/Сильно зависает

*   Драйвера фреймбуфера `radeonfb` в прошлом вызывали проблемы такого характера. Если ваше ядро скомпилировано с поддержкой radeonfb, вы можете попробовать другое ядро и посмотреть, помогает ли это.

*   Если у вас притормаживает система когда вы выходите из DE (выключение, режим ожидания, переключение на tty и т.д.), то вы скорее всего забыли выключить KMS. (смотрите [#Отключение kernel mode setting](#.D0.9E.D1.82.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_kernel_mode_setting))

### Конфликты оборудования

Видеокарты Radeon в сочетании с некоторыми версиями чипсетов nForce3 (например, nForce 3 250Gb) не будут иметь 3D-ускорения. В настоящее время причина этой проблемы неизвестна, но некоторые источники указывают, что можно включить 3D-ускорение с таким сочетанием оборудования. Нужно загрузиться в Windows с драйверами от Nvidia, а затем перезагрузить систему. Работоспособность можно проверить получив сообщения похожие на эти (с использованием системы, основанной на nForce3):

 `$ dmesg | grep agp` 
```
agpgart: Detected AGP bridge 0
agpgart: Setting up Nforce3 AGP.
agpgart: aperture base > 4G

```

а также, если вы получите следующий вывод:

 `$ tail -n 100 /var/log/Xorg.0.log | grep agp`  `(EE) fglrx(0): [agp] unable to acquire AGP, error "xf86_ENODEV"` 

у вас есть этот баг.

Некоторые источники указывают, что в некоторых ситуациях может помочь откат на предыдущую версию BIOS, но это невозможно проверить во всех случаях. Кроме того, **неправильный откат BIOS может привести оборудование в негодное состояние, будьте осторожны.**

Смотрите [этот отчет об ошибке](http://bugzilla.kernel.org/show_bug.cgi?id=6350/) для получения дополнительной информации и потенциальных решений.

### Временные зависания при воспроизведении видео

Эта проблема может возникнуть при использовании проприетарного Catalyst.

Если у вас возникают временные зависания продолжительностью от нескольких секунд до нескольких минут, происходящее случайным образом во время воспроизведения в mplayer, проверьте системные логи и вывод должен быть примерно таким:

 `/var/log/messages.log` 
```
Nov 28 18:31:56 pandemonium [<c01c64a6>] ? proc_get_sb+0xc6/0x160
Nov 28 18:31:56 pandemonium [<c01c64a6>] ? proc_get_sb+0xc6/0x160
Nov 28 18:31:56 pandemonium [<f8bc628c>] ? ip_firegl_ioctl+0x1c/0x30 [fglrx]
Nov 28 18:31:56 pandemonium [<c01c64a6>] ? proc_get_sb+0xc6/0x160
Nov 28 18:31:56 pandemonium [<c0197038>] ? vfs_ioctl+0x78/0x90
Nov 28 18:31:56 pandemonium [<c01970b7>] ? do_vfs_ioctl+0x67/0x2f0
Nov 28 18:31:56 pandemonium [<c01973a6>] ? sys_ioctl+0x66/0x70
Nov 28 18:31:56 pandemonium [<c0103ef3>] ? sysenter_do_call+0x12/0x33
Nov 28 18:31:56 pandemonium [<c01c64a6>] ? proc_get_sb+0xc6/0x160
Nov 28 18:31:56 pandemonium =======================
```

Добавьте `nopat` и/или `nomodeset` в [параметры ядра](/index.php/Kernel_parameters_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Kernel parameters (Русский)"), после этого все должно работать.

### "aticonfig: No supported adapters detected"

If you get the following:

 `# aticonfig --initial` 
```
aticonfig: No supported adapters detected

```

It may still be possible to get Catalyst working by manually setting the device in your your `etc/X11/xorg.conf` file or by copying an older working `/etc/ati/control` file (preferred - this also fixes the watermark issue).

To get an older control file, download a previous version of fglrx from AMD and run it with `--extract driver` parameter. You'll find the control file in `driver/common/etc/ati/control`. Copy the extracted file over the system file and restart Xorg. You can try different versions of the file.

To set your model in `xorg.conf`, edit the device section of `/etc/X11/xorg.conf` to:

 `/etc/X11/xorg.conf` 
```
Section "Device"
        Identifier "ATI radeon ********"
        Driver     "fglrx"
EndSection

```

Where `****` should be replaced with your device's marketing number (e.g. 6870 for the HD 6870 and 6310 for the E-350 APU).

Xorg will start and it is possible to use `amdcccle` instead of `aticonfig`. There will be an "AMD Unsupported hardware" watermark.

You can remove this watermark using the following script:

```
#!/bin/sh
DRIVER=/usr/lib/xorg/modules/drivers/fglrx_drv.so
for x in $(objdump -d $DRIVER|awk '/call/&&/EnableLogo/{print "\\x"$2"\\x"$3"\\x"$4"\\x"$5"\\x"$6}'); do
   sed -i "s/$x/\x90\x90\x90\x90\x90/g" $DRIVER
done

```

and then reboot your machine.

### Поддержка WebGL в chromium

Google has blacklisted Linux's Catalyst driver from supporting webGL in their Chromium/Chrome browsers. See [Chromium#WebGL](/index.php/Chromium_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#WebGL "Chromium (Русский)") for details.

### Задержки/подтормаживания просматривая flash видео через Adobe's flashplugin

Edit:

 `/etc/adobe/mms.cfg` 
```
#EnableLinuxHWVideoDecode=1
OverrideGPUValidation=true
```

If you are using KDE make sure that "Suspend desktop effects for fullscreen windows" is unchecked under `System Settings` → `Desktop Effects` → `Advanced`.

### Задержки/медленные перемещения окон в GNOME3

You can try this solution, it has been reported to work for many people.

Add this line into `~/.profile` or into `/etc/profile`:

```
export CLUTTER_VBLANK=none

```

Restart X server or reboot your system.

### Not using full screen resolution at 1920x1080 (underscanning, black borders around the screen)

This usually happens when you use a HDMI connection to connect your monitor/TV to your computer.

Seemed to be a feature by AMD/ATI to work with all HDTVs that could be adjusted via the amdccle.

Using the amdcccle GUI you can select the affected display, go to adjustments, and set underscan to 0% (aticonfig defaults to 15% underscan). It is possible as well that the underscan slider won't show under the display's adjustments, as sometimes in (at least) version 14.10.

The problem is that the settings will not persist after restarting X server or rebooting or wake up or might even revert after changing TTYs.

For the changes to become permanent, you will need to adjust the underscan settings manually using "aticonfig" via console (as root) or manually edit the file `/etc/ati/amdpcsdb` (as root)

**using aticonfig method:**

```
# aticonfig --set-pcs-u32=MCIL,DigitalHDTVDefaultUnderscan,0

```

After changing the settings, reboot.

For newer version (for example, 12.11), if Catalyst control center repeatedly fails to save the overscan setting you can also try:

```
# aticonfig --set-pcs-u32=MCIL,TVEnableOverscan,0

```

**Manually editing /etc/ati/amdpcsdb method:**

Add the following line anywhere under the following header `[AMDPCSROOT/SYSTEM/MCIL]`

```
# DigitalHDTVDefaultUnderscan=V0

```

For newer version (for example, 12.11), if Catalyst control center repeatedly fails to save the overscan setting you can also try: locate under `[AMDPCSROOT/SYSTEM/MCIL]` the following line

```
# TVEnableOverscan=V1

```

and change it to

```
# TVEnableOverscan=V0

```

After changing the settings, reboot.

**Note:** You might find that the file `/etc/ati/amdpcsdb` will be overwritten and revert no matter what you do as user or as root even with log in/log out/reboot, ergo the modification will not stick.

For the amd database file not to be overwritten you have to modify it without the fgrlx driver running.

This can be made by rebooting in any "safe mode" that will not use the driver or directly booting into console mode

**Workaround:** For whatever reason you can find yourself not wanting to touch ATI's config files you can circumvent the problem by forcing the panel's position and resolution: as user:

```
# aticonfig --set-dispattrib=DISPLAYTYPE,positionX:0
# aticonfig --set-dispattrib=DISPLAYTYPE,positionY:0
# aticonfig --set-dispattrib=DISPLAYTYPE,sizeX:1920
# aticonfig --set-dispattrib=DISPLAYTYPE,sizeY:1080

```

`DISPLAYTYPE` will be the name of the monitor you want to change it's attributes, for example "dfp9". To get the name of your `DISPLAYTYPE` run the following command:

```
# xrandr --current

```

Should RandR be not enabled use:

```
# aticonfig --query-monitor

```

Using the display switch or DISPLAY variable set to the appropriate display/screen (:0.1 for example) might be necessary.

That will show you which displays are connected and disconnected and it's properties

This workaround will not persist but it is a quick fix that will show that the panel works just fine and that the above solutions are to be put into place.

**Note:** `aticonfig --set-pcs-val=MCIL,DigitalHDTVDefaultUnderscan,0` should not be used on newer versions of the driver as it is deprecated and will be soon removed as stated by ATI.

Try `aticonfig --help | grep set-pcs-val` to read ATI's notice

### Dual Screen Setup: general problems with acceleration, OpenGL, compositing, performance

Try to disable xinerama and xrandr12\. Check out ie. this way:

Type those commands:

```
# aticonfig --initial
# aticonfig --set-pcs-str="DDX,EnableRandR12,FALSE"

```

Then reboot your system. In `/etc/X11/xorg.conf` check that xinerama is disabled, if it's not disable it and reboot your system.

Next run `amdcccle` and pick up amdcccle → display manager → multi-display → multidisplay desktop with display(s) 2.

Reboot again and set up your display layout whatever you desire.

### Disabling VariBright feature

Type the following command to disable VariBright:

```
# aticonfig --set-pcs-u32=MCIL,PP_UserVariBrightEnable,0

```

### Hybrid/PowerXpress: turning off discrete GPU

When you are using [catalyst-total-pxp](https://aur.archlinux.org/packages/catalyst-total-pxp/) or catalyst-utils-pxp and you are switching to integrated GPU you may notice that discrete GPU is still working, consuming power and making your system's temperature higher.

Sometimes ie. when your integrated GPU is intel's one you can use `vgaswitcheroo` to turn the discrete GPU off. Sometimes unfortunatelly, it's not working.

Then you may check out [acpi_call](https://aur.archlinux.org/packages/?O=0&K=acpi_call). MrDeepPurple has prepared the script which he's using to perform 'turn off' task, he's calling script via systemd service while booting and resuming his system. Here's his script:

```
#!/bin/sh
libglx=$(/usr/lib/fglrx/switchlibglx query)
modprobe acpi_call
if [ "$libglx" = "intel" ]; then
    echo '\_SB.PCI0.PEG0.PEGP._OFF' > /proc/acpi/call
fi

```

### Switching from X session to TTYs gives a blank screen/low resolution TTY

Workaround for this "feature", which appeared in catalyst 13.2 betas, is to use `vga=` kernel option, like `vga=792`. You can get the list of supported resolutions with the

```
$ hwinfo --framebuffer

```

command. Get the one that corresponds to your wanted resolution, and copy-paste it into kernel line of your bootloader, so it could look like ie. `vga=0x03d4`

### Switching from X session to TTYs gives a black screen with the monitor backlight on

Используйте [uvesafb](/index.php/Uvesafb "Uvesafb") в качестве драйвера для фреймбуфера. Кроме того с помощью `uvesafb` вы можете установить любое разрешение в TTY.

### Switching to TTYs then back to X session gives a black screen with a mouse cursor

If you experience this bug, try adding

```
Option      "XAANoOffscreenPixmaps" "true"

```

to the 'Device' section of your xorg.conf file.

Also, make sure you have a [polkit authentication agent](/index.php/Polkit#Authentication_agents "Polkit") installed and running, as this behavior can happen when a program is asking for a password, but doesn't have an authentication agent installed to display the password dialog box.

### 30 FPS / Tear-Free / V-Sync bug

Bug introduced in Catalyst 13.6 beta, not fixed till now (13.9).

After enabling "Tear-Free" functionality every freshly started OpenGL application is lagging, often generates only 30 FPS, it also touches composited desktop.

Workaround is pretty simple and was found by M132\. Here are the steps, do everything in "AMD Catalyst Control Center" (amdcccle) application:

```
1\. Enable Tear-Free, it will set 3D V-Sync option to "Always on".
2\. Set 3D V-Sync to "Always Off".
3\. Make sure Tear-Free is still on.
4\. Restart X / Re-login.

```

It is working well on KDE 4.11.x, but in case of problems M132 suggests: "Try disabling "Detect refresh rate" and specify monitor's refresh rate in the Composite plugin."

### Backlight adjustment does not work

If you have a problem with backlight adjustment, you can try the following command:

```
# aticonfig --set-pcs-u32=MCIL,PP_PhmUseDummyBackEnd,1

```

Some users reported that this can decrease FPS. To restore defaults, run:

```
# aticonfig --set-pcs-u32=MCIL,PP_PhmUseDummyBackEnd,0

```

[Read more about this bug](http://ati.cchtml.com/show_bug.cgi?id=711)

## See also

*   [Unofficial Wiki for the ATI Linux Driver](http://wiki.cchtml.com/index.php/Main_Page)
*   [Unofficial ATI Linux Driver Bugzilla](http://ati.cchtml.com/query.cgi)