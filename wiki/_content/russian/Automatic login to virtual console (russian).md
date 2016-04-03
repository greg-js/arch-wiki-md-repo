В этой статье описывается автоматический вход в [virtual console](https://en.wikipedia.org/wiki/Virtual_console "wikipedia:Virtual console") в конце процесса загрузки ([boot process](/index.php/Boot_process "Boot process")). Для автоматической загрузки Х смотрите [Запуск X при входе](/index.php/%D0%97%D0%B0%D0%BF%D1%83%D1%81%D0%BA_X_%D0%BF%D1%80%D0%B8_%D0%B2%D1%85%D0%BE%D0%B4%D0%B5 "Запуск X при входе").

## Contents

*   [1 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [1.1 Виртуальная консоль](#.D0.92.D0.B8.D1.80.D1.82.D1.83.D0.B0.D0.BB.D1.8C.D0.BD.D0.B0.D1.8F_.D0.BA.D0.BE.D0.BD.D1.81.D0.BE.D0.BB.D1.8C)
    *   [1.2 Последовательная консоль](#.D0.9F.D0.BE.D1.81.D0.BB.D0.B5.D0.B4.D0.BE.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D0.B0.D1.8F_.D0.BA.D0.BE.D0.BD.D1.81.D0.BE.D0.BB.D1.8C)
*   [2 Смотри также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Настройка

Конфигурация зависит от параметров systemd см: [редактирование предоставленных пакетами файлов юнитов](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A0.D0.B5.D0.B4.D0.B0.D0.BA.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.B5.D0.B4.D0.BE.D1.81.D1.82.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.BD.D1.8B.D1.85_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.B0.D0.BC.D0.B8_.D1.84.D0.B0.D0.B9.D0.BB.D0.BE.D0.B2_.D1.8E.D0.BD.D0.B8.D1.82.D0.BE.D0.B2 "Systemd (Русский)") определяющих настройки по умолчанию, передавемые *agetty*.

Настройки для виртуальной и последовательной консолей отличаются. В большинстве случаев вам необходим автологин в виртуальную консоль, (с именами устройств `tty*N*`, где `*N*` номер). Для последовательной консоли имена устройств `ttyS*N*`, где `*N*` номер.

### Виртуальная консоль

Создайте следующий файл (и промежуточные каталоги):

 `/etc/systemd/system/getty@tty1.service.d/override.conf` 
```
[Service]
ExecStart=
ExecStart=-/usr/bin/agetty --autologin *username* --noclear %I 38400 linux
```

**Совет:** Используйте опцию `Type=idle` для задержки и ожидания запуска всех необходимых служб. Или используйте `Type=simple`, для немедленного запуска сервиса, но сообщения при загрузке могут засорять строку входа. Эта опция полезна при [starting X automatically](/index.php/Start_X_at_Login_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Start X at Login (Русский)"). Для этого добавьте `Type=simple` в `autologin.conf`.

Если вы хотите использовать *tty* отличный от *tty1*, смотрите [systemd FAQ](/index.php/Systemd_FAQ#How_do_I_change_the_default_number_of_gettys.3F "Systemd FAQ").

### Последовательная консоль

Создайте следующий файл (и промежуточные каталоги):

 `/etc/systemd/system/serial-getty@ttyS0.service.d/override.conf` 
```
[Service]
ExecStart=
ExecStart=-/usr/bin/agetty --autologin *username* -s %I 115200,38400,9600 vt102
```

## Смотри также

*   [systemd (Русский)#Изменение цели загрузки по умолчанию](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.98.D0.B7.D0.BC.D0.B5.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D1.86.D0.B5.D0.BB.D0.B8_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B8_.D0.BF.D0.BE_.D1.83.D0.BC.D0.BE.D0.BB.D1.87.D0.B0.D0.BD.D0.B8.D1.8E "Systemd (Русский)")