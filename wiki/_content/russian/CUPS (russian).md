Ссылки по теме

*   [CUPS/Printer sharing (Русский)](/index.php/CUPS/Printer_sharing_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "CUPS/Printer sharing (Русский)")
*   [CUPS/Printer-specific problems](/index.php/CUPS/Printer-specific_problems "CUPS/Printer-specific problems")
*   [CUPS/Troubleshooting](/index.php/CUPS/Troubleshooting "CUPS/Troubleshooting")
*   [Samba (Русский)](/index.php/Samba_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Samba (Русский)")
*   [LPRng](/index.php/LPRng "LPRng")

**Состояние перевода:** На этой странице представлен перевод статьи [CUPS](/index.php/CUPS "CUPS"). Дата последней синхронизации: 19 августа 2017\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=CUPS&diff=0&oldid=485933).

	"*Common UNIX Printing System ([CUPS](https://en.wikipedia.org/wiki/ru:Common_UNIX_Printing_System "w:ru:Common UNIX Printing System"), общая UNIX система печати) - это кроссплатформенное решение для печати для всех UNIX систем. Оно основано на "Internet Printing Protocol" (IPP, интернет-протокол печати) и предоставляет полный спектр возможностей для печати для большинства Postscript и растровых принтеров. CUPS распространяется под GNU GPL....*"

