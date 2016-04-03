[Clam AntiVirus](http://www.clamav.net) это антивирусный инструмент для UNIX с открытым исходным кодом (GPL). Он предоставляет несколько утилит, включая гибкий и масштабируемый многопоточный демон (службу), сканер для командной строки и расширенные средства для автоматического обновления баз. Поскольку ClamAV в основном используется на файловых и почтовых серверах в Windows-сетях, он предназначен для обнаружения Windows-вирусов и вредоносного ПО.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Запуск службы](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D1.81.D0.BB.D1.83.D0.B6.D0.B1.D1.8B)
*   [3 Обновление баз](#.D0.9E.D0.B1.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B1.D0.B0.D0.B7)
*   [4 Тестирование](#.D0.A2.D0.B5.D1.81.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5)
*   [5 Сканирование](#.D0.A1.D0.BA.D0.B0.D0.BD.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5)
*   [6 Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [6.1 Error: Clamd was NOT notified](#Error:_Clamd_was_NOT_notified)
    *   [6.2 Error: No supported database files found](#Error:_No_supported_database_files_found)
    *   [6.3 Error: Can't create temporary directory](#Error:_Can.27t_create_temporary_directory)

## Установка

[Установите](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.BE.D0.B2 "Pacman (Русский)") пакет [clamav](https://www.archlinux.org/packages/?name=clamav), доступный в [официальных репозиториях](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)").

## Запуск службы

Смотрите раздел [Systemd:Использование юнитов](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.8E.D0.BD.D0.B8.D1.82.D0.BE.D0.B2 "Systemd (Русский)") для получения информации об управлении службами.

Название службы: `clamd.service`.

## Обновление баз

Антивирусные базы обновляются при помощи команды:

```
# freshclam

```

Файлы баз сохраняются в:

```
/var/lib/clamav/daily.cvd
/var/lib/clamav/main.cvd

```

## Тестирование

Для того, чтобы убедиться что ClamAV и его антивирусные базы корректно установились, просканируйте [тестовый файл EICAR](http://www.eicar.org/86-0-Intended-use.html) (эмуляция вируса, [см. Википедию](https://en.wikipedia.org/wiki/ru:EICAR-Test-File "wikipedia:ru:EICAR-Test-File")):

```
$ wget -O- [http://www.eicar.org/download/eicar.com.txt](http://www.eicar.org/download/eicar.com.txt) | clamscan -

```

В результатах сканирования **должна** быть строка:

```
Eicar-Test-Signature FOUND

```

В противном случае, см. раздел [Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC) или воспользуйтесь [форумом](https://bbs.archlinux.org/).

## Сканирование

Команда `clamscan` используется для проверки отдельных файлов, каталогов или всей системы:

```
$ clamscan myfile
$ clamscan --recursive=yes --infected /home # или используйте параметры -r -i
$ clamscan --recursive=yes --infected --exclude-dir='^/sys|^/proc|^/dev|^/lib|^/bin|^/sbin' /

```

Для автоматического удаления инфицированных файлов добавьте параметр `--remove`, или можете использовать `--move=/директория` для перемещения их в карантин.

При использовании параметра `-l /путь/к/файлу` результаты сканирования будут записываться в указанный log-файл.

## Решение проблем

### Error: Clamd was NOT notified

Если при запуске freshclam вы получаете сообщение:

```
WARNING: Clamd was NOT notified: Cannot connect to clamd through 
/var/lib/clamav/clamd.sock connect(): No such file or directory

```

Создайте отсутствующий sock-файл:

```
# touch /var/lib/clamav/clamd.sock
# chown clamav:clamav /var/lib/clamav/clamd.sock

```

Затем в файле `/etc/clamav/clamd.conf` раскомментируйте стоку:

```
LocalSocket /var/lib/clamav/clamd.sock

```

Сохраните файл и [перезапустите службу](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.8E.D0.BD.D0.B8.D1.82.D0.BE.D0.B2 "Systemd (Русский)")

### Error: No supported database files found

Если при запуске службы вы получаете сообщение:

```
LibClamAV Error: cli_loaddb(): No supported database files found
in /var/lib/clamav ERROR: Not supported data format

```

Создайте базу данных от имени пользователя root:

```
# freshclam -v

```

### Error: Can't create temporary directory

Если вы получили следующую ошибку, содержащую номера UID и GUID:

```
# ERROR: can't create temporary directory
# Hint: The database directory must be writable for UID XXX or GID YYY

```

Установите правильные права на директорию:

```
# chown UID:GID /var/lib/clamav & chmod 755 /var/lib/clamav

```