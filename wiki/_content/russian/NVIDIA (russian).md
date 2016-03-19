Данная статья описывает процесс установки и настройки проприетарного драйвера графических карт [NVIDIA](http://www.nvidia.com). Для получения информации о драйверах с открытым исходным кодом обратитесь к статье [Nouveau (Русский)](/index.php/Nouveau_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Nouveau (Русский)"). Также есть отдельная статья для обладателей ноутбуков с технологиями на базе [NVIDIA Optimus](/index.php/NVIDIA_Optimus "NVIDIA Optimus").

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
    *   [1.1 Неподдерживаемые драйвера](#.D0.9D.D0.B5.D0.BF.D0.BE.D0.B4.D0.B4.D0.B5.D1.80.D0.B6.D0.B8.D0.B2.D0.B0.D0.B5.D0.BC.D1.8B.D0.B5_.D0.B4.D1.80.D0.B0.D0.B9.D0.B2.D0.B5.D1.80.D0.B0)
    *   [1.2 Альтернативная установка: собственное ядро](#.D0.90.D0.BB.D1.8C.D1.82.D0.B5.D1.80.D0.BD.D0.B0.D1.82.D0.B8.D0.B2.D0.BD.D0.B0.D1.8F_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0:_.D1.81.D0.BE.D0.B1.D1.81.D1.82.D0.B2.D0.B5.D0.BD.D0.BD.D0.BE.D0.B5_.D1.8F.D0.B4.D1.80.D0.BE)
        *   [1.2.1 Автоматическая пересборка модуля NVIDIA при обновлении ядра](#.D0.90.D0.B2.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B0.D1.8F_.D0.BF.D0.B5.D1.80.D0.B5.D1.81.D0.B1.D0.BE.D1.80.D0.BA.D0.B0_.D0.BC.D0.BE.D0.B4.D1.83.D0.BB.D1.8F_NVIDIA_.D0.BF.D1.80.D0.B8_.D0.BE.D0.B1.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B8_.D1.8F.D0.B4.D1.80.D0.B0)
*   [2 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [2.1 Минимальная настройка](#.D0.9C.D0.B8.D0.BD.D0.B8.D0.BC.D0.B0.D0.BB.D1.8C.D0.BD.D0.B0.D1.8F_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [2.2 Автоматическая настройка](#.D0.90.D0.B2.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B0.D1.8F_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [2.3 Несколько мониторов](#.D0.9D.D0.B5.D1.81.D0.BA.D0.BE.D0.BB.D1.8C.D0.BA.D0.BE_.D0.BC.D0.BE.D0.BD.D0.B8.D1.82.D0.BE.D1.80.D0.BE.D0.B2)
        *   [2.3.1 Использование NVIDIA Settings](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_NVIDIA_Settings)
        *   [2.3.2 ConnectedMonitor](#ConnectedMonitor)
        *   [2.3.3 TwinView](#TwinView)
            *   [2.3.3.1 Ручная конфигурация из командной строки с использованием xrandr](#.D0.A0.D1.83.D1.87.D0.BD.D0.B0.D1.8F_.D0.BA.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D1.8F_.D0.B8.D0.B7_.D0.BA.D0.BE.D0.BC.D0.B0.D0.BD.D0.B4.D0.BD.D0.BE.D0.B9_.D1.81.D1.82.D1.80.D0.BE.D0.BA.D0.B8_.D1.81_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5.D0.BC_xrandr)
        *   [2.3.4 Режим Mosaic](#.D0.A0.D0.B5.D0.B6.D0.B8.D0.BC_Mosaic)
            *   [2.3.4.1 Base Mosaic](#Base_Mosaic)
            *   [2.3.4.2 SLI Mosaic](#SLI_Mosaic)
    *   [2.4 Драйвер Persistence](#.D0.94.D1.80.D0.B0.D0.B9.D0.B2.D0.B5.D1.80_Persistence)
*   [3 Тонкая настройка](#.D0.A2.D0.BE.D0.BD.D0.BA.D0.B0.D1.8F_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [3.1 Графический интерфейс: nvidia-settings](#.D0.93.D1.80.D0.B0.D1.84.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8.D0.B9_.D0.B8.D0.BD.D1.82.D0.B5.D1.80.D1.84.D0.B5.D0.B9.D1.81:_nvidia-settings)
    *   [3.2 Дополнительно: 20-nvidia.conf](#.D0.94.D0.BE.D0.BF.D0.BE.D0.BB.D0.BD.D0.B8.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D0.BE:_20-nvidia.conf)
        *   [3.2.1 Запрет логотипа при загрузке](#.D0.97.D0.B0.D0.BF.D1.80.D0.B5.D1.82_.D0.BB.D0.BE.D0.B3.D0.BE.D1.82.D0.B8.D0.BF.D0.B0_.D0.BF.D1.80.D0.B8_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B5)
        *   [3.2.2 Переопределение обнаружения монитора](#.D0.9F.D0.B5.D1.80.D0.B5.D0.BE.D0.BF.D1.80.D0.B5.D0.B4.D0.B5.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BE.D0.B1.D0.BD.D0.B0.D1.80.D1.83.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F_.D0.BC.D0.BE.D0.BD.D0.B8.D1.82.D0.BE.D1.80.D0.B0)
        *   [3.2.3 Включение контроля яркости](#.D0.92.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BA.D0.BE.D0.BD.D1.82.D1.80.D0.BE.D0.BB.D1.8F_.D1.8F.D1.80.D0.BA.D0.BE.D1.81.D1.82.D0.B8)
        *   [3.2.4 Включение SLI](#.D0.92.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_SLI)
        *   [3.2.5 Включение разгона](#.D0.92.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D1.80.D0.B0.D0.B7.D0.B3.D0.BE.D0.BD.D0.B0)
            *   [3.2.5.1 Настройка статического 2D/3D разгона](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D1.81.D1.82.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.BE.D0.B3.D0.BE_2D.2F3D_.D1.80.D0.B0.D0.B7.D0.B3.D0.BE.D0.BD.D0.B0)
*   [4 Советы и подсказки](#.D0.A1.D0.BE.D0.B2.D0.B5.D1.82.D1.8B_.D0.B8_.D0.BF.D0.BE.D0.B4.D1.81.D0.BA.D0.B0.D0.B7.D0.BA.D0.B8)
    *   [4.1 Исправление разрешения терминала](#.D0.98.D1.81.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D1.80.D0.B0.D0.B7.D1.80.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D1.8F_.D1.82.D0.B5.D1.80.D0.BC.D0.B8.D0.BD.D0.B0.D0.BB.D0.B0)
    *   [4.2 Включение Pure Video HD (VDPAU/VAAPI)](#.D0.92.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_Pure_Video_HD_.28VDPAU.2FVAAPI.29)
    *   [4.3 Избежание разрывов изображения (тьюринга) в KDE (KWin)](#.D0.98.D0.B7.D0.B1.D0.B5.D0.B6.D0.B0.D0.BD.D0.B8.D0.B5_.D1.80.D0.B0.D0.B7.D1.80.D1.8B.D0.B2.D0.BE.D0.B2_.D0.B8.D0.B7.D0.BE.D0.B1.D1.80.D0.B0.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F_.28.D1.82.D1.8C.D1.8E.D1.80.D0.B8.D0.BD.D0.B3.D0.B0.29_.D0.B2_KDE_.28KWin.29)
    *   [4.4 Аппартное ускорение декодирования видео с помощью XvMC](#.D0.90.D0.BF.D0.BF.D0.B0.D1.80.D1.82.D0.BD.D0.BE.D0.B5_.D1.83.D1.81.D0.BA.D0.BE.D1.80.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B4.D0.B5.D0.BA.D0.BE.D0.B4.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D1.8F_.D0.B2.D0.B8.D0.B4.D0.B5.D0.BE_.D1.81_.D0.BF.D0.BE.D0.BC.D0.BE.D1.89.D1.8C.D1.8E_XvMC)
    *   [4.5 Использование ТВ-выхода](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.A2.D0.92-.D0.B2.D1.8B.D1.85.D0.BE.D0.B4.D0.B0)
    *   [4.6 X на ТВ (DFP) как основной экран](#X_.D0.BD.D0.B0_.D0.A2.D0.92_.28DFP.29_.D0.BA.D0.B0.D0.BA_.D0.BE.D1.81.D0.BD.D0.BE.D0.B2.D0.BD.D0.BE.D0.B9_.D1.8D.D0.BA.D1.80.D0.B0.D0.BD)
    *   [4.7 Проверка источника питания](#.D0.9F.D1.80.D0.BE.D0.B2.D0.B5.D1.80.D0.BA.D0.B0_.D0.B8.D1.81.D1.82.D0.BE.D1.87.D0.BD.D0.B8.D0.BA.D0.B0_.D0.BF.D0.B8.D1.82.D0.B0.D0.BD.D0.B8.D1.8F)
    *   [4.8 Отображение температуры графического процессора в оболочке](#.D0.9E.D1.82.D0.BE.D0.B1.D1.80.D0.B0.D0.B6.D0.B5.D0.BD.D0.B8.D0.B5_.D1.82.D0.B5.D0.BC.D0.BF.D0.B5.D1.80.D0.B0.D1.82.D1.83.D1.80.D1.8B_.D0.B3.D1.80.D0.B0.D1.84.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.BE.D0.B3.D0.BE_.D0.BF.D1.80.D0.BE.D1.86.D0.B5.D1.81.D1.81.D0.BE.D1.80.D0.B0_.D0.B2_.D0.BE.D0.B1.D0.BE.D0.BB.D0.BE.D1.87.D0.BA.D0.B5)
        *   [4.8.1 Метод 1 - nvidia-settings](#.D0.9C.D0.B5.D1.82.D0.BE.D0.B4_1_-_nvidia-settings)
        *   [4.8.2 Метод 2 - nvidia-smi](#.D0.9C.D0.B5.D1.82.D0.BE.D0.B4_2_-_nvidia-smi)
        *   [4.8.3 Метод 3 - nvclock](#.D0.9C.D0.B5.D1.82.D0.BE.D0.B4_3_-_nvclock)
    *   [4.9 Утсановка скорости вентилятора при входе](#.D0.A3.D1.82.D1.81.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D1.81.D0.BA.D0.BE.D1.80.D0.BE.D1.81.D1.82.D0.B8_.D0.B2.D0.B5.D0.BD.D1.82.D0.B8.D0.BB.D1.8F.D1.82.D0.BE.D1.80.D0.B0_.D0.BF.D1.80.D0.B8_.D0.B2.D1.85.D0.BE.D0.B4.D0.B5)
    *   [4.10 Порядок установки/удаления при смене драйвера](#.D0.9F.D0.BE.D1.80.D1.8F.D0.B4.D0.BE.D0.BA_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B8.2F.D1.83.D0.B4.D0.B0.D0.BB.D0.B5.D0.BD.D0.B8.D1.8F_.D0.BF.D1.80.D0.B8_.D1.81.D0.BC.D0.B5.D0.BD.D0.B5_.D0.B4.D1.80.D0.B0.D0.B9.D0.B2.D0.B5.D1.80.D0.B0)
    *   [4.11 Переключение между драйверами NVIDIA и nouveau](#.D0.9F.D0.B5.D1.80.D0.B5.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BC.D0.B5.D0.B6.D0.B4.D1.83_.D0.B4.D1.80.D0.B0.D0.B9.D0.B2.D0.B5.D1.80.D0.B0.D0.BC.D0.B8_NVIDIA_.D0.B8_nouveau)
    *   [4.12 Как избежать разрывов/тьюринга на картах GeForce 500/600/700/900 series](#.D0.9A.D0.B0.D0.BA_.D0.B8.D0.B7.D0.B1.D0.B5.D0.B6.D0.B0.D1.82.D1.8C_.D1.80.D0.B0.D0.B7.D1.80.D1.8B.D0.B2.D0.BE.D0.B2.2F.D1.82.D1.8C.D1.8E.D1.80.D0.B8.D0.BD.D0.B3.D0.B0_.D0.BD.D0.B0_.D0.BA.D0.B0.D1.80.D1.82.D0.B0.D1.85_GeForce_500.2F600.2F700.2F900_series)
*   [5 Возможные проблемы](#.D0.92.D0.BE.D0.B7.D0.BC.D0.BE.D0.B6.D0.BD.D1.8B.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D1.8B)
    *   [5.1 Игры при использовании TwinView](#.D0.98.D0.B3.D1.80.D1.8B_.D0.BF.D1.80.D0.B8_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B8_TwinView)
    *   [5.2 Вертикальная синхронизация при использовании TwinView](#.D0.92.D0.B5.D1.80.D1.82.D0.B8.D0.BA.D0.B0.D0.BB.D1.8C.D0.BD.D0.B0.D1.8F_.D1.81.D0.B8.D0.BD.D1.85.D1.80.D0.BE.D0.BD.D0.B8.D0.B7.D0.B0.D1.86.D0.B8.D1.8F_.D0.BF.D1.80.D0.B8_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B8_TwinView)
    *   [5.3 Wayland (gdm) рушится после установки nvidia-libgl](#Wayland_.28gdm.29_.D1.80.D1.83.D1.88.D0.B8.D1.82.D1.81.D1.8F_.D0.BF.D0.BE.D1.81.D0.BB.D0.B5_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B8_nvidia-libgl)
    *   [5.4 Старые настройки Xorg](#.D0.A1.D1.82.D0.B0.D1.80.D1.8B.D0.B5_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B8_Xorg)
    *   [5.5 Поврежденный экран: проблема "Шести экранов"](#.D0.9F.D0.BE.D0.B2.D1.80.D0.B5.D0.B6.D0.B4.D0.B5.D0.BD.D0.BD.D1.8B.D0.B9_.D1.8D.D0.BA.D1.80.D0.B0.D0.BD:_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D0.B0_.22.D0.A8.D0.B5.D1.81.D1.82.D0.B8_.D1.8D.D0.BA.D1.80.D0.B0.D0.BD.D0.BE.D0.B2.22)
    *   [5.6 '/dev/nvidia0' input/output error](#.27.2Fdev.2Fnvidia0.27_input.2Foutput_error)
    *   [5.7 Ошибки '/dev/nvidiactl'](#.D0.9E.D1.88.D0.B8.D0.B1.D0.BA.D0.B8_.27.2Fdev.2Fnvidiactl.27)
    *   [5.8 Не запускаются 32-битные приложения](#.D0.9D.D0.B5_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA.D0.B0.D1.8E.D1.82.D1.81.D1.8F_32-.D0.B1.D0.B8.D1.82.D0.BD.D1.8B.D0.B5_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F)
    *   [5.9 Ошибки после обновления ядра](#.D0.9E.D1.88.D0.B8.D0.B1.D0.BA.D0.B8_.D0.BF.D0.BE.D1.81.D0.BB.D0.B5_.D0.BE.D0.B1.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D1.8F_.D1.8F.D0.B4.D1.80.D0.B0)
    *   [5.10 Crashing in general](#Crashing_in_general)
    *   [5.11 Bad performance after installing a new driver version](#Bad_performance_after_installing_a_new_driver_version)
    *   [5.12 CPU spikes with 400 series cards](#CPU_spikes_with_400_series_cards)
    *   [5.13 Laptops: X hangs on login/out, worked around with Ctrl+Alt+Backspace](#Laptops:_X_hangs_on_login.2Fout.2C_worked_around_with_Ctrl.2BAlt.2BBackspace)
    *   [5.14 No screens found on a laptop/NVIDIA Optimus](#No_screens_found_on_a_laptop.2FNVIDIA_Optimus)
        *   [5.14.1 Possible Workaround](#Possible_Workaround)
    *   [5.15 Screen(s) found, but none have a usable configuration](#Screen.28s.29_found.2C_but_none_have_a_usable_configuration)
    *   [5.16 Blackscreen at X startup with new driver](#Blackscreen_at_X_startup_with_new_driver)
    *   [5.17 Backlight is not turning off in some occasions](#Backlight_is_not_turning_off_in_some_occasions)
    *   [5.18 Blue tint on videos with Flash](#Blue_tint_on_videos_with_Flash)
    *   [5.19 Bleeding overlay with Flash](#Bleeding_overlay_with_Flash)
    *   [5.20 Full system freeze using Flash](#Full_system_freeze_using_Flash)
    *   [5.21 Xorg fails to load or Red Screen of Death](#Xorg_fails_to_load_or_Red_Screen_of_Death)
    *   [5.22 Black screen on systems with Intel integrated GPU](#Black_screen_on_systems_with_Intel_integrated_GPU)
    *   [5.23 Black screen on systems with VIA integrated GPU](#Black_screen_on_systems_with_VIA_integrated_GPU)
    *   [5.24 X fails with "no screens found" with Intel iGPU](#X_fails_with_.22no_screens_found.22_with_Intel_iGPU)
    *   [5.25 Xorg fails during boot, but otherwise starts fine](#Xorg_fails_during_boot.2C_but_otherwise_starts_fine)
    *   [5.26 Flash video players crashes](#Flash_video_players_crashes)
    *   [5.27 Override EDID](#Override_EDID)
    *   [5.28 Fix rendering lag (firefox, gedit, vim, tmux …)](#Fix_rendering_lag_.28firefox.2C_gedit.2C_vim.2C_tmux_.E2.80.A6.29)
    *   [5.29 Screen Tearing with Multiple Monitor Orientations](#Screen_Tearing_with_Multiple_Monitor_Orientations)
*   [6 See also](#See_also)

## Установка

Данная инструкция предназначена для предоставляемых в дистрибутиве пакетов ядра [linux](https://www.archlinux.org/packages/?name=linux) или [linux-lts](https://www.archlinux.org/packages/?name=linux-lts). Для пользователей ядра, собранного самостоятельно, следует обратится к [следующему](#.D0.90.D0.BB.D1.8C.D1.82.D0.B5.D1.80.D0.BD.D0.B0.D1.82.D0.B8.D0.B2.D0.BD.D0.B0.D1.8F_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0:_.D1.81.D0.BE.D0.B1.D1.81.D1.82.D0.B2.D0.B5.D0.BD.D0.BD.D0.BE.D0.B5_.D1.8F.D0.B4.D1.80.D0.BE) подразделу.

**Важно:** Избегайте установки пакета драйвера NVIDIA, предоставляемого веб-сайтом NVIDIA. Установка через [pacman](/index.php/Pacman "Pacman"), позволяет обновлять драйвер вместе с остальной системой.

1\. Если вы не знаете модель графической карты, установленной у вас, для поиска используйте данный запрос:

	 `$ lspci -k | grep -A 2 -E "(VGA|3D)"` 

2\. Есть несколько вариантов определения необходимой для вас версии драйвера:

*   поиск по кодовому имени (т.к. NV50, NVC0, и др.) на [странице с кодовыми именами nouveau](http://nouveau.freedesktop.org/wiki/CodeNames)
*   просмотр модели в [списке устаревших графических карт](http://www.nvidia.com/object/IO_32667.html) NVIDIA: если вашей карты нет в списке, используйте драйвер для нового оборудования
*   также можно посетить [страницу загрузки драйвера с сайта](http://www.nvidia.com/Download/index.aspx) NVIDIA

3\. Установите подходящий драйвер для своей карты:

*   Для карт GeForce 400 series и более новых [NVCx и новее], установите (см. [install](/index.php/Install "Install")) пакет [nvidia](https://www.archlinux.org/packages/?name=nvidia) или пакет [nvidia-lts](https://www.archlinux.org/packages/?name=nvidia-lts) вместе с пакетом [nvidia-libgl](https://www.archlinux.org/packages/?name=nvidia-libgl).
*   Для карт GeForce 8000/9000 и 100-300 series [NV5x, NV8x, NV9x и NVAx] года производства 2006-2010, установите (см. [install](/index.php/Install "Install")) пакет [nvidia-340xx](https://www.archlinux.org/packages/?name=nvidia-340xx) или пакет [nvidia-340xx-lts](https://www.archlinux.org/packages/?name=nvidia-340xx-lts) вместе с пакетом [nvidia-340xx-libgl](https://www.archlinux.org/packages/?name=nvidia-340xx-libgl).
*   Для карт GeForce 6000/7000 series [NV4x и NV6x] года производства 2004-2006, установите (см. [install](/index.php/Install "Install")) пакет [nvidia-304xx](https://www.archlinux.org/packages/?name=nvidia-304xx) или пакет [nvidia-304xx-lts](https://www.archlinux.org/packages/?name=nvidia-304xx-lts) вместе с пакетом [nvidia-304xx-libgl](https://www.archlinux.org/packages/?name=nvidia-304xx-libgl).

*   Для более старых моделей, обратитесь к подразделу [#Неподдерживаемые драйвера](#.D0.9D.D0.B5.D0.BF.D0.BE.D0.B4.D0.B4.D0.B5.D1.80.D0.B6.D0.B8.D0.B2.D0.B0.D0.B5.D0.BC.D1.8B.D0.B5_.D0.B4.D1.80.D0.B0.D0.B9.D0.B2.D0.B5.D1.80.D0.B0).
*   Для очень новых моделей графических ускорителей может потребоваться установка (см. [install](/index.php/Install "Install")) пакета [nvidia-beta](https://aur.archlinux.org/packages/nvidia-beta/), т.к. стабильная версия драйвера может не поддерживать новые функции, добавленные в эти карты.

4\. Если у вас разрядность ОС 64-бит и вам необходима поддержка OpenGL 32-бит,то необходимо установить соответствующие пакеты *lib32* с репозитория [multilib](/index.php/Multilib "Multilib") (т.к. [lib32-nvidia-libgl](https://www.archlinux.org/packages/?name=lib32-nvidia-libgl), [lib32-nvidia-340xx-libgl](https://www.archlinux.org/packages/?name=lib32-nvidia-340xx-libgl) или [lib32-nvidia-304xx-libgl](https://www.archlinux.org/packages/?name=lib32-nvidia-304xx-libgl)).

5\. Перезагрузите систему. Пакет [nvidia](https://www.archlinux.org/packages/?name=nvidia) содержит файл с чёрным списком для модуля *nouveau*, поэтому перезагрузка необходима.

После того, как драйвер будет установлен, можно перейти к разделу [#Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0).

### Неподдерживаемые драйвера

Если вы имеете карту GeForce 5 FX series или старее, Nvidia не поддерживает больше драйвера для вашей карты. Это означает, что эти драйвера [не поддерживают текущую версию Xorg](http://nvidia.custhelp.com/app/answers/detail/a_id/3142/). В вашем случае, проще использовать драйвер [nouveau](/index.php/Nouveau "Nouveau"), который поддерживает старые карты в текущей версии Xorg.

Однако, старые драйвера Nvidia пока ещё доступны и могут прдоставлять лучшую 3D производительность/стабильность если вы откатите версию Xorg:

*   Для карт GeForce 5 FX series [NV30-NV36], установите пакет [nvidia-173xx-dkms](https://aur.archlinux.org/packages/nvidia-173xx-dkms/). Последняя поддерживаемая версия Xorg 1.15.
*   Для карт GeForce 2/3/4 MX/Ti series [NV11, NV17-NV28], установите пакет [nvidia-96xx-dkms](https://aur.archlinux.org/packages/nvidia-96xx-dkms/). Последняя поддерживаемая версия Xorg 1.12.

**Совет:** Устаревшие драйвера nvidia-96xx-dkms и nvidia-173xx-dkms также можно установить с неофициального [репозитория [city]](http://pkgbuild.com/~bgyorgy/city.html). (Настоятельно рекомендуется использовать данный способ, который поможет избежать любых проблем с зависимостями после установки.)

### Альтернативная установка: собственное ядро

Прежде всего, очень хорошо понимать, как работает система ABS, путём прочтения некоторых статей об этом:

*   Основная статья о [ABS](/index.php/ABS "ABS")
*   Статья о [makepkg](/index.php/Makepkg "Makepkg")
*   Статья о [Creating packages](/index.php/Creating_packages "Creating packages")

Следующее небольшое руководство описывает процесс создания собственного пакета драйвера NVIDIA, используя [ABS](/index.php/ABS "ABS"):

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [abs](https://www.archlinux.org/packages/?name=abs) и сгенерируйте дерево:

```
# abs

```

Как обычный пользователь, сделайте временный каталог для создания нового пакета:

```
$ mkdir -p ~/abs

```

Сделайте копию каталога пакета `nvidia`:

```
$ cp -r /var/abs/extra/nvidia/ ~/abs/

```

Зайдите в временный каталог сборки `nvidia`:

```
$ cd ~/abs/nvidia

```

Теперь необходимо отредактировать файлы `nvidia.install` и `PKGBUILD`, они должны содержать правильные переменные версии ядра.

Когда запущено собственное ядро, узнайте версию и имя ядра:

```
$ uname -r

```

1.  В nvidia.install, замените переменную `EXTRAMODULES='extramodules-3.4-ARCH'` собственной версией ядра, например `EXTRAMODULES='extramodules-3.4.4'` или `EXTRAMODULES='extramodules-3.4.4-custom'` в зависимости от названия и версии вашего ядра. Сделайте эти изменения для всех найденых совпадений в этом файле.
2.  В PKGBUILD, измените переменную `_extramodules=extramodules-3.4-ARCH` на совпадающую с вашей версией ядра, как описано выше.
3.  Если вы установили параллельно несколько ядер (например собственное ядро и ядро -ARCH, предоставляемое по умолчанию), измените название в PKGBUILD `pkgname=nvidia` на уникальное, такое как nvidia-344 или nvidia-custom. Это позволяет ядрам использовать разные модули nvidia, собственный модуль nvidia будет иметь другое название пакета и не будет переписан оригинальным. Вам также понадобится закоментировать строку в `package()`, которая добавляет в чёрный список модуль nouveau в `/usr/lib/modprobe.d/nvidia.conf` (нет необходимости делать это снова).

Теперь выполните:

```
$ makepkg -ci

```

Ключ `-c` говорит makepkg очистить оставшиеся файлы после сборки пакета, ключ `-i` указывает makepkg автоматически выполнить запуск pacman для установки собранного пакета.

#### Автоматическая пересборка модуля NVIDIA при обновлении ядра

Это возможно благодаря пакету [nvidia-hook](https://aur.archlinux.org/packages/nvidia-hook/) с [AUR](/index.php/AUR "AUR"). Вам необходимо установить пакет с исходным кодом модуля: [nvidia-dkms](https://www.archlinux.org/packages/?name=nvidia-dkms). В *nvidia-hook*, автоматическая пересборка выполняется хуком `nvidia` в [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") принудительно, при обновлении пакета [linux-headers](https://www.archlinux.org/packages/?name=linux-headers). Вам необходимо добавить `nvidia` в раздел HOOKS файла `/etc/mkinitcpio.conf`.

Хук будет вызывать команду *dkms* для обновления модуля NVIDIA при обновлении версии вашего ядра.

**Примечание:**

*   Если вы используете данную функциональность **необходимо** наблюдать процесс установки пакета [linux](https://www.archlinux.org/packages/?name=linux) (или другого ядра). Хук nvidia будет сообщать вам, если что-то пойдет не так.
*   Если вы хотите это делать вручную, обратитесь к статье [Dynamic Kernel Module Support (Русский)#Использование](/index.php/Dynamic_Kernel_Module_Support_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5 "Dynamic Kernel Module Support (Русский)").

## Настройка

Вполне возможно, что после установки драйвера, вам будет не нужно создавать конфигурационные файлы для сервера Xorg. Вы можете запустить [тест](/index.php/Xorg#Running "Xorg") для проверки корректной работы сервера Xorg без файла конфигурации. Однако, может потребоваться создание конфигурационного файла (предпочтительно `/etc/X11/xorg.conf.d/20-nvidia.conf` поверх `/etc/X11/xorg.conf`) для дополнительной настройки. Это конфигурация может быть сгенерирована инструментом конфигурации NVIDIA Xorg или можно создать её вручную. Если создается вручную, это может быть минимальной конфигурацией (в том смысле, что она будет содержать базовые настройки сервера [Xorg](/index.php/Xorg "Xorg")), либо она может включать в себя ряд настроек, которые могут обоходить автоматически обнаруженные настройки Xorg или предварительно заданные настройки.

**Примечание:** Начиная с версии 1.8.x, Xorg использует разделение конфигурационных файлов в `/etc/X11/xorg.conf.d/` - проверьте раздел [advanced configuration](#Advanced:_20-nvidia.conf).

### Минимальная настройка

Базовый блок конфигурации в `20-nvidia.conf` (или устаревший блок в `xorg.conf`) должен выглядеть так:

 `/etc/X11/xorg.conf.d/20-nvidia.conf` 
```
Section "Device"
        Identifier "Nvidia Card"
        Driver "nvidia"
        VendorName "NVIDIA Corporation"
        Option "NoLogo" "true"
        #Option "UseEDID" "false"
        #Option "ConnectedMonitor" "DFP"
        # ...
EndSection

```

**Совет:** Если вы перешли с драйвера nouveau, удостоверьтесь, в том что вы удалили "`nouveau`" из `/etc/mkinitcpio.conf`. Дополнительно смотрите [Switching between NVIDIA and nouveau drivers](#Switching_between_NVIDIA_and_nouveau_drivers), если вы часто переключаетесь между открытым и закрытым драйвером.

### Автоматическая настройка

Пакет NVIDIA, включает в себя автоматический инструмент для создания файла конфигурации сервера Xorg (`xorg.conf`) и может быть запущен путем выполнения:

```
# nvidia-xconfig

```

Данная команда автоматически обнаруживает и создает (или изменяет, если было уже создано) конфигурацию `/etc/X11/xorg.conf`, в соответствии с текущим аппаратным обеспечением.

Если есть строка с указанием загрузки DRI, убедитесь, что она закомментирована:

```
#    Load        "dri"

```

Проверьте ещё раз `/etc/X11/xorg.conf`, убедитесь, что глубина по умолчанию, горизонтальная синхронизация, частота кадров и разрешение допустимы.

**Важно:** Это может не работать корректно с сервером Xorg версии 1.8

### Несколько мониторов

	*Смотрите [Multihead](/index.php/Multihead "Multihead") для получения основной информации*

#### Использование NVIDIA Settings

Вы можете использовать инструмент [nvidia-settings](https://www.archlinux.org/packages/?name=nvidia-settings) для настройки много-мониторной конфигурации. Этот метод использует закрытое програмнное обеспечение NVIDIA поставляемое с драйверами. Просто запустите `nvidia-settings` как root, затем настройте как вам надо и сохраните конфигурацию в `/etc/X11/xorg.conf.d/10-monitor.conf`.

#### ConnectedMonitor

Если драйвер не определил второй монитор, вы можете принудительно указать его с помощью опции ConnectedMonitor

 `/etc/X11/xorg.conf` 
```

Section "Monitor"
    Identifier     "Monitor1"
    VendorName     "Panasonic"
    ModelName      "Panasonic MICRON 2100Ex"
    HorizSync       30.0 - 121.0 # this monitor has incorrect EDID, hence Option "UseEDIDFreqs" "false"
    VertRefresh     50.0 - 160.0
    Option         "DPMS"
EndSection

Section "Monitor"
    Identifier     "Monitor2"
    VendorName     "Gateway"
    ModelName      "GatewayVX1120"
    HorizSync       30.0 - 121.0
    VertRefresh     50.0 - 160.0
    Option         "DPMS"
EndSection

Section "Device"
    Identifier     "Device1"
    Driver         "nvidia"
    Option         "NoLogo"
    Option         "UseEDIDFreqs" "false"
    Option         "ConnectedMonitor" "CRT,CRT"
    VendorName     "NVIDIA Corporation"
    BoardName      "GeForce 6200 LE"
    BusID          "PCI:3:0:0"
    Screen          0
EndSection

Section "Device"
    Identifier     "Device2"
    Driver         "nvidia"
    Option         "NoLogo"
    Option         "UseEDIDFreqs" "false"
    Option         "ConnectedMonitor" "CRT,CRT"
    VendorName     "NVIDIA Corporation"
    BoardName      "GeForce 6200 LE"
    BusID          "PCI:3:0:0"
    Screen          1
EndSection

```

Дублирование устройств с опцией `Screen` описывает использование сервером Xorg двух мониторов на одной карте без технологии `TwinView`. Учтите, что `nvidia-settings` будет вырезать любое упоминание опции `ConnectedMonitor`.

#### TwinView

Вы хотите только один большой экран вместо двух. Установите значение опции `TwinView` в `1`. Эта опция должна использоваться если вы хотите композитинга. Технология TwinView работает только на базе одной карты, когда все мониторы подключены к одной карте.

```
Option "TwinView" "1"

```

Пример конфигурцаии:

 `/etc/X11/xorg.conf.d/10-monitor.conf` 
```
Section "ServerLayout"
    Identifier     "TwinLayout"
    Screen         0 "metaScreen" 0 0
EndSection

Section "Monitor"
    Identifier     "Monitor0"
    Option         "Enable" "true"
EndSection

Section "Monitor"
    Identifier     "Monitor1"
    Option         "Enable" "true"
EndSection

Section "Device"
    Identifier     "Card0"
    Driver         "nvidia"
    VendorName     "NVIDIA Corporation"

    #refer to the link below for more information on each of the following options.
    Option         "HorizSync"          "DFP-0: 28-33; DFP-1 28-33"
    Option         "VertRefresh"        "DFP-0: 43-73; DFP-1 43-73"
    Option         "MetaModes"          "1920x1080, 1920x1080"
    Option         "ConnectedMonitor"   "DFP-0, DFP-1"
    Option         "MetaModeOrientation" "DFP-1 LeftOf DFP-0"
EndSection

Section "Screen"
    Identifier     "metaScreen"
    Device         "Card0"
    Monitor        "Monitor0"
    DefaultDepth    24
    Option         "TwinView" "True"
    SubSection "Display"
        Modes          "1920x1080"
    EndSubSection
EndSection

```

[Дополнительная информация о технологии TwinView (англ.)](ftp://download.nvidia.com/XFree86/Linux-x86/355.11/README/configtwinview.html).

Если вы имеете несколько карт, которые совместимы с технологией SLI, вы можете использовать несколько мониторов присоединённых к разным картам (пример: две карты в режиме SLI с подключением монитора на каждой карте). Опция "MetaModes" совместно с режимом SLI Mosaic позволяет это. Ниже указана конфигурация, которая работает для вышеупомянутого примера и безупречно запускает [GNOME](/index.php/GNOME "GNOME").

 `/etc/X11/xorg.conf.d/10-monitor.conf` 
```
Section "Device"
        Identifier      "Card A"
        Driver          "nvidia"
        BusID           "PCI:1:00:0"
EndSection

Section "Device"
        Identifier      "Card B"
        Driver          "nvidia"
        BusID           "PCI:2:00:0"
EndSection

Section "Monitor"
        Identifier      "Right Monitor"
EndSection

Section "Monitor"
        Identifier      "Left Monitor"
EndSection

Section "Screen"
        Identifier      "Right Screen"
        Device          "Card A"
        Monitor         "Right Monitor"
        DefaultDepth    24
        Option          "SLI" "Mosaic"
        Option          "Stereo" "0"
        Option          "BaseMosaic" "True"
        Option          "MetaModes" "GPU-0.DFP-0: 1920x1200+4480+0, GPU-1.DFP-0:1920x1200+0+0"
        SubSection      "Display"
                        Depth           24
        EndSubSection
EndSection

Section "Screen"
        Identifier      "Left Screen"
        Device          "Card B"
        Monitor         "Left Monitor"
        DefaultDepth    24
        Option          "SLI" "Mosaic"
        Option          "Stereo" "0"
        Option          "BaseMosaic" "True"
        Option          "MetaModes" "GPU-0.DFP-0: 1920x1200+4480+0, GPU-1.DFP-0:1920x1200+0+0"
        SubSection      "Display"
                        Depth           24
        EndSubSection
EndSection

Section "ServerLayout"
        Identifier      "Default"
        Screen 0        "Right Screen" 0 0
        Option          "Xinerama" "0"
EndSection
```

##### Ручная конфигурация из командной строки с использованием xrandr

Если вышеуказанные решения не сработали, вы можете использовать *автозапуск* вашего менеджера окон совместно с пакетом [xorg-xrandr](https://www.archlinux.org/packages/?name=xorg-xrandr).

Некоторые примеры работы с командой `xrandr`:

```
xrandr --output DVI-I-0 --auto --primary --left-of DVI-I-1

```

или:

```
xrandr --output DVI-I-1 --pos 1440x0 --mode 1440x900 --rate 75.0

```

Где:

*   `--output` используется для указания "монитора", к которому применяются опции.
*   `DVI-I-1` имя второго монитора.
*   `--pos` позиция второго монитора относительно первого.
*   `--mode` разрешение второго монитора.
*   `--rate` частота обновления (в Гц).

#### Режим Mosaic

Режим Mosaic единственный способ использовать более чем два монитора через несколько видеокарт с использованием композитинга. Ваш оконный менджер может распознать, а может и не распознать различия между мониторами.

##### Base Mosaic

Режим Base Mosaic работает с картами Geforce 8000 series или выше. Его нельзя включить через графический интерфейс nvidia-setting. Вы должны использовать команду `nvidia-xconfig`, либо отредактировать `xorg.conf` самостоятельно. Опция Metamodes должна быть указана. Следующий пример для четырёх DFP мониторов в конфигурации 2х2, каждый запущен в разрешении 1920x1024, по два подключенных DFP монитора на две карты:

```
$ nvidia-xconfig --base-mosaic --metamodes="GPU-0.DFP-0: 1920x1024+0+0, GPU-0.DFP-1: 1920x1024+1920+0, GPU-1.DFP-0: 1920x1024+0+1024, GPU-1.DFP-1: 1920x1024+1920+1024"

```

**Примечание:** Хотя в документации и указано конфигурация мониторов 2х2, Nvidia уменьшила данную возможность до трех мониторов в режиме Base Mosaic в 304 версии драйвера. Большее количество мониторов доступно в картах серии Quadro, а в обычных картах ограничение в три монитора. Как объяснение данного уменьшения озвучивается как "Паритетное свойство драйвера Windows". С сентября 2014, Windows не имеет ограничение на количество мониторов с той же самой версией драйвера. Это не ошибка, так задумано по дизайну архитектуры.

##### SLI Mosaic

Если вы имеете конфигурацию SLI и все графические ускорители серии Quadro FX 5800, Quadro Fermi или новее, тогда вы можете использовать режим SLI Mosaic. он можеть быть включен из графического интерфейса nvidia-settings или из командной строки:

```
$ nvidia-xconfig --sli=Mosaic --metamodes="GPU-0.DFP-0: 1920x1024+0+0, GPU-0.DFP-1: 1920x1024+1920+0, GPU-1.DFP-0: 1920x1024+0+1024, GPU-1.DFP-1: 1920x1024+1920+1024"

```

### Драйвер Persistence

Начиная с версии 319, Nvidia изменила порядок работы драйвера persistence, теперь он запускается как демон при загрузке. Смотрите раздел [драйвер Persistence (англ.)](http://docs.nvidia.com/deploy/driver-persistence/index.html) документации Nvidia, для получения детальной информации.

Для запуска демона persistence [разрешите](/index.php/Enable "Enable") `nvidia-persistenced.service`. Для использования вручную смотрите [документацию разработчика](http://docs.nvidia.com/deploy/driver-persistence/index.html#usage).

## Тонкая настройка

### Графический интерфейс: nvidia-settings

Пакет NVIDIA включает в себя программу `nvidia-settings`, которая позволяет настраивать различные параметры.

Для загрузки настроек при входе, запустите эту команду из терминала:

```
$ nvidia-settings --load-config-only

```

Метод автозапуска среды рабочего стола 'может' не сработать при загрузке nvidia-settings (KDE). Чтобы удостовериться, что настройки реально загружены, поместите команду в файл ~/.xinitrc (создайте сами, если его нет)

**Совет:** Иногда `~/.nvidia-settings-rc` может повреждаться. Если это произошло, сервер Xorg может не загрузится и нужно удалить файл для решения проблемы загрузки.

### Дополнительно: 20-nvidia.conf

Отредактируйте `/etc/X11/xorg.conf.d/20-nvidia.conf` и добавьте опции в нужные секции. Сервер Xorg необходимо перегрузить для применения любых изменений.

Смотрите [NVIDIA Accelerated Linux Graphics Driver README и Руководство по установке (англ.)](ftp://download.nvidia.com/XFree86/Linux-x86/355.11/README/README.txt) для получения дополнительной информации и опций.

#### Запрет логотипа при загрузке

Добавьте опцию `"NoLogo"` внутри секции `Device`:

```
Option "NoLogo" "1"

```

#### Переопределение обнаружения монитора

Опция `"ConnectedMonitor"` в секции `Device` позволяет переопределить обнаружение монитора при запуске X, что позволяет сэкономить время при загрузке. Доступные опции: `"CRT"` для аналоговых мониторов, `"DFP"` для цифровых мониторов и `"TV"` для телевизоров.

Следующая строка принуждает драйвер NVIDIA в обход проверки и определения использовать монитор как DFP:

```
Option "ConnectedMonitor" "DFP"

```

**Примечание:** Используйте "CRT" для все аналоговых соединений типа VGA 15-пин, даже если монитор тонкий. "DFP" предназначен только для цифровых подключений такие как DVI, HDMI и DisplayPort.

#### Включение контроля яркости

Добавьте в секцию `Device` строку:

```
Option "RegistryDwords" "EnableBrightnessControl=1"

```

Если контроль яркости не заработает после применения данной опции, попробуйте установить [nvidia-bl](https://aur.archlinux.org/packages/nvidia-bl/) или [nvidiabl](https://aur.archlinux.org/packages/nvidiabl/).

#### Включение SLI

**Важно:** По состоянию на Май 7, 2011, вы можете испытывать проблемы с производительностью видео в GNOME 3, после включения SLI.

Выдержка из [README](ftp://download.nvidia.com/XFree86/Linux-x86/355.11/README/xconfigoptions.html) драйвера NVIDIA Приложение B: *Данная опция контролирует рендеринг SLI в поддерживаемых конфигурациях.* Другими словами, в "поддерживаемых конфигурациях" обозначены компьютеры оборудованные материнской платой c сертифицированной поддержкой SLI и 2 или 3 графических процессора GeForce, также с сертифицированной поддержкой SLI. Смотрите [Зона SLI (англ.)](http://www.slizone.com/page/home.html) для получения подробной информации.

Найдем первый PCI Bus ID графического процессора, используя `lspci`:

 `$ lspci | grep VGA` 
```
03:00.0 VGA compatible controller: nVidia Corporation G92 [GeForce 8800 GTS 512] (rev a2)
05:00.0 VGA compatible controller: nVidia Corporation G92 [GeForce 8800 GTS 512] (rev a2)

```

Добавим BusID (3 в нашем случае) в секцию `Device`:

```
BusID "PCI:3:0:0"

```

**Примечание:** Формат написания очень важен. Значение BusID должно быть указано в таком формате `"PCI:<BusID>:0:0"`

Добавьте желаемое значение режима рендеринга SLI в секцию `Screen`:

```
Option "SLI" "AA"

```

Следущая таблица описывает доступные режимы рендеринга.

| Значение | Описание |
| 0, no, off, false, Single | Использовать только один графический процессор для рендеринга. |
| 1, yes, on, true, Auto | Включить SLI и позволить драйверу автоматически выбрать режим рендеринга. |
| AFR | Включить SLI и использовать режим поочередного рендеринга кадров. |
| SFR | Включить SLI и использовать режим разделённого рендеринга кадров. |
| AA | Включить SLI и использовать сглаживание SLI. Используйте в сочетании с полным сглаживанием сцены, для улучшения качества визуализации. |

Другой вариант, вы можете использовать утилиту `nvidia-xconfig` для вставки изменений в `xorg.conf` одной командой:

```
# nvidia-xconfig --busid=PCI:3:0:0 --sli=AA

```

Для проверки работы режима SLI в консольном режиме:

 `$ nvidia-settings -q all | grep SLIMode` 
```
  Attribute 'SLIMode' (arch:0.0): AA 
    'SLIMode' is a string attribute.
    'SLIMode' is a read-only attribute.
    'SLIMode' can use the following target types: X Screen.

```

**Важно:** После включения SLI ваша система может зависать/не отвечать после запуска Xorg. Желательно отключить менеджер входа до перезагрузки.

#### Включение разгона

**Важно:** Помните, что разгон может привести к повреждению оборудования и авторы этой страницы снимают с себя любую ответственность за повреждение оборудования, вся информация, в том числе и возможность разгона, указывается изготовителем в спецификации к оборудованию.

Разгон контролируется через опцию *Coolbits* в секции `Device`, позволяя использовать различные неподдерживаемые свойства:

```
Option "Coolbits" "*value*"

```

**Совет:** Опция *Coolbits* легко контролируется через *nvidia-xconfig*, которая может управлять файлами конфигурации Xorg: `# nvidia-xconfig --cool-bits=*value*` 

Значение *Coolbits* - сумма его составляющих битов в двоичной системе исчисления. Типы битов:

*   `1` (bit 0) - Включает возможность разгона для старых (до архитектуры Fermi) ядер, вкладка *Clock Frequencies* в *nvidia-settings*.
*   `2` (bit 1) - Когда бит установлен, драйвер "будет пытаться инициализировать режим SLI, когда используются два графических процессора с разным количеством видеопамяти".
*   `4` (bit 2) - Включает ручное управление охлаждением графического процессора вкладка *Thermal Monitor* в *nvidia-settings*.
*   `8` (bit 3) - Включает возможность разгона на вкладке *PowerMizer* в *nvidia-settings*. Доступна с версии 337.12 для архитектур Fermi и новее. [[1]](http://www.phoronix.com/scan.php?px=MTY1OTM&page=news_item)
*   `16` (bit 4) - Включает возможность повышения напряжения через параметры командной строки *nvidia-settings*. Доступна с версии 337.12 для архитектур Fermi и новее.[[2]](http://www.phoronix.com/scan.php?page=news_item&px=MTg0MDI)

Чтобы включить несколько свойств, сложите значения *Coolbits*. Например, чтобы включить возможности разгона и повышения напряжения для архитектуры Fermi, установите значение `Option "Coolbits" "24"`.

Документация по *Coolbits* находится в `/usr/share/doc/nvidia/html/xconfigoptions.html`. Последния онлайн-версия документации по *Coolbits* (версия драйвера 355.11) находится [тут (англ.)](ftp://download.nvidia.com/XFree86/Linux-x86/355.11/README/xconfigoptions.html).

**Примечание:** Также, возможно отредактировать и переписать BIOS графического процессора, используя DOS (предпочтительнее) или с использованием Win32 окружения с помощью [nvflash](http://www.mvktech.net/component/option,com_remository/Itemid,26/func,select/id,127/orderby,2/page,1/) и [NiBiTor 6.0](http://www.mvktech.net/component/option,com_remository/Itemid,26/func,select/id,135/orderby,2/page,1/). Преимущество данного способа в том, что вы можете поднять не только напряжение, но и повысить стабильность программных методов разгона, такие как Coolbits. [Руководство по модификации BIOS архитектуры Fermi (англ.)](http://ivanvojtko.blogspot.sk/2014/03/how-to-overclock-geforce-460gtx-fermi.html)

##### Настройка статического 2D/3D разгона

Установите следующую строку в секции `Device` для включения PowerMizer на максимальную производительность (VSync не будет работать без этой строки):

```
Option "RegistryDwords" "PerfLevelSrc=0x2222"

```

## Советы и подсказки

### Исправление разрешения терминала

Переход с драйвера nouveau будет сопровождаться низким разрешением экрана терминала при загрузке. Для загрузчика GRUB, обратитесь к [GRUB/Tips and tricks#Setting the framebuffer resolution](/index.php/GRUB/Tips_and_tricks#Setting_the_framebuffer_resolution "GRUB/Tips and tricks"), чтобы увеличить разрешение.

### Включение Pure Video HD (VDPAU/VAAPI)

**Аппаратные требования:**

Как миниум, видеокарта с вторым поколением PureVideo HD [wikipedia:Nvidia_PureVideo#Table_of_PureVideo_.28HD.29_GPUs](https://en.wikipedia.org/wiki/Nvidia_PureVideo#Table_of_PureVideo_.28HD.29_GPUs "wikipedia:Nvidia PureVideo").

**Программные требования:**

Видеокарты Nvidia с установленым проприетарным драйвером будут предоставлять декодирование видео, совместимое с интерфейсом VDPAU в различных вариантах, в зависимости от поколения PureVideo.

Вы можете также добавить поддержку интерфейса VA-API с помощью [libva-vdpau-driver](https://www.archlinux.org/packages/?name=libva-vdpau-driver).

Проверка подержки VA-API:

```
$ vainfo

```

Для получения всех преимуществ апаратного декодирования вашей видеокарты, вам необходим медиаплеер с поддержкой VDPAU или VA-API.

Для включения аппаратного ускорения в [MPlayer](/index.php/MPlayer "MPlayer") добавьте в `~/.mplayer/config`

```
vo=vdpau
vc=ffmpeg12vdpau,ffwmv3vdpau,ffvc1vdpau,ffh264vdpau,ffodivxvdpau,

```

**Важно:** Кодек `ffodivxvdpau` поддерживается только в последних сериях видеокарт NVIDIA. Данный пример рассматривается, без учета специфики вашего оборудования.

Для включения аппаратного ускорения в [VLC](/index.php/VLC "VLC") перейдите:

`Инструменты > Настройки > Ввод/кодеки`, теперь выберите `VDPAU` в меню `**Декодирование с аппаратным ускорением**`

Для включения аппаратного ускорения в **smplayer** перейдите:

`Настройки > Настройки > Основные > вкладка Видео`, теперь выберите `vdpau` в меню `**Устройство вывода**`

Для включения аппаратного ускорения в **gnome-mplayer** перейдите:

`Правка > Параметры`, теперь выберите в меню `**Вывод видео**` значение `vdpau`

**Просмотр HD видео на картах с малым количеством памяти:**

Если ваша видеокарта имеет мало памяти (>512MB?), вы можете столкнуться с глюками при просмотре видео в разрешениях 1080p или 720p. Чтобы этого избежать, запускайте простые менеджеры окон типа TWM или MWM.

Также может помочь увеличение размера кэша MPlayer в `~/.mplayer/config`, когда ваш жёсткий диск останавливается при просмотре HD видео.

### Избежание разрывов изображения (тьюринга) в KDE (KWin)

 `/etc/profile.d/kwin.sh` 
```
export __GL_YIELD="USLEEP"

```

Если вышеуказанная строка не поможет, попробуйте заменить на это:

 `/etc/profile.d/kwin.sh` 
```
export KWIN_TRIPLE_BUFFER=1

```

Не включайте обе вышеуказанные опции одновременно. Также, если вы включили тройную буферизацию, убедитесь что включена опция TripleBuffering в самом драйвере. Источник: [https://bugs.kde.org/show_bug.cgi?id=322060](https://bugs.kde.org/show_bug.cgi?id=322060)

### Аппартное ускорение декодирования видео с помощью XvMC

Ускорение декодирования видео MPEG-1 и MPEG-2 через [XvMC](/index.php/XvMC "XvMC") поддерживается на сериях видеокарт GeForce4, GeForce 5 FX, GeForce 6 и GeForce 7\. Чтобы использовать его, создайте новый файл `/etc/X11/XvMCConfig` с следующим содержимым:

```
libXvMCNVIDIA_dynamic.so.1

```

Смотрите примеры конфигураций [поддерживаемого програмного обеспечения](/index.php/XvMC#Supported_software "XvMC").

### Использование ТВ-выхода

Хорошая статья об этом есть [тут](http://en.wikibooks.org/wiki/NVidia/TV-OUT).

### X на ТВ (DFP) как основной экран

Сервер X откатывается к CRT-0, если нет автоматически определённого монитора. Это может стать проблемой при использовании подключения ТВ через DVI как основной монитор, и сервер X был запущен при выключенном ТВ или он был не подключен.

Для принудительного использования DFP драйвером NVIDIA, сохраните копию EDID в файловой системе там, где его сможет прочитать сервер X, вместо чтения EDID с ТВ/DFP.

Для получения EDID запустите nvidia-settings. Появится различная информация в древовидном формате, игнорируя все настройки выберите графический процессор (соответствующее поле должно называться "GPU-0" или быть похожим на него), щелкните по `DFP` секции (также возможно `DFP-0` или что-то похожее), нажмите на кнопку `Acquire Edid` и сохраните куда-нибудь, например в `/etc/X11/dfp0.edid`.

Если у вас не подключена мышь и клавиатура, EDID может быть получен из командной строки. Запустите сервер X с нужным логированием для вывода блока EDID:

```
$ startx -- -logverbose 6

```

После окончания иницализации сервера X закройте его, ваш лог файл сохранится в `/var/log/Xorg.0.log`. Извлеките блок EDID используя nvidia-xconfig:

```
$ nvidia-xconfig --extract-edids-from-file=/var/log/Xorg.0.log --extract-edids-output-file=/etc/X11/dfp0.bin

```

Отредактируйте `xorg.conf` добавив в секцию `Device` строки:

```
Option "ConnectedMonitor" "DFP"
Option "CustomEDID" "DFP-0:/etc/X11/dfp0.edid"

```

Опция `ConnectedMonitor` принуждает драйвер распознавать DFP так, как буд-то он подключен. `CustomEDID` предоставляет данные EDID для устройства и говорит, что при загрузке ТВ/DFP как бы был подключен во время процесса запуска X.

Таким образом, можно автоматически запускать менеджер экрана при загрузке, иметь рабочий и настроенный экран для X до включения питания ТВ.

Если вышеуказанные изменения не работают, в `xorg.conf` в секции `Device` вы можете попробовать удалить строку `Option "ConnectedMonitor" "DFP"` и добавить следующие строки:

```
Option "ModeValidation" "NoDFPNativeResolutionCheck"
Option "ConnectedMonitor" "DFP-0"

```

Опция драйвера NVIDIA `NoDFPNativeResolutionCheck` предотвращает отключение всех режимов, которые не подходят к основному разрешению.

### Проверка источника питания

Драйвер NVIDIA может также использовать графический процессор для определения источника питания. Чтобы увидеть текущий источник питания, проверьте параметр 'GPUPowerSource' (0 - сеть, 1 - батарея):

 `$ nvidia-settings -q GPUPowerSource -t`  `1` 

Если вы видите сообщение об ошибке похожее на то что указано ниже, тогда вам необходимо или установить [acpid](/index.php/Acpid "Acpid") или запустить systemd сервис `systemctl start acpid.service` если он уже установлен

```
ACPI: failed to connect to the ACPI event daemon; the daemon
may not be running or the "AcpidSocketPath" X
configuration option may not be set correctly. When the
ACPI event daemon is available, the NVIDIA X driver will
try to use it to receive ACPI event notifications. For
details, please see the "ConnectToAcpid" and
"AcpidSocketPath" X configuration options in Appendix B: X
Config Options in the README.

```

(Если вы не видите этой ошибки, вам нет необходимости ставить/запускать acpid. Источник питания должен определяться даже если не установлен acpid.)

### Отображение температуры графического процессора в оболочке

#### Метод 1 - nvidia-settings

**Примечание:** Данный метод требует наличия сервера X. Используйте второй или третий метод если X сервер вам не нужен. Также, третий метод не работает с новыми картами NVIDIA, такими как GeForce 200 series, и с интегрированными графическими решениями, такими как Zotac IONITX's 8800GS.

Для отображения температуры графического ядра в оболочке используйте `nvidia-settings` как указано ниже:

```
$ nvidia-settings -q gpucoretemp

```

Вывод должен быть примерно такой:

```
Attribute 'GPUCoreTemp' (hostname:0.0): 41.
'GPUCoreTemp' is an integer attribute.
'GPUCoreTemp' is a read-only attribute.
'GPUCoreTemp' can use the following target types: X Screen, GPU.

```

Температура графического процессора этой платы 41 °C.

Пример того, как получить значение температуры для использования в утилитах `rrdtool` или `conky` и др.:

 `$ nvidia-settings -q gpucoretemp -t`  `41` 

#### Метод 2 - nvidia-smi

`nvidia-smi` может читать температуру прямо с графического процессора без использования сервера X. Это важно для небольшой группы пользователей, которые не имеют запущенного сервера X, те, кто используют ОС для серверных приложений. Отображение температуры графического процессора с использованием nvidia-smi:

```
$ nvidia-smi

```

Пример вывода результата работы программы:

 `$ nvidia-smi` 
```
Fri Jan  6 18:53:54 2012       
+------------------------------------------------------+                       
| NVIDIA-SMI 2.290.10   Driver Version: 290.10         |                       
|-------------------------------+----------------------+----------------------+
| Nb.  Name                     | Bus Id        Disp.  | Volatile ECC SB / DB |
| Fan   Temp   Power Usage /Cap | Memory Usage         | GPU Util. Compute M. |
|===============================+======================+======================|
| 0\.  GeForce 8500 GT           | 0000:01:00.0  N/A    |       N/A        N/A |
|  30%   62 C  N/A   N/A /  N/A |  17%   42MB /  255MB |  N/A      Default    |
|-------------------------------+----------------------+----------------------|
| Compute processes:                                               GPU Memory |
|  GPU  PID     Process name                                       Usage      |
|=============================================================================|
|  0\.           ERROR: Not Supported                                          |
+-----------------------------------------------------------------------------+

```

Только температура:

 `$ nvidia-smi -q -d TEMPERATURE` 
```

==============NVSMI LOG==============

Timestamp                           : Sun Apr 12 08:49:10 2015
Driver Version                      : 346.59

Attached GPUs                       : 1
GPU 0000:01:00.0
    Temperature
        GPU Current Temp            : 52 C
        GPU Shutdown Temp           : N/A
        GPU Slowdown Temp           : N/A

```

Пример того, как получить значение температуры для использования в утилитах `rrdtool` или `conky` и др.:

 `$ nvidia-smi -q -d TEMPERATURE | awk '/GPU Current Temp/ {print $5}'`  `52` 

Ссылка на руководство: [http://www.question-defense.com/2010/03/22/gpu-linux-shell-temp-get-nvidia-gpu-temperatures-via-linux-cli](http://www.question-defense.com/2010/03/22/gpu-linux-shell-temp-get-nvidia-gpu-temperatures-via-linux-cli).

#### Метод 3 - nvclock

Используйте [nvclock](https://aur.archlinux.org/packages/nvclock/), который доступен в [AUR](/index.php/AUR "AUR").

**Примечание:** `nvclock` не может получить доступ к тепловому сенсору на картах NVIDIA новее Geforce 200 series.

Могут быть расхождения значений температуры между nvclock и nvidia-settings/nv-control. В соответствии с [этим сообщением](http://sourceforge.net/projects/nvclock/forums/forum/67426/topic/1906899) от автора (thunderbird) nvclock, значения выдаваемые nvclock более точные.

### Утсановка скорости вентилятора при входе

Вы можете выставить скорость вентилятора вашей графической карты с помощью консольного интерфейса *nvidia-settings*. Сначала убедитесь в том, что в вашем конфигурационом файле Xorg значения опции Coolbits установлены в `4`, `5` или `12` для архитектуры Ферми и выше в секции `Device` для включения управления скоростью вентилятора.

```
Option "Coolbits" "4"

```

**Примечание:** Для карт GeForce 400/500 series, на текущий момент, этот метод при входе не устанавливает скорость вентилятора. Также, этот метод только позволяет настраивать скорость вентилятора только для текущей сессии X через nvidia-settings.

Поместите следующую строку в ваш файл [xinitrc](/index.php/Xinitrc "Xinitrc") для управления вентилятором при запуске Xorg. Замените `*n*` на значение скорости вентилятора нужное вам в процентах.

```
nvidia-settings -a "[gpu:0]/GPUFanControlState=1" -a "[fan:0]/GPUCurrentFanSpeed=*n*"

```

Также вы можете указать и второй графический процессор, путем увеличения счетчика графического процесора и вентилятора.

```
nvidia-settings -a "[gpu:0]/GPUFanControlState=1" -a "[fan:0]/GPUCurrentFanSpeed=*n*" \
                -a "[gpu:1]/GPUFanControlState=1" -a  [fan:1]/GPUCurrentFanSpeed=*n*" &

```

Если вы ипользуете менеджер входа такой как GDM или KDM, вы можете создать файл настроек. Создайте `~/.config/autostart/nvidia-fan-speed.desktop` и вставьте следующий текст.Снова измените `*n*` на значение скорости вентилятора нужное вам в процентах.

```
[Desktop Entry]
Type=Application
Exec=nvidia-settings -a "[gpu:0]/GPUFanControlState=1" -a "[fan:0]/GPUCurrentFanSpeed=*n*"
X-GNOME-Autostart-enabled=true
Name=nvidia-fan-speed

```

**Примечание:** С версии драйвера 349.16, опция `GPUCurrentFanSpeed` заменена на `GPUTargetFanSpeed`. [[3]](https://devtalk.nvidia.com/default/topic/821563/linux/can-t-control-fan-speed-with-beta-driver-349-12/post/4526208/#4526208)

### Порядок установки/удаления при смене драйвера

Здесь указаны старый драйвер как nvidiaO и новый драйвер как nvidiaN.

*   удаляем nvidiaO
*   устанавливаем nvidia-libglN
*   устанавливаем nvidiaN
*   устанавливаем lib32-nvidia-libgl-N (если требуется)

### Переключение между драйверами NVIDIA и nouveau

Если вам необходимо переключение между драйверами, вы можете использовать следующий скрипт, запуская его от root (для всех подтверждений, отвечайте да):

```
#!/bin/bash
BRANCH= # Enter a branch if needed, i.e. -340xx or -304xx
NVIDIA=nvidia${BRANCH} # If no branch entered above this would be "nvidia"
NOUVEAU=xf86-video-nouveau

# Replace -R with -Rs to if you want to remove the unneeded dependencies
if [ $(pacman -Qqs ^mesa-libgl$) ]; then
    pacman -S $NVIDIA ${NVIDIA}-libgl # Add lib32-${NVIDIA}-libgl and ${NVIDIA}-lts if needed
    # pacman -R $NOUVEAU
elif [ $(pacman -Qqs ^${NVIDIA}$) ]; then
    pacman -S --needed $NOUVEAU mesa-libgl # Add lib32-mesa-libgl if needed
    pacman -R $NVIDIA # Add ${NVIDIA}-lts if needed
fi

```

### Как избежать разрывов/тьюринга на картах GeForce 500/600/700/900 series

Разрывов можно избежать принудительным включением цепочки полного композитинга, независимо от используего вами композитора. Для проверки работоспособности опции, выполните

```
nvidia-settings --assign CurrentMetaMode="nvidia-auto-select +0+0 { ForceFullCompositionPipeline = On }"

```

Вам будет сообщено, что производительность некоторых приложений OpenGL может быть снижена.

Для постоянного использования сделанных изменений, вам необходимо добавить следующую строку в секцию `"Screen"` вашего конфигурационного файла Xorg, например `/etc/X11/xorg.conf.d/20-nvidia.conf`:

```
Option  "metamodes" "nvidia-auto-select +0+0 { ForceFullCompositionPipeline = On }"

```

Если у вас нет конфигурационного файла Xorg, вы можете создать его для текущей видеокарты исполльзуя `nvidia-xconfig` (смотрите [#Автоматическая настройка](#.D0.90.D0.B2.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B0.D1.8F_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)) и переместить его из `/etc/X11/xorg.conf` в более удобное место `/etc/X11/xorg.conf.d/20-nvidia.conf`.

## Возможные проблемы

### Игры при использовании TwinView

В случае, если вы хотите играть в игры в полноэкранном режиме используя TwinView, вы должны учитывать, что игры распознают два экрана как один большой. С технической точки зрения это утверждение корректно (виртуальный размер экрана X из комбинации ваших экранов), скорее всего вы не захотите играть на двух экранах одновременно.

Для исправления данного поведния для SDL, попробуйте:

```
export SDL_VIDEO_FULLSCREEN_HEAD=1

```

Для OpenGL, добавьте подходящие режимы в ваш файл xorg.conf в секцию `Device` и перезапустите сервер X:

```
Option "Metamodes" "1680x1050,1680x1050; 1280x1024,1280x1024; 1680x1050,NULL; 1280x1024,NULL;"

```

Есть ещё другой способ который, может работать как отдельно, так и в сочетании с вышеупомянутым способом, это [запуск игр в разделеных серверах X](/index.php/Gaming#Starting_games_in_a_separate_X_server "Gaming").

### Вертикальная синхронизация при использовании TwinView

Если вы используете TwinView и вертикальную синхронизацию (опция "Sync to VBlank" в **nvidia-settings**), вы заметите, что только один экран снихронизируется должным образом, если у вас два одинаковых монитора. Несмотря на то, что **nvidia-settings** даёт возможность изменять какой экран должен быть синхронизирован (опция "Sync to this display device"), это не всегда работает. Как решение, добавьте следующие переменные окружения при загрузке, на пример в файл `/etc/profile`:

```
export __GL_SYNC_TO_VBLANK=1
export __GL_SYNC_DISPLAY_DEVICE=DFP-0
export __VDPAU_NVIDIA_SYNC_DISPLAY_DEVICE=DFP-0

```

Вы можете изменить `DFP-0` на нужный вам тип экрана (`DFP-0` это DVI порт и `CRT-0` это VGA порт).Вы можете найти идентификатор вашего монитора в **nvidia-settings**, секция "X Server XVideoSettings".

### Wayland (gdm) рушится после установки nvidia-libgl

В некоторых процессорах Intel устаревший микрокод может привести к нестабильности работы с Wayland когда установлен драйвер nvidia, вызывая крах gdm.

[Обновление микрокода](/index.php/Microcode#Updating_Microcode "Microcode") должно решить проблему.

### Старые настройки Xorg

При обновлении с предыдущей установки, пожалуйста удалите старые пути `/usr/X11R6/`, т.к. это может привести к проблемам при установки.

### Поврежденный экран: проблема "Шести экранов"

Некоторые пользователи, использующие GeForce GT 100M, могут столкнуться с повреждением экрана при запуске X, разделенным на 6 секций с ограниченным разрешением в 640x480\. Похожая проблема недавно была замечена с Quadro 2000 и мониторами высокого разрешения.

Для решения проблемы, укажите значение `NoTotalSizeCheck` режима проверки в разделе `Device`:

```
Section "Device"
 ...
 Option "ModeValidation" "NoTotalSizeCheck"
 ...
EndSection

```

### '/dev/nvidia0' input/output error

This error can occur for several different reasons, and the most common solution given for this error is to check for group/file permissions, which in almost every case is *not* the problem. The NVIDIA documentation does not talk in detail on what you should do to correct this problem but there are a few things that have worked for some people. The problem can be a IRQ conflict with another device or bad routing by either the kernel or your BIOS.

First thing to try is to remove other video devices such as video capture cards and see if the problem goes away. If there are too many video processors on the same system it can lead into the kernel being unable to start them because of memory allocation problems with the video controller. In particular on systems with low video memory this can occur even if there is only one video processor. In such case you should find out the amount of your system's video memory (e.g. with `lspci -v`) and pass allocation parameters to the kernel, e.g. for a 32-bit kernel:

```
vmalloc=384M

```

If running a 64bit kernel, a driver defect can cause the NVIDIA module to fail initializing when IOMMU is on. Turning it off in the BIOS has been confirmed to work for some users. [[4]](http://www.nvnews.net/vbulletin/showthread.php?s=68bb2fabadcb53b10b286aa42d13c5bc&t=159335)[User:Clickthem#nvidia module](/index.php/User:Clickthem#nvidia_module "User:Clickthem")

Another thing to try is to change your BIOS IRQ routing from `Operating system controlled` to `BIOS controlled` or the other way around. The first one can be passed as a kernel parameter:

```
PCI=biosirq

```

The `noacpi` kernel parameter has also been suggested as a solution but since it disables ACPI completely it should be used with caution. Some hardware are easily damaged by overheating.

**Note:** The kernel parameters can be passed either through the kernel command line or the bootloader configuration file. See your bootloader Wiki page for more information.

### Ошибки '/dev/nvidiactl'

При запуске OpenGL приложений может возникнуть ошибка:

```
Error: Could not open /dev/nvidiactl because the permissions are too
restrictive. Please see the `FREQUENTLY ASKED QUESTIONS` 
section of `/usr/share/doc/NVIDIA_GLX-1.0/README` 
for steps to correct.

```

Решением, будет добавление нужного пользователя в группу `video`, после этот нужно перезайти:

```
# gpasswd -a username video

```

### Не запускаются 32-битные приложения

В 64-битных системах, установка пакета `lib32-nvidia-libgl`, который имеет ту же версию, что и установленный 64-битный драйвер решит проблему.

### Ошибки после обновления ядра

Если вы используете самосборный модуль NVIDIA вместо пакета из репозитория *extra*, то требуется пересборка пакета каждый раз после обновления ядра. Рекомендуется перезагрузка после обновления ядра и графических драйверов.

### Crashing in general

*   Try disabling `RenderAccel` in xorg.conf.
*   If Xorg outputs an error about "conflicting memory type" or "failed to allocate primary buffer: out of memory", add `nopat` at the end of the `kernel` line in `/boot/grub/menu.lst`.
*   If the NVIDIA compiler complains about different versions of GCC between the current one and the one used for compiling the kernel, add in `/etc/profile`:

```
export IGNORE_CC_MISMATCH=1

```

*   If Xorg is crashing with a "Signal 11" while using nvidia-96xx drivers, try disabling PAT. Pass the argument `nopat` to [kernel parameters](/index.php/Kernel_parameters "Kernel parameters").

More information about troubleshooting the driver can be found in the [NVIDIA forums.](https://forums.geforce.com/)

### Bad performance after installing a new driver version

If FPS have dropped in comparison with older drivers, first check if direct rendering is turned on (glxinfo is included in [mesa-demos](https://www.archlinux.org/packages/?name=mesa-demos)):

```
$ glxinfo | grep direct

```

If the command prints:

```
direct rendering: No

```

then that could be an indication for the sudden FPS drop.

A possible solution could be to regress to the previously installed driver version and rebooting afterwards.

### CPU spikes with 400 series cards

If you are experiencing intermittent CPU spikes with a 400 series card, it may be caused by PowerMizer constantly changing the GPU's clock frequency. Switching PowerMizer's setting from Adaptive to Performance, add the following to the `Device` section of your Xorg configuration:

```
 Option "RegistryDwords" "PowerMizerEnable=0x1; PerfLevelSrc=0x3322; PowerMizerDefaultAC=0x1"

```

### Laptops: X hangs on login/out, worked around with Ctrl+Alt+Backspace

If, while using the legacy NVIDIA drivers, Xorg hangs on login and logout (particularly with an odd screen split into two black and white/gray pieces), but logging in is still possible via `Ctrl+Alt+Backspace` (or whatever the new "kill X" key binding is), try adding this in `/etc/modprobe.d/modprobe.conf`:

```
options nvidia NVreg_Mobile=1

```

One user had luck with this instead, but it makes performance drop significantly for others:

```
options nvidia NVreg_DeviceFileUID=0 NVreg_DeviceFileGID=33 NVreg_DeviceFileMode=0660 NVreg_SoftEDIDs=0 NVreg_Mobile=1

```

Note that `NVreg_Mobile` needs to be changed according to the laptop:

*   1 for Dell laptops.
*   2 for non-Compal Toshiba laptops.
*   3 for other laptops.
*   4 for Compal Toshiba laptops.
*   5 for Gateway laptops.

See [NVIDIA Driver's README: Appendix K](ftp://download.nvidia.com/XFree86/Linux-x86/355.11/README/README.txt) for more information.

### No screens found on a laptop/NVIDIA Optimus

On a laptop, if the NVIDIA driver cannot find any screens, you may have an NVIDIA Optimus setup : an Intel chipset connected to the screen and the video outputs, and a NVIDIA card that does all the hard work and writes to the chipset's video memory.

Check if `$ lspci | grep VGA` outputs something similar to:

```
00:02.0 VGA compatible controller: Intel Corporation Core Processor Integrated Graphics Controller (rev 02)
01:00.0 VGA compatible controller: nVidia Corporation Device 0df4 (rev a1)

```

NVIDIA drivers now offer Optimus support since 319.12 Beta [[5]](http://www.nvidia.com/object/linux-display-amd64-319.12-driver.html) with kernels above and including 3.9.

Another solution is to install the [Intel](/index.php/Intel "Intel") driver to handle the screens, then if you want 3D software you should run them through [Bumblebee](/index.php/Bumblebee "Bumblebee") to tell them to use the NVIDIA card.

#### Possible Workaround

Enter the BIOS and changed the default graphics setting from 'Optimus' to 'Discrete' and the install NVIDIA drivers (295.20-1 at time of writing) recognized the screens.

Steps:

1.  Enter BIOS.
2.  Find Graphics Settings (should be in tab *Config > Display*).
3.  Change 'Graphics Device' to 'Discrete Graphics' (Disables Intel integrated graphics).
4.  Change OS Detection for Nvidia Optimus to "Disabled".
5.  Save and exit.

Tested on a Lenovo W520 with a Quadro 1000M and Nvidia Optimus

### Screen(s) found, but none have a usable configuration

Sometimes NVIDIA and X have trouble finding the active screen. If your graphics card has multiple outputs try plugging your monitor into the other ones. On a laptop it may be because your graphics card has vga/tv outs. Xorg.0.log will provide more info.

Another thing to try is adding invalid `"ConnectedMonitor" Option` to `Section "Device"` to force Xorg throws error and shows you how correct it. [Here](ftp://download.nvidia.com/XFree86/Linux-x86/355.11/README/xconfigoptions.html) more about ConnectedMonitor setting.

After re-run X see Xorg.0.log to get valid CRT-x,DFP-x,TV-x values.

`nvidia-xconfig --query-gpu-info` could be helpful.

### Blackscreen at X startup with new driver

If you have installed an update of Nvidia and you screen stay black after launching Xorg. You have to use the `rcutree.rcu_idle_gp_delay=1` [kernel parameter](/index.php/Kernel_parameter "Kernel parameter").

You can also try to add the `nvidia` module directly to your [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") config file.

If the screen still stays black with **both** the `rcutree.rcu_idle_gp_delay=1` [kernel parameter](/index.php/Kernel_parameter "Kernel parameter") and the `nvidia` module directly in the [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") config file, try re-installing [nvidia](https://www.archlinux.org/packages/?name=nvidia) and [nvidia-libgl](https://www.archlinux.org/packages/?name=nvidia-libgl) in that order, and finally reload the driver:

```
# modprobe nvidia

```

### Backlight is not turning off in some occasions

By default, DPMS should turn off backlight with the timeouts set or by running xset. However, probably due to a bug in the proprietary Nvidia drivers the result is a blank screen with no powersaving whatsoever. To workaround it, until the bug has been fixed you can use the `vbetool` as root.

Install the [vbetool](https://www.archlinux.org/packages/?name=vbetool) package.

Turn off your screen on demand and then by pressing a random key backlight turns on again:

```
vbetool dpms off && read -n1; vbetool dpms on

```

Alternatively, xrandr is able to disable and re-enable monitor outputs without requiring root.

```
xrandr --output DP-1 --off; read -n1; xrandr --output DP-1 --auto

```

### Blue tint on videos with Flash

A problem with [flashplugin](https://www.archlinux.org/packages/?name=flashplugin) versions 11.2.202.228-1 and 11.2.202.233-1 causes it to send the U/V panes in the incorrect order resulting in a blue tint on certain videos. There are a few potential fixes for this bug:

1.  Install the latest [libvdpau](https://www.archlinux.org/packages/?name=libvdpau).
2.  Patch `vdpau_trace.so` with [this makepkg](https://bbs.archlinux.org/viewtopic.php?pid=1078368#p1078368).
3.  Right click on a video, select "Settings..." and uncheck "Enable hardware acceleration". Reload the page for it to take affect. Note that this disables GPU acceleration.
4.  [Downgrade](/index.php/Downgrade "Downgrade") the [flashplugin](https://www.archlinux.org/packages/?name=flashplugin) package to version 11.1.102.63-1 at most.
5.  Use [google-chrome](https://aur.archlinux.org/packages/google-chrome/) with the new Pepper API [chromium-pepper-flash](https://aur.archlinux.org/packages/chromium-pepper-flash/).
6.  Try one of the few Flash alternatives.

The merits of each are discussed in [this thread](https://bbs.archlinux.org/viewtopic.php?id=137877).

### Bleeding overlay with Flash

This bug is due to the incorrect colour key being used by the [flashplugin](https://www.archlinux.org/packages/?name=flashplugin) version 11.2.202.228-1 and causes the flash content to "leak" into other pages or solid black backgrounds. To avoid this problem simply install the latest [libvdpau](https://www.archlinux.org/packages/?name=libvdpau) or export `VDPAU_NVIDIA_NO_OVERLAY=1` within either your shell profile (E.g. `~/.bash_profile` or `~/.zprofile`) or `~/.xinitrc`

### Full system freeze using Flash

If you experience occasional full system freezes (only the mouse is moving) using flashplugin and get:

 `/var/log/errors.log` 
```
NVRM: Xid (0000:01:00): 31, Ch 00000007, engmask 00000120, intr 10000000

```

A possible workaround is to switch off Hardware Acceleration in Flash, setting

 `/etc/adobe/mms.cfg`  `EnableLinuxHWVideoDecode=0` 

Or, if you want to keep Hardware acceleration enabled, you may try to::

```
export VDPAU_NVIDIA_NO_OVERLAY=1

```

...before starting the browser. Note that this may introduce tearing.

### Xorg fails to load or Red Screen of Death

If you get a red screen and use GRUB disable the GRUB framebuffer by editing `/etc/default/grub` and uncomment GRUB_TERMINAL_OUTPUT. For more information see [GRUB](/index.php/GRUB#Disable_framebuffer "GRUB").

### Black screen on systems with Intel integrated GPU

If you have an Intel CPU with an integrated GPU (e.g. Intel HD 4000) and have installed the [nvidia](https://www.archlinux.org/packages/?name=nvidia) package, you may experience a black screen on boot, when changing virtual terminal, or when exiting an X session. This may be caused by a conflict between the graphics modules. This is solved by blacklisting the Intel GPU modules. Create the file `/etc/modprobe.d/blacklist.conf` and prevent the *i915* and *intel_agp* modules from loading on boot:

 `/etc/modprobe.d/blacklist.conf` 
```
install i915 /usr/bin/false
install intel_agp /usr/bin/false

```

### Black screen on systems with VIA integrated GPU

As above, blacklisting the *viafb* module may resolve conflicts with NVIDIA drivers:

 `/etc/modprobe.d/blacklist.conf` 
```
install viafb /usr/bin/false

```

### X fails with "no screens found" with Intel iGPU

Like above, if you have an Intel CPU with an integrated GPU and X fails to start with

```
[ 76.633] (EE) No devices detected.
[ 76.633] Fatal server error:
[ 76.633] no screens found

```

then you need to add your discrete card's BusID to your X configuration. Find it:

 `# lspci | grep VGA` 
```
00:02.0 VGA compatible controller: Intel Corporation Xeon E3-1200 v2/3rd Gen Core processor Graphics Controller (rev 09)
01:00.0 VGA compatible controller: NVIDIA Corporation GK107 [GeForce GTX 650] (rev a1)

```

then you fix it by adding it to the card's Device section in your X configuration. In my case:

 `/etc/X11/xorg.conf.d/10-nvidia.conf` 
```
Section "Device"
    Identifier     "Device0"
    Driver         "nvidia"
    VendorName     "NVIDIA Corporation"
    BusID          "PCI:1:0:0"
EndSection

```

Note how `01:00.0` is written as `1:0:0`.

### Xorg fails during boot, but otherwise starts fine

On very fast booting systems, systemd may attempt to start the display manager before the NVIDIA driver has fully initialized. You will see a message like the following in your logs only when Xorg runs during boot.

 `/var/log/Xorg.0.log` 
```
[     1.807] (EE) NVIDIA(0): Failed to initialize the NVIDIA kernel module. Please see the
[     1.807] (EE) NVIDIA(0):     system's kernel log for additional error messages and
[     1.808] (EE) NVIDIA(0):     consult the NVIDIA README for details.
[     1.808] (EE) NVIDIA(0):  *** Aborting ***
```

In this case you will need to establish an ordering dependency from the display manager to the DRI device. First create device units for DRI devices by creating a new udev rules file.

 `/etc/udev/rules.d/99-systemd-dri-devices.rules`  `ACTION=="add", KERNEL=="card*", SUBSYSTEM=="drm", TAG+="systemd"` 

Then create dependencies from the display manager to the device(s).

 `/etc/systemd/system/display-manager.service.d/10-wait-for-dri-devices.conf` 
```
[Unit]
Wants=dev-dri-card0.device
After=dev-dri-card0.device
```

If you have additional cards needed for the desktop then list them in Wants and After seperated by spaces.

### Flash video players crashes

If you are getting frequent crashes of Flash video players, try to switch off Hardware Acceleration:

 `/etc/adobe/mms.cfg`  `EnableLinuxHWVideoDecode=0` 

(This problem appeared after installing the proprietary nvidia driver, and was fixed by changing this setting.)

### Override EDID

If your monitor is providing wrong EDID information, the nvidia-driver will pick a very small solution. Nvidia's driver options change, this guide refers to nvidia 346.47-11.

Aside from manually setting modelines in the xorg config, you have to allow non-edid modes and disable edid in the device section:

 `/etc/X11/xorg.conf.d/10-monitor.conf` 
```
Section "Monitor"
    Identifier     "Monitor0"
    VendorName     "Unknown"
    ModelName      "Unknown"
    HorizSync       30-94
    VertRefresh     56-76
    DisplaySize    518.4 324.0
    Option         "DPMS"
    # 1920x1200 59.95 Hz (CVT 2.30MA-R) hsync: 74.04 kHz; pclk: 154.00 MHz
    Modeline "1920x1200R"  154.00  1920 1968 2000 2080  1200 1203 1209 1235 +hsync -vsync
EndSection

Section "Device"
    Identifier     "Device0"
    Driver         "nvidia"
    VendorName     "NVIDIA Corporation"
    Option         "UseEdidFreqs" "FALSE"
    Option         "UseEDID" "FALSE"
    Option         "ModeValidation" "AllowNonEdidModes"
EndSection

Section "Screen"
    Identifier     "Screen0"
    Device         "Device0"
    Monitor        "Monitor0"
    DefaultDepth    24
    SubSection     "Display"
        Depth       24
        Modes      "1920x1200R"
    EndSubSection
EndSection
```

### Fix rendering lag (firefox, gedit, vim, tmux …)

```
nvidia-settings -a InitialPixmapPlacement=0

```

[https://bugzilla.gnome.org/show_bug.cgi?id=728464](https://bugzilla.gnome.org/show_bug.cgi?id=728464)

### Screen Tearing with Multiple Monitor Orientations

When running multiple monitors in different orientations (through [Xrandr](/index.php/Xrandr "Xrandr") settings) such as portrait and landscape simultaneously, you may notice screen tearing in one of the orientations/monitors. Unfortunately, this issue is fixed by setting all monitors to the same orientation via [Xrandr](/index.php/Xrandr "Xrandr") settings

## See also

*   [NVIDIA User forums](https://forums.geforce.com/)
*   [Official README for NVIDIA drivers, all on one text page. Most Recent Driver Version as of September 7, 2015: 355.11.](ftp://download.nvidia.com/XFree86/Linux-x86/355.11/README/README.txt)
*   [README Appendix B. X Config Options, 355.11 (direct link)](ftp://download.nvidia.com/XFree86/Linux-x86/355.11/README/xconfigoptions.html)