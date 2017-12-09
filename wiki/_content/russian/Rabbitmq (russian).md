[RabbitMQ](https://www.rabbitmq.com/) - брокер сообщений на основе [AMQP](https://ru.wikipedia.org/wiki/AMQP). Он предоставляет общую платформу для отправки и приёма сообщений и надёжное хранилище необработанных сообщений.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [2.1 Включение MQTT](#.D0.92.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_MQTT)
    *   [2.2 Включение администрации через HTTP](#.D0.92.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B0.D0.B4.D0.BC.D0.B8.D0.BD.D0.B8.D1.81.D1.82.D1.80.D0.B0.D1.86.D0.B8.D0.B8_.D1.87.D0.B5.D1.80.D0.B5.D0.B7_HTTP)
*   [3 Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [3.1 Остановка rabbitmq.service зависает на минуты](#.D0.9E.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_rabbitmq.service_.D0.B7.D0.B0.D0.B2.D0.B8.D1.81.D0.B0.D0.B5.D1.82_.D0.BD.D0.B0_.D0.BC.D0.B8.D0.BD.D1.83.D1.82.D1.8B)
    *   [3.2 Изменение имени хоста](#.D0.98.D0.B7.D0.BC.D0.B5.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B8.D0.BC.D0.B5.D0.BD.D0.B8_.D1.85.D0.BE.D1.81.D1.82.D0.B0)
    *   [3.3 После обновления RabbitMQ до последней версии, он не может запуститься](#.D0.9F.D0.BE.D1.81.D0.BB.D0.B5_.D0.BE.D0.B1.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D1.8F_RabbitMQ_.D0.B4.D0.BE_.D0.BF.D0.BE.D1.81.D0.BB.D0.B5.D0.B4.D0.BD.D0.B5.D0.B9_.D0.B2.D0.B5.D1.80.D1.81.D0.B8.D0.B8.2C_.D0.BE.D0.BD_.D0.BD.D0.B5_.D0.BC.D0.BE.D0.B6.D0.B5.D1.82_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D1.82.D0.B8.D1.82.D1.8C.D1.81.D1.8F)
    *   [3.4 Erlang cookie error](#Erlang_cookie_error)
    *   [3.5 can't establish TCP connection](#can.27t_establish_TCP_connection)
*   [4 Ссылки](#.D0.A1.D1.81.D1.8B.D0.BB.D0.BA.D0.B8)

## Установка

Установите пакет [rabbitmq](https://www.archlinux.org/packages/?name=rabbitmq).

## Настройка

Просто [запустите](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd (Русский)") сервис `rabbitmq`.

По умолчанию файл с настройками располагается в `/etc/rabbitmq/rabbitmq-env.conf`. Больше информации можно найти в [официально документации](https://www.rabbitmq.com/configure.html)

### Включение MQTT

RabbitMQ может работать в роли сервера [MQTT](https://ru.wikipedia.org/wiki/MQTT). Для использования такого функционала необходимо подключение плагина.

```
   sudo -u rabbitmq rabbitmq-plugins enable rabbitmq_mqtt

```

Чтобы изменения вступили в силу, необходимо перезапустить сервис RabbitMQ.

Клиенты должны пройти аутентификацию, прежде чем они смогут писать в темы. RabbitMQ распределяет трафик между виртуальными хостами, вам необходимо использовать `**your_login:virtual_host**` в качесте имени пользователя чтобы аутентифицироваться.

### Включение администрации через HTTP

Чтобы включить Web-консоль администратора выполните:

```
   rabbitmq-plugins enable rabbitmq_management

```

Затем перейдите на `<ip_address_of_host>:15672`. Учётные данные по умолчанию - `guest:guest`

Чтобы разрешеить удалённым машинам подключаться к консоли администратора по HTTP впишите в `/etc/rabbitmq/rabbitmq.config` следующую строку:

```
[{rabbit, [{loopback_users, []}]}].

```

## Решение проблем

### Остановка rabbitmq.service зависает на минуты

Пакет rabbitmq устанавливает зависимость [epmd](https://www.archlinux.org/packages/?name=epmd) (Erlang Port Mapping Daemon). Если вы запустите rabbitmq через systemd, он запустит демон epmd, который не будет остановлен после выполнения команды `systemctl stop rabbitmq`. Для решения, добавьте юнит epmd.service как зависимость `/etc/systemd/system/rabbitmq.service` в секции `Unit`

```
After=epmd.service

```

Не забудьте перезагрузить демоны и сервис `systemctl daemon-reload && systemctl restart rabbitmq`

### Изменение имени хоста

Если после установки rabbitmq, вы изменили сетевое имя машины, сервис не сможет запуститься. Это связано с записью `NODENAME` в `/etc/rabbitmq/rabbitmq-env.conf`. Обновите его:

 `/etc/rabbitmq/rabbitmq-env.conf` 
```
NODENAME=rabbit@new-hostname
...

```

### После обновления RabbitMQ до последней версии, он не может запуститься

Проблема может быть вызвана неверным `NODENAME` в `/etc/rabbitmq/rabbitmq-env.conf`. Вы можете скорректировать `@hostname` так же как в [#Изменение имени хоста](#.D0.98.D0.B7.D0.BC.D0.B5.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B8.D0.BC.D0.B5.D0.BD.D0.B8_.D1.85.D0.BE.D1.81.D1.82.D0.B0).

### Erlang cookie error

Ошибка аутентификации может быть вызвана неверной настройкой HOME для rabbitmq:

```
Authentication failed (rejected by the remote node), please check the Erlang cookie
...
home dir: /root

```

Домашняя директория может быть задана в конфигурационном файле:

 `/etc/rabbitmq/rabbitmq-env.conf` 
```
...
HOME=/var/lib/rabbitmq
...

```

### can't establish TCP connection

Если вы получили эту ошибку, тогда проверьте, что первая строка с вашим хостом в `/etc/hosts` содержит тот же IP-адрес, что и в `/etc/rabbitmq/rabbitmq-env.conf` (эта ошибка часто случается, если вы привязали сервер rabbitmq к определённому интерфейсу).

## Ссылки

[конфигурация ядра erlang](http://erlang.org/doc/man/kernel_app.html) для тонкой настройки

[rabbitmq.config примеры](https://github.com/rabbitmq/rabbitmq-server/blob/master/docs/rabbitmq.config.example), не включены в пакет rabbitmq