В этой статье описывается, как подключить и произвести первичную настройку 4G модема Huawei E3276 в Arch Linux. Инструкция написана для модема от оператора МегаФон. С этой инструкцией вы сможете настроить подключение к сети для дальнейшей установки Arch Linux.

## Contents

*   [1 Подготовка](#.D0.9F.D0.BE.D0.B4.D0.B3.D0.BE.D1.82.D0.BE.D0.B2.D0.BA.D0.B0)
    *   [1.1 Информация о режимах модема](#.D0.98.D0.BD.D1.84.D0.BE.D1.80.D0.BC.D0.B0.D1.86.D0.B8.D1.8F_.D0.BE_.D1.80.D0.B5.D0.B6.D0.B8.D0.BC.D0.B0.D1.85_.D0.BC.D0.BE.D0.B4.D0.B5.D0.BC.D0.B0)
    *   [1.2 Установка и настройка необходимого ПО](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.B8_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D0.BD.D0.B5.D0.BE.D0.B1.D1.85.D0.BE.D0.B4.D0.B8.D0.BC.D0.BE.D0.B3.D0.BE_.D0.9F.D0.9E)
        *   [1.2.1 Linux](#Linux)
        *   [1.2.2 Windows](#Windows)
*   [2 Переключение режима модема](#.D0.9F.D0.B5.D1.80.D0.B5.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D1.80.D0.B5.D0.B6.D0.B8.D0.BC.D0.B0_.D0.BC.D0.BE.D0.B4.D0.B5.D0.BC.D0.B0)
    *   [2.1 Завершение работы программы](#.D0.97.D0.B0.D0.B2.D0.B5.D1.80.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D1.8B_.D0.BF.D1.80.D0.BE.D0.B3.D1.80.D0.B0.D0.BC.D0.BC.D1.8B)
*   [3 Настройка сети](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D1.81.D0.B5.D1.82.D0.B8)
    *   [3.1 Автоподключение](#.D0.90.D0.B2.D1.82.D0.BE.D0.BF.D0.BE.D0.B4.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5)

## Подготовка

### Информация о режимах модема

Для того, чтобы система корректно распознавала модем, необходимо переключить режим модема, оставив включенными только два порта: PCUI и

модемный. В этом случае вы больше не сможете пользоваться другими встроенными функциями модема, например карт-ридером. До того как

производить нижеследующие операции, рекомендуется скопировать на компьютер ПО модема, оно может вам пригодится при работе с модемом на

операционной системе Windows.

**Примечание:** Необходимо отключить проверку PIN кода на сим-карте.

### Установка и настройка необходимого ПО

#### Linux

*   Установите [minicom](https://www.archlinux.org/packages/?name=minicom). Посмотрите все подключенные устройства следующей командой:

```
$ ls /dev/tty*

```

Если к другим USB-портам вашей машины ничего не подключено, помимо всего остального, в конце списка у вас должны определиться два

устройства: **ttyUSB0** и **ttyUSB1**.

*   Запустите minicom следующей командой:

```
$ minicom --device=/dev/ttyUSB0

```

**Примечание:** **/dev/ttyUSB0** в данном случае — это имя девайса, к которому будет обращаться демон ppp. Имя может отличаться.

#### Windows

*   Отключите модем от сети, закройте ПО, использующее модем.
*   Скачайте и запустите бесплатную программу [DC-unlocker](https://www.dc-unlocker.com).
*   Нажмите **Определить модем** (иконка в виде лупы).

## Переключение режима модема

*   После того, как вы подключились к модему, попробуйте ввести следующую команду, не обращая внимания на входящие сообщения:

```
ATE

```

*   Если все хорошо, отключите входящие сообщения следующей командой:

```
AT^CURC=0

```

*   Переключите, наконец, режим модема:

```
AT^SETPORT="FF;10,12"

```

### Завершение работы программы

**Linux:** Завершите работу minicom последовательным нажатием «Ctrl+A» и «Q».
**Windows:** Просто закройте окно программы.
**Извлеките модем и вставьте обратно.**

## Настройка сети

*   Создайте файл **/etc/ppp/options-mobile** со следующим содержимым:

```
/dev/ttyUSB0
921600
defaultroute
usepeerdns
crtscts
lock
noauth
local
persist
modem
nopcomp
novjccomp
nobsdcomp
nodeflate
noaccomp
ipcp-accept-local
ipcp-accept-remote
noipdefault

```

*   Создайте файл **/etc/ppp/peers/megafon** и пропишите в нем следующее:

```
file /etc/ppp/options-mobile
connect "/usr/sbin/chat -v -t15 -f /etc/ppp/chatscripts/megafon.chat"

```

*   Создайте папку **/etc/ppp/chatscripts**, а в нем файл **megafon.chat**. Пропишите в него:

```
ABORT 'NO CARRIER'
REPORT CONNECT
TIMEOUT 6
'' 'AT'
'OK' 'AT+CGDCONT=1,"IP","internet"'
'OK' 'ATD*99*1#'
TIMEOUT 30
CONNECT

```

Готово, теперь вы можете подключиться к интернету, используя следующую команду:

```
sudo pon megafon

```

И отключиться, введя:

```
sudo poff megafon

```

### Автоподключение

Чтобы сеть поднималась автоматически при старте системы, необходимо включить соответствующий юнит:

```
systemctl enable ppp@megafon.service

```