Хотя существуют другие пакеты печати, такие как LPRNG, CUPS более популярен и довольно прост в использовании. Это система печати по умолчанию как в Arch Linux, так и во многих других Linux-дистрибутивах.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
    *   [1.1 Драйверы принтеров](#.D0.94.D1.80.D0.B0.D0.B9.D0.B2.D0.B5.D1.80.D1.8B_.D0.BF.D1.80.D0.B8.D0.BD.D1.82.D0.B5.D1.80.D0.BE.D0.B2)
        *   [1.1.1 Загрузка PPD для принтера](#.D0.97.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B0_PPD_.D0.B4.D0.BB.D1.8F_.D0.BF.D1.80.D0.B8.D0.BD.D1.82.D0.B5.D1.80.D0.B0)
*   [2 Настройка CUPS](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_CUPS)
    *   [2.1 Модули ядра](#.D0.9C.D0.BE.D0.B4.D1.83.D0.BB.D0.B8_.D1.8F.D0.B4.D1.80.D0.B0)
        *   [2.1.1 USB-принтеры](#USB-.D0.BF.D1.80.D0.B8.D0.BD.D1.82.D0.B5.D1.80.D1.8B)
        *   [2.1.2 Принтеры с параллельным портом](#.D0.9F.D1.80.D0.B8.D0.BD.D1.82.D0.B5.D1.80.D1.8B_.D1.81_.D0.BF.D0.B0.D1.80.D0.B0.D0.BB.D0.BB.D0.B5.D0.BB.D1.8C.D0.BD.D1.8B.D0.BC_.D0.BF.D0.BE.D1.80.D1.82.D0.BE.D0.BC)
        *   [2.1.3 Автозагрузка](#.D0.90.D0.B2.D1.82.D0.BE.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B0)
    *   [2.2 Демон CUPS](#.D0.94.D0.B5.D0.BC.D0.BE.D0.BD_CUPS)
    *   [2.3 Web-интерфейс и средства управления](#Web-.D0.B8.D0.BD.D1.82.D0.B5.D1.80.D1.84.D0.B5.D0.B9.D1.81_.D0.B8_.D1.81.D1.80.D0.B5.D0.B4.D1.81.D1.82.D0.B2.D0.B0_.D1.83.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D1.8F)
        *   [2.3.1 Администрирование CUPS](#.D0.90.D0.B4.D0.BC.D0.B8.D0.BD.D0.B8.D1.81.D1.82.D1.80.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_CUPS)
        *   [2.3.2 Удаленный доступ к веб-интерфейсу](#.D0.A3.D0.B4.D0.B0.D0.BB.D0.B5.D0.BD.D0.BD.D1.8B.D0.B9_.D0.B4.D0.BE.D1.81.D1.82.D1.83.D0.BF_.D0.BA_.D0.B2.D0.B5.D0.B1-.D0.B8.D0.BD.D1.82.D0.B5.D1.80.D1.84.D0.B5.D0.B9.D1.81.D1.83)
*   [3 Устранение проблем](#.D0.A3.D1.81.D1.82.D1.80.D0.B0.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [3.1 Проблемы в результате обновления](#.D0.9F.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D1.8B_.D0.B2_.D1.80.D0.B5.D0.B7.D1.83.D0.BB.D1.8C.D1.82.D0.B0.D1.82.D0.B5_.D0.BE.D0.B1.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D1.8F)
        *   [3.1.1 CUPS останавливается](#CUPS_.D0.BE.D1.81.D1.82.D0.B0.D0.BD.D0.B0.D0.B2.D0.BB.D0.B8.D0.B2.D0.B0.D0.B5.D1.82.D1.81.D1.8F)
        *   [3.1.2 Для всех заданий - "остановлено" ("stopped")](#.D0.94.D0.BB.D1.8F_.D0.B2.D1.81.D0.B5.D1.85_.D0.B7.D0.B0.D0.B4.D0.B0.D0.BD.D0.B8.D0.B9_-_.22.D0.BE.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.BE.22_.28.22stopped.22.29)
        *   [3.1.3 Для всех заданий - "Принтер не отвечает" ("The printer is not responding")](#.D0.94.D0.BB.D1.8F_.D0.B2.D1.81.D0.B5.D1.85_.D0.B7.D0.B0.D0.B4.D0.B0.D0.BD.D0.B8.D0.B9_-_.22.D0.9F.D1.80.D0.B8.D0.BD.D1.82.D0.B5.D1.80_.D0.BD.D0.B5_.D0.BE.D1.82.D0.B2.D0.B5.D1.87.D0.B0.D0.B5.D1.82.22_.28.22The_printer_is_not_responding.22.29)
        *   [3.1.4 Версия PPD не совместима с gutenprint](#.D0.92.D0.B5.D1.80.D1.81.D0.B8.D1.8F_PPD_.D0.BD.D0.B5_.D1.81.D0.BE.D0.B2.D0.BC.D0.B5.D1.81.D1.82.D0.B8.D0.BC.D0.B0_.D1.81_gutenprint)
    *   [3.2 USB-принтеры под CUPS 1.4.x](#USB-.D0.BF.D1.80.D0.B8.D0.BD.D1.82.D0.B5.D1.80.D1.8B_.D0.BF.D0.BE.D0.B4_CUPS_1.4.x)
        *   [3.2.1 Занесение в черный список usblp](#.D0.97.D0.B0.D0.BD.D0.B5.D1.81.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B2_.D1.87.D0.B5.D1.80.D0.BD.D1.8B.D0.B9_.D1.81.D0.BF.D0.B8.D1.81.D0.BE.D0.BA_usblp)
        *   [3.2.2 Определение устройства](#.D0.9E.D0.BF.D1.80.D0.B5.D0.B4.D0.B5.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D1.83.D1.81.D1.82.D1.80.D0.BE.D0.B9.D1.81.D1.82.D0.B2.D0.B0)
            *   [3.2.2.1 Устранение неполадок при определении устройств](#.D0.A3.D1.81.D1.82.D1.80.D0.B0.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BD.D0.B5.D0.BF.D0.BE.D0.BB.D0.B0.D0.B4.D0.BE.D0.BA_.D0.BF.D1.80.D0.B8_.D0.BE.D0.BF.D1.80.D0.B5.D0.B4.D0.B5.D0.BB.D0.B5.D0.BD.D0.B8.D0.B8_.D1.83.D1.81.D1.82.D1.80.D0.BE.D0.B9.D1.81.D1.82.D0.B2)
            *   [3.2.2.2 Загрузка прошивки (firmware)](#.D0.97.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B0_.D0.BF.D1.80.D0.BE.D1.88.D0.B8.D0.B2.D0.BA.D0.B8_.28firmware.29)
    *   [3.3 Остальное](#.D0.9E.D1.81.D1.82.D0.B0.D0.BB.D1.8C.D0.BD.D0.BE.D0.B5)
        *   [3.3.1 Устранение ошибок CUPS](#.D0.A3.D1.81.D1.82.D1.80.D0.B0.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BE.D1.88.D0.B8.D0.B1.D0.BE.D0.BA_CUPS)
        *   [3.3.2 Принтер HPLIP выдает ошибку "/usr/lib/cups/backend/hp failed"](#.D0.9F.D1.80.D0.B8.D0.BD.D1.82.D0.B5.D1.80_HPLIP_.D0.B2.D1.8B.D0.B4.D0.B0.D0.B5.D1.82_.D0.BE.D1.88.D0.B8.D0.B1.D0.BA.D1.83_.22.2Fusr.2Flib.2Fcups.2Fbackend.2Fhp_failed.22)
        *   [3.3.3 Настройка HPLIP выполнена, но принтер не работает](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_HPLIP_.D0.B2.D1.8B.D0.BF.D0.BE.D0.BB.D0.BD.D0.B5.D0.BD.D0.B0.2C_.D0.BD.D0.BE_.D0.BF.D1.80.D0.B8.D0.BD.D1.82.D0.B5.D1.80_.D0.BD.D0.B5_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.B0.D0.B5.D1.82)
        *   [3.3.4 hp-toolbox выдает ошибку "Unable to communicate with device" ("Невозможно соединиться с устройством")](#hp-toolbox_.D0.B2.D1.8B.D0.B4.D0.B0.D0.B5.D1.82_.D0.BE.D1.88.D0.B8.D0.B1.D0.BA.D1.83_.22Unable_to_communicate_with_device.22_.28.22.D0.9D.D0.B5.D0.B2.D0.BE.D0.B7.D0.BC.D0.BE.D0.B6.D0.BD.D0.BE_.D1.81.D0.BE.D0.B5.D0.B4.D0.B8.D0.BD.D0.B8.D1.82.D1.8C.D1.81.D1.8F_.D1.81_.D1.83.D1.81.D1.82.D1.80.D0.BE.D0.B9.D1.81.D1.82.D0.B2.D0.BE.D0.BC.22.29)
        *   [3.3.5 CUPS с принтером HP возвращает '"foomatic-rip" not available/stopped with status 3' ('"foomatic-rip" не используется/остановлен со статусом 3')](#CUPS_.D1.81_.D0.BF.D1.80.D0.B8.D0.BD.D1.82.D0.B5.D1.80.D0.BE.D0.BC_HP_.D0.B2.D0.BE.D0.B7.D0.B2.D1.80.D0.B0.D1.89.D0.B0.D0.B5.D1.82_.27.22foomatic-rip.22_not_available.2Fstopped_with_status_3.27_.28.27.22foomatic-rip.22_.D0.BD.D0.B5_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D1.83.D0.B5.D1.82.D1.81.D1.8F.2F.D0.BE.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD_.D1.81.D0.BE_.D1.81.D1.82.D0.B0.D1.82.D1.83.D1.81.D0.BE.D0.BC_3.27.29)
        *   [3.3.6 Завершение печати из-за ошибок авторизации](#.D0.97.D0.B0.D0.B2.D0.B5.D1.80.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D0.B5.D1.87.D0.B0.D1.82.D0.B8_.D0.B8.D0.B7-.D0.B7.D0.B0_.D0.BE.D1.88.D0.B8.D0.B1.D0.BE.D0.BA_.D0.B0.D0.B2.D1.82.D0.BE.D1.80.D0.B8.D0.B7.D0.B0.D1.86.D0.B8.D0.B8)
        *   [3.3.7 Неактивна кнопка Печать в диалогах приложений GNOME](#.D0.9D.D0.B5.D0.B0.D0.BA.D1.82.D0.B8.D0.B2.D0.BD.D0.B0_.D0.BA.D0.BD.D0.BE.D0.BF.D0.BA.D0.B0_.D0.9F.D0.B5.D1.87.D0.B0.D1.82.D1.8C_.D0.B2_.D0.B4.D0.B8.D0.B0.D0.BB.D0.BE.D0.B3.D0.B0.D1.85_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D0.B9_GNOME)
        *   [3.3.8 Не найдена поддержка формата: application/postscript](#.D0.9D.D0.B5_.D0.BD.D0.B0.D0.B9.D0.B4.D0.B5.D0.BD.D0.B0_.D0.BF.D0.BE.D0.B4.D0.B4.D0.B5.D1.80.D0.B6.D0.BA.D0.B0_.D1.84.D0.BE.D1.80.D0.BC.D0.B0.D1.82.D0.B0:_application.2Fpostscript)
        *   [3.3.9 Определение URIs для Windows Print Servers](#.D0.9E.D0.BF.D1.80.D0.B5.D0.B4.D0.B5.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_URIs_.D0.B4.D0.BB.D1.8F_Windows_Print_Servers)
        *   [3.3.10 Ошибка задания для печати client-error-document-format-not-supported](#.D0.9E.D1.88.D0.B8.D0.B1.D0.BA.D0.B0_.D0.B7.D0.B0.D0.B4.D0.B0.D0.BD.D0.B8.D1.8F_.D0.B4.D0.BB.D1.8F_.D0.BF.D0.B5.D1.87.D0.B0.D1.82.D0.B8_client-error-document-format-not-supported)
        *   [3.3.11 Не работает /usr/lib/cups/backend/hp](#.D0.9D.D0.B5_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.B0.D0.B5.D1.82_.2Fusr.2Flib.2Fcups.2Fbackend.2Fhp)
        *   [3.3.12 Принтер Samsung не печатает некоторые документы](#.D0.9F.D1.80.D0.B8.D0.BD.D1.82.D0.B5.D1.80_Samsung_.D0.BD.D0.B5_.D0.BF.D0.B5.D1.87.D0.B0.D1.82.D0.B0.D0.B5.D1.82_.D0.BD.D0.B5.D0.BA.D0.BE.D1.82.D0.BE.D1.80.D1.8B.D0.B5_.D0.B4.D0.BE.D0.BA.D1.83.D0.BC.D0.B5.D0.BD.D1.82.D1.8B)
        *   [3.3.13 Не отображается локальный USB-принтер](#.D0.9D.D0.B5_.D0.BE.D1.82.D0.BE.D0.B1.D1.80.D0.B0.D0.B6.D0.B0.D0.B5.D1.82.D1.81.D1.8F_.D0.BB.D0.BE.D0.BA.D0.B0.D0.BB.D1.8C.D0.BD.D1.8B.D0.B9_USB-.D0.BF.D1.80.D0.B8.D0.BD.D1.82.D0.B5.D1.80)
        *   [3.3.14 "Не удается получить список драйверов для принтеров"](#.22.D0.9D.D0.B5_.D1.83.D0.B4.D0.B0.D0.B5.D1.82.D1.81.D1.8F_.D0.BF.D0.BE.D0.BB.D1.83.D1.87.D0.B8.D1.82.D1.8C_.D1.81.D0.BF.D0.B8.D1.81.D0.BE.D0.BA_.D0.B4.D1.80.D0.B0.D0.B9.D0.B2.D0.B5.D1.80.D0.BE.D0.B2_.D0.B4.D0.BB.D1.8F_.D0.BF.D1.80.D0.B8.D0.BD.D1.82.D0.B5.D1.80.D0.BE.D0.B2.22)
*   [4 Приложение](#.D0.9F.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D0.B5)
    *   [4.1 Альтернативные интерфейсы CUPS](#.D0.90.D0.BB.D1.8C.D1.82.D0.B5.D1.80.D0.BD.D0.B0.D1.82.D0.B8.D0.B2.D0.BD.D1.8B.D0.B5_.D0.B8.D0.BD.D1.82.D0.B5.D1.80.D1.84.D0.B5.D0.B9.D1.81.D1.8B_CUPS)
    *   [4.2 Виртуальный PDF-принтер](#.D0.92.D0.B8.D1.80.D1.82.D1.83.D0.B0.D0.BB.D1.8C.D0.BD.D1.8B.D0.B9_PDF-.D0.BF.D1.80.D0.B8.D0.BD.D1.82.D0.B5.D1.80)
        *   [4.2.1 Печать в postscript: тонкости использования виртуального CUPS-PDF-принтера](#.D0.9F.D0.B5.D1.87.D0.B0.D1.82.D1.8C_.D0.B2_postscript:_.D1.82.D0.BE.D0.BD.D0.BA.D0.BE.D1.81.D1.82.D0.B8_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D1.8F_.D0.B2.D0.B8.D1.80.D1.82.D1.83.D0.B0.D0.BB.D1.8C.D0.BD.D0.BE.D0.B3.D0.BE_CUPS-PDF-.D0.BF.D1.80.D0.B8.D0.BD.D1.82.D0.B5.D1.80.D0.B0)
            *   [4.2.1.1 Настройка виртуального CUPS-PDF-принтера](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D0.B2.D0.B8.D1.80.D1.82.D1.83.D0.B0.D0.BB.D1.8C.D0.BD.D0.BE.D0.B3.D0.BE_CUPS-PDF-.D0.BF.D1.80.D0.B8.D0.BD.D1.82.D0.B5.D1.80.D0.B0)
    *   [4.3 Другие источники драйверов для принтеров](#.D0.94.D1.80.D1.83.D0.B3.D0.B8.D0.B5_.D0.B8.D1.81.D1.82.D0.BE.D1.87.D0.BD.D0.B8.D0.BA.D0.B8_.D0.B4.D1.80.D0.B0.D0.B9.D0.B2.D0.B5.D1.80.D0.BE.D0.B2_.D0.B4.D0.BB.D1.8F_.D0.BF.D1.80.D0.B8.D0.BD.D1.82.D0.B5.D1.80.D0.BE.D0.B2)
*   [5 Дополнение](#.D0.94.D0.BE.D0.BF.D0.BE.D0.BB.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5)
    *   [5.1 Особые случаи](#.D0.9E.D1.81.D0.BE.D0.B1.D1.8B.D0.B5_.D1.81.D0.BB.D1.83.D1.87.D0.B0.D0.B8)
        *   [5.1.1 Принтеры с параллельным портом HP (hplip)](#.D0.9F.D1.80.D0.B8.D0.BD.D1.82.D0.B5.D1.80.D1.8B_.D1.81_.D0.BF.D0.B0.D1.80.D0.B0.D0.BB.D0.BB.D0.B5.D0.BB.D1.8C.D0.BD.D1.8B.D0.BC_.D0.BF.D0.BE.D1.80.D1.82.D0.BE.D0.BC_HP_.28hplip.29)
        *   [5.1.2 Печать не работает/прерывается на принтерах HP Deskjet 700](#.D0.9F.D0.B5.D1.87.D0.B0.D1.82.D1.8C_.D0.BD.D0.B5_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.B0.D0.B5.D1.82.2F.D0.BF.D1.80.D0.B5.D1.80.D1.8B.D0.B2.D0.B0.D0.B5.D1.82.D1.81.D1.8F_.D0.BD.D0.B0_.D0.BF.D1.80.D0.B8.D0.BD.D1.82.D0.B5.D1.80.D0.B0.D1.85_HP_Deskjet_700)
        *   [5.1.3 Заставить работать HP LaserJet 1010](#.D0.97.D0.B0.D1.81.D1.82.D0.B0.D0.B2.D0.B8.D1.82.D1.8C_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.B0.D1.82.D1.8C_HP_LaserJet_1010)
        *   [5.1.4 Заставить работать HP LaserJet 1020 (1018 и похожие)](#.D0.97.D0.B0.D1.81.D1.82.D0.B0.D0.B2.D0.B8.D1.82.D1.8C_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.B0.D1.82.D1.8C_HP_LaserJet_1020_.281018_.D0.B8_.D0.BF.D0.BE.D1.85.D0.BE.D0.B6.D0.B8.D0.B5.29)
            *   [5.1.4.1 HPLIP](#HPLIP)
        *   [5.1.5 Выполнение сервисных операций на принтерах Epson](#.D0.92.D1.8B.D0.BF.D0.BE.D0.BB.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D1.81.D0.B5.D1.80.D0.B2.D0.B8.D1.81.D0.BD.D1.8B.D1.85_.D0.BE.D0.BF.D0.B5.D1.80.D0.B0.D1.86.D0.B8.D0.B9_.D0.BD.D0.B0_.D0.BF.D1.80.D0.B8.D0.BD.D1.82.D0.B5.D1.80.D0.B0.D1.85_Epson)
            *   [5.1.5.1 Escputil](#Escputil)
            *   [5.1.5.2 Mtink](#Mtink)
*   [6 См. также](#.D0.A1.D0.BC._.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [cups](https://www.archlinux.org/packages/?name=cups).

Для печати из приложений GTK3 вам потребуется дополнительно установить пакет [gtk3-print-backends](https://www.archlinux.org/packages/?name=gtk3-print-backends).

Если вы намерены "распечатать" документ PDF, тогда вам необходимо установить пакет [cups-pdf](https://www.archlinux.org/packages/?name=cups-pdf). По умолчанию файлы PDF хранятся в `/var/spool/cups-pdf/$USER`. Местоположение можно изменить в `/etc/cups/cups-pdf.conf`.

[Включите](/index.php/%D0%92%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D0%B5 "Включите") и [запустите](/index.php/%D0%97%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D0%B5 "Запустите") службу `org.cups.cupsd.service`.

### Драйверы принтеров

Выбор пакета с драйверами для принтера зависит от используемого вами принтера. Если вы не уверены, установите [gutenprint](https://www.archlinux.org/packages/?name=gutenprint).

*   [gutenprint](https://www.archlinux.org/packages/?name=gutenprint) - набор высококачественных драйверов для принтеров Canon, Epson, Lexmark, Sony, Olympus и PCL, использующихся с GhostSscript, CUPS, Foomatic и [GIMP](/index.php/List_of_applications/Multimedia_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A0.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B2.D0.B0.D1.8F_.D0.B3.D1.80.D0.B0.D1.84.D0.B8.D0.BA.D0.B0 "List of applications/Multimedia (Русский)")
*   [foomatic-db](https://www.archlinux.org/packages/?name=foomatic-db), [foomatic-db-engine](https://www.archlinux.org/packages/?name=foomatic-db-engine), [foomatic-db-nonfree](https://www.archlinux.org/packages/?name=foomatic-db-nonfree) и [foomatic-filters](https://www.archlinux.org/packages/?name=foomatic-filters) - система под управлением базы данных для интеграции открытых драйверов для принтера с обычными спулерами под Unix. Установка [foomatic-filters](https://www.archlinux.org/packages/?name=foomatic-filters) должна разрешить ваши проблемы, если в `error.log` от CUPS будут такие записи: "stopped with status 22!"
*   [foo2zjs](https://aur.archlinux.org/packages/foo2zjs/) - драйвер для принтеров, использующих протокол ZjStream, например таких, как HP Laserjet 1018\. Смотрите дополнительную информацию [здесь](http://foo2zjs.rkkda.com). Для использования Foo2zsj установите пакет [foo2zjs](https://aur.archlinux.org/packages/foo2zjs/)
*   [hplip](https://www.archlinux.org/packages/?name=hplip) - HP GNU/Linux драйвер. Обеспечивает поддержку DeskJet, OfficeJet, Photosmart, Business Inkjet и других принтеров моделей LaserJet, a также ряд принтеров Brother
*   [splix](https://www.archlinux.org/packages/?name=splix) - драйверы Samsung для принтеров SPL (Samsung Printer Language). Для USB принтеров, возможно, понадобится пакет [cups-usblp](https://aur.archlinux.org/packages/cups-usblp/)
*   [samsung-unified-driver](https://aur.archlinux.org/packages/samsung-unified-driver/) - универсальный драйвер для принтеров и сканеров Samsung. Неодходим, если вы используете новый принтер (например, ML-2160), для которого пока нет драйвера в [splix](https://www.archlinux.org/packages/?name=splix)
*   [ufr2](https://aur.archlinux.org/packages/ufr2/) или [cndrvcups-lb](https://aur.archlinux.org/packages/cndrvcups-lb/) - UFR2-драйвер для Canon, обеспечивающий поддержку принтеров серий LBP, iR и MF
*   [cups-pdf](https://www.archlinux.org/packages/?name=cups-pdf) - пакет, позволяющий настроить виртуальный PDF-принтер, который будет создавать PDF из всего, что на него отправят

Если вы не уверены в работоспособности драйвера вашего принтера или он не работает, возможно, стоит установить все доступные драйверы, поскольку для вашей модели принтера может подойти драйвер от другого производителя. Например, для Brother HL-2140 необходимо установить драйвер [hplip](https://www.archlinux.org/packages/?name=hplip).

#### Загрузка PPD для принтера

Так как CUPS в стандартной установке уже содержит множество файлов PPD (Postscript Printer Description), в зависимости от вашего принтера этот пункт является необязательным и может быть пропущен. Более того, в пакетах [foomatic-filters](https://www.archlinux.org/packages/?name=foomatic-filters), [gimp-print](https://www.archlinux.org/packages/?name=gimp-print) и [hplip](https://www.archlinux.org/packages/?name=hplip) уже имеется большое количество файлов PPD, которые будут автоматически определены CUPS.

Вот объяснение того, что такое PPD файл, с сайта Linux Printing:

	"*Для каждого PostScript принтера производитель предоставляет PPD-файл, содержащий всю уникальную информацию об этой модели принтера: основные возможности принтера (цветной он или нет, шрифты, уровень PostScript и т.д.) и особенно настройки, которые может изменять пользователь, такие как размер бумаги, разрешение печати и т.д.*"

Если в CUPS для вашего принтера отсутствует нужный PPD-файл, то:

*   Поищите пакеты для вашего принтера/производителя в [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)").
*   Посетите [базу данных OpenPrinting](http://www.openprinting.org/printers) и выберите своего производителя и модель принтера.
*   Поищите драйверы под GNU/Linux на сайте производителя.

**Примечание:** Поместите PPD файлы в `/usr/share/cups/model/`

# Настройка CUPS

Итак, после установки CUPS, у вас есть множество способов его настройки. Вы всегда можете использовать старую добрую командную строку. Некоторые DE, такие как GNOME и KDE, предоставляют удобные программы, которые могут вам помочь в управлении принтерами. Однако, для того чтобы сделать этот процесс максимально доступным обыкновенному пользователю, мы будем использовать web-интерфейс, предоставляемый CUPS.

Если планируется подключение не к локальному, а к сетевому принтеру, то, возможно, вначале стоит почитать о настройке [общего доступа к принтерам в CUPS](/index.php/CUPS_printer_sharing_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "CUPS printer sharing (Русский)"). Настройка общего доступа к принтерам внутри GNU/Linux довольно проста и имеет малое количество опций, а вот организация общего доступа к принтерам между Windows и GNU/Linux является немного более сложной.

### Модули ядра

Перед использованием веб-интерфейса CUPS, вам понадобится загрузить соответствующие модули ядра. Далее описаны шаги, взятые из руководства по установке принтера в Gentoo.

Данный раздел может понадобиться в зависимости от используемого ядра. После подключения принтера нужный модуль ядра может быть загружен автоматически. Воспользуйтесь командой `tail` (описана далее) для того, чтобы определить обнаружен ли принтер. Для просмотра загруженных модулей ядра также можно воспользоваться утилитой `lsmod`.

#### USB-принтеры

Для использования USB-принтера может потребоваться внести в черный список модуль `usblp`. Учтите, что насчет добавления `usblp` в черный список имеется некоторая [неопределенность](https://bbs.archlinux.org/viewtopic.php?pid=660601), так как некоторые USB-принтеры, в частности некоторые серии принтеров Canon и Epson, не определяются без этого модуля. Несколько пользователей принтеров Samsung, после добавления в черный список модуля `usblp`, сообщили о проблемах с `cups`, в качестве решения предлагается повторное включение модуля `usblp` и установка из [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)") пакета `cups-usblp` вместо стандартного пакета `cups` ([https://bbs.archlinux.org/viewtopic.php?pid=778104](https://bbs.archlinux.org/viewtopic.php?pid=778104)). С февраля 2012, ранее работавший с cups-usblp USB-принтер Samsung ML2010, работает с cups и внесением в черный список usblp.

Добавление модуля в черный список:

 `/etc/modprobe.d/blacklist.conf`  `blacklist usblp` 

либо создав в `/etc/modprobe.d/` свой файл, например `usblp_blacklist.conf`, со следующим содержимым:

 `/etc/modprobe.d/usblp_blacklist.conf`  `blacklist usblp` 

При использовании ядра собранного самостоятельно, возможно придется вручную загрузить модуль `usbcore`:

```
# modprobe usbcore

```

После загрузки всех необходимых модулей - включите принтер и проверьте обнаружен ли он ядром, для этого выполните следующее:

```
# tail /var/log/messages.log

```

или

```
# dmesg

```

При использовании `usblp`, сообщение об обнаружении принтера будет выглядеть примерно так:

```
Feb 19 20:17:11 kernel: printer.c: usblp0: USB Bidirectional
printer dev 2 if 0 alt 0 proto 2 vid 0x04E8 pid 0x300E
Feb 19 20:17:11 kernel: usb.c: usblp driver claimed interface cfef3920
Feb 19 20:17:11 kernel: printer.c: v0.13: USB Printer Device Class driver

```

Если `usblp` находится в черном списке, то будет выведено примерно следующее:

```
usb 3-2: new full speed USB device using uhci_hcd and address 3
usb 3-2: configuration #1 chosen from 1 choice

```

#### Принтеры с параллельным портом

Если вы желаете использовать принтер с параллельным портом, настройка в общем-то такая же, за исключением модулей:

```
# modprobe lp
# modprobe parport
# modprobe parport_pc

```

Еще раз проверьте настройки выполнив команду:

```
# tail /var/log/messages.log

```

Должно быть показано что-то вроде этого:

```
lp0: using parport0 (polling)

```

При использовании адаптера с USB на параллельный порт, CUPS не сможет обнаружить принтер. В качестве обходного пути - добавьте принтер используя другие типы соединений, а затем измените DeviceID в файле `/etc/cups/printers.conf`:

```
DeviceID = parallel:/dev/usb/lp0

```

#### Автозагрузка

Возможно, вам будет удобнее если соответствующий модуль будет загружен при старте системы. Для этого откройте в текстовом редакторе файл `/etc/[rc.conf](/index.php/Rc.conf "Rc.conf")`, и добавьте нужный модуль в строку `MODULES=()`. Например, так:

```
MODULES=(!usbserial scsi_mod sd_mod snd-ymfpci snd-pcm-oss **lp parport parport_pc** ide-scsi)

```

### Демон CUPS

После установки соответствующих модулей ядра, можно приступать к [запуску демона CUPS](/index.php/Daemon#Performing_daemon_actions_manually "Daemon"). Для автоматического запуска демона при старте системы следует добавить cupsd в [строку DAEMONS](/index.php/Daemons_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Daemons (Русский)").

### Web-интерфейс и средства управления

После запуска демона

```
# systemctl start org.cups.cupsd

```

откройте браузер и зайдите на: [http://localhost:631](http://localhost:631) (*Строку **localhost**, возможно, придется заменить на имя хоста из* `/etc/hosts`).

Теперь для добавления принтера можно использовать различные мастера. Для запуска обыкновенной процедуры установки кликните *Добавление принтеров и групп*, затем *Добавить принтер*. При запросе имени пользователя и пароля нужно будет войти в качестве root. Далее будет представлен список устройств для выбора. Фактическое имя принтера отображается рядом с меткой ( например, USB-принтеры напротив *USB Printer #1*). Принтеру можно присваивать любое имя, аналогично для пунктов 'Расположение' и 'Описание'. После выбора соответствующего драйвера настройки будут окончены.

Убедитесь в правильности настроек, нажав на кнопку *Print Test Page* (*Печать тестовой страницы*) в выпадающем меню *Maintenance* (*Обслуживание*). Если принтер не печатает, но вы уверены в правильности всех настроек, попытайтесь сменить драйвер принтера на другой.

**Tip:** Ознакомьтесь с другими программами в разделе [#Альтернативные интерфейсы CUPS](#.D0.90.D0.BB.D1.8C.D1.82.D0.B5.D1.80.D0.BD.D0.B0.D1.82.D0.B8.D0.B2.D0.BD.D1.8B.D0.B5_.D0.B8.D0.BD.D1.82.D0.B5.D1.80.D1.84.D0.B5.D0.B9.D1.81.D1.8B_CUPS).

**Примечание:** При установке USB-принтер должен отображаться в списке устройств на странице *Добавить принтер*. Если будет доступен только вариант "SCSI printer", то это означает, что CUPS не смог распознать ваш принтер.

#### Администрирование CUPS

При администрировании принтера через веб-интерфейс (например для: добавления или удаления принтеров, остановки заданий печати, и т.д) понадобятся имя пользователя и пароль. Пользователем по-умолчанию может быть пользователь из группы *sys* или root (для изменения измените значение в строке *SystemGroup* файла `/etc/cups/cupsd.conf`).

При заблокированной учетной записи root (т.е. используя sudo) будет невозможно войти в веб-интерфейс управления CUPS с именем пользователя по умолчанию и его паролем. В этом случае придерживайтесь [инструкций](http://www.cups.org/articles.php?L237+T+Qprintadmin) из CUPS FAQ. Дополнительно прочтите [это сообщение](https://bbs.archlinux.org/viewtopic.php?id=35567).

#### Удаленный доступ к веб-интерфейсу

По умолчанию, доступ к веб-интерфейсу CUPS разрешен только *localhost*; т.е. компьютеру на котором он установлен. Для разрешения удаленного доступа нужно внести следующие изменения в файл `/etc/cups/cupsd.conf`. Замените строку:

```
Listen localhost:631

```

на строку

```
Port 631

```

для того, чтобы CUPS мог слушать входящие запросы.

Можно предоставить три уровня доступа:

```
<Location />           #доступ к серверу
<Location /admin>	#доступ к странице администрирования
<Location /admin/conf>	#доступ к конфигурационным файлам

```

Для разрешения удаленного доступа к одному из уровней, добавьте параметр `Allow` в секцию соответствующую выбранному уровню. Параметр `Allow` может принимать одно или несколько из перечисленных ниже значений:

```
Allow all
Allow host.domain.com
Allow *.domain.com
Allow ip-address
Allow ip-address/netmask

```

Параметр также может быть использован для запрета. Например, если нужно дать полный доступ всем хостам подсети 192.168.1.0/255.255.255.0, файл `/etc/cups/cupsd.conf` должен содержать следующее:

```
# Ограничение доступа к серверу...
# По умолчанию возможны только локальные подключения
<Location />
   Order allow,deny
   Allow From localhost
   **Allow From 192.168.1.0/255.255.255.0**
</Location>

# Ограничение доступа к странице администрирования...
<Location /admin>
   # Encryption disabled by default
   #Encryption Required
   Order allow,deny
   Allow From localhost
   **Allow From 192.168.1.0/255.255.255.0**
</Location>

# Ограничение доступа к конфигурационным файлам...
<Location /admin/conf>
   AuthType Basic
   Require user @SYSTEM
   Order allow,deny
   Allow From localhost
   **Allow From 192.168.1.0/255.255.255.0**
</Location>

```

Также вам потребуется добавить:

```
DefaultEncryption Never

```

Для того, чтоб избежать получения ошибки: 426 - Upgrade Required when using the CUPS web interface from a remote machine.

# Устранение проблем

Наилучший способ борьбы с неисправностями - это выставить 'LogLevel' в файле `/etc/cups/cupsd.conf` в:

```
LogLevel debug

```

А потом посмотреть вывод из файла `/var/log/cups/error_log` например так:

```
# tail -n 100 -f /var/log/cups/error_log

```

Символы слева от вывода означают следующее:

*   D=Debug (отладка)
*   E=Error (ошибка)
*   I=Information (информация)
*   И так далее

Следующие файлы также могут быть полезны:

*   `/var/log/cups/page_log` - каждый раз при успешной печати, пишет новую запись
*   `/var/log/cups/access_log` - записывает всю активность на cupsd http1.1 сервере

Также, если вы хотите решить свои проблемы, важно понимать, как вообще работает CUPS. Вот краткая информация об этом:

1.  Когда вы жмёте 'печать' приложение отправляет .ps-файл (PostScript, язык-скрипт, который описывает, как выглядит страница) в систему CUPS (так происходит в большинстве программ).
2.  CUPS смотрит на PPD-файл (файл описания принтера) и находит, фильтры которые ему нужно использовать для преобразования .ps-файла в файл, который понимает ваш принтер (например, PJL,PCL). Обычно для этого ему требуется ghostscript.
3.  GhostScript принимает ввод и решает, какие фильтры ему использовать, потом применяет их и преобразовывает .ps-файл в формат, который понимает принтер.
4.  Затем файл передается бэкенду. Например, если у вас принтер подключен к usb порту, то используется usb бэкенд

### Проблемы в результате обновления

*Проблемы возникшие после обновления CUPS и сопутствующего ему набора программ*

#### CUPS останавливается

Существует вероятность, что для правильной работы в обновленной версии понадобится новый файл конфигурации. Например, получение сообщения "404 - page not found" при попытке входа в панель управления CUPS через localhost:631.

Для того, чтобы воспользоваться новым конфигом, скопируйте `/etc/cups/cupsd.conf.default` в `/etc/cups/cupsd.conf` (при необходимости сделайте резервную копию старого конфига):

```
# cp /etc/cups/cupsd.conf.default /etc/cups/cupsd.conf

```

и, чтобы новые настройки вступили в силу, перезапустите CUPS.

#### Для всех заданий - "остановлено" ("stopped")

Если для всех отправленных на печать заданий установился статус "остановлено" ("stopped"), - удалите принтер и установите его заново. Для этого войдите в [веб-интерфейс CUPS](http://localhost:631), перейдите Принтеры > Удалить Принтер.

Для проверки настроек принтера перейдите во вкладку *Принтеры*, затем *Администрирование*. В выпадающем списке кликните 'Изменить принтер', перейдите к следующей странице (ам), и так далее.

#### Для всех заданий - "Принтер не отвечает" ("The printer is not responding")

Для сетевых принтеров, поскольку CUPS подключается через URI, необходимо убедиться, что в DNS настроен доступ к принтерам по IP. Например, если принтер подключен следующим образом:

```
lpd://BRN_020554/BINARY_P1

```

то имени хоста 'BRN_020554' должны соответствовать IP принтеров, управляемых сервером CUPS.

#### Версия PPD не совместима с gutenprint

Запустите:

```
# /usr/sbin/cups-genppdupdate

```

И перезагрузите CUPS (будет выведено соответствующее сообщение после установки gutenprint).

### USB-принтеры под CUPS 1.4.x

Новый CUPS 1.4.x принес множество изменений:

#### Занесение в черный список usblp

Теперь CUPS, вместо генерирования устройств /dev/usb/lpX с помощью usblp, использует устройства libusb и USB-принтеры (из /dev/bus/usb/). Для того, чтобы заработали USB-принтеры - необходимо выключить модуль usblp. Выключить можно либо добавив в `/etc/modprobe.d/modprobe.conf`:

 `/etc/modprobe.d/modprobe.conf`  `blacklist usblp` 

либо создав в `/etc/modprobe.d/` свой файл, например `usblp_blacklist.conf`, со следующим содержимым:

 `/etc/modprobe.d/usblp_blacklist.conf`  `blacklist usblp` 

Некоторым пользователям, возможно, прийдется переустановить принтер.

#### Определение устройства

В дополнение к отключению загрузки usblp, CUPS могут понадобится права на файл устройства USB-принтера - root:lp, и должны быть 660\. Например.

```
$ ls -l /dev/bus/usb/003/002
crw-rw---- 1 root lp 189, 257 20\. Okt 10:32 /dev/bus/usb/003/002

```

Этого можно добиться добавлением двумя правилами udev в `/lib/udev/rules.d/50-udev-default.rules`:

```
# hplip and cups 1.4+ use raw USB devices, so permissions should be similar to
# the ones from the old usblp kernel module
SUBSYSTEM=="usb", ENV{DEVTYPE}=="usb_device", ENV{ID_USB_INTERFACES}=="", IMPORT{program}="usb_id --export %p"
SUBSYSTEM=="usb", ENV{DEVTYPE}=="usb_device", ENV{ID_USB_INTERFACES}==":0701*:", GROUP="lp", MODE="660"

```

Тем не менее, для некоторых устройств, например, многофункциональных устройств принтер/сканер, эти правила либо не используются, либо перекрываются правилами пакета 'sane'. В этом случае нужно будет добавлять пользовательские правила udev. Смотри далее.

##### Устранение неполадок при определении устройств

Узнаем файл устройства принтера и права доступа к нему:

```
$ lsusb
...
Bus 003 Device 002: ID 04b8:0841 Seiko Epson Corp.
$ ls -l /dev/bus/usb/003/002
crw-rw---- 1 root lp 189, 257 20\. Okt 10:32 /dev/bus/usb/003/002

```

Если права доступа не root:lp 660, придется создать пользовательское правило [udev](/index.php/Udev "Udev") для этого устройства, пример

 `cat /etc/udev/rules.d/10-usbprinter.rules`  `ATTR{idVendor}=="04b8", ATTR{idProduct}=="0841", MODE:="0660", GROUP:="lp"` 

Для многофункциональных устройств (принтер+сканер), для того, чтоб [SANE](/index.php/SANE "SANE") определил его корректно:

 `cat /etc/udev/rules.d/10-usbprinter.rules`  `ATTR{idVendor}=="04b8", ATTR{idProduct}=="0841", MODE:="0660", GROUP:="lp", ENV{libsane_matched}:="yes"` 

Обратите внимание:

*   `idVendor` и `idProduct` взяты из вывода команды `lsusb` показанного выше.
*   некоторым принтерам понадобятся права доступа `666`.

##### Загрузка прошивки (firmware)

Для некоторых принтеров и драйверов понадобится загрузка прошивки принтера (таким как, использующие foo2zjs, принтеры HP LaserJet 10xx) и сделать это будет нужно путем записи прямо на устройство lp, такие функциональные возможности предоставляет usblp. Для обхода этого ограничения нужно будет загрузить модуль usblp при загрузке прошивки, а затем, для нормальной работы CUPS, удалить модуль. Для ручной загрузки модуля выполните

```
$ modprobe usblp

```

загрузка прошивки, затем:

```
$ rmmod usblp

```

Также можно обойтись без добавления usblp в черный список, добавьте "rmmod usblp" в `/etc/rc.local`, при этом прошивка будет загружена при старте системы, а затем, при чтении `rc.local`, модуль usblp будет выгружен.

В случае если принтер окажется подключенным или на нем будет включено питание уже на работающей системе - файл `/etc/rc.local` не будет использован и модуль usblp останется подгруженным. Обойти это можно изменив `/etc/udev/rules.d/11-hpj10xx.rules`, созданный для foo2zjs, таким образом чтоб при добавлении устройства выполнялось нужное событие, например: 15 секунд для загрузки прошивки и автоматического удаления usblp. Следующий пример для HP LaserJet 1018\. Для других моделей значения ATTRS{idProduct} должны быть изменены, соответственно модели принтера.

Найдите в `/etc/udev/rules.d/11-hpj10xx.rules` строку соответствующую вашему принтеру:

```
ACTION=="add", KERNEL=="lp*", SUBSYSTEM=="usb", ATTRS{idVendor}=="03f0",     \
       ATTRS{idProduct}=="4117", RUN+="/sbin/foo2zjs-loadfw 1018 $tempnode"

```

Добавьте после нее следующие строки, при этом убедитесь, что соответствуют IDs продукта и производителя:

```
ACTION=="add", KERNEL=="lp*", SUBSYSTEM=="usb", ATTRS{idVendor}=="03f0",     \
       ATTRS{idProduct}=="4117", RUN+="/usr/bin/sleep 15"
ACTION=="add", KERNEL=="lp*", SUBSYSTEM=="usb", ATTRS{idVendor}=="03f0",     \
       ATTRS{idProduct}=="4117", RUN+="/usr/bin/rmmod usblp"

```

### Остальное

##### Устранение ошибок CUPS

*   Пользователям, регулярно получающим ошибки вида 'NT_STATUS_ACCESS_DENIED' (Windows-клиенты), следует слегка изменить синтаксис:

```
smb://workgroup/username:password@hostname/printer_name

```

*   Иногда, блочные устройства могут иметь не правильные права:

```
# ls /dev/usb/
lp0
# chgrp lp /dev/usb/lp0

```

#### Принтер HPLIP выдает ошибку "/usr/lib/cups/backend/hp failed"

Убедитесь, что dbus установлен и запущен, для этого или проверьте секцию DAEMONS в `/etc/rc.conf`, или выполните `ls /var/run/daemons`.

Если демон dbus запущен, но ошибка все равно повторяется - нужен avahi-daemon.

**Примечание:** возможно понадобиться решить вопрос с правами. Более подробно можно прочесть здесь: [Определение устройства](#.D0.9E.D0.BF.D1.80.D0.B5.D0.B4.D0.B5.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D1.83.D1.81.D1.82.D1.80.D0.BE.D0.B9.D1.81.D1.82.D0.B2.D0.B0).

#### Настройка HPLIP выполнена, но принтер не работает

Данная проблема возникает при использовании драйвера hpijs (устарел) (напр. для серии Deskjet D1600). Вместо него, при добавлении принтера, выбирайте драйвер hpcups.

#### hp-toolbox выдает ошибку "Unable to communicate with device" ("Невозможно соединиться с устройством")

Если в результате запуска hp-toolbox от обычного пользователя получаете сообщение:

```
# hp-toolbox
# error: Unable to communicate with device (code=12): hp:/usb/<printer id>

```

или, "`Unable to communicate with device"`", значит следует добавить пользователя в группу lp, для этого выполните следующую команду:

```
# gpasswd -a <username> lp

```

#### CUPS с принтером HP возвращает '"foomatic-rip" not available/stopped with status 3' ('"foomatic-rip" не используется/остановлен со статусом 3')

Если, во время использования принтера HP, задания появляются в очереди, но все завершаются со статусом 'stopped', а в `/var/log/cups/error_log` возникает одно из следующих сообщений об ошибках:

```
Filter "foomatic-rip" for printer "<printer_name>" not available: No such file or director

```

или:

```
PID 5771 (/usr/lib/cups/filter/foomatic-rip) stopped with status 3!

```

Убедитесь, что установлен **hplip**, также может понадобится пакет **net-snmp**. Прочитайте [эти сообщения на форуме](https://bbs.archlinux.org/viewtopic.php?id=65615).

```
# pacman -S hplip

```

#### Завершение печати из-за ошибок авторизации

Если пользователь уже добавлен в группу lp, и ему разрешена печать (настраивается в `cupsd.conf`), то проблему следует искать в файле `/etc/cups/printers.conf`. Проблема может заключаться в следующей строке:

```
AuthInfoRequired negotiate

```

Закомментируйте ее и перезапустите CUPS.

#### Неактивна кнопка Печать в диалогах приложений GNOME

	*<small>Источник: [I can't print from gnome applications. - Arch Forums](https://bbs.archlinux.org/viewtopic.php?id=70418)</small>*

Убедитесь, что установлен пакет: **libgnomeprint**

Отредактируйте `/etc/cups/cupsd.conf` добавив в него

```
# HostNameLookups Double

```

Перезапустите CUPS:

```
# /etc/rc.d/cupsd restart

```

#### Не найдена поддержка формата: application/postscript

Закомментируйте строки:

```
application/octet-stream        application/vnd.cups-raw        0      -

```

в `/etc/cups/mime.convs`, и:

```
application/octet-stream

```

в `/etc/cups/mime.types`.

#### Определение URIs для Windows Print Servers

Иногда Windows предоставляет не полную информацию об URI (расположение устройств). Если в CUPS возникли проблемы с указанием местоположения устройств - необходимо выполнить команду получения списка всех ресурсов, которые доступны данному windows-пользователю:

```
$ smbtree -U *windowsusername*

```

Если [Samba](/index.php/Samba_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Samba (Русский)") работает и настроена правильно, то будут отображены все, доступные выбранному Windows-пользователю, ресурсы локальной сети. Команда должна отобразить что-то, типа этого:

```
 WORKGROUP
	\\REGULATOR-PC   		
		\\REGULATOR-PC\Z              	
		\\REGULATOR-PC\Public         	
		\\REGULATOR-PC\print$         	Printer Drivers
		\\REGULATOR-PC\G              	
		\\REGULATOR-PC\EPSON Stylus CX8400 Series	EPSON Stylus CX8400 Series
```

Нам понадобится первая часть последней строки -ресурс соответствующий описанию принтера. Таким образом, для получения возможности печатать на принтере EPSON Stylus, в качестве URI в CUPS следует ввести:

```
smb://username:password@REGULATOR-PC/EPSON Stylus CX8400 Series

```

Обратите внимание на то, что в URI допускаются пробелы, а знаки "\\" следует заменять на "//".

#### Ошибка задания для печати client-error-document-format-not-supported

Нужно установить пакет foomatic и использовать драйвер foomatic.

#### Не работает /usr/lib/cups/backend/hp

В `/etc/cups/cupsd.conf` замените:

```
 SystemGroup sys root

```

на

```
 SystemGroup lp root

```

#### Принтер Samsung не печатает некоторые документы

Бывает, что принтер Samsung прекрасно работает с `cups`, но не печатает некоторые документы (файлы Inkscape с текстом) и даже сбоит. В качестве решения можно посоветовать использовать пакет [cups-usblp](https://aur.archlinux.org/packages/cups-usblp/) с добавлением модуля `usblp` в черный список (как было описано ранее).

#### Не отображается локальный USB-принтер

Если ваш usb-принтер не отображается - попробуйте заменить [cups](https://www.archlinux.org/packages/?name=cups) на [cups-usblp](https://aur.archlinux.org/packages/cups-usblp/) (пакет можно найти в [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)")). Затем проверьте работоспособность сначала с загруженным модулем `usblp`, а затем, если не поможет, - с добавленным в черный список.

#### "Не удается получить список драйверов для принтеров"

Попробуйте удалить драйверы Foomatic.

# Приложение

### Альтернативные интерфейсы CUPS

В среде [GNOME](/index.php/GNOME_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GNOME (Русский)"), вы можете конфингурировать ваш принтер с помощью system-config-printer-gnome. С помощью pacman можно установить этот пакет:

```
# pacman -S system-config-printer-gnome

```

Для нормальной работы system-config-printer понадобиться или запуск с правами администратора, или, если от обычного пользователя, то такому пользователю должно быть разрешено администрировать CUPS (если это так - **выполните шаги 1-3**)

*   1\. Создайте группу и внесите в нее нужного пользователя:

```
# groupadd lpadmin
# usermod -aG lpadmin <username>

```

*   2\. Добавьте "lpadmin" (без кавычек) в следующую строку файла `/etc/cups/cups-files.conf`

```
SystemGroup sys root <insert here>

```

*   3\. Перезапустите cups, выйдите и снова войдите в систему (или перезагрузите компьютер)

 `# rc.d restart cupsd` 

Пользователи [KDE](/index.php/KDE "KDE") могут изменять настройки из "Control Center" (kcontrol). Для получения дополнительной информации, обратитесь к документации вашего рабочего окружения (DE).

Также в [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)") можно найти пакет [gtklp](https://aur.archlinux.org/packages.php?ID=43505)

### Виртуальный PDF-принтер

Существует прекрасный пакет - CUPS-PDF. Этот пакет позволяет настроить виртуальный принтер, генерирующий PDF-файлы из того, что отправлено на печать на этот принтер. Возможно этот пакет вам и не понадобится, но иногда он может быть очень полезен.

Созданные PDF-документы можно найти в `var/spool/cups-pdf`. Обычно, более удобно такие документы добавлять в домашнюю директорию пользователя. Настроить такое поведение несложно. В файле /etc/cups/cups-pdf.conf найдите и строку:

```
#Out /var/spool/cups-pdf/${USER}

```

и приведите ее к такому виду:

```
Out /home/${USER}

```

Установить этот пакет можно командой:

```
# pacman -S cups-pdf

```

После установки пакета, настройте PDF-принтер аналогично обычному принтеру, например с помощью веб-интерфейса. В Device (Оборудование) выберите - **CUPS-PDF (Virtual PDF Printer)**; Make/Manufacturer (Марка/Производитель) выберите - **Generic**; Model/Driver (Модель/Драйвер) выберите - **Generic postscript color printer** или **Generic Cups-PDF Printer**. В качестве альтернативы, [по этой ссылке](http://www.physik.uni-wuerzburg.de/~vrbehr/cups-pdf/cups-pdf-CURRENT/extra/CUPS-PDF.ppd) можно найти другой PPD-файл.

#### Печать в postscript: тонкости использования виртуального CUPS-PDF-принтера

Для большинства приложений, таких как OpenOffice, печать в PDF не является проблемой; достаточно просто нажать кнопку. Для печати в postscript, потребуется выполнить небольшой дополнительный объем работ. CUPS-PDF (Виртуальный PDF-принтер) на самом деле создает postscript-файл, а затем уже с помощью утилиты ps2pdf, преобразовывает его в PDF. Для печати в postscript, необходимо сначала передать созданные CUPS-PDF postscript-файлы. Для этого в диалоге печати нужно выбрать вариант "print to file" ("печатать в файл"). (выберите расширение для файла или .ps, или .eps). После того, как будет отмечен флажок "print to file" ("печатать в файл"), введите имя файла и нажмите "print" ("печать").

##### Настройка виртуального CUPS-PDF-принтера

1.  Прочтите инструкция по настройке демона cups.
2.  Установите [cups-pdf](https://www.archlinux.org/packages/?name=cups-pdf) из [extra].
3.  Запустите менеджер печати cups: [http://localhost:631](http://localhost:631) и выберите:

```
Administration -> Add Printer
Select CUPS-PDF (Virtual PDF), выберите марку и модель:
Make:	Generic
Driver:	Generic CUPS-PDF Printer

```

Теперь, для печати в postscript, в диалоговом окне печати установите "CUPS-PDF" в качестве принтера, установите флажок на "print to file" ("печатать в файл"), нажмите печать, введите имя_файла.ps и кликните сохранить. Метод удобен при обработке факсов и т.д...

### Другие источники драйверов для принтеров

[Turboprint](http://www.turboprint.de/english.html) - проприетарный драйвер для многих моделей принтеров, которые до сих пор не поддерживаются в GNU/Linux (например Canon i*). Единственная проблема в том, что высококачественная печать будет либо с водяным знаком, либо за отдельную плату...

# Дополнение

Список вебсайтов, которые могут быть вам полезны:

*   **Official CUPS documentation on your computer** [http://localhost:631/documentation.html](http://localhost:631/documentation.html)
*   **Official CUPS Website** - [http://www.cups.org/](http://www.cups.org/)
*   **Linux Printing** - [http://www.linuxprinting.org/](http://www.linuxprinting.org/)
*   **Tips and Suggestions on common CUPS problems** - [http://home.nyc.rr.com/computertaijutsu/cups.html](http://home.nyc.rr.com/computertaijutsu/cups.html)
*   **Gentoo's Printing Guide** - [http://www.gentoo.org/doc/en/printing-howto.xml](http://www.gentoo.org/doc/en/printing-howto.xml)
*   **Arch Linux User Forums** - [https://bbs.archlinux.org/](https://bbs.archlinux.org/)

## Особые случаи

Дальнейшее описание посвящено специфическим проблемам и их решениям. Если вы сталкивались с какой-либо *необычной* работой принтера, пожалуйста, поместите решение проблемы здесь.

### Принтеры с параллельным портом HP (hplip)

**Примечание:** Действия проводились для настройки HP LaserJet 6L

Если HP принтер подключен через параллельный порт, то потребуется пересобрать пакет **hplip** с опцией **--enable-pp-build**. Для этого устанавливаем и обновляем ABS:

```
# pacman -S abs
# abs

```

Копируем необходимые файлы для сборки

```
# cp -r /var/abs/extra/hplip /tmp

```

Правим файл `/tmp/hplip/PKGBUILD` и добавляем опцию **--enable-pp-build** для **./configure**:

```
[...]
./configure --prefix=/usr \
            --enable-qt4 \
            --enable-pp-build \
            --enable-foomatic-rip-hplip-install \
            --enable-foomatic-ppd-install \
            --enable-hpcups-install \
            --enable-cups-drv-install \
            --enable-hpijs-install \
            --enable-foomatic-drv-install \
            --enable-udev-acl-rules
[...]

```

Собираем и ставим пакет:

```
cd /tmp/hplip
makepkg -s
pacman -U hplip-3.10.6-1-i686.pkg.tar.xz

```

Далее принтер настраивается обычным путем через web-интерфейс **CUPS** [http://localhost:631](http://localhost:631).

Если принтер правильно настроен для работы с **hplip**, то строка подключения в **CUPS** будет начинаться с **hp:**

```
hp:/par/HP_LaserJet_6L?device=/dev/parport0

```

**Примечание:** Действия проводились для настройки HP LaserJet 5L, x86_64

Устанавливаем hplip (пересобирать пакет не надо, он уже собран с --enable-pp-build)

```
# pacman -S hplip

```

Далее запускаем

```
# hp-setup -i -a -x /dev/parport0

```

для автоматического добавления принтера в CUPS, либо добавляем "ручками" через веб-интерфейс [http://localhost:631](http://localhost:631).

### Печать не работает/прерывается на принтерах HP Deskjet 700

Проблема решается установкой фильтра pnm2ppa для принтеров HP Deskjet 700 series. Без этого задания на печать будут отменяться системой. [PKGBUILD](/index.php/Arch_Build_System_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch Build System (Русский)") для pnm2ppa можно найти здесь: [AUR](https://aur.archlinux.org/index.php?setlang=ru).

### Заставить работать HP LaserJet 1010

Мне для этого пришлось самому собрать ghostscript, потому что gs ESP в репозитории был версии 7.07 и имел некоторые ошибки, исправленные в ESP 8.15.1\. Я никогда не пользовался пакетом 'foomatic' из репозитория. Я думаю что этот пакет устарел.

```
$ pacman -Qs cups a2ps psutils foo ghost
local/cups 1.1.23-3
    The CUPS Printing System
local/a2ps 4.13b-3
    a2ps is an Any to PostScript filter
local/psutils p17-3
    A set of postscript utilities.
local/foomatic-db 3.0.2-1
    Foomatic is a system for using free software printer drivers with common
    spoolers on Unix
local/foomatic-db-engine 3.0.2-1
    Foomatic is a system for using free software printer drivers with common
    spoolers on Unix
local/foomatic-db-ppd 3.0.2-1
    Foomatic is a system for using free software printer drivers with common
    spoolers on Unix
local/foomatic-filters 3.0.2-1
    Foomatic is a system for using free software printer drivers with common
    spoolers on Unix
local/espgs 8.15.1-1
    ESP Ghostscript

```

Также я был вынужден выставить LogLevel в /etc/cups/cupsd.conf в debug2 для того чтобы обнаружить отсутствие некоторых шрифтов "Nimbus". Затем я переименовал их и положил туда, куда мне подсказывал лог. Тут нужно привести хитрый способ поиска в google, [например](http://www.google.com/search?q=n019003l+filetype%3Apfb) т.к. шрифты являются проприетарными (уверен что в windows это по умолчанию). В любом случае, после скачивания шрифтов (около 7) и помещения их в правильную директорию печать заработала.

До этого я получал ошибки описанные [здесь](http://linuxprinting.org/show_printer.cgi?recnum=HP-LaserJet_1010): 'Unsupport PCL' и т.п...

Уверен что это работало бы и с gs ESP 7.07 (в репозитории) если бы у меня раньше хватило ума включить DebugLevel2 :-/

*Обновление:* да, это работает... может быть эта информация окажется полезной для кого-либо ещё... извините за неудобства.

### Заставить работать HP LaserJet 1020 (1018 и похожие)

После множества попыток связанных с hplib и gutenprint я наконец нашёл решение как заставить мой HP Laserjet 1020 печатать.

Первым делом вам надо уставить cups и ghostscript. Затем пройдите по ссылке [http://www.linuxprinting.org/show_printer.cgi?recnum=HP-LaserJet_1020](http://www.linuxprinting.org/show_printer.cgi?recnum=HP-LaserJet_1020) на страницу драйверов печати [http://foo2zjs.rkkda.com/](http://foo2zjs.rkkda.com/) и следуйте интрукциям по установке. Залогиньтесь как root. После скачивания и распаковки архива переместитесь в распакованную директорию foo2zjs. Теперь вы можете делать всё по оригинальной инструкции по установке, лишь с небольшой модификацией для изменения userid пользователя для печати:

```
 $ make
 $ ./getweb 1020

```

Откройте *Makefile*

 `$ nano Makefile` 

найдите там строку

 `# LPuid=-olp` 

и модифицируйте её таки образом:

 `# LPuid=-oroot` 

дальше выполняйте сборку

```
 $ make install
 $ make install-hotplug
 $ make cups

```

Сейчас в этих действиях нет необходимости. Теперь строка **LPuid=-oroot** стоит по умолчанию.

Вы также можете взять пакет foo2zjs из [AUR](https://aur.archlinux.org/index.php?setlang=ru) и модифицировать [PKGBUILD](/index.php/Arch_Build_System_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch Build System (Русский)"): измените строку

 `./getweb all` 

на

 `./getweb 1020` 

(или, если устанавливаете другой принтер, измените эту строку на что, что вам нужно).

Последним шагом является добавление и конфигурирование принтера в CUPS manager. Принтер должен определиться автоматически. Это отлично работает для root'а и всех ползователей. Когда ОС загружается, принтер инициализируется и сигнализирует о том, что он работает. Так же строку

 `./getweb 1020` 

можно изменять на необходимые 1018 (для работы принтера Hewlett-Packard 1018) и т.д.

 `./getweb 1018` 

Список поддерживаемы моделей тут: [http://foo2zjs.rkkda.com/](http://foo2zjs.rkkda.com/)

#### HPLIP

Больше нет необходимости устанавливать драйвер foo2zjs для работы принтера HP LJ 1018/1020, поскольку в последних версиях hplip он работает "из коробки". Вам следует установить hplip, gnomesu или gksu, qt и pyqt4, после чего запустить

 `sudo hp-setup` 

CUPS-сервер должен быть запущен. Мастер установки hplip автоматически установит ваш принтер. После следует установить плагин к принтеру. Для этого запустить от пользователя программу hp-toolbox и выберите "install required plugin". Плагин автоматически загрузится с сайта производителя. Никаких дополнительных действий (вроде внесения usblp и MODULES_BLACKLIST) выполнять не надо.

### Выполнение сервисных операций на принтерах Epson

#### Escputil

Здесь объясняется как выполнить некоторые вспомогательные операции, такие как очистка и проверка сопел на принтерах Epson. Для этого мы будем использовать утилиту escputil, которая входит в состав пакета gutenprint.

Man-страница этой утилиты ("man escputil") содержит очень полезную информацию, но не включает в себя необходимых сведений о том как идентифицировать ваш принтер. Для этого могут быть использованы два параметра. Первый из них --printer; он принимает имя принтера, которое вы использовали при его конфигурировании. Другой &mdash --raw-device. Эта опция примаетпуть к устройству. Если ваш принтер подключен к последовательному порту, то устройство будет выглядеть примерно как "/dev/lp0". Если же ваш принтер подключен к USB, по устройство будет "/dev/usb/lp0". Если у вас более одного принтера они будут иметь имена файлов устройств "lp1", "lp2" и т.д.

*   очистка печатающей головки:

 `escputil -u --clean-head` 

*   проверка сопел:

 `escputil -u --nozzle-check` 

Если вам необходимо произвести операцию, которая требует двухстороннего общения с принтером вы должны использовать спецификацию "--raw-device", а ваш пользователь должен состоять в группе "lp" или быть root'ом.

*   получение внутреннего имени принтера:

```
  sudo escputil --raw-device=/dev/usb/lp0 --identify

```

*   получение уровня чернил:

```
  sudo escputil --raw-device=/dev/usb/lp0 --ink-level

```

#### Mtink

Это монитор состояния принтера, который позволяет получить количество оставшихся чернил, печатать тестовые страницы, сбрасывать принтер и очищать сопла. Он использует интуитивный графический интерфейс пользователя. Пакет можно скачать [отсюда](https://aur.archlinux.org/packages.php?ID=476).

# См. также

*   [Официальная документация CUPS documentation](http://localhost:631/documentation.html), *локальная установка*
*   [Официальный Веб-сайт CUPS](http://www.cups.org/)
*   [Linux Printing](http://www.linuxprinting.org/), *[Linux Foundation](http://www.linuxfoundation.org)*
*   [Руководство по печати в Gentoo](http://www.gentoo.org/doc/en/printing-howto.xml), *[Источники Документации Gentoo](http://www.gentoo.org/doc/en)*
*   [Форум пользователей Arch Linux](https://bbs.archlinux.org/)

*   [Простая установка принтеров HP](http://wiki.gotux.net/config/hp-printer)