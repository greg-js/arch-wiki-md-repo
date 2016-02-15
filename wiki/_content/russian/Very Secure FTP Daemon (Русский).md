vsftpd расшифровывается как «Very Secure FTP Daemon» (очень безопасный FTP демон). Это хороший маленький FTP-сервер.

Он может работать и без xinetd, но я опишу способ использования с xinetd.

Сначала установите необоходимые пакеты с помощью pacman:

```
# pacman -S xinetd vsftpd

```

Следующий файл настроек нуждается в редактировании:

/etc/xinetd.d/vsftpd:

```
service ftp
{
        socket_type             = stream
        wait                    = no
        user                    = root
        server                  = /usr/sbin/vsftpd
        log_on_success  += HOST DURATION
        log_on_failure  += HOST
        disable                 = no
}

```

`/etc/vsftpd.conf` достаточно хорошо документированный конфигурационный файл, но, возможно, по умолчанию вы захотите изменить что либо, например:

```
anonymous_enable=NO      # Запрещает анонимный доступ к FTP-серверу
local_enable=YES         # Пользователи с локальной машины могут заходить
write_enable=YES    # Будьте осторожны, при использовании опции совместно с anonymous_enable=YES

```

Наконец, добавьте xinetd в список демонов в файле /etc/rc.conf. Не надо добавлять туда vsftpd, он будет вызван xinetd, когда это будет необходимо.

Если вы получили ошибку типа:

```
500 OOPS: cap_set_proc

```

при соединении с сервером, вам необходимо добавить _capability_ в список MODULES в /etc/rc.conf.

ВНИМАНИЕ: После апгрейда до версии 2.1.0 вы можете получить сообщение об ошибке типа приведённого ниже, при попытке соединения с сервером:

```
500 OOPS: could not bind listening IPv4 socket

```

В старых версиях этом можно было исправить оставив следующую строчку закоментированной:

```
# Use this to use vsftpd in standalone mode, otherwise it runs through (x)inetd
# listen=YES

```

В новой версии, и возможно в следующих релизах, требуется явно указать в конфигурации, что сервер не работает демоном, а вызывается через (x)inetd. Пример ниже:

```
# Use this to use vsftpd in standalone mode, otherwise it runs through (x)inetd
listen=NO

```