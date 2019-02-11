**netconsole** это модуль Linux ядра, который отправляет все сообщения журнала ядра (т.е. [dmesg](/index.php/Dmesg "Dmesg")) на удаленный компьютер по сети, без участия пространства пользователя (например, syslogd). Имя "netconsole" является некорректным, т.к. больше похож на удаленный сервис регистрации, нежели на "console".

Он может быть или встроен в ядро или загружен в виде модуля. Встроенный *netconsole* инициализирует сразу после сетевых карт(NIC). Модуль используется в основном для захвата выхода "паники ядра" из зависшей машины, или в других ситуациях, когда пользователь пространство не доступно.

Документация доступна в подкаталоге **[Documentation/networking/netconsole.txt](http://lxr.linux.no/linux+v2.6.32/Documentation/networking/netconsole.txt)**

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Установка](#Установка)
*   [2 Настройка](#Настройка)
*   [3 Динамическая настройка](#Динамическая_настройка)
*   [4 Прием](#Прием)
*   [5 Начальная загрузка с запуском ядра](#Начальная_загрузка_с_запуском_ядра)

## Установка

Установите [gnu-netcat](https://www.archlinux.org/packages/?name=gnu-netcat) из [Official repositories (Русский)](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)").

## Настройка

Опции *Netconsole* и других модулей ядра могут передаваться от загрузчика к ядру при его запуске посредством командной строки ядра, изменяя параметры загрузки. Пример для U-Boot, где первый адрес машины с которого слать, его порт и IP, и 2-й адрес машины куда отправляем логи, его порт, IP-и MAC-адрес:

```
fw_setenv usb_custom_params 'loglevel=7 netconsole=6666@192.168.1.28/eth0,6666@192.168.1.19/00:13:32:20:r9:a5'

```

Ведение журнала в системе осущетвляет *syslog-ng* или иной другой логгер, поэтому доступны уровнях протоколирования (вывод информации) определяется функцией протоколирования сообщений. Можно также передавать параметры *netconsole* в ядро во время выполнения (конфигурационного файла не требуется), затем запустить два экземпляра *netconsole* по мониторингу машин (один на чтение выхода, другой для ввода), и перезапустить его на машине или устройстве, таким образом вы логируетесь с *динамической настройкой*:

```
# set log level for kernel messages
dmesg -n 8

netconsole=6666@192.168.1.28/eth0,6666@192.168.1.19/00:13:32:20:r9:a5

nc -l -u -p 6666 &
nc -u 192.168.1.28 6666

```

Возможно, придется выключить компьютер и маршрутизатор/брандмауэр и настроить перенаправление портов маршрутизатора для мониторинга и приема данных в *netconsole*.

## Динамическая настройка

Netconsole может быть загружен как модуль ядра вручную после загрузки или автоматически при загрузке в зависимости от конфигурации этого модуля. См. [kernel modules (Русский)](/index.php/Kernel_modules_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Kernel modules (Русский)") для настройки загрузки. Для загрузки вручную:

```
# set log level for kernel messages
dmesg -n 8

modprobe configfs
modprobe netconsole
mount none -t configfs /sys/kernel/config

# 'netconsole' dir is auto created if the module is loaded 
mkdir /sys/kernel/config/netconsole/target1
cd /sys/kernel/config/netconsole/target1

# set local IP address
echo 192.168.0.111 > local_ip
# set destination IP address
echo 192.168.0.17 > remote_ip
# set local network device name (find it trough ifconfig, examples: eth0, eno1, wlan0)
echo eno1 > dev_name
# find destination MAC address
arping -I $(cat dev_name) $(cat remote_ip) -f | grep -o ..:..:..:..:..:.. > remote_mac

echo 1 > enabled

```

netconsole теперь должен быть настроен. Чтобы проверить, запустить 'dmesg |tail' и вы должны увидеть "netconsole: network logging started". Проверьте доступные уровни логирования 'dmesg -h'.

## Прием

```
nc -u -l 6666

```

или

```
nc -u -l -p 6666

```

## Начальная загрузка с запуском ядра

Просто добавьте netconsole к строке kernel. Он принимает строку параметров "netconsole" в следующем формате::

```
  netconsole=[src-port]@[src-ip]/[<dev>],[tgt-port]@<tgt-ip>/[tgt-macaddr]
        src-port      source for UDP packets (defaults to 6665)
        src-ip        source IP to use (interface address)
        dev           network interface (eth0)
        tgt-port      port for logging agent (6666)
        tgt-ip        IP address for logging agent
        tgt-macaddr   ethernet MAC address for logging agent (broadcast)
```

Примеры:

```
linux /vmlinuz-linux root=UUID=a322511e-b028-4f11-87b6-e48b5d99bbd8 ro netconsole=514@10.0.0.1/eth1,514@10.0.0.2/12:34:56:78:9a:bc
linux /vmlinuz-linux root=/dev/disk/by-label/ROOT ro netconsole=514@10.0.0.2/12:34:56:78:9a:bc

```

From: [Net Console for Boot Debugging](/index.php/Boot_debugging#Net_Console "Boot debugging